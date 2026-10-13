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


### 🧭 DAX Function — Purpose and Target Map

| **DAX Function** | **Purpose** | **Target in This Section** |
|---|---|---|
| `CALCULATE()` | Evaluates an expression under a modified filter context | Recalculate Production Quantity for another time period or relationship |
| `PREVIOUSMONTH()` | Returns the dates belonging to the previous month | Compare current production with the immediately preceding month |
| `DIVIDE()` | Performs safe division and handles zero/blank denominators | Calculate MoM %, YoY %, and Plan Attainment % |
| `SAMEPERIODLASTYEAR()` | Returns the corresponding date period one year earlier | Compare current production with the same period last year |
| `TOTALMTD()` | Accumulates a measure from the start of the month | Calculate Month-to-Date production |
| `TOTALQTD()` | Accumulates a measure from the start of the quarter | Calculate Quarter-to-Date production |
| `TOTALYTD()` | Accumulates a measure from the start of the year | Calculate Calendar YTD and April–March Fiscal YTD |
| `SUM()` | Adds all numeric values in a column under the current filter context | Calculate total Planned Production |
| `USERELATIONSHIP()` | Uses a specified inactive relationship for the current calculation | Analyze production by Release Date instead of Manufacture Date |
| `RANKX()` | Ranks items by an expression | Optional: rank Products or Plants by performance |
| `SELECTEDVALUE()` | Returns the single selected value in the current context | Optional: read a learner/user-selected KPI |
| `SWITCH()` | Returns different results based on a selected condition/value | Optional: switch between KPIs dynamically |

> 💡 **Learner Connection:** Focus on the **business question first**, then identify which DAX function helps answer it.

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

### 💡 Standard Demonstration Period

Use **May 2024** as the primary demonstration month wherever practical.

- Previous Month → April 2024
- Previous Year → May 2023
- Following Month → June 2024
- Fiscal Year → FY2024-25

This gives learners useful historical and forward context around the selected period.

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

- 🎯 **`CALCULATE()` Purpose:** Re-evaluates a measure under a changed filter context.
- 🎯 **`PREVIOUSMONTH()` Purpose:** Supplies the dates from the immediately preceding month.
- 🧭 **Target:** Compare current Production Quantity with the previous month's production.

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

- 🎯 **`DIVIDE()` Purpose:** Calculates a ratio safely when the denominator may be zero or blank.
- 🧭 **Target:** Express the month-over-month production change as a percentage.

### ✅ Validation — Previous Month, MoM Variance, and MoM %

Use the **raw `DimDate[Date]` field**, not the automatic Date Hierarchy.

#### Step 1 — Select One Complete Month

- 🛠️ Add `DimDate[Date]` to a slicer.
- 🛠️ Set the slicer type to **Between**.
- 🛠️ Select one complete month, for example:
  - From: `01-May-2024`
  - To: `31-May-2024`

#### Step 2 — Add Four Card Visuals

Create separate Cards for:

- `[Production Quantity]`
- `[Production Previous Month]`
- `[Production MoM Variance]`
- `[Production MoM %]`

#### Step 3 — Verify the Expected Behavior

- ✅ `[Production Quantity]` → production for the selected/current month.
- ✅ `[Production Previous Month]` → production for the immediately preceding month.
- ✅ `[Production MoM Variance]` → Current Production − Previous Month Production.
- ✅ `[Production MoM %]` → MoM Variance ÷ Previous Month Production.

### 🧮 Manual Cross-Check

For May 2024:

- Current Production = `613,548`
- Previous Month Production = `564,164`

```text
MoM Variance
= 613,548 - 564,164
= 49,384
```

```text
MoM %
= 49,384 ÷ 564,164
≈ 8.75%
```

Expected Cards:

| Measure | Expected Value |
|---|---:|
| Production Quantity | 613,548 |
| Production Previous Month | 564,164 |
| Production MoM Variance | 49,384 |
| Production MoM % | 8.75% |

### 💡 Interpretation

- Positive MoM Variance / % → production increased.
- Negative MoM Variance / % → production decreased.
- `0%` → no month-over-month change.

> 💡 **Teaching Point:** Manually verify at least one MoM example. A DAX measure returning a number does not automatically mean the result is correct.

> ⚠️ Avoid the automatic **Year → Quarter → Month** Date Hierarchy for this first `PREVIOUSMONTH()` demonstration because additional hierarchy filters can make the result blank or confusing.

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

- 🎯 **`SAMEPERIODLASTYEAR()` Purpose:** Returns the corresponding Date period one year earlier.
- 🧭 **Target:** Compare current production with the same period in the previous year.

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

- 🧭 **Target of `DIVIDE()`:** Convert the year-over-year production variance into a safe percentage calculation.

### ✅ Validation — Previous Year, YoY Variance, and YoY %

Use the same **raw `DimDate[Date]` Between slicer** and select one complete month that has prior-year data.

For example:

- From: `01-May-2024`
- To: `31-May-2024`

Create four Cards:

- `[Production Quantity]`
- `[Production Previous Year]`
- `[Production YoY Variance]`
- `[Production YoY %]`

### ✅ Expected Behavior

- `[Production Quantity]` → production for May 2024.
- `[Production Previous Year]` → production for May 2023.
- `[Production YoY Variance]` → Current Production − Previous Year Production.
- `[Production YoY %]` → YoY Variance ÷ Previous Year Production.

### 🧮 Manual Cross-Check

Using the practice data:

- May 2024 Production = `613,548`
- May 2023 Production = `655,701`

```text
YoY Variance
= 613,548 - 655,701
= -42,153
```

```text
YoY %
= -42,153 ÷ 655,701
≈ -6.43%
```

Expected Cards:

| Measure | Expected Value |
|---|---:|
| Production Quantity | 613,548 |
| Production Previous Year | 655,701 |
| Production YoY Variance | -42,153 |
| Production YoY % | -6.43% |

> 💡 If the selected period has no corresponding prior-year production data, `[Production Previous Year]` may legitimately be blank.

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

- 🎯 **`TOTALMTD()` Purpose:** Accumulates a measure from the beginning of the current month.
- 🧭 **Target:** Show production achieved so far within the selected month.

### Quarter-to-Date

```DAX
Production QTD =
TOTALQTD(
    [Production Quantity],
    DimDate[Date]
)
```

- 🎯 **`TOTALQTD()` Purpose:** Accumulates a measure from the beginning of the current quarter.
- 🧭 **Target:** Show production achieved so far within the selected quarter.

### Calendar Year-to-Date

```DAX
Production Calendar YTD =
TOTALYTD(
    [Production Quantity],
    DimDate[Date]
)
```

- 🎯 **`TOTALYTD()` Purpose:** Accumulates a measure from the beginning of the year.
- 🧭 **Target:** Show cumulative production from January 1 to the selected date.

### 💡 Teaching Point

- **MTD** → start of month to current date
- **QTD** → start of quarter to current date
- **YTD** → start of year to current date

### ✅ Validation — MTD, QTD, and Calendar YTD

Use the **raw `DimDate[Date]` field** in a slicer, not the automatic Date Hierarchy.

#### Step 1 — Select a Partial-Month Range

- 🛠️ Set the slicer type to **Between**.
- 🛠️ Select:
  - From: `01-May-2024`
  - To: `15-May-2024`

#### Step 2 — Add Four Card Visuals

- `[Production Quantity]`
- `[Production MTD]`
- `[Production QTD]`
- `[Production Calendar YTD]`

#### Step 3 — Verify the Time Windows

- ✅ `[Production Quantity]` → production visible in the selected Date range.
- ✅ `[Production MTD]` → production from the beginning of May 2024 through May 15, 2024.
- ✅ `[Production QTD]` → production from April 1, 2024 through May 15, 2024.
- ✅ `[Production Calendar YTD]` → production from January 1, 2024 through May 15, 2024.

### 💡 Relative Check

For the same ending date, the accumulation window normally becomes wider:

```text
MTD ⊆ QTD ⊆ Calendar YTD
```

Where production exists in the earlier periods:

```text
Production MTD ≤ Production QTD ≤ Production Calendar YTD
```

> 💡 Use a **partial-month** range for demonstration. If the entire month is selected, MTD may appear equal to the month's Production Quantity, which is correct but less illustrative.

> ⚠️ Validate the **date window and business meaning**, not only whether the Cards contain numbers.

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

- 🎯 **`TOTALYTD()` Purpose here:** Accumulates production using a custom year-end date.
- 🧭 **Target:** Calculate cumulative production for the **April–March fiscal year**.

### 💡 Teaching Point

- Calendar YTD resets on **January 1**.
- Fiscal YTD resets after **March 31**.

### ✅ Validation — Fiscal YTD

Use:

- Fiscal Year slicer
- Month/Fiscal Month visual
- `[Production Quantity]`
- `[Production Fiscal YTD]`

Then:

1. 🛠️ Select one Fiscal Year.
2. 🛠️ Review April, May, June, and later months.
3. ✅ April Fiscal YTD should contain April production only.
4. ✅ May Fiscal YTD should contain April + May production.
5. ✅ June Fiscal YTD should contain April + May + June production.
6. ✅ The cumulative value should continue through March.
7. ✅ When the next Fiscal Year begins in April, Fiscal YTD should restart.

> 💡 **Teaching Point:** Fiscal YTD validates both the DAX formula and the April–March fiscal-calendar requirement.

---

## 💻 6. Production Plan Measure

### Business Question

> How much production was planned?

Create:

```DAX
Planned Production =
SUM(FactProductionPlan[PlannedProductionUnits])
```

- 🎯 **`SUM()` Purpose:** Adds numeric values in a column under the current filter context.
- 🧭 **Target:** Calculate total Planned Production for the selected Month, Product, and Plant.

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

- 🎯 **`DIVIDE()` Purpose here:** Safely divides Actual Production by Planned Production.
- 🧭 **Target:** Show how much of the production plan was achieved as a percentage.

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

### ✅ Validation — Plan vs Actual

Use a **Matrix visual** to validate Plan vs Actual at a compatible business grain.

#### 🛠️ Visual Type

**Matrix**

#### 🛠️ Configure the Matrix

**Rows**
- `DimDate[FiscalYearMonth]` / Fiscal Month

**Values**
- `[Production Quantity]`
- `[Planned Production]`
- `[Production Variance]`
- `[Plan Attainment %]`

**Slicers**
- `DimProduct[ProductName]`
- `DimPlant[PlantName]`

### ✅ Validation Steps

1. Select one **Product**.
2. Select one **Plant**.
3. Review one Fiscal Month, for example a month in **FY2024-25**.
4. Verify:

   **Production Variance = Production Quantity − Planned Production**

5. Verify:

   **Plan Attainment % = Production Quantity ÷ Planned Production**

### 💡 Interpretation

- Positive Variance → Actual Production is above Plan.
- Negative Variance → Actual Production is below Plan.
- `100%` Attainment → Actual exactly meets Plan.
- Above `100%` → Plan exceeded.
- Below `100%` → Plan not fully achieved.

### 🧮 Manual Cross-Check

Choose one row from the Matrix and manually calculate:

```text
Variance = Actual - Plan
Plan Attainment % = Actual ÷ Plan

Confirm:

- ✅ Actual and Plan respond to the same Fiscal Month, Product, and Plant selection.
- ✅ `Production Variance = Production Quantity − Planned Production`.
- ✅ `Plan Attainment % = Production Quantity ÷ Planned Production`.
- ✅ Positive Variance means Actual is above Plan.
- ✅ Negative Variance means Actual is below Plan.
- ✅ `100%` attainment means Actual exactly matches Plan.

### 🧮 Manual Cross-Check

Pick **one Fiscal Month + one Product + one Plant** from the visual and manually verify:

```text
Variance = Actual - Plan
Attainment % = Actual ÷ Plan
```

> ⚠️ Do not compare daily production directly with the monthly plan.

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

- 🎯 **`USERELATIONSHIP()` Purpose:** Uses the specified inactive relationship for this calculation.
- 🎯 **`CALCULATE()` Purpose here:** Re-evaluates `[Production Quantity]` using that alternative Date relationship.
- 🧭 **Target:** Analyze production by **Release Date** instead of the default **Manufacture Date**.

### 💡 Interpretation

`USERELATIONSHIP()` tells **this measure only** to use the inactive Release Date relationship.

It does **not** permanently change the semantic model.

### ✅ Validation — Active vs Inactive Date Relationship

Use the **same raw Date selection** for both measures and display them side by side.

Create:

- Date / Month
- `[Production Quantity]`
- `[Released Production]`

#### Step 1 — No Date Filter

- ✅ Compare the overall totals.
- 💡 They may be the same because no Date relationship is restricting the fact rows.

#### Step 2 — Apply One Date/Month Filter

Use the same Date selection for both measures.

Interpretation:

- `[Production Quantity]` → uses the active **Manufacture Date** relationship.
- `[Released Production]` → uses the inactive **Release Date** relationship through `USERELATIONSHIP()`.

#### Step 3 — Explain the Business Meaning

- ✅ Different values are valid because the **same Produced Quantity** is being viewed through two different Date roles.
- ✅ `USERELATIONSHIP()` changes the Date lens for `[Released Production]` only.
- ✅ The model relationship itself is not permanently changed.

> 💡 **Teaching Point:**  
> Without `USERELATIONSHIP()` → **When was it manufactured?**  
> With `USERELATIONSHIP()` → **When was it released?**

> 🖼️ **Image Placeholder S06-03:** Comparison of Production by Manufacture Date and Release Date using `USERELATIONSHIP()`.  
> **Planned file:** `images/S06_03_USERELATIONSHIP.png`

---

## ✅ Validation Rule

For every DAX measure, validate three things:

1. **Base Value** — Does the measure return a sensible value without filters?
2. **Filter Response** — Does it change correctly with Date, Product, or Plant selections?
3. **Business Meaning** — Does the result answer the intended business question?

> 💡 A DAX formula is not considered validated only because it returns a number.

---

## 💻 9. Simple Validation Page — Consolidation

Create one compact report page only to **consolidate and verify the measures already created**.  
Do not introduce new DAX here.

### Slicers

- `DimPlant[PlantName]`
- `DimProduct[ProductName]`
- `DimDate[Date]`

### Visual 1 — Current vs Previous Period

- `[Production Quantity]`
- `[Production Previous Month]`
- `[Production MoM Variance]`
- `[Production MoM %]`
- `[Production Previous Year]`
- `[Production YoY Variance]`
- `[Production YoY %]`

### Visual 2 — Plan vs Actual

- `[Production Quantity]`
- `[Planned Production]`
- `[Production Variance]`
- `[Plan Attainment %]`

### Visual 3 — Date Role

- `[Production Quantity]`
- `[Released Production]`

### ✅ Final Consolidation Check

Confirm that:

- ✅ Every base measure returns a sensible value before filters are applied.
- ✅ Product and Plant slicers filter the relevant measures correctly.
- ✅ Previous Month responds correctly to the **raw Date selection**.
- ✅ MoM Variance and MoM % reconcile with the Current and Previous Month values.
- ✅ Previous Year responds correctly when prior-year data exists.
- ✅ YoY Variance and YoY % reconcile with the Current and Previous Year values.
- ✅ MTD/QTD/YTD use the intended accumulation windows.
- ✅ Fiscal YTD follows the April–March fiscal year and resets in April.
- ✅ Plan vs Actual is compared at **Fiscal Month + Product + Plant** grain.
- ✅ Production Variance and Plan Attainment % reconcile manually for at least one selection.
- ✅ `[Production Quantity]` and `[Released Production]` use different Date roles under the same Date selection.
- ✅ `USERELATIONSHIP()` affects only `[Released Production]`.

---

## 🚀 10. Optional Topics — Mention Only

If time permits, briefly mention:

- `RANKX()`  
  - 🎯 **Purpose:** Rank rows/items based on a measure or expression.  
  - 🧭 **Target:** Rank Products or Plants by Production Quantity.

- `SELECTEDVALUE()`  
  - 🎯 **Purpose:** Return the single selected value in the current filter context.  
  - 🧭 **Target:** Read the KPI selected by a learner/user from a slicer.

- `SWITCH()`  
  - 🎯 **Purpose:** Return different results based on a selected condition or value.  
  - 🧭 **Target:** Switch dynamically between Production, Yield, Rejection, or another KPI.

- **Field Parameters** → dynamic report interaction *(Power BI feature, not a DAX function)*

⚠️ Do not make these mandatory hands-on exercises in this session.

They will fit better in the later **Advanced Reporting and Interactivity** session.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Create `[Production Previous Month]`.
2. 💻 Create `[Production MoM Variance]`.
3. 💻 Create `[Production MoM %]`.
4. 💻 Validate one MoM calculation manually.
5. 💻 Create `[Production Previous Year]`.
6. 💻 Create `[Production YoY Variance]`.
7. 💻 Create `[Production YoY %]`.
8. 💻 Validate one YoY calculation manually.
9. 💻 Create `[Production Fiscal YTD]`.
10. 💻 Create `[Planned Production]`.
11. 💻 Create `[Production Variance]`.
12. 💻 Create `[Plan Attainment %]`.
13. 💻 Create `[Released Production]` using `USERELATIONSHIP()`.
14. 💻 Validate Previous Month / Previous Year using the **raw Date slicer**.
15. 💻 Validate Plan vs Actual at **Fiscal Month + Product + Plant** grain.
16. 💻 Compare `[Production Quantity]` and `[Released Production]` under the same Date selection.

### ✅ Expected Outcome

Learners can create understandable advanced DAX measures for **previous-period analysis, fiscal reporting, Plan vs Actual, and inactive relationships** without using unnecessarily complex formulas.

---

## 💡 Trainer Guidelines

- 💡 Use **one business question → one short formula → one validation visual**.
- 💡 Validate every measure using **Base Value → Filter Response → Business Meaning**.
- 💡 Manually reconcile at least one **MoM**, one **YoY**, and one **Plan vs Actual** calculation during the demonstration.
- 💡 For every DAX function, state **Purpose → Target → Result** before explaining syntax.
- 💡 Reuse the base measures created in Section 05.
- 💡 Keep the Date dimension visible while explaining time intelligence.
- 💡 Start Previous Month / Previous Year with a simple **Date slicer** rather than a complex fiscal Matrix.
- 💡 Use **May 2024** as the default demonstration month for consistency across the session.
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
