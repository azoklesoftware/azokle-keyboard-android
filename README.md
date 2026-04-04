<div align="center">
  <img src="static/logo/logo.png" height="150" alt="Azokle Keyboard Logo">

  <h1>Azokle Keyboard</h1>
  <p><b>Secure, Serverless, End-to-End Encrypted (E2EE) Communication for Any Messenger</b></p>
  
  [![GitHub version](https://img.shields.io/badge/version-v0.1.5-brightgreen)](https://github.com/azoklesoftware/azokle-keyboard-android/releases)
  [![License](https://img.shields.io/badge/license-GPLv3-blue)](LICENSE)
  [![Privacy First](https://img.shields.io/badge/privacy-first-blueviolet)](https://policies.azokle.com/privacy/)

  <p>
    <a href="#overview">Overview</a> •
    <a href="#features">Features</a> •
    <a href="#installation">Installation</a> •
    <a href="#documentation">Documentation</a>
  </p>
</div>

---

## Overview

**Azokle Keyboard** by [Azokle Software](https://azokle.com) is an Android custom keyboard engineered to inject verified end-to-end encryption (E2EE) into *any* third-party messenger—without relying on external servers or trusting the underlying chat application. 

With laws continually threatening standard E2EE (e.g., chat control legislation), Azokle Keyboard empowers users to encrypt messages autonomously using the battle-tested **Signal Protocol** (X3DH Key Agreement & Double Ratchet Algorithm).

## Key Features

- 🛡️ **Universal E2EE Integration:** Works independently on top of WhatsApp, Telegram, SMS, or any text field.
- 📡 **Serverless Protocol:** Keys and session exchanges are securely managed without a central key server.
- 🥷 **Fairytale Steganography Mode:** Optionally hide encrypted ciphertexts as invisible, zero-width Unicode characters wrapped within an innocent decoy message (like a fairytale story).
- 🧩 **Raw JSON Mode:** Highly compressed, minified JSON payloads for standard encrypted exchanges.
- 📇 **In-Keyboard Contacts:** Keep a localized contact list separated from your phone's main OS.
- 📋 **Secure Clipboard Interception:** Automatically detect and decrypt incoming Azokle messages natively within the keyboard view.

## Screenshots

<div align="center">
  <img alt="App Usage" src="static/screenshots/demo.gif" width="70%">
</div>

## Installation

Azokle Keyboard requires **Android 8.0 (API 26)** or higher.

| Platform | Link |
|----------|------|
| **F-Droid** | [<img alt='Get it on F-Droid' src='https://gitlab.com/fdroid/artwork/-/raw/master/badge/get-it-on-en.png' height='40'/>](https://f-droid.org/en/packages/com.azokle.keyboard/) |
| **IzzyOnDroid** | [<img alt='Get it on IzzyOnDroid' src='https://gitlab.com/IzzyOnDroid/repo/-/raw/master/assets/IzzyOnDroid.png' height='40'/>](https://android.izzysoft.de/repo/apk/com.azokle.keyboard) |
| **GitHub Releases** | [<img alt='Get it on Github' src='static/github/get-it-on-github.png' height='40'/>](https://github.com/azoklesoftware/azokle-keyboard-android/releases) |

## Documentation

- [**User Guide & Help**](HELP.md) - Learn how to invite contacts, initiate sessions, and send messages.
- [**Architecture & Technical Specs**](ARCHITECTURE.md) - Deep dive into how we adapted the Signal Protocol for serverless environments and our payload minification.
- [**Security Policy**](SECURITY.md) - Vulnerability disclosure and algorithm specifics.
- [**Privacy Policy**](PRIVACY.md) - Our data and telemetry practices.

## Limitations

- **1-to-1 Centric:** Designed primarily as a POC for point-to-point communication. While group chats work, encrypted messages are tightly locked to single recipient keys.
- **Payload Limits:** Threema and other messengers cap inputs at ~3500 bytes. To ensure seamless delivery, raw and fairytale modes are capped at roughly 500 characters of input.
- **Formatting Corruptions:** Apps like Telegram format clipboard copies via HTML, which invariably destroys the invisible zero-width Unicode entities used in *Fairytale Mode*. For Telegram, **Raw Mode** is strictly required.

---

<div align="center">
  <p>Built with privacy by <b><a href="https://azokle.com">Azokle Private Limited</a></b></p>
  <p><a href="https://policies.azokle.com/privacy/">Privacy Policy</a> • <a href="https://azokle.com/foundation">Support Our Foundation</a></p>
</div>
