# Section 11 — Power BI Service, Refresh, RLS and Enterprise Sharing

**Day:** 6 — Pre-Lunch  
**Duration:** 3 Hours  
**Case Company:** **Nirvaan Pharma Ltd** *(fictitious pharma company)*

---

## 🎯 Session Objectives

By the end of this session, learners should be able to:

- 🎯 Publish a Power BI Desktop report to the **Power BI Service / Microsoft Fabric**.
- 🎯 Understand **Workspaces** and the main workspace roles.
- 🎯 Distinguish a **Report** from its underlying **Semantic Model**.
- 🎯 Configure or explain **scheduled refresh** and when a **gateway** is required.
- 🎯 Understand **standard vs personal on-premises gateway** scenarios.
- 🎯 Create and validate **Row-Level Security (RLS)**.
- 🎯 Understand optional **dynamic RLS** using `USERPRINCIPALNAME()`.
- 🎯 Distinguish collaboration through a Workspace from controlled distribution through a **Power BI App / Workspace App**.
- 🎯 Apply a practical enterprise-sharing and validation checklist.
- 🎯 Recognize licensing/capacity considerations without turning the session into a licensing deep dive.

---

## 🗂️ Resources Used

### Primary Case-Study Content

- 🗂️ `NirvaanPharma_DW.xlsx`
- 🗂️ Power BI report containing the analytical pages created in Sections 07–10

### Existing Report Pages

- **Production Performance**
- **Inventory & Expiry Analysis**
- **Quality, Deviations & Downtime**
- **Product Detail** *(Drill-through page, if created)*
- **Plant Tooltip** *(Tooltip page, if created)*

### Main Tables Used for RLS Demonstration

- `DimPlant`
- `DimProduct`
- `FactProduction`
- `FactInventorySnapshot`
- `FactProductionPlan`

### Optional Dynamic-RLS Table

Create a small training table named:

**`UserPlantAccess`**

Example:

| UserEmail | PlantName |
|---|---|
| trainer1@contoso.com | Kolkata Plant |
| trainer2@contoso.com | Pune Plant |
| trainer3@contoso.com | Hyderabad Plant |

> ⚠️ Replace these sample email addresses with valid training/test accounts in the tenant if you actually test Dynamic RLS.

---

## 🌐 Microsoft References

- 🌐 Power BI RLS:  
  `https://learn.microsoft.com/power-bi/service-admin-rls`
- 🌐 Data Refresh in Power BI:  
  `https://learn.microsoft.com/power-bi/connect-data/refresh-data`
- 🌐 On-premises Data Gateway:  
  `https://learn.microsoft.com/power-bi/connect-data/service-gateway-onprem`
- 🌐 Workspace Access / Roles:  
  `https://learn.microsoft.com/power-bi/collaborate-share/service-give-access-new-workspaces`
- 🌐 Publish a Workspace App:  
  `https://learn.microsoft.com/power-bi/collaborate-share/service-create-distribute-apps`

---

## 📚 Service & Governance Coverage

| # | Topic | Main Activity | Delivery |
|---|---|---|---|
| 1 | Publish | Desktop → Power BI Service | 💻 Guided |
| 2 | Workspace | Roles and collaboration | 🧑‍🏫 Demo |
| 3 | Semantic Model | Report vs model vs refresh | 🧑‍🏫 Demo |
| 4 | Refresh | Credentials, schedule, history | 💻 Guided |
| 5 | Gateway | Standard vs Personal | 🧑‍🏫 Demo |
| 6 | Static RLS | Plant-based access | 💻 Guided |
| 7 | Dynamic RLS | `USERPRINCIPALNAME()` | 🚀 Optional |
| 8 | RLS Validation | View As / Test as Role | 💻 Guided |
| 9 | Sharing | Direct Share vs Workspace vs App | 🧑‍🏫 Demo |
| 10 | App Distribution | Audience-based consumption | 💻 Guided |
| 11 | Validation | Enterprise checklist | 💻 Guided |

---

## 🧭 DAX — Purpose and Target Map

Only one new DAX function is introduced, and only for the optional Dynamic RLS example.

| DAX Function | Purpose | Target |
|---|---|---|
| `USERPRINCIPALNAME()` | Returns the signed-in user's user principal name (typically email/UPN) | Match the current user to rows in an access table for Dynamic RLS |

> 💡 **Static RLS does not require a new DAX function.**  
> It can use simple Boolean filters such as:

```DAX
DimPlant[PlantName] = "Kolkata Plant"
```

---

## ⏱️ Suggested 3-Hour Flow

| Time | Activity |
|---|---|
| 00:00–00:15 | 🔁 Desktop vs Service / Fabric recap |
| 00:15–00:35 | 💻 Publish report to a Workspace |
| 00:35–00:55 | 🧑‍🏫 Workspace roles and semantic model |
| 00:55–01:20 | 💻 Refresh, credentials, refresh history |
| 01:20–01:40 | 🧑‍🏫 Gateway concepts |
| 01:40–02:10 | 💻 Static RLS |
| 02:10–02:30 | 🚀 Optional Dynamic RLS |
| 02:30–02:45 | 💻 RLS validation in Service |
| 02:45–02:55 | 💻 App / enterprise sharing |
| 02:55–03:00 | ✅ Recap |

> 📝 The 12 MCQs can be used as an end-of-session or post-session self-check.

---

# POWER BI SERVICE

## 📚 1. Desktop vs Power BI Service

### Power BI Desktop

Primarily used to:

- connect to data
- transform data
- create the semantic model
- create DAX
- build reports
- test RLS roles

### Power BI Service / Fabric

Primarily used to:

- host published reports and semantic models
- collaborate through Workspaces
- configure refresh
- manage gateway connections
- assign RLS role membership
- share reports
- publish Apps
- monitor refresh and usage

### 💡 Simple Rule

> **Desktop = Build**  
> **Service = Publish, Refresh, Secure, Share, Govern**

---

## 💻 2. Publish the Nirvaan Pharma Report

### Step 1 — Save the PBIX

Before publishing:

- save the latest Power BI Desktop file
- verify the report pages
- verify RLS roles if already created
- verify data-source paths

### Step 2 — Publish

In Power BI Desktop:

**Home → Publish**

Sign in with the organization's Power BI account if required.

### Step 3 — Select the Destination Workspace

Choose the training / project Workspace.

> ⚠️ Avoid publishing enterprise content into **My workspace** when the content is intended for team collaboration and controlled distribution.

### Step 4 — Open the Published Content

After publishing, open the Power BI Service.

You should see:

- the **Report**
- the underlying **Semantic Model**

### ✅ Validation

Confirm:

- ✅ Report pages open successfully.
- ✅ Slicers work.
- ✅ Drill-through works.
- ✅ Tooltip pages work.
- ✅ The Semantic Model appears in the Workspace.
- ✅ The report is connected to the expected Semantic Model.

> 🖼️ **Image Placeholder S11-01:** Power BI Service Workspace showing the published Report and Semantic Model.  
> **Planned file:** `images/S11_01_Published_Workspace.png`

---

# WORKSPACES

## 📚 3. Understand Workspace Roles

Common Power BI Workspace roles are:

| Workspace Role | Typical Purpose |
|---|---|
| **Admin** | Full workspace administration and access management |
| **Member** | Broad content management and collaboration |
| **Contributor** | Create/edit content without full workspace administration |
| **Viewer** | Read/consume content |

### 💡 Important RLS Rule

For users who should be restricted by RLS:

> **Use Viewer-level consumption rather than Admin / Member / Contributor.**

RLS applies to consumers, but users with editing-level Workspace roles such as **Admin, Member, or Contributor** are not restricted by RLS in the same way.

### ✅ Validation

Open:

**Workspace → Manage access**

Review the role assigned to each training/test user.

> ⚠️ Do not give report consumers more Workspace permission than they need.

---

# SEMANTIC MODEL AND REFRESH

## 📚 4. Report vs Semantic Model

When a PBIX is published, learners should distinguish:

### Report

Contains:

- report pages
- visuals
- filters
- interactions
- bookmarks
- navigation

### Semantic Model

Contains:

- imported/modelled data
- relationships
- DAX measures
- RLS roles
- metadata used by reports

### 💡 Teaching Point

> **Refreshing the Semantic Model refreshes the report's underlying data.**

The report visuals themselves are not a separate copy of the source data.

---

## 💻 5. Review Semantic Model Settings

In the Workspace:

1. Locate the **Semantic Model**.
2. Open **Settings** / **Semantic model settings**.
3. Review:
   - Data source credentials / connections
   - Gateway and cloud connections
   - Refresh settings
   - Refresh history
   - Parameters where applicable

### ✅ Validation

Confirm that Power BI can authenticate to the required data source.

> ⚠️ A report can publish successfully even when later refresh cannot reach the source. Publishing and refreshing are separate checks.

---

# REFRESH

## 📚 6. Understand Refresh

For an **Import** semantic model, refresh means:

> Power BI reconnects to the source, re-runs the required queries/transformations, and reloads updated data into the semantic model.

### Refresh Options

- **Refresh now** → run an on-demand refresh
- **Scheduled refresh** → Power BI refreshes at configured times
- **Refresh history** → review success/failure records

### Current Service Limits — Teaching Awareness

Current Microsoft guidance allows approximately:

- **Shared capacity** → up to **8 scheduled refreshes per day**
- **Premium / PPU / qualifying Fabric capacity** → up to **48 scheduled refreshes per day**

> ⚠️ Capacity and licensing behavior can change. Verify current Microsoft documentation before a production implementation.

---

## 💻 7. Configure a Simple Scheduled Refresh

If the training tenant/source configuration supports it:

### Steps

1. Open the Semantic Model settings.
2. Confirm **Data source credentials / Gateway and cloud connections**.
3. Open **Refresh** settings.
4. Turn on scheduled refresh.
5. Select the appropriate:
   - Time zone
   - Refresh frequency
   - Refresh time(s)
6. Enable refresh-failure notifications where appropriate.
7. Save.

### ✅ Validation

Use:

**Refresh now**

Then open:

**Refresh history**

Confirm:

- ✅ Status = Completed / Succeeded
- ✅ Expected start/end time
- ✅ No credential or gateway errors

> 🖼️ **Image Placeholder S11-02:** Semantic Model refresh settings and Refresh History.  
> **Planned file:** `images/S11_02_Refresh_Settings.png`

---

# GATEWAYS

## 📚 8. When Is a Gateway Required?

A gateway is commonly needed when the Power BI Service must access a data source that is not directly reachable as a supported cloud source.

Examples:

- SQL Server inside a company network
- local/on-premises file source
- other supported on-premises enterprise systems

### Nirvaan Pharma Training Example

If `NirvaanPharma_DW.xlsx` remains only on a trainer's **local disk**, the Power BI Service cannot simply reach that local file by itself.

A practical enterprise approach would be either:

- place the source in a supported cloud location such as SharePoint / OneDrive where appropriate, **or**
- use an appropriate gateway for an on-premises/local source.

---

## 📚 9. Gateway Types

### On-premises Data Gateway — Standard Mode

Recommended for:

- shared/team scenarios
- centrally managed enterprise data sources
- multiple users
- DirectQuery / live connection scenarios
- high availability / clustering requirements

### On-premises Data Gateway — Personal Mode

Suitable mainly for:

- one individual user
- personal Import semantic models
- limited personal refresh scenarios

### Virtual Network (VNet) Gateway

Used for supported data sources secured inside virtual networks.

### 💡 Enterprise Recommendation

> **Standard mode is normally preferred for departmental or enterprise BI.**

Do not design enterprise refresh around one employee's personal gateway unless that is genuinely the intended operating model.

---

## 🧑‍🏫 10. Gateway Demonstration Flow

If a gateway environment is available:

1. Open **Settings → Manage connections and gateways**.
2. Review the available gateway / gateway cluster.
3. Review the connection used by the semantic model.
4. Confirm credentials.
5. Map the semantic model to the correct connection.
6. Trigger **Refresh now**.
7. Check Refresh History.

### If No Gateway Is Available During Training

Explain conceptually:

```text
Power BI Service
      |
      | Secure gateway communication
      v
On-premises Data Gateway
      |
      v
On-premises / Local Data Source
```

> 💡 Do not spend class time installing enterprise infrastructure unless gateway setup is explicitly part of the training environment.

---

# ROW-LEVEL SECURITY

## 📚 11. What Is RLS?

**Row-Level Security (RLS)** restricts which **rows of data** a user is allowed to see.

Example:

- Kolkata user → Kolkata Plant data
- Pune user → Pune Plant data
- Hyderabad user → Hyderabad Plant data

RLS does **not** mean:

- hiding a report page
- hiding a measure
- hiding a column
- assigning Workspace edit permissions

### 💡 Simple Rule

> **RLS controls data rows visible to a user.**

---

## 💻 12. Static RLS — Plant Example

Start with a simple static role.

### Step 1 — Open Manage Roles

In Power BI Desktop:

**Modeling → Manage roles**

Create:

**Kolkata Plant Role**

### Step 2 — Apply the Filter

Select `DimPlant`.

Use:

```DAX
DimPlant[PlantName] = "Kolkata Plant"
```

### 🎯 Purpose and Target

- 🎯 **Purpose:** Restrict `DimPlant` to one Plant.
- 🧭 **Target:** Allow role members to see only data reachable through the Kolkata Plant relationship path.

### Step 3 — Validate in Desktop

Use:

**Modeling → View as**

Select:

**Kolkata Plant Role**

### ✅ Validation

Open the Production Performance page.

Confirm:

- ✅ Only Kolkata Plant data is visible.
- ✅ Production KPI Cards recalculate.
- ✅ Product charts show only production related to Kolkata.
- ✅ Inventory visuals connected through Plant are restricted appropriately.
- ✅ Other unrelated tables are not accidentally filtered unless relationships propagate the filter.

> 💡 **Teaching Point:** Apply RLS to a dimension such as `DimPlant` rather than repeating equivalent filters separately on many fact tables.

---

# OPTIONAL DYNAMIC RLS

## 🚀 13. Dynamic RLS with `USERPRINCIPALNAME()`

Static RLS works well when there are only a few fixed roles.

Dynamic RLS is useful when access varies by user.

### Step 1 — Create `UserPlantAccess`

Example:

| UserEmail | PlantName |
|---|---|
| trainer1@contoso.com | Kolkata Plant |
| trainer2@contoso.com | Pune Plant |
| trainer3@contoso.com | Hyderabad Plant |

### Step 2 — Relate the Access Table

Create an appropriate relationship from the access table's Plant value/key to the Plant dimension.

For an enterprise implementation, prefer a proper Plant key rather than relying on names where possible.

### Step 3 — Create the Dynamic Role

Create:

**Dynamic Plant Role**

Apply this filter to `UserPlantAccess`:

```DAX
UserPlantAccess[UserEmail] =
USERPRINCIPALNAME()
```

### 🎯 Purpose and Target

- 🎯 **`USERPRINCIPALNAME()` Purpose:** Return the signed-in user's UPN/email identity.
- 🧭 **Target:** Filter `UserPlantAccess` to the current user and allow the related Plant filter to propagate to the fact tables.

### Example

If the signed-in user is:

```text
trainer2@contoso.com
```

and the access table maps that account to:

```text
Pune Plant
```

the report should show only data allowed for Pune Plant.

> ⚠️ Dynamic RLS requires careful relationship design and valid tenant identities. Treat this as an optional extension unless test accounts are available.

---

## 💻 14. Publish and Assign RLS Members

After creating RLS roles in Desktop:

1. Publish / republish the report and semantic model.
2. In the Power BI Service, open the Workspace.
3. Locate the Semantic Model.
4. Open **... → Security**.
5. Select the appropriate RLS role.
6. Add:
   - users, or
   - supported groups
7. Save.

### 💡 Enterprise Practice

Prefer supported security groups where practical rather than maintaining many individual users manually.

---

## ✅ 15. Validate RLS in the Power BI Service

Use the Service's role-testing capability such as:

**Test as role**

Confirm:

- ✅ Kolkata role sees Kolkata data only.
- ✅ Other Plant data is excluded.
- ✅ Dynamic RLS resolves the expected test account if demonstrated.
- ✅ Report pages still render correctly.
- ✅ Drill-through and Tooltips do not bypass the intended data restriction.

### ⚠️ Critical Workspace Role Check

A user assigned **Admin, Member, or Contributor** in the Workspace has edit-level permissions and is not restricted by RLS in the same way as a Viewer.

Therefore:

> **If the training objective is to prove RLS for a consumer, test with a Viewer / app consumer scenario.**

> 🖼️ **Image Placeholder S11-03:** Semantic Model Security page showing RLS roles and role membership.  
> **Planned file:** `images/S11_03_RLS_Security.png`

---

# SHARING AND DISTRIBUTION

## 📚 16. Choose the Right Sharing Method

| Method | Best Use |
|---|---|
| **Workspace access** | Authors / collaborators who need to work with content |
| **Direct Share** | Controlled sharing of a specific report/dashboard |
| **Power BI App / Workspace App** | Curated distribution to a broader consumer audience |
| **Teams / Link-based access** | Convenient access path when permissions are already correctly configured |

### 💡 Teaching Point

> **Workspace = collaboration**  
> **App = curated consumption**

---

## 💻 17. Share a Report Directly

From the Power BI Service:

1. Open the report.
2. Select **Share**.
3. Choose the intended users/groups.
4. Review permission options carefully.
5. Send or copy the link.

### ⚠️ Important

Sharing a report also involves access to the underlying semantic model required for the report to function.

Do not grant unnecessary:

- resharing permission
- Build permission
- Workspace editing rights

---

# POWER BI APP / WORKSPACE APP

## 💻 18. Publish a Workspace App

A Workspace App packages selected content for consumers.

### Step 1 — Open the Workspace

Ensure the intended reports are ready.

### Step 2 — Create / Update App

Select:

**Create app** / **Update app**

### Step 3 — Configure the App

Set:

- App name
- Description
- Contact / support information where appropriate

### Step 4 — Add Content

Include the relevant report(s).

Example:

- Production Performance
- Inventory & Expiry Analysis
- Quality, Deviations & Downtime

### Step 5 — Configure Audience

Choose the intended users or groups.

Where useful, different audiences can receive different subsets of app content.

### Step 6 — Publish

Select:

**Publish app**

Copy the app link for the intended consumers.

### ✅ Validation

Using a test consumer account where possible:

- ✅ App opens successfully.
- ✅ Intended report pages are visible.
- ✅ Hidden helper pages do not appear unexpectedly.
- ✅ RLS still restricts data appropriately.
- ✅ Consumer cannot edit report content.
- ✅ Navigation works.

> 🖼️ **Image Placeholder S11-04:** Published Workspace App containing the Nirvaan Pharma analytical reports.  
> **Planned file:** `images/S11_04_Published_App.png`

---

# LICENSING / CAPACITY AWARENESS

## 📚 19. Licensing — Keep It Conceptual

Power BI sharing behavior depends on:

- user licenses
- workspace capacity
- organization / tenant configuration

### Practical Teaching Points

- Content creators commonly require **Power BI Pro** or an appropriate higher license/capacity setup.
- Consumers may also require paid licenses unless the content is hosted on qualifying capacity.
- App and sharing behavior can depend on Premium / Fabric capacity.

> ⚠️ Licensing changes over time. For a real deployment, always verify the organization's current Microsoft licensing and capacity configuration.

---

## ✅ 20. Enterprise Validation Checklist

Before declaring the report ready for enterprise consumption, validate:

### Publishing

- ✅ Correct PBIX version published.
- ✅ Correct Workspace selected.
- ✅ Report and Semantic Model appear.

### Data Access

- ✅ Data-source credentials are valid.
- ✅ Gateway / cloud connection is correct.
- ✅ Refresh now succeeds.
- ✅ Refresh history shows successful execution.

### Scheduled Refresh

- ✅ Correct time zone.
- ✅ Appropriate refresh frequency.
- ✅ Failure notification configured where required.

### Security

- ✅ RLS roles exist.
- ✅ RLS members/groups assigned.
- ✅ RLS tested with consumer-level access.
- ✅ Workspace Admin/Member/Contributor roles are not being used as the RLS test.

### Sharing

- ✅ Consumers receive only the access required.
- ✅ App audience is correct.
- ✅ Helper pages are hidden where appropriate.
- ✅ Build / Reshare permission is granted only when justified.

### User Experience

- ✅ App/report navigation works.
- ✅ Drill-through works.
- ✅ Tooltips work.
- ✅ Synced slicers behave correctly.
- ✅ No broken visuals after publishing.

---

## 💻 Guided Hands-on Challenge

Learners should:

1. 💻 Publish the latest Nirvaan Pharma report to a Workspace.
2. 💻 Identify the Report and Semantic Model.
3. 💻 Review Workspace access roles.
4. 💻 Review Semantic Model settings.
5. 💻 Trigger **Refresh now** where supported.
6. 💻 Review Refresh History.
7. 🧑‍🏫 Explain when a gateway is required.
8. 💻 Create **Kolkata Plant Role** in Desktop.
9. 💻 Validate it using **View as**.
10. 💻 Publish the role to the Service.
11. 💻 Assign a test user/group to the role where available.
12. 💻 Validate RLS using **Test as role**.
13. 🚀 Optionally create Dynamic RLS using `USERPRINCIPALNAME()`.
14. 💻 Publish / update a Workspace App.
15. 💻 Validate the app as a consumer.

### ✅ Expected Outcome

Learners understand the complete path:

```text
Power BI Desktop
      ↓
Publish
      ↓
Workspace
      ↓
Semantic Model + Report
      ↓
Refresh / Gateway
      ↓
RLS
      ↓
App / Sharing
      ↓
Controlled Consumer Access
```

---

## 💡 Trainer Guidelines

- 💡 Use **Semantic Model** terminology consistently rather than the older “dataset” terminology.
- 💡 Keep the session practical: Publish → Refresh → Secure → Share.
- 💡 Distinguish **Workspace collaboration** from **App consumption**.
- 💡 Explain that publishing success does not guarantee refresh success.
- 💡 Use **standard gateway mode** as the enterprise recommendation.
- 💡 Keep personal gateway discussion short and clearly label it as a limited/personal scenario.
- 💡 Demonstrate Static RLS before Dynamic RLS.
- 💡 Explain the difference between a Workspace role and an RLS role.
- 💡 Emphasize that RLS is for **row restriction**, not hiding columns/measures.
- 💡 Validate RLS using a Viewer/app-consumer scenario.
- 💡 Mention licensing/capacity only at the level needed to explain why sharing behavior may differ.
- ⚠️ Never demonstrate enterprise governance using real confidential data.
- ⚠️ Do not grant Admin/Member/Contributor access merely to make a report visible.
- ⚠️ Do not store production credentials in screenshots or training documents.
- ⚠️ Do not assume a gateway is unnecessary simply because Desktop refresh works.

---

## 🔁 Session Recap

Learners should now understand:

- 🔁 Desktop vs Power BI Service responsibilities.
- 🔁 Report vs Semantic Model.
- 🔁 Workspace roles.
- 🔁 Refresh and Refresh History.
- 🔁 Standard vs Personal Gateway.
- 🔁 Static RLS.
- 🔁 Optional Dynamic RLS with `USERPRINCIPALNAME()`.
- 🔁 Why Viewer-level testing matters for RLS.
- 🔁 Direct Share vs Workspace vs App.
- 🔁 Enterprise validation before consumer rollout.

---

## 📝 Knowledge Check — 12 MCQs

### 🔴 Q1. What is the primary role of Power BI Desktop?

A. Build models, DAX, and reports <br>
B. Manage enterprise email <br>
C. Replace Microsoft Entra ID <br>
D. Host production databases <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Build models, DAX, and reports**

**Explanation:** Power BI Desktop is the primary authoring environment for connecting, modeling, calculating, and designing reports.

</details>

### 🔴 Q2. What is the underlying analytical model called in current Power BI terminology?

A. Semantic Model <br>
B. Slide Deck <br>
C. Workbook Macro <br>
D. Workspace App only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Semantic Model**

**Explanation:** The Semantic Model contains the modelled data, relationships, measures, and security roles used by reports.

</details>

### 🔴 Q3. Which Workspace role is appropriate for a consumer who should be restricted by RLS?

A. Viewer <br>
B. Admin <br>
C. Member <br>
D. Contributor <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Viewer**

**Explanation:** RLS is intended to restrict consumer-level access; edit-level Workspace roles such as Admin, Member, and Contributor are not restricted in the same way.

</details>

### 🔴 Q4. What does scheduled refresh do for an Import semantic model?

A. Reloads updated data from the source according to a schedule <br>
B. Changes report colors <br>
C. Creates a new Workspace <br>
D. Creates RLS roles automatically <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Reloads updated data from the source according to a schedule**

**Explanation:** Scheduled refresh reconnects to the data source and updates the imported semantic model.

</details>

### 🔴 Q5. When is an on-premises gateway commonly needed?

A. When the Power BI Service must reach an on-premises/local data source <br>
B. To create a Card visual <br>
C. To write DAX in Desktop <br>
D. To sort a Matrix <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. When the Power BI Service must reach an on-premises/local data source**

**Explanation:** The gateway provides a secure bridge between the cloud service and supported on-premises data sources.

</details>

### 🔴 Q6. Which gateway mode is generally recommended for shared enterprise scenarios?

A. Standard mode <br>
B. Personal mode only <br>
C. No gateway under any circumstance <br>
D. Excel mode <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Standard mode**

**Explanation:** Standard mode supports centralized, multi-user enterprise scenarios and broader connectivity/governance requirements.

</details>

### 🔴 Q7. What does Row-Level Security control?

A. Which rows of data a user can see <br>
B. The font size of a report <br>
C. Whether a visual has a title <br>
D. The PBIX filename <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Which rows of data a user can see**

**Explanation:** RLS filters model rows according to security roles and rules.

</details>

### 🔴 Q8. Where is an RLS role typically created for a Power BI Desktop model?

A. Modeling → Manage roles <br>
B. Insert → Text box <br>
C. Home → Transform Data only <br>
D. View → Performance Analyzer only <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Modeling → Manage roles**

**Explanation:** RLS role definitions can be created and tested in Power BI Desktop before publishing.

</details>

### 🔴 Q9. What does `USERPRINCIPALNAME()` support in this session?

A. Dynamic RLS based on the signed-in user's identity <br>
B. Product ranking <br>
C. Data-source refresh frequency <br>
D. Visual sorting <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Dynamic RLS based on the signed-in user's identity**

**Explanation:** The function can match the current user's UPN/email to an access table that determines allowed data.

</details>

### 🔴 Q10. What is the main difference between Workspace access and a Power BI App?

A. Workspace supports collaboration; an App provides curated consumer distribution <br>
B. They are exactly the same <br>
C. Apps are only for Excel files <br>
D. Workspaces cannot contain reports <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Workspace supports collaboration; an App provides curated consumer distribution**

**Explanation:** Authors collaborate in Workspaces, while Apps provide a controlled consumption experience for broader audiences.

</details>

### 🔴 Q11. Why should Refresh History be checked after configuring refresh?

A. To confirm refresh succeeded and diagnose failures <br>
B. To create a new DAX measure <br>
C. To rank Products <br>
D. To hide a report page <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. To confirm refresh succeeded and diagnose failures**

**Explanation:** Refresh History records the status of refresh attempts and is essential for operational validation.

</details>

### 🔴 Q12. What is the recommended enterprise flow taught in this section?

A. Publish → Refresh → Secure → Share <br>
B. Share → Delete → Rebuild → Ignore Security <br>
C. Format → Export → Delete Model → Publish <br>
D. Create Chart → Remove Data → Share Password <br>

<details>
<summary><b>Answer & Explanation</b></summary>

**Answer: A. Publish → Refresh → Secure → Share**

**Explanation:** The session teaches a controlled path from authoring to reliable and secure enterprise consumption.

</details>

---

### ➡️ Next Session

**Section 12 — Capstone, AI/Copilot and Course Consolidation**

Learners will consolidate the full Power BI workflow, complete a capstone reporting scenario, review the key concepts from Sections 01–11, and explore appropriate AI/Copilot-assisted reporting workflows.
