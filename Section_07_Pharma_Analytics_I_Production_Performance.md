# Section 07 — Pharma Analytics I: Production Performance

**Day:** 4 — Pre-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Convert production business questions into suitable Power BI visuals.
- 🎯 Build a focused **Production Performance dashboard** using the existing semantic model.
- 🎯 Reuse the DAX measures created in Sections 05 and 06.
- 🎯 Compare production across **time, plants, and products**.
- 🎯 Monitor **Production Quantity, Good Quantity, Rejected Quantity, Yield %, Rejection %, Cost, and Batch Count**.
- 🎯 Compare **Actual vs Planned Production** using a Combo Chart.
- 🎯 Use slicers, sorting, conditional formatting, and visual interactions effectively.
- 🎯 Validate dashboard numbers before drawing business conclusions.

---

## 🗂️ Resources Used

### Primary Case-Study Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

### Primary Tables

- `FactProduction`
- `FactProductionPlan`
- `DimDate`
- `DimProduct`
- `DimPlant`
- `DimBatch`

### Measures Reused from Section 05

- `[Production Quantity]`
- `[Good Quantity]`
- `[Rejected Quantity]`
- `[Production Cost]`
- `[Batch Count]`
- `[Yield %]`
- `[Rejection %]`
- `[Avg Production per Batch]`

### Measures Reused from Section 06

- `[Production Previous Month]`
- `[Production MoM Variance]`
- `[Production MoM %]`
- `[Planned Production]`
- `[Production Variance]`
- `[Plan Attainment %]`

> 💡 **Prerequisite:** The semantic model, relationships, and measures created in Sections 04–06 should already be available.

> 💡 **Scope:** This session focuses on **production analytics and report building**. Advanced bookmarks, field parameters, custom tooltip pages, and deeper report UX are covered in **Section 10**.

---

## 📚 Production Analytics Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Business Questions | Define production KPIs and analysis goals | 🧑‍🏫 Demo |
| 2 | Dashboard Filters | Fiscal Year, Product, Plant slicers | 💻 Guided |
| 3 | KPI Summary | Production, Yield, Rejection, Cost, Batches | 💻 Guided |
| 4 | Production Trend | Month-wise production analysis | 💻 Guided |
| 5 | Plant Performance | Compare production across plants | 💻 Guided |
| 6 | Product Performance | Compare production across products | 💻 Guided |
| 7 | Yield / Rejection | Identify quality-performance patterns | 💻 Guided |
| 8 | Plan vs Actual | Actual, Plan, Variance, Attainment | 💻 Guided |
| 9 | Detailed Analysis | Matrix and conditional formatting | 💻 Guided |
| 10 | Dashboard Validation | Reconcile numbers and slicer behavior | 💻 Guided |

---

## 🧭 Visual — Purpose and Target Map

| Visual | Purpose | Target in This Session |
|---|---|---|
| **Card** | Highlight one important KPI | Production, Yield %, Rejection %, Cost, Batch Count |
| **Slicer** | Control report filter context | Fiscal Year, Product, Plant |
| **Line Chart** | Show change over ordered time | Monthly Production trend |
| **Clustered Bar Chart** | Compare categories clearly | Production by Plant / Product |
| **Line and Clustered Column Chart** | Compare volumes plus a rate/trend | Actual vs Plan with Plan Attainment % |
| **Matrix** | Validate and analyze exact values | Product × Plant production and quality KPIs |
| **Conditional Formatting** | Draw attention to high/low values | Yield %, Rejection %, Production Variance |

> 💡 **Teaching Rule:**  
> **Business Question → Measure → Visual → Validation → Insight**

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:15 | 🔁 Production KPI recap and dashboard objective |
| 00:15–00:30 | 💻 Create report page and slicers |
| 00:30–00:55 | 💻 KPI Cards |
| 00:55–01:20 | 💻 Monthly Production trend |
| 01:20–01:45 | 💻 Plant and Product performance |
| 01:45–02:10 | 💻 Yield / Rejection analysis |
| 02:10–02:35 | 💻 Plan vs Actual Combo Chart |
| 02:35–02:50 | 💻 Detailed Matrix and conditional formatting |
| 02:50–03:00 | ✅ Dashboard validation and recap |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. Start with Business Questions

Before adding visuals, define what the dashboard should answer.

### Core Production Questions

1. How much was produced?
2. How much production was good vs rejected?
3. What is the current Yield % and Rejection %?
4. Which plants contribute the most production?
5. Which products contribute the most production?
6. How is production changing month by month?
7. Is Actual Production meeting the Production Plan?
8. Which Product–Plant combinations need attention?

### 💡 Teaching Point

Do not begin with:

> “Which chart should I use?”

Begin with:

> **“What business question am I trying to answer?”**

---

## 💻 2. Create the Production Performance Report Page

Create a new Power BI report page.

### Suggested Page Name

**Production Performance**

### 🛠️ Add Three Slicers

#### Fiscal Year

- **Visual Type:** Slicer
- **Field:** `DimDate[FiscalYear]`

#### Product

- **Visual Type:** Slicer
- **Field:** `DimProduct[ProductName]`

#### Plant

- **Visual Type:** Slicer
- **Field:** `DimPlant[PlantName]`

### 💡 Recommended Position

Place the slicers together across the top or left side of the report page.

### ✅ Validation

1. Select one Fiscal Year.
2. Select one Product.
3. Select one Plant.
4. Confirm that the production visuals created later respond to the same filter context.

> 💡 Keep the dashboard filters simple. More advanced filter/navigation design is reserved for Section 10.

---

## 💻 3. KPI Summary — Production at a Glance

### Business Question

> What is the current production-performance position?

### 🛠️ Visual Type

Use **Card visuals**.

Create separate Cards for:

- `[Production Quantity]`
- `[Good Quantity]`
- `[Rejected Quantity]`
- `[Yield %]`
- `[Rejection %]`
- `[Production Cost]`
- `[Batch Count]`

### 💡 Recommended Formatting

- Production / Good / Rejected Quantity → Whole number with thousand separator.
- Production Cost → Currency / INR formatting.
- Yield % / Rejection % → Percentage.
- Batch Count → Whole number.

### ✅ Validation

Use the **Fiscal Year, Product, and Plant slicers**.

Confirm that:

- ✅ Every Card changes when its relevant filter context changes.
- ✅ `[Yield %] = Good Quantity ÷ Production Quantity`.
- ✅ `[Rejection %] = Rejected Quantity ÷ Production Quantity`.
- ✅ Batch Count represents distinct batches, not production rows.
- ✅ With May 2024 selected at overall level, `[Production Quantity]` should show **613,548**.

> 💡 **Teaching Point:** Cards are excellent for headline KPIs, but they do not explain *why* a KPI is high or low. The next visuals provide the analysis.

> 🖼️ **Image Placeholder S07-01:** Production Performance KPI Cards with Fiscal Year, Product, and Plant slicers.  
> **Planned file:** `images/S07_01_Production_KPIs.png`

---

## 💻 4. Monthly Production Trend

### Business Question

> How is production changing over time?

### 🛠️ Visual Type

**Line Chart**

### 🛠️ Configure the Line Chart

**X-axis**
- `DimDate[FiscalYearMonth]`

**Y-axis**
- `[Production Quantity]`

### 🛠️ Sort Fiscal Months Correctly

`DimDate[FiscalYearMonth]` is a text label, so Power BI may not automatically display fiscal months in chronological order.

Use these **two separate sorting steps**:

#### Step 1 — Set the Model-Level Sort Order

1. Select `DimDate[FiscalYearMonth]` in the **Data** or **Model** view.
2. Go to **Column tools → Sort by column**.
3. Select `DimDate[FiscalPeriodSortKey]`.

This tells Power BI the correct chronological order behind the `FiscalYearMonth` text labels.

#### Step 2 — Set the Visual-Level Sort Order

1. Select the **Line Chart**.
2. Click the **... (More options)** menu on the visual.
3. Choose **Sort axis / Sort by**.
4. Select **FiscalYearMonth** — not `[Production Quantity]`.
5. Choose **Ascending**.

The X-axis should then appear in fiscal sequence, for example:

```text
FY2024-25 M01
FY2024-25 M02
FY2024-25 M03
...
FY2024-25 M12
```

> 💡 **Important:**  
> **Sort by column** defines the chronological order of `FiscalYearMonth`.  
> **Visual Sort** determines whether the chart follows that order or instead ranks the months by a measure such as Production Quantity.

### ⚠️ If Sorting Still Does Not Work

Create a temporary **Table** visual containing:

- `DimDate[FiscalYearMonth]`
- `DimDate[FiscalPeriodSortKey]`

Confirm that each `FiscalYearMonth` maps to exactly **one** `FiscalPeriodSortKey`.

If one Fiscal Year Month maps to multiple sort-key values, Power BI cannot reliably use that column for sorting.

### Optional Addition

Add:

- `[Production Previous Month]`

as a second line if learners are comfortable comparing the two measures.

### ✅ Validation

1. Select **FY2024-25**.
2. Confirm the X-axis follows the fiscal sequence **M01 → M02 → ... → M12**.
3. Confirm the chart is sorted by **FiscalYearMonth**, not by `[Production Quantity]`.
4. Hover over **May 2024**.
5. Confirm Production Quantity = **613,548**.
6. Select a Plant and verify the line recalculates.

### 💡 Interpretation Questions

Ask learners:

- Which month had the highest production?
- Is production increasing or decreasing?
- Are there sudden spikes or drops?
- Does the trend change after selecting a Plant?

> 🖼️ **Image Placeholder S07-02:** Monthly Production trend by Fiscal Month.  
> **Planned file:** `images/S07_02_Monthly_Production_Trend.png`

---

## 💻 5. Plant Performance Comparison

### Business Question

> Which plants contribute the most production?

### 🛠️ Visual Type

**Clustered Bar Chart**

A horizontal Bar Chart is useful because Plant names remain easy to read.

### 🛠️ Configure the Visual

**Y-axis / Category**
- `DimPlant[PlantName]`

**X-axis / Values**
- `[Production Quantity]`

### Sort

Sort by:

**Production Quantity → Descending**

### Optional Tooltips

Add:

- `[Yield %]`
- `[Rejection %]`
- `[Production Cost]`

### ✅ Validation

1. Clear the Plant slicer.
2. Confirm all Plants appear.
3. Select one Fiscal Year.
4. Compare the Plant bars.
5. Click one Plant bar and confirm other visuals cross-filter.

### 💡 Interpretation Questions

- Which Plant produces the most?
- Does the highest-volume Plant also have the highest Yield %?
- Does a lower-volume Plant show a higher Rejection %?

> 💡 High production volume does not automatically mean better overall performance. Volume and quality should be interpreted together.

---

## 💻 6. Product Performance Comparison

### Business Question

> Which products contribute the most production?

### 🛠️ Visual Type

**Clustered Bar Chart**

### 🛠️ Configure the Visual

**Y-axis / Category**
- `DimProduct[ProductName]`

**X-axis / Values**
- `[Production Quantity]`

### Sort

Sort:

**Production Quantity → Descending**

### Optional

If the chart becomes crowded, use the **Filters pane** to focus on a manageable number of products for classroom demonstration.

### ✅ Validation

1. Clear the Product slicer.
2. Select a Fiscal Year or Plant.
3. Confirm Product bars respond to the selection.
4. Click one Product and confirm the KPI Cards update.

### 💡 Interpretation Questions

- Which Product has the largest production volume?
- Does the ranking change from one Plant to another?
- Which Products deserve deeper Yield / Rejection analysis?

---

## 💻 7. Yield and Rejection Analysis

### Business Question

> Which Product–Plant combinations show stronger or weaker production quality?

### 🛠️ Visual Type

Use a **Matrix**.

### 🛠️ Configure the Matrix

**Rows**
- `DimProduct[ProductName]`

**Columns**
- `DimPlant[PlantName]`

**Values**
- `[Production Quantity]`
- `[Yield %]`
- `[Rejection %]`

### 🛠️ Conditional Formatting

Apply conditional formatting to:

- `[Yield %]`
- `[Rejection %]`

Use formatting only to make unusually high/low values easier to notice.

### ✅ Validation

Select one Product or Plant and confirm:

- ✅ Production Quantity recalculates.
- ✅ Yield % recalculates.
- ✅ Rejection % recalculates.
- ✅ Percentage values are measures, not fixed stored values.

### 💡 Interpretation Questions

- Which Product–Plant combinations have comparatively lower Yield %?
- Where is Rejection % comparatively higher?
- Is a high Rejection % associated with high production volume?

> ⚠️ Do not label a Plant or Product as “poor” based on one percentage alone. Use the visual to identify where deeper investigation may be needed.

---

## 💻 8. Production Plan vs Actual

### Business Question

> Is Actual Production meeting the monthly Production Plan?

### 🛠️ Visual Type for Presentation

**Line and Clustered Column Chart** *(Combo Chart)*

### 🛠️ Configure the Combo Chart

**X-axis**
- `DimDate[FiscalYearMonth]`

**Column Y-axis**
- `[Production Quantity]`
- `[Planned Production]`

**Line Y-axis**
- `[Plan Attainment %]`

### Slicers

Use:

- `DimProduct[ProductName]`
- `DimPlant[PlantName]`
- `DimDate[FiscalYear]`

### 💡 Why This Visual?

- Columns → compare **Actual vs Plan**.
- Line → show **Plan Attainment %** across time.

### ✅ Validation

Use a **Matrix** beside or temporarily instead of the Combo Chart.

**Rows**
- `DimDate[FiscalYearMonth]`

**Values**
- `[Production Quantity]`
- `[Planned Production]`
- `[Production Variance]`
- `[Plan Attainment %]`

Then select one row and manually verify:

```text
Production Variance
= Production Quantity - Planned Production
```

```text
Plan Attainment %
= Production Quantity ÷ Planned Production
```

### 💡 Interpretation

- Positive Variance → Actual is above Plan.
- Negative Variance → Actual is below Plan.
- `100%` Attainment → Actual meets Plan.
- Above `100%` → Plan exceeded.
- Below `100%` → Plan not fully achieved.

> ⚠️ Compare Plan and Actual at **monthly grain** because `FactProductionPlan` contains monthly planning data.

> 🖼️ **Image Placeholder S07-03:** Plan vs Actual Combo Chart with Production Quantity, Planned Production, and Plan Attainment %.  
> **Planned file:** `images/S07_03_Plan_vs_Actual.png`

---

## 💻 9. Detailed Production Analysis Matrix

### Business Question

> Can we inspect production performance at a more detailed Product and Plant level?

### 🛠️ Visual Type

**Matrix**

### 🛠️ Configure the Matrix

**Rows**
- `DimProduct[ProductName]`

**Columns**
- `DimPlant[PlantName]`

**Values**
- `[Production Quantity]`
- `[Good Quantity]`
- `[Rejected Quantity]`
- `[Yield %]`
- `[Rejection %]`
- `[Production Cost]`
- `[Batch Count]`

### Conditional Formatting

Good candidates:

- `[Yield %]`
- `[Rejection %]`
- `[Production Quantity]`

### ✅ Validation

Confirm:

- ✅ Product and Plant totals reconcile with the KPI Cards under the same filters.
- ✅ Selecting a Product/Plant changes all dependent measures.
- ✅ Grand totals use measure logic and should not be interpreted as a simple average of visible percentages.
- ✅ Yield % and Rejection % are calculated from the underlying quantities in the current context.

### 💡 Teaching Point

The Matrix is the best **validation and investigation** visual in this session because learners can inspect exact values while still using the same measures as the dashboard.

---

## 💻 10. Visual Interactions

Power BI visuals interact automatically unless the interaction is changed.

### Guided Demonstration

1. Click one Plant in the Plant Bar Chart.
2. Observe the Product Chart.
3. Observe KPI Cards.
4. Observe the Production Trend.
5. Clear the selection.

### ✅ Expected Behavior

The selected Plant should filter or highlight related visuals according to the model relationships and visual-interaction settings.

### 💡 Teaching Point

> **Slicer filtering** and **visual cross-filtering** are both forms of filter context reaching the same measures.

> 🚀 Keep advanced interaction editing, bookmarks, drill-through design, and field parameters for Section 10.

---

## 🧩 11. Recommended Dashboard Layout

A simple production dashboard can follow this structure:

```text
┌─────────────────────────────────────────────────────────────┐
│ Fiscal Year Slicer | Product Slicer | Plant Slicer          │
├─────────────────────────────────────────────────────────────┤
│ Production | Good Qty | Rejected | Yield % | Rejection %   │
│ Production Cost | Batch Count                               │
├─────────────────────────────┬───────────────────────────────┤
│ Monthly Production Trend    │ Plant Performance             │
├─────────────────────────────┼───────────────────────────────┤
│ Product Performance         │ Plan vs Actual Combo Chart    │
├─────────────────────────────────────────────────────────────┤
│ Product × Plant Detailed Matrix                             │
└─────────────────────────────────────────────────────────────┘
```

### 💡 Design Guidance

- Keep the most important KPIs near the top.
- Place trend/comparison visuals in the middle.
- Put detailed Matrix analysis lower on the page.
- Use consistent titles and number formatting.
- Avoid overcrowding the page with unnecessary visuals.

> 🖼️ **Image Placeholder S07-04:** Final Production Performance dashboard layout.  
> **Planned file:** `images/S07_04_Production_Dashboard.png`

---

## ✅ 12. Dashboard Validation Checklist

Before considering the dashboard complete, validate the following.

### Base Values

- ✅ `[Production Quantity]` produces a sensible total.
- ✅ May 2024 overall Production Quantity = **613,548**.
- ✅ Yield % and Rejection % reconcile with their base quantities.

### Filter Response

- ✅ Fiscal Year slicer filters all relevant visuals.
- ✅ Product slicer filters relevant visuals.
- ✅ Plant slicer filters relevant visuals.
- ✅ Clicking a Plant or Product visual changes related visuals as expected.

### Visual Meaning

- ✅ Line Chart is used for ordered time trend.
- ✅ Bar Charts are used for Plant/Product comparison.
- ✅ Matrix is used for exact-value investigation and validation.
- ✅ Combo Chart compares Actual vs Plan and shows Attainment %.
- ✅ Plan vs Actual uses monthly grain.

### Reconciliation

Choose one filter combination and confirm:

```text
KPI Card Production Quantity
=
Line Chart value for the same context
=
Plant/Product visual total for the same context
=
Matrix total for the same context
```

> 💡 **Validation Rule:** A dashboard is not validated merely because every visual displays a number. Different visuals using the same filter context should reconcile logically.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Create the **Production Performance** report page.
2. 💻 Add Fiscal Year, Product, and Plant slicers.
3. 💻 Create the production KPI Cards.
4. 💻 Create the Monthly Production Line Chart.
5. 💻 Create the Plant Performance Bar Chart.
6. 💻 Create the Product Performance Bar Chart.
7. 💻 Create the Product × Plant Yield/Rejection Matrix.
8. 💻 Create the Plan vs Actual Combo Chart.
9. 💻 Apply simple conditional formatting in the Matrix.
10. 💻 Test visual cross-filtering.
11. 💻 Validate one May 2024 production value.
12. 💻 Reconcile one Matrix/Chart value with the corresponding KPI Card.

### ✅ Expected Outcome

Learners complete **Dashboard Page 1 — Production Performance** and can explain what each visual answers, how its measures respond to filters, and how to validate the displayed values.

---

## 💡 Trainer Guidelines

- 💡 Start with the **business question**, not the chart gallery.
- 💡 Reuse the measures from Sections 05 and 06 instead of creating unnecessary new DAX.
- 💡 Use **Cards for headline KPIs**.
- 💡 Use **Line Charts for time trends**.
- 💡 For fiscal time axes, explain both **Sort by column** and the visual's **Sort by FiscalYearMonth → Ascending** setting.
- 💡 Use **Bar Charts for Plant/Product comparison**.
- 💡 Use **Matrices for exact validation and detailed investigation**.
- 💡 Use the **Combo Chart for Actual vs Plan storytelling**.
- 💡 Keep **May 2024 / FY2024-25** as the main demonstration context for continuity with Section 06.
- 💡 Manually reconcile at least one value across Card, Chart, and Matrix.
- ⚠️ Do not compare daily Actual Production directly with monthly Plan data.
- ⚠️ Do not introduce advanced bookmarks, field parameters, or complex navigation here.
- ⚠️ Avoid drawing strong operational conclusions from one visual without checking the underlying filter context.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 How business questions map to Power BI visuals.
- 🔁 How to create a Production KPI summary.
- 🔁 How to analyze production trends over time.
- 🔁 How to compare Plant and Product performance.
- 🔁 How to analyze Yield % and Rejection %.
- 🔁 How to present Actual vs Plan using a Combo Chart.
- 🔁 Why Matrix visuals are useful for validation.
- 🔁 How slicers and visual interactions change filter context.
- 🔁 How to validate a production dashboard before interpreting it.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. Which visual is most suitable for showing a single headline KPI such as Production Quantity?

A. Card <br>
B. Pie Chart <br>
C. Scatter Chart <br>
D. Map <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Card**

**Explanation:** A Card highlights one important KPI clearly and is ideal for summary measures such as Production Quantity or Yield %.

</details>

### 🔴 Q2. Which visual is most suitable for showing monthly Production Quantity over time?

A. Line Chart <br>
B. Pie Chart <br>
C. Gauge only <br>
D. Text box <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Line Chart**

**Explanation:** A Line Chart is well suited to ordered time-series data and makes production trends easy to identify.

</details>

### 🔴 Q3. Which visual is recommended for comparing Production Quantity across Plants?

A. Clustered Bar Chart <br>
B. Card <br>
C. Slicer <br>
D. Text box <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Clustered Bar Chart**

**Explanation:** A Bar Chart makes category-to-category comparisons clear and keeps Plant labels readable.

</details>

### 🔴 Q4. What is the main purpose of a Slicer in the Production dashboard?

A. Change the filter context interactively <br>
B. Create new source rows <br>
C. Create relationships automatically <br>
D. Replace DAX measures <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Change the filter context interactively**

**Explanation:** Slicers allow learners/users to filter the report by dimensions such as Fiscal Year, Product, or Plant.

</details>

### 🔴 Q5. Which visual is recommended for exact Product × Plant validation?

A. Matrix <br>
B. Card <br>
C. Donut Chart <br>
D. Map <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Matrix**

**Explanation:** A Matrix displays exact values across multiple dimensions and is useful for detailed validation.

</details>

### 🔴 Q6. What does a positive Production Variance indicate?

A. Actual Production is above Planned Production <br>
B. Actual Production is always zero <br>
C. The Date table is missing <br>
D. The relationship is inactive <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Actual Production is above Planned Production**

**Explanation:** Production Variance is Actual minus Plan, so a positive result means Actual exceeded Plan.

</details>

### 🔴 Q7. Which Combo Chart setup is recommended for Plan vs Actual?

A. Actual and Plan as columns, Attainment % as a line <br>
B. Actual as a map and Plan as a table <br>
C. Attainment % only as a column <br>
D. Product name as the line value <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Actual and Plan as columns, Attainment % as a line**

**Explanation:** The columns compare production volumes while the line shows the percentage attainment trend.

</details>

### 🔴 Q8. Why should Plan vs Actual be compared at monthly grain in this case study?

A. The Production Plan is stored at monthly grain <br>
B. Power BI cannot display dates <br>
C. Production Quantity is always monthly <br>
D. Slicers only work with months <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. The Production Plan is stored at monthly grain**

**Explanation:** Comparing Actual and Plan at compatible grains avoids misleading results.

</details>

### 🔴 Q9. Why is conditional formatting useful in the Yield/Rejection Matrix?

A. It helps draw attention to comparatively high or low values <br>
B. It changes the source data permanently <br>
C. It creates new relationships <br>
D. It replaces the measures <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. It helps draw attention to comparatively high or low values**

**Explanation:** Conditional formatting makes patterns easier to spot while leaving the underlying values unchanged.

</details>

### 🔴 Q10. What should happen to KPI Cards when a Plant is selected?

A. Relevant measures should recalculate for that Plant <br>
B. All values should remain fixed <br>
C. The semantic model should be deleted <br>
D. The Date table should disappear <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Relevant measures should recalculate for that Plant**

**Explanation:** Measures respond to filter context transmitted through slicers and model relationships.

</details>

### 🔴 Q11. Why should the same measure reconcile across a Card, Chart, and Matrix under the same filters?

A. They are evaluating the same measure under the same filter context <br>
B. Every Power BI visual stores a separate copy of the data <br>
C. Visuals ignore model relationships <br>
D. Cards automatically correct other visuals <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. They are evaluating the same measure under the same filter context**

**Explanation:** If the measure and filter context are the same, the corresponding value should reconcile logically across visuals.

</details>

### 🔴 Q12. What is the main deliverable of this session?

A. Production Performance dashboard page <br>
B. A new database server <br>
C. An RLS configuration <br>
D. A Power BI Service deployment <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Production Performance dashboard page**

**Explanation:** The session consolidates the model and DAX work into a focused Production Performance dashboard.

</details>

---

### ➡️ Next Session

**Section 08 — Pharma Analytics II: Inventory and Expiry Analysis**

Learners will use the Nirvaan Pharma Ltd model to analyze **inventory levels, warehouse distribution, stock movement, expiry exposure, and inventory-risk patterns**.
