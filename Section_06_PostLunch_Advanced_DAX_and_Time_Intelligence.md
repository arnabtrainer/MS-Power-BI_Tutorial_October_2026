# Section 06 — Advanced DAX and Time Intelligence

**Day:** 3 — Post-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Apply basic **time-intelligence calculations** using the Date dimension.
- 🎯 Compare current production with the **previous month** and **previous year**.
- 🎯 Understand **MTD, QTD, Calendar YTD, and Fiscal YTD**.
- 🎯 Build **Production Plan vs Actual** measures.
- 🎯 Calculate **variance** and **plan attainment %**.
- 🎯 Use `USERELATIONSHIP()` with an inactive Date relationship.
- 🎯 Validate DAX measures using simple Date, Product, and Plant filters.

---

## 🗂️ Resources Used

### Primary Classwork

- 🗂️ `Classwork Files/ClassWork-4 (DAX).pbix`
- 🗂️ `Classwork Files/DAX Classwork.md`

### Primary Case-Study Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

Primary tables:

- `DimDate`
- `DimProduct`
- `DimPlant`
- `FactProduction`
- `FactProductionPlan`

### Measures Reused from Section 05

- `[Production Quantity]`
- `[Good Quantity]`
- `[Rejected Quantity]`
- `[Production Cost]`
- `[Batch Count]`
- `[Yield %]`
- `[Rejection %]`

> 💡 **Prerequisite:** The relationships created in Section 04 and the base measures created in Section 05 should already be available.

---

## 📚 Advanced DAX Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Date Context | Validate Date table | 💻 Guided |
| 2 | Previous Period | Previous Month / Previous Year | 💻 Guided |
| 3 | MTD / QTD / YTD | Short time-intelligence examples | 🧑‍🏫 Demo |
| 4 | Fiscal YTD | April–March fiscal year | 💻 Guided |
| 5 | Plan vs Actual | Production vs production plan | 💻 Guided |
| 6 | Variance / Attainment | Business KPI calculations | 💻 Guided |
| 7 | Inactive Relationship | `USERELATIONSHIP()` | 💻 Guided |
| 8 | Validation | Simple cards, table, and slicers | 💻 Guided |

> 💡 **Scope:** Ranking, dynamic KPI selection, field parameters, and more complex filter-context patterns are moved to later advanced-reporting sessions.

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:15 | 🔁 DAX recap and Date-table validation |
| 00:15–00:45 | 💻 Previous Month and Previous Year |
| 00:45–01:05 | 🧑‍🏫 MTD, QTD, Calendar YTD overview |
| 01:05–01:25 | 💻 Fiscal YTD |
| 01:25–02:05 | 💻 Production Plan vs Actual |
| 02:05–02:25 | 💻 Variance and Plan Attainment % |
| 02:25–02:45 | 💻 `USERELATIONSHIP()` with Release Date |
| 02:45–03:00 | 🔁 Validation, recap, and Q&A |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. Time Intelligence Prerequisites

Time intelligence requires a reliable Date dimension.

Use:

- 🗂️ `DimDate`
- `DimDate[Date]` as the main date column
- active Date relationships created in Section 04

### Confirm

- ✅ Dates are unique and continuous.
- ✅ `DimDate` is marked as a Date table where applicable.
- ✅ Date relationships are correctly configured.
- ✅ Fiscal fields follow the April–March calendar.

### 💡 Teaching Rule

> **One business question → one short DAX measure → one visual validation.**

Avoid teaching several long formulas together.

---

## 💻 2. Previous Month Production

### Business Question

> How much production was recorded in the previous month?

Create:

```DAX
Production Previous Month =
CALCULATE(
    [Production Quantity],
    PREVIOUSMONTH(DimDate[Date])
)
```

### Month-over-Month Variance

```DAX
Production MoM Variance =
[Production Quantity] - [Production Previous Month]
```

### Month-over-Month %

```DAX
Production MoM % =
DIVIDE(
    [Production MoM Variance],
    [Production Previous Month],
    0
)
```

### ✅ Simple Validation

Use:

- a **Date slicer** based on `DimDate[Date]`
- Card → `[Production Quantity]`
- Card → `[Production Previous Month]`

Select a complete month in the Date slicer and compare the two values.

> 💡 Keep the first demonstration simple. Avoid using custom `FiscalYearMonth` as the Matrix row while introducing `PREVIOUSMONTH()`.

---

## 💻 3. Previous Year Production

### Business Question

> How much production was recorded during the corresponding period one year earlier?

Create:

```DAX
Production Previous Year =
CALCULATE(
    [Production Quantity],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

### Year-over-Year Variance

```DAX
Production YoY Variance =
[Production Quantity] - [Production Previous Year]
```

### Year-over-Year %

```DAX
Production YoY % =
DIVIDE(
    [Production YoY Variance],
    [Production Previous Year],
    0
)
```

### ✅ Simple Validation

Use the same Date slicer and compare:

- `[Production Quantity]`
- `[Production Previous Year]`

> 💡 If the selected period has no corresponding prior-year production data, the Previous Year measure may legitimately be blank.

---

## 🧑‍🏫 4. MTD, QTD and Calendar YTD

Introduce these as short standard patterns.

### Month-to-Date

```DAX
Production MTD =
TOTALMTD(
    [Production Quantity],
    DimDate[Date]
)
```

### Quarter-to-Date

```DAX
Production QTD =
TOTALQTD(
    [Production Quantity],
    DimDate[Date]
)
```

### Calendar Year-to-Date

```DAX
Production Calendar YTD =
TOTALYTD(
    [Production Quantity],
    DimDate[Date]
)
```

### 💡 Teaching Point

- **MTD** → start of month to current date
- **QTD** → start of quarter to current date
- **YTD** → start of year to current date

> 🚀 **Optional:** Learners may create all three measures if time permits. The main objective is to understand the pattern, not memorize every function.

> 🖼️ **Image Placeholder S06-01:** Simple visual showing Production Quantity with MTD, QTD, and Calendar YTD under a selected Date range.  
> **Planned file:** `images/S06_01_Time_Intelligence.png`

---

## 💻 5. Fiscal YTD — April to March

Nirvaan Pharma Ltd uses an **April–March fiscal year**.

Create:

```DAX
Production Fiscal YTD =
TOTALYTD(
    [Production Quantity],
    DimDate[Date],
    "3/31"
)
```

### 💡 Teaching Point

- Calendar YTD resets on **January 1**.
- Fiscal YTD resets after **March 31**.

### ✅ Validation

Use:

- Fiscal Year slicer
- Date/Month visual
- `[Production Quantity]`
- `[Production Fiscal YTD]`

Observe how Fiscal YTD accumulates from April onward.

---

## 💻 6. Production Plan Measure

### Business Question

> How much production was planned?

Create:

```DAX
Planned Production =
SUM(FactProductionPlan[PlannedProductionUnits])
```

### 💡 Grain Reminder

`FactProductionPlan` is monthly planning data.

Therefore, compare Plan vs Actual using:

- Month / Fiscal Month
- Product
- Plant

⚠️ Avoid comparing daily production directly with a monthly plan.

---

## 💻 7. Production Plan vs Actual

### Production Variance

```DAX
Production Variance =
[Production Quantity] - [Planned Production]
```

### Plan Attainment %

```DAX
Plan Attainment % =
DIVIDE(
    [Production Quantity],
    [Planned Production],
    0
)
```

### 💡 Interpretation

- Positive Variance → Actual is above Plan.
- Negative Variance → Actual is below Plan.
- Attainment = `1.00` or `100%` → Plan achieved exactly.
- Attainment > `100%` → Plan exceeded.
- Attainment < `100%` → Plan not fully achieved.

### Suggested Visual

Use a **Matrix or Combo Chart** with:

- Fiscal Month
- `[Production Quantity]`
- `[Planned Production]`
- `[Production Variance]`
- `[Plan Attainment %]`

Add:

- Product slicer
- Plant slicer

> 🖼️ **Image Placeholder S06-02:** Nirvaan Pharma Ltd Plan vs Actual visual showing Actual, Plan, Variance, and Plan Attainment %.  
> **Planned file:** `images/S06_02_Plan_vs_Actual.png`

---

## 💻 8. Using an Inactive Relationship

Section 04 created:

```text
DimDate[DateKey]
   ├── ✅ Active   → FactProduction[ManufactureDateKey]
   └── ⚪ Inactive → FactProduction[ReleaseDateKey]
```

A normal Date filter therefore uses **Manufacture Date**.

### Business Question

> How much production should be analyzed by Release Date instead?

Create:

```DAX
Released Production =
CALCULATE(
    [Production Quantity],
    USERELATIONSHIP(
        DimDate[DateKey],
        FactProduction[ReleaseDateKey]
    )
)
```

### 💡 Interpretation

`USERELATIONSHIP()` tells **this measure only** to use the inactive Release Date relationship.

It does **not** permanently change the semantic model.

### ✅ Validation

Create a simple visual containing:

- Date / Month
- `[Production Quantity]`
- `[Released Production]`

The values may differ because the measures use different business-date roles.

> 🖼️ **Image Placeholder S06-03:** Comparison of Production by Manufacture Date and Release Date using `USERELATIONSHIP()`.  
> **Planned file:** `images/S06_03_USERELATIONSHIP.png`

---

## 💻 9. Simple Validation Page

Create one compact report page.

### Slicers

- `DimPlant[PlantName]`
- `DimProduct[ProductName]`
- `DimDate[Date]`

### Visual 1 — Current vs Previous Period

- `[Production Quantity]`
- `[Production Previous Month]`
- `[Production Previous Year]`

### Visual 2 — Plan vs Actual

- `[Production Quantity]`
- `[Planned Production]`
- `[Production Variance]`
- `[Plan Attainment %]`

### Visual 3 — Date Role

- `[Production Quantity]`
- `[Released Production]`

### ✅ Validation

Confirm that:

- ✅ Product and Plant slicers filter the measures correctly.
- ✅ Previous Month and Previous Year respond to Date selection.
- ✅ Plan vs Actual is compared at monthly grain.
- ✅ Fiscal YTD follows the April–March fiscal year.
- ✅ `USERELATIONSHIP()` affects only `[Released Production]`.

---

## 🚀 10. Optional Topics — Mention Only

If time permits, briefly mention:

- `RANKX()` → ranking products or plants
- `SELECTEDVALUE()` → reading one selected value
- `SWITCH()` → dynamic calculation selection
- Field Parameters → dynamic report interaction

⚠️ Do not make these mandatory hands-on exercises in this session.

They will fit better in the later **Advanced Reporting and Interactivity** session.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Create `[Production Previous Month]`.
2. 💻 Create `[Production MoM Variance]`.
3. 💻 Create `[Production Previous Year]`.
4. 💻 Create `[Production Fiscal YTD]`.
5. 💻 Create `[Planned Production]`.
6. 💻 Create `[Production Variance]`.
7. 💻 Create `[Plan Attainment %]`.
8. 💻 Create `[Released Production]` using `USERELATIONSHIP()`.
9. 💻 Validate the measures using Date, Product, and Plant filters.

### ✅ Expected Outcome

Learners can create understandable advanced DAX measures for **previous-period analysis, fiscal reporting, Plan vs Actual, and inactive relationships** without using unnecessarily complex formulas.

---

## 💡 Trainer Guidelines

- 💡 Use **one business question → one short formula → one validation visual**.
- 💡 Reuse the base measures created in Section 05.
- 💡 Keep the Date dimension visible while explaining time intelligence.
- 💡 Start Previous Month / Previous Year with a simple **Date slicer** rather than a complex fiscal Matrix.
- 💡 Explain monthly grain before Plan vs Actual.
- 💡 Keep MTD/QTD as short patterns; do not over-explain them.
- 💡 Reinforce that `USERELATIONSHIP()` affects only the current measure.
- ⚠️ Do not introduce long `VAR + FILTER + REMOVEFILTERS` troubleshooting patterns to learners.
- ⚠️ Do not mix daily production with monthly planning data.
- ⚠️ Do not create additional active Date relationships to solve a DAX problem.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 Previous Month and Previous Year comparisons.
- 🔁 MTD, QTD, Calendar YTD, and Fiscal YTD concepts.
- 🔁 Production Plan vs Actual.
- 🔁 Variance and Plan Attainment %.
- 🔁 Practical use of `USERELATIONSHIP()`.
- 🔁 Why simple DAX and correct visual context should be taught together.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What is required for reliable DAX time-intelligence calculations?

A. A proper Date table and valid Date relationships <br>
B. A dashboard background image <br>
C. Bidirectional relationships everywhere <br>
D. At least ten report pages <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. A proper Date table and valid Date relationships**

**Explanation:** Time-intelligence calculations depend on a reliable Date dimension and correctly configured relationships.

</details>

### 🔴 Q2. Which function is used in this section to calculate production for the previous month?

A. `PREVIOUSMONTH()` <br>
B. `COUNTROWS()` <br>
C. `FORMAT()` <br>
D. `RELATED()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `PREVIOUSMONTH()`**

**Explanation:** `PREVIOUSMONTH()` returns the Date period for the month immediately before the current Date context.

</details>

### 🔴 Q3. Which function compares the corresponding period one year earlier?

A. `SAMEPERIODLASTYEAR()` <br>
B. `SUMX()` <br>
C. `DISTINCTCOUNT()` <br>
D. `FILTER()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `SAMEPERIODLASTYEAR()`**

**Explanation:** `SAMEPERIODLASTYEAR()` shifts the current Date context to the corresponding period in the previous year.

</details>

### 🔴 Q4. What does `TOTALMTD()` calculate?

A. Month-to-date value <br>
B. Maximum value in a table <br>
C. Monthly row count only <br>
D. Model-table dependencies <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Month-to-date value**

**Explanation:** `TOTALMTD()` evaluates a measure from the beginning of the current month through the current Date context.

</details>

### 🔴 Q5. Why does the Fiscal YTD formula use `"3/31"`?

A. The fiscal year ends on March 31 <br>
B. Power BI requires every year to end in March <br>
C. `SUM()` only works in March <br>
D. It disables Date filtering <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. The fiscal year ends on March 31**

**Explanation:** An April–March fiscal year ends on March 31, so Fiscal YTD should reset after that date.

</details>

### 🔴 Q6. Which measure represents Actual Production minus Planned Production?

A. `[Production Variance]` <br>
B. `[Batch Count]` <br>
C. `[Production Previous Month]` <br>
D. `[Yield %]` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `[Production Variance]`**

**Explanation:** Production Variance measures the difference between actual production and planned production.

</details>

### 🔴 Q7. What does Plan Attainment % measure?

A. Actual production relative to planned production <br>
B. Number of Date rows <br>
C. Number of relationships <br>
D. Number of products only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Actual production relative to planned production**

**Explanation:** Plan Attainment % is calculated as Actual Production divided by Planned Production.

</details>

### 🔴 Q8. Why should Production Plan vs Actual normally be compared at Month level?

A. The production plan is stored at monthly grain <br>
B. Production data has no dates <br>
C. DAX cannot calculate daily values <br>
D. Month names automatically create relationships <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. The production plan is stored at monthly grain**

**Explanation:** Comparing data at compatible levels of detail prevents misleading Plan vs Actual results.

</details>

### 🔴 Q9. What does `USERELATIONSHIP()` do?

A. Uses a specified inactive relationship for the current calculation <br>
B. Permanently activates every relationship <br>
C. Deletes an active relationship <br>
D. Creates a new table <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Uses a specified inactive relationship for the current calculation**

**Explanation:** `USERELATIONSHIP()` allows a measure to use an alternative relationship without permanently changing the model.

</details>

### 🔴 Q10. In the example, which Date relationship is active by default for `FactProduction`?

A. Manufacture Date <br>
B. Release Date <br>
C. Expiry Date <br>
D. No Date relationship <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Manufacture Date**

**Explanation:** The active relationship connects `DimDate` to `FactProduction[ManufactureDateKey]`.

</details>

### 🔴 Q11. Why is `DIVIDE()` used for Plan Attainment %?

A. It handles zero or blank denominators safely <br>
B. It creates a Date table <br>
C. It changes relationship direction <br>
D. It imports data <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. It handles zero or blank denominators safely**

**Explanation:** `DIVIDE()` provides safer ratio calculations when Planned Production may be zero or blank.

</details>

### 🔴 Q12. What is the recommended teaching approach for advanced DAX in this session?

A. One business question, one short formula, and one validation visual <br>
B. Memorize as many DAX functions as possible <br>
C. Use only long formulas <br>
D. Avoid visual validation <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. One business question, one short formula, and one validation visual**

**Explanation:** Short, purposeful DAX examples are easier to understand, demonstrate, and validate during training.

</details>

---

### ➡️ Next Session

**Section 07 — Pharma Analytics I: Production Performance**

Learners will use the completed model and DAX measures to build a focused **Production Performance dashboard** for Nirvaan Pharma Ltd.
