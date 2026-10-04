# Section 02 — Power Query: Data Cleaning and Preparation

**Day:** 1 — Post-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious training company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Open and navigate **Power Query Editor**.
- 🎯 Profile data for nulls, errors, duplicates, and inconsistent values.
- 🎯 Apply common cleaning and transformation steps.
- 🎯 Assign correct data types and rename/remove columns.
- 🎯 Create simple conditional columns.
- 🎯 Understand **Applied Steps** and finish with **Close & Apply**.

---

## 🗂️ Resources Used

### Primary Classwork

- 🗂️ `Classwork Files/ClassWork-2 (Power Query).pbix`

### Primary Practice Dataset

- 🗂️ `DashboardResources/HR_Analytics_Dataset.csv`
  - **Rows:** 1,480
  - **Columns:** 36

### Later Application

- 🗂️ `NirvaanPharma_DW.xlsx`
- 💡 The same cleaning principles will later be applied to the **Nirvaan Pharma Ltd** case-study tables.

---

## 📚 Power Query Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Power Query Editor | Interface and Query Settings | 🧑‍🏫 Demo |
| 2 | Data profiling | Column Quality, Distribution, Profile | 💻 Guided |
| 3 | Data types | Detect and correct types | 💻 Guided |
| 4 | Null values | Identify and decide treatment | 💻 Guided |
| 5 | Duplicate checks | EmpID vs exact-row duplicates | 💻 Guided |
| 6 | Replace Values | Standardize `BusinessTravel` | 💻 Guided |
| 7 | Remove/keep columns | Remove unnecessary fields | 🧑‍🏫 Demo |
| 8 | Filter/sort rows | Basic row-level preparation | 💻 Guided |
| 9 | Conditional columns | Attrition/Age/Salary categories | 💻 Guided |
| 10 | Applied Steps | Review, reorder, rename, delete steps | 💻 Guided |
| 11 | Close & Apply | Load cleaned result to model | 💻 Guided |

> 💡 **Scope:** Merge, Append, Pivot, Unpivot, parameters, and deeper M-language work are covered in **Section 03**.

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:20 | 📚 Power Query purpose, interface and workflow |
| 00:20–00:45 | 💻 Data profiling and data-type inspection |
| 00:45–01:15 | 💻 Null-value and duplicate analysis |
| 01:15–01:40 | 💻 Replace values, rename/remove columns, filter rows |
| 01:40–02:15 | 💻 Conditional columns and transformation sequence |
| 02:15–02:35 | 🛠️ Applied Steps, Query Settings and Close & Apply |
| 02:35–02:50 | 💻 Independent cleaning challenge |
| 02:50–03:00 | 🔁 Recap and knowledge check |

---

## 📚 1. What is Power Query?

Power Query is the data-preparation layer used to connect, inspect, clean, reshape, and combine data before analysis.

### 🧑‍🏫 Open Power Query Editor

- 🛠️ **Path:** Home → Transform Data
- 🧑‍🏫 Identify:
  - Queries pane
  - Data preview
  - Ribbon
  - Formula bar
  - Query Settings
  - Applied Steps

---

<img width="1624" height="969" alt="image" src="https://github.com/user-attachments/assets/451e4256-c3bd-4105-b341-97a0ab6c08b7" />

---

### 💡 Key Principle

Every transformation normally becomes an **Applied Step**.  
Steps are executed in sequence, so their order matters.

---

## 💻 2. Load the Practice Dataset

- 🗂️ **Source:** `DashboardResources/HR_Analytics_Dataset.csv`
- 🛠️ **Path:** Home → Get Data → Text/CSV
- 🛠️ Select **Transform Data**.
- 🛠️ Rename the query, if required, to `HR_Analytics_Dataset`.

### ✅ Initial Validation

Confirm:

- ✅ **1,480 rows**
- ✅ **36 columns**
- ✅ Column headers are correctly detected.

---

## 💻 3. Data Profiling

### Enable Profiling Tools

- 🛠️ Power Query Editor → **View**
- ☑️ Enable **Column Quality**
- ☑️ Enable **Column Distribution**
- ☑️ Enable **Column Profile**

Use these tools to inspect:

- 📚 Valid values
- 📚 Empty/null values
- 📚 Errors
- 📚 Distinct and unique values
- 📚 Value distribution

> 🖼️ **Image Placeholder S02-02:** Column Quality, Column Distribution and Column Profile enabled for the HR dataset.  
> **Planned file:** `images/S02_02_Data_Profiling.png`

> ⚠️ **Trainer Note:** If profiling is based on the top 1,000 rows, switch to profiling the **entire dataset** before drawing conclusions.

---

## 💻 4. Null-Value Analysis

Inspect `YearsWithCurrManager`.

### Dataset Finding

- 📚 **57 null values**
- 📚 Approximately **3.85%** of the 1,480 rows

### 💡 Teaching Point

Do **not** teach a fixed rule such as:

> “Delete every column containing around 4% null values.”

Instead ask:

- 💡 Is the column important to the analysis?
- 💡 Can missing values be interpreted or replaced safely?
- 💡 Would removing the column lose useful information?

For this exercise, demonstrate the available choices:

- 🛠️ Keep the column
- 🛠️ Remove the column
- 🛠️ Replace values when business rules justify it

⚠️ Do not invent replacement values without a valid rule.

---

## 💻 5. Duplicate Analysis

### Step A — Check Repeated Employee IDs

- 🛠️ Select `EmpID`.
- 🛠️ Use **Group By** with Row Count or inspect duplicate values.
- 📚 The dataset contains **10 EmpIDs with repeated records**.

### Step B — Check Exact Duplicate Rows

- 🛠️ Return to the original query.
- 🛠️ Select all columns.
- 🛠️ Choose **Remove Rows → Remove Duplicates**.

### ✅ Expected Result

- ✅ Rows before: **1,480**
- ✅ Exact duplicate rows removed: **7**
- ✅ Rows after: **1,473**

> 💡 **Important:** A repeated business key such as `EmpID` does not automatically mean that the entire row is an exact duplicate.

---

## 💻 6. Standardize Inconsistent Values

Inspect `BusinessTravel`.

The source contains:

- `Travel_Rarely`
- `Travel_Frequently`
- `Non-Travel`
- `TravelRarely`

### Cleaning Step

- 🛠️ Select `BusinessTravel`.
- 🛠️ Transform → **Replace Values**
- Replace:
  - `TravelRarely`
  - with `Travel_Rarely`

✅ **Outcome:** The category naming becomes consistent.

---

## 🧑‍🏫 7. Remove Unnecessary or Low-Value Columns

Demonstrate **Remove Columns** and **Choose Columns**.

Examples of constant fields in this dataset include:

- `EmployeeCount`
- `Over18`
- `StandardHours`

💡 These fields may be removed when they add no analytical value.

⚠️ Column removal should be based on the reporting requirement, not only on technical convenience.

---

## 💻 8. Correct Data Types

- 🛠️ Select relevant columns.
- 🛠️ Transform → **Detect Data Type**, then verify manually.
- 🛠️ Correct any unsuitable types.

Examples:

- `Age` → Whole Number
- `MonthlyIncome` → Whole Number
- `Attrition` → Text
- `BusinessTravel` → Text

### 💡 Best Practice

Assign correct types **before** calculations, joins, or date-based analysis.

---

## 💻 9. Filter, Sort, Rename and Reorder

Demonstrate:

- 🛠️ Filtering rows
- 🛠️ Sorting values
- 🛠️ Renaming a column
- 🛠️ Reordering columns
- 🛠️ Removing unnecessary columns

💡 Use these operations to demonstrate how every action appears under **Applied Steps**.

---

## 💻 10. Create Conditional Columns

For this Power Query session, create the following as transformation exercises.

### A. AttritionFlag

- 🛠️ Add Column → Conditional Column
- If `Attrition = "Yes"` → `1`
- Else → `0`

### B. AgeGroup

Use:

- `18–25`
- `26–35`
- `36–45`
- `46–55`
- `55+`

### C. SalarySlab

Use:

- `Upto 5K`
- `5K+ to 10K`
- `10K+ to 15K`
- `15K+`

💡 Later, learners will compare **Power Query columns** with **DAX calculated columns** and understand when each approach is appropriate.

---

## 🛠️ 11. Applied Steps and Query Settings

Review the transformation sequence.

Typical steps may include:

1. 🛠️ Source
2. 🛠️ Promoted Headers
3. 🛠️ Changed Type
4. 🛠️ Removed Duplicates
5. 🛠️ Replaced Value
6. 🛠️ Removed Columns
7. 🛠️ Added Conditional Columns

Demonstrate:

- 🛠️ Renaming a step
- 🛠️ Deleting a step
- 🛠️ Editing an existing step
- 🛠️ Understanding why later steps may depend on earlier steps

> 🖼️ **Image Placeholder S02-03:** Query Settings showing a clean sequence of **Applied Steps** for the HR dataset.  
> **Planned file:** `images/S02_03_Applied_Steps.png`

---

## 💻 12. Close & Apply

- 🛠️ Home → **Close & Apply**
- 🧑‍🏫 Return to Power BI Desktop.
- ✅ Confirm that the cleaned table is loaded.

### ✅ Final Validation

Check:

- ✅ Row count after exact duplicate removal: **1,473**
- ✅ `TravelRarely` has been standardized.
- ✅ Data types are appropriate.
- ✅ Required conditional columns are available.
- ✅ Unnecessary transformations are not present.

---

## 💻 Guided Hands-on Challenge

Without trainer assistance, learners should:

1. 💻 Load `HR_Analytics_Dataset.csv`.
2. 💻 Enable data profiling.
3. 💻 Find the null values in `YearsWithCurrManager`.
4. 💻 Identify repeated `EmpID` values.
5. 💻 Remove exact duplicate rows.
6. 💻 Standardize `BusinessTravel`.
7. 💻 Verify data types.
8. 💻 Create `AttritionFlag`.
9. 💻 Create either `AgeGroup` or `SalarySlab`.
10. 💻 Close & Apply.

### ✅ Expected Outcome

A clean, analysis-ready HR table with **1,473 rows** after exact duplicate removal.

---

## 💡 Trainer Guidelines

- 💡 Explain the **reason** for every transformation, not only the menu path.
- 💡 Keep the original source unchanged; perform cleaning through Power Query steps.
- 💡 Emphasize the difference between **duplicate key values** and **exact duplicate rows**.
- 💡 Avoid automatic null-handling rules without business context.
- 💡 Use descriptive query and step names where useful.
- ⚠️ Do not introduce Merge, Append, Pivot, or Unpivot in depth here; reserve them for Section 03.
- ⚠️ Do not start DAX calculations in this session.
- 🖼️ Use screenshots only for concepts that benefit from a static visual; routine transformations can be demonstrated live.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 The role of Power Query in data preparation.
- 🔁 How profiling helps identify data-quality issues.
- 🔁 How to handle nulls and duplicates carefully.
- 🔁 How to standardize inconsistent values.
- 🔁 How to assign data types and create conditional columns.
- 🔁 How Applied Steps create a repeatable transformation process.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What is the primary role of Power Query in Power BI?

A. To design presentation slides <br>
B. To clean and transform data before analysis <br>
C. To manage Windows users <br>
D. To create database servers <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. To clean and transform data before analysis**

**Explanation:** Power Query is used to connect, inspect, clean, reshape, and prepare data before it is loaded for analysis.

</details>

### 🔴 Q2. Where can you open Power Query Editor from Power BI Desktop?

A. Home → Transform Data <br>
B. Insert → Text Box <br>
C. Modeling → New Measure <br>
D. View → Bookmarks <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Home → Transform Data**

**Explanation:** The Transform Data command opens Power Query Editor.

</details>

### 🔴 Q3. Which feature helps identify valid, empty, and error values in a column?

A. Column Quality <br>
B. Page Navigator <br>
C. Drill Through <br>
D. Bookmark Navigator <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Column Quality**

**Explanation:** Column Quality displays the proportion of valid, error, and empty values in a column.

</details>

### 🔴 Q4. What should be done before deciding to remove a column containing null values?

A. Always delete it immediately <br>
B. Consider its business importance and the meaning of the missing values <br>
C. Convert every null to zero <br>
D. Sort the report alphabetically <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Consider its business importance and the meaning of the missing values**

**Explanation:** Null handling should depend on the analytical requirement and valid business rules rather than a fixed percentage threshold.

</details>

### 🔴 Q5. Why is a repeated EmpID not necessarily an exact duplicate row?

A. Other column values may be different <br>
B. EmpID can only contain dates <br>
C. Power Query ignores EmpID <br>
D. Duplicate rows never occur in CSV files <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Other column values may be different**

**Explanation:** Two rows may share the same business key while containing different values in other columns.

</details>

### 🔴 Q6. How many rows remain after exact duplicate rows are removed from the practice HR dataset?

A. 1,480 <br>
B. 1,473 <br>
C. 1,500 <br>
D. 1,470 <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. 1,473**

**Explanation:** The source has 1,480 rows and seven exact duplicate rows are removed.

</details>

### 🔴 Q7. Which Power Query operation is used to change `TravelRarely` to `Travel_Rarely`?

A. Replace Values <br>
B. Append Queries <br>
C. Pivot Column <br>
D. Group By only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Replace Values**

**Explanation:** Replace Values is used to standardize inconsistent text values within a column.

</details>

### 🔴 Q8. Why are correct data types important?

A. They support correct calculations, relationships, and analysis <br>
B. They only change the report background <br>
C. They increase the number of pages automatically <br>
D. They remove all null values automatically <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. They support correct calculations, relationships, and analysis**

**Explanation:** Power BI operations depend on columns being stored with suitable data types such as number, text, or date.

</details>

### 🔴 Q9. Where are Power Query transformations recorded?

A. Applied Steps <br>
B. Visualizations pane <br>
C. Report page tabs <br>
D. Status bar <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Applied Steps**

**Explanation:** Each transformation is recorded as a step in Query Settings and is normally executed in sequence.

</details>

### 🔴 Q10. What is a suitable use of a Conditional Column?

A. Creating categories based on existing column values <br>
B. Installing Power BI Desktop <br>
C. Publishing a report to the Service <br>
D. Configuring Windows security <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Creating categories based on existing column values**

**Explanation:** Conditional Columns can derive values such as age groups, salary bands, or flags using defined rules.

</details>

### 🔴 Q11. What does Close & Apply do?

A. Discards the source file permanently <br>
B. Applies Power Query transformations and returns to Power BI Desktop <br>
C. Creates a Power BI Service workspace <br>
D. Deletes all Applied Steps <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Applies Power Query transformations and returns to Power BI Desktop**

**Explanation:** Close & Apply processes the query steps and loads the prepared result into the Power BI model.

</details>

### 🔴 Q12. Which principle is most appropriate when cleaning business data?

A. Apply every available transformation <br>
B. Transform data only when there is a valid analytical or business reason <br>
C. Replace every null with zero <br>
D. Remove every text column <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Transform data only when there is a valid analytical or business reason**

**Explanation:** Good data preparation preserves useful information and applies transformations that support the intended analysis.

</details>

---

### ➡️ Next Session

**Section 03 — Advanced Power Query and M Fundamentals**

Learners will extend Power Query skills with **Append, Merge, Pivot, Unpivot, Folder-based consolidation, query dependencies, parameters, and introductory M language**.
