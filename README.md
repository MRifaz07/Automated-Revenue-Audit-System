# Case Study: Regional Revenue Discrepancy Audit (100k Records)

## 📌 Step 1: The Problem (Scope & Objectives)
**Context:** Our regional partners submitted monthly revenue reports, but the totals did not align with our internal bank records.

**The Task:** Audit **100,000+ transactions** to identify where revenue was being misreported.

**The Goal:** Isolate the exact rows causing the mismatch, calculate the error percentage, and identify the **"Root Cause."**

---

## 🛠 Step 2: Data Consolidation (The SQL Phase)
To audit the data, I brought two separate datasets together into a single "Source of Truth."
* **Action:** Used **Pandas** to ingest raw CSVs and migrated them into a **SQL Sandbox (SQLite)**.
* **The Join:** Wrote an **INNER JOIN** query to compare internal truth vs. partner claims.
* **Technical Logic:** Used the `<>` (Not Equal To) operator to filter out matching records and only return the discrepancies.
  > `WHERE i.actual_revenue <> p.reported_revenue`



---

## 🐍 Step 3: Diagnostic Logic (The Python Script)
Instead of a manual review, I developed a Python script to perform the detection and categorization of the 10,000 flagged anomalies.
* **The Check:** Built a custom Python function `automated_triage` to scan the revenue gap.
* **The Math:** Used `abs(val)` (Absolute Value) to ensure both over-reporting and under-reporting were captured equally.
* **The Discovery:** The script identified exactly **10,000 rows** with errors, confirming a **10% discrepancy rate**.

---

## 🎯 Step 4: The Outcome (Business Impact)
* **Root Cause Analysis:** By **aggregating** the errors by region, I discovered that **100% of the discrepancies** were concentrated in the **South Region**.
* **Finding:** Identified that the South Region's reporting API was malfunctioning due to an outdated exchange rate.
* **The Result:** Delivered a **repeatable audit script** that ensures 100% data coverage. This moves the team from manual sampling to a comprehensive, script-based verification process.
