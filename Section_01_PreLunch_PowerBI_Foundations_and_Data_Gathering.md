# Section 01 — Power BI Foundations and Data Gathering

**Day:** 1 — Pre-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious training company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Understand the Power BI workflow: **Get Data → Transform → Model → Analyze → Visualize → Publish**.
- 🎯 Navigate the essential areas of **Power BI Desktop**.
- 🎯 Connect to common file, database, folder, and web sources.
- 🎯 Use **Navigator** and decide between **Load** and **Transform Data**.
- 🎯 Recognize which sources require additional inspection before loading.

---

## 🗂️ Resources Used

### Primary Classwork

- 🗂️ `Classwork Files/ClassWork-1 (Data Sources).pbix`

### Repository Data Sources

- 🗂️ `DataSources/Revenue.xlsx`
- 🗂️ `DataSources/SuperMarketSales.csv`
- 🗂️ `DataSources/SMSSpamCollection.tsv`
- 🗂️ `DataSources/iris.json`
- 🗂️ `DataSources/departureBoard.xml`
- 🗂️ `DataSources/iris.pdf`
- 🗂️ `DataSources/MyEmployee.accdb`
- 🗂️ `DataSources/MyEmpDB.html`
- 🗂️ `DataSources/IrisData/` — multiple CSV files

### Nirvaan Pharma Ltd Dataset — Preview Only

- 🗂️ `NirvaanPharma_DW.xlsx`

### Live Web Demonstration

- 🌐 `https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population`
- ⚠️ Use the local repository material if external web access is restricted.

---

## 📚 Data Gathering Coverage

This session demonstrates **8 common source formats/types** plus **Folder** and **Web** acquisition.

| # | Source | Example | Connector / Method | Delivery |
|---|---|---|---|---|
| 1 | Excel `.xlsx` | `Revenue.xlsx` | **Get Data → Excel Workbook** | 💻 Guided |
| 2 | CSV `.csv` | `SuperMarketSales.csv` | **Get Data → Text/CSV** | 💻 Guided |
| 3 | TSV `.tsv` | `SMSSpamCollection.tsv` | **Get Data → Text/CSV** | 🧑‍🏫 Demo |
| 4 | JSON `.json` | `iris.json` | **Get Data → JSON** | 💻 Guided |
| 5 | XML `.xml` | `departureBoard.xml` | **Get Data → XML** | 🧑‍🏫 Demo |
| 6 | PDF `.pdf` | `iris.pdf` | **Get Data → PDF** | 🧑‍🏫 Demo |
| 7 | Access `.accdb` | `MyEmployee.accdb` | **Get Data → Access Database** | 🧑‍🏫 Demo |
| 8 | HTML `.html` | `MyEmpDB.html` | HTML/Web example | 🧑‍🏫 Demo |
| 9 | Folder | `IrisData/` | **Get Data → Folder** | 💻 Guided |
| 10 | Web portal | Wikipedia page | **Get Data → Web** | 🧑‍🏫 Demo |

> 💡 **Clarification:** Folder and Web are acquisition methods, not file formats. A Folder can combine many files; a Web source may expose HTML or other structured content.

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:25 | 📚 Power BI overview, workflow and interface |
| 00:25–00:40 | 🧑‍🏫 Get Data, Navigator, Load vs Transform Data |
| 00:40–01:35 | 🧑‍🏫 Excel, CSV, TSV, JSON, XML |
| 01:35–02:05 | 🧑‍🏫 PDF, Access, HTML/Web |
| 02:05–02:30 | 💻 Folder import and learner practice |
| 02:30–02:45 | 🗂️ `NirvaanPharma_DW.xlsx` preview |
| 02:45–03:00 | 🔁 Recap, validation and Q&A |

---

## 📚 1. Power BI Foundations

Introduce only the essentials:

- 📚 **Power BI Desktop** — connect, prepare, model and report.
- 📚 **Power Query** — data cleaning and transformation.
- 📚 **Semantic Model** — tables, relationships and calculations.
- 📚 **DAX** — analytical calculations.
- 📚 **Power BI Service** — publishing, refresh, sharing and security; covered later.

### 🧑‍🏫 Interface Demonstration

Show:

- 🧑‍🏫 **Home → Get Data**
- 🧑‍🏫 Report View
- 🧑‍🏫 Data/Table View
- 🧑‍🏫 Model View
- 🧑‍🏫 **Transform Data** → Power Query Editor

> 🖼️ **Image Placeholder S01-01:** Power BI Desktop with **Get Data**, Report View, Data View and Model View highlighted.  
> **Planned file:** `images/S01_01_PowerBI_Desktop_Interface.png`

⚠️ Do not teach detailed modelling, DAX or visualization here; they have dedicated sessions.

---

## 🧑‍🏫 2. Get Data, Navigator and Load Options

Demonstrate:

- 🛠️ Selecting a connector.
- 🛠️ Browsing to the source.
- 🛠️ Previewing tables/sheets in **Navigator**.
- 🛠️ **Load** versus **Transform Data**.
- 🛠️ Checking headers, delimiters and basic data types.

> 🖼️ **Image Placeholder S01-02:** Navigator window showing source preview and **Load / Transform Data** options.  
> **Planned file:** `images/S01_02_Navigator_Load_Transform.png`

---

## 🧑‍🏫 3. Connectivity Demonstrations

### Demo 1 — Excel Workbook

- 🗂️ **Source:** `DataSources/Revenue.xlsx`
- 🛠️ **Path:** Home → Get Data → Excel Workbook
- 🧑‍🏫 Preview available sheets/tables in Navigator.
- 💡 Compare **Load** with **Transform Data**.
- ✅ **Outcome:** Understand Excel workbook navigation and table selection.

---

### Demo 2 — CSV

- 🗂️ **Source:** `DataSources/SuperMarketSales.csv`
- 🛠️ **Path:** Home → Get Data → Text/CSV
- 🧑‍🏫 Check delimiter, headers and detected data types.
- ✅ **Outcome:** Understand flat-file import.

---

### Demo 3 — TSV

- 🗂️ **Source:** `DataSources/SMSSpamCollection.tsv`
- 🛠️ **Path:** Home → Get Data → Text/CSV
- 🧑‍🏫 Show that the Text/CSV connector can also read tab-delimited data.
- ✅ **Outcome:** Understand the difference between file extension and delimiter.

---

### Demo 4 — JSON

- 🗂️ **Source:** `DataSources/iris.json`
- 🛠️ **Path:** Home → Get Data → JSON
- 🧑‍🏫 Show List/Record structures and expand them into columns.
- ✅ **Outcome:** Understand basic semi-structured data expansion.

> 🖼️ **Image Placeholder S01-03:** JSON List/Record structure before and after expansion.  
> **Planned file:** `images/S01_03_JSON_Expansion.png`

---

### Demo 5 — XML

- 🗂️ **Source:** `DataSources/departureBoard.xml`
- 🛠️ **Path:** Home → Get Data → XML
- 🧑‍🏫 Inspect nested content and expand required elements.
- ✅ **Outcome:** Understand how hierarchical XML becomes tabular data.

---

### Demo 6 — PDF

- 🗂️ **Source:** `DataSources/iris.pdf`
- 🛠️ **Path:** Home → Get Data → PDF
- 🧑‍🏫 Identify extractable tables/pages in Navigator.
- ⚠️ Validate imported rows and columns because PDF extraction depends on document structure.
- ✅ **Outcome:** Understand PDF ingestion and its limitations.

---

### Demo 7 — Microsoft Access

- 🗂️ **Source:** `DataSources/MyEmployee.accdb`
- 🛠️ **Path:** Home → Get Data → Access Database
- 🧑‍🏫 Select and preview a table.
- ⚠️ Verify the required Microsoft Access database driver before training.
- ✅ **Outcome:** Understand database-file connectivity.

---

### Demo 8 — HTML / Web

- 🗂️ **Repository reference:** `DataSources/MyEmpDB.html`
- 🌐 **Live source:** `https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population`
- 🛠️ **Path:** Home → Get Data → Web
- 🧑‍🏫 Select a detected HTML table in Navigator.
- ⚠️ Live websites may change or be blocked by the client network.
- ✅ **Outcome:** Understand acquisition of tabular data from web pages.

> 🖼️ **Image Placeholder S01-04:** Web Navigator showing detected HTML tables.  
> **Planned file:** `images/S01_04_Web_Navigator.png`

---

### Demo 9 — Folder Import

- 🗂️ **Source:** `DataSources/IrisData/`
- 🛠️ **Path:** Home → Get Data → Folder
- 🧑‍🏫 Show file listing and **Combine & Transform Data**.
- 💡 Explain that files being combined should have compatible structures.
- ✅ **Outcome:** Understand scalable ingestion of recurring files.

> 🖼️ **Image Placeholder S01-05:** Folder connector showing multiple files and **Combine & Transform Data**.  
> **Planned file:** `images/S01_05_Folder_Combine.png`

---

## 🗂️ 4. Nirvaan Pharma Ltd Dataset Preview

- 🗂️ **Source:** `NirvaanPharma_DW.xlsx`
- 🛠️ **Path:** Home → Get Data → Excel Workbook
- 🧑‍🏫 Open Navigator and show the presence of multiple related business tables.
- 📚 Briefly identify examples such as Product, Plant, Batch, Production, Inventory and Quality.
- ⚠️ Do **not** build relationships or measures yet.
- ✅ **Outcome:** Learners understand the pharmaceutical case-study dataset that will be used progressively later.

> 🖼️ **Image Placeholder S01-06:** Navigator showing selected `NirvaanPharma_DW.xlsx` tables.  
> **Planned file:** `images/S01_06_NirvaanPharma_Navigator.png`

---

## 💻 5. Guided Hands-on Exercise

Learners import:

- 💻 `Revenue.xlsx`
- 💻 `SuperMarketSales.csv`
- 💻 `iris.json`
- 💻 `IrisData/` using the Folder connector

### ✅ Validation

Learners should be able to:

- ✅ Select the correct connector.
- ✅ Preview data before loading.
- ✅ Recognize delimiter or structural differences.
- ✅ Choose between **Load** and **Transform Data**.
- ✅ Explain when Folder import is useful.

---

## 💡 Trainer Guidelines

- 💡 Keep the session focused on **data gathering**, not deep transformation.
- 💡 Demonstrate many connectors but make learners practice only the most reusable ones.
- 💡 Prefer repository files so the class does not depend on internet availability.
- ⚠️ Test the Web URL and Access driver before class.
- ⚠️ Treat `NirvaanPharma_DW.xlsx` only as fictitious **Nirvaan Pharma Ltd** training data.
- 🖼️ Capture screenshots only after the section content and UI flow are finalized.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 The basic Power BI workflow.
- 🔁 How to connect to common enterprise data sources.
- 🔁 Structured versus semi-structured sources.
- 🔁 File format versus acquisition method.
- 🔁 Why data must be previewed before loading.

### ➡️ Next Session

**Section 02 — Power Query: Data Cleaning and Preparation**

The imported data will be profiled, cleaned and transformed before modelling.
