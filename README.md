# SAMSON Hospital — Full-Stack Mobile Workspace 

> **NDA & Confidentiality Notice:** This repository provides a technical case study of a proprietary medical system currently undergoing pre-release testing in a closed network at a healthcare facility in Krasnodar, Russia. To comply with strict medical regulations and non-disclosure agreements, production source code and database credentials are fully omitted. 

SAMSON Hospital is a production-ready internal full-stack mobile application designed for hospital physicians. It streamlines daily clinical operations by integrating a modern mobile workspace directly with an enterprise Hospital Medical Information System (MIS).

## 🛠 Tech Stack
- **Mobile (Android):** Kotlin, Jetpack Compose, Navigation Compose, Retrofit, OkHttp, Coroutines.
- **Backend API:** Python 3.11, Django REST Framework.
- **Database & Architecture:** MySQL / MariaDB (Legacy & Modern deployments).
- **Infrastructure & Environment:** Linux (CentOS, RED OS, Astra Linux), Git, Postman.

---

## 📊 Comprehensive Project Presentation
A detailed, fully anonymized visual walkthrough of the system, including its screens, interactive elements, and patient management workflows, is available in the attached presentation file. 

**Review or download the full document here:**
👉 **[SAMSON_Hospital_Portfolio_2026.pdf](SAMSON_Hospital_Portfolio_2026.pdf)** *(or look at the PowerPoint version in the root directory)*

---

## 🏛 Architecture Overview

The system operates as a high-performance, non-intrusive metadata adapter over the active MIS infrastructure.

```text
[Android Client (Compose)] <---> [Django REST API Adapter] <---> [Legacy MIS DB (MySQL/MariaDB)]
                                                                <---> [Internal File Services]
```

### Key Architectural Principle
The mobile client **never modifies or alters the base MIS database schema**. Instead, the Django-based backend dynamically introspects legacy tables and `ActionPropertyType` metadata, translating them into a unified, lightweight REST contract for native rendering on the mobile app.

---

## 🚀 Key Engineering Highlights & Solutions

### 1. Metadata-Driven Dynamic Forms
* **Challenge:** Hardcoding UI screens for an expanding list of medical forms (laboratory analyses, X-ray parameters, specialized gynecological lookups) was highly unmaintainable and restricted flexibility.
* **Solution:** Engineered a dynamic UI rendering engine. The backend reads metadata definitions, dynamically maps complex value domains (including `rbThesaurus` constructors), and outputs a structured JSON layout. The Android client evaluates this contract at runtime and dynamically builds native Compose widgets.

### 2. Live Desktop MIS Compatibility
* **Challenge:** Ensuring that any medical records or treatment paths initiated on a mobile device immediately synchronize with the desktop MIS client utilized by hospital departments.
* **Solution:** Designed backend write actions to map directly into core legacy `ActionProperty_*` structures. This preserves correct tracking states (`Assigned`, `Completed`) and integrity rules without breaking the existing desktop application workflows.

### 3. Fault-Tolerant Offline Drafts & Closed Circuit Operations
* **Challenge:** Hospital environments suffer from highly unstable Wi-Fi zones, and utilizing external cloud SaaS platforms is strictly prohibited due to healthcare data protection acts.
* **Solution:** Implemented local state persistence for clinical diary entries. Doctors can create, modify, and auto-save encrypted local drafts. Once the network connection is restored, the app securely syncs the queue back to the MIS server. The entire stack runs without any external internet dependencies.
