# SAMSON Hospital — Full-Stack Mobile Workspace

> **Note on Confidentiality:** This repository represents a comprehensive case of a proprietary medical system deployed within a secured, closed network. In compliance with NDA and healthcare regulations, the source code and production data are omitted. This document highlights the architecture, engineering challenges, and technical solutions.

SAMSON Hospital is an internal full-stack mobile solution designed for hospital physicians. It streamlines daily clinical workflows by integrating a modern mobile experience with a legacy Hospital Medical Information System (MIS).

## 🛠 Tech Stack
- **Mobile (Android):** Kotlin, Jetpack Compose, Navigation Compose, Retrofit, OkHttp, Coroutines.
- **Backend API:** Python 3.11, Django REST Framework.
- **Database / Legacy Integration:** MySQL / MariaDB.
- **Infrastructure & QA:** Linux (CentOS, RED OS, Astra Linux), Git, Postman.

---

## 🏛 Architecture Overview

The system acts as a non-intrusive metadata adapter over the legacy MIS database.

```text
[Android Client (Compose)] <---> [Django REST API Adapter] <---> [Legacy MIS DB (MySQL/MariaDB)]
                                                                <---> [Internal File Services]
```

### Key Architectural Principle
The mobile client **never modifies the base MIS schema**. Instead, the Django backend introspects the legacy DB metadata (`ActionPropertyType`) and translates it into a unified, dynamic REST model for the Android app.

---

## 🚀 Key Engineering Highlights & Solutions

### 1. Metadata-Driven Dynamic Forms
* **Challenge:** Hardcoding UI screens for dozens of medical forms (laboratory analyses, X-rays, specialist lookups) was unmaintainable.
* **Solution:** Developed a dynamic UI rendering engine. The backend reads `ActionPropertyType` definitions, maps value domains (including `rbThesaurus` constructors), and delivers a JSON layout contract. The Android app dynamically builds native Compose widgets based on this layout.

### 2. Desktop MIS Legacy Compatibility
* **Challenge:** Ensuring that actions performed on the mobile device instantly reflect in the desktop version used by the rest of the hospital staff.
* **Solution:** Mobile writes are directly bound to the core legacy `ActionProperty_*` structures, maintaining correct system states (`Assigned`, `Completed`) without breaking business constraints.

### 3. Resilient Offline-State & Closed-Network Operation
* **Challenge:** Hospital Wi-Fi zones can be highly unstable; public cloud SaaS solutions are strictly prohibited in the medical closed circuit.
* **Solution:** Built local caching for clinical diary drafts. The app allows seamless creation and auto-saving of offline drafts, safely syncing with the server once connection is re-established. The runtime environment has zero external internet dependencies.

---

## 📸 Interface Examples (Anonymized)
*Below are examples of how the production system structures complex doctor workflows.*

| Patient Menu & Authentication | Metadata-driven UI Forms | Medical Treatments History |
|---|---|---|
| <img src="screenshots/01_auth_and_menu.png" width="250"/> | <img src="screenshots/02_dynamic_forms.png" width="250"/> | <img src="screenshots/03_treatment_history.png" width="250"/> |

---

## 📄 Available Documentation
For a deeper dive into technical definitions and user flows, explore the `docs/` folder:
* [Architecture & Configuration Notes (EN)](docs/architecture_notes.md)
* [User Guide (RU)](docs/user_guide_ru.md) — *Contains localized step-by-step screens.*
