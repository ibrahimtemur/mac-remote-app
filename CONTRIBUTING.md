# Contributing to Mac Remote

Thank you for your interest in contributing to **Mac Remote**! We welcome all contributions, including bug reports, feature requests, documentation improvements, and code changes.

---

## 🧭 Code of Conduct
This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

---

## 🛠️ Development Setup

Mac Remote is structured as a monorepo:
- `/mac-app`: macOS desktop server written in Python 3.9+ with PyQt6 and CoreGraphics.
- `/android-app`: Android client application written in Kotlin and Jetpack Compose.

### macOS App Setup
1. Prerequisites: macOS 12+ (tested on Sequoia), Python 3.9+.
2. Navigate to `mac-app`:
   ```bash
   cd mac-app
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```
3. Run in development mode:
   ```bash
   ./run.sh
   ```

### Android App Setup
1. Prerequisites: Android Studio Hedgehog or newer, JDK 17+.
2. Open `/android-app` in Android Studio or build via CLI:
   ```bash
   cd android-app
   ./gradlew assembleDebug
   ```

---

## 🔀 Workflow & Pull Requests

1. **Fork the repository** on GitHub.
2. **Create a branch** for your feature or bugfix:
   ```bash
   git checkout -b feature/my-new-feature
   ```
3. **Commit your changes**:
   - Write clear, concise commit messages following the Conventional Commits format (e.g., `feat: add swipe gestures`, `fix: prevent ngrok duplicate process`).
4. **Ensure code quality**:
   - Verify that both macOS and Android builds pass locally without errors.
   - Do NOT commit sensitive keys, personal tokens, or build artifacts.
5. **Open a Pull Request**:
   - Target the `main` branch.
   - Provide a clear description of the changes made and any relevant screenshots/screen recordings.

---

## 🐞 Reporting Bugs
- Use the [Bug Report Template](.github/ISSUE_TEMPLATE/bug_report.md).
- Specify your macOS version, Android version, and device models.
- Include console logs from both the Mac server and the Android app if applicable.

---

## 💡 Suggesting Enhancements
- Use the [Feature Request Template](.github/ISSUE_TEMPLATE/feature_request.md).
- Clearly explain the problem you are trying to solve and how the proposed feature addresses it.
