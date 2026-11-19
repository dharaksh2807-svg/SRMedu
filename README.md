# SRM Smart Study Hub

[![Live Platform](https://img.shields.io/badge/Live%20Platform-srmedu.in-f59e0b?style=for-the-badge&logo=googlechrome&logoColor=white)](https://www.srmedu.in/)
[![GitHub Repo](https://img.shields.io/badge/GitHub-srmedu.in-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/dharaksh2807-svg/srmedu.in)
[![PWA Ready](https://img.shields.io/badge/PWA-Installable-10b981?style=for-the-badge&logo=pwa&logoColor=white)](https://www.srmedu.in/)
[![Backend](https://img.shields.io/badge/Cloud-Firebase%20%7C%20Firestore-ffca28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com/)
[![AI Integration](https://img.shields.io/badge/AI%20Tutor-BYOK%20Multi--Model-8b5cf6?style=for-the-badge&logo=openai&logoColor=white)](https://www.srmedu.in/)
[![Hosting](https://img.shields.io/badge/Deploy-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com/)

> **SRM Smart Study Hub** is a data-driven, offline-first academic workspace and curriculum portal engineered for undergraduate engineering students following the SRM Institute of Science and Technology (SRM IST) syllabus. The platform consolidates modular lecture notes, mathematically prioritized Previous Year Questions (PYQs), interactive solution walkthroughs, formula cheat sheets, an advanced CGPA simulator, and an embedded multi-model AI study companion into a zero-friction, single-page interface.

---

## 📌 Institutional Disclaimer

**Smart Study Hub is an independent, student-run academic initiative.** It is **not** affiliated with, endorsed by, certified by, or officially associated with **SRM Institute of Science and Technology (SRM IST)** or any of its constituent colleges. Course codes, syllabi names, and past examination papers referenced on the platform are utilized exclusively for educational indexing, reference, and supplementary examination preparation under fair use.

---

## 📖 Table of Contents

- [Project Overview](#-project-overview)
- [System Architecture & Design Philosophy](#-system-architecture--design-philosophy)
- [Core Features](#-core-features)
  - [1. Data-Driven Exam Intelligence & Analytics](#1-data-driven-exam-intelligence--analytics)
  - [2. Dual-Tier Previous Year Questions (PYQ) Arsenal](#2-dual-tier-previous-year-questions-pyq-arsenal)
  - [3. Modular Academic Notes & Cloud Drive Streaming](#3-modular-academic-notes--cloud-drive-streaming)
  - [4. Embedded "Smart Panel" (AI Tutor, Live Compiler & Scratchpad)](#4-embedded-smart-panel-ai-tutor-live-compiler--scratchpad)
  - [5. Active Recall Practice, Quizzes & Formula Vault](#5-active-recall-practice-quizzes--formula-vault)
  - [6. Advanced CGPA Calculator & Goal Predictor](#6-advanced-cgpa-calculator--goal-predictor)
  - [7. Client-First State, Google Sign-In & Cloud Sync](#7-client-first-state-google-sign-in--cloud-sync)
  - [8. Theme Customization & Progressive Web App (PWA)](#8-theme-customization--progressive-web-app-pwa)
- [Curriculum & Semester Coverage](#-curriculum--semester-coverage)
- [Technology Stack](#-technology-stack)
- [Directory Structure](#-directory-structure)
- [Security, Key Management & Privacy](#-security-key-management--privacy)
- [Local Setup & Development](#-local-setup--development)
- [Build & Maintenance Utilities](#-build--maintenance-utilities)
- [Roadmap & Planned Features](#-roadmap--planned-features)
- [Contributing](#-contributing)
- [License & Contact](#-license--contact)

---

## 💡 Project Overview

### The Problem
Undergraduate engineering students frequently face acute academic friction due to scattered learning materials:
1. **Resource Fragmentation**: Study materials, past papers, and presentation decks are splintered across Google Drive links, WhatsApp groups, and student portals.
2. **Context Switching**: Reviewing code requires external IDEs, verifying mathematics demands external calculators, and clearing doubts involves external LLM tabs.
3. **Information Overload**: Heavy, 500-page academic textbooks make strategic, time-sensitive examination revision inefficient.
4. **Opaque Question Patterns**: Students study without insight into which concepts are recurring across university cycles.

### The Solution
Smart Study Hub standardizes course content into an integrated, high-performance dashboard. It combines curated modular course breakdowns (Units 1 to 5) with data-backed recurrence analytics, instant formula lookups, self-checking PYQ drills, and on-demand artificial intelligence, all accessible through the browser on mobile or desktop without mandatory authentication.

---

## 🏗️ System Architecture & Design Philosophy

Smart Study Hub is built on three architectural principles: **Zero Runtime Overhead**, **Guest-First Persistence**, and **Client-Side Security**.

```
┌────────────────────────────────────────────────────────────────────────┐
│                        SRM SMART STUDY HUB (Client)                    │
│                                                                        │
│   ┌─────────────────────┐   ┌─────────────────┐   ┌────────────────┐   │
│   │   Index Dashboard   │   │  Subject Hubs   │   │ CGPA Simulator │   │
│   │ (Search & Semesters)│   │ (Units 1-5 DOM) │   │ (10-Point Scale│   │
│   └──────────┬──────────┘   └────────┬────────┘   └────────────────┘   │
│              │                       │                                 │
│   ┌──────────┴───────────────────────┴─────────────────────────────┐   │
│   │                 Core Shared Engine (`/shared/`)                │   │
│   │  • search-engine.js      • unit-renderer.js  • app.js          │   │
│   │  • pyq-controller.js     • themes_config.js  • notes-panel.js  │   │
│   └──────┬───────────────────────┬─────────────────────────┬───────┘   │
│          │                       │                         │           │
│   ┌──────┴──────────────┐ ┌──────┴──────────────┐   ┌──────┴───────┐   │
│   │  ProgressManager    │ │  AuthManager        │   │ AI Assistant │   │
│   │  (localStorage)     │ │  (Firebase Auth/DB) │   │ (BYOK API)   │   │
│   └──────┬──────────────┘ └──────┬──────────────┘   └──────┬───────┘   │
└──────────┼───────────────────────┼─────────────────────────┼───────────┘
           │                       │                         │
     Browser Storage               │                   sessionStorage
     (Offline-First)               ▼                   (Keys Wiped)
                    ┌──────────────────────────────┐         │
                    │   Google Cloud & Firebase    │         ▼
                    │ • Cloud Firestore (Progress) │   Direct API Calls
                    │ • Google Drive API v3 (Files)│  (Gemini/Claude/GPT)
                    │ • Firebase Auth (Google SSO) │
                    └──────────────────────────────┘
```

1. **Native Web Stack**: Engineered with vanilla HTML5, CSS3 Custom Properties, and modular ES6 JavaScript. The application runs with zero framework overhead, ensuring sub-second initial loads and smooth 60fps rendering even on low-powered mobile devices.
2. **Guest-First, Offline-First**: Every core feature (notes, formulas, PYQs, calculators, progress checklists) executes entirely in the browser using `localStorage`. Cloud authentication is strictly opt-in for multi-device synchronization.
3. **Service Worker Layer (`sw.js`)**: Employs a Cache-First strategy for static stylesheets, scripts, and fonts, paired with a Network-First strategy and offline page fallback (`offline.html`) for dynamic documents.
4. **BYOK Security Barrier**: AI study assistant keys are stored strictly in `sessionStorage` (cleared automatically upon tab closure), preventing credential leakage into persistent storage.

---

## ⚡ Core Features

### 1. Data-Driven Exam Intelligence & Analytics
- **Pareto 80/20 Analysis**: Course content is mapped to historical question appearances to isolate the 20% of syllabus topics that yield 80% of exam marks.
- **Topic Recurrence Heatmaps**: Interactive heatmaps (`HEATMAP_DATA`) indicate how frequently specific topics appeared across historical university cycles (e.g., `7/8 papers`), highlighted with severity-coded color bars.
- **Exam Predictions**: Data-driven prediction cards identify high-probability question formats (rated *Very High*, *High*, or *Medium*) for upcoming Cycle Tests (CTs) and Semester Finals.

### 2. Dual-Tier Previous Year Questions (PYQ) Arsenal
- **Tier 1: Interactive Solved Papers**: Fully solved past semester examination papers featuring step-by-step mathematical solutions, embedded diagrams, and collapsible `<details>` dropdowns for self-evaluation.
- **Tier 2: Original Question Paper Vault**: Direct catalog of blank, original question papers covering Cycle Tests (CT-1, CT-2, CT-3), Model Exams, and End-Semester papers streamed from cloud storage with automatic title normalization.
- **Subject-Specific PYQ Viewer**: Dedicated full-screen viewing mode (`pyq_viewer.html`) with printable view and focus settings.

### 3. Modular Academic Notes & Cloud Drive Streaming
- **Structured 5-Unit Breakdown**: Complete coverage of standard 5-unit university syllabi organized in accordion hierarchies.
- **Dynamic Google Drive Ingestion**: Real-time integration via Google Drive API v3 (`notes-panel.js`) to stream verified lecture presentations, professor handouts, and student notes directly within the browser.
- **Static Fallback Resilience**: Equipped with a 2.5-second connection timeout guard and pre-compiled local database cache (`notes_database.json`) to guarantee instant access even during cloud API rate limits or network drops.
- **Single-Click Downloads**: Direct download links for all PDFs, PPTs, and reference documents.

### 4. Embedded "Smart Panel" (AI Tutor, Live Compiler & Scratchpad)
A draggable, collapsible side drawer (`smartPanel`) available on subject pages:
- **BYOK Multi-Model AI Study Assistant (`ai-panel-v3.js`)**:
  - Connects to **Google Gemini** (*Gemini 3.8 Flash, 3.1 Pro, Flash Lite*), **Anthropic Claude** (*Opus 5.5, Sonnet 5, Haiku 4.5*), **OpenAI** (*GPT-6 Astra, Sol, Luna*), and **DeepSeek** (*V4 Pro, Flash*).
  - Context-aware prompt injection that automatically primes the model with the active subject name, course code, and curriculum type.
  - **Viva Exam Mode**: Interactive oral exam simulator that drills students with conceptual and scenario questions.
  - Starred responses saved per subject in local storage.
- **Integrated Code Compiler (`compiler-panel.js`)**:
  - Embedded OneCompiler execution sandbox supporting **C, C++, Java, and Python**.
  - **"Run This Code" One-Click Injections**: Interactive code snippets in programming notes inject directly into the compiler runner without manual copy-pasting.
- **Persistent Scratchpad**: Scratchpad tab for rough math, derivations, and draft algorithm tracing that auto-saves locally.

### 5. Active Recall Practice, Quizzes & Formula Vault
- **Gamified MCQs**: End-of-unit objective drills with randomized answer validation, detailed rationales, and score tracking.
- **Interactive Formula Vault**: Categorized mathematical identities, algorithm complexities, and engineering laws typeset with **MathJax 3** (`tex-svg.js`). Includes one-click formula copying and quick-pinning.
- **Progress Tracking & Checklists**: Topic-level completion checkboxes (`ProgressManager`), bookmarks, confidence ratings, and celebratory animations upon unit completion.
- **Data Portability**: Full JSON export and import capabilities to backup and restore study progress manually without an account.

### 6. Advanced CGPA Calculator & Goal Predictor
Located at `/cgpa.html`, tailored specifically to SRM IST academic regulations:
- **10-Point Grade Scale**: Configured with official SRM grade points:
  $$\text{O} = 10 \quad|\quad \text{A+} = 9 \quad|\quad \text{A} = 8 \quad|\quad \text{B+} = 7 \quad|\quad \text{B} = 6 \quad|\quad \text{C} = 5 \quad|\quad \text{P} = 4 \quad|\quad \text{F} = 0$$
- **Current Semester SGPA**: Dynamic course entry with credit-weighted calculations:
  $$\text{SGPA} = \frac{\sum (\text{Credit}_i \times \text{Grade Point}_i)}{\sum \text{Credit}_i}$$
- **Cumulative CGPA Simulator**: Supports both aggregate past credit calculation and semester-by-semester entry.
- **Target Grade Predictor**: Calculates the exact minimum GPA required across remaining semesters to achieve a target graduation CGPA, warning if mathematically unattainable.

### 7. Client-First State, Google Sign-In & Cloud Sync
- **Frictionless Guest Experience**: The platform is 100% functional without an account.
- **Optional Cloud Backup**: Optional Google Sign-In powered by Firebase Authentication (v10.14.1).
- **Non-Blocking Synchronization**: Asynchronously debounces and synchronizes local study checklist states, starred items, and personal notes to Cloud Firestore (`progress/{userId}`).
- **Community Discussion Board (`community-notes.js`)**: Real-time peer question-and-answer board powered by Firestore, featuring category tagging (*Doubt*, *Tip*, *Resource*, *General*), upvoting, threaded replies, and rate limiting.

### 8. Theme Customization & Progressive Web App (PWA)
- **23 Curated Themes Across 3 Tiers**:
  - *Tier 1 (Signature)*: Dark Academia (Canva library embed), Clean Dark, Refined Amber, Chalkboard Slate, Field Notebook, Observatory Midnight, Nord Frost, Cosmic Abyss, OLED Pure Black.
  - *Tier 2 (Ergonomic)*: Arctic Light, Minimalist Mono, Deep Ocean, Rose Gold, Pine Forest, Emerald Glass.
  - *Tier 3 (Creative)*: Warm Macchiato, Dracula, Monokai Pro, Solarized Light, Aurora Glass, Cobalt Blue, Amethyst Glass, Sakura Night.
- **Independent Scope Theming**: Allows distinct themes for the main dashboard (`home_theme_class`) and individual subject pages (`study_theme_class`).
- **PWA Capabilities**: Installable on Android, iOS, macOS, and Windows with custom app shortcuts, offline asset caching, and standalone window display.
- **Real-Time Global Search**: Keyboard-activated (`/` or `⌘K` / `Ctrl+K`) dashboard filtering that queries course codes, titles, subject aliases, and curriculum keywords with instant DOM isolation.

---

## 📚 Curriculum & Semester Coverage

The platform maps to the **SRM IST B.Tech Regulations** (covering 2018 and 2021 curriculum regulations). Subject data is categorized into three implementation tiers:

| Semester | Subjects Listed | Key Covered Courses | Implementation Status |
| :---: | :---: | :--- | :---: |
| **Semester 1** | 20 Courses | Engineering Chemistry (`21CHC101J`), Calculus & Linear Algebra (`21MAB101T`), Programming for Problem Solving (`21CSC101T`), Philosophy of Engineering (`21EES101T`), Computational Biology (`21CSC102J`), Foreign Languages (French, German, Spanish, Japanese, Chinese, Korean) | **Production Active** *(Full Notes + Solved PYQs)* |
| **Semester 2** | 10 Courses | Semiconductor Physics (`21PYB102J`), Electrical & Electronics Eng (`21EES101J`), Object-Oriented Design & Programming (`21CSC102J`), Advanced Calculus & Complex Analysis (`21MAB102T`), Communicative English (`21LEH101T`) | **Production Active** *(Full Notes + Solved PYQs)* |
| **Semester 3** | 16 Courses | Data Structures & Algorithms (`21CSC201J`), Operating Systems (`21CSC205J`), Computer Organization & Architecture (`21CSC202J`), Advanced Programming Practice / Java, Foundation of Data Science (`21CSC203J`), Transforms & Boundary Value Problems (`21MAB201T`), Universal Human Values | **Production Active** *(Full Notes, Heatmaps, PYQs & Compilers)* |
| **Semester 4** | 14 Courses | Artificial Intelligence (`21CSC206T`), Database Management Systems (`21CSC204J`), Design & Analysis of Algorithms (`21CSC203J`), Computer Graphics & Applications (`21CSC204J`), Internet of Things (`21ECC201T`), Probability & Queueing Theory (`21MAB204T`) | **Core Active** *(CGA/DAA Complete; others Drive-integrated)* |
| **Semester 5** | 4 Courses | Computer Networks (`21CSC302J`), Discrete Mathematics (`21MAB301T`), Formal Languages & Automata Theory (`21CSC301T`), Full Stack Web Development (`21CSC303J`) | **Core Active** *(Full syllabi & solved sets)* |
| **Semester 6** | 3 Courses | Compiler Design (`21CSC304J`), Cloud Computing, Cryptography & Network Security | **In Development** *(Curriculum structure indexed)* |

---

## 🛠️ Technology Stack

| Category | Technology | Usage & Implementation Details |
| :--- | :--- | :--- |
| **Frontend Core** | **HTML5 & CSS3** | Semantic HTML5 structure, CSS Grid, Flexbox, Custom Properties (variables), Glassmorphism backdrop filters. Zero client JS frameworks. |
| **Scripting & Logic** | **Vanilla JavaScript (ES6+)** | IIFE modules, Singleton patterns, Custom Events, client-side routing, IntersectionObserver scrollspy, and DOM manipulation. |
| **Mathematics Rendering** | **MathJax 3 (`tex-svg.js`)** | Client-side LaTeX typesetting for complex integrals, formulas, and matrices with vector SVG outputs. |
| **Typography & Icons** | **Google Fonts & SVG** | *Inter*, *Outfit*, and *JetBrains Mono*; custom inline SVG graphics and icons. |
| **Cloud Authentication** | **Firebase Auth v10.14.1** | Lazy-loaded Google OAuth provider with token validation and guest-to-authenticated account binding. |
| **Cloud Database** | **Google Cloud Firestore** | Secure cloud synchronization of study progress (`/progress/{userId}`) and real-time community boards (`/community_notes`). |
| **Cloud File Storage** | **Google Drive API v3** | Direct dynamic indexing and document streaming from shared institutional storage folders. |
| **AI Integration** | **Multi-LLM Fetch API (BYOK)** | Direct browser-to-API calls for Google Gemini, Anthropic Claude, OpenAI, and DeepSeek with isolated `sessionStorage` credential management. |
| **Code Execution** | **OneCompiler API** | Secure sandboxed iframe runner supporting C, C++, Java, and Python with dynamic code injection. |
| **PWA & Offline** | **Service Worker API** | `sw.js` with Cache-First precaching of critical shell assets and Network-First offline fallback (`offline.html`). |
| **Deployment & CDN** | **Vercel** | Serverless global edge delivery with SSL/TLS, automated asset compression, and clean routing (`vercel.json`). |
| **Build Automation** | **Python 3** | Automated Drive metadata indexing (`scripts/build_notes_db.py`), analytics injection, and dataset schema validation. |

---

## 📂 Directory Structure

```text
srmedu.in/
├── assets/                       # Branding logos, platform icons, social cards
├── css/                          # Core dashboard stylesheets
│   └── dashboard.css             # Main portal grid, navigation, and hero animations
├── docs/                         # Technical protocols and internal documentation
│   └── KEY_ROTATION.md           # API key rotation, restriction, and compromise protocol
├── legal/                        # Transparency, terms, and compliance pages
│   ├── copyright.html            # Copyright & content attribution notice
│   ├── disclaimer.html           # Non-affiliation disclaimer and educational scope
│   ├── privacy.html              # Privacy policy and local storage disclosure
│   └── terms.html                # Terms of service
├── raw_materials/                # Historical source question papers, scanned tests & materials
├── scripts/                      # Developer maintenance scripts
│   ├── add_adsense.py            # Global monetization snippet manager
│   ├── add_gtag.py               # Google Analytics injection utility
│   └── build_notes_db.py         # Google Drive crawler & static JSON index builder
├── semester_1/ ... semester_6/   # Semester directories containing individual subject modules
│   └── [subject_slug]/           # e.g., semester_3/os/
│       ├── assets/               # Subject-specific diagrams and flowcharts
│       ├── data.js               # Syllabus topics, formulas, MCQs, and solved PYQ data
│       ├── index.html            # Interactive 5-unit subject study hub
│       ├── pyq_viewer.html       # Focused printable exam viewer
│       └── pyqs/                 # Standalone solved exam paper HTML modules
├── shared/                       # Global engine modules utilized across all pages
│   ├── ai-panel-v3.js            # BYOK multi-model AI assistant & Viva engine
│   ├── app.js                    # Subject page controller & view orchestration
│   ├── auth-manager.js           # Firebase Auth & Firestore synchronization singleton
│   ├── auth-ui.css               # Authentication modal & user avatar styling
│   ├── community-notes.js        # Real-time peer discussion board logic
│   ├── compiler-panel.js         # OneCompiler drawer controller & code runner
│   ├── notes-panel.js            # Google Drive dynamic document streaming client
│   ├── notes_config.js           # Google Drive folder IDs & MIME configuration
│   ├── notes_database.json       # Precompiled static fallback catalog of Drive notes
│   ├── pyq-controller.js         # Question paper title normalizer & exam viewer
│   ├── search-engine.js          # In-page global subject topic search engine
│   ├── storage-manager.js        # LocalStorage progress, bookmarks & export manager
│   ├── style.css                 # Universal design system, typography & utilities
│   ├── themes.css                # 23-theme palette definitions & glassmorphism tokens
│   ├── themes_config.js          # Theme gallery modal, previewer, and persistence
│   └── unit-renderer.js          # Accordion, LaTeX, heatmap & formula DOM generator
├── about.html                    # Mission statement, roadmap & team information
├── cgpa.html                     # SRM 10-point SGPA/CGPA calculator & predictor
├── firestore.rules               # Production Firestore database access control rules
├── guide.html                    # Interactive platform tour and user manual
├── index.html                    # Central university dashboard & subject navigator
├── manifest.json                 # Web App Manifest for PWA installation
├── offline.html                  # Network-disconnect fallback UI
├── package.json                  # Node.js dev dependencies (jsdom, ignore)
├── sw.js                         # Production Service Worker precache & fetch router
└── vercel.json                   # Edge routing, trailing slash, and header rules
```

---

## 🔒 Security, Key Management & Privacy

The platform implements rigorous security protocols to protect user data and API integrity:

### 1. Bring-Your-Own-Key (BYOK) Isolation (Protocol `SEC-KEY-001`)
- AI provider API keys (Google Gemini, Anthropic Claude, OpenAI, DeepSeek) entered by users are **never written to persistent storage (`localStorage` or cookies)** and **never transmitted to any intermediary backend**.
- Keys are saved exclusively in browser `sessionStorage`. When the tab or browser session is closed, keys are instantly discarded by the browser.
- A silent migration function checks for and destroys legacy persistent key instances.

### 2. Google Cloud Key Restrictions
- Publicly visible client API keys (used for Google Drive metadata fetching) are strictly locked in Google Cloud Console with HTTP Referrer Restrictions:
  ```text
  https://www.srmedu.in/*
  http://localhost:*
  http://127.0.0.1:*
  ```
- These keys are restricted exclusively to the **Google Drive API** and **Firebase Services**, preventing unauthorized quota usage.

### 3. Firestore Security Rules
Cloud Firestore operates under strict cryptographic identity verification (`firestore.rules`):
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Authenticated users can only read and write their own progress record
    match /progress/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    // Community notes: Read-only for public, authenticated writes with length checks
    match /community_notes/{noteId} {
      allow read: if true;
      allow create: if request.auth != null && request.resource.data.text.size() <= 500;
      allow update, delete: if request.auth != null && request.auth.uid == resource.data.userId;
    }
    // Catch-all: Explicitly deny all other paths
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

---

## 💻 Local Setup & Development

Because Smart Study Hub utilizes a vanilla web architecture, it requires no complex compiler pipelines, bundlers, or heavy runtime dependencies.

### Prerequisites
- A modern web browser (Google Chrome, Firefox, Safari, or Edge)
- Python 3.8+ (for local HTTP serving and maintenance scripts)
- Git

### 1. Clone the Repository
```bash
git clone https://github.com/dharaksh2807-svg/srmedu.in.git
cd srmedu.in
```

### 2. Start a Local Development Server
Because Service Workers and ES6 module features require a secure origin (`http://localhost` or `https://`), run a local web server from the project root:

**Using Python 3:**
```bash
python3 -m http.server 3000
```

**Using Node.js:**
```bash
npx serve . -l 3000
```

Open your browser and navigate to:
```text
http://localhost:3000
```

### 3. Optional: Configure Development Firebase Credentials
If testing cloud authentication and Firestore synchronization locally, ensure `localhost:3000` is added to your **Firebase Console > Authentication > Settings > Authorized Domains**.

---

## ⚙️ Build & Maintenance Utilities

The `/scripts/` directory contains automation tools for maintaining datasets:

### Rebuilding the Google Drive Offline Fallback Database
To crawl configured Google Drive subject folders and update the local static catalog (`shared/notes_database.json`):
```bash
python3 scripts/build_notes_db.py
```
*This parses `shared/notes_config.js`, verifies active Google Drive folder IDs, fetches file metadata via Google Drive API v3, and compiles a unified JSON database.*

---

## 🗺️ Roadmap & Known Limitations

### Confirmed Operational Features
- [x] Responsive 6-semester central dashboard with instant keyword filtering
- [x] Comprehensive 5-unit study modules for core Semester 1–5 subjects
- [x] Interactive step-by-step solved PYQ modules with solution toggling
- [x] Pareto 80/20 exam analysis and recurrence heatmaps
- [x] SRM 10-point GPA calculator and cumulative target simulator
- [x] Multi-model BYOK AI Study Assistant with Viva examination mode
- [x] OneCompiler live code execution drawer for C, C++, Java, and Python
- [x] 23 custom study themes with scoped persistence
- [x] PWA offline caching and standalone installation
- [x] Optional Google Sign-In with Firestore study checklist synchronization

### Development Roadmap
- [ ] **Curriculum Regulation Selector**: Dynamic filtering for 2018 vs. 2021 curriculum differences.
- [ ] **Branch Filter**: Dropdown filtering to isolate CSE, ECE, Mechanical, and Biotechnology specializations.
- [ ] **Unit-Level Discussion Threads**: Direct peer-to-peer contextual comments underneath specific topics.
- [ ] **Expanded Semester 6 Datasets**: Complete interactive `data.js` authoring for Cloud Computing, Cryptography, and remaining upper-level electives.

---

## 🤝 Contributing

Contributions to Smart Study Hub are welcomed, particularly in verifying solutions, improving mathematical explanations, and expanding curriculum coverage:

1. **Reporting Errors**: If you identify an error in a formula sheet, an inaccurate PYQ solution, or a broken download link, please open an issue on the [srmedu.in Issue Tracker](https://github.com/dharaksh2807-svg/srmedu.in/issues).
2. **Adding Solutions**: Solutions to past question papers must be submitted with full step-by-step mathematical working and explanatory derivations.
3. **Adding Subjects**: New subjects must adhere to the standardized `data.js` schema (`UNIT_DATA`, `FORMULA_DATA`, `MCQ_DATA`, `HEATMAP_DATA`, `PYQ_DATA`).

---

## 📄 License & Contact

- **Copyright**: © 2026 Smart Study Hub. All rights reserved.
- **Source Code**: Distributed under proprietary terms for educational use.
- **Support & Inquiries**: Reach out via email at [`srmeduhelp@gmail.com`](mailto:srmeduhelp@gmail.com) or on Instagram at [`@srmedu.in`](https://www.instagram.com/srmedu.in).
```

---
