# MY HISAB BOOK — Android starter project

This is a runnable React + TypeScript + Capacitor project with Ionic mobile UI and a SQLite adapter. It is a **starter implementation, not a fully production-ready finance product**. The dashboard, transaction entry, basic person/account creation and persistence scaffold are present. Features listed as future work below are not falsely represented as completed.

## Run in browser
1. Install Node.js 20+ and Android Studio (for APK).
2. In this folder: `npm install`
3. `npm run dev` (browser development; browser fallback stores records in localStorage).

## Create Android project / build
1. `npm run android:add`
2. `npm run android:sync`
3. `npm run android:open`
4. In Android Studio wait for Gradle sync; choose **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
5. Debug APK typically appears at `android/app/build/outputs/apk/debug/app-debug.apk`.
6. For a signed release: **Build > Generate Signed Bundle / APK > APK**, create and securely retain a keystore, choose release, then build. Never share the keystore/password.

Package ID: `com.myhisabbook.app`; app name: `MY HISAB BOOK`.

## Database / limitations to address before real financial use
- Native SQLite tables are initialized in `src/db/database.ts`. Its current query/CRUD helper is intentionally minimal; browser mode is only a localStorage development fallback. Complete migrations, prepared statements, robust update/delete and test coverage before release.
- Balance updating needs transaction-safe atomic logic, account-transfer handling, opening-balance and reconciliation flows. Never rely on the displayed total as audited accounting.
- No cloud backup provider configured. A real encrypted backup needs a backend/provider, authentication, encryption key management, conflict resolution and restore validation.
- Native notifications need permission prompt, timezone-aware schedule, rescheduling on edits and Android exact-alarm policy review.
- SMS gateway requires a provider account/API key and costs; no message is sent by this starter.
- Urdu/Roman Urdu voice command parsing needs native speech recognition and confirmation UX; not included.
- PDF/Excel export, PIN/biometric protection, full localization, attachment storage, obligations, complete reports, edit/delete, custom fields/categories and P&L business/personal classification remain to implement.
- Before publishing, perform security review, accounting tests, device tests, accessibility/localization checks and Play policy review.

## Common commands
`npm run build` — compile web app
`npm run android:sync` — rebuild web assets and sync native project

## Free GitHub Actions APK build
A workflow is included at `.github/workflows/android-apk.yml`.
1. Upload/push the complete project contents (including hidden `.github` folder) to a GitHub repository.
2. Open the repository's **Actions** tab and enable Actions if prompted.
3. Select **Build MY HISAB BOOK APK** and click **Run workflow** (or push to `main`).
4. When the run completes, open it and download the artifact named `my-hisab-book-debug-apk`.
5. Extract the artifact; it contains `app-debug.apk`. This is a debug APK, not a Play Store signed release.

GitHub Actions free usage is subject to GitHub's current account/usage limits. The workflow does not make unfinished app features production-ready.
