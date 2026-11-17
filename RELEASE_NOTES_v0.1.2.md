# ParseQuest Desktop v0.1.2 Release Notes

**Release Date:** November 15, 2026  
**Build:** v0.1.2  
**Tag:** `v0.1.2`

## Highlights & Fixes

### 1. Collector Authentication Resilience (`BUG-002`)
- **Interactive Login Wall Detection:** Resolved issue where collector processes prematurely timed out when encountering interactive social login walls (e.g. X / Twitter authentication).
- **Graceful Polling:** Added up to 300 seconds interactive login window with 2.0s polling interval, allowing manual authentication before collecting.

### 2. Auto-Updater & Security Infrastructure
- Decoupled updater checks from vault session lock state to allow continuous background update discovery.
- Fully signed NSIS Windows installer with Authenticode & Tauri minisign cryptographic verification.
- Zero-downgrade policy enforced.

## Release Assets
- `ParseQuest Desktop_0.1.2_x64-setup.exe` (SHA256: `e60ccb8ecd5e401e144ce376d87bdd21a03d9adac094b3b48bf3b0394e933490`)
- `ParseQuest Desktop_0.1.2_x64-setup.exe.sig`
- `SHA256SUMS_v0.1.2.txt`
- `latest.json`
