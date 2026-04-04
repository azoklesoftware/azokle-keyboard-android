# User Guide & Support

Welcome to **Azokle Keyboard**. This guide will step you through bootstrapping an encrypted session with your peers purely over your existing messaging applications.

---

## The Basics

### How do I configure my identity?
Your identity is handled automatically! Upon installation, the keyboard creates a randomized UUID that acts as your private identity layer. You are entirely decoupled from phone numbers or emails.

### How do I start a chat?
Since there’s no central server, you have to directly pass an "Invite Metadata Payload" to your friend utilizing whatever app you're currently in:
1. Open up WhatsApp, Signal, SMS, etc.
2. Select the Azokle Contact List icon on our keyboard.
3. Tap **Send My Invite**. A payload will be pasted into your chat box. Hit send in your messenger app.

### How do I accept an invite from someone?
1. Highlight and **Copy** the invite payload your friend just sent you into your clipboard.
2. Swap to Azokle Keyboard and press the **Decrypt** button.
3. A prompt will appear asking you to save this new identity signature. Type their name and press **Done**.
4. To finish the handshake, you must eagerly send an encrypted message back. Select their newly saved profile internally and send an encrypted reply.

---

## Daily Use

### How do I encrypt a message?
1. Confirm the chat partner is actively selected in your Azokle Keyboard toolbar.
2. Type your secret text natively into the Azokle text bar (do *not* type it into the messenger app's normal text field).
3. Hit the **Encrypt** button on the keyboard.
4. Your ciphertext (or Fairytale string) will immediately populate the traditional input box of the messaging app. Go ahead and send it!

### How do I decrypt a message?
1. Tell your OS to **Copy** the incoming encrypted message block your friend sent you to your clipboard.
2. Ensure your friend's profile is selected inside Azokle. 
3. Tap the **Decrypt** button. The plaintext payload will populate inside the isolated Azokle display layer.

### How do I check old messages?
Azokle locally caches an internal ledger. Open the **Message Log** section dynamically within the keyboard overlay. *Warning: Deleting a contact permanently purges all localized histories linked to their UUID.*

---

## Security Verification

### How do I know my chat partner isn't being impersonated?
A man-in-the-middle (MITM) attack is severely mitigated by performing an out-of-band UUID verification:
1. Tap the verified/unverified crest next to the contact profile.
2. A shared numeric fingerprint block will display on your screen.
3. Read these numbers aloud over a secure voice call or compare them in-person with your friend to ensure they perfectly match.
4. If identical, hit **Mark as Verified**.