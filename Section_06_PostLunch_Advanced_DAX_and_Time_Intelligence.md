# Section 06 — Advanced DAX and Time Intelligence

**Day:** 3 — Post-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Apply **time-intelligence calculations** using the Date dimension.
- 🎯 Compare current performance with **previous month** and **previous year**.
- 🎯 Calculate **MTD, QTD, Calendar YTD, and Fiscal YTD**.
- 🎯 Build **Production Plan vs Actual** measures.
- 🎯 Create **variance, attainment, and ranking** measures.
- 🎯 Use `SELECTEDVALUE()` and `SWITCH()` for simple dynamic calculations.
- 🎯 Use `USERELATIONSHIP()` with inactive Date relationships.
- 🎯 Validate advanced DAX using Product, Plant, and Date filters.

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
| 1 | Date Context | Validate Date table and fiscal sorting | 💻 Guided |
| 2 | Previous Period | Previous Month / Previous Year | 💻 Guided |
| 3 | MTD / QTD / YTD | Time-intelligence measures | 💻 Guided |
| 4 | Fiscal YTD | April–March fiscal year | 💻 Guided |
| 5 | Plan vs Actual | Production vs production plan | 💻 Guided |
| 6 | Variance / Attainment | Business KPI calculations | 💻 Guided |
| 7 | Ranking | Product ranking with `RANKX` | 💻 Guided |
| 8 | Dynamic Selection | `SELECTEDVALUE` + `SWITCH` | 🧑‍🏫 Demo |
| 9 | Inactive Relationships | `USERELATIONSHIP()` | 💻 Guided |
| 10 | Validation | Slicers, matrix, trend visual | 💻 Guided |

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:15 | 🔁 DAX context recap and Date-table validation |
| 00:15–00:45 | 💻 Previous-period calculations |
| 00:45–01:15 | 💻 MTD, QTD, Calendar YTD and Fiscal YTD |
| 01:15–01:50 | 💻 Production Plan vs Actual and variance |
| 01:50–02:10 | 💻 Ranking and Top-N logic |
| 02:10–02:30 | 🧑‍🏫 Dynamic measure selection |
| 02:30–02:50 | 💻 `USERELATIONSHIP()` with Release Date |
| 02:50–03:00 | 🔁 Validation and recap |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. Time Intelligence Prerequisites

Time intelligence works correctly only when the model has a reliable Date dimension.

Use:

- 🗂️ `DimDate`
- `DimDate[Date]` as the main date column
- active Date relationships created in Section 04

### Confirm

- ✅ Dates are unique and continuous.
- ✅ `DimDate` is marked as a Date table where applicable.
- ✅ Month labels are sorted correctly.
- ✅ Fiscal fields use the April–March calendar.

Useful fields include:

- `Date`
- `MonthName`
- `MonthNumber`
- `CalendarYear`
- `FiscalYear`
- `FiscalMonthNumber`
- `FiscalYearMonth`
- `FiscalPeriodSortKey`

### 💡 Important

For **Production Plan vs Actual**, prefer Month/Fiscal Month context rather than individual day context because `FactProductionPlan` is stored at monthly planning grain.

---

## 💻 2. Previous Month Production

Create:

```DAX
Production Previous Month =
VAR PreviousMonthDates =
    DATEADD(
        VALUES(DimDate[Date]),
        -1,
        MONTH
    )
RETURN
    CALCULATE(
        [Production Quantity],
        REMOVEFILTERS(DimDate),
        PreviousMonthDates
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

### ✅ Validation

Use a matrix:

- Rows → `DimDate[FiscalYearMonth]`
- Values → Production Quantity, Previous Month, MoM Variance, MoM %

Sort `FiscalYearMonth` using `FiscalPeriodSortKey`.

---

## 💻 3. Previous Year Production

Create:

```DAX
Production Previous Year =
CALCULATE(
    [Production Quantity],
    SAMEPERIODLASTYEAR(
        DimDate[Date]
    )
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

### 💡 Teaching Point

`SAMEPERIODLASTYEAR()` shifts the current Date context to the corresponding period one year earlier.

---

## 💻 4. MTD, QTD and Calendar YTD

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

### ✅ Validation

Use Date/Month filters and confirm that each measure accumulates according to its time window.

> 🖼️ **Image Placeholder S06-01:** Matrix showing Production Quantity, Previous Month, Previous Year, MTD, QTD, and YTD by fiscal month.  
> **Planned file:** `images/S06_01_Time_Intelligence_Matrix.png`

---

## 💻 5. Fiscal YTD — April to March

Nirvaan Pharma Ltd uses an **April–March fiscal year**.

Use `DATESYTD()` with March 31 as the fiscal year end:

```DAX
Production Fiscal YTD =
CALCULATE(
    [Production Quantity],
    DATESYTD(
        DimDate[Date],
        "3/31"
    )
)
```

### 💡 Teaching Point

- Calendar YTD resets on **January 1**.
- Fiscal YTD resets after **March 31**.

### ✅ Validation

Compare:

- `[Production Calendar YTD]`
- `[Production Fiscal YTD]`

around March and April.

---

## 💻 6. Production Plan Measure

Create:

```DAX
Planned Production =
SUM(
    FactProductionPlan[PlannedProductionUnits]
)
```

### 💡 Grain Reminder

`FactProductionPlan` is monthly planning data.

Use:

- Month
- Fiscal Month
- Product
- Plant

for meaningful Plan vs Actual analysis.

---

## 💻 7. Plan vs Actual

### Production Variance

```DAX
Production Variance =
[Production Quantity] - [Planned Production]
```

### Production Variance %

```DAX
Production Variance % =
DIVIDE(
    [Production Variance],
    [Planned Production],
    0
)
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

### Suggested Visual

Use a matrix or combo chart with:

- `DimDate[FiscalYearMonth]`
- `[Production Quantity]`
- `[Planned Production]`
- `[Production Variance]`
- `[Plan Attainment %]`

Apply Product and Plant slicers.

> 🖼️ **Image Placeholder S06-02:** Nirvaan Pharma Ltd Plan vs Actual visual showing actual production, planned production, variance, and attainment %.  
> **Planned file:** `images/S06_02_Plan_vs_Actual.png`

---

## 💻 8. Product Ranking with RANKX

Create:

```DAX
Product Production Rank =
RANKX(
    ALL(
        DimProduct[ProductName]
    ),
    [Production Quantity],
    ,
    DESC,
    DENSE
)
```

### 💡 Interpretation

- `ALL(DimProduct[ProductName])` removes the current Product Name filter for ranking.
- Plant, Date, and other external filters can still affect the measure.
- `DESC` ranks the highest production as Rank 1.
- `DENSE` avoids gaps in rank values after ties.

### ✅ Validation

Create a table with:

- Product Name
- Production Quantity
- Product Production Rank

Then apply Plant and Date slicers.

---

## 🧑‍🏫 9. Dynamic Measure Selection

Create a small disconnected table using **Enter Data**:

### `Metric Selector`

| Metric |
|---|
| Production Quantity |
| Good Quantity |
| Rejected Quantity |
| Yield % |

Do **not** create a relationship from this table.

### Selected Metric

```DAX
Selected Metric =
SELECTEDVALUE(
    'Metric Selector'[Metric],
    "Production Quantity"
)
```

### Dynamic KPI

```DAX
Dynamic KPI =
SWITCH(
    [Selected Metric],
    "Production Quantity", [Production Quantity],
    "Good Quantity", [Good Quantity],
    "Rejected Quantity", [Rejected Quantity],
    "Yield %", [Yield %],
    [Production Quantity]
)
```

### ✅ Outcome

A slicer based on `Metric Selector[Metric]` can control which KPI the measure returns.

> 💡 Field Parameters provide another native approach and will be covered later under advanced reporting.

---

## 💻 10. Using an Inactive Relationship

Section 04 created:

```text
DimDate[DateKey]
   ├── ✅ Active   → FactProduction[ManufactureDateKey]
   └── ⚪ Inactive → FactProduction[ReleaseDateKey]
```

A normal Date slicer therefore filters Production by **Manufacture Date**.

### Production by Release Date

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

`USERELATIONSHIP()` tells this calculation to use the inactive **Release Date** relationship.

It does **not** permanently change the model relationship.

### Compare

Create a visual containing:

- Date / Month
- `[Production Quantity]`
- `[Released Production]`

The two measures can differ because they use different business-date roles.

> 🖼️ **Image Placeholder S06-03:** Visual comparing Production by Manufacture Date vs Production by Release Date using `USERELATIONSHIP()`.  
> **Planned file:** `images/S06_03_USERELATIONSHIP_Comparison.png`

---

## 💻 11. Optional Expiry-Date Example

If time permits:

```DAX
Production by Expiry Date =
CALCULATE(
    [Production Quantity],
    USERELATIONSHIP(
        DimDate[DateKey],
        FactProduction[ExpiryDateKey]
    )
)
```

🚀 Use this only as a short extension of the Release Date example.

---

## 💻 12. Advanced Validation

Create a report page containing:

### Slicers

- `DimDate[FiscalYear]`
- `DimPlant[PlantName]`
- `DimProduct[ProductName]`

### Visual 1 — Time Trend

- Fiscal Month
- Production Quantity
- Previous Month
- Previous Year

### Visual 2 — Plan vs Actual

- Planned Production
- Production Quantity
- Production Variance
- Plan Attainment %

### Visual 3 — Ranking

- Product
- Production Quantity
- Product Production Rank

### Visual 4 — Relationship Role

- Production Quantity by Manufacture Date
- Released Production by Release Date

### ✅ Validation

Confirm that:

- ✅ Product and Plant filters affect relevant measures.
- ✅ Date context drives time intelligence.
- ✅ Fiscal YTD resets at the correct fiscal boundary.
- ✅ Plan vs Actual is evaluated at compatible monthly grain.
- ✅ `USERELATIONSHIP()` changes only the selected calculation.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Create `[Production Previous Month]`.
2. 💻 Create `[Production MoM %]`.
3. 💻 Create `[Production Previous Year]`.
4. 💻 Create `[Production YoY %]`.
5. 💻 Create `[Production MTD]`.
6. 💻 Create `[Production Fiscal YTD]`.
7. 💻 Create `[Planned Production]`.
8. 💻 Create `[Production Variance]`.
9. 💻 Create `[Plan Attainment %]`.
10. 💻 Create `[Product Production Rank]`.
11. 💻 Create `[Released Production]` using `USERELATIONSHIP()`.
12. 💻 Validate all measures with Date, Product, and Plant filters.

### ✅ Expected Outcome

Learners can build advanced, filter-aware DAX measures for time trends, plan-vs-actual analysis, ranking, and alternative Date relationships.

---

## 💡 Trainer Guidelines

- 💡 Reuse the base measures created in Section 05.
- 💡 Keep the Date dimension visible while explaining time intelligence.
- 💡 Validate calculations using simple tables before creating complex visuals.
- 💡 Use fiscal fields for April–March reporting.
- 💡 Explain monthly grain before Plan vs Actual.
- 💡 Reinforce that `USERELATIONSHIP()` affects only the current DAX calculation.
- 💡 Keep the Dynamic KPI example simple; deeper dynamic reporting comes later.
- ⚠️ Do not mix daily production with monthly plan without a compatible Month context.
- ⚠️ Do not create additional active Date relationships to solve a measure problem.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 Previous-month and previous-year analysis.
- 🔁 MTD, QTD, Calendar YTD, and Fiscal YTD.
- 🔁 Production Plan vs Actual.
- 🔁 Variance and attainment measures.
- 🔁 Product ranking with `RANKX()`.
- 🔁 Simple dynamic KPI selection.
- 🔁 Practical use of `USERELATIONSHIP()`.
- 🔁 Validation of advanced measures under slicers and relationships.

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

**Explanation:** Time-intelligence functions depend on a reliable Date dimension and appropriate filter relationships.

</details>

### 🔴 Q2. Which function can shift the current Date context by one month?

A. `DATEADD()` <br>
B. `COUNTROWS()` <br>
C. `FORMAT()` <br>
D. `RELATED()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `DATEADD()`**

**Explanation:** `DATEADD()` shifts a Date context forward or backward by a specified interval.

</details>

### 🔴 Q3. Which function is commonly used to compare the same period in the previous year?

A. `SAMEPERIODLASTYEAR()` <br>
B. `SUMX()` <br>
C. `SELECTEDVALUE()` <br>
D. `DISTINCTCOUNT()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `SAMEPERIODLASTYEAR()`**

**Explanation:** `SAMEPERIODLASTYEAR()` returns the corresponding Date period one year earlier.

</details>

### 🔴 Q4. What does `TOTALMTD()` calculate?

A. Month-to-date value <br>
B. Maximum value in the model <br>
C. Monthly row count only <br>
D. Model-table dependencies <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Month-to-date value**

**Explanation:** `TOTALMTD()` evaluates an expression over the dates from the start of the current month through the current Date context.

</details>

### 🔴 Q5. Why does the Fiscal YTD example use March 31 as year end?

A. Nirvaan Pharma Ltd uses an April–March fiscal calendar <br>
B. Power BI only supports March year ends <br>
C. It is required by `SUM()` <br>
D. It disables Date filtering <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Nirvaan Pharma Ltd uses an April–March fiscal calendar**

**Explanation:** A fiscal year beginning in April ends on March 31, so Fiscal YTD must reset after that date.

</details>

### 🔴 Q6. Which measure represents the difference between actual and planned production?

A. `[Production Quantity] - [Planned Production]` <br>
B. `[Production Quantity] + [Planned Production]` <br>
C. `COUNTROWS(DimDate)` <br>
D. `MAX(DimPlant[PlantName])` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `[Production Quantity] - [Planned Production]`**

**Explanation:** Variance is calculated by subtracting the planned amount from the actual amount.

</details>

### 🔴 Q7. What does Plan Attainment % measure?

A. Actual production relative to planned production <br>
B. Number of Date rows <br>
C. Number of relationships <br>
D. Average Product Name <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Actual production relative to planned production**

**Explanation:** Plan Attainment % is the ratio of actual production to planned production.

</details>

### 🔴 Q8. Which function is used to rank products by production?

A. `RANKX()` <br>
B. `FILTER()` <br>
C. `DATEADD()` <br>
D. `FORMAT()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `RANKX()`**

**Explanation:** `RANKX()` evaluates an expression across a table and returns the rank of the current item.

</details>

### 🔴 Q9. What does `SELECTEDVALUE()` typically return?

A. The single selected value when one value is in context <br>
B. Every row from a table <br>
C. A new relationship <br>
D. The total number of report pages <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. The single selected value when one value is in context**

**Explanation:** `SELECTEDVALUE()` is useful when a slicer or filter should drive a dynamic calculation.

</details>

### 🔴 Q10. What is the purpose of `SWITCH()` in the Dynamic KPI example?

A. Return different measures based on the selected metric <br>
B. Create a database connection <br>
C. Change Power Query data types <br>
D. Activate every relationship <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Return different measures based on the selected metric**

**Explanation:** `SWITCH()` maps the selected metric to the appropriate DAX measure.

</details>

### 🔴 Q11. What does `USERELATIONSHIP()` do?

A. Uses a specified inactive relationship for the current calculation <br>
B. Permanently activates every relationship <br>
C. Deletes the active relationship <br>
D. Creates a new table <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Uses a specified inactive relationship for the current calculation**

**Explanation:** `USERELATIONSHIP()` allows a measure to evaluate using an alternative relationship without permanently changing the model.

</details>

### 🔴 Q12. Why should Production Plan vs Actual usually be compared at Month level?

A. The plan table is stored at monthly planning grain <br>
B. Production data contains no dates <br>
C. DAX cannot calculate daily totals <br>
D. Month names automatically create relationships <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. The plan table is stored at monthly planning grain**

**Explanation:** Comparing facts at compatible grain prevents misleading results and makes the plan-vs-actual comparison meaningful.

</details>

---

### ➡️ Next Session

**Section 07 — Pharma Analytics I: Production Performance**

Learners will use the completed model and DAX measures to build a focused **Production Performance dashboard** for Nirvaan Pharma Ltd.
