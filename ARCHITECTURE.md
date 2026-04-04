# Azokle Keyboard: Technical Architecture

**Azokle Keyboard**, developed by [Azokle Software](https://azokle.com), is a standalone custom Android keyboard based on the AOSP LatinIME layout variants (forked conceptually via Simple Keyboard). Its purpose is to deliver self-sovereign End-to-End Encryption (E2EE) seamlessly across any text field by leveraging the Android version of the [Signal Protocol](https://mvnrepository.com/artifact/org.signal/libsignal-android).

## Core Philosophy: Serverless Signal Protocol

Typically, Signal Protocol relies on a centralized server infrastructure to securely distribute `PreKeyBundles`. Azokle Keyboard modifies this topology to function entirely peer-to-peer over the user's selected transport layer (i.e. existing messenger apps).

1. **Identity & Storage:** 
   - Instead of linking to a phone number, users are identified via a randomized UUID bound to an arbitrary device ID (`SignalProtocolAddress`).
   - The device initializes an `IdentityKeyStore`, `PreKeyStore`, `SessionStore`, and a `SignedPreKeyStore`.
   - All protocol states are securely serialized into the application’s `SharedPreferences` via Jackson.

2. **Custom Message Payloads:**
   - Instead of network requests, keys are passed via minified JSON arrays directly into the application's text entry point.
   - We utilize four specialized message composites to mimic network exchanges:
      - `PreKeyResponse`: Exchange `PreKeyBundle` (Invite Protocol).
      - `PreKeySignalMessage`: Bootstraps session over the first ciphertext payload.
      - `SignalMessage`: Standard ratcheted ciphertext frame.
      - `PreKeyResponse` + `SignalMessage`: Force KeyBundle refresh to rotate sessions without establishing background sync connections.

---

## Session Establishment

### Key Constraints vs Standard Signal
To minimize payload size (since all parameters route through tiny text fields instead of broadband backend APIs), Azokle Keyboard limits the prekey generation to just **2 one-time prekeys** (down from Signal's standard 100). These are replaced continuously after each consumption. 

### The Handshake View
If Bob and Alice wish to communicate:
1. **Invite**: Alice generates and shares a `PreKeyBundle` via an invite message (`PreKeyResponse`).
2. **Accept**: Bob registers Alice in his localized keyboard contact list. The keyboard consumes her bundle and boots up a local session.
3. **Reply**: Bob fires back a `PreKeySignalMessage` containing additional protocol information necessary to force Alice's device to reciprocate the session handshake.
4. **Link**: Once Alice detects the `PreKeySignalMessage`, her session is fully locked in. Subsequent interactions purely utilize standard `SignalMessage` payloads.

Periodically (30 days), signed prekeys are dynamically rotated and shipped along with normal `SignalMessages` to implicitly force a KeyBundle refresh without the user noticing an interruption.

---

## Payload Masking & Encoding

### 1. Raw Mode (Minified JSON)
All standard information (`SignalProtocolAddress`, Timestamps, Key Responses) are assembled into a `MessageEnvelope`. To retain viability over constrained channels (like Threema's 3500 byte limit):
- Keys are aliased identically minified mappings (e.g. `preKeyResponse` -> `pR`).
- Spaces and tabs are purged.
- The raw JSON payload is GZIP compressed and sent identically over the pipe as plain text strings.

### 2. Fairytale Mode (Zero-Width Steganography)
To evade AI surveillance or network pattern analyzers (e.g., EU Chat Control DPI implementations), the GZIP binary is effectively rendered invisible.
- Every 4 bits of binary are mapped to one of 16 distinct "Invisible" Unicode sequences (such as `U+200C ZERO WIDTH NON-JOINER`).
- This invisible blob of payload is appended securely onto the end of a decoy sentence pulled randomly from a curated database of folklore text (e.g., Cinderella, Rapunzel).
- **Extraction:** Upon interception locally, the keyboard trims the visible decoy folklore, parses the invisible unicodes back into binary, inflates the GZIP string, deserializes the JSON envelope, and pipes it directly into the decryption ratchet.

*Note: Some platforms structurally normalize and sanitize unicodes or wrap text inside HTML abstractions upon copying (e.g. Telegram Desktop/Mobile), which permanently destructs the zero-width steganographic payload. In these instances, Raw Mode must be used.*

---

## Cryptography Specifications
Azokle Keyboard adheres to the existing security paradigms established by the core Signal Library:
- **Elliptic Curve:** X25519
- **Hashing/Fingerprinting:** SHA-512 (Initialization and public key mapping) and SHA-256 for Double Ratchet KDF chain routing.
- **Transport Cipher:** AES-256 (CBC with PKCS#7 padding).

The application requires no network or contact permissions, drastically reducing its threat model against local sandboxing escapes.
