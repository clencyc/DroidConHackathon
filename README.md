<<<<<<< HEAD
This is a Kotlin Multiplatform project targeting Android, Web, Desktop (JVM).

* [/shared](./shared/src) is for code that will be shared across your Compose Multiplatform applications.
  It contains several subfolders:
  - [commonMain](./shared/src/commonMain/kotlin) is for code that’s common for all targets.
  - Other folders are for Kotlin code that will be compiled for only the platform indicated in the folder name.
    For example, if you want to use Apple’s CoreCrypto for the iOS part of your Kotlin app,
    the [iosMain](./shared/src/iosMain/kotlin) folder would be the right place for such calls.
    Similarly, if you want to edit the Desktop (JVM) specific part, the [jvmMain](./shared/src/jvmMain/kotlin)
    folder is the appropriate location.

### Running the apps

Use the run configurations provided by the run widget in your IDE's toolbar. You can also use these commands and options:

- Android app: `./gradlew :androidApp:assembleDebug`
- Desktop app:
  - Hot reload: `./gradlew :desktopApp:hotRun --auto`
  - Standard run: `./gradlew :desktopApp:run`
- Web app:
  - Wasm target (faster, modern browsers): `./gradlew :webApp:wasmJsBrowserDevelopmentRun`
  - JS target (slower, supports older browsers): `./gradlew :webApp:jsBrowserDevelopmentRun`

### Running tests

Use the run button in your IDE's editor gutter, or run tests using Gradle tasks:

- Android tests: `./gradlew :shared:testAndroidHostTest`
- Desktop tests: `./gradlew :shared:jvmTest`
- Web tests:
  - Wasm target: `./gradlew :shared:wasmJsTest`
  - JS target: `./gradlew :shared:jsTest`

---

Learn more about [Kotlin Multiplatform](https://www.jetbrains.com/help/kotlin-multiplatform-dev/get-started.html),
[Compose Multiplatform](https://kotlinlang.org/compose-multiplatform/),
[Kotlin/Wasm](https://kotl.in/wasm/)…

We would appreciate your feedback on Compose/Web and Kotlin/Wasm in the public Slack channel [#compose-web](https://slack-chats.kotlinlang.org/c/compose-web).
If you face any issues, please report them on [YouTrack](https://youtrack.jetbrains.com/newIssue?project=CMP).
=======
# NetState

**Test your UI under every network state, in one line.**

A small Kotlin Multiplatform library that pairs a network state monitor with a snapshot-testing helper. Write one test and get a screenshot of your screen for each network condition: online, offline, metered and slow.

> Status: hackathon prototype, built in 40 minutes. Android is the supported target. Other platforms are stubbed.

---

## The problem

Most mobile apps are designed and tested on fast Wi-Fi. Real users, especially across Africa, spend a lot of time on flaky, metered or offline connections. Teams rarely test those states because it is tedious: you have to toggle airplane mode by hand, remember every screen, and notice visual regressions yourself.

Connectivity libraries tell you the network state. Snapshot libraries capture a screen. Nothing connects the two, so offline UI is the part of the app that gets broken and nobody notices.

## What NetState does

1. **Network monitor.** One interface that exposes the current network state as an observable stream, with four states: Online, Offline, Metered and Slow.
2. **Fake monitor for tests.** A controllable implementation so any screen can be put into any network state without touching a real network.
3. **Multi-state snapshot helper.** Give it a screen, and it renders that screen once per network state and saves an image of each. If a saved image already exists, it compares against it and fails the test on a difference.

The result: one test, four screenshots, and a failing build when someone breaks the offline banner.

## Who it's for

- Mobile developers who want offline and low-data states covered by tests instead of manual checks.
- Designers and QA who want to review every network state of a screen side by side.
- Teams building for markets where connectivity is unreliable.

## Design decisions

- **Why four states and not a raw connection type.** UI usually reacts to what the user can do (everything works, nothing works, be careful with data, expect delays), not to whether the radio is Wi-Fi or cellular. The states map to those UI decisions.
- **Why a fake monitor instead of simulating the network.** Tests stay fast and deterministic, and need no emulator network settings.
- **Why a helper instead of generating test files.** Generating test code needs a compiler plugin or symbol processor, which is too much for the time budget and hard to maintain. A single helper call gives most of the value with a fraction of the complexity.
- **Why Android first.** It is the platform with the largest reach for the target audience, and its connectivity APIs are well understood. iOS and desktop implementations are left as stubs on purpose rather than half-built.

## Scope

| Included | Not included yet |
|---|---|
| Shared network state model | Real iOS network monitoring |
| Android network monitor | Real bandwidth measurement for the Slow state |
| Fake monitor for tests | Automatic test file generation |
| Multi-state snapshot capture | Visual diff reports |
| Sample app with an offline banner | Published artifacts |

## Demo

The sample app shows a screen with an offline banner and a retry button.

1. Run the snapshot test and see four images generated, one per network state.
2. Break the offline banner on purpose.
3. Run the test again and watch it fail on the offline image only.

*(Add a GIF of this flow here.)*

## Project layout

- **Core module:** the network state model, the monitor interface and the Android implementation.
- **Testing module:** the fake monitor and the multi-state snapshot helper.
- **Sample app:** a small screen used for the demo and as usage documentation.

## Known limitations

- The Slow state is a label you set, not something measured from real traffic.
- Snapshot comparison is strict, so tiny rendering differences between machines can cause false failures. Run snapshots on the same environment you recorded them on.
- The Compose multiplatform UI test API used by the helper is experimental and may change between versions.

## Roadmap

- iOS monitor using the system path monitor.
- Real Slow detection from measured round-trip time.
- Tolerance settings for snapshot comparison.
- A side-by-side HTML report of all states for a screen.
- Test file generation, once a clean approach exists.

## Team

Built at the mobile developer conference hackathon by:

- *Micah Nyabuto*
- *Clency Christine*

## License

*Choose one before publishing (MIT or Apache 2.0 are common for libraries).*
>>>>>>> 7fafd3aca854883305835e8a3dde3ed40f85b598
