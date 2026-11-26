# Hanto App (Android)

Native Android app for Hanto staff. Fork of [`element-hq/element-x-android`](https://github.com/element-hq/element-x-android), Rust-SDK based Matrix client.

Owner: Hanto Workspace Technologies Private Limited. Public per AGPL-3.0.

## Why a fork

Field staff (supervisors, technicians, CS) use this app on their work phones for:

- Chat (same Matrix rooms the web console sees)
- **Check-in / check-out** at client sites (selfie + geo + time)
- **Attendance** (self-punch or marked-for)
- **Daily / per-visit checklists**
- **Issue capture** (photo + one-line description → ticket in Automata)

Non-chat screens are Hanto-specific and live inside the fork; chat behaviour matches upstream.

## Upstream relationship

- **Base**: `element-hq/element-x-android` (default branch `develop`)
- **Our default branch**: `develop` — we track upstream and layer Hanto changes on top
- **Our topic branches**: `hanto/<feature>` — e.g. `hanto/check-in`, `hanto/branding`
- **Upstream sync cadence**: weekly; rebase `develop` on upstream `main`, resolve conflicts, PR against ourselves

## Build

Currently depends on Android Studio Hedgehog or newer + Rust toolchain (Cargo). See upstream [`docs/`](./docs/) for build steps.

For a release APK:

```bash
./gradlew :app:assembleGplayRelease   # Google Play variant (release signed)
./gradlew :app:assembleFdroidRelease  # F-Droid variant (no proprietary deps)
```

Release signing uses a keystore kept by the operator; see `fastlane/README.md` for pipeline notes.

## What's changed vs upstream

Minimal day-1 fork:

- **App id**: `co.hanto.app` (was `io.element.android.x`)
- **App name**: `Hanto` (was `Element X`)
- **Default homeserver**: `automata.hanto.co` (was `matrix.org`)
- **Copyright + website URL** (BuildTimeConfig)

All changes are in config files — no logic touched yet.

## Licence

AGPL-3.0, inherited from upstream. See [LICENSE](./LICENSE-AGPL-3.0). If you install this app from the Hanto team, you have the right to request the source — which is this repo.

## Backend

The app talks to:
- **Synapse** at `https://automata.hanto.co` (Matrix homeserver, including `.well-known/matrix/{client,server}` discovery)
- **Automata API** at `https://automata-api.automata.hanto.co` — Hanto-specific endpoints for check-in/attendance/ticketing (added in subsequent HANs)

## Issues / tracking

Internal Linear project `Hanto Automata (Hanto V2)` — issues prefixed `HAN-`.
