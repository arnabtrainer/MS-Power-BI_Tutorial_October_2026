# Section 01 — Power BI Foundations and Data Gathering

**Day:** 1 — Pre-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious training company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Understand the Power BI workflow: **Get Data → Transform → Model → Analyze → Visualize → Publish**.
- 🎯 Navigate the key areas of **Power BI Desktop**.
- 🎯 Use **Enter Data** for small manually created tables.
- 🎯 Connect to common file, database, folder, PDF, and web sources.
- 🎯 Use **Navigator** and choose between **Load** and **Transform Data**.
- 🎯 Recognize structured and semi-structured data sources.

---

## 🗂️ Resources Used

### Primary Classwork

- 🗂️ `Classwork Files/ClassWork-1 (Data Sources).pbix`

### Repository Data Sources

- 🗂️ `DataSources/Revenue.xlsx`
- 🗂️ `DataSources/SuperMarketSales.csv`
- 🗂️ `DataSources/SMSSpamCollection.tsv`
- 🗂️ `DataSources/iris.json`
- 🗂️ `DataSources/food.xml`
- 🗂️ `DataSources/iris.pdf`
- 🗂️ `DataSources/MyEmployee.accdb`
- 🗂️ `DataSources/MyEmpDB.html`
- 🗂️ `DataSources/IrisData/` — multiple CSV files

### Nirvaan Pharma Ltd Dataset — Preview Only

- 🗂️ `NirvaanPharma_DW.xlsx`

### Web Sources

- 🌐 **Web PDF:**  
  `https://racemedia1.s3.ap-south-1.amazonaws.com/wp-content/uploads/20240103171943/Countries-Capitals.pdf`

- 🌐 **Web Portal 1:**  
  `https://worldpopulationreview.com/countries`

- 🌐 **Web Portal 2:**  
  `https://www.contextures.com/xlsampledata01.html`

---

## 📚 Data Gathering Coverage

This session demonstrates **8 common file/source formats** plus **Enter Data, Folder, and Web acquisition**.

| # | Source | Example | Connector / Method | Delivery |
|---|---|---|---|---|
| 1 | Enter Data | Manual lookup table | **Home → Enter Data** | 💻 Guided |
| 2 | Excel `.xlsx` | `Revenue.xlsx` | **Get Data → Excel Workbook** | 💻 Guided |
| 3 | CSV `.csv` | `SuperMarketSales.csv` | **Get Data → Text/CSV** | 💻 Guided |
| 4 | TSV `.tsv` | `SMSSpamCollection.tsv` | **Get Data → Text/CSV** | 🧑‍🏫 Demo |
| 5 | JSON `.json` | `iris.json` | **Get Data → JSON** | 💻 Guided |
| 6 | XML `.xml` | `food.xml` | **Get Data → XML** | 🧑‍🏫 Demo |
| 7 | PDF `.pdf` | `iris.pdf` | **Get Data → PDF** | 🧑‍🏫 Demo |
| 8 | Access `.accdb` | `MyEmployee.accdb` | **Get Data → Access Database** | 🧑‍🏫 Demo |
| 9 | HTML `.html` | `MyEmpDB.html` | HTML/Web example | 🧑‍🏫 Demo |
| 10 | Folder | `IrisData/` | **Get Data → Folder** | 💻 Guided |
| 11 | Web PDF | Countries-Capitals PDF | **Get Data → Web** | 🧑‍🏫 Demo |
| 12 | Web Portal | World Population Review | **Get Data → Web** | 🧑‍🏫 Demo |
| 13 | Web Portal | Contextures Sample Data | **Get Data → Web** | 🧑‍🏫 Demo |

> 💡 **Clarification:** Folder and Web are acquisition methods, not file formats. A Web source may expose HTML, PDF, CSV, JSON, or another structured source.

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:20 | 📚 Power BI overview, workflow and interface |
| 00:20–00:35 | 💻 Enter Data, Get Data, Navigator, Load vs Transform Data |
| 00:35–01:25 | 🧑‍🏫 Excel, CSV, TSV, JSON, XML |
| 01:25–01:55 | 🧑‍🏫 Local PDF, Access and HTML |
| 01:55–02:25 | 🌐 Web PDF and Web Portal demonstrations |
| 02:25–02:40 | 💻 Folder connector and learner practice |
| 02:40–02:50 | 🗂️ `NirvaanPharma_DW.xlsx` preview |
| 02:50–03:00 | 🔁 Recap and quick knowledge check |

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
- 🧑‍🏫 **Home → Enter Data**
- 🧑‍🏫 Report View
- 🧑‍🏫 Data/Table View
- 🧑‍🏫 Model View
- 🧑‍🏫 **Transform Data** → Power Query Editor

> 🖼️ **Image Placeholder S01-01:** Power BI Desktop with **Get Data**, **Enter Data**, Report View, Data View and Model View highlighted.  
> **Planned file:** `images/S01_01_PowerBI_Desktop_Interface.png`

---

## 💻 2. Enter Data Utility

- 🛠️ **Path:** Home → Enter Data
- 💻 Create a small manual lookup table.

| PlantCode | PlantName |
|---|---|
| P01 | Kolkata Plant |
| P02 | Pune Plant |
| P03 | Hyderabad Plant |

- 🛠️ Rename the table as `ManualPlantLookup`.
- 🛠️ Select **Load**.

✅ **Outcome:** Learners understand how to create small manual tables directly inside Power BI.

⚠️ **Use Enter Data only for small and relatively static tables.** Do not use it as a replacement for large or frequently changing source systems.

> 🖼️ **Image Placeholder S01-02:** Enter Data window with the sample plant lookup table.  
> **Planned file:** `images/S01_02_Enter_Data.png`

---

## 🧑‍🏫 3. Get Data, Navigator and Load Options

Demonstrate:

- 🛠️ Selecting the correct connector.
- 🛠️ Browsing to the source.
- 🛠️ Previewing tables/sheets in **Navigator**.
- 🛠️ **Load** versus **Transform Data**.
- 🛠️ Checking headers, delimiters and detected data types.

> 🖼️ **Image Placeholder S01-03:** Navigator showing source preview and **Load / Transform Data**.  
> **Planned file:** `images/S01_03_Navigator_Load_Transform.png`

---

## 🧑‍🏫 4. File-Based Connectivity Demonstrations

### Demo 1 — Excel Workbook

- 🗂️ **Source:** `DataSources/Revenue.xlsx`
- 🛠️ **Path:** Home → Get Data → Excel Workbook
- 🧑‍🏫 Preview sheets/tables in Navigator.
- ✅ **Outcome:** Understand Excel workbook navigation and table selection.

### Demo 2 — CSV

- 🗂️ **Source:** `DataSources/SuperMarketSales.csv`
- 🛠️ **Path:** Home → Get Data → Text/CSV
- 🧑‍🏫 Check delimiter, headers and detected data types.
- ✅ **Outcome:** Understand flat-file import.

### Demo 3 — TSV

- 🗂️ **Source:** `DataSources/SMSSpamCollection.tsv`
- 🛠️ **Path:** Home → Get Data → Text/CSV
- 🧑‍🏫 Show that the Text/CSV connector can read tab-delimited data.
- ✅ **Outcome:** Understand the difference between file extension and delimiter.

### Demo 4 — JSON

- 🗂️ **Source:** `DataSources/iris.json`
- 🛠️ **Path:** Home → Get Data → JSON
- 🧑‍🏫 Show List/Record structures and expand them into columns.
- ✅ **Outcome:** Understand basic semi-structured data expansion.

> 🖼️ **Image Placeholder S01-04:** JSON List/Record structure before and after expansion.  
> **Planned file:** `images/S01_04_JSON_Expansion.png`

### Demo 5 — XML

- 🗂️ **Source:** `DataSources/food.xml`
- 🛠️ **Path:** Home → Get Data → XML
- 🧑‍🏫 Inspect nested content and expand required elements.
- ✅ **Outcome:** Understand how hierarchical XML data becomes tabular.

### Demo 6 — Local PDF

- 🗂️ **Source:** `DataSources/iris.pdf`
- 🛠️ **Path:** Home → Get Data → PDF
- 🧑‍🏫 Identify extractable tables/pages in Navigator.
- ⚠️ Validate imported rows and columns because PDF extraction depends on document structure.
- ✅ **Outcome:** Understand local PDF ingestion and its limitations.

### Demo 7 — Microsoft Access

- 🗂️ **Source:** `DataSources/MyEmployee.accdb`
- 🛠️ **Path:** Home → Get Data → Access Database
- 🧑‍🏫 Select and preview a table.
- ⚠️ Verify the required Microsoft Access database driver before training.
- ✅ **Outcome:** Understand database-file connectivity.

### Demo 8 — Local HTML

- 🗂️ **Source:** `DataSources/MyEmpDB.html`
- 🧑‍🏫 Use it to explain how tabular HTML content may be imported through Web-based acquisition.
- ✅ **Outcome:** Understand HTML as a possible tabular source.

---

## 🌐 5. Web-Based Connectivity Demonstrations

### Demo 9 — Web PDF

- 🌐 **Source:**  
  `https://racemedia1.s3.ap-south-1.amazonaws.com/wp-content/uploads/20240103171943/Countries-Capitals.pdf`
- 🛠️ **Path:** Home → Get Data → Web
- 🧑‍🏫 Paste the PDF URL and inspect available tables/pages.
- ⚠️ Web access must be available in the training environment.
- ✅ **Outcome:** Understand how Power BI can access a PDF directly from a web URL.

### Demo 10 — Web Portal: World Population Review

- 🌐 **Source:**  
  `https://worldpopulationreview.com/countries`
- 🛠️ **Path:** Home → Get Data → Web
- 🧑‍🏫 Inspect detected web tables or structured content.
- ⚠️ Web-page structure may change over time.
- ✅ **Outcome:** Understand extraction of web-hosted tabular data.

### Demo 11 — Web Portal: Contextures Sample Data

- 🌐 **Source:**  
  `https://www.contextures.com/xlsampledata01.html`
- 🛠️ **Path:** Home → Get Data → Web
- 🧑‍🏫 Inspect available tables and select suitable tabular content.
- ✅ **Outcome:** Reinforce web-table acquisition using another public portal.

> 🖼️ **Image Placeholder S01-05:** Web Navigator showing detected tables from a public web page.  
> **Planned file:** `images/S01_05_Web_Navigator.png`

---

## 💻 6. Folder Import

- 🗂️ **Source:** `DataSources/IrisData/`
- 🛠️ **Path:** Home → Get Data → Folder
- 🧑‍🏫 Show the file listing.
- 🛠️ Select **Combine & Transform Data**.
- 💡 Explain that files being combined should have compatible structures.
- ✅ **Outcome:** Understand scalable ingestion of recurring files.

> 🖼️ **Image Placeholder S01-06:** Folder connector showing multiple files and **Combine & Transform Data**.  
> **Planned file:** `images/S01_06_Folder_Combine.png`

---

## 🗂️ 7. Nirvaan Pharma Ltd Dataset Preview

- 🗂️ **Source:** `NirvaanPharma_DW.xlsx`
- 🛠️ **Path:** Home → Get Data → Excel Workbook
- 🧑‍🏫 Open Navigator and show the multiple related business tables.
- 📚 Briefly identify examples such as Product, Plant, Batch, Production, Inventory and Quality.
- ⚠️ Do **not** build relationships or measures yet.
- ✅ **Outcome:** Learners recognize the main pharmaceutical case-study dataset that will be used progressively later.

> 🖼️ **Image Placeholder S01-07:** Navigator showing selected `NirvaanPharma_DW.xlsx` tables.  
> **Planned file:** `images/S01_07_NirvaanPharma_Navigator.png`

---

## 💻 8. Guided Hands-on Exercise

Learners import or create:

- 💻 A small lookup table using **Enter Data**.
- 💻 `Revenue.xlsx`
- 💻 `SuperMarketSales.csv`
- 💻 `iris.json`
- 💻 `IrisData/` using the Folder connector.

### ✅ Validation

Learners should be able to:

- ✅ Select the correct connector.
- ✅ Preview data before loading.
- ✅ Choose between **Load** and **Transform Data**.
- ✅ Recognize flat, hierarchical and semi-structured sources.
- ✅ Explain when Folder import and Enter Data are useful.

---

## 💡 Trainer Guidelines

- 💡 Keep the session focused on **data gathering**, not deep transformation.
- 💡 Demonstrate many connectors, but make learners practice only the most reusable ones.
- 💡 Prefer repository files when internet access is uncertain.
- ⚠️ Test all three web URLs before class.
- ⚠️ Verify the Access driver before delivery.
- ⚠️ Web sources can change; always keep a local fallback.
- ⚠️ Treat `NirvaanPharma_DW.xlsx` only as fictitious **Nirvaan Pharma Ltd** training data.
- 🖼️ Capture actual screenshots only after the section content and UI flow are finalized.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 The basic Power BI workflow.
- 🔁 How **Enter Data** differs from external data connectors.
- 🔁 How to connect to common file and database sources.
- 🔁 How to connect to PDF and Web sources.
- 🔁 How Folder ingestion supports recurring files.
- 🔁 Why data should be previewed before loading.

---

## 📝 Knowledge Check — 12 MCQs

### Q1. What is the main purpose of Power BI's Get Data feature?

A. To create operating system users <br>
B. To connect Power BI to external data sources <br>
C. To create presentation slides <br>
D. To install database servers <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. To connect Power BI to external data sources**

**Explanation:** Get Data provides connectors for files, databases, web sources and other data platforms.

</details>

### Q2. When is the Enter Data utility most appropriate?

A. For loading millions of frequently changing records <br>
B. For creating small manually maintained tables <br>
C. For replacing all database systems <br>
D. For connecting to web portals <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. For creating small manually maintained tables**

**Explanation:** Enter Data is useful for small static tables such as mappings, categories, targets or lookup values.

</details>

### Q3. Which Power BI connector is normally used for a `.csv` file?

A. XML <br>
B. Text/CSV <br>
C. PDF <br>
D. Access Database <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Text/CSV**

**Explanation:** The Text/CSV connector is designed for delimited text files such as CSV and TSV.

</details>

### Q4. Which connector can also be used for a `.tsv` file?

A. Text/CSV <br>
B. Excel Workbook <br>
C. PDF <br>
D. SQL Server <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Text/CSV**

**Explanation:** TSV is a tab-delimited text format, and Power BI's Text/CSV connector can interpret its delimiter.

</details>

### Q5. Why may JSON data require expansion after import?

A. JSON frequently contains nested Lists and Records <br>
B. JSON always contains images <br>
C. JSON cannot contain text <br>
D. JSON can only contain one column <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. JSON frequently contains nested Lists and Records**

**Explanation:** JSON is semi-structured and commonly contains nested structures that must be expanded into tabular columns.

</details>

### Q6. Which file is used for the XML demonstration in this session?

A. `iris.xml` <br>
B. `food.xml` <br>
C. `Revenue.xml` <br>
D. `MyEmployee.xml` <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. `food.xml`**

**Explanation:** `DataSources/food.xml` is the selected XML source for demonstrating hierarchical XML import.

</details>

### Q7. What should be checked carefully after importing a PDF?

A. Monitor brightness <br>
B. Extracted rows, columns and table structure <br>
C. Windows wallpaper <br>
D. Keyboard settings <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Extracted rows, columns and table structure**

**Explanation:** PDF extraction depends on the document layout, so the resulting table must be validated before use.

</details>

### Q8. What does the Navigator window primarily help users do?

A. Install Power BI <br>
B. Preview and select available tables or objects <br>
C. Create Windows folders <br>
D. Write DAX measures automatically <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Preview and select available tables or objects**

**Explanation:** Navigator displays the tables, sheets or other objects detected in a selected data source before loading.

</details>

### Q9. What is the main difference between Load and Transform Data?

A. Load imports the selected data directly, while Transform Data opens Power Query first <br>
B. Load deletes data, while Transform Data restores it <br>
C. Load creates charts, while Transform Data creates dashboards <br>
D. There is no difference <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Load imports the selected data directly, while Transform Data opens Power Query first**

**Explanation:** Transform Data allows the data to be inspected and prepared before it is loaded into the model.

</details>

### Q10. What is the main advantage of the Folder connector?

A. It changes the Windows desktop theme <br>
B. It can combine multiple similarly structured files <br>
C. It creates PowerPoint slides <br>
D. It converts DAX to SQL <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. It can combine multiple similarly structured files**

**Explanation:** The Folder connector is useful when recurring files with compatible structures need to be consolidated.

</details>

### Q11. Which method can be used to access a PDF directly from a web URL?

A. Home → Enter Data <br>
B. Home → Get Data → Web <br>
C. Home → New Measure <br>
D. Home → Publish <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. Home → Get Data → Web**

**Explanation:** A web-hosted PDF can be accessed by providing its URL through the Web connector.

</details>

### Q12. What should you consider first when selecting a data connector in Power BI?

A. The color theme of the report <br>
B. The type and location of the data source <br>
C. The number of visuals on the report page <br>
D. The size of the Power BI logo <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: B. The type and location of the data source**

**Explanation:** The correct connector depends mainly on where the data is stored and in what format, such as Excel, CSV, database, folder, PDF, or web source.

</details>

---

### ➡️ Next Session

**Section 02 — Power Query: Data Cleaning and Preparation**

The imported data will be profiled, cleaned and transformed before modelling.
