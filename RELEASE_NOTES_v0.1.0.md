# ParseQuest Desktop v0.1.0 — Public Beta Release

**ParseQuest** is a local-first desktop research and preservation workspace for Windows 10/11 (64-bit). Capture what you view in your own foreground browser session, keep cryptographic provenance (`SHA-256`) and version history on every record, and export citable datasets (`JSON`, `CSV`, `PDF`).

## What's Included in v0.1.0 (Public Beta)
- **Masonry Split-Pane Workbench:** Two-column masonry triage grid paired with a full record & provenance inspector pane (`45% / 55%` split, 2D keyboard navigation, media & video playback).
- **Foreground, Rate-Respecting Capture:** Dedicated Chromium research profile per project; user-present session mode with built-in hourly collection guardrails (`max 3 runs/hour`).
- **Cryptographic Provenance & Versioned Records:** Every captured record is sealed in local SQLite (`WAL + FTS5`, 19 versioned migrations) with a `SHA-256` content digest and append-only version lineage.
- **Scope & Author Erasure Controls (`GDPR Art. 17`):** Preview and delete all stored records for any author `@handle` in one step (**Settings → Delete results by author**), with deletion audit logging.
- **Portable Offline Exports:** Export collections to `JSON` (with cryptographic dataset manifest), `CSV`, or formatted `PDF` reports.
- **Optional Cloud Sync:** Off by default; sync selected collections when you choose. Credentials and browser sessions never leave your device.

## System Requirements
- **OS:** Windows 10 or Windows 11 (64-bit `x86_64`)
- **Installer:** `ParseQuest-Desktop-0.1.0-x64-setup.exe` (~`99.8 MB`)

## Checksums (`SHA-256`)
```text
4740EF0D677263AA8AF6EAC7F0951C9C848BAD9D680A80F6555D528E0A89B83F  ParseQuest-Desktop-0.1.0-x64-setup.exe
```

To verify on Windows PowerShell:
```powershell
Get-FileHash .\ParseQuest-Desktop-0.1.0-x64-setup.exe -Algorithm SHA256
```
