# SalahSync

Offline-first Flutter app for managing prayer times and mosque-specific Jamaat schedules, built for Khanewal, Pakistan. All core features work with no network connection: prayer times are computed on-device by a pure-Dart engine, and mosque schedules live in a local encrypted-backup-capable Drift/SQLite database.

## Features

- `Today`, `Mosques`, `Compare`, and `Settings` tabs with a live current-time clock, next-prayer countdown, and utility launcher
- Pure-Dart prayer-time engine wrapper around `adhan_dart`
- Local Hijri date derivation with override support
- Qibla bearing calculation plus a compass-backed Qibla screen with live/saved coordinates
- Timing-rule model and resolver for offset, fixed, and date-range-fixed rules
- Drift-backed mosque/settings persistence and seeded data
- Mosque CRUD, timing-rule editing, and side-by-side Jamaat comparison UI
- Local notification scheduling with a rolling 48-hour window, permissions, and exact-alarm fallback
- Notification runtime diagnostics, manual 48-hour window rebuild, and battery-optimization guidance
- Persisted theme mode (`system`, `light`, `dark`)
- Passphrase-protected backup export/import for the local Drift database, with legacy plaintext import compatibility and file-share/file-import flows
- Ibadah planner with recurring tasks, task editor, daily checklist expansion, and tasbih counters
- Prayer log with date navigation, Friday Jummah handling, and weekly/monthly summaries
- Monthly timetable view with Friday Jummah rows and Ramadan highlighting
- Manual AlAdhan verification screen using unadjusted engine-vs-API comparison
- Android home-screen widget support with shared widget sync data and pin-request action
- Unit and widget tests for core domain logic, persistence, scheduling, and the app shell

## Roadmap

Native work still requiring physical-device signoff:

- Android widget placement/update behavior on a real launcher
- Qibla compass accuracy and calibration messaging on actual hardware
- iOS WidgetKit extension creation/signing beyond the shared app-group groundwork already in place

## Tooling

- Flutter `3.41.5`
- Dart `3.11.3`
- Android min SDK `26`
- iOS deployment target `14.0`

## Commands

```bash
flutter pub get
flutter pub run build_runner build --delete-conflicting-outputs
flutter analyze
flutter test
```

## Notes

- Defaults to the Karachi calculation method and Hanafi Asr, which the domain layer currently uses.
- Release validation notes are mapped to the SRS checklist in `docs/release-validation.md`; the build plan lives in `docs/build-plan.md`.
- The original SRS sample for March 22, 2026 lists `Asr 15:46`, but AlAdhan's Hanafi response for that date is `16:41`. The tests follow the external Hanafi reference values and allow the `±1 minute` tolerance already defined in the SRS.
