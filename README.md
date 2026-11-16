# Advocate Client Manager — Android App

A full native Android application built with **Kotlin** and **Jetpack Compose**, replicating all functionality from the desktop Python application (`AdvocateClientManager.pyw`).

---

## 🏛 Features

1. **Dual Court Database Architecture**:
   - Independent databases for **High Court** and **District Court**.
   - Instant switching between court databases via top tabs.
   - Separate, customizable matter types for each court section.

2. **Client Management**:
   - Add, edit, search, and delete clients.
   - Search by client name, phone number, email address, or matter details (case number, party, district).
   - Real-time active case count badge for each client.

3. **Case / Matter Management**:
   - Matter types (Civil/Criminal Writ Petition, Appeals, Bail Applications, Regular Suits, Darkhast, etc.).
   - Full case attributes: Case No, Party Names (Title), Bench, Court, District, Opposite Party, Appearing For (Petitioner / Respondent No.), Filing Date, VP Date, Next Hearing Date, Disposal Date.
   - Case status tags: **Pending**, **Hearing**, **Judgment Reserved**, **Disposed** (distinct color coding: green for pending, red/italic for disposed).
   - Client transfer option when editing a matter.

4. **Date-wise Payment Register (Financials)**:
   - Tracks agreed professional fees and out-of-pocket expenses per case.
   - Date-wise receipt ledger (record payment date, amount, payment mode/remarks).
   - Real-time recalculation of total fees, amount received, and remaining balance due.
   - **WhatsApp Reminder Integration**: One-click button generates a pre-formatted, polite payment reminder message and opens WhatsApp with the client's phone number (`https://wa.me/...`).

5. **Matter Proceedings / Stage Register**:
   - Date-wise court proceeding history (Admission, W.S., Reply, Say, Evidence, Arguments, Orders, etc.).
   - Backdated entries support for recording past dates and court remarks.
   - Add, modify, or delete proceeding records.

6. **Hearing Register & Interactive Calendar**:
   - **Hearings Screen**: Filter upcoming hearings (Next 7 days, 14 days, 30 days, or all upcoming).
   - **Monthly Calendar**: Month-by-month grid displaying matter counts on scheduled dates. Tapping any day highlights hearings and disposal events scheduled for that date.

7. **eCourts Import (My Cases)**:
   - Import eCourts mobile app exports (`.txt` or `.json`).
   - Auto-detects whether the file contains High Court (`HCBM`) or District Court (`MH`) matters.
   - **Mode 1 (Sync)**: Updates status and next hearing dates without overwriting existing client/party details.
   - **Mode 2 (New)**: Imports new cases into the client database.

8. **Export & Backup**:
   - **CSV Export**: Exports client info and all attached matters with full details to CSV and triggers Android's native share sheet.
   - **ZIP Backup & Restore**: Creates complete zip backups of both SQLite databases and supports restoring from zip.
   - **Factory Reset**: Safety-gated with the exact confirmation phrase (`RESET HIGH COURT` / `RESET DISTRICT COURT`) before wiping court data.

---

## 📂 Project Architecture

```
AdvocateClientManager/
├── app/
│   ├── build.gradle.kts
│   ├── proguard-rules.pro
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/advocate/clientmanager/
│       │   ├── AdvocateApp.kt               // Application class, initializes Room DBs & matter types
│       │   ├── MainActivity.kt              // Single activity setup
│       │   ├── data/
│       │   │   ├── AppDatabase.kt           // Room database for High Court & District Court
│       │   │   ├── entity/                  // Client, Case, CasePayment, CaseProceeding, etc.
│       │   │   ├── dao/                     // DAOs for Room operations
│       │   │   └── repository/              // Unified repository layer
│       │   ├── ui/
│       │   │   ├── navigation/NavGraph.kt   // Jetpack Compose Navigation routes
│       │   │   ├── theme/                   // Black/Cream theme matching desktop palette
│       │   │   ├── components/              // TopBar, DatePickerField, ConfirmDialog, EmptyState
│       │   │   └── screens/
│       │   │       ├── HomeScreen.kt
│       │   │       ├── AddEditClientScreen.kt
│       │   │       ├── AddEditCaseScreen.kt
│       │   │       ├── CaseDetailScreen.kt
│       │   │       ├── HearingsScreen.kt
│       │   │       ├── CalendarScreen.kt
│       │   │       ├── FeesScreen.kt
│       │   │       ├── PaymentRegisterScreen.kt
│       │   │       ├── ProceedingsScreen.kt
│       │   │       ├── SettingsScreen.kt
│       │   │       ├── MatterTypesScreen.kt
│       │   │       └── EcourtsImportScreen.kt
│       │   └── util/                        // DateUtils, MoneyUtils, Constants, CsvExporter, EcourtsImporter, BackupManager
│       └── res/
│           ├── values/strings.xml, themes.xml
│           └── xml/file_paths.xml           // FileProvider paths for sharing CSV & backups
├── build.gradle.kts
├── settings.gradle.kts
└── gradle.properties
```

---

## 🚀 How to Open and Run in Android Studio

1. Open **Android Studio**.
2. Select **File > Open...** and navigate to:
   `C:\Users\LENOVO\.gemini\antigravity\scratch\AdvocateClientManager`
3. Allow Gradle to sync the dependencies (requires internet connection on first sync).
4. Connect an Android device with USB debugging enabled or launch an Android Virtual Device (AVD).
5. Click **Run > Run 'app'** (or press `Shift + F10`).

---

## 🛠 Tech Stack
- **Language**: Kotlin 1.9.21
- **UI Framework**: Jetpack Compose with Material 3
- **Local Persistence**: Room SQLite Database (v2.6.1)
- **Architecture**: MVVM with Kotlin Coroutines & Flow
- **Minimum SDK**: Android 8.0 (API 26)
- **Target SDK**: Android 14 (API 34)
