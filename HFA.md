# 📘 HFA – Detailed Walkthrough
> *From Manual Financial Analysis to Automated, Validated Financial Architecture*

## Overview

This document provides a detailed walkthrough of the **HFA (Historical Financial Analysis)** framework:

 *  How HFA was performed earlier.

 *  Why automation was required.

 *  How the current system works logically.

 *  What business and technical benefits are achieved.


# 🔴 Earlier Approach (Manual Process)

This document outlines the step-by-step manual workflow previously used for financial data extraction and analysis.

---

## 📅 Step-by-Step Manual Workflow

The previous process involved several laborious, manual steps to gather, align, and validate financial data from company filings.

### 1. Data Acquisition

The process began with individually sourcing the required filings:

*   Download 10-K / 10-Q PDFs for each reporting period.

### 2. Manual Data Location & Extraction

Key financial statements within the PDFs had to be located and copied manually:

*   Manually locate:
    *   Income Statement
    *   Balance Sheet
    *   Cash Flow Statement

*   Copy-paste tables into Excel.

### 3. Data Alignment & Calculation

Once the raw data was in Excel, significant manual effort was required to structure and analyze it:

*   Manually align line items across years.
*   Write Excel formulas for:
    *   Derived metrics
    *   Aggregations

### 4. Validation

The final step was a manual quality assurance process:

*   Manually validate numbers against prior years.

---

## 🚫 Summary of Limitations

This manual approach was time-consuming, prone to human error during data entry and alignment, and lacked scalability.

---
**📌 Key Risk:**
Even small formula changes caused **silent inaccuracies** across years.

---

🧱 **High-Level Architecture (ETL Flow)**



```mermaid

flowchart LR

    subgraph Historical Data
        A1[Excel 3Y Data] --> B1[Break Components]
        B1 --> C1[JSON Conversion]
    end

    subgraph SEC Data
        A2[Download 10-K/10-Q PDFs] --> B2[Extract Content]
        B2 --> C2[CSV Conversion]
    end

    subgraph Mapping Layer
        C1 --> D[Universal Mapping]
        C2 --> D
    end

    D --> I{Mapping Valid?}

    I -->|Yes| Z[Generate 2025 Excel from New 10-K/10-Q PDF]

    I -->|No| E[Run Unified Mapping Pipeline]
    E --> F[Mapping Fixed]
    F --> Z


```
--------------------------------------------------------------------------------------------------------------------

**Proposed Architecture Logical Layering:**

```mermaid
graph TD
    %% Define the style for the blocks (rectangles)
    classDef layer fill:#4a90e2,stroke:#333,stroke-width:2px,color:#fff;

    %% Define the nodes (layers)
    A([Data Ingestion Layer])
    B([Data Processing Layer])
    C([Data Mapping and Validation Layer])
    D([Data Output])

    %% Define the flow (arrows)
    A --> B
    B --> C
    C --> D

    %% Apply the style to the nodes
    class A,B,C,D layer;
```
-------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------

