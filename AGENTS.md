# SiphonDSP

SiphonDSP is an Android app for system-wide JamesDSP audio processing without root.

Android builds and dependency resolution use the Gradle Wrapper (`./gradlew`); Fastlane dependencies use Bundler (`bundle`).

## Where code lives

- `app/src/main/` contains shared app code, resources, and native build files.
- `app/src/{rootless,root,plugin,full,fdroid}/` contains flavor-specific app code and resources.
- `app/src/main/cpp/` contains JNI wrappers and native DSP code. `libjamesdsp/` is a Git submodule.
- `codeview/` and `hidden-api-*` are supporting Gradle modules.

## Verifying

- Run unit tests and rootless full lint with `./gradlew test :app:lintRootlessFullDebug`.
- For flavor-specific changes, assemble the affected variant, such as `./gradlew :app:assembleRootlessFdroidDebug`.
- See the [README build guide](README.md#building) for available variants and SDK requirements.

## Additional tips

- Keep shared behavior in `app/src/main/`; use flavor source sets only for differences.
- Rootless is the primary build. Rooted builds receive less testing; see [BUILD_ROOT.md](BUILD_ROOT.md).
- Install the JDK, NDK, and CMake versions required by the Gradle configuration before building.
