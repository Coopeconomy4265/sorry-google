<p align="center">
  <img src="logo.png" alt="Sorry Google" width="200"/>
</p>

# Sorry Google

Minimal stub APKs that block Google from automatically installing or updating
unwanted system apps. Each stub declares the same package name as the target
app but is signed with a different key, causing a signature mismatch that
prevents the original from being pushed.

## Targeted Packages

| Package | App Name | Google Play |
|---------|----------|-------------|
| `com.google.android.safetycore` | Android System SafetyCore | [Play Store](https://play.google.com/store/apps/details?id=com.google.android.safetycore) |
| `com.google.android.contactkeys` | Android System Key Verifier | [Play Store](https://play.google.com/store/apps/details?id=com.google.android.contactkeys) |
| `com.google.android.verifier` | Android Developer Verifier | [Play Store](https://play.google.com/store/apps/details?id=com.google.android.verifier) |

> **⚠️ System App Warning:** Some of these apps are pre-installed as system apps.
> You **cannot uninstall** them without root access.
> - Without root: use `adb shell pm disable-user <package>` to disable them
> - With root: use `adb shell pm uninstall --user 0 <package>` to fully remove
> - After removing, install the matching stub from this project to prevent Google from pushing them back

## How It Works

1. Each module is a valid Android APK with the exact package name of the target
2. The stubs are signed with your own key (not Google's key)
3. When Google tries to push the real app, the signature mismatch blocks it
4. The stubs contain no code — just manifest + icon

## Downloading

Download the latest APKs from [GitHub Releases](https://github.com/rushiranpise/sorry-google/releases).
Just download the APK file and open it on your phone — Android will install it directly.

## Building from Source

```bash
./gradlew assembleDebug
# or for release (requires signing config in local.properties):
./gradlew assembleRelease
```

## GitHub Actions

Push a tag to trigger a build and publish signed APKs as a GitHub Release:

```bash
git tag v1.0
git push origin v1.0
```
