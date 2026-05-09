# AGENTS.md

## Project Shape
- ARMSX2 is primarily an Android app with a large native PCSX2-derived core under `app/src/main/cpp`.
- The active game selector and emulator UI are native Android Java/XML in `app/src/main/java` and `app/src/main/res`.
- The React Native files in `app_ui`, `App.js`, and related JS config are experimental and are only enabled with `-PenableRN=true`.

## Build And Verify
- Use the Gradle wrapper from the repo root.
- For Java/XML UI changes, prefer `./gradlew :app:compileDebugJavaWithJavac` or the Windows equivalent `.\gradlew.bat :app:compileDebugJavaWithJavac`.
- A JDK is required. If Gradle reports `JAVA_HOME is not set and no 'java' command could be found`, install or point `JAVA_HOME` at a JDK before treating verification as a code failure.
- Full APK builds are heavier because they can touch the native C++ core.
- If a compile cannot run locally, still run `git diff --check` and parse touched XML resources to catch whitespace and resource syntax issues.
- Do not add local signing keys, Discord credentials, generated `jniLibs`, `node_modules`, or other ignored build outputs.

## Local Tooling
- Prefer `rg` for search when available. If the bundled Windows `rg.exe` is blocked, use `git grep` inside the repo.
- PowerShell may not accept Unix-style `&&` command chaining in this environment. Run separate commands or use native PowerShell syntax.
- Network access and SSH Git remotes are expected to work; this repo was cloned from `git@github.com:noeldvictor/ARMSX2.git`.

## Git Workflow
- After completing requested code or documentation changes, commit and push the branch unless the user explicitly asks not to.
- Keep commit messages short and specific to the completed change.

## Android UI Notes
- Keep game-grid changes scoped to `MainActivity.java` and the `item_game*.xml` layouts unless navigation or settings behavior needs to move.
- Cover art defaults to the xlenore PS2 covers raw GitHub template. Preserve user overrides, but blank cover-source preferences should fall back to the hardcoded default.
- Cheat badges on game covers should represent real `.pnach` files in the app data `cheats` directory. Do not light these badges from widescreen, 60 FPS, compatibility, or other patch folders.
- Individual cheat toggles are named PNACH sections. Keep them name-based and sourced from the active game's cheat list; do not mix in widescreen or 60 FPS patch metadata.
- When cheat files are imported, refresh any cached PNACH index and notify the game adapter so cover badges update without restarting the app.

## Native Core Notes
- Treat `app/src/main/cpp/pcsx2` and third-party code as high-blast-radius. Keep edits small and verify with a native build when touching it.
- Prefer existing JNI bridges in `NativeApp.java`/`main.cpp` over adding new cross-boundary APIs casually.

## Style
- Match the existing Java style in nearby code, including defensive `try/catch` around optional Android platform calls.
- Use Android resources for UI text and drawables.
- Keep repo-wide refactors out of feature branches unless they are required for the change.
