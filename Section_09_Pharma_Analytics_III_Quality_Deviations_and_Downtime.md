# Section 09 — Pharma Analytics III: Quality, Deviations and Downtime

**Day:** 5 — Pre-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Analyze **Quality Test performance**, including Pass, Fail, OOS (Out of Specification), Retest, and Turnaround Time.
- 🎯 Analyze **Batch Deviations** by severity, category, CAPA requirement, and closure age.
- 🎯 Analyze **Downtime** by category, reason, shift, equipment, and month.
- 🎯 Reuse familiar DAX functions instead of learning unnecessary new syntax.
- 🎯 Build a focused **Quality, Deviations & Downtime dashboard**.
- 🎯 Use suitable visuals for categorical comparison, trend analysis, and detailed validation.
- 🎯 Validate KPI measures using a consistent **Calendar Year 2025** demonstration context.
- 🎯 Interpret operational quality indicators without drawing conclusions from a single measure alone.

---

## 🗂️ Resources Used

### Primary Case-Study Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

### Primary Fact Tables

- `FactQualityTest`
- `FactBatchDeviation`
- `FactDowntime`

### Supporting Dimensions

- `DimDate`
- `DimProduct`
- `DimBatch`
- `DimQCTest`
- `DimDeviationReason`
- `DimDowntimeReason`
- `DimEquipment`
- `DimShift`
- `DimOperator`

### Important Fields

#### `FactQualityTest`

- `QCResultID`
- `BatchKey`
- `ProductKey`
- `QCTestKey`
- `TestDateKey`
- `AnalystOperatorKey`
- `ResultStatus`
- `TurnaroundDays`
- `IsRetest`

#### `FactBatchDeviation`

- `DeviationID`
- `BatchKey`
- `DeviationReasonKey`
- `ReportedDateKey`
- `ClosureDateKey`
- `ClosureAgeDays`
- `IsCAPARequired`
- `DeviationStatus`

#### `FactDowntime`

- `DowntimeID`
- `DateKey`
- `EquipmentKey`
- `ShiftKey`
- `DowntimeReasonKey`
- `BatchKey`
- `DurationMinutes`

---

## 🔗 Relevant Model Relationships

Verify the relationships required for this session.

### Quality Tests

```text
DimDate[DateKey]
   └── ✅ Active → FactQualityTest[TestDateKey]

DimProduct[ProductKey]
   └── ✅ Active → FactQualityTest[ProductKey]

DimBatch[BatchKey]
   └── ✅ Active → FactQualityTest[BatchKey]

DimQCTest[QCTestKey]
   └── ✅ Active → FactQualityTest[QCTestKey]

DimOperator[OperatorKey]
   └── ✅ Active → FactQualityTest[AnalystOperatorKey]
```

### Batch Deviations

```text
DimDate[DateKey]
   ├── ✅ Active   → FactBatchDeviation[ReportedDateKey]
   └── ⚪ Inactive → FactBatchDeviation[ClosureDateKey]

DimBatch[BatchKey]
   └── ✅ Active → FactBatchDeviation[BatchKey]

DimDeviationReason[DeviationReasonKey]
   └── ✅ Active → FactBatchDeviation[DeviationReasonKey]
```

### Downtime

```text
DimDate[DateKey]
   └── ✅ Active → FactDowntime[DateKey]

DimEquipment[EquipmentKey]
   └── ✅ Active → FactDowntime[EquipmentKey]

DimShift[ShiftKey]
   └── ✅ Active → FactDowntime[ShiftKey]

DimDowntimeReason[DowntimeReasonKey]
   └── ✅ Active → FactDowntime[DowntimeReasonKey]
```

> 💡 **Teaching Point:** The common `DimDate` allows one Calendar Year slicer to filter all three analytical areas through their active business-date relationships.

---

## 📚 Analytics Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Quality KPIs | Test count, Pass Rate, Retest %, TAT | 💻 Guided |
| 2 | Quality Breakdown | Result Status and Test Category | 💻 Guided |
| 3 | Deviation KPIs | Count, CAPA %, Closure Age | 💻 Guided |
| 4 | Deviation Analysis | Severity and Category | 💻 Guided |
| 5 | Downtime KPIs | Hours, Events, Unplanned % | 💻 Guided |
| 6 | Downtime Trend | Planned vs Unplanned by Month | 💻 Guided |
| 7 | Downtime Reasons | Identify major downtime contributors | 💻 Guided |
| 8 | Dashboard Layout | Combine three analytical areas | 💻 Guided |
| 9 | Validation | Reconcile measures and visuals | 💻 Guided |

---

## 🧭 DAX — Purpose and Target Map

This session intentionally **reuses DAX already learned**.

| DAX Function / Construct | Purpose | Target in This Section |
|---|---|---|
| `COUNTROWS()` | Count fact-table rows | Quality Tests, Deviations, Downtime Events |
| `CALCULATE()` | Re-evaluate a measure under a changed filter context | Pass, Fail, OOS, Retest, CAPA, Unplanned Downtime |
| `DIVIDE()` | Safe ratio calculation | Pass Rate %, Retest %, CAPA %, Unplanned Downtime % |
| `AVERAGE()` | Calculate mean value | Test Turnaround Days, Deviation Closure Age |
| `SUM()` | Add numeric values | Downtime Minutes |
| `VAR` / `RETURN` | Improve readability when required | Optional measure organization |

> 💡 **No major new DAX function is introduced in this session.**  
> The emphasis is **business interpretation using DAX learners already understand**.

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:15 | 🔁 Model and business-question recap |
| 00:15–00:50 | 💻 Quality measures and visuals |
| 00:50–01:20 | 💻 Deviation measures and visuals |
| 01:20–01:55 | 💻 Downtime measures |
| 01:55–02:20 | 💻 Downtime trend and reason analysis |
| 02:20–02:40 | 💻 Build combined dashboard page |
| 02:40–02:55 | ✅ Validation and manual reconciliation |
| 02:55–03:00 | 🔁 Recap |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. Start with the Business Questions

### Quality

- How many QC tests were performed?
- What percentage passed?
- How many tests were Fail or OOS (Out of Specification)?
- How often were retests required?
- What was the average turnaround time?

### Deviations

- How many deviations were reported?
- How many required CAPA?
- Which severities and categories occur most frequently?
- How long do closed deviations take to close?

### Downtime

- How many downtime events occurred?
- How many downtime hours were recorded?
- How much downtime was unplanned?
- Which reasons contributed most?
- How did downtime change month by month?

### 💡 Teaching Rule

> **Business Question → Measure → Visual → Validation → Insight**

---

## 💻 2. Add the Main Dashboard Filter

### 🛠️ Visual Type

**Slicer**

### Field

- `DimDate[CalendarYear]`

For classroom demonstration, select:

**2025**

### 💡 Why 2025?

The dataset contains useful history before 2025 and additional records afterward, so the year provides a practical middle-period context for comparison and validation.

---

# QUALITY ANALYTICS

## 💻 3. Create Core Quality Measures

### QC Test Count

```DAX
QC Test Count =
COUNTROWS(FactQualityTest)
```

- 🎯 **Purpose:** Count quality-test result rows.
- 🧭 **Target:** Show how many QC tests were recorded in the selected context.

### Passed Test Count

```DAX
Passed Test Count =
CALCULATE(
    [QC Test Count],
    FactQualityTest[ResultStatus] = "Pass"
)
```

### Failed Test Count

```DAX
Failed Test Count =
CALCULATE(
    [QC Test Count],
    FactQualityTest[ResultStatus] = "Fail"
)
```

### OOS (Out of Specification) Test Count

```DAX
OOS Test Count =
CALCULATE(
    [QC Test Count],
    FactQualityTest[ResultStatus] = "OOS"
)
```

### Pass Rate %

```DAX
Pass Rate % =
DIVIDE(
    [Passed Test Count],
    [QC Test Count],
    0
)
```

- 🎯 **Purpose:** Express passed tests as a percentage of total tests.
- 🧭 **Target:** Monitor overall QC result performance.

### Retest Count

```DAX
Retest Count =
CALCULATE(
    [QC Test Count],
    FactQualityTest[IsRetest] = TRUE()
)
```

### Retest %

```DAX
Retest % =
DIVIDE(
    [Retest Count],
    [QC Test Count],
    0
)
```

### Average Test Turnaround Days

```DAX
Avg Test Turnaround Days =
AVERAGE(FactQualityTest[TurnaroundDays])
```

---

## ✅ Quality KPI Validation

### 🛠️ Visual Type

Use separate **Card visuals**.

Create Cards for:

- `[QC Test Count]`
- `[Passed Test Count]`
- `[Failed Test Count]`
- `[OOS Test Count]`
- `[Pass Rate %]`
- `[Retest Count]`
- `[Retest %]`
- `[Avg Test Turnaround Days]`

Set:

**Calendar Year = 2025**

Expected values:

| Measure | Expected Value |
|---|---:|
| QC Test Count | 2,362 |
| Passed Test Count | 2,331 |
| Failed Test Count | 20 |
| OOS Test Count | 11 |
| Pass Rate % | ≈ 98.69% |
| Retest Count | 149 |
| Retest % | ≈ 6.31% |
| Avg Test Turnaround Days | ≈ 4.48 days |

### 🧮 Manual Cross-Check

```text
Pass Rate %
= 2,331 ÷ 2,362
≈ 98.69%
```

```text
Retest %
= 149 ÷ 2,362
≈ 6.31%
```

> 💡 **Validation Point:**  
> Passed + Failed + OOS should reconcile with Total QC Tests.

```text
2,331 + 20 + 11
= 2,362
```

---

## 💻 4. Quality Results by Test Category

### Business Question

> Which Test Categories have the most QC activity, and where do Fail/OOS results occur?

### 🛠️ Visual Type

**Stacked Column Chart**

### Configure the Visual

**X-axis**
- `DimQCTest[TestCategory]`

**Y-axis**
- `[QC Test Count]`

**Legend**
- `FactQualityTest[ResultStatus]`

### Optional Tooltips

Add:

- `[Pass Rate %]`
- `[Retest %]`
- `[Avg Test Turnaround Days]`

### ✅ Validation

For Calendar Year 2025:

| Test Category | QC Test Count |
|---|---:|
| Physical | 1,220 |
| Chemical | 575 |
| Microbiological | 567 |

Confirm:

```text
1,220 + 575 + 567
= 2,362
```

### 💡 Interpretation Questions

- Which Test Category has the largest workload?
- Where are Fail or OOS results concentrated?
- Does a category with more tests automatically have a worse Pass Rate?

> 🖼️ **Image Placeholder S09-01:** Quality Test Results by Test Category and Result Status.  
> **Planned file:** `images/S09_01_Quality_Test_Results.png`

---

# DEVIATION ANALYTICS

## 💻 5. Create Core Deviation Measures

### Deviation Count

```DAX
Deviation Count =
COUNTROWS(FactBatchDeviation)
```

### CAPA Required Count

```DAX
CAPA Required Count =
CALCULATE(
    [Deviation Count],
    FactBatchDeviation[IsCAPARequired] = TRUE()
)
```

### CAPA Required %

```DAX
CAPA Required % =
DIVIDE(
    [CAPA Required Count],
    [Deviation Count],
    0
)
```

### Closed Deviation Count

```DAX
Closed Deviation Count =
CALCULATE(
    [Deviation Count],
    FactBatchDeviation[DeviationStatus] = "Closed"
)
```

### Average Closed Deviation Age

```DAX
Avg Closed Deviation Age =
CALCULATE(
    AVERAGE(FactBatchDeviation[ClosureAgeDays]),
    FactBatchDeviation[DeviationStatus] = "Closed"
)
```

- 🎯 **Purpose:** Calculate the average closure age only for deviations marked Closed.
- 🧭 **Target:** Avoid mixing open deviations into the closure-age KPI.

---

## ✅ Deviation KPI Validation

### 🛠️ Visual Type

Use **Card visuals**.

Create Cards for:

- `[Deviation Count]`
- `[CAPA Required Count]`
- `[CAPA Required %]`
- `[Closed Deviation Count]`
- `[Avg Closed Deviation Age]`

Set:

**Calendar Year = 2025**

Expected values:

| Measure | Expected Value |
|---|---:|
| Deviation Count | 138 |
| CAPA Required Count | 95 |
| CAPA Required % | ≈ 68.84% |
| Closed Deviation Count | 123 |
| Avg Closed Deviation Age | ≈ 50.48 days |

### 🧮 Manual Cross-Check

```text
CAPA Required %
= 95 ÷ 138
≈ 68.84%
```

---

## 💻 6. Deviations by Severity

### Business Question

> Which deviation severities occur most frequently?

### 🛠️ Visual Type

**Clustered Bar Chart**

### Configure the Visual

**Y-axis / Category**
- `DimDeviationReason[Severity]`

**X-axis / Values**
- `[Deviation Count]`

### Sort

**Deviation Count → Descending**

### Optional Tooltips

Add:

- `[CAPA Required Count]`
- `[CAPA Required %]`
- `[Avg Closed Deviation Age]`

### ✅ Validation

For Calendar Year 2025:

| Severity | Deviation Count |
|---|---:|
| Major | 49 |
| Critical | 46 |
| Minor | 43 |

Confirm:

```text
49 + 46 + 43
= 138
```

### 💡 Interpretation Questions

- Which severity appears most frequently?
- Which severity has the greatest CAPA requirement?
- Should frequency alone determine priority?

> ⚠️ Frequency and severity are different concepts. A lower-frequency Critical issue may still require more attention than a high-frequency Minor issue.

---

## 💻 7. Deviations by Category

### 🛠️ Visual Type

**Clustered Bar Chart**

### Configure the Visual

**Y-axis**
- `DimDeviationReason[DeviationCategory]`

**X-axis**
- `[Deviation Count]`

### Sort

**Deviation Count → Descending**

### ✅ 2025 Reference Values

| Deviation Category | Count |
|---|---:|
| Facility | 47 |
| Equipment | 26 |
| Process | 16 |
| Documentation | 16 |
| Packaging | 13 |
| Human | 10 |
| Material | 10 |

### 💡 Interpretation Questions

- Which category contributes the largest number of deviations?
- Are high-count categories also associated with higher severity?
- Where might deeper root-cause analysis be useful?

> 🖼️ **Image Placeholder S09-02:** Deviation analysis by Severity and Category.  
> **Planned file:** `images/S09_02_Deviation_Analysis.png`

---

# DOWNTIME ANALYTICS

## 💻 8. Create Core Downtime Measures

### Downtime Minutes

```DAX
Downtime Minutes =
SUM(FactDowntime[DurationMinutes])
```

### Downtime Hours

```DAX
Downtime Hours =
DIVIDE(
    [Downtime Minutes],
    60,
    0
)
```

### Downtime Event Count

```DAX
Downtime Event Count =
COUNTROWS(FactDowntime)
```

### Unplanned Downtime Minutes

```DAX
Unplanned Downtime Minutes =
CALCULATE(
    [Downtime Minutes],
    DimDowntimeReason[DowntimeCategory] = "Unplanned"
)
```

### Unplanned Downtime Hours

```DAX
Unplanned Downtime Hours =
DIVIDE(
    [Unplanned Downtime Minutes],
    60,
    0
)
```

### Unplanned Downtime %

```DAX
Unplanned Downtime % =
DIVIDE(
    [Unplanned Downtime Minutes],
    [Downtime Minutes],
    0
)
```

---

## ✅ Downtime KPI Validation

### 🛠️ Visual Type

Use **Card visuals**.

Create Cards for:

- `[Downtime Hours]`
- `[Downtime Event Count]`
- `[Unplanned Downtime Hours]`
- `[Unplanned Downtime %]`

Set:

**Calendar Year = 2025**

Expected values:

| Measure | Expected Value |
|---|---:|
| Downtime Hours | 489.75 |
| Downtime Event Count | 1,462 |
| Unplanned Downtime Hours | ≈ 340.23 |
| Unplanned Downtime % | ≈ 69.47% |

### 🧮 Manual Cross-Check

```text
Unplanned Downtime %
= 340.23 ÷ 489.75
≈ 69.47%
```

---

## 💻 9. Planned vs Unplanned Downtime by Month

### Business Question

> How does Planned and Unplanned Downtime change month by month?

### 🛠️ Visual Type

**Stacked Column Chart**

### Configure the Visual

**X-axis**
- `DimDate[CalendarYearMonth]`

**Y-axis**
- `[Downtime Hours]`

**Legend**
- `DimDowntimeReason[DowntimeCategory]`

### Sorting

Select `DimDate[CalendarYearMonth]` and sort it using the proper Month sort key.

Then ensure the visual itself is sorted by:

**CalendarYearMonth → Ascending**

### ✅ Validation

Set:

**Calendar Year = 2025**

Hover over **May 2025**.

Expected:

| Downtime Category | Hours |
|---|---:|
| Planned | ≈ 11.48 |
| Unplanned | 23.40 |
| Total | ≈ 34.88 |

Confirm:

```text
11.48 + 23.40
≈ 34.88 hours
```

### 💡 Interpretation Questions

- Which months show higher Unplanned Downtime?
- Is Planned Downtime relatively stable?
- Are there months requiring deeper reason analysis?

---

## 💻 10. Downtime by Reason

### Business Question

> Which reasons consume the most downtime hours?

### 🛠️ Visual Type

**Clustered Bar Chart**

### Configure the Visual

**Y-axis**
- `DimDowntimeReason[DowntimeReasonName]`

**X-axis**
- `[Downtime Hours]`

### Sort

**Downtime Hours → Descending**

### Optional Tooltips

Add:

- `[Downtime Event Count]`
- `[Unplanned Downtime %]`
- `DimDowntimeReason[DowntimeCategory]`
- `DimDowntimeReason[OEEPillar]`

### 💡 Interpretation Questions

- Which downtime reasons contribute the most lost time?
- Does a high event count always mean high downtime hours?
- Which reasons are Planned vs Unplanned?
- Which reasons are classified as OEE losses?

> 🖼️ **Image Placeholder S09-03:** Planned vs Unplanned Downtime trend and Downtime Hours by Reason.  
> **Planned file:** `images/S09_03_Downtime_Analysis.png`

---

## 💻 11. Optional Detailed Downtime Matrix

### 🛠️ Visual Type

**Matrix**

### Rows

- `DimEquipment[EquipmentName]`

### Columns

- `DimShift[ShiftName]`

### Values

- `[Downtime Hours]`
- `[Downtime Event Count]`
- `[Unplanned Downtime Hours]`

### ✅ Validation

Select Calendar Year 2025 and verify that Matrix totals reconcile with the Downtime KPI Cards.

### 💡 Teaching Point

Use the Matrix for **investigation and validation**, while the Bar/Column Charts are better for **pattern recognition**.

---

## 🧩 12. Recommended Dashboard Layout

Create one report page named:

**Quality, Deviations & Downtime**

Suggested layout:

```text
┌────────────────────────────────────────────────────────────────┐
│ Calendar Year Slicer                                           │
├────────────────────────────────────────────────────────────────┤
│ QUALITY KPIs                                                   │
│ Tests | Pass Rate | Fail | OOS | Retest % | Avg TAT           │
├───────────────────────┬────────────────────────────────────────┤
│ Quality by Category   │ DEVIATION KPIs                         │
│ Stacked Column        │ Count | CAPA % | Closure Age           │
├───────────────────────┼────────────────────────────────────────┤
│ Deviation Severity    │ Deviation Category                     │
│ Bar Chart             │ Bar Chart                              │
├────────────────────────────────────────────────────────────────┤
│ DOWNTIME KPIs: Hours | Events | Unplanned Hours | Unplanned % │
├─────────────────────────────┬──────────────────────────────────┤
│ Planned vs Unplanned Trend  │ Downtime by Reason               │
│ Stacked Column Chart        │ Bar Chart                        │
└─────────────────────────────┴──────────────────────────────────┘
```

### 💡 Design Guidance

- Keep Quality, Deviations, and Downtime visually separated into clear sections.
- Use the same Calendar Year slicer for all three areas.
- Avoid overloading the page with too many slicers.
- Keep exact-value validation in temporary Cards or Matrix visuals if needed.
- Use consistent percentage and decimal formatting.

> 🖼️ **Image Placeholder S09-04:** Final Quality, Deviations & Downtime dashboard.  
> **Planned file:** `images/S09_04_Quality_Deviation_Downtime_Dashboard.png`

---

## ✅ 13. Dashboard Validation Checklist

### Quality

For Calendar Year 2025:

- ✅ Total QC Tests = **2,362**
- ✅ Pass = **2,331**
- ✅ Fail = **20**
- ✅ OOS = **11**
- ✅ Pass Rate ≈ **98.69%**
- ✅ Retest Count = **149**
- ✅ Retest % ≈ **6.31%**
- ✅ Avg Turnaround ≈ **4.48 days**

### Deviations

For Calendar Year 2025:

- ✅ Deviation Count = **138**
- ✅ CAPA Required = **95**
- ✅ CAPA Required % ≈ **68.84%**
- ✅ Closed Deviation Count = **123**
- ✅ Avg Closed Deviation Age ≈ **50.48 days**

### Downtime

For Calendar Year 2025:

- ✅ Downtime Hours = **489.75**
- ✅ Downtime Event Count = **1,462**
- ✅ Unplanned Downtime Hours ≈ **340.23**
- ✅ Unplanned Downtime % ≈ **69.47%**

### Reconciliation Rules

```text
Pass + Fail + OOS
=
QC Test Count
```

```text
Severity-level Deviation Counts
=
Total Deviation Count
```

```text
Planned Downtime Hours + Unplanned Downtime Hours
=
Total Downtime Hours
```

> 💡 **Validation Rule:** A KPI is trustworthy only when its base components and visual totals reconcile under the same filter context.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Add a Calendar Year slicer and select 2025.
2. 💻 Create `[QC Test Count]`.
3. 💻 Create Pass, Fail, and OOS measures.
4. 💻 Create `[Pass Rate %]`.
5. 💻 Create `[Retest Count]` and `[Retest %]`.
6. 💻 Create `[Avg Test Turnaround Days]`.
7. 💻 Build the Quality Result Stacked Column Chart.
8. 💻 Create Deviation Count, CAPA %, and Closure Age measures.
9. 💻 Build Severity and Category Bar Charts.
10. 💻 Create Downtime Hours and Event Count.
11. 💻 Create Unplanned Downtime measures.
12. 💻 Build Planned vs Unplanned Downtime by Month.
13. 💻 Build Downtime by Reason.
14. 💻 Validate one KPI from each analytical area manually.
15. 💻 Complete **Dashboard Page 3 — Quality, Deviations & Downtime**.

### ✅ Expected Outcome

Learners can analyze **quality results, deviations, and downtime** using familiar DAX, select appropriate visuals, and validate the main KPIs before interpreting operational performance.

---

## 💡 Trainer Guidelines

- 💡 Reuse DAX already taught instead of introducing unnecessary new functions.
- 💡 Use **Calendar Year 2025** as the common demonstration period.
- 💡 Explain the difference between **Fail** and **OOS** as separate result statuses in the dataset.
- 💡 Use Cards for headline KPIs.
- 💡 Use Stacked Columns for status/category composition and monthly Planned vs Unplanned Downtime.
- 💡 Use Bar Charts for Severity, Deviation Category, and Downtime Reason comparisons.
- 💡 Use a Matrix only when exact detailed investigation is needed.
- 💡 Manually reconcile at least one ratio in each domain.
- ⚠️ Do not interpret a high Test Count as poor quality.
- ⚠️ Do not interpret deviation frequency without considering severity and CAPA.
- ⚠️ Do not interpret downtime event count without also considering duration.
- ⚠️ Avoid drawing operational conclusions from a single KPI without checking the related breakdown.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 QC Test Count, Pass Rate, Fail/OOS, Retest, and Turnaround Time.
- 🔁 Deviation Count, CAPA %, Severity, Category, and Closure Age.
- 🔁 Downtime Hours, Event Count, Planned vs Unplanned, and Downtime Reasons.
- 🔁 How one Date slicer can drive multiple fact tables through active relationships.
- 🔁 How to choose visuals according to the business question.
- 🔁 How to validate operational analytics before interpreting the results.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. Which measure counts the number of QC test records?

A. `COUNTROWS(FactQualityTest)` <br>
B. `SUM(DimQCTest[TestCategory])` <br>
C. `MAX(FactQualityTest[ResultStatus])` <br>
D. `DIVIDE(FactQualityTest)` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `COUNTROWS(FactQualityTest)`**

**Explanation:** Each fact row represents a QC test result, so `COUNTROWS()` can count test records under the current filter context.

</details>

### 🔴 Q2. How is Pass Rate % calculated in this session?

A. Passed Test Count ÷ QC Test Count <br>
B. Failed Test Count ÷ Retest Count <br>
C. OOS Count + Batch Count <br>
D. Turnaround Days ÷ Deviation Count <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Passed Test Count ÷ QC Test Count**

**Explanation:** Pass Rate expresses passed QC tests as a percentage of all QC test records in the current context.

</details>

### 🔴 Q3. What does OOS mean in the Quality Result Status context?

A. Out of Specification <br>
B. Out of Service report page <br>
C. Overall Operating Shift <br>
D. Order of Sorting <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Out of Specification**

**Explanation:** OOS is used as a distinct QC result status for results that fall outside the applicable specification.

</details>

### 🔴 Q4. Which field is used to identify Retest records?

A. `FactQualityTest[IsRetest]` <br>
B. `FactDowntime[DurationMinutes]` <br>
C. `DimDate[CalendarYear]` <br>
D. `DimShift[ShiftName]` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `FactQualityTest[IsRetest]`**

**Explanation:** `IsRetest` is the Boolean field used to distinguish retest records from original tests.

</details>

### 🔴 Q5. Why is Average Closed Deviation Age filtered to Closed deviations?

A. Closure age is intended to describe completed closure performance <br>
B. DAX cannot calculate averages <br>
C. Open deviations have no Product key <br>
D. Severity cannot be filtered <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Closure age is intended to describe completed closure performance**

**Explanation:** Restricting the measure to Closed records keeps the KPI aligned with completed deviation-closure performance.

</details>

### 🔴 Q6. What does CAPA Required % represent?

A. CAPA-required deviations ÷ total deviations <br>
B. Downtime Hours ÷ Quality Tests <br>
C. Passed Tests ÷ Retests <br>
D. Minor deviations only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. CAPA-required deviations ÷ total deviations**

**Explanation:** The measure expresses the proportion of deviations requiring corrective/preventive action.

</details>

### 🔴 Q7. Which visual is recommended for comparing Deviation Count by Severity?

A. Clustered Bar Chart <br>
B. Card only <br>
C. Map <br>
D. Gauge only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Clustered Bar Chart**

**Explanation:** A Bar Chart clearly compares categorical counts such as Critical, Major, and Minor deviations.

</details>

### 🔴 Q8. How is Downtime Hours derived?

A. Downtime Minutes ÷ 60 <br>
B. Downtime Minutes × 60 <br>
C. Event Count ÷ QC Tests <br>
D. CAPA Count + Downtime Minutes <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Downtime Minutes ÷ 60**

**Explanation:** Duration is stored in minutes, so dividing by 60 converts it to hours.

</details>

### 🔴 Q9. What does Unplanned Downtime % compare?

A. Unplanned Downtime Minutes to Total Downtime Minutes <br>
B. Quality Tests to Deviations <br>
C. Planned Production to Actual Production <br>
D. Retests to Batches <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Unplanned Downtime Minutes to Total Downtime Minutes**

**Explanation:** The ratio shows what share of total downtime duration was classified as Unplanned.

</details>

### 🔴 Q10. Which visual is suitable for Planned vs Unplanned Downtime by Month?

A. Stacked Column Chart <br>
B. Single Card <br>
C. Pie Chart with months as slices <br>
D. Text box <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Stacked Column Chart**

**Explanation:** The visual shows total monthly downtime while separating the Planned and Unplanned components.

</details>

### 🔴 Q11. Why should Downtime Event Count and Downtime Hours be considered together?

A. Many short events and a few long events can have very different operational impact <br>
B. They are always identical <br>
C. Event Count automatically contains hours <br>
D. DurationMinutes is a text field <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Many short events and a few long events can have very different operational impact**

**Explanation:** Frequency and duration describe different aspects of downtime and should be interpreted together.

</details>

### 🔴 Q12. What is the main deliverable of Section 09?

A. Quality, Deviations & Downtime dashboard page <br>
B. A new database server <br>
C. Power BI Service deployment only <br>
D. An Excel macro <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Quality, Deviations & Downtime dashboard page**

**Explanation:** The session consolidates quality, deviation, and downtime measures into a validated operational dashboard.

</details>

---

### ➡️ Next Session

**Section 10 — Advanced Reporting, Interactivity and Report UX**

Learners will enhance the existing dashboards using **advanced interactivity, ranking, dynamic selections, field parameters, bookmarks, drill-through, tooltips, and report-design techniques**.
