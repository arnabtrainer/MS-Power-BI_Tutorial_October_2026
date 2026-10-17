# Section 10 — Advanced Reporting, Interactivity and Report UX

**Day:** 5 — Post-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Rank Products using `RANKX()`.
- 🎯 Build a simple dynamic KPI using `SELECTEDVALUE()` and `SWITCH()`.
- 🎯 Use **Field Parameters** for user-controlled visual analysis.
- 🎯 Create **Drill-through** navigation to a detailed Product page.
- 🎯 Create a **Report Page Tooltip** for richer hover information.
- 🎯 Use **Bookmarks** and a Bookmark Navigator to switch report views.
- 🎯 Use a **Page Navigator** for multi-page report navigation.
- 🎯 Understand **Edit interactions** and **Sync slicers**.
- 🎯 Apply practical report-UX principles for clarity, consistency, and usability.
- 🎯 Validate advanced interactivity without changing the underlying business logic.

---

## 🗂️ Resources Used

### Primary Case-Study Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

### Existing Report Pages Reused

- **Production Performance** — Section 07
- **Inventory & Expiry Analysis** — Section 08
- **Quality, Deviations & Downtime** — Section 09

### Main Tables / Fields Used

- `DimDate`
- `DimProduct`
- `DimPlant`
- `FactProduction`

### Measures Reused

- `[Production Quantity]`
- `[Good Quantity]`
- `[Rejected Quantity]`
- `[Yield %]`
- `[Rejection %]`
- `[Production Cost]`
- `[Batch Count]`

> 💡 **Prerequisite:** The main analytical pages from Sections 07–09 should already exist.

> 💡 **Scope:** This session improves **interactivity and report experience**. Publishing, workspaces, refresh, RLS, and enterprise sharing are covered in **Section 11**.

---

## 📚 Advanced Reporting Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Product Ranking | `RANKX()` | 💻 Guided |
| 2 | Dynamic KPI | `SELECTEDVALUE()` + `SWITCH()` | 💻 Guided |
| 3 | Field Parameters | Dynamic Product / Plant analysis | 💻 Guided |
| 4 | Drill-through | Product Detail page | 💻 Guided |
| 5 | Report Page Tooltip | Rich Plant hover details | 💻 Guided |
| 6 | Bookmarks | Chart View vs Matrix View | 💻 Guided |
| 7 | Page Navigation | Multi-page navigation | 💻 Guided |
| 8 | Edit Interactions | Control visual-to-visual behavior | 🧑‍🏫 Demo |
| 9 | Sync Slicers | Reuse Product filter across pages | 🧑‍🏫 Demo |
| 10 | Report UX | Layout, consistency, accessibility | 🧑‍🏫 Demo |
| 11 | Validation | Verify dynamic behavior | 💻 Guided |

---

## 🧭 DAX Function — Purpose and Target Map

This is the main session where the previously deferred advanced DAX functions are introduced.

| DAX Function | Purpose | Target in This Session |
|---|---|---|
| `RANKX()` | Rank items using a measure/expression | Rank Products by Production Quantity |
| `SELECTEDVALUE()` | Return one selected value from the current context | Read the KPI selected in a slicer |
| `SWITCH()` | Return different results based on a selected value | Return Production, Good, or Rejected Quantity dynamically |
| `ALL()` | Remove a selected filter during a calculation | Allow Product ranking across all Products |

> 💡 **Field Parameters are a Power BI feature, not a DAX function.**

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:15 | 🔁 Report UX goals and existing-dashboard review |
| 00:15–00:40 | 💻 Product ranking with `RANKX()` |
| 00:40–01:05 | 💻 Dynamic KPI with `SELECTEDVALUE()` + `SWITCH()` |
| 01:05–01:30 | 💻 Field Parameters |
| 01:30–01:55 | 💻 Drill-through Product Detail page |
| 01:55–02:15 | 💻 Report Page Tooltip |
| 02:15–02:35 | 💻 Bookmarks and Bookmark Navigator |
| 02:35–02:50 | 💻 Page Navigator, Sync Slicers, Edit interactions |
| 02:50–03:00 | ✅ Validation and recap |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. Report UX — Start with the User Journey

Before adding advanced features, ask:

> **What should the report user be able to discover or do more easily?**

Examples:

- Identify the highest-producing Products.
- Change which KPI is displayed.
- Switch a chart between Product and Plant analysis.
- Right-click a Product and open detailed information.
- Hover over a Plant and see supporting KPIs.
- Switch between Chart and Matrix views.
- Move easily between Production, Inventory, and Quality pages.

### 💡 Teaching Rule

> **Add interactivity only when it makes the analysis easier.**

More buttons, bookmarks, or slicers do not automatically create a better report.

---

# PRODUCT RANKING

## 💻 2. Rank Products with `RANKX()`

### Business Question

> Which Products rank highest by Production Quantity?

Create:

```DAX
Product Production Rank =
RANKX(
    ALL(DimProduct[ProductName]),
    [Production Quantity],
    ,
    DESC,
    DENSE
)
```

### 🎯 Purpose and Target

- 🎯 **`RANKX()` Purpose:** Evaluate a measure across a set of items and return the rank of the current item.
- 🎯 **`ALL()` Purpose:** Remove the current Product Name filter so all Products can be compared.
- 🧭 **Target:** Rank Products from highest to lowest Production Quantity.
- 💡 **`DESC`** → the Product with the highest Production Quantity receives **Rank 1**.
- 💡 **`DENSE`** → if two or more Products have the same Production Quantity, they receive the same rank and the next rank continues without a gap.

Example:

| Product | Production Quantity | Dense Rank |
|---|---:|---:|
| Product A | 100,000 | 1 |
| Product B | 90,000 | 2 |
| Product C | 90,000 | 2 |
| Product D | 80,000 | 3 |

Without dense ranking, the sequence could be `1, 2, 2, 4`.  
With **`DENSE`**, it becomes `1, 2, 2, 3`.

> 💡 **Simple Rule:** `DENSE` means **“same value → same rank, but do not skip the next rank.”**

---

## ✅ Validate Product Ranking

### 🛠️ Visual Type

**Table**

### Add

- `DimProduct[ProductName]`
- `[Production Quantity]`
- `[Product Production Rank]`

### Slicer

- `DimDate[FiscalYear]`

Select:

**FY2024-25**

### Sort

Sort the Table by:

**Product Production Rank → Ascending**

### ✅ Expected Top 5

| Rank | Product | Production Quantity |
|---:|---|---:|
| 1 | Salinex 1000 mL | 271,356 |
| 2 | Metrozol 100 mL | 221,597 |
| 3 | Salinex 500 mL | 217,131 |
| 4 | Cispral 50 mg/50 mL | 215,428 |
| 5 | Ringlac 500 mL | 206,614 |

### Filter-Response Check

Add a Plant slicer and select one Plant.

- ✅ Production Quantity should change.
- ✅ Product ranks should recalculate under the selected Plant context.
- ✅ Rank 1 should still represent the highest-production Product within that context.

> 🖼️ **Image Placeholder S10-01:** Product ranking Table showing Production Quantity and Product Production Rank.  
> **Planned file:** `images/S10_01_Product_Ranking.png`

---

# DYNAMIC KPI

## 💻 3. Create a Simple KPI Selector

The purpose is to let the report user choose which quantity KPI a Card should display.

### Step 1 — Create a Disconnected Table

Go to:

**Home → Enter Data**

Create:

### `Metric Selector`

| Metric |
|---|
| Production Quantity |
| Good Quantity |
| Rejected Quantity |

> ⚠️ Do **not** create a relationship from `Metric Selector` to the semantic model.

### 💡 Why Disconnected?

The table exists only to capture a user's selection.  
The DAX measure reads that selection and decides which existing measure to return.

---

## 💻 4. Use `SELECTEDVALUE()` and `SWITCH()`

### Selected Metric

```DAX
Selected Metric =
SELECTEDVALUE(
    'Metric Selector'[Metric],
    "Production Quantity"
)
```

- 🎯 **`SELECTEDVALUE()` Purpose:** Return the single Metric currently selected.
- 🧭 **Target:** Identify which KPI the user wants to display.
- 💡 If no single value is selected, `"Production Quantity"` becomes the default.

### Dynamic KPI

```DAX
Dynamic KPI =
SWITCH(
    [Selected Metric],
    "Production Quantity", [Production Quantity],
    "Good Quantity", [Good Quantity],
    "Rejected Quantity", [Rejected Quantity],
    [Production Quantity]
)
```

- 🎯 **`SWITCH()` Purpose:** Return a different result based on the selected Metric.
- 🧭 **Target:** Reuse one Card to display one of three quantity KPIs.

---

## ✅ Validate the Dynamic KPI

### 🛠️ Visual Types

- **Slicer** → `'Metric Selector'[Metric]`
- **Card** → `[Dynamic KPI]`
- **Date Slicer** → `DimDate[Date]`

Set the Date slicer to:

**01-May-2024 → 31-May-2024**

Select each Metric one at a time.

Expected:

| Selected Metric | Dynamic KPI |
|---|---:|
| Production Quantity | 613,548 |
| Good Quantity | 590,766 |
| Rejected Quantity | 22,782 |

### ✅ Check

```text
590,766 + 22,782
= 613,548
```

> 💡 **Teaching Point:** The slicer does not directly filter `FactProduction`. It controls which measure `SWITCH()` returns.

> ⚠️ Keep this first example to measures with similar numeric formatting. Mixing quantities, percentages, and currency in one simple dynamic measure can create formatting confusion.

---

# FIELD PARAMETERS

## 💻 5. Dynamic Analysis with a Field Parameter

Field Parameters provide a native Power BI approach for letting report users change fields used by a visual.

### Business Question

> Can the same Bar Chart switch between Product analysis and Plant analysis?

### Step 1 — Create the Field Parameter

Go to:

**Modeling → New parameter → Fields**

Create a parameter named:

**Analyze By**

Add:

- `DimProduct[ProductName]`
- `DimPlant[PlantName]`

Enable the option to add a slicer to the page if available.

### Step 2 — Configure a Bar Chart

**Visual Type:** Clustered Bar Chart

**Y-axis / Category**
- `Analyze By`

**X-axis / Values**
- `[Production Quantity]`

### Step 3 — Use the Parameter Slicer

Select:

- Product → chart groups by Product.
- Plant → chart groups by Plant.

### ✅ Validation

1. Select **FY2024-25**.
2. Choose **Product** in the parameter slicer.
3. Confirm Product names appear.
4. Choose **Plant**.
5. Confirm Plant names replace Product names.
6. Confirm `[Production Quantity]` remains the measure in both cases.

> 💡 **Teaching Point:** Field Parameters change the field used by the visual without requiring separate Product and Plant charts.

> 💡 **Difference from the Dynamic KPI example:**  
> `SELECTEDVALUE()` + `SWITCH()` changes **which measure is returned**.  
> The Field Parameter here changes **which dimension is displayed**.

> 🖼️ **Image Placeholder S10-02:** Field Parameter slicer switching one Production Bar Chart between Product and Plant.  
> **Planned file:** `images/S10_02_Field_Parameter.png`

---

# DRILL-THROUGH

## 💻 6. Create a Product Detail Drill-through Page

### Business Question

> Can a user right-click a Product and open a detailed page filtered to that Product?

### Step 1 — Add a New Page

Create a page named:

**Product Detail**

### Step 2 — Add the Drill-through Field

With the Product Detail page selected, locate the **Drill-through** area in the Filters / Build pane.

Add:

- `DimProduct[ProductName]`

Keep **Keep all filters** enabled if you want relevant source-page filters to follow the user.

### Step 3 — Add Detail Visuals

Suggested:

#### Cards

- `[Production Quantity]`
- `[Yield %]`
- `[Rejection %]`
- `[Production Cost]`

#### Line Chart

**X-axis**
- `DimDate[FiscalYearMonth]`

**Y-axis**
- `[Production Quantity]`

#### Matrix

**Rows**
- `DimPlant[PlantName]`

**Values**
- `[Production Quantity]`
- `[Yield %]`
- `[Rejection %]`

### Step 4 — Test Drill-through

Return to **Production Performance**.

Right-click one Product in the Product Performance Bar Chart:

**Right-click Product → Drill through → Product Detail**

### ✅ Validation

- ✅ Product Detail page should be filtered to the selected Product.
- ✅ Cards, Line Chart, and Matrix should all reflect that Product.
- ✅ Use the automatically available Back button or add one if necessary.
- ✅ Return to the source page and test another Product.

> 💡 Drill-through provides detail **on demand** without overcrowding the main dashboard.

> 🖼️ **Image Placeholder S10-03:** Product Detail Drill-through page with KPI Cards, trend, and Plant Matrix.  
> **Planned file:** `images/S10_03_Drillthrough_Product_Detail.png`

---

# REPORT PAGE TOOLTIP

## 💻 7. Create a Plant Report Page Tooltip

Section 7 used standard tooltip fields. Now create a richer **Report Page Tooltip**.

### Business Question

> Can the user hover over a Plant and see additional production KPIs without leaving the dashboard?

### Step 1 — Add a New Page

Create:

**Plant Tooltip**

### Step 2 — Configure It as a Tooltip Page

With the page selected:

- Open the page/canvas formatting settings.
- Set the page type / canvas size to **Tooltip** where available.
- Turn **Allow use as tooltip** / Tooltip setting **On**.

*(Exact labels can vary slightly by Power BI Desktop version.)*

### Step 3 — Add Small Visuals

Use compact Cards for:

- `[Production Quantity]`
- `[Yield %]`
- `[Rejection %]`
- `[Production Cost]`

Optionally add:

- `DimPlant[PlantName]`

as a small heading or Card-style value.

### Step 4 — Assign the Tooltip

Return to the **Plant Performance Bar Chart**.

In the visual's Tooltip settings:

- Tooltip Type → **Report page**
- Page → **Plant Tooltip**

### ✅ Validation

Hover over a Plant bar.

Confirm:

- ✅ Tooltip opens.
- ✅ Tooltip displays the hovered Plant's values.
- ✅ Values change when hovering over another Plant.
- ✅ Values also respect Fiscal Year / Product filters on the source page.

> 💡 The tooltip page receives the hovered data point's filter context automatically.

---

# BOOKMARKS

## 💻 8. Use Bookmarks to Switch Between Chart and Matrix Views

### Business Question

> Can users switch between a visual summary and a detailed table without creating another report page?

### Step 1 — Create Two Visuals

On a practice page, create:

- **Chart View** → Product Production Bar Chart
- **Matrix View** → Product × Plant Matrix

Place them in approximately the same report area.

### Step 2 — Open the Required Panes

Go to:

**View → Selection**

and:

**View → Bookmarks**

### Step 3 — Create `Chart View` Bookmark

In the **Selection pane**:

- Show the Bar Chart.
- Hide the Matrix.

In the **Bookmarks pane**:

- Add a bookmark.
- Rename it **Chart View**.

### Step 4 — Create `Matrix View` Bookmark

In the Selection pane:

- Hide the Bar Chart.
- Show the Matrix.

Add another bookmark:

**Matrix View**

### Step 5 — Preserve Slicer Selections

For these display-only bookmarks, open each bookmark's options.

If the bookmark should **not reset slicers**, turn off / uncheck the **Data** option and retain the display/page-state behavior.

### Step 6 — Add a Bookmark Navigator

Use:

**Insert → Buttons / Navigator → Bookmark navigator**

Place the navigator above the visual area.

### ✅ Validation

1. Select **FY2024-25** and one Plant/Product filter.
2. Click **Chart View**.
3. Click **Matrix View**.
4. Confirm the correct visual appears.
5. Confirm the slicer selection remains unchanged.

> 💡 **Teaching Point:** Bookmarks can store display state. Be intentional about whether they should also store filter/data state.

---

# PAGE NAVIGATION

## 💻 9. Add a Page Navigator

Use a Page Navigator so users can move between the main analytical pages.

### Suggested Visible Pages

- Production Performance
- Inventory & Expiry Analysis
- Quality, Deviations & Downtime

### Steps

Use:

**Insert → Buttons / Navigator → Page navigator**

Place the navigator consistently near the top or side of each main report page.

### Hide Utility Pages

Pages such as:

- `Plant Tooltip`

should normally be hidden from normal page navigation.

`Product Detail` may also be hidden if you want users to reach it only through Drill-through.

### ✅ Validation

Click each page-navigation item and confirm that it opens the intended page.

---

# SYNC SLICERS

## 🧑‍🏫 10. Sync a Product Slicer Across Pages

### Business Question

> Can the user's Product selection remain consistent across multiple analytical pages?

Use:

- `DimProduct[ProductName]`

because Product is relevant to Production, Inventory, and Quality analysis.

### Steps

1. Select the Product slicer.
2. Open **View → Sync slicers**.
3. Enable **Sync** for:
   - Production Performance
   - Inventory & Expiry Analysis
   - Quality, Deviations & Downtime
4. Choose whether the slicer should also be **Visible** on each page.

### ✅ Validation

1. Select one Product on Production Performance.
2. Navigate to Inventory.
3. Confirm the Product selection is retained.
4. Navigate to Quality.
5. Confirm the same Product filter is applied.

> ⚠️ A synced slicer can filter a page even when the slicer itself is hidden. Use hidden synced slicers carefully.

---

# EDIT INTERACTIONS

## 🧑‍🏫 11. Control Visual Interactions

Power BI normally allows visuals to cross-filter or cross-highlight one another.

### Guided Demonstration

On the Production Performance page:

1. Select the **Plant Performance Bar Chart**.
2. Use **Format → Edit interactions**.
3. Observe the interaction icons shown on the other visuals.
4. Demonstrate:
   - **Filter**
   - **Highlight** *(where supported)*
   - **None**
5. Restore the desired/default behavior after the demonstration.

### 💡 Teaching Point

Use **None** only when there is a clear business reason for one visual not to respond.

> ⚠️ Disabling interactions without explanation can make a dashboard look inconsistent or incorrect.

---

# REPORT UX

## 📚 12. Practical Report UX Guidelines

### Visual Hierarchy

- Keep the most important KPI Cards at the top.
- Place trends and comparisons in the middle.
- Keep detailed Matrices lower on the page or on drill-through pages.

### Consistency

Use consistent:

- titles
- number formats
- slicer placement
- terminology
- spacing and alignment

### Reduce Clutter

Avoid:

- too many visuals on one page
- unnecessary borders
- excessive labels
- repeated information
- too many slicers

### Interactivity

Use:

- Tooltips → additional context
- Drill-through → deeper detail
- Bookmarks → alternate views
- Field Parameters → dynamic analysis
- Page Navigator → predictable navigation

### Accessibility

Where appropriate:

- use meaningful visual titles
- keep text readable
- do not rely only on color to communicate meaning
- add useful alt text to important visuals
- maintain logical reading/tab order where required

### 💡 UX Rule

> **A user should know where to look, what to click, and what changed.**

---

## ✅ 13. Advanced Reporting Validation Checklist

Before considering the enhanced report complete, verify the following.

### Ranking

- ✅ Product ranks change when relevant Date or Plant context changes.
- ✅ Under FY2024-25, Salinex 1000 mL is Rank 1 with Production Quantity **271,356**.

### Dynamic KPI

For May 2024:

- ✅ Production Quantity → **613,548**
- ✅ Good Quantity → **590,766**
- ✅ Rejected Quantity → **22,782**
- ✅ Slicer selection changes the Dynamic KPI Card correctly.

### Field Parameter

- ✅ Product selection shows Product categories.
- ✅ Plant selection shows Plant categories.
- ✅ Production Quantity remains the measure.

### Drill-through

- ✅ Selected Product reaches Product Detail.
- ✅ Detail-page visuals inherit the Product context.
- ✅ Back navigation works.

### Tooltip

- ✅ Hovered Plant controls the tooltip values.
- ✅ Source-page slicers continue to affect tooltip values.

### Bookmarks

- ✅ Chart View and Matrix View switch correctly.
- ✅ Slicer state remains unchanged when `Data` is excluded from the bookmark.

### Navigation

- ✅ Page Navigator opens the intended page.
- ✅ Tooltip/helper pages are hidden from normal navigation when appropriate.

### Sync Slicers

- ✅ Product selection remains consistent across intended pages.

### Interactions

- ✅ Visuals cross-filter/highlight according to the intended design.
- ✅ Any disabled interaction has a clear business reason.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Create `[Product Production Rank]`.
2. 💻 Validate the FY2024-25 Top 5 Product ranking.
3. 💻 Create the disconnected `Metric Selector` table.
4. 💻 Create `[Selected Metric]`.
5. 💻 Create `[Dynamic KPI]`.
6. 💻 Validate the May 2024 Dynamic KPI values.
7. 💻 Create the **Analyze By** Field Parameter.
8. 💻 Switch one Bar Chart between Product and Plant.
9. 💻 Create the **Product Detail** Drill-through page.
10. 💻 Create the **Plant Tooltip** report page.
11. 💻 Create Chart View and Matrix View bookmarks.
12. 💻 Add a Bookmark Navigator.
13. 💻 Add a Page Navigator.
14. 💻 Sync the Product slicer across the analytical pages.
15. 💻 Demonstrate Edit interactions.
16. 💻 Complete the Advanced Reporting validation checklist.

### ✅ Expected Outcome

Learners transform the three analytical dashboards into a more polished, interactive **multi-page Power BI report experience** without changing the underlying business measures.

---

## 💡 Trainer Guidelines

- 💡 Introduce `RANKX()`, `SELECTEDVALUE()`, and `SWITCH()` using short, purposeful examples.
- 💡 Explain **Purpose → Target → Result → Validation** for each new DAX function.
- 💡 Keep the disconnected selector table small and relationship-free.
- 💡 Explain that Field Parameters are a native feature, not a DAX function learners need to write manually.
- 💡 Use Drill-through for detail-on-demand rather than adding every detail to the main dashboard.
- 💡 Use Report Page Tooltips for supporting context, not for critical information users can see only by hovering.
- 💡 When using Bookmarks for show/hide behavior, explain the **Data** option carefully.
- 💡 Hide helper/tooltip pages from normal navigation where appropriate.
- 💡 Sync slicers only where the same filter has consistent business meaning.
- 💡 Validate each interaction after adding it.
- ⚠️ Do not add interactivity merely because the feature exists.
- ⚠️ Avoid bookmarks that unexpectedly reset user filters.
- ⚠️ Avoid hidden slicers that filter pages without learners understanding why.
- ⚠️ Do not overload the session with custom visuals; native Power BI visuals are sufficient.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 Product ranking using `RANKX()`.
- 🔁 Dynamic measure selection using `SELECTEDVALUE()` and `SWITCH()`.
- 🔁 Field Parameters for dynamic dimensions.
- 🔁 Drill-through pages for detailed analysis.
- 🔁 Report Page Tooltips for richer hover context.
- 🔁 Bookmarks and Bookmark Navigators for alternate views.
- 🔁 Page Navigators for multi-page report UX.
- 🔁 Sync Slicers and Edit interactions.
- 🔁 Practical report-design and accessibility principles.
- 🔁 How to validate advanced interactivity without changing business logic.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What is the main purpose of `RANKX()`?

A. Rank items using a measure or expression <br>
B. Create a relationship automatically <br>
C. Import an Excel file <br>
D. Refresh a semantic model <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Rank items using a measure or expression**

**Explanation:** `RANKX()` evaluates an expression over a set of items and returns the rank of the current item.

</details>

### 🔴 Q2. In the Product ranking example, what does `DESC` mean?

A. Highest Production Quantity receives the best rank <br>
B. Products are deleted in descending order <br>
C. Only text values are ranked <br>
D. The Date table is disabled <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Highest Production Quantity receives the best rank**

**Explanation:** Descending ranking places the largest Production Quantity at Rank 1.

</details>

### 🔴 Q3. What does `SELECTEDVALUE()` do in the Dynamic KPI example?

A. Reads the single Metric selected in the slicer <br>
B. Creates a new Power Query step <br>
C. Publishes the report <br>
D. Deletes duplicate rows <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Reads the single Metric selected in the slicer**

**Explanation:** `SELECTEDVALUE()` retrieves the one value currently selected and can return a default when there is no single selection.

</details>

### 🔴 Q4. What is the purpose of `SWITCH()` in the Dynamic KPI measure?

A. Return a different existing measure according to the selected Metric <br>
B. Change a relationship to bidirectional <br>
C. Create a Date table <br>
D. Change the Power BI theme <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Return a different existing measure according to the selected Metric**

**Explanation:** `SWITCH()` maps each selected Metric to the appropriate business measure.

</details>

### 🔴 Q5. Why is the `Metric Selector` table disconnected?

A. It is used to capture a selection rather than filter the fact table through a relationship <br>
B. Power BI does not allow relationships <br>
C. It contains no rows <br>
D. It is a Power Query error table <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. It is used to capture a selection rather than filter the fact table through a relationship**

**Explanation:** DAX reads the slicer selection and decides which measure to return.

</details>

### 🔴 Q6. What does the `Analyze By` Field Parameter control in this session?

A. Whether the Bar Chart groups Production by Product or by Plant <br>
B. The database connection string <br>
C. Row-level security <br>
D. Dataset refresh frequency <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Whether the Bar Chart groups Production by Product or by Plant**

**Explanation:** The Field Parameter dynamically changes the dimension used on the visual's category axis.

</details>

### 🔴 Q7. What is Drill-through best suited for?

A. Opening a detailed page filtered to the selected item <br>
B. Replacing the semantic model <br>
C. Refreshing data automatically <br>
D. Creating an Excel workbook <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Opening a detailed page filtered to the selected item**

**Explanation:** Drill-through allows users to move from a summary visual to a detail page while carrying the selected context.

</details>

### 🔴 Q8. What is a Report Page Tooltip?

A. A specially configured report page displayed when hovering over a data point <br>
B. A database error message <br>
C. A type of Power Query join <br>
D. An RLS role <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. A specially configured report page displayed when hovering over a data point**

**Explanation:** Report Page Tooltips can contain multiple compact visuals and automatically receive the hovered data context.

</details>

### 🔴 Q9. Why might the `Data` option be disabled for a Chart/Matrix bookmark?

A. To switch visual display without resetting the user's slicer/filter selections <br>
B. To remove all data from the model <br>
C. To disable DAX permanently <br>
D. To prevent page navigation <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. To switch visual display without resetting the user's slicer/filter selections**

**Explanation:** A display-only bookmark should usually preserve the user's current filter state.

</details>

### 🔴 Q10. What does Sync Slicers allow?

A. One slicer selection to be applied across selected report pages <br>
B. One DAX measure to create several tables <br>
C. Power Query to merge databases automatically <br>
D. A bookmark to publish the report <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. One slicer selection to be applied across selected report pages**

**Explanation:** Synced slicers help maintain a consistent filter selection across relevant pages.

</details>

### 🔴 Q11. What does Edit interactions control?

A. How one visual filters, highlights, or does not affect other visuals <br>
B. The underlying Excel formulas <br>
C. User account permissions <br>
D. Data-source credentials <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. How one visual filters, highlights, or does not affect other visuals**

**Explanation:** Edit interactions lets report authors control visual-to-visual behavior on a report page.

</details>

### 🔴 Q12. What is the main objective of Section 10?

A. Improve report interactivity, navigation, and usability without changing the underlying business logic <br>
B. Replace all existing DAX measures <br>
C. Build a new data warehouse <br>
D. Publish directly without validation <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Improve report interactivity, navigation, and usability without changing the underlying business logic**

**Explanation:** Section 10 turns the existing analytical pages into a more polished and interactive report experience.

</details>

---

### ➡️ Next Session

**Section 11 — Power BI Service, Refresh, RLS and Enterprise Sharing**

Learners will move from Power BI Desktop to the Power BI Service and cover **publishing, workspaces, semantic-model refresh, gateways, Row-Level Security, and controlled enterprise sharing**.
