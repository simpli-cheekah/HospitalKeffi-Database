# 🏥 Hospital Database Design — General Hospital Keffi
### Microsoft Elevate AI Developers Program | DP-900: Azure Data Fundamentals

![Microsoft](https://img.shields.io/badge/Microsoft-Elevate_Program-0078D4?style=for-the-badge&logo=microsoft)
![SQLite](https://img.shields.io/badge/SQLite-Database-003B57?style=for-the-badge&logo=sqlite)
![Azure](https://img.shields.io/badge/Azure-SQL_Database-0089D6?style=for-the-badge&logo=microsoftazure)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

---

## 📋 Project Overview

General Hospital Keffi records approximately 200 patient visits per week across 8 wards using paper ledgers and an unmanaged Excel file. This project designs and builds a proper relational database to replace that system — eliminating duplicate records, inconsistent diagnosis naming, and the inability to generate structured reports.

This is a Capstone Project for the DP-900 (Azure Data Fundamentals) certification track, delivered by Data Science Nigeria in partnership with Microsoft.

---

## 🎯 Problem Statement

The existing Excel system at General Hospital Keffi suffers from three critical problems:

| Problem | Impact |
|---|---|
| Duplicate patient records | Same patient entered multiple times with different spellings |
| Inconsistent diagnosis naming | "Malaria", "malaria fever", "P. falciparum" all mean the same thing |
| No structured reporting | Cannot reliably answer "how many malaria cases this month?" |

---

## 🗄️ Database Design

The database contains 5 tables designed to reflect how the hospital actually operates:

```
Patients ──────┐
               ├──► Visits ──────► Diagnoses
Wards ─────────┤
               │
Staff ─────────┘
Wards ────────────► Staff
```

### Tables

| Table | Description | Rows (Test Data) |
|---|---|---|
| Patients | Personal details of each patient | 7 |
| Wards | The 6 hospital wards | 6 |
| Staff | Doctors and nurses | 7 |
| Visits | Every patient visit recorded | 8 |
| Diagnoses | Illness diagnoses using WHO ICD-10 codes | 8 |

---

## 🔑 Key Design Decisions

### 1. WHO ICD-10 Standard Codes
Instead of storing diagnosis names as free text (which causes inconsistency), this database uses the WHO International Classification of Diseases (ICD-10) standard codes. For example:
- Malaria → B54
- Appendicitis → K37
- Normal Delivery → O80

This means every staff member records the same illness the same way, enabling accurate reporting.

### 2. Separate Diagnoses Table
One key design trade-off was whether to store diagnosis data inside the Visits table or in a separate Diagnoses table. A separate table was chosen because:
- A single visit can result in multiple diagnoses (e.g., malaria AND anaemia)
- Storing multiple diagnoses as columns in Visits would create rigid limits
- A separate table follows proper database normalisation principles

### 3. Foreign Key Relationships
Every relationship between tables is enforced through foreign keys, making orphaned or inconsistent records structurally impossible — unlike Excel where any cell can contain anything.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| SQLite Browser | Free offline database tool used to build and test the database |
| Microsoft Azure SQL Database | Cloud service that would host this database in real deployment |
| WHO ICD-10 | International standard used for diagnosis codes |
| SQL | Language used to create tables and insert data |

---

## ☁️ Azure SQL Database Deployment Plan

In a real hospital deployment, this SQLite database would be migrated to Microsoft Azure SQL Database which provides:

- ✅ Multi-user access — all 8 wards access the database simultaneously
- ✅ Automatic backups — data backed up every 5–10 minutes
- ✅ Role-based security — nurses can add records but not delete them
- ✅ Scalability — handles growth from 200 to 2,000+ visits per week
- ✅ Integration — connects to Azure Data Factory and Power BI for reporting dashboards

---
## 📊 How This Database Beats Excel

### Problem 1: Duplicate Records
In Excel, Amina Bello can be entered 10 times with 10 different spellings. In this database, she exists once with patient_id = 1. All her visits reference that single ID.

### Problem 2: Inconsistent Diagnoses
In Excel, "Malaria" and "malaria fever" are treated as different illnesses. In this database, both are B54 — the same ICD-10 code — regardless of who enters it.

### Problem 3: Structured Reporting
In Excel, answering "Which doctor attended the most Emergency ward patients last month?" requires complex manual filtering. In this database, it's a single SQL JOIN query across Visits, Staff, and Wards tables.


---

## 📁 Project Files

```
📦 HospitalKeffi-Database
 ┣ 📄 README.md              — This file
 ┣ 📄 HospitalKeffi.db       — SQLite database file (open with SQLite Browser)
 ┗ 📊 index.html — Interactive data visualization dashboard
```

📂 Full submission documents & screenshots:
[View on Google Drive](https://drive.google.com/drive/folders/1tdVjmK43URncIhSS3lrM8Vs6YEYRINW1)

---

## 👤 Author

Nkemjika Chika

Microsoft Elevate AI Developers Program — Cohort 1

DP-900: Azure Data Fundamentals

---

## 🏆 Certification

This project was completed as part of the Microsoft Elevate AI Developers Program, delivered by Data Science Nigeria in partnership with Microsoft. Completion of this capstone project is a requirement for receiving the AI Developers Certificate of Participation.

---

*Built with real Nigerian context, real hospital data scenarios, and WHO international medical standards.*
