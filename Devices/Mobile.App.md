# Mobile App Testing — Cheat Sheet

## Pre-flight & Environment

* Verify build type and flags: Debug vs Release, staging vs prod endpoints, feature flags/remote config, analytics toggles, logging level.
* Know your credentials & data: seeded test users, IAP/test cards, push notification test accounts, clean uninstall/reinstall routine.
* Baseline the app version, OS version, device model, locale, and network conditions in your notes.

## Device/OS Matrix (minimum viable)

* OS: Latest, latest-1, and your app’s minimum supported.
* Devices: small vs large screens, low-RAM/older CPU vs flagship, notched vs non-notched, tablet vs phone.
* Form factors/sensors: biometric types, GPS, camera, NFC, Bluetooth.

## Install / Update / Uninstall

* Fresh install: first-run experience, onboarding, default permissions, analytics first-open event.
* Update paths: old→new with data migration, schema upgrades, feature flag changes, deep link handling post-update.
* Uninstall/reinstall: orphaned data, keychain/keystore remnants, re-permission prompts, notification token refresh.

## Authentication & Session

* Sign up/login: valid/invalid flows, SSO/social, MFA, rate limiting, lockouts.
* Session life: token refresh, expiry, revocation, logout clears sensitive state.
* Remember me/biometric re-entry: app kill, background > X mins, device reboot.

## Permissions (granularly)

* Ask timing: on first use of a feature, not on app start (unless justified).
* States: granted, denied, denied-forever (“Don’t ask again”), revoked in OS Settings.
* Degradation: graceful fallbacks, inline education, quick path to Settings.

## Navigation, Deep Links & Routing

* Tab stacks, back stack, state restoration after rotate/background/kill.
* Deep links/app links/universal links: cold start vs warm start, authenticated vs anonymous, expired links, tracking params.
* External intents: open web, map, email, phone; return flow intact.

## Offline, Poor Network, and Sync

* Modes: offline, flaky 2G/3G, captive portal, switching Wi-Fi⇄cell.
* Queueing & retries: idempotency, duplicate submissions, backoff, conflict resolution on reconnect.
* Caching: stale labels, manual refresh, pull-to-refresh feedback.

## Interrupts & App Lifecycle

* Interrupts: calls, alarms, notifications, permission popups, OS dialogs, app store prompts.
* Lifecycle: foreground⇄background, app kill by OS, low-memory evictions, restore last screen and inputs.
* Media: audio focus, PiP where relevant, playback continuity.

## Data, Privacy, and Storage

* Sensitive data at rest: no plaintext in logs/storage; proper use of Keychain/Keystore.
* Clipboard hygiene, screenshots in app switcher (sensitive screens blurred where needed).
* GDPR/DSAR: export/delete account flows, cookie/consent equivalence on mobile.

## Push & Local Notifications

* Registration: token created/rotated, permission timing, per-platform nuances (APNs/FCM).
* Delivery: foreground/background/terminated, action buttons, deeplink targets.
* Opt-in/out granularity and in-app “Marketing vs Transactional” toggles.

## Payments & IAP (if applicable)

* Environment: sandbox test users, product IDs correct, prices/regions/taxes.
* Purchase flow: success, cancel, failure, declined, interrupted mid-flow.
* Restore purchases, duplicate receipt handling, server-side validation.

## Media & Sensors

* Camera/mic/gallery: permission states, EXIF handling, orientation, size/format limits.
* GPS: accuracy modes, mock location prevention if required, no-signal behavior (indoors).
* Bluetooth/NFC: scan, pair, disconnect, background constraints.

## Accessibility (always)

* VoiceOver/TalkBack traversal order and labels, hit targets ≥44px, focus visible.
* Dynamic type/font scaling, contrast, dark mode, color-blind palettes.
* Motion & haptics respect OS “Reduce motion” and “Haptics off.”

## Performance, Stability & Battery

* App start: cold < 2–3s target (depends), warm < 1s; first contentful UI visible.
* Scrolling/jank: 60fps target, lazy loading lists, image placeholders.
* Memory: leaks, OOM on media-heavy screens; CPU/Battery: background tasks throttled.
* Network: payload size, compression, HTTP caching, pagination.

## Security Sanity Pass

* TLS pinning (if used), cert errors handled, no mixed content.
* Hidden debug menus, test endpoints, and verbose logs disabled in Release.
* Input validation client + server, jailbreak/root detections policy.

## Localization & Time

* Locales: RTL/LTR, long strings wrap, pluralization, numerals, date/timezones, DST edges.
* Regional content: content policies, payment availability, map/address formats.

## Analytics & Logging

* Event map complete: screen views, key actions, errors, user properties.
* Idempotent events (no dupes on rotate/restore), consent gating respected.
* Crash/exception reporting: breadcrumb richness, PII scrubbed.

## What to Automate vs. Explore

* Good for automation: login, nav smoke, critical CRUD, deeplinks, offline queue logic, feature flags happy paths.
* Keep exploratory: new UX, visuals, gestures, accessibility nuance, sensor edge cases, perf feel, interrupt storms.

## Lightning Smoke Tour (10–15 mins)

* Launch → first screen renders → login → primary feature happy path → create/edit/delete item → background/restore → rotate → deep link → push received → settings toggle → logout → relaunch.

## High-Value Exploratory Charters

* “Interrupt Storm”: perform a long form action while simulating calls, notifications, permission prompts; assess resilience and user messaging.
* “Dirty Network”: create/edit flows under throttled/flickering network; confirm dedupe, retries, and user feedback.
* “Cold Start Realism”: app terminated overnight, reopen via notification/deeplink; verify auth, route, and state integrity.
* “Accessibility First”: complete a core flow using only a screen reader at 130% text size in dark mode.
* “Update in Motion”: start an operation on vN, update to vN+1, reopen; validate migrations and continuity.

## Useful ADB / iOS Tips (quick)

* Android throttle: `adb shell cmd network latency gsm` and `adb shell cmd network speed edge`.
* Kill & cold-start Android: `adb shell am force-stop com.your.app && adb shell monkey -p com.your.app -c android.intent.category.LAUNCHER 1`.
* iOS simulators: test Dynamic Type, VoiceOver, location mock routes via Xcode; notifications with `xcrun simctl push`.

## Reporting Nuggets

* Always attach: device/OS/build, logs (redacted), steps + screenshots/screen recordings, network traces, and expected vs actual with user impact estimate.
* Note reproducibility across network states and devices. Call out whether it’s a regression and from which version.

## Automation Pointers (tool-agnostic)

* Appium/Detox/XCUITest/Espresso for native. Playwright is great for mobile web/PWAs; for native wrappers, prefer Appium.
* Build a small but reliable “Golden Path” suite per platform, then layer device-agnostic API/UI checks.
* Stabilize with: test IDs, wait for network idle/state rather than sleeps, and avoid over-mocking real device behaviors you care about (push, sensors).

## Release Gate Checklist

* ✅ Crash-free rate on beta ≥ target; no new top-10 crash.
* ✅ First-run/onboarding solid; analytics first-open & consent tracked.
* ✅ Auth/session, deep links, and notifications verified.
* ✅ Offline/poor network behavior acceptable for core flows.
* ✅ Payments/IAP sanity, receipts validated.
* ✅ Accessibility pass and dynamic type OK.
* ✅ No debug artifacts/log leakage in Release.
* ✅ Store listing metadata/screenshots updated if UI changed.
