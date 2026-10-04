# Section 04 — Data Modeling and Star Schema Design

**Day:** 2 — Post-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Distinguish **fact tables** from **dimension tables**.
- 🎯 Define the **grain** of a table before creating relationships.
- 🎯 Build a basic **star schema** in Power BI.
- 🎯 Configure relationship **cardinality** and **filter direction** correctly.
- 🎯 Understand **active/inactive** and role-playing relationships.
- 🎯 Create and use a proper **Date table**.
- 🎯 Organize a semantic model for usability and scalability.

---

## 🗂️ Resources Used

### Primary Classwork

- 🗂️ `Classwork Files/ClassWork-3 (Data Model).pbix`

### Generic Model Used for Demonstration

The classwork model contains tables such as:

- 🗂️ `Calendar`
- 🗂️ `Customer`
- 🗂️ `Product`
- 🗂️ `Territories`
- 🗂️ `Sales`
- 🗂️ `Budget`

### Nirvaan Pharma Ltd Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

For this session, focus mainly on:

- 🗂️ `DimDate`
- 🗂️ `DimProduct`
- 🗂️ `DimPlant`
- 🗂️ `DimBatch`
- 🗂️ `DimWarehouse`
- 🗂️ `FactProduction`
- 🗂️ `FactProductionPlan`
- 🗂️ `FactInventorySnapshot`

> 💡 Other fact tables such as Quality, Downtime, Inventory Movement, and Deviations will be used progressively in later analytics sessions.

### Reference for Active/Inactive Relationships

- 🌐 [Microsoft Learn — Active vs inactive relationship guidance](https://learn.microsoft.com/en-us/power-bi/guidance/relationships-active-inactive)

---

## 📚 Data Modeling Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Fact vs Dimension | Identify table roles | 💻 Guided |
| 2 | Grain | Define row-level meaning | 🧑‍🏫 Demo |
| 3 | Star Schema | Build dimension-to-fact structure | 💻 Guided |
| 4 | Relationships | Create and edit relationships | 💻 Guided |
| 5 | Cardinality | One-to-many, many-to-many awareness | 🧑‍🏫 Demo |
| 6 | Filter Direction | Single vs bidirectional | 🧑‍🏫 Demo |
| 7 | Active/Inactive | Role-playing relationship concept | 🧑‍🏫 Demo |
| 8 | Date Table | Calendar, fiscal attributes, sorting | 💻 Guided |
| 9 | Hierarchies | Date/Product navigation | 💻 Guided |
| 10 | Model Hygiene | Hide keys, naming, layout | 💻 Guided |
| 11 | Pharma Star Schema | Nirvaan Pharma Ltd model | 💻 Guided |

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:20 | 📚 Fact, dimension, grain and star-schema concepts |
| 00:20–00:45 | 💻 Review the Sales/Budget model |
| 00:45–01:15 | 💻 Relationships, cardinality and filter direction |
| 01:15–01:40 | 💻 Date table, sorting and hierarchies |
| 01:40–02:15 | 💻 Build the Nirvaan Pharma Ltd model |
| 02:15–02:35 | 🧑‍🏫 Active/inactive relationships and role-playing dates |
| 02:35–02:50 | 💻 Model cleanup and validation |
| 02:50–03:00 | 🔁 Recap and guided challenge review |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. Fact Tables and Dimension Tables

### Fact Table

A fact table usually stores measurable business events.

Examples:

- 📚 Sales transactions
- 📚 Production records
- 📚 Inventory snapshots
- 📚 Production plans

Typical fact-table fields:

- foreign keys
- quantity
- amount
- cost
- duration
- status measures

### Dimension Table

A dimension table describes the business entities used to filter or group facts.

Examples:

- 📚 Date
- 📚 Product
- 📚 Customer
- 📚 Plant
- 📚 Warehouse

### 💡 Simple Rule

- 💡 **Facts = What happened?**
- 💡 **Dimensions = Who / What / Where / When?**

---

## 📚 2. Understand the Grain First

**Grain** means what one row in a table represents.

Examples:

- `Sales` → one sales transaction/record
- `FactProduction` → one production record at its defined business level
- `FactProductionPlan` → one production-plan record at its defined planning level
- `FactInventorySnapshot` → one inventory snapshot record at its defined snapshot level

### 💡 Teaching Point

Before creating a relationship, ask:

> **“What does one row represent in each table?”**

⚠️ Relationships built without understanding grain can produce incorrect totals or duplicate results.

---

## 💻 3. Review the Existing Sales/Budget Model

Open:

- 🗂️ `Classwork Files/ClassWork-3 (Data Model).pbix`

Identify:

### Dimension-Type Tables

- `Calendar`
- `Customer`
- `Product`
- `Territories`

### Fact-Type Tables

- `Sales`
- `Budget`

### Guided Discussion

- 🛠️ Open **Model View**.
- 🛠️ Identify relationship lines.
- 🛠️ Identify the **one** side and **many** side.
- 🛠️ Observe how dimensions can filter fact tables.
- 🛠️ Compare the different business grains of Sales and Budget.

---

<img width="1308" height="526" alt="image" src="https://github.com/user-attachments/assets/925b9e0d-4656-4904-850e-5359b52a6ab0" />

---

## 📚 4. Star Schema

A **star schema** places fact tables in the center and descriptive dimensions around them.

### Typical Structure

```text
              DimDate
                 |
DimProduct — Fact Table — DimPlant
                 |
            DimWarehouse
```

### ✅ Benefits

- ✅ Easier to understand
- ✅ Cleaner filter flow
- ✅ Reusable dimensions
- ✅ Simpler DAX
- ✅ Better scalability

---

<img width="997" height="600" alt="image" src="https://github.com/user-attachments/assets/02f28b62-3afc-40b0-a49e-5254ee3625de" />

---

## 💻 5. Creating Relationships

### 🛠️ Method 1 — Model View

Drag the key from the dimension table to the matching key in the fact table.

### 🛠️ Method 2 — Manage Relationships

- Home → **Manage Relationships**
- Select **New**
- Choose both tables and matching columns
- Verify cardinality and filter direction

### ✅ Validation

Check that:

- ✅ Dimension keys are unique.
- ✅ Fact-side keys may repeat.
- ✅ Matching columns use compatible data types.
- ✅ The intended relationship is active.

---

## 📚 6. Relationship Cardinality

### Common Types

| Cardinality | Meaning | Typical Use |
|---|---|---|
| **One-to-Many (1:*)** | One dimension row relates to many fact rows | Preferred star-schema relationship |
| **One-to-One (1:1)** | One row matches one row | Less common |
| **Many-to-Many (*:*)** | Repeated values exist on both sides | Use only when justified |

### 💡 Preferred Pattern

```text
Dimension (1) ───────── (*) Fact
```

⚠️ Do not use many-to-many simply to make a model “work.” First check the grain and key design.

---

## 📚 7. Cross-Filter Direction

### Single Direction

Preferred default:

```text
Dimension  →  Fact
```

The dimension filters the fact table.

### Bidirectional

Filters can travel both ways.

⚠️ Use bidirectional filtering only when there is a clear modeling requirement. Unnecessary bidirectional relationships can create ambiguous filter paths and confusing results.

---

## 💻 8. Date Table

A proper Date table supports consistent filtering and time-based analysis.

### Use

- 🗂️ `DimDate` from `NirvaanPharma_DW.xlsx`

Review attributes such as:

- Date
- Year
- Quarter
- Month
- Month Number
- Fiscal Year / fiscal attributes

### Guided Steps

- 🛠️ Confirm the date column contains unique dates.
- 🛠️ Use **Mark as Date Table** where applicable.
- 🛠️ Sort Month Name by Month Number.
- 🛠️ Create a Date hierarchy if useful.

### 💡 Important

The Nirvaan Pharma Ltd case uses an **April–March fiscal calendar**, so fiscal fields should be used when the business question requires fiscal reporting.

---

## 💻 9. Hierarchies and Sorting

### Date Hierarchy

Example:

```text
Year
  → Quarter
    → Month
      → Date
```

### Product Hierarchy

Use suitable product attributes where available.

### Sorting

Examples:

- Month Name → sort by Month Number
- Fiscal Month → sort by Fiscal Month Number

✅ **Outcome:** Learners can drill through business levels in the correct sequence.

---

## 💻 10. Build the Nirvaan Pharma Ltd Core Model

Load the selected tables from:

- 🗂️ `NirvaanPharma_DW.xlsx`

### Dimensions

- `DimDate`
- `DimProduct`
- `DimPlant`
- `DimBatch`
- `DimWarehouse`

### Facts

- `FactProduction`
- `FactProductionPlan`
- `FactInventorySnapshot`

### Guided Modeling Approach

- 🛠️ Identify the grain of each fact.
- 🛠️ Use the matching surrogate/business key fields available in the workbook.
- 🛠️ Create **one-to-many** relationships from dimensions to facts.
- 🛠️ Keep filter direction **single** unless a specific requirement justifies otherwise.
- 🛠️ Arrange dimensions around facts for a readable star-schema layout.


### 🔗 Recommended Relationship Wires

Use **single-direction filtering from Dimension → Fact** for the following relationships.

| **Sl. No.** | **From Table** | **From Column** | **To Table**            | **To Column**        | **Cardinality** | **Status** | **Filter Direction** |
| -----------: | -------------- | --------------- | ----------------------- | -------------------- | --------------- | ---------- | -------------------- |
| 1 | `DimDate`      | `DateKey`       | `FactProduction`        | `ManufactureDateKey` | 1 → \*          | ✅ Active   | Dim → Fact |
| 2 | `DimDate`      | `DateKey`       | `FactProduction`        | `ReleaseDateKey`     | 1 → \*          | ⚪ Inactive | Dim → Fact |
| 3 | `DimDate`      | `DateKey`       | `FactProduction`        | `ExpiryDateKey`      | 1 → \*          | ⚪ Inactive | Dim → Fact |
| 4 | `DimDate`      | `DateKey`       | `FactProductionPlan`    | `PlanMonthDateKey`   | 1 → \*          | ✅ Active   | Dim → Fact |
| 5 | `DimDate`      | `DateKey`       | `FactInventorySnapshot` | `SnapshotDateKey`    | 1 → \*          | ✅ Active   | Dim → Fact |
| 6 | `DimDate`      | `DateKey`       | `FactInventorySnapshot` | `ExpiryDateKey`      | 1 → \*          | ⚪ Inactive | Dim → Fact |
| 7 | `DimProduct`   | `ProductKey`    | `FactProduction`        | `ProductKey`         | 1 → \*          | ✅ Active   | Dim → Fact |
| 8 | `DimProduct`   | `ProductKey`    | `FactProductionPlan`    | `ProductKey`         | 1 → \*          | ✅ Active   | Dim → Fact |
| 9 | `DimProduct`   | `ProductKey`    | `FactInventorySnapshot` | `ProductKey`         | 1 → \*          | ✅ Active   | Dim → Fact |
| 10 | `DimPlant`    | `PlantKey`      | `FactProduction`        | `PlantKey`           | 1 → \*          | ✅ Active   | Dim → Fact |
| 11 | `DimPlant`    | `PlantKey`      | `FactProductionPlan`    | `PlantKey`           | 1 → \*          | ✅ Active   | Dim → Fact |
| 12 | `DimPlant`    | `PlantKey`      | `FactInventorySnapshot` | `PlantKey`           | 1 → \*          | ✅ Active   | Dim → Fact |
| 13 | `DimBatch`    | `BatchKey`      | `FactProduction`        | `BatchKey`           | 1 → \*          | ✅ Active   | Dim → Fact |
| 14 | `DimBatch`    | `BatchKey`      | `FactInventorySnapshot` | `BatchKey`           | 1 → \*          | ✅ Active   | Dim → Fact |
| 15 | `DimWarehouse`| `WarehouseKey`  | `FactInventorySnapshot` | `WarehouseKey`       | 1 → \*          | ✅ Active   | Dim → Fact |

### 💡 Filter Transmission Rule

> **Dimension (1) → Fact (*)**, using **single-direction filtering** by default.

Examples:

- `DimProduct` should filter Production, Production Plan, and Inventory Snapshot.
- `DimPlant` should filter all three selected fact tables.
- `DimBatch` should filter Production and Inventory Snapshot, but **not** Production Plan.
- `DimWarehouse` should filter **Inventory Snapshot only**.
- `DimDate` should use the intended active business date for each fact.

⚠️ Do not create extra Dimension-to-Dimension relationships merely because matching keys exist. They may create unnecessary or ambiguous filter paths.

---

<img width="1512" height="742" alt="image" src="https://github.com/user-attachments/assets/b5b22141-6f20-4896-a5e5-18635594a7b6" />

---

### ✅ Expected Model Behavior

Examples:

- Product filtering should affect relevant production and inventory facts.
- Plant filtering should affect the relevant operational facts.
- Date filtering should follow the intended business date relationship.

---

## 🧑‍🏫 11. Active, Inactive and Role-Playing Relationships

A fact table may contain multiple business dates.

Examples:

- production date
- release date
- expiry date
- snapshot date

A single Date dimension may therefore play different roles.

### Teaching Concept

- 📚 **Active relationship** — the default filter path used automatically.
- 📚 **Inactive relationship** — an alternative relationship available for a different business meaning.
- 📚 **Role-playing date dimension** — one Date dimension reused for multiple date roles.

For `FactProduction`:

```text
DimDate[DateKey]
   ├── ✅ Active   → FactProduction[ManufactureDateKey]
   ├── ⚪ Inactive → FactProduction[ReleaseDateKey]
   └── ⚪ Inactive → FactProduction[ExpiryDateKey]
```

Therefore, a normal `DimDate` slicer filters Production by **Manufacture Date**.

### 🧮 Using an Inactive Relationship in DAX

The DAX function used to activate an inactive relationship **inside a calculation** is:

`USERELATIONSHIP()`

Example:

```DAX
Released Production =
CALCULATE(
    SUM(FactProduction[ProducedQtyUnits]),
    USERELATIONSHIP(
        DimDate[DateKey],
        FactProduction[ReleaseDateKey]
    )
)
```

### 💡 What to Teach at This Stage

- 💡 Explain **why** the inactive relationship exists.
- 💡 Show the `USERELATIONSHIP()` syntax once.
- 💡 Explain that it temporarily changes the relationship used by that measure.
- ⚠️ Do not teach advanced DAX behavior here; detailed practice comes in the DAX sessions.
- ⚠️ Do not make multiple competing date relationships active when they create ambiguity.

### 🌐 Learn More

Learners may refer to:

[Microsoft Learn — Active vs inactive relationship guidance](https://learn.microsoft.com/en-us/power-bi/guidance/relationships-active-inactive)

---

## 💻 12. Model Hygiene and Usability

Before reporting:

- 🛠️ Hide technical key columns not needed by report users.
- 🛠️ Use clear business-friendly names.
- 🛠️ Keep fact and dimension tables visually organized.
- 🛠️ Avoid unnecessary relationships.
- 🛠️ Remove unused columns when appropriate.
- 🛠️ Use consistent formatting for numeric/date fields.
- 🛠️ Keep the model understandable to another developer.

### 💡 Naming Guidance

Prefer:

- `Production Quantity`
- `Plant`
- `Product`

Avoid unexplained technical abbreviations where possible.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Open `ClassWork-3 (Data Model).pbix`.
2. 💻 Identify fact and dimension tables.
3. 💻 Explain the grain of `Sales` and `Budget`.
4. 💻 Verify one relationship's cardinality and filter direction.
5. 💻 Load the selected Nirvaan Pharma Ltd tables.
6. 💻 Identify the five core dimensions.
7. 💻 Identify the three selected fact tables.
8. 💻 Create the relationships according to the **Recommended Relationship Wires** table.
9. 💻 Verify active and inactive Date relationships.
10. 💻 Configure the Date table and month sorting.
11. 💻 Create at least one hierarchy.
12. 💻 Hide unnecessary technical keys.
13. 💻 Arrange the model into a readable star-schema layout.

### ✅ Expected Outcome

A clean semantic model in which dimensions filter the appropriate fact tables through understandable and controlled relationships.

---

## 💡 Trainer Guidelines

- 💡 Teach **grain before relationships**.
- 💡 Reinforce **Dimension (1) → Fact (*)** as the preferred pattern.
- 💡 Keep cross-filter direction single by default.
- 💡 Explain many-to-many as an exception, not a shortcut.
- 💡 Use the simpler Sales/Budget model before the pharma model.
- 💡 Introduce only the Nirvaan Pharma Ltd tables needed for this session.
- 💡 Demonstrate `USERELATIONSHIP()` once to show how an inactive Date relationship can be used in a measure.
- ⚠️ Do not build complex DAX measures yet.
- ⚠️ Do not enable bidirectional filtering merely to fix a visual.
- ⚠️ Validate slicer/filter behavior after creating relationships.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 Fact tables, dimension tables, and grain.
- 🔁 Star-schema design.
- 🔁 One-to-many relationships.
- 🔁 Cardinality and filter direction.
- 🔁 Date tables and hierarchies.
- 🔁 Active/inactive relationship concepts and the purpose of `USERELATIONSHIP()`.
- 🔁 Basic semantic-model hygiene.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What does the grain of a table describe?

A. The report background color <br>
B. What one row in the table represents <br>
C. The Power BI license type <br>
D. The number of report pages <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. What one row in the table represents**

**Explanation:** Grain defines the level of detail represented by each row and should be understood before relationships are designed.

</details>

### 🔴 Q2. Which type of table normally stores measurable business events?

A. Dimension table <br>
B. Fact table <br>
C. Parameter table only <br>
D. Navigation table <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Fact table**

**Explanation:** Fact tables normally contain business events and numeric measures such as quantity, cost, sales, or duration.

</details>

### 🔴 Q3. Which table is most likely to be a dimension?

A. Product <br>
B. Sales Transactions <br>
C. Production Transactions <br>
D. Inventory Movements <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Product**

**Explanation:** Product describes a business entity used to categorize or filter facts.

</details>

### 🔴 Q4. What is the preferred relationship pattern in a basic star schema?

A. Fact (1) → Dimension (\*) <br>
B. Dimension (1) → Fact (\*) <br>
C. Fact (\*) ↔ Fact (\*) for every table <br>
D. No relationships <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Dimension (1) → Fact (*)**

**Explanation:** Dimension keys are normally unique, while the corresponding foreign key can repeat many times in the fact table.

</details>

### 🔴 Q5. What is the preferred default cross-filter direction in a star schema?

A. Dimension to Fact <br>
B. Fact to Dimension only <br>
C. Bidirectional everywhere <br>
D. No filtering <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Dimension to Fact**

**Explanation:** Single-direction filtering from dimensions to facts creates a predictable and understandable filter flow.

</details>

### 🔴 Q6. Why should bidirectional relationships be used carefully?

A. They always delete records <br>
B. They can create ambiguous filter paths and confusing results <br>
C. They prevent all DAX calculations <br>
D. They convert numbers to text <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. They can create ambiguous filter paths and confusing results**

**Explanation:** Bidirectional filters can create multiple filter paths, so they should be enabled only when the model genuinely requires them.

</details>

### 🔴 Q7. What is a major benefit of a star schema?

A. It makes filtering and analysis easier to understand <br>
B. It removes the need for data cleaning <br>
C. It eliminates all DAX <br>
D. It converts Power BI into a database server <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. It makes filtering and analysis easier to understand**

**Explanation:** A star schema separates descriptive dimensions from business facts and produces a cleaner semantic model.

</details>

### 🔴 Q8. Why is a dedicated Date table useful?

A. It supports consistent date filtering and time-based analysis <br>
B. It replaces every fact table <br>
C. It publishes reports automatically <br>
D. It removes the need for relationships <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. It supports consistent date filtering and time-based analysis**

**Explanation:** A Date table provides reusable calendar attributes and supports time-oriented reporting across fact tables.

</details>

### 🔴 Q9. Why should Month Name often be sorted by Month Number?

A. To prevent alphabetical month ordering <br>
B. To create a many-to-many relationship <br>
C. To hide the Date table <br>
D. To convert months into measures <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. To prevent alphabetical month ordering**

**Explanation:** Sorting Month Name by Month Number ensures January–December or the intended fiscal sequence is displayed correctly.

</details>

### 🔴 Q10. Which DAX function can use an inactive relationship inside a calculation?

A. `SUM()` <br>
B. `USERELATIONSHIP()` <br>
C. `FORMAT()` <br>
D. `COUNTROWS()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. `USERELATIONSHIP()`**

**Explanation:** `USERELATIONSHIP()` tells a DAX calculation to use a specified inactive relationship for that calculation.

</details>

### 🔴 Q11. Why are technical key columns often hidden from report users?

A. They are usually implementation fields rather than useful business attributes <br>
B. Power BI cannot store keys <br>
C. Hidden columns are automatically deleted <br>
D. Keys cannot participate in relationships <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. They are usually implementation fields rather than useful business attributes**

**Explanation:** Keys remain available to the model while hiding them keeps the report field list cleaner for users.

</details>

### 🔴 Q12. What should be checked first if a relationship produces unexpected totals?

A. Report wallpaper <br>
B. Table grain, keys, cardinality, and filter direction <br>
C. Monitor resolution <br>
D. Page navigation buttons <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Table grain, keys, cardinality, and filter direction**

**Explanation:** Unexpected totals often indicate a modeling issue such as incorrect grain, duplicate keys, wrong cardinality, or unintended filter flow.

</details>

---

### ➡️ Next Session

**Section 05 — DAX Fundamentals**

Learners will use the semantic model to create **measures, calculated columns, aggregations, iterators, row context, filter context, and core DAX calculations**.
