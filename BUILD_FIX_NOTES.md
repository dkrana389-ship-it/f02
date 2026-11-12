# Build fix notes

## Dependency resolution fix

Coil 3 is published under the Maven group `io.coil-kt.coil3`, not `io.coil-kt`.
The version catalog now uses:

```toml
coil = "3.6.3"
coil-compose = { module = "io.coil-kt.coil3:coil-compose", version.ref = "coil" }
```

This corrects the missing-artifact coordinate shown in the GitHub Actions log.

## GitHub Actions

The workflow uses the checked-in Gradle wrapper (`./gradlew`). It always builds and uploads a debug APK. Signed release APK/AAB builds run only when all four signing secrets are configured.

## Verification limits

This environment could not download Gradle from `services.gradle.org` because network DNS access was unavailable. Therefore an actual Gradle compilation could not be completed here. GitHub Actions must perform the authoritative build.

The current application ID is `com.keepfocus.app`; it must match the already-published Play Store application's ID before publishing an update.

The accessibility implementation currently uses scroll events from selected target apps as a heuristic. It cannot guarantee that every event represents a distinct Reel or Short across all app versions. Real-device testing and an accurate Play Console Accessibility API declaration are required before release.
