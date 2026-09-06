# HealthConnect Clinic Experience Lab 

**AnalystLab Africa Experience Lab | Data Analytics Track | Tool: Power BI**

## Project Overview

HealthConnect Clinic is a fictional healthcare provider experiencing **missed appointments, inefficient use of appointment slots, and repetitive patient enquiries**.

The clinic aims to use **data and AI** to improve decision-making, reduce missed appointments, and enhance the patient support experience.

### Central Project Question

**How can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?**

As part of the Data Analytics track, Week 4 focused on understanding the appointment dataset, assessing data quality, identifying important variables, defining business questions, proposing KPIs, and establishing an analytical approach. Week 5 moved into practical implementation: data cleaning, KPI calculation, exploratory analysis, and an initial Power BI dashboard.

---

## Project Objectives

* Understand the HealthConnect business problem.
* Review and understand the appointment dataset.
* Validate dataset variables against the Data Dictionary.
* Assess data quality and consistency.
* Identify variables relevant to appointment attendance and no-shows.
* Define key business questions.
* Propose, then calculate, relevant KPIs.
* Build an initial Power BI dashboard and translate findings into recommendations.

---

## Dataset Overview

The **HealthConnect Appointment Dataset** contains fictional and anonymised appointment-level records used to study attendance behaviour and support a no-show reduction strategy.

* **Records:** 5,000 appointments
* **Variables:** 18 (original), 20 in the cleaned Week 5 version (2 additional missingness-flag columns)
* **Appointment period:** January 2025 – June 2026
* **Primary outcome:** `appointment_outcome`

### Main Variable Categories

| Category             | Variables                                                                           |
| -------------------- | ----------------------------------------------------------------------------------- |
| Patient Demographics | Gender, Age, Age Group                                                              |
| Appointment Details  | Appointment Type, Booking Date, Appointment Date, Appointment Day, Appointment Time |
| Booking Behaviour    | Booking Lead Days, Previous Appointments, Previous No-Shows                         |
| Reminders            | Reminder Sent, Reminder Channel                                                     |
| Logistics            | Distance to Clinic, Waiting Time                                                    |
| Outcome              | Appointment Outcome                                                                 |

---

## Appointment Outcome Breakdown

| Outcome   |     Count | % of Total |
| --------- | --------: | ---------: |
| No-Show   |     2,423 |      48.5% |
| Attended  |     2,314 |      46.3% |
| Cancelled |       263 |       5.3% |
| **Total** | **5,000** |   **100%** |

**Key observation:** No-shows are the largest single outcome category, making missed appointments a significant operational issue.

---

## Data Dictionary Review

All **18 variables** were reviewed against the HealthConnect Data Dictionary. Key variables identified for no-show analysis include age/age group, appointment type, booking lead days, previous appointments/no-shows, reminder sent/channel, distance to clinic, waiting time, and appointment outcome (the target). No undocumented or unexpected variables were identified.

---

## Data Quality Assessment & Week 5 Cleaning

| Check                       | Finding                             |
| ---------------------------- | ------------------------------------ |
| Missing Values               | Present in three fields (see below)  |
| Duplicate Records            | None identified                      |
| Appointment ID               | Unique across all 5,000 records      |
| Data Types                   | Consistent with the Data Dictionary  |
| Invalid/Inconsistent Values  | None identified                      |
| Potential Outliers           | None flagged                         |
| Outcome Categories           | Consistent with documented values    |

### Missing Values & How They Were Handled (Week 5)

| Variable                | Missing | Decision                                                   |
| ------------------------ | ------: | ----------------------------------------------------------- |
| `reminder_channel`       |   1,366 | Filled with `"No Reminder"` — matches `reminder_sent = No`   |
| `distance_to_clinic_km`  |      90 | Filled with median (8.7 km); flagged in `distance_was_missing` |
| `waiting_time_minutes`   |      60 | Filled with median (24 min); flagged in `waiting_time_was_missing` |

`Cancelled` appointments (263 records, 5.3%) were excluded from the No-Show Rate and Attendance Rate denominators, since a cancellation is a distinct outcome from a no-show, and tracked separately as a Cancellation Rate.

The cleaned dataset was saved separately as `HealthConnect_Appointment_Data_CLEANED.csv` — the original file was never modified.

---

## Business Questions

1. What proportion of appointments are missed?
2. Which patient or appointment characteristics are associated with no-shows?
3. Does reminder status and reminder channel relate to attendance?
4. Does waiting time influence attendance?
5. Does distance from the clinic relate to missed appointments?
6. How does previous no-show history relate to future attendance?

---

## KPIs — Calculated (Week 5)

| KPI                              | Result                                   | Business Question Answered                     |
| --------------------------------- | ----------------------------------------- | ------------------------------------------------ |
| Appointment No-Show Rate          | **51.2%**                                | How frequently are appointments missed? (Q1)    |
| Attendance Rate                   | **48.8%**                                | What proportion of appointments are attended?   |
| Reminder-Linked Attendance Rate   | 50.1% (reminder sent) vs 45.4% (none)    | Does reminder status relate to attendance? (Q3) |
| Repeat No-Show Rate               | 57.8% (prior no-show) vs 46.3% (none)    | Does history relate to future attendance? (Q6)  |

> **Appointment Slot Utilisation Rate**, proposed in Week 4, was dropped in Week 5 — the dataset only contains booked appointments with no record of total available slots, so it cannot be calculated from this data.

Cancellation Rate (5.3%) is tracked as operational context rather than a core KPI.

---

## Power BI Dashboard (Week 5)

<img width="1287" height="717" alt="Week 5 Dashboard" src="https://github.com/user-attachments/assets/63204fa7-1501-442d-b8ed-b0e7c3b22555" />

The dashboard includes KPI cards (No-Show Rate, Attendance Rate, Cancellation Rate), an outcome donut chart, and comparison bar charts for reminder status, prior no-show history, distance band, and waiting-time band, with a slicer for interactive filtering.

---

## Exploratory Data Analysis — Key Findings (Week 5)

* **Distance:** No-show rate rises steadily from 48.7% (0–5km) to 56.9% (15km+).
* **Prior no-show history:** 57.8% (has history) vs 46.3% (no history) — the strongest predictor found.
* **Reminders:** No Reminder has the highest no-show rate (54.6%); SMS has the lowest among all reminder channels (47.9%), ahead of Email (51.0%) and WhatsApp (52.7%).
* **Waiting time:** No meaningful relationship with no-shows (49.9%–52.6% across all bands).
* **Appointment type:** Follow-up appointments are missed more (54.2%) than General Consultations (49.1%).
* **Day of week:** Monday (53.1%) and Sunday (52.8%) run slightly higher than Friday (48.7%) and Tuesday (48.9%).

These are descriptive associations, not proof of causation.

---

## Business Recommendations

* Make SMS the default reminder channel; ensure every appointment has a reminder scheduled.
* Flag patients with prior no-show history for extra confirmation contact.
* Investigate transport support or telehealth options for patients 15km+ from the clinic.
* Review the follow-up appointment process specifically.
* Do not prioritise waiting-time reduction as a no-show intervention — no meaningful effect found here.

---

## Assumptions, Limitations & Risk

* The dataset is a fictional simulation; patterns are illustrative, not clinically validated.
* Slot Utilisation Rate could not be calculated — no total-slots field exists in the data.
* All relationships identified (distance, reminders, history) are correlational, not causal.
* The dataset omits operational factors such as staff availability or clinic capacity.
* Any extension to real patient data would require compliance with applicable healthcare data-protection requirements.

---

## Cross-Track Collaboration

Shared KPI results and segment-level no-show rates (prior history, distance, reminders) with the **Data Science track**, as candidate predictive features and as evidence supporting the exclusion of `Cancelled` appointments from their target variable definition.

---

## Tools Used

* **Power BI** – Data cleaning (Power Query), KPI development (DAX measures), and dashboarding
* **Microsoft Excel** – Data Dictionary review
* **CSV** – Appointment dataset (raw and cleaned versions)

---

## Repository Structure

```text
HealthConnect-Project/
│
├── README.md
│
├── week4/
│   ├── HealthConnect_Week4_Data_Analytics_Initial_Analysis.docx
│   └── Week4_Project_Summary.docx
│
├── week5/
│   ├── HealthConnect_Week5_Analytics_Report.docx
│   ├── Week5_Project_Summary.docx
│   └── HealthConnect_Appointment_Data_CLEANED.csv
│
├── data/
│   ├── HealthConnect_Appointment_Data.csv        (original, unmodified)
│   └── HealthConnect_Data_Dictionary.xlsx
│
└── screenshots/
    └── Power BI dashboard screenshots
```

---

## Project Status

**Current Stage:** Week 5 – Exploratory Analysis, KPI Development & Business Insights

### Completed

* Business problem understanding (Week 4)
* Dataset review, Data Dictionary validation, data-quality assessment (Week 4)
* Business question definition and KPI proposal (Week 4)
* Data cleaning with documented decisions (Week 5)
* KPI calculation and interpretation (Week 5)
* Exploratory data analysis across all key variables (Week 5)
* Power BI dashboard (KPI cards, outcome donut, segment comparison charts) (Week 5)
* Business insights and recommendations (Week 5)
* Cross-track collaboration with Data Science (Week 5)

### Next Stage

**Week 6 – Refine the dashboard, deepen relationship analysis, and align with Data Science track findings.**
