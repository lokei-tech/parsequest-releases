# ParseQuest Desktop v0.1.1 — Post-Beta Stabilization & Security Hardening

**Release Date:** 2026-11-12 (pending installer build)
**Status:** Code complete — awaiting Windows code signing (REL-A3) before installer build

## What's Fixed in v0.1.1

### Collector Resilience & OTA Hotfix Channel
- **Remote config alignment (FND-01):** Primary URL now points to `https://parse.quest/v1/config.json` with `config.parse.quest` fallback and env-var override. Deep-merge and atomic cache write prevent stale configs.
- **Externalized DOM selectors (FND-02):** All 17 tweet/snapshot DOM selectors and detection strings moved from hardcoded Python into `bundled_config.json` and remote `v1/config.json` (v2), enabling over-the-air selector hotfixes without app update.
- **Browser profile mutex (FND-11):** Added per-profile singleton lock (`BrowserProfileInUseError`) preventing concurrent jobs/probes/preserves from corrupting `browser_profile/`.
- **Health probe leak fix (ADD-001):** Fixed browser context leak when health probe ran while collector was stopped.

### Security & Local Sandbox Hardening
- **Tauri scope narrowing (FND-03):** Restricted `assetProtocol.scope` from `["**"]` (full filesystem) to app-data and resource directories only.
- **Media proxy hardening (FND-07):** `/media/proxy` now enforces HTTPS + port 443 and validates every redirect hop against `ALLOWED_HOSTS` (max 3 hops).
- **Session token encryption (FND-12):** Local session tokens are now stored encrypted at rest — OS keyring preferred (`keyring:v1`), with `enc:v1` file cipher fallback.
- **Supabase key rotation (FND-14):** Verified legacy keys purged from git history; added runtime key-type validation guards.

### Data Integrity & Product Reality
- **Uncapped export pagination (FND-04):** Replaced hardcoded `limit=5000` with paginated retrieval (up to 50K records) and added `truncated` metadata to export manifests.
- **Real export preview (FND-06):** Replaced frontend mock (`previewExport`) with real `POST /artifacts/export/preview` backend endpoint returning actual record counts, byte sizes, and date ranges.
- **Evidentiary screenshots (FND-13):** Preserve now captures a viewport PNG screenshot with SHA-256 hash for chain-of-custody evidence (`screenshot_path` + `screenshot_sha256` on every snapshot record).
- **Opt-in activation telemetry (FND-05):** Strictly opt-in telemetry with PII sanitizer, Settings toggle, and SQLite-backed milestone tracking for Gate 1 measurement.

### Commercial Alignment & Codebase Hygiene
- **Unified plan ladder (FND-08):** Consolidated from 7 inconsistent tiers to canonical 5-tier ladder (`FREE`, `RESEARCHER`, `PRO`, `TEAM`, `ENTERPRISE`) with backward-compatible legacy alias normalization.
- **Dead stub cleanup (FND-09):** Replaced 8 Phase-9 `NotImplementedError` stub files with clean re-export modules.
- **Documentation update (FND-10):** Updated `ParseQuest_Product_Capability_Brief.md` to v2.0 reflecting Oct 10 rate-respecting capture guardrails.

### Verification Audit Fixes
- Fixed `get_remote_config_manager` → `get_active_manager()` API in export pagination
- Extended GDPR author deletion to also clean evidentiary screenshot PNGs
- Upgraded session persistence to keyring-first storage with encrypted fallback
- Added `_isolate_os_keyring` test fixture for CI safety (prevents tests from touching real OS credentials)

## Verification Results
| Gate | Result |
|---|---|
| `pytest` (parsequest-local) | **1,076 passed**, 5 skipped |
| `vitest` (parsequest-desktop) | **81/81 passed** |
| `tsc --noEmit` | 0 errors |
| `lint:ux` | 58 files, 0 warnings |
| `cargo check` | 0 errors (2 pre-existing dead-code warnings) |

## Commits
- `parsequest-core`: [`b0fae51`](https://github.com/lokei-tech/parsequest-core/commit/b0fae51) — 1,740 files, 50,657 insertions, 9,839 deletions
- `parsequest-website-v5-brand`: [`91a3134`](https://github.com/lokei-tech/parsequest-website-v5-brand/commit/91a3134) — v2 remote config with externalized selectors

## System Requirements (Unchanged)
- **OS:** Windows 10 or Windows 11 (64-bit `x86_64`)
- **Installer:** Pending build (will be `ParseQuest-Desktop-0.1.1-x64-setup.exe`)
