

# HealthConnect Clinic Experience Lab 

**AnalystLab Africa Experience Lab | Data Analytics Track | Tool: Power BI**

## Project Overview

HealthConnect Clinic is a fictional healthcare provider experiencing **missed appointments, inefficient use of appointment slots, and repetitive patient enquiries**.

The clinic aims to use **data and AI** to improve decision-making, reduce missed appointments, and enhance the patient support experience.

### Central Project Question

**How can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?**

As part of the Data Analytics track, Week 4 focused on understanding the appointment dataset, assessing data quality, identifying important variables, defining business questions, proposing KPIs, and establishing an analytical approach for deeper analysis in subsequent weeks.

---

## Project Objectives

* Understand the HealthConnect business problem.
* Review and understand the appointment dataset.
* Validate dataset variables against the Data Dictionary.
* Assess data quality and consistency.
* Identify variables relevant to appointment attendance and no-shows.
* Define key business questions.
* Propose and justify relevant KPIs.
* Establish an analytical approach for future Power BI analysis.

---

## Dataset Overview

The **HealthConnect Appointment Dataset** contains fictional and anonymised appointment-level records used to study attendance behaviour and support a no-show reduction strategy.

* **Records:** 5,000 appointments
* **Variables:** 18
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

**Key observation:** No-shows are the largest single outcome category, making missed appointments a significant operational issue for further investigation.

---

## Data Dictionary Review

All **18 variables** were reviewed against the HealthConnect Data Dictionary.

Key variables identified for no-show analysis include:

* **Age / Age Group** – investigates whether attendance differs across age groups.
* **Appointment Type** – examines whether no-show behaviour varies by visit type.
* **Booking Lead Days** – assesses whether booking further in advance relates to missed appointments.
* **Previous Appointments / Previous No-Shows** – investigates attendance history.
* **Reminder Sent / Reminder Channel** – examines the relationship between reminders and attendance.
* **Distance to Clinic** – investigates whether travel distance relates to missed appointments.
* **Waiting Time** – examines whether expected waiting time relates to attendance or cancellations.
* **Appointment Outcome** – serves as the primary outcome variable.

No undocumented or unexpected variables were identified.

---

## Initial Data Quality Assessment

| Check                       | Finding                             |
| --------------------------- | ----------------------------------- |
| Missing Values              | Present in three fields             |
| Duplicate Records           | None identified                     |
| Appointment ID              | Unique across all 5,000 records     |
| Data Types                  | Consistent with the Data Dictionary |
| Invalid/Inconsistent Values | None identified                     |
| Potential Outliers          | None flagged                        |
| Outcome Categories          | Consistent with documented values   |

### Missing Values

| Variable                | Missing Records | Assessment                            |
| ----------------------- | --------------: | ------------------------------------- |
| `reminder_channel`      |           1,366 | Expected because no reminder was sent |
| `distance_to_clinic_km` |              90 | Requires documented handling          |
| `waiting_time_minutes`  |              60 | Requires documented handling          |

The **1,366 missing `reminder_channel` values** correspond exactly to records where `reminder_sent = No`. This is therefore expected structure rather than a data-quality defect.

The missing values in `distance_to_clinic_km` and `waiting_time_minutes` are relatively small but require a documented handling approach before KPI calculations.

---

## Initial Analytical Observations

### Appointment Outcomes

No-shows account for **48.5%** of all appointments, making them the largest single outcome category.

### Previous No-Show History

The preliminary descriptive analysis indicates that no-show rates increase with previous no-show history:

* **0 previous no-shows:** approximately 44%
* **3 previous no-shows:** approximately 68%

This makes previous attendance behaviour an important variable for further segmentation.

### Reminder Status

The preliminary analysis showed:

* **Reminder sent:** 47.4% no-show rate
* **No reminder:** 51.4% no-show rate

These observations are **descriptive associations only** and should not be interpreted as evidence that reminders cause improved attendance.

---

## Business Questions

The Week 4 analysis identified the following questions for further investigation:

1. What proportion of appointments are missed?
2. Which patient or appointment characteristics are associated with no-shows?
3. Does reminder status and reminder channel relate to attendance?
4. Does waiting time influence attendance?
5. Does distance from the clinic relate to missed appointments?
6. How does previous no-show history relate to future attendance?

---

## Proposed KPIs

| KPI                                 | Business Question                                              | Why It Matters                                |
| ----------------------------------- | -------------------------------------------------------------- | --------------------------------------------- |
| Appointment No-Show Rate            | How frequently are appointments missed?                        | Measures the scale of the problem             |
| Attendance Rate                     | What proportion of appointments are attended?                  | Tracks appointment utilisation                |
| Reminder Response / Attendance Rate | Are reminders associated with better attendance?               | Helps assess reminder performance             |
| Repeat No-Show Rate                 | Are patients with previous no-shows more likely to miss again? | Helps identify higher-risk groups             |
| Appointment Slot Utilisation Rate   | How efficiently are available slots being used?                | Connects attendance to operational efficiency |

> **Week 4 scope:** The KPIs were identified and justified. KPI calculation and dashboard visualisation are planned for later stages of the project.

---

## Proposed Analysis Approach

### 1. Data Inspection

Validate structure, data types, ranges, and values against the Data Dictionary.

### 2. Data Cleaning

Document and apply an appropriate approach to missing values in:

* `distance_to_clinic_km`
* `waiting_time_minutes`

### 3. Descriptive Analysis

Summarise appointment volumes by:

* Appointment type
* Day
* Time
* Demographic group

### 4. No-Show Segmentation

Analyse no-show rates across the key variables identified during Week 4.

### 5. Relationship Analysis

Investigate relationships between no-shows and:

* Reminder status
* Reminder channel
* Distance
* Waiting time
* Previous no-show history
* Booking behaviour

### 6. KPI Development

Calculate the proposed KPIs using Power BI.

### 7. Visualisation

Build a Power BI dashboard presenting KPI performance and segment comparisons.

### 8. Business Recommendations

Translate analytical findings into practical recommendations for reducing missed appointments and improving patient experience.

---

## Assumptions and Limitations

### Assumptions

* The dataset represents a fictional simulation of clinic appointment behaviour.
* Patterns identified are illustrative and are not clinically validated.

### Limitations

* `distance_to_clinic_km` contains 90 missing records.
* `waiting_time_minutes` contains 60 missing records.
* The dataset does not include operational factors such as appointment cost, staff availability, or clinic capacity.

### Analytical Risk

The Week 4 findings are descriptive. Observed relationships should not automatically be interpreted as causal relationships.

For example, a lower no-show rate among patients who received reminders does not prove that reminders caused better attendance.

### Ethical Consideration

The dataset is fictional and anonymised. Any extension of this analysis to real patient data would need to comply with applicable healthcare data protection and privacy requirements.

---

## Week 5 Focus

The next stage of the project will focus on:

* Finalising the missing-data handling approach.
* Calculating the five proposed KPIs.
* Conducting deeper no-show segmentation.
* Comparing attendance across key patient and appointment characteristics.
* Developing Power BI visuals.
* Building the initial HealthConnect dashboard.
* Translating findings into actionable recommendations.

---

## Tools Used

* **Power BI** – Data analysis, KPI development and dashboarding
* **Microsoft Excel** – Data Dictionary review
* **CSV** – Appointment dataset

---

## Repository Structure

```text
HealthConnect-Week4/
│
├── README.md
│
├── documentation/
│   ├── HealthConnect_Project_Summary.pdf
│   └── HealthConnect_Data_Analytics_Deliverable.pdf
│
├── data/
│   └── HealthConnect_Data_Dictionary.xlsx
│
└── screenshots/
    └── Power BI / analysis screenshots
```

---

## Project Status

**Current Stage:** Week 4 – Project Kickoff & Problem Understanding

### Completed

* Business problem understanding
* Dataset review
* Data Dictionary validation
* Initial data-quality assessment
* Preliminary descriptive exploration
* Business question definition
* KPI identification and justification
* Proposed analytical approach

### Next Stage

**Week 5 – KPI calculation, deeper analysis and Power BI dashboard development.**

