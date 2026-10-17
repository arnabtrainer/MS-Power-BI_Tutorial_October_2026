# Section 12 — Capstone, AI/Copilot and Course Consolidation

**Day:** 6 — Post-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Consolidate the complete Power BI workflow from **data acquisition to enterprise sharing**.
- 🎯 Complete a practical **Nirvaan Pharma Ltd capstone** using the model, measures, and report pages built earlier.
- 🎯 Validate KPIs across multiple visuals before presenting insights.
- 🎯 Understand where **Copilot in Power BI** can assist report authors and consumers.
- 🎯 Use Copilot prompts for report creation, report summarization, and semantic-model exploration.
- 🎯 Understand why Copilot requires a well-prepared semantic model.
- 🎯 Validate AI-generated output instead of accepting it blindly.
- 🎯 Recognize Copilot licensing/capacity and tenant-enable­ment prerequisites.
- 🎯 Present a concise business story from the completed Power BI solution.
- 🎯 Review the key learning outcomes from Sections 01–11.

---

## 🗂️ Resources Used

### Primary Case-Study Dataset

- 🗂️ `NirvaanPharma_DW.xlsx`

### Report Pages Created Earlier

- **Production Performance**
- **Inventory & Expiry Analysis**
- **Quality, Deviations & Downtime**
- **Product Detail** *(Drill-through, if created)*
- **Plant Tooltip** *(Tooltip page, if created)*

### Existing Skills Reused

- Power Query
- Star-schema modeling
- Relationships
- DAX measures
- Time intelligence
- Production analytics
- Inventory / expiry analytics
- Quality / deviation / downtime analytics
- Ranking and dynamic interaction
- Drill-through / Tooltips / Bookmarks
- Power BI Service
- Refresh / Gateway
- RLS
- Workspace App / sharing

> 💡 **No major new DAX function is required in this session.**  
> The focus is **integration, validation, storytelling, and responsible use of AI/Copilot**.

---

## 🌐 Microsoft References

- 🌐 Copilot for Power BI overview:  
  `https://learn.microsoft.com/power-bi/create-reports/copilot-introduction`
- 🌐 Enable and configure Copilot in Fabric / Power BI:  
  `https://learn.microsoft.com/fabric/fundamentals/copilot-enable-fabric`
- 🌐 Create and edit Power BI reports with Copilot:  
  `https://learn.microsoft.com/power-bi/create-reports/copilot-create-report-service`
- 🌐 Use Copilot with semantic models:  
  `https://learn.microsoft.com/power-bi/create-reports/copilot-semantic-models`
- 🌐 Prepare / optimize a semantic model for Copilot:  
  `https://learn.microsoft.com/power-bi/create-reports/copilot-evaluate-data`
- 🌐 Create a narrative visual with Copilot:  
  `https://learn.microsoft.com/power-bi/create-reports/copilot-create-narrative`
- 🌐 Copilot prompt guidance for report pages:  
  `https://learn.microsoft.com/power-bi/create-reports/copilot-prompts-report-pages`

---

## 📚 Session Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Capstone Brief | Understand business challenge | 🧑‍🏫 Demo |
| 2 | Capstone Build | Consolidate report solution | 💻 Guided |
| 3 | Validation | Reconcile KPIs across pages | 💻 Guided |
| 4 | Business Story | Present insights clearly | 💻 Guided |
| 5 | Copilot Overview | Capabilities and prerequisites | 🧑‍🏫 Demo |
| 6 | Copilot Report Creation | Prompt-based report assistance | 💻 Demo |
| 7 | Copilot Summaries | Report / visual summarization | 💻 Demo |
| 8 | Copilot + Semantic Model | Ask data questions / DAX assistance | 🧑‍🏫 Demo |
| 9 | Responsible AI | Validate AI output | 🧑‍🏫 Demo |
| 10 | Course Consolidation | End-to-end review | 🔁 Recap |

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:15 | 📚 Capstone brief and expected deliverable |
| 00:15–01:15 | 💻 Capstone build / refinement |
| 01:15–01:35 | ✅ Capstone validation |
| 01:35–01:55 | 💻 Business-story presentation |
| 01:55–02:15 | 🧑‍🏫 Copilot overview and prerequisites |
| 02:15–02:35 | 💻 Copilot report / summary demonstrations |
| 02:35–02:50 | 🧑‍🏫 Copilot validation and responsible-use guidance |
| 02:50–03:00 | 🔁 Course consolidation and final knowledge check |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

# CAPSTONE

## 📚 1. Capstone Scenario

Nirvaan Pharma Ltd leadership wants a concise Power BI solution that answers three operational questions:

### Production

> Are we producing enough, and are we meeting the production plan?

### Inventory

> Where is inventory held, and how much stock is at near-term expiry risk?

### Quality / Operations

> Are quality performance, deviations, and downtime indicating operational areas requiring attention?

The final solution should allow a business user to:

- move between the main analytical pages
- filter the analysis
- understand headline KPIs
- investigate supporting detail
- identify exceptions
- validate the displayed numbers

---

## 🎯 2. Capstone Deliverable

Learners should deliver a small multi-page Power BI solution containing:

### Page 1 — Production Performance

Include:

- Production Quantity
- Yield %
- Rejection %
- Production Cost
- Production Trend
- Plant / Product comparison
- Plan vs Actual

### Page 2 — Inventory & Expiry Analysis

Include:

- Inventory Quantity
- Inventory Value
- Inventory Batch Count
- Inventory by Warehouse
- Stock Status
- Near-expiry inventory
- Expiry Risk %

### Page 3 — Quality, Deviations & Downtime

Include:

- QC Test Count
- Pass Rate %
- Retest %
- Deviation Count
- CAPA Required %
- Downtime Hours
- Unplanned Downtime %

### Interactivity

Use at least:

- one Slicer
- one Tooltip
- one Drill-through page or Bookmark interaction
- one navigation method

### Security / Service Awareness

Learners should be able to explain:

- where the report would be published
- how it would refresh
- when a gateway might be required
- how RLS could restrict Plant-level data
- how consumers would access the report/app

---

## 💻 3. Suggested Capstone Build Steps

### Step 1 — Review the Semantic Model

Confirm:

- relationships
- active Date roles
- measure organization
- hidden technical fields where appropriate

### Step 2 — Review the Existing Pages

Check:

- visual titles
- number formats
- slicer placement
- interaction behavior
- page navigation

### Step 3 — Add an Executive-Level Entry Point

Optionally create a simple page named:

**Executive Overview**

Suggested content:

- `[Production Quantity]`
- `[Yield %]`
- `[Inventory Quantity]`
- `[Expiry Risk %]`
- `[Pass Rate %]`
- `[Downtime Hours]`

Use:

- Card visuals
- Page Navigator / buttons to reach the detailed analytical pages

> 💡 Keep this page intentionally simple. The detailed analysis already exists on the other pages.

### Step 4 — Apply Consistent Formatting

Standardize:

- titles
- percentage formats
- currency formats
- thousand separators
- date formats
- page names
- alignment / spacing

### Step 5 — Test Navigation

Confirm:

- Production page opens
- Inventory page opens
- Quality page opens
- Drill-through works
- Back button works
- Tooltip works

---

## ✅ 4. Capstone Validation

A capstone is not complete merely because all visuals render.

Validate:

### Production

Using the demonstration context established earlier:

- ✅ May 2024 Production Quantity = **613,548**
- ✅ Good Quantity = **590,766**
- ✅ Rejected Quantity = **22,782**
- ✅ Good + Rejected = Production Quantity

### Inventory

Using Snapshot Date = **31-May-2025**:

- ✅ Inventory Quantity = **2,437,829**
- ✅ Inventory Value = **₹917,003,680.38**
- ✅ Inventory Batch Count = **549**
- ✅ Near-expiry quantity = **64,243**
- ✅ Expiry Risk % ≈ **2.64%**

### Quality

Using Calendar Year = **2025**:

- ✅ QC Test Count = **2,362**
- ✅ Passed = **2,331**
- ✅ Failed = **20**
- ✅ OOS = **11**
- ✅ Pass Rate ≈ **98.69%**

### Deviations

Using Calendar Year = **2025**:

- ✅ Deviation Count = **138**
- ✅ CAPA Required Count = **95**
- ✅ CAPA Required % ≈ **68.84%**

### Downtime

Using Calendar Year = **2025**:

- ✅ Downtime Hours = **489.75**
- ✅ Downtime Event Count = **1,462**
- ✅ Unplanned Downtime % ≈ **69.47%**

### 💡 Validation Rule

> **Same Measure + Same Filter Context = Logically Reconciled Result**

If a Card, Chart, and Matrix are showing the same measure under the same filters, their corresponding values should reconcile.

---

## 🧑‍🏫 5. Capstone Business Story

Ask learners to present the report in this sequence:

### 1 — What happened?

Example:

- Production increased/decreased.
- Inventory is concentrated in selected warehouses.
- A certain amount is nearing expiry.
- Quality pass rate remains high.
- Unplanned downtime forms a meaningful share of downtime.

### 2 — Where?

Use:

- Plant
- Product
- Warehouse
- Test Category
- Deviation Category
- Downtime Reason

### 3 — How significant?

Use:

- quantity
- percentage
- value
- ranking
- variance

### 4 — What should be investigated next?

Avoid overclaiming.

Use wording such as:

> “This area deserves deeper investigation.”

rather than:

> “This visual proves the root cause.”

---

# AI / COPILOT

## 📚 6. What Is Copilot in Power BI?

Copilot in Power BI is a generative-AI assistant designed to help users work with Power BI content.

Depending on the experience available in the tenant, Copilot can assist with tasks such as:

- creating or editing report pages from natural-language prompts
- suggesting report content
- summarizing a report or visual
- asking data questions against a semantic model
- supporting semantic-model development
- helping explain or generate DAX queries in DAX Query View

> 💡 **Important:** Copilot assists the analyst. It does not replace correct data modeling, validation, or business judgment.

---

## 📚 7. Copilot Prerequisites

Copilot availability depends on the organization's tenant and capacity configuration.

Current Microsoft guidance requires:

- Copilot enabled by the tenant / capacity administrator
- access to an appropriate paid **Fabric capacity (F2 or higher)** or **Power BI Premium capacity (P1 or higher)**, or a configured Fabric Copilot capacity
- supported regional / organizational configuration
- appropriate report / semantic-model permissions

### Power BI Desktop

To use Copilot in Power BI Desktop, the user needs access to a Copilot-capable workspace/capacity environment.

### 💡 Trainer Check Before Class

Before attempting a live Copilot demonstration:

1. Confirm Copilot is enabled.
2. Confirm the workspace/capacity supports it.
3. Confirm the trainer account has the required access.
4. Open Copilot once before the training day.
5. Keep screenshots or prepared prompts as fallback.

> ⚠️ **Pro or PPU licensing alone does not automatically provide Copilot capacity.**

---

## 🚀 8. If Copilot Is Not Available

Do **not** let the entire Section 12 depend on Copilot availability.

Use a fallback demonstration:

- show the prepared prompt
- discuss the expected type of output
- show saved screenshots if available
- ask learners how they would validate the AI-generated result
- continue with the capstone and consolidation activities

### 💡 Teaching Point

> The learning objective is not “click Copilot.”  
> It is **how to use AI assistance responsibly in a BI workflow**.

---

# COPILOT DEMO 1 — REPORT CREATION

## 💻 9. Ask Copilot to Suggest / Create Report Content

Open Copilot in Power BI Desktop or the Power BI Service where available.

### Example Prompt

```text
Create a report page for Nirvaan Pharma Ltd to analyze production performance.

Use Production Quantity, Yield %, Rejection %, Planned Production,
Production Variance, and Plan Attainment %.

Show the monthly trend and comparisons by Product and Plant.
Keep the page suitable for an operations manager.
```

### What to Observe

Copilot may:

- suggest report content
- create a report page
- select visuals
- place measures/fields
- generate a starting layout

### ✅ Validation

After Copilot produces the page:

1. Verify the measures used.
2. Verify the Date field.
3. Verify the visual grain.
4. Verify Product / Plant context.
5. Compare at least one value with the manually validated dashboard.

> 💡 **Rule:** Treat AI-generated report pages as a **starting point**, not as automatically approved analytical output.

---

# COPILOT DEMO 2 — ASK DATA QUESTIONS

## 💻 10. Ask Questions Against the Semantic Model

Where the Copilot semantic-model experience is available, try prompts such as:

```text
Which products had the highest production quantity in FY2024-25?
```

```text
Summarize production performance for May 2024.
```

```text
Which plants show comparatively higher rejection percentage?
```

```text
What stands out in inventory expiry risk?
```

### ✅ Validation

For a question whose answer is already known, compare Copilot with the validated report.

Example:

```text
What was Production Quantity in May 2024?
```

Expected validated result:

**613,548**

### 💡 Teaching Point

Ask learners:

> “How do we know the AI response is correct?”

Answer:

> **We verify it against the semantic model, trusted measures, filter context, and validated visuals.**

---

# COPILOT DEMO 3 — SUMMARIZE REPORT / VISUAL

## 💻 11. Summarize a Report or Visual

Copilot can summarize report content and, in supported experiences, generate insight-focused summaries for a selected visual.

### Demonstration

Use the **Production Performance** page.

Ask:

```text
Summarize the main production insights on this report page.
```

Or use the supported Copilot summary option for an individual visual.

### What to Review

Check whether the summary:

- reflects the current slicers
- identifies the correct trend
- uses the correct Product / Plant context
- distinguishes quantity from percentage
- avoids unsupported causal claims

### 💡 Important

A summary such as:

> “Plant A has lower production and therefore poor operational efficiency”

would be too strong unless the underlying analysis supports that conclusion.

Prefer:

> “Plant A has lower production in the selected period and may warrant further investigation.”

---

# COPILOT DEMO 4 — NARRATIVE VISUAL

## 🧑‍🏫 12. Optional Copilot Narrative Visual

Where available, demonstrate the **Narrative** visual with Copilot.

A narrative can summarize:

- an entire report
- selected report pages
- selected visuals

### Suggested Target

Use:

- Production trend
- Plan vs Actual
- Yield / Rejection

Ask Copilot for a concise management summary.

### ✅ Validation

Confirm that the narrative:

- matches the selected visual/filter context
- uses the correct numbers
- does not confuse Actual vs Plan
- does not present unsupported recommendations as facts

> 💡 Use AI narratives for communication support, not as a substitute for analytical validation.

---

# COPILOT + SEMANTIC MODEL

## 📚 13. Why Semantic-Model Quality Matters

Copilot works best when the semantic model is well prepared.

Good practices include:

- clear table names
- clear field names
- reusable measures
- correct relationships
- correct data types
- meaningful descriptions
- hidden technical fields where appropriate
- removal of unnecessary ambiguity

### Example

Prefer:

```text
Production Quantity
Plan Attainment %
Inventory Value
Pass Rate %
```

over unexplained names such as:

```text
PQ
PA
IV1
PR_X
```

### 💡 Teaching Point

> **Better semantic model → better human analysis AND better AI grounding.**

Microsoft explicitly warns that poorly prepared semantic models can lead to low-quality or misleading Copilot outputs.

---

## 🧑‍🏫 14. Copilot for DAX / Model Development

Where supported, Copilot can help with tasks such as:

- explaining DAX
- generating DAX queries
- helping understand model logic
- drafting measure descriptions

### Example Prompt

```text
Explain what this measure does in simple business language:

Production MoM % =
DIVIDE(
    [Production MoM Variance],
    [Production Previous Month],
    0
)
```

### Expected Teaching Outcome

Learners should still be able to explain:

```text
(Current Month Production - Previous Month Production)
÷ Previous Month Production
```

without depending on Copilot.

> 💡 AI can accelerate understanding, but the learner should still understand the underlying calculation.

---

# RESPONSIBLE AI

## ⚠️ 15. Validate Copilot Output

Copilot responses are generative and can vary even when prompts are similar.

Therefore, validate:

### Data

- Did Copilot use the correct measure?
- Did it use the correct date?
- Did it use the correct grain?

### Filter Context

- Which slicers/filters are active?
- Is RLS affecting the result?
- Is the answer scoped to the correct page/visual?

### Business Meaning

- Is the interpretation supported?
- Is correlation being presented as causation?
- Is an exception being generalized too broadly?

### Security

Copilot respects the data permissions available to the user.

It should not be treated as a way to bypass report or semantic-model security.

### 💡 AI Validation Rule

> **Prompt → Output → Verify → Interpret → Use**

Never:

> **Prompt → Output → Assume Correct**

---

## 📚 16. Prompt-Writing Guidance

A better Power BI Copilot prompt should include:

- business objective
- measures
- dimensions
- time context
- desired comparison
- audience
- expected output

### Weak Prompt

```text
Create a production report.
```

### Better Prompt

```text
Create an operations-focused production report for Nirvaan Pharma Ltd.

Show Production Quantity, Yield %, Rejection %, Planned Production,
Production Variance, and Plan Attainment %.

Analyze monthly performance across Product and Plant for FY2024-25.
Use a clear management-friendly layout.
```

### 💡 Simple Prompt Formula

```text
Goal + Measures + Dimensions + Time + Audience
```

---

## 🧩 17. Suggested Final Solution Structure

The completed training solution can contain:

```text
Nirvaan Pharma Ltd Power BI Solution
│
├── Executive Overview
├── Production Performance
├── Inventory & Expiry Analysis
├── Quality, Deviations & Downtime
├── Product Detail        (Drill-through)
└── Plant Tooltip         (Tooltip page)
```

Published through:

```text
Power BI Desktop
      ↓
Workspace
      ↓
Semantic Model + Report
      ↓
Refresh / Gateway
      ↓
RLS
      ↓
Workspace App
      ↓
Consumers
```

Copilot sits as an **assistance layer**, not as a replacement for this architecture.

---

# COURSE CONSOLIDATION

## 🔁 18. End-to-End Power BI Workflow

Learners should now be able to explain:

```text
1. Get Data
      ↓
2. Transform with Power Query
      ↓
3. Build the Data Model
      ↓
4. Create DAX Measures
      ↓
5. Build Visual Analytics
      ↓
6. Add Interactivity
      ↓
7. Validate the Numbers
      ↓
8. Publish to the Service
      ↓
9. Configure Refresh / Gateway
      ↓
10. Apply RLS
      ↓
11. Share through Workspace / App
      ↓
12. Use AI/Copilot responsibly
```

---

## 🔁 19. Section-Wise Consolidation

| Section | Learner Outcome |
|---|---|
| **01** | Connect to common data sources |
| **02** | Clean and prepare data with Power Query |
| **03** | Combine, reshape, and understand basic M |
| **04** | Build a star-schema semantic model |
| **05** | Create DAX fundamentals and reusable measures |
| **06** | Apply advanced DAX and time intelligence |
| **07** | Build Production Performance analytics |
| **08** | Build Inventory & Expiry analytics |
| **09** | Analyze Quality, Deviations, and Downtime |
| **10** | Add advanced reporting interactivity and UX |
| **11** | Publish, refresh, secure, and share |
| **12** | Consolidate the solution and use Copilot responsibly |

---

## ✅ 20. Final Capstone Evaluation Checklist

### Data & Model

- ✅ Correct tables used.
- ✅ Relationships work correctly.
- ✅ Date roles are understood.
- ✅ No obvious duplicate/ambiguous paths.

### DAX

- ✅ Measures are reusable.
- ✅ Ratios use appropriate base measures.
- ✅ Time calculations are validated.
- ✅ No unnecessary duplicate measures.

### Visuals

- ✅ Visual type matches the business question.
- ✅ Titles are meaningful.
- ✅ Numbers are formatted correctly.
- ✅ Time axes are sorted correctly.

### Interactivity

- ✅ Slicers behave correctly.
- ✅ Drill-through works.
- ✅ Tooltip works.
- ✅ Navigation works.
- ✅ Bookmarks / Field Parameters work if used.

### Validation

- ✅ At least one Production KPI reconciled.
- ✅ At least one Inventory KPI reconciled.
- ✅ At least one Quality/Deviation/Downtime KPI reconciled.

### Service / Governance

- ✅ Publishing path understood.
- ✅ Refresh / gateway requirement understood.
- ✅ RLS concept understood.
- ✅ Sharing method understood.

### AI / Copilot

- ✅ Prompt is specific.
- ✅ Output is checked against trusted measures.
- ✅ AI summary does not overstate conclusions.
- ✅ Learner understands that Copilot output can vary.

---

## 💻 Guided Capstone Challenge

Learners should:

1. 💻 Review the three analytical pages.
2. 💻 Add or refine an **Executive Overview** page.
3. 💻 Add at least one navigation method.
4. 💻 Validate May 2024 Production Quantity.
5. 💻 Validate 31-May-2025 Inventory Quantity and Expiry Risk %.
6. 💻 Validate Calendar Year 2025 Pass Rate %.
7. 💻 Validate Calendar Year 2025 CAPA Required %.
8. 💻 Validate Calendar Year 2025 Unplanned Downtime %.
9. 💻 Present three meaningful business observations.
10. 💻 Explain one area that requires further investigation.
11. 🚀 Use Copilot to create or summarize one analytical view, if available.
12. 💻 Validate the Copilot output against the trusted report.
13. 💻 Explain the Publish → Refresh → Secure → Share flow.

### ✅ Expected Outcome

Learners can present a complete Power BI solution and explain:

- where the data came from
- how it was transformed
- how the semantic model works
- how KPIs were calculated
- why each visual was selected
- how results were validated
- how the report would be published and secured
- how AI/Copilot can assist without replacing analytical responsibility

---

## 💡 Trainer Guidelines

- 💡 Keep the capstone focused on **integration**, not new feature overload.
- 💡 Ask learners to explain their choices, not only demonstrate clicks.
- 💡 Require at least one manual KPI reconciliation.
- 💡 Use familiar Nirvaan Pharma measures rather than inventing unnecessary new DAX.
- 💡 Explain Copilot prerequisites before opening the Copilot pane.
- 💡 Keep a fallback plan if Copilot is unavailable.
- 💡 Use Copilot on already validated business questions first.
- 💡 Compare AI output with known values.
- 💡 Emphasize semantic-model quality as the foundation for AI-assisted BI.
- 💡 Explain that Copilot results can vary.
- ⚠️ Never accept AI-generated numbers without validation.
- ⚠️ Do not expose confidential enterprise data in training prompts.
- ⚠️ Do not imply Copilot replaces data governance, RLS, or model design.
- ⚠️ Do not let Copilot availability determine whether the session succeeds.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 The complete Power BI lifecycle.
- 🔁 How to consolidate Production, Inventory, Quality, and Operational analytics.
- 🔁 How to validate KPIs before presenting insights.
- 🔁 How to communicate findings without overclaiming.
- 🔁 What Copilot can assist with in Power BI.
- 🔁 Why Copilot requires a well-prepared semantic model.
- 🔁 How to write more effective Copilot prompts.
- 🔁 Why AI-generated results must be verified.
- 🔁 How Power BI moves from Desktop to governed enterprise consumption.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What is the main objective of the Section 12 capstone?

A. Consolidate the complete Power BI solution and validate it <br>
B. Create a new operating system <br>
C. Replace Power BI with Excel <br>
D. Delete all previous report pages <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Consolidate the complete Power BI solution and validate it**

**Explanation:** The capstone combines the modeling, DAX, analytics, interactivity, and Service concepts covered throughout the course.

</details>

### 🔴 Q2. What should be done before presenting a KPI as a business insight?

A. Validate the measure and filter context <br>
B. Assume every Card is correct <br>
C. Remove all relationships <br>
D. Convert every measure to a calculated column <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Validate the measure and filter context**

**Explanation:** A visual displaying a number does not guarantee that the business logic or filter context is correct.

</details>

### 🔴 Q3. What can Copilot in Power BI help with?

A. Report creation, summaries, data questions, and selected development tasks <br>
B. Physically repair a database server <br>
C. Replace all data governance <br>
D. Ignore RLS permissions <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Report creation, summaries, data questions, and selected development tasks**

**Explanation:** Copilot assists Power BI development and consumption workflows, but it does not replace modeling, security, or validation.

</details>

### 🔴 Q4. Why is semantic-model quality important for Copilot?

A. Copilot relies on the semantic model as grounding context <br>
B. Copilot ignores all model metadata <br>
C. Relationships never affect AI output <br>
D. Only report colors matter <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Copilot relies on the semantic model as grounding context**

**Explanation:** Clear measures, relationships, names, and metadata help Copilot interpret the model more accurately.

</details>

### 🔴 Q5. Which capacity is part of the current Copilot prerequisite guidance?

A. Paid Fabric capacity such as F2+ or Power BI Premium P1+ <br>
B. Free capacity only <br>
C. Excel workbook capacity <br>
D. Any local hard drive <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Paid Fabric capacity such as F2+ or Power BI Premium P1+**

**Explanation:** Copilot requires appropriate organizational enablement and qualifying capacity; licensing alone is not sufficient in every setup.

</details>

### 🔴 Q6. What should the trainer do if Copilot is unavailable during class?

A. Use prepared prompts/screenshots and continue the capstone <br>
B. Cancel the entire session <br>
C. Skip course consolidation <br>
D. Disable the semantic model <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Use prepared prompts/screenshots and continue the capstone**

**Explanation:** The learning objective is responsible AI-assisted BI, not dependence on one live feature.

</details>

### 🔴 Q7. What is the best way to validate a Copilot answer about May 2024 Production Quantity?

A. Compare it with the trusted measure/report result <br>
B. Accept the first answer automatically <br>
C. Remove the Date filter <br>
D. Ignore the semantic model <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Compare it with the trusted measure/report result**

**Explanation:** AI output should be reconciled against known measures and filter context.

</details>

### 🔴 Q8. Which prompt is generally better?

A. A prompt specifying goal, measures, dimensions, time, and audience <br>
B. “Make something” <br>
C. A prompt with no business objective <br>
D. A prompt that avoids naming measures <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. A prompt specifying goal, measures, dimensions, time, and audience**

**Explanation:** Specific context gives Copilot a clearer analytical target.

</details>

### 🔴 Q9. Why should AI-generated summaries avoid unsupported causal claims?

A. The report may show association without proving cause <br>
B. Causation is always obvious from a chart <br>
C. Visuals cannot contain numbers <br>
D. Power BI automatically proves root cause <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. The report may show association without proving cause**

**Explanation:** A dashboard can identify patterns or exceptions, but further investigation may be required before establishing root cause.

</details>

### 🔴 Q10. Which sequence represents the core Power BI lifecycle?

A. Get Data → Transform → Model → Analyze → Visualize → Publish <br>
B. Publish → Delete → Guess → Share <br>
C. Format → Print → Delete Data → Publish <br>
D. Create Buttons → Ignore Model → Share <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Get Data → Transform → Model → Analyze → Visualize → Publish**

**Explanation:** The Power BI workflow progresses from data acquisition and preparation through modeling, analysis, reporting, and distribution.

</details>

### 🔴 Q11. What is the recommended AI workflow in this section?

A. Prompt → Output → Verify → Interpret → Use <br>
B. Prompt → Assume Correct → Publish <br>
C. Prompt → Ignore Filters → Share <br>
D. Prompt → Delete Model → Present <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Prompt → Output → Verify → Interpret → Use**

**Explanation:** Verification is essential before AI-generated content is used for business decisions or reporting.

</details>

### 🔴 Q12. What is the final learning outcome of the complete course?

A. Build, validate, publish, secure, and responsibly enhance a Power BI solution <br>
B. Memorize every DAX function <br>
C. Use only one visual type <br>
D. Avoid data modeling <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Build, validate, publish, secure, and responsibly enhance a Power BI solution**

**Explanation:** The course integrates the complete Power BI lifecycle from source data to governed, AI-assisted business analytics.

</details>

---

## 🎓 Course Completion

Learners have now completed the full **12-session Power BI learning journey** for the Nirvaan Pharma Ltd case study.

The final solution demonstrates:

> **Data → Transformation → Model → DAX → Analytics → UX → Service → Security → AI-assisted Insight**
