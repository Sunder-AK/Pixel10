# Pixel Guardian v1.0

A minimal **native Android/Kotlin** anti-theft companion for Pixel 10 (Android 10+). No accounts, analytics, cloud servers, or root.

## Features
- User-started foreground monitoring with persistent notification
- Records screen off, screen on, and user-present (unlock) broadcasts
- Records default network connectivity changes and posts an on-device alert when offline
- Stores up to 200 events locally; view and clear from app
- No internet permission: nothing is uploaded

## Open and build
1. Install Android Studio with Android SDK 35 and JDK 17.
2. Extract this ZIP and open the **PixelGuardian** directory in Android Studio.
3. Allow Android Studio to sync/download Gradle and Android Gradle Plugin 8.7.3.
4. Choose **Build > Build APK(s)** or run on your Pixel 10 with USB debugging.
5. Open the app, allow notifications, and tap **Start monitoring**.
6. Use **Stop monitoring** to stop the foreground service.

Note: This ZIP includes Gradle build files but not a generated Gradle wrapper JAR. Android Studio can use its installed Gradle or generate a wrapper with `gradle wrapper --gradle-version 8.9` on a machine with Gradle installed.

## Security and OS limitations
- A normal app **cannot** require PIN before toggling Quick Settings, power-off, restart, or hardware forced reboot.
- Screen-off is not proof of lock; `ACTION_USER_PRESENT` is not a comprehensive authentication audit.
- Connectivity events do not prove Airplane Mode was toggled. A lost connection may be due to coverage, Wi-Fi handover, or network changes.
- A notification cannot be delivered remotely after connectivity is lost; this app only posts **local** alerts.
- Monitoring starts only when the user taps Start. Android may stop the service under some conditions. No boot persistence is claimed.
- The specialUse foreground-service declaration is for a user-initiated monitoring task; Play Store distribution may require policy review and approval.
- No Accessibility Service, device-admin tricks, root, or attempts to bypass system restrictions.

## Source layout
- `MainActivity.kt`: simple interface
- `GuardianService.kt`: foreground monitoring and local alerts
- `EventStore.kt`: local event log

## Build verification
The source was generated and inspected but **not compiled** here because the Android SDK/Gradle toolchain is unavailable in this environment. Android Studio sync/build may require updates for your installed tooling.
