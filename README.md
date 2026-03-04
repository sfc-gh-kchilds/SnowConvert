# College of Analytics and Migration HOL: Snowconvert HOL with SQL Server and AI
**Utilize Snowconvert to quickly understand the scope of your migration**

---

## 🛠️ Hands-On Lab Overview

In this hands-on lab, you'll step into the shoes of **Data Engineer** tasked with **Migrating from SQL Server to Snowflake**.

### 📋 What You’ll Do:
In this lab we will look at the Adventure Works database inside a SQL Server database. We will take a look at the catalog objects (tables, views) and some of the code that is there (stored procedures). Snowconvert will then extract that information and look for possible roadblocks to a migration and processes to consider. It will suggest some solutions but we will find out that the solutions it offers are not a best practice. This is where the GenAI integration of Snowflake Cortex will come into play to help us get possible solutions to this other than what SnowConvert generates programmatically.

We will then take those changes and migrate the structures as well as the data to our snowflake environment.

- **Task 1:** Connect to a SQL Server database and pull catalog information
- **Task 2:** Generate the input code from SQL Server
- **Task 3:** Understand the errors that SnowConvert surfaces
- **Task 4:** Resolve those errors using Cortex
- **Task 5:** Move the structure and the data to Snowflake

### ⏲️ Estimated Lab Timeline

- **Phase 1 (Env setup & model training):** ~10 min
- **[Phase 2 (Running the Migration)](/lab_instructions/readme.md):** ~30 min
- **[Phase 3 (Grading and validation)](/config):** ~5 min
  
---

## 📖 Table of Contents

- [Why this Matters](#-why-this-matters)
- [Suggested Discovery Questions](#-suggested-discovery-questions)
- [Repository Structure](#-repository-structure)
- [Prerequisites & Setup Details](#-prerequisites--setup-details)
- [Estimated Lab Timeline](#%EF%B8%8F-estimated-lab-timeline)
- [Troubleshooting & FAQ](#%EF%B8%8F-troubleshooting--faq)
- [Cleanup & Cost-Stewardship Procedures](#-cleanup--cost-stewardship-procedures)
- [Links to Internal Resources & Helpful Documents](#-links-to-internal-resources--helpful-documents)

---

## 📌 Why this Matters

- **Business value:** Migration is multifaceted, involving code, data structures, pipelines, and business logic. SnowConvert simplifies code and structure migration. The Snowpark Migration Assistant is intended to aid in pipeline conversions, offering a foundational step for a complex migration process. 
> SnowConvert provides a high-level overview of migration complexity, aiding customers in developing detailed migration plans and understanding the scope and effort required. Automated migration tools can underestimate the necessary work due to business rule and technology changes; simply replicating old processes in a new system is often insufficient. The effectiveness of SnowConvert depends on the quality of the data it analyzes and is typically not the only part of a migration to worry about but is a great place to get started
- **Pricing impact:** There is no cost to utilize this tool, the cost comes in the work done on the database and the storage of the new objects, but the tool itself is free to use

---

## ❓ Suggested Discovery Questions

- "How are you currently handling migrations from legacy systems to Snowflake?"
- "What metrics matter most when evaluating costs or complexity of a migration?"
- "Have you faced any security or compliance roadblocks with migrating sensitive data from legacy systems?"
- "How would you customize this pattern for your environment?"

---

## 📂 Repository Structure

```bash
├── README.md           # Main entry point
├── config             # DORA Setup
├── images             # Diagrams and visual assets
├── lab_instructions   # Step-by-step detailed instructions
│ ├── images           # Screenshots for the lab
└── troubleshooting/   # Common issues and resolutions
```
---

## ✅ Prerequisites & Setup Details

Internally helpful setup requirements:

- **Knowledge prerequisites:** Understanding of the goals, pipelines, sources, data size, frequency of updates, ETL patterns of the current environment
- **Account and entitlement checks:** None
- **Hardware/software:** This is a stand alone application you download and is only supported on Macs and Windows

---

## ⚠️ Troubleshooting & FAQ

Common errors and resolutions:

**Issue:** "Failed to prepare code processor for SqlServer" during conversion  
**Cause:** The `~/.config/Snowflake Inc` directory may be owned by root instead of your user account.  
**Solution:** Run the following commands to fix ownership:
```bash
sudo mkdir -p ~/.config/Snowflake\ Inc
sudo chown -R $(whoami) ~/.config/Snowflake\ Inc/
```

**Issue:** Cannot connect to the SQL Server source database  
**Cause:** You must be on a full-tunnel VPN to reach the lab SQL Server. Also, make sure you are entering the **SQL Server** URL (`snowconvert-datamigration.database.windows.net`), not your Snowflake account URL.  
**Solution:** Connect to one of the **RTF labeled VPN gateways** (full tunnel). Double-check you are entering the SQL Server connection details, not Snowflake credentials.

**Issue:** PAT (Personal Access Token) authentication fails or is truncated  
**Cause:** PAT authentication does not work reliably with SnowConvert.  
**Solution:** Use **Standard** authentication (username/password) for your Snowflake connection instead of PAT.

**Issue:** "Convert with AI" button does not work  
**Cause:** This feature is not functional in the current version of SnowConvert AI.  
**Solution:** Use the **"Convert code and ETL/BI projects"** option instead.

**Issue:** DatabaseLog table error during data migration  
**Cause:** The DatabaseLog table may fail to migrate due to XML data type conversion differences.  
**Solution:** This error can be safely ignored. The rest of the tables will migrate successfully.

**Issue:** DV10 data validation error  
**Cause:** The data validation feature is still in development and may produce errors.  
**Solution:** This is a known issue and can be ignored for the purposes of this lab.

For additional help, see the [SnowConvert FAQ](https://docs.snowconvert.com/sc/general/frequently-asked-questions-faq) or reach out on the Slack channels listed below.

---

## 🧹 Cleanup & Cost-Stewardship Procedures

🗑 **Cleanup Instructions:**
- Run the command in Snowflake after lab completion.
```sql
DROP database IF EXISTS AdventureWorks;
``` 
- You can optionally remove any folders locally that were created for the migration by SnowConvert

---


## 🔗 Links to Internal Resources & Helpful Documents

- [Snowflake Documentation](https://docs.snowflake.com/en/migrations/snowconvert-docs/general/getting-started/README)
- [Professional Services GTM Catalog](https://snowflake.seismic.com/Link/Content/DC4X82m96XPWcGWGMpCRMpMPW4p3)
- [Internal Wiki & Guidelines](#)

---

## 👤 Author & Support

**Originally created by:** Dan Murphy – SE Enablement Senior Manager  
**Updated by:** Kirsten Childs – SE Enablement  
**Created on:** July 23, 2025 | **Last updated:** March 2026

💬 **Need Help or Have Feedback?**  
- Slack Channel: [#college-of-analytics-and-migrations](https://snowflake.enterprise.slack.com/archives/C06R6B6MBNC)  
- Slack Channel: [#snowconvert-technical-support](https://snowflake.enterprise.slack.com/archives/C04QD2LN37H)

🌟 *We greatly value your feedback to continuously improve our HOL experiences!*
