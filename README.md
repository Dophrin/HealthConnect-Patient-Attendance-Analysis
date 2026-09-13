# HealthConnect Clinic Experience Lab 

**AnalystLab Africa Experience Lab | Data Analytics Track | Tool: Power BI**

## Project Overview

HealthConnect Clinic is a fictional healthcare provider experiencing **missed appointments, inefficient use of appointment slots, and repetitive patient enquiries**.

The clinic aims to use **data and AI** to improve decision-making, reduce missed appointments, and enhance the patient support experience.

### Central Project Question

**How can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?**

As part of the Data Analytics track, Week 4 focused on understanding the appointment dataset, assessing data quality, identifying important variables, defining business questions, proposing KPIs, and establishing an analytical approach. Week 5 moved into practical implementation: data cleaning, KPI calculation, exploratory analysis, and an initial Power BI dashboard. Week 6 moved into deeper, validated analysis and cross-track integration, building on Week 5 rather than repeating it.

---

## Project Objectives

* Understand the HealthConnect business problem.
* Review and understand the appointment dataset.
* Validate dataset variables against the Data Dictionary.
* Assess data quality and consistency.
* Identify variables relevant to appointment attendance and no-shows.
* Define key business questions.
* Propose, then calculate, relevant KPIs.
* Build and iteratively improve a Power BI dashboard.
* Deepen and validate key findings, and integrate with other project tracks.

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

## KPIs — Calculated (Week 5, Validated in Week 6)

| KPI                              | Result                                   | Business Question Answered                     |
| --------------------------------- | ----------------------------------------- | ------------------------------------------------ |
| Appointment No-Show Rate          | **51.2%**                                | How frequently are appointments missed? (Q1)    |
| Attendance Rate                   | **48.8%**                                | What proportion of appointments are attended?   |
| Reminder-Linked Attendance Rate   | 50.1% (reminder sent) vs 45.4% (none)    | Does reminder status relate to attendance? (Q3) |
| Repeat No-Show Rate               | 57.8% (prior no-show) vs 46.3% (none)    | Does history relate to future attendance? (Q6)  |

> **Appointment Slot Utilisation Rate**, proposed in Week 4, was dropped in Week 5 — the dataset only contains booked appointments with no record of total available slots, so it cannot be calculated from this data.

Cancellation Rate (5.3%) is tracked as operational context rather than a core KPI. All four KPIs above were re-validated in Week 6 against a full effect-size ranking across every variable in the dataset and confirmed to still hold.

**New candidate KPI (Week 6): Lead-Time-Adjusted No-Show Rate** — No-Show Rate segmented by booking lead time, since the blended 51.2% figure masks a 34-point range depending on how far ahead the appointment was booked (see below).

---

## Power BI Dashboard (Week 5)

<img width="1287" height="717" alt="Week 5 Dashboard" src="https://github.com/user-attachments/assets/63204fa7-1501-442d-b8ed-b0e7c3b22555" />

The dashboard includes KPI cards (No-Show Rate, Attendance Rate, Cancellation Rate), an outcome donut chart, and comparison bar charts for reminder status, prior no-show history, distance band, and waiting-time band, with a slicer for interactive filtering.

---

## Power BI Dashboard (Week 6 — Deep Analysis)

<img width="642" height="378" alt="Week 6 Dashboard" src="https://github.com/user-attachments/assets/9b6189f1-ce13-4cfd-bb9b-329403cfab4c" />

Built on top of the Week 5 dashboard (not a rebuild) with an added **Booking Lead Time Band** chart, based on the strongest new finding from Week 6's deeper analysis (see below).

---

## Exploratory Data Analysis — Key Findings (Week 5)

* **Distance:** No-show rate rises steadily from 48.7% (0–5km) to 56.9% (15km+).
* **Prior no-show history:** 57.8% (has history) vs 46.3% (no history) — the strongest predictor found in Week 5.
* **Reminders:** No Reminder has the highest no-show rate (54.6%); SMS has the lowest among all reminder channels (47.9%), ahead of Email (51.0%) and WhatsApp (52.7%).
* **Waiting time:** No meaningful relationship with no-shows (49.9%–52.6% across all bands).
* **Appointment type:** Follow-up appointments are missed more (54.2%) than General Consultations (49.1%).
* **Day of week:** Monday (53.1%) and Sunday (52.8%) run slightly higher than Friday (48.7%) and Tuesday (48.9%).

These are descriptive associations, not proof of causation.

---

## Advanced Analysis — Key Findings (Week 6)

Week 6 re-examined every variable in the dataset (not just the ones covered in Week 5) using point-biserial correlation and effect-size ranking, to check whether anything important had been missed and whether the Week 5 conclusions still held.

* **Booking lead time is the strongest predictor of no-shows found in the entire project** — a variable not examined in Week 5. No-show rate rises from **29.5%** (booked 0–7 days ahead) to **63.9%** (booked 30+ days ahead), a 34.4-point spread — larger than distance or prior history.
* **Prior no-show history and distance were validated, not just repeated** — after checking against every other variable, they remain the two strongest *categorical* drivers (11.5 and 8.2-point spreads respectively), confirming the Week 5 conclusions were correct.
* **Gender showed a moderate effect (6.7 points)** not previously highlighted in Week 5 — worth monitoring, though smaller than lead time or history.
* **Waiting time was confirmed as the weakest driver** in the dataset after being checked against every other variable, not just the segments tested in Week 5.
* **Combined-risk segment identified:** patients with both prior no-show history and a 30+ day booking lead time represent a compounding high-risk group, worth a dedicated Week 7 follow-up.

---

## Business Recommendations

* Prioritise confirmation contact closer to the appointment date for anything booked 30+ days out — the highest-impact lever identified across two weeks of analysis (Week 6).
* Combine the lead-time and prior-history signals into a single "high-risk" flag for booking staff (Week 6).
* Make SMS the default reminder channel; ensure every appointment has a reminder scheduled (Week 5, retained).
* Flag patients with prior no-show history for extra confirmation contact (Week 5, retained).
* Investigate transport support or telehealth options for patients 15km+ from the clinic (Week 5, retained).
* Review the follow-up appointment process specifically (Week 5, retained).
* De-prioritise waiting-time-focused interventions — confirmed as the weakest lever after wider Week 6 testing.

---

## Assumptions, Limitations & Risk

* The dataset is a fictional simulation; patterns are illustrative, not clinically validated.
* Slot Utilisation Rate could not be calculated — no total-slots field exists in the data.
* All relationships identified (distance, reminders, history, lead time) are correlational, not causal.
* The dataset omits operational factors such as staff availability or clinic capacity.
* The booking-lead-time effect and reminder timing cannot yet be fully separated, since the dataset does not record reminder timing relative to lead time (Week 6).
* Gender categories are unevenly sized, so that effect size should be treated cautiously pending a larger sample (Week 6).
* Any extension to real patient data would require compliance with applicable healthcare data-protection requirements.

---

## Cross-Track Collaboration

**Week 5:** Shared KPI results and segment-level no-show rates (prior history, distance, reminders) with the **Data Science track**, as candidate predictive features and as evidence supporting the exclusion of `Cancelled` appointments from their target variable definition.

**Week 6:** Attempted direct coordination with the Data Science track to exchange findings; the track was not available/willing to collaborate this week. A standalone **Feature-Relevance Handoff Note** was prepared regardless, ranking all dataset variables by their measured effect on no-shows (booking lead time, prior no-show history, and distance ranked highest), so the analytical output exists and is usable by that track whenever they are able to engage with it. This is documented honestly as a one-directional integration activity rather than a completed two-way exchange.

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
├── week6/
│   ├── HealthConnect_Week6_Advanced_Analytics_Report.docx
│   ├── Feature_Relevance_Handoff_Note.docx
│   └── Week6_Project_Summary.docx
│
├── data/
│   ├── HealthConnect_Appointment_Data.csv        (original, unmodified)
│   └── HealthConnect_Data_Dictionary.xlsx
│
└── screenshots/
    └── Power BI dashboard screenshots (Week 5 and Week 6)
```

---

## Project Status

**Current Stage:** Week 6 – Advanced Analytics, Decision Support & Cross-Track Integration

### Completed

* Business problem understanding (Week 4)
* Dataset review, Data Dictionary validation, data-quality assessment (Week 4)
* Business question definition and KPI proposal (Week 4)
* Data cleaning with documented decisions (Week 5)
* KPI calculation and interpretation (Week 5)
* Exploratory data analysis across all key variables (Week 5)
* Power BI dashboard (KPI cards, outcome donut, segment comparison charts) (Week 5)
* Business insights and recommendations (Week 5)
* Cross-track collaboration attempt with Data Science (Week 5)
* Full-dataset correlation and effect-size validation of Week 5 findings (Week 6)
* Discovery of booking lead time as the strongest no-show predictor in the project (Week 6)
* Dashboard extended with a new Lead Time Band chart (Week 6)
* Feature-Relevance Handoff Note prepared for Data Science (Week 6)

### Next Stage

**Week 7 – Testing, refinement, and end-to-end validation; re-attempt Data Science integration using the handoff note.**
