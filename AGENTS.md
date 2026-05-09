# AGENTS.md

## Project Shape
- ARMSX2 is primarily an Android app with a large native PCSX2-derived core under `app/src/main/cpp`.
- The active game selector and emulator UI are native Android Java/XML in `app/src/main/java` and `app/src/main/res`.
- The React Native files in `app_ui`, `App.js`, and related JS config are experimental and are only enabled with `-PenableRN=true`.

## Build And Verify
- Use the Gradle wrapper from the repo root.
- For Java/XML UI changes, prefer `./gradlew :app:compileDebugJavaWithJavac` or the Windows equivalent `.\gradlew.bat :app:compileDebugJavaWithJavac`.
- Full APK builds are heavier because they can touch the native C++ core.
- Do not add local signing keys, Discord credentials, generated `jniLibs`, `node_modules`, or other ignored build outputs.

## Android UI Notes
- Keep game-grid changes scoped to `MainActivity.java` and the `item_game*.xml` layouts unless navigation or settings behavior needs to move.
- Cover art defaults to the xlenore PS2 covers raw GitHub template. Preserve user overrides, but blank cover-source preferences should fall back to the hardcoded default.
- Cheat badges on game covers should represent real `.pnach` files in the app data `cheats` directory. Do not light these badges from widescreen, 60 FPS, compatibility, or other patch folders.

## Native Core Notes
- Treat `app/src/main/cpp/pcsx2` and third-party code as high-blast-radius. Keep edits small and verify with a native build when touching it.
- Prefer existing JNI bridges in `NativeApp.java`/`main.cpp` over adding new cross-boundary APIs casually.

## Style
- Match the existing Java style in nearby code, including defensive `try/catch` around optional Android platform calls.
- Use Android resources for UI text and drawables.
- Keep repo-wide refactors out of feature branches unless they are required for the change.
