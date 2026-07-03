---
name: android-cli
description: Orchestrates Android development tasks including project creation, deployment, SDK management, and environment diagnostics using the `android` command-line tool.
---

## Diagnostics
```powershell
adb devices               # check attached devices/emulators
adb shell getprop ro.build.version.release # get OS release
adb logcat -d -t 100      # fetch last 100 logs (dump and exit)
adb logcat *:E            # stream error level logs only
```

## Setup & Emulate
```powershell
emulator -list-avds       # list local emulators
emulator -avd <AVD_NAME>  # launch specific emulator
adb install -r <APK_PATH> # install or update application package
```

## Intent & App Control
```powershell
adb shell am start -n <PACKAGE>/<ACTIVITY> # launch app
adb shell am force-stop <PACKAGE>          # stop target package
adb shell pm clear <PACKAGE>               # wipe user data/cache
```

## Rules
- Never launch an emulator blockingly in the primary run task shell (always append background parameters or run async).
- Always verify connected status using `adb devices` before running build scripts.
