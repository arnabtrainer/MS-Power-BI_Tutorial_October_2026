# Section 05 — DAX Fundamentals

**Day:** 3 — Pre-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Understand the purpose of **DAX** in Power BI.
- 🎯 Differentiate **measures** from **calculated columns**.
- 🎯 Create basic aggregation measures using `SUM`, `AVERAGE`, `COUNT`, `COUNTROWS`, `MIN`, and `MAX`.
- 🎯 Understand **row context** and **filter context**.
- 🎯 Use iterator functions such as `SUMX` and `AVERAGEX`.
- 🎯 Modify filter context using `CALCULATE`.
- 🎯 Use `FILTER`, `ALL` / `REMOVEFILTERS`, `DIVIDE`, and simple `VAR` / `RETURN`.
- 🎯 Create reusable DAX measures for the **Nirvaan Pharma Ltd** model.

---

## 🗂️ Resources Used

### Primary Classwork

- 🗂️ `Classwork Files/ClassWork-4 (DAX).pbix`
- 🗂️ `Classwork Files/DAX Classwork.md`

### Generic Practice Dataset

- 🗂️ `PracticeData.xlsx`
- 🗂️ Worksheet: `RN_East1`

For the DAX classwork, the month columns are unpivoted into:

- `Product`
- `Month`
- `EastSales`

### Nirvaan Pharma Ltd Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

Primary tables used:

- `FactProduction`
- `DimProduct`
- `DimPlant`
- `DimDate`

---

## 📚 DAX Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | DAX Basics | Measures and calculated columns | 🧑‍🏫 Demo |
| 2 | Aggregations | SUM, AVERAGE, COUNT, MIN, MAX | 💻 Guided |
| 3 | COUNTROWS / DISTINCTCOUNT | Counting records and entities | 💻 Guided |
| 4 | Row vs Filter Context | Understand DAX evaluation | 🧑‍🏫 Demo |
| 5 | Iterator Functions | SUMX, AVERAGEX, MINX, MAXX | 💻 Guided |
| 6 | CALCULATE | Modify filter context | 💻 Guided |
| 7 | FILTER | Return filtered tables | 💻 Guided |
| 8 | ALL / REMOVEFILTERS | Ignore selected filters | 🧑‍🏫 Demo |
| 9 | DIVIDE | Safe ratio calculations | 💻 Guided |
| 10 | VAR / RETURN | Improve measure readability | 💻 Guided |
| 11 | Pharma Measures | Production KPIs | 💻 Guided |

> 💡 **Scope:** Time intelligence, `USERELATIONSHIP()`, rankings, dynamic selections, and advanced context manipulation are covered in **Section 06**.


### 🧭 DAX Function — Purpose and Target Map

| **DAX Function / Construct** | **Purpose** | **Target in This Section** |
|---|---|---|
| `SUM()` | Adds numeric values in a column | Total Sales, Production Quantity, Good Quantity, Rejected Quantity, Production Cost |
| `AVERAGE()` | Returns the arithmetic mean of a numeric column | Average Sales |
| `COUNT()` | Counts non-blank numeric values | Count populated Sales values |
| `COUNTROWS()` | Counts rows in a table | Count Sales rows |
| `DISTINCTCOUNT()` | Counts unique values in a column | Count unique Products or Batches |
| `MIN()` / `MAX()` | Return the minimum / maximum value in a column | Identify lowest and highest Sales |
| `IF()` | Returns one result when a condition is true and another when false | Create a simple Sales classification column |
| `SUMX()` | Evaluates an expression row by row and sums the results | Calculate row-level GST values and total them |
| `AVERAGEX()` | Evaluates an expression row by row and averages the results | Average row-level GST |
| `MINX()` / `MAXX()` | Evaluate an expression row by row and return minimum / maximum | Lowest / highest row-level GST |
| `CALCULATE()` | Re-evaluates an expression under modified filter context | Calculate Sales for a selected Month/Product combination |
| `FILTER()` | Returns a filtered table | Supply only the required rows to another DAX calculation |
| `ALL()` | Removes filters from a table/column and returns all values | Compare filtered Sales with overall Sales |
| `REMOVEFILTERS()` | Clears selected filter context | Ignore Month while keeping other filters |
| `DIVIDE()` | Performs safe division with an alternate result | Yield %, Rejection %, Average Production per Batch |
| `VAR` / `RETURN` | Store and reuse intermediate values | Make larger measures easier to read and maintain |
| `STDEV.S()` | Calculates sample standard deviation | Optional: measure Sales variability |
| `VAR.S()` | Calculates sample variance | Optional: measure Sales dispersion |

> 💡 **Learner Connection:** Start with the **business question**, then identify which DAX function helps answer it.

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:20 | 📚 DAX purpose, measures vs calculated columns |
| 00:20–00:50 | 💻 Basic aggregation measures |
| 00:50–01:15 | 🧑‍🏫 Row context vs filter context |
| 01:15–01:40 | 💻 Iterator functions |
| 01:40–02:10 | 💻 CALCULATE and FILTER |
| 02:10–02:30 | 🧑‍🏫 ALL / REMOVEFILTERS and DIVIDE |
| 02:30–02:50 | 💻 Nirvaan Pharma Ltd production measures |
| 02:50–03:00 | 🔁 Recap and guided challenge review |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. What is DAX?

**DAX (Data Analysis Expressions)** is the formula language used in Power BI semantic models for analytical calculations.

DAX is commonly used to create:

- 📚 Measures
- 📚 Calculated columns
- 📚 Calculated tables
- 📚 Filter-aware business calculations

### 💡 Key Principle

Power Query prepares the data **before loading**.  
DAX performs calculations **inside the semantic model**.

---

## 📚 2. Measures vs Calculated Columns

| Feature | Measure | Calculated Column |
|---|---|---|
| Calculation | Evaluated when required | Calculated row by row |
| Responds to slicers | ✅ Yes | Value itself is stored |
| Stored in model | Formula only | Result stored for every row |
| Typical use | KPI, total, ratio, variance | Classification, row-level attribute |

### Example Measure

```DAX
TotalSales =
SUM(RN_East1[EastSales])
```

- 🎯 **`SUM()` Purpose:** Adds numeric values in a column under the current filter context.
- 🧭 **Target:** Calculate Total Sales that automatically responds to Month/Product filters.

### Example Calculated Column (Table View → RN_East1 → New Column)

```DAX
SalesBand =
IF(
    RN_East1[EastSales] >= 4500,
    "High",
    "Regular"
)
```

- 🎯 **`IF()` Purpose:** Returns one result when a condition is true and another when it is false.
- 🧭 **Target:** Classify each Sales row as `High` or `Regular`.

### 💡 Guidance

Use a **measure** when the result should change with report filters.

Use a **calculated column** when a persistent row-level value is required.

---

<img width="1712" height="795" alt="Comparison of a Power BI measure and calculated column with examples" src="https://github.com/user-attachments/assets/f30e8d88-ed21-47ca-a085-ac1f27c9d5b0" />

**Figure S05-01 — DAX Measures vs Calculated Columns: Key Differences**

---

## 💻 3. Create Basic Aggregation Measures

Use:

- 🗂️ `PracticeData.xlsx`
- 🗂️ `RN_East1`

### Total Sales

```DAX
TotalSales =
SUM(RN_East1[EastSales])
```

- 🎯 **`SUM()` Purpose:** Add all visible Sales values.
- 🧭 **Target:** Show total Sales for the current Product/Month filter context.

### Average Sales

```DAX
AverageSales =
AVERAGE(RN_East1[EastSales])
```

- 🎯 **`AVERAGE()` Purpose:** Calculate the arithmetic mean of visible numeric values.
- 🧭 **Target:** Show typical/average Sales under the current filters.

### Count of Non-Blank Sales Values

```DAX
CountSale =
COUNT(RN_East1[EastSales])
```

- 🎯 **`COUNT()` Purpose:** Count non-blank numeric values in a column.
- 🧭 **Target:** Count how many Sales values are present in the current context.

### Maximum and Minimum

```DAX
MaxSales =
MAX(RN_East1[EastSales])
```

- 🎯 **`MAX()` Purpose:** Return the highest visible Sales value.
- 🧭 **Target:** Identify the maximum Sales value under the current filters.

```DAX
MinSales =
MIN(RN_East1[EastSales])
```

- 🎯 **`MIN()` Purpose:** Return the lowest visible Sales value.
- 🧭 **Target:** Identify the minimum Sales value under the current filters.

### ✅ Validation

Create:

- Card → `[TotalSales]`
- Card → `[AverageSales]`
- Card → `[CountSale]`
- Card → `[MaxSales]`
- Card → `[MinSales]`
- Table → `Product`, `Month`, and the measures above

Then:

- 🛠️ Add a `Month` slicer.
- 🛠️ Select one Month and confirm every measure recalculates.
- 🛠️ Add a `Product` slicer and select one Product.
- ✅ `TotalSales`, `AverageSales`, `MinSales`, and `MaxSales` should change with the filter context.
- ✅ `CountSale` should show the number of non-blank Sales values in the selected context.

---

## 💻 4. COUNT, COUNTROWS, and DISTINCTCOUNT

These functions answer different questions.

### Count Non-Blank Numeric Values

```DAX
CountSale =
COUNT(RN_East1[EastSales])
```

- 🎯 **`COUNT()` Purpose:** Count non-blank numeric values.
- 🧭 **Target:** Count populated Sales values, not necessarily all table rows.

### Count Table Rows

```DAX
SalesRowCount =
COUNTROWS(RN_East1)
```

- 🎯 **`COUNTROWS()` Purpose:** Count the rows in a table or table expression.
- 🧭 **Target:** Count all Sales rows currently visible after filters.

### Count Distinct Products

```DAX
ProductCount =
DISTINCTCOUNT(RN_East1[Product])
```

- 🎯 **`DISTINCTCOUNT()` Purpose:** Count unique values in a column.
- 🧭 **Target:** Count how many different Products exist in the current context.

### 💡 Simple Rule

- `COUNT()` → counts non-blank values in a column.
- `COUNTROWS()` → counts rows in a table.
- `DISTINCTCOUNT()` → counts unique values.


### ✅ Validation

Create three Cards:

- `[CountSale]`
- `[SalesRowCount]`
- `[ProductCount]`

Then filter by one Product.

- ✅ `[ProductCount]` should become `1`.
- ✅ `[SalesRowCount]` should show all rows for that Product.
- ✅ `[CountSale]` should count only non-blank numeric Sales values.

---

## 📚 5. Row Context vs Filter Context

This is one of the most important DAX concepts.

### Row Context

Row context means:

> **“Which row am I currently evaluating?”**

It commonly exists in:

- calculated columns
- iterator functions such as `SUMX`

### Filter Context

Filter context means:

> **“Which subset of the model is currently visible to this calculation?”**

It can come from:

- slicers
- visual rows/columns
- filters
- relationships
- `CALCULATE()`

### Example

If a visual displays `TotalSales` by Month:

```DAX
TotalSales =
SUM(RN_East1[EastSales])
```

the same measure is evaluated separately under each Month's **filter context**.

---

<img width="1860" height="791" alt="Diagram explaining DAX row context and filter context" src="https://github.com/user-attachments/assets/740a866d-46f7-427d-8a66-db529807c504" />

**Figure S05-02 — DAX Evaluation Context: Row Context vs Filter Context**

---

## 💻 6. Iterator Functions — X Functions

Iterator functions evaluate an expression **row by row** over a table.

### `SUMX`

Assume an 18% tax for demonstration:

```DAX
GSTSalesSumX =
SUMX(
    RN_East1,
    RN_East1[EastSales] * 0.18
)
```

- 🎯 **`SUMX()` Purpose:** Evaluate an expression row by row and sum the results.
- 🧭 **Target:** Calculate 18% GST for every Sales row and then total the GST.

### `AVERAGEX`

```DAX
GSTSalesAvgX =
AVERAGEX(
    RN_East1,
    RN_East1[EastSales] * 0.18
)
```

- 🎯 **`AVERAGEX()` Purpose:** Evaluate an expression row by row and average the results.
- 🧭 **Target:** Calculate the average row-level GST amount.

### `MINX`

```DAX
GSTSalesMinX =
MINX(
    RN_East1,
    RN_East1[EastSales] * 0.18
)
```

- 🎯 **`MINX()` Purpose:** Evaluate an expression row by row and return the smallest result.
- 🧭 **Target:** Find the lowest row-level GST amount.

### `MAXX`

```DAX
GSTSalesMaxX =
MAXX(
    RN_East1,
    RN_East1[EastSales] * 0.18
)
```

- 🎯 **`MAXX()` Purpose:** Evaluate an expression row by row and return the largest result.
- 🧭 **Target:** Find the highest row-level GST amount.

### 💡 Difference

```text
SUM(Column)
```

aggregates an existing column.

```text
SUMX(Table, Expression)
```

evaluates an expression row by row and then sums the results.


### ✅ Validation

Create a table with:

- `Product`
- `EastSales`
- `[GSTSalesSumX]`

Then apply a Product slicer.

- ✅ `[GSTSalesSumX]` should recalculate for the selected Product.
- 💡 Compare the result conceptually with `TotalSales × 18%` to confirm the iterator is producing the expected total.

---

## 💻 7. CALCULATE — Modify Filter Context

`CALCULATE()` is one of the most important DAX functions.

### Mental Model

> **CALCULATE = evaluate this expression under modified filters.**

Example:

```DAX
AugP013Sales =
CALCULATE(
    [TotalSales],
    RN_East1[Month] = "AUG",
    RN_East1[Product] = "P013"
)
```

- 🎯 **`CALCULATE()` Purpose:** Evaluate an expression after modifying filter context.
- 🧭 **Target:** Return Total Sales specifically for `AUG` and Product `P013`.

This evaluates `[TotalSales]` using:

- Month = `AUG`
- Product = `P013`

### 💡 Teaching Point

`CALCULATE()` does not simply “filter rows.”  
Its major role is to **change filter context before evaluating an expression**.


### ✅ Validation

Create:

- Card → `[TotalSales]`
- Card → `[AugP013Sales]`
- Month slicer
- Product slicer

Then change the slicers.

- ✅ `[TotalSales]` should follow the slicer selections.
- ✅ `[AugP013Sales]` should continue to represent the DAX-defined `AUG` + `P013` context.

---

## 💻 8. FILTER — Return a Filtered Table

`FILTER()` returns a table containing only rows that satisfy a condition.

Example:

```DAX
AugSales =
CALCULATE(
    [TotalSales],
    FILTER(
        RN_East1,
        RN_East1[Month] = "AUG"
    )
)
```

- 🎯 **`FILTER()` Purpose:** Return only the rows that satisfy a condition.
- 🧭 **Target:** Supply only `AUG` rows to `CALCULATE()` for the Sales calculation.

### 💡 Difference from CALCULATE

- `CALCULATE()` → changes filter context and evaluates an expression.
- `FILTER()` → returns a filtered table that another DAX function can use.

⚠️ Do not describe `FILTER()` as a direct substitute for `CALCULATE()`.


### ✅ Validation

Create:

- Card → `[TotalSales]`
- Card → `[AugSales]`

Then select another Month in a slicer.

- ✅ `[TotalSales]` should change with the slicer.
- ✅ `[AugSales]` should continue to calculate using the August rows defined by the measure.

---

## 🧑‍🏫 9. Ignore Filters with ALL / REMOVEFILTERS

### Using `ALL`

```DAX
TotalSalesAll =
CALCULATE(
    [TotalSales],
    ALL(RN_East1)
)
```

- 🎯 **`ALL()` Purpose:** Remove filters and return all rows/values from the specified table or column.
- 🧭 **Target:** Show overall Sales even when the report is filtered.

This removes filters from the entire `RN_East1` table.

### Using `REMOVEFILTERS`

```DAX
TotalSalesNoMonthFilter =
CALCULATE(
    [TotalSales],
    REMOVEFILTERS(RN_East1[Month])
)
```

- 🎯 **`REMOVEFILTERS()` Purpose:** Clear filter context from the specified table or column.
- 🧭 **Target:** Ignore the Month filter while preserving other filters such as Product.

This removes only the Month filter.

### ✅ Validation

Create a table containing:

- `Product`
- `[TotalSales]`
- `[TotalSalesAll]`
- `[TotalSalesNoMonthFilter]`

Add:

- Month slicer
- Product slicer

Then:

- ✅ `[TotalSales]` should respond to both Month and Product filters.
- ✅ `[TotalSalesAll]` should ignore filters from `RN_East1`.
- ✅ `[TotalSalesNoMonthFilter]` should ignore Month but continue to respond to Product.

**Outcome:** Learners see the difference between removing **all table filters** and removing **one selected filter**.

---

## 💻 10. Safe Ratios with DIVIDE

Prefer `DIVIDE()` for ratios because it handles division-by-zero safely.

### Nirvaan Pharma Ltd Example

```DAX
Production Quantity =
SUM(FactProduction[ProducedQtyUnits])
```

- 🎯 **`SUM()` Purpose here:** Add all produced units in the current filter context.
- 🧭 **Target:** Provide the denominator/base production measure for production KPIs.

```DAX
Good Quantity =
SUM(FactProduction[GoodQtyUnits])
```

- 🎯 **`SUM()` Purpose here:** Add all good units in the current filter context.
- 🧭 **Target:** Provide the numerator for Yield %.

```DAX
Yield % =
DIVIDE(
    [Good Quantity],
    [Production Quantity],
    0
)
```

- 🎯 **`DIVIDE()` Purpose:** Perform safe division and return an alternate result when the denominator is zero/blank.
- 🧭 **Target:** Calculate the percentage of produced units that are good units.

### 💡 Why `DIVIDE()`?

It is safer than:

```DAX
[Good Quantity] / [Production Quantity]
```

when the denominator may be zero or blank.


### ✅ Validation

Create Cards for:

- `[Production Quantity]`
- `[Good Quantity]`
- `[Yield %]`

Then apply Product and Plant slicers.

- ✅ `[Yield %]` should recalculate as Good Quantity ÷ Production Quantity.
- ✅ If Production Quantity becomes zero/blank, the measure should safely return the alternate result `0`.

---

## 💻 11. VAR and RETURN

Variables improve readability and avoid repeating expressions.

Example:

```DAX
Rejection % =
VAR ProducedQty =
    SUM(FactProduction[ProducedQtyUnits])
VAR RejectedQty =
    SUM(FactProduction[RejectedQtyUnits])
RETURN
    DIVIDE(RejectedQty, ProducedQty, 0)
```

- 🎯 **`VAR` Purpose:** Store an intermediate result with a meaningful name.
- 🎯 **`RETURN` Purpose:** Return the final expression after the variables are defined.
- 🧭 **Target:** Keep the Rejection % measure readable by naming Produced and Rejected quantities before calculating the ratio.

### 💡 Benefits

- 💡 Easier to read
- 💡 Easier to debug
- 💡 Avoids repeating the same expression
- 💡 Useful in larger DAX measures


### ✅ Validation

Create Cards for:

- `[Rejected Quantity]`
- `[Production Quantity]`
- `[Rejection %]`

Then filter by Product or Plant.

- ✅ Rejection % should recalculate using the selected context.
- 💡 Compare the displayed ratio with `Rejected Quantity ÷ Production Quantity`.

---

## 💻 12. Nirvaan Pharma Ltd — Core Production Measures

Create the following measures.

### Production Quantity

```DAX
Production Quantity =
SUM(FactProduction[ProducedQtyUnits])
```

### Good Quantity

```DAX
Good Quantity =
SUM(FactProduction[GoodQtyUnits])
```

### Rejected Quantity

```DAX
Rejected Quantity =
SUM(FactProduction[RejectedQtyUnits])
```

- 🎯 **`SUM()` Purpose:** Add rejected units under the current filters.
- 🧭 **Target:** Measure production loss/rejection volume.

### Production Cost

```DAX
Production Cost =
SUM(FactProduction[ProductionCostINR])
```

- 🎯 **`SUM()` Purpose:** Add production cost values under the current filters.
- 🧭 **Target:** Calculate total production cost by Product, Plant, or Date context.

### Batch Count

```DAX
Batch Count =
DISTINCTCOUNT(FactProduction[BatchKey])
```

- 🎯 **`DISTINCTCOUNT()` Purpose:** Count unique Batch keys.
- 🧭 **Target:** Measure how many distinct production batches are represented.

### Yield %

```DAX
Yield % =
DIVIDE(
    [Good Quantity],
    [Production Quantity],
    0
)
```

### Rejection %

```DAX
Rejection % =
DIVIDE(
    [Rejected Quantity],
    [Production Quantity],
    0
)
```

- 🎯 **`DIVIDE()` Target:** Express rejected units as a percentage of total production.

### Average Production per Batch

```DAX
Avg Production per Batch =
DIVIDE(
    [Production Quantity],
    [Batch Count],
    0
)
```

- 🎯 **`DIVIDE()` Target:** Calculate average produced units per distinct batch.

### ✅ Validation

Create a Matrix:

**Rows**

- `DimProduct[ProductName]`

**Columns / Slicer**

- `DimPlant[PlantName]`

**Values**

- `[Production Quantity]`
- `[Good Quantity]`
- `[Rejected Quantity]`
- `[Production Cost]`
- `[Batch Count]`
- `[Yield %]`
- `[Rejection %]`
- `[Avg Production per Batch]`

Then:

- 🛠️ Select one Plant and verify all measures change.
- 🛠️ Select one Product and verify all measures change again.
- ✅ `Good Quantity + Rejected Quantity` should reconcile with Production Quantity for the underlying production records.
- ✅ Yield % and Rejection % should behave as ratios, not fixed stored values.
- ✅ Batch Count should count unique Batch keys, not production rows.

---

<img width="1792" height="922" alt="Nirvaan Pharma Ltd production KPI measures displayed in Power BI" src="https://github.com/user-attachments/assets/72c4a85a-114d-4cf0-848d-fd3e42767be1" />

**Figure S05-03 — Nirvaan Pharma Ltd Production KPIs: Core DAX Measures**

---

## 📚 13. Optional Statistical Functions

The repository classwork also demonstrates:

- `STDEV.S()`
- `VAR.S()`

Example:

```DAX
SDSales =
STDEV.S(RN_East1[EastSales])
```

- 🎯 **`STDEV.S()` Purpose:** Measure sample standard deviation—how spread out values are around the mean.
- 🧭 **Target:** Demonstrate Sales variability across observations.

```DAX
VarSales =
VAR.S(RN_East1[EastSales])
```

- 🎯 **`VAR.S()` Purpose:** Measure sample variance.
- 🧭 **Target:** Demonstrate another way to quantify Sales dispersion.

🚀 Use these as an **optional demonstration** if time permits.  
They are not required before moving to Section 6.


### ✅ Optional Validation

Create Cards for:

- `[SDSales]`
- `[VarSales]`

Apply a Product or Month filter.

- ✅ Both values should recalculate for the selected subset.
- 💡 Explain that larger values generally indicate greater spread/variability.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Create `[TotalSales]`.
2. 💻 Create `[AverageSales]`.
3. 💻 Create `[SalesRowCount]`.
4. 💻 Create `[ProductCount]`.
5. 💻 Create one `SUMX()` measure.
6. 💻 Create one measure using `CALCULATE()`.
7. 💻 Create one measure using `FILTER()`.
8. 💻 Compare `[TotalSales]` with `[TotalSalesAll]`.
9. 💻 Create `[Production Quantity]`.
10. 💻 Create `[Good Quantity]` and `[Rejected Quantity]`.
11. 💻 Create `[Yield %]` using `DIVIDE()`.
12. 💻 Create `[Rejection %]` using `VAR` / `RETURN`.
13. 💻 Validate the measures using Product and Plant filters.

### ✅ Expected Outcome

Learners can create reusable measures and explain how filter context changes their results.

---

## 💡 Trainer Guidelines

- 💡 Teach **measures first**; avoid creating unnecessary calculated columns.
- 💡 For every DAX function, explain **Purpose → Target → Formula → Validation**.
- 💡 Explain the difference between **row context** and **filter context** carefully.
- 💡 Reinforce `CALCULATE()` as a **filter-context modifier**.
- 💡 Explain that `FILTER()` returns a table.
- 💡 Use `DIVIDE()` for business ratios.
- 💡 Encourage measure reuse, for example `[Yield %]` reusing `[Good Quantity]` and `[Production Quantity]`.
- 💡 Keep statistical functions optional if time is limited.
- ⚠️ Do not introduce time-intelligence functions yet.
- ⚠️ Do not go deeply into `USERELATIONSHIP()` here; it will be practiced in Section 06.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 Measures vs calculated columns.
- 🔁 Basic aggregation measures.
- 🔁 COUNT vs COUNTROWS vs DISTINCTCOUNT.
- 🔁 Row context vs filter context.
- 🔁 Iterator functions.
- 🔁 `CALCULATE()` and `FILTER()`.
- 🔁 `ALL()` / `REMOVEFILTERS()`.
- 🔁 `DIVIDE()` and `VAR` / `RETURN`.
- 🔁 Reusable production KPI measures.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What is a Power BI measure primarily designed to do?

A. Store a fixed value for every row <br>
B. Calculate a result dynamically according to filter context <br>
C. Replace Power Query completely <br>
D. Create relationships automatically <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Calculate a result dynamically according to filter context**

**Explanation:** Measures are evaluated when needed and respond dynamically to slicers, filters, and visual context.

</details>

### 🔴 Q2. Which DAX function adds values from a numeric column?

A. `SUM()` <br>
B. `FILTER()` <br>
C. `FORMAT()` <br>
D. `RELATED()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `SUM()`**

**Explanation:** `SUM()` returns the total of the numeric values in a column under the current filter context.

</details>

### 🔴 Q3. Which function counts rows in a table?

A. `COUNTROWS()` <br>
B. `SUMX()` <br>
C. `DIVIDE()` <br>
D. `MAX()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `COUNTROWS()`**

**Explanation:** `COUNTROWS()` returns the number of rows in a table or table expression.

</details>

### 🔴 Q4. What does `DISTINCTCOUNT()` return?

A. Total numeric value <br>
B. Number of unique values in a column <br>
C. Highest value in a column <br>
D. Number of report pages <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Number of unique values in a column**

**Explanation:** `DISTINCTCOUNT()` counts unique values, such as unique products, batches, or customers.

</details>

### 🔴 Q5. What does filter context represent?

A. The current subset of model data visible to a calculation <br>
B. Only the current physical row <br>
C. The report theme <br>
D. The data-source password <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. The current subset of model data visible to a calculation**

**Explanation:** Filter context is created by slicers, visual selections, filters, relationships, and DAX functions such as `CALCULATE()`.

</details>

### 🔴 Q6. What is the main difference between `SUM()` and `SUMX()`?

A. `SUMX()` evaluates an expression row by row before summing <br>
B. `SUM()` can only be used with text <br>
C. `SUMX()` creates relationships <br>
D. There is no difference <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `SUMX()` evaluates an expression row by row before summing**

**Explanation:** `SUM()` aggregates one column directly, while `SUMX()` iterates over a table and evaluates an expression for each row.

</details>

### 🔴 Q7. What is the primary role of `CALCULATE()`?

A. Modify filter context and evaluate an expression <br>
B. Rename columns <br>
C. Import CSV files <br>
D. Create report pages <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Modify filter context and evaluate an expression**

**Explanation:** `CALCULATE()` evaluates an expression after applying or modifying filters.

</details>

### 🔴 Q8. What does `FILTER()` return?

A. A table <br>
B. A relationship <br>
C. A report page <br>
D. A Power BI workspace <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. A table**

**Explanation:** `FILTER()` returns a table containing the rows that satisfy the specified condition.

</details>

### 🔴 Q9. What is the purpose of `REMOVEFILTERS()`?

A. Remove selected filter context from a calculation <br>
B. Delete rows permanently from the source <br>
C. Remove Power Query steps <br>
D. Delete relationships <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Remove selected filter context from a calculation**

**Explanation:** `REMOVEFILTERS()` clears filters from specified tables or columns for the current DAX calculation.

</details>

### 🔴 Q10. Why is `DIVIDE()` recommended for ratio calculations?

A. It handles zero or blank denominators safely <br>
B. It automatically creates a Date table <br>
C. It changes relationship direction <br>
D. It imports data automatically <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. It handles zero or blank denominators safely**

**Explanation:** `DIVIDE()` can return an alternate result instead of producing an error when the denominator is zero.

</details>

### 🔴 Q11. What is the main benefit of `VAR` in a DAX measure?

A. It improves readability and avoids repeating expressions <br>
B. It creates an Excel worksheet <br>
C. It changes Power Query data types <br>
D. It publishes the semantic model <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. It improves readability and avoids repeating expressions**

**Explanation:** Variables store intermediate results and make larger DAX measures easier to understand and maintain.

</details>

### 🔴 Q12. Which formula is the safest way to calculate Yield %?

A. `[Good Quantity] + [Production Quantity]` <br>
B. `DIVIDE([Good Quantity], [Production Quantity], 0)` <br>
C. `COUNT([Good Quantity])` <br>
D. `MAX([Production Quantity])` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. `DIVIDE([Good Quantity], [Production Quantity], 0)`**

**Explanation:** Yield is a ratio of good quantity to production quantity, and `DIVIDE()` handles zero denominators safely.

</details>

---

### ➡️ Next Session

**Section 06 — Advanced DAX and Time Intelligence**

Learners will extend DAX skills with **advanced filter context, time intelligence, plan-vs-actual analysis, previous-period comparisons, ranking, dynamic measures, and practical use of inactive relationships**.
