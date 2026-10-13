# Section 08 — Pharma Analytics II: Inventory and Expiry Analysis

**Day:** 4 — Post-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Understand **inventory snapshot** and **inventory movement** analysis.
- 🎯 Explain why inventory balances are **semi-additive** across time.
- 🎯 Create reusable measures for **Inventory Quantity, Inventory Value, Batch Count, Expiry Risk, and Stock Movement**.
- 🎯 Analyze inventory by **Product, Plant, Warehouse, and Stock Status**.
- 🎯 Identify inventory **expiring within 90 days** from a selected snapshot date.
- 🎯 Compare **Inbound vs Outbound** stock movement.
- 🎯 Build a focused **Inventory & Expiry Analysis dashboard**.
- 🎯 Validate inventory balances and expiry-risk calculations before interpreting them.

---

## 🗂️ Resources Used

### Primary Case-Study Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

### Primary Tables

- `FactInventorySnapshot`
- `FactInventoryMovement`
- `DimDate`
- `DimProduct`
- `DimBatch`
- `DimPlant`
- `DimWarehouse`

### Important Inventory Fields

#### `FactInventorySnapshot`

- `SnapshotDateKey`
- `ProductKey`
- `BatchKey`
- `PlantKey`
- `WarehouseKey`
- `ExpiryDateKey`
- `QtyOnHandUnits`
- `InventoryValueINR`

#### `FactInventoryMovement`

- `MovementDateKey`
- `ProductKey`
- `BatchKey`
- `WarehouseKey`
- `MovementType`
- `MovementDirection`
- `QuantityUnits`
- `MovementValueINR`

#### Supporting Dimensions

- `DimBatch[ExpiryDate]`
- `DimWarehouse[WarehouseName]`
- `DimWarehouse[StockStatus]`
- `DimWarehouse[StorageType]`
- `DimProduct[ProductName]`
- `DimPlant[PlantName]`

> 💡 **Important:** `QtyOnHandUnits` and `InventoryValueINR` are **month-end snapshot balances**. They are semi-additive and should **not be summed across multiple snapshot dates**.

---

## 🔗 Required Relationships

The inventory snapshot relationships created earlier should include:

```text
DimDate[DateKey]
   ├── ✅ Active   → FactInventorySnapshot[SnapshotDateKey]
   └── ⚪ Inactive → FactInventorySnapshot[ExpiryDateKey]

DimProduct[ProductKey]
   └── ✅ Active   → FactInventorySnapshot[ProductKey]

DimBatch[BatchKey]
   └── ✅ Active   → FactInventorySnapshot[BatchKey]

DimPlant[PlantKey]
   └── ✅ Active   → FactInventorySnapshot[PlantKey]

DimWarehouse[WarehouseKey]
   └── ✅ Active   → FactInventorySnapshot[WarehouseKey]
```

For `FactInventoryMovement`, add or verify:

```text
DimDate[DateKey]
   └── ✅ Active → FactInventoryMovement[MovementDateKey]

DimProduct[ProductKey]
   └── ✅ Active → FactInventoryMovement[ProductKey]

DimBatch[BatchKey]
   └── ✅ Active → FactInventoryMovement[BatchKey]

DimWarehouse[WarehouseKey]
   └── ✅ Active → FactInventoryMovement[WarehouseKey]
```

> ⚠️ Keep the Snapshot Date relationship active for inventory-balance analysis. Do not make the competing Expiry Date relationship active merely to build an expiry visual.

---

## 📚 Inventory Analytics Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Snapshot vs Movement | Understand inventory grains | 🧑‍🏫 Demo |
| 2 | Semi-Additive Inventory | Latest visible snapshot measures | 💻 Guided |
| 3 | KPI Summary | Quantity, Value, Batches | 💻 Guided |
| 4 | Warehouse Analysis | Inventory by Warehouse | 💻 Guided |
| 5 | Stock Status | Released / Quarantine / Rejected | 💻 Guided |
| 6 | Expiry Risk | Inventory expiring within 90 days | 💻 Guided |
| 7 | Product Expiry Risk | Identify products needing attention | 💻 Guided |
| 8 | Inventory Movement | Inbound / Outbound / Net movement | 💻 Guided |
| 9 | Detailed Analysis | Product × Warehouse Matrix | 💻 Guided |
| 10 | Dashboard Validation | Reconcile balances and risk measures | 💻 Guided |

---

## 🧭 DAX — Purpose and Target Map

This section mainly **reuses DAX functions already learned**.

| DAX Function / Construct | Purpose | Target in This Section |
|---|---|---|
| `SUM()` | Add numeric values | Inventory Quantity, Inventory Value, Movement Quantity |
| `MAX()` | Find the latest visible snapshot/date | Latest inventory snapshot |
| `CALCULATE()` | Re-evaluate a measure under changed filters | Latest snapshot, Stock Status, Expiry Risk |
| `FILTER()` | Return rows meeting a condition | Expiry-window analysis |
| `DISTINCTCOUNT()` | Count unique values | Inventory Batch Count |
| `DIVIDE()` | Safe ratio calculation | Expiry Risk % |
| `VAR` / `RETURN` | Store and reuse intermediate values | Latest snapshot measures |

> 💡 **No major new DAX function is required here.** The focus is applying familiar DAX to a new business problem.

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:20 | 📚 Snapshot vs movement and semi-additive concept |
| 00:20–00:45 | 💻 Inventory balance measures |
| 00:45–01:05 | 💻 KPI Cards and Snapshot Date filtering |
| 01:05–01:30 | 💻 Warehouse and Stock Status analysis |
| 01:30–02:00 | 💻 Expiry-risk measures and visuals |
| 02:00–02:25 | 💻 Inventory movement analysis |
| 02:25–02:45 | 💻 Detailed Matrix and dashboard layout |
| 02:45–03:00 | ✅ Validation, recap, and Q&A |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

## 📚 1. Inventory Snapshot vs Inventory Movement

These two fact tables answer different questions.

### Inventory Snapshot

`FactInventorySnapshot` represents a **month-end closing inventory position**.

Typical question:

> How much inventory was on hand at a particular month end?

### Inventory Movement

`FactInventoryMovement` represents **stock movement transactions**.

Typical question:

> How much inventory moved in or out during a period?

### 💡 Simple Rule

- **Snapshot** → “What balance did we have?”
- **Movement** → “What changed during the period?”

---

## 📚 2. Understand Semi-Additive Inventory

Inventory balance is different from sales or production.

Suppose:

```text
April Closing Inventory = 2,000 units
May Closing Inventory   = 2,500 units
June Closing Inventory  = 2,200 units
```

Do **not** calculate:

```text
2,000 + 2,500 + 2,200 = 6,700 units
```

That would incorrectly add three separate closing balances.

Instead, for a selected reporting period, use the **latest applicable snapshot**.

### 💡 Teaching Point

> **Inventory is additive across Product / Plant / Warehouse, but not across Snapshot Dates.**

---

## 💻 3. Create Core Inventory Measures

### Inventory Quantity

```DAX
Inventory Quantity =
VAR LatestSnapshotKey =
    MAX(FactInventorySnapshot[SnapshotDateKey])
RETURN
    CALCULATE(
        SUM(FactInventorySnapshot[QtyOnHandUnits]),
        FactInventorySnapshot[SnapshotDateKey] = LatestSnapshotKey
    )
```

- 🎯 **Purpose:** Return quantity from the latest visible inventory snapshot.
- 🧭 **Target:** Avoid incorrectly summing inventory balances across several months.

### Inventory Value

```DAX
Inventory Value =
VAR LatestSnapshotKey =
    MAX(FactInventorySnapshot[SnapshotDateKey])
RETURN
    CALCULATE(
        SUM(FactInventorySnapshot[InventoryValueINR]),
        FactInventorySnapshot[SnapshotDateKey] = LatestSnapshotKey
    )
```

- 🎯 **Purpose:** Return closing inventory value from the latest visible snapshot.
- 🧭 **Target:** Show inventory value at standard cost for the selected context.

### Inventory Batch Count

```DAX
Inventory Batch Count =
VAR LatestSnapshotKey =
    MAX(FactInventorySnapshot[SnapshotDateKey])
RETURN
    CALCULATE(
        DISTINCTCOUNT(FactInventorySnapshot[BatchKey]),
        FactInventorySnapshot[SnapshotDateKey] = LatestSnapshotKey
    )
```

- 🎯 **Purpose:** Count distinct batches in the latest visible inventory snapshot.
- 🧭 **Target:** Understand how many batches make up current inventory.

### ✅ Validation

Use a **Date Slicer** with:

- `DimDate[Date]`

Select exactly:

**31-May-2025**

Create three **Card visuals**:

- `[Inventory Quantity]`
- `[Inventory Value]`
- `[Inventory Batch Count]`

Expected values:

| Measure | Expected Value |
|---|---:|
| Inventory Quantity | 2,437,829 |
| Inventory Value | ₹917,003,680.38 |
| Inventory Batch Count | 549 |

> 💡 **Trainer Note:** Use a month-end Snapshot Date for the demonstration because the fact table stores month-end balances.

---

## 💻 4. Build the Inventory KPI Summary

### 🛠️ Slicers

Add:

- **Snapshot Date** → `DimDate[Date]`
- **Product** → `DimProduct[ProductName]`
- **Plant** → `DimPlant[PlantName]`
- **Warehouse** → `DimWarehouse[WarehouseName]`

### 🛠️ KPI Cards

Create Cards for:

- `[Inventory Quantity]`
- `[Inventory Value]`
- `[Inventory Batch Count]`

### ✅ Validation

With Snapshot Date = **31-May-2025**:

1. Select one Product.
2. Confirm all Cards recalculate.
3. Clear Product and select one Plant.
4. Confirm all Cards recalculate again.
5. Clear all filters and confirm the overall values return.

> 🖼️ **Image Placeholder S08-01:** Inventory KPI Cards with Snapshot Date, Product, Plant, and Warehouse slicers.  
> **Planned file:** `images/S08_01_Inventory_KPIs.png`

---

## 💻 5. Inventory by Warehouse

### Business Question

> Where is inventory physically held?

### 🛠️ Visual Type

**Clustered Bar Chart**

### 🛠️ Configure the Visual

**Y-axis / Category**
- `DimWarehouse[WarehouseName]`

**X-axis / Values**
- `[Inventory Quantity]`

### Tooltips

Add:

- `[Inventory Value]`
- `[Inventory Batch Count]`
- `DimWarehouse[StockStatus]`
- `DimWarehouse[StorageType]`

### Sort

Sort:

**Inventory Quantity → Descending**

### ✅ Validation

Using Snapshot Date = **31-May-2025**:

- Clear the Warehouse slicer.
- Confirm all Warehouses appear.
- Click one Warehouse bar.
- Confirm the KPI Cards respond to that Warehouse.

### 💡 Interpretation Questions

- Which Warehouse holds the most inventory?
- Is that inventory Released, Quarantine, or Rejected?
- Is it Ambient or Cold Chain stock?
- Does Warehouse concentration change by Product?

---

## 💻 6. Inventory by Stock Status

### Business Question

> How is inventory distributed between Released, Quarantine, and Rejected stock?

### 🛠️ Visual Type

**Donut Chart**

### 🛠️ Configure the Visual

**Legend**
- `DimWarehouse[StockStatus]`

**Values**
- `[Inventory Quantity]`

### ✅ Validation

For Snapshot Date = **31-May-2025**, expected quantities are:

| Stock Status | Inventory Quantity |
|---|---:|
| Released | 1,610,259 |
| Quarantine | 781,866 |
| Rejected | 45,704 |

Confirm:

```text
1,610,259 + 781,866 + 45,704
= 2,437,829
```

This should reconcile with the `[Inventory Quantity]` Card.

> 💡 **Teaching Point:** A Donut Chart is appropriate here because the three Stock Status categories form parts of one total inventory balance.

> 🖼️ **Image Placeholder S08-02:** Inventory composition by Released, Quarantine, and Rejected Stock Status.  
> **Planned file:** `images/S08_02_Inventory_Status.png`

---

## 💻 7. Expiry Risk — Inventory Expiring Within 90 Days

### Business Question

> How much inventory will expire within 90 days of the selected Snapshot Date?

Use `DimBatch[ExpiryDate]` for the expiry condition.

### Inventory Expiring in 90 Days

```DAX
Inventory Expiring in 90 Days =
VAR SnapshotDate =
    MAX(DimDate[Date])
RETURN
    CALCULATE(
        [Inventory Quantity],
        FILTER(
            DimBatch,
            DimBatch[ExpiryDate] >= SnapshotDate
                && DimBatch[ExpiryDate] <= SnapshotDate + 90
        )
    )
```

- 🎯 **`MAX()` Purpose:** Read the selected/latest Date in the current context.
- 🎯 **`FILTER()` Purpose:** Keep only batches expiring inside the 90-day window.
- 🧭 **Target:** Quantify near-expiry inventory.

### Inventory Value Expiring in 90 Days

```DAX
Inventory Value Expiring in 90 Days =
VAR SnapshotDate =
    MAX(DimDate[Date])
RETURN
    CALCULATE(
        [Inventory Value],
        FILTER(
            DimBatch,
            DimBatch[ExpiryDate] >= SnapshotDate
                && DimBatch[ExpiryDate] <= SnapshotDate + 90
        )
    )
```

### Expiry Risk %

```DAX
Expiry Risk % =
DIVIDE(
    [Inventory Expiring in 90 Days],
    [Inventory Quantity],
    0
)
```

- 🎯 **`DIVIDE()` Purpose:** Safely calculate the share of total inventory that is near expiry.
- 🧭 **Target:** Express expiry exposure as a percentage of inventory quantity.

### ✅ Validation

Select Snapshot Date:

**31-May-2025**

Create three Cards:

- `[Inventory Expiring in 90 Days]`
- `[Inventory Value Expiring in 90 Days]`
- `[Expiry Risk %]`

Expected values:

| Measure | Expected Value |
|---|---:|
| Inventory Expiring in 90 Days | 64,243 |
| Inventory Value Expiring in 90 Days | ₹21,183,019.11 |
| Expiry Risk % | ≈ 2.64% |

Manual check:

```text
64,243 ÷ 2,437,829
≈ 2.64%
```

> 💡 **Business Meaning:** This measure represents inventory expiring from the selected Snapshot Date through the next 90 days.

---

## 💻 8. Products with Near-Expiry Inventory

### Business Question

> Which Products account for the most near-expiry inventory?

### 🛠️ Visual Type

**Clustered Bar Chart**

### 🛠️ Configure the Visual

**Y-axis**
- `DimProduct[ProductName]`

**X-axis**
- `[Inventory Expiring in 90 Days]`

### Tooltips

Add:

- `[Inventory Value Expiring in 90 Days]`
- `[Expiry Risk %]`
- `[Inventory Quantity]`

### Sort

Sort:

**Inventory Expiring in 90 Days → Descending**

### ✅ Validation

With Snapshot Date = **31-May-2025**:

- Confirm the visual total reconciles to **64,243** units.
- Hover over a Product and verify its tooltip measures respond to the same filter context.
- Select one Product and confirm KPI Cards update.

### 💡 Interpretation Questions

- Which Products account for the largest near-expiry quantity?
- Does high near-expiry quantity also represent high inventory value?
- Does one Warehouse or Plant account for most of the exposure?

> ⚠️ Use this visual to identify areas for further investigation; do not automatically treat every near-expiry batch as unusable inventory.

> 🖼️ **Image Placeholder S08-03:** Product-level near-expiry inventory analysis.  
> **Planned file:** `images/S08_03_Expiry_Risk.png`

---

## 💻 9. Inventory Movement Analysis

### Business Question

> How much stock moved into and out of inventory during a period?

`FactInventoryMovement[QuantityUnits]` is **signed**:

- Inbound movement → positive quantity.
- Outbound movement → negative quantity.

### Inbound Quantity

```DAX
Inbound Quantity =
CALCULATE(
    SUM(FactInventoryMovement[QuantityUnits]),
    FactInventoryMovement[MovementDirection] = "In"
)
```

### Outbound Quantity

Display outbound quantity as a positive magnitude:

```DAX
Outbound Quantity =
-
CALCULATE(
    SUM(FactInventoryMovement[QuantityUnits]),
    FactInventoryMovement[MovementDirection] = "Out"
)
```

### Net Movement Quantity

```DAX
Net Movement Quantity =
SUM(FactInventoryMovement[QuantityUnits])
```

### 💡 Important

`MovementValueINR` is an inventory movement value, not sales revenue.

Also, outbound `MovementValueINR` values are stored as positive amounts, so do **not** calculate Net Movement Value by simply summing inbound and outbound values together.

### 🛠️ Visual Type

Use a **Clustered Column Chart**.

**X-axis**
- `DimDate[CalendarYearMonth]`

**Y-axis / Values**
- `[Inbound Quantity]`
- `[Outbound Quantity]`

### Optional Card

- `[Net Movement Quantity]`

### ✅ Validation

Filter the movement analysis to:

**May 2025**

Expected:

| Measure | Expected Value |
|---|---:|
| Inbound Quantity | 738,295 |
| Outbound Quantity | 968,595 |
| Net Movement Quantity | -230,300 |

Manual check:

```text
738,295 - 968,595
= -230,300
```

> 💡 **Teaching Point:** Snapshot inventory shows the balance; movement data helps explain how inventory changed.

---

## 💻 10. Detailed Product × Warehouse Inventory Matrix

### Business Question

> Which Products are held in which Warehouses, and where is expiry exposure concentrated?

### 🛠️ Visual Type

**Matrix**

### 🛠️ Configure the Matrix

**Rows**
- `DimProduct[ProductName]`

**Columns**
- `DimWarehouse[WarehouseName]`

**Values**
- `[Inventory Quantity]`
- `[Inventory Value]`
- `[Inventory Expiring in 90 Days]`
- `[Expiry Risk %]`

### Conditional Formatting

Recommended:

- `[Inventory Expiring in 90 Days]`
- `[Expiry Risk %]`

### ✅ Validation

Using Snapshot Date = **31-May-2025**:

- ✅ Matrix Inventory Quantity total = **2,437,829**.
- ✅ Matrix Inventory Value total = **₹917,003,680.38**.
- ✅ Near-expiry total = **64,243**.
- ✅ Matrix totals reconcile with the KPI Cards.
- ✅ Product and Warehouse selections change the measures consistently.

> 💡 The Matrix is the main **investigation and validation visual** in this session.

---

## 🧩 11. Recommended Dashboard Layout

Create one report page named:

**Inventory & Expiry Analysis**

Suggested layout:

```text
┌──────────────────────────────────────────────────────────────┐
│ Snapshot Date | Product | Plant | Warehouse                 │
├──────────────────────────────────────────────────────────────┤
│ Inventory Qty | Inventory Value | Batches | Expiring 90D   │
│ Value at Risk | Expiry Risk %                               │
├─────────────────────────────┬────────────────────────────────┤
│ Inventory by Warehouse      │ Stock Status Donut            │
├─────────────────────────────┼────────────────────────────────┤
│ Near-Expiry by Product      │ Inbound vs Outbound Movement  │
├──────────────────────────────────────────────────────────────┤
│ Product × Warehouse Inventory / Expiry Matrix               │
└──────────────────────────────────────────────────────────────┘
```

### 💡 Page Design Guidance

- Keep inventory KPI Cards at the top.
- Use Warehouse and Status visuals for inventory composition.
- Keep near-expiry analysis visually prominent.
- Place the detailed Matrix at the bottom.
- Keep movement analysis secondary to the closing inventory position.

> 🖼️ **Image Placeholder S08-04:** Final Inventory & Expiry Analysis dashboard layout.  
> **Planned file:** `images/S08_04_Inventory_Dashboard.png`

---

## ✅ 12. Dashboard Validation Checklist

### Snapshot Logic

- ✅ Snapshot Date uses the active `SnapshotDateKey` relationship.
- ✅ Inventory Quantity uses the latest visible snapshot.
- ✅ Inventory balances are not summed across multiple months.

### Base Values

For **31-May-2025**:

- ✅ Inventory Quantity = **2,437,829**.
- ✅ Inventory Value = **₹917,003,680.38**.
- ✅ Inventory Batch Count = **549**.

### Stock Status Reconciliation

```text
Released + Quarantine + Rejected
=
Total Inventory Quantity
```

### Expiry Risk Reconciliation

```text
Expiry Risk %
=
Inventory Expiring in 90 Days
÷
Inventory Quantity
```

### Movement Reconciliation

```text
Net Movement Quantity
=
Inbound Quantity
-
Outbound Quantity
```

### Filter Response

- ✅ Product filters inventory visuals correctly.
- ✅ Plant filters Inventory Snapshot visuals correctly.
- ✅ Warehouse filters Snapshot and Movement visuals correctly.
- ✅ Snapshot Date and Movement Date are interpreted according to the correct fact-table grain.

> 💡 **Validation Rule:** Always validate **Snapshot Balance**, **Expiry Window**, and **Movement Direction** separately.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Create `[Inventory Quantity]`.
2. 💻 Create `[Inventory Value]`.
3. 💻 Create `[Inventory Batch Count]`.
4. 💻 Validate the 31-May-2025 closing inventory.
5. 💻 Create the Warehouse Bar Chart.
6. 💻 Create the Stock Status Donut Chart.
7. 💻 Create `[Inventory Expiring in 90 Days]`.
8. 💻 Create `[Inventory Value Expiring in 90 Days]`.
9. 💻 Create `[Expiry Risk %]`.
10. 💻 Create the Near-Expiry Product Bar Chart.
11. 💻 Create Inbound, Outbound, and Net Movement measures.
12. 💻 Build the Product × Warehouse Matrix.
13. 💻 Apply conditional formatting.
14. 💻 Reconcile one Matrix total with a KPI Card.
15. 💻 Complete **Dashboard Page 2 — Inventory & Expiry Analysis**.

### ✅ Expected Outcome

Learners can distinguish **inventory balances from inventory movements**, identify **near-expiry exposure**, and build a validated inventory dashboard without incorrectly summing month-end balances.

---

## 💡 Trainer Guidelines

- 💡 Explain **semi-additive inventory** before creating any inventory measures.
- 💡 Use **31-May-2025** as the main Snapshot Date because it provides meaningful expiry-risk data.
- 💡 Keep Snapshot Date and Movement Date concepts separate.
- 💡 Reuse `SUM`, `MAX`, `CALCULATE`, `FILTER`, `DISTINCTCOUNT`, `DIVIDE`, and `VAR / RETURN`.
- 💡 Use Cards for headline inventory KPIs.
- 💡 Use a Donut Chart only for the small Stock Status part-to-whole comparison.
- 💡 Use Bar Charts for Warehouse/Product comparison.
- 💡 Use the Matrix for exact validation and investigation.
- 💡 Manually reconcile at least one expiry-risk percentage and one movement period.
- ⚠️ Never sum `QtyOnHandUnits` or `InventoryValueINR` across Snapshot Dates.
- ⚠️ Do not interpret `MovementValueINR` as sales revenue.
- ⚠️ Do not treat positive outbound Movement Value as an inbound movement; use `MovementDirection` / signed `QuantityUnits`.
- ⚠️ Do not activate the Expiry Date relationship and unintentionally replace Snapshot Date semantics.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 Inventory Snapshot vs Inventory Movement.
- 🔁 Why inventory balances are semi-additive.
- 🔁 Latest-snapshot inventory measures.
- 🔁 Warehouse and Stock Status analysis.
- 🔁 Near-expiry inventory and Expiry Risk %.
- 🔁 Inbound, Outbound, and Net Movement.
- 🔁 Product × Warehouse investigation.
- 🔁 How to validate an Inventory & Expiry dashboard.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What does `FactInventorySnapshot` primarily represent?

A. Month-end inventory balances <br>
B. Employee attendance <br>
C. Customer master data <br>
D. Production-plan targets only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Month-end inventory balances**

**Explanation:** The snapshot fact stores closing inventory quantity and value at month-end snapshot dates.

</details>

### 🔴 Q2. Why should inventory quantity not be summed across multiple Snapshot Dates?

A. Inventory is semi-additive across time <br>
B. `SUM()` cannot work with numbers <br>
C. Snapshot dates cannot be filtered <br>
D. Inventory has no Product key <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Inventory is semi-additive across time**

**Explanation:** Each snapshot is a separate closing balance, so adding balances from several months would overstate inventory.

</details>

### 🔴 Q3. Which function is used to identify the latest visible Snapshot key in the inventory measure?

A. `MAX()` <br>
B. `MINX()` <br>
C. `SWITCH()` <br>
D. `RANKX()` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `MAX()`**

**Explanation:** `MAX()` identifies the latest SnapshotDateKey available in the current filter context.

</details>

### 🔴 Q4. Which dimension is most directly used to analyze inventory by Warehouse?

A. `DimWarehouse` <br>
B. `DimOperator` <br>
C. `DimQCTest` <br>
D. `DimCustomer` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `DimWarehouse`**

**Explanation:** `DimWarehouse` describes inventory locations and attributes such as Warehouse Name, Stock Status, and Storage Type.

</details>

### 🔴 Q5. Which visual is suitable for Released / Quarantine / Rejected inventory composition?

A. Donut Chart <br>
B. Scatter Chart <br>
C. Map only <br>
D. Text box <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Donut Chart**

**Explanation:** The three Stock Status categories form a small and meaningful part-to-whole inventory comparison.

</details>

### 🔴 Q6. What does `[Inventory Expiring in 90 Days]` measure?

A. Inventory whose batch Expiry Date falls within 90 days of the selected Snapshot Date <br>
B. Inventory produced exactly 90 days ago <br>
C. All historical production <br>
D. Only rejected inventory <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Inventory whose batch Expiry Date falls within 90 days of the selected Snapshot Date**

**Explanation:** The measure filters batches by their Expiry Date relative to the selected Snapshot Date.

</details>

### 🔴 Q7. How is Expiry Risk % calculated?

A. Expiring Inventory ÷ Total Inventory Quantity <br>
B. Production Quantity ÷ Inventory Value <br>
C. Batch Count + Inventory Quantity <br>
D. Outbound Quantity ÷ Inbound Quantity only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Expiring Inventory ÷ Total Inventory Quantity**

**Explanation:** Expiry Risk % expresses near-expiry quantity as a share of the total closing inventory quantity.

</details>

### 🔴 Q8. What does a positive `QuantityUnits` value represent in `FactInventoryMovement`?

A. Inbound stock movement <br>
B. Always an expiry write-off <br>
C. A report filter <br>
D. An inactive relationship <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Inbound stock movement**

**Explanation:** Movement quantity is signed: inbound is positive and outbound is negative.

</details>

### 🔴 Q9. Why is Outbound Quantity multiplied by `-1` in the reporting measure?

A. To display outbound magnitude as a positive number for easier comparison <br>
B. To convert inventory to revenue <br>
C. To activate the Date relationship <br>
D. To count batches <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. To display outbound magnitude as a positive number for easier comparison**

**Explanation:** The source stores outbound quantities as negative values, so reversing the sign makes Inbound vs Outbound comparison easier to read.

</details>

### 🔴 Q10. Which visual is best for exact Product × Warehouse inventory validation?

A. Matrix <br>
B. Card only <br>
C. Donut Chart only <br>
D. Gauge only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Matrix**

**Explanation:** A Matrix allows exact inventory and expiry measures to be inspected across Product and Warehouse dimensions.

</details>

### 🔴 Q11. What is the active Date relationship for `FactInventorySnapshot`?

A. `SnapshotDateKey` <br>
B. `ExpiryDateKey` <br>
C. `ReleaseDateKey` <br>
D. No Date relationship <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. `SnapshotDateKey`**

**Explanation:** Snapshot Date is the default business date for the inventory-balance fact; Expiry Date is an alternate inactive date role.

</details>

### 🔴 Q12. What is the main deliverable of Section 08?

A. Inventory & Expiry Analysis dashboard page <br>
B. A new database server <br>
C. A security-role deployment <br>
D. An unrelated Excel macro <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Inventory & Expiry Analysis dashboard page**

**Explanation:** The session applies inventory, expiry, warehouse, and movement measures to a validated reporting page.

</details>

---

### ➡️ Next Session

**Section 09 — Pharma Analytics III: Quality, Deviations and Downtime**

Learners will analyze **quality-test performance, batch deviations, downtime, and operational quality patterns** using the Nirvaan Pharma Ltd model.
