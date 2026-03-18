# medical-billing-analytics-performance
Interactive Power BI dashboard for analyzing financial &amp; operational efficiency in a medical network.
# Medical Billing & Operational Efficiency Dashboard (2021–2025)

## 🎯 Project Objective
The goal of this project was to analyze the financial and operational health of a multi-specialty medical network. I focused on evaluating the **"Efficiency Gap"** across various insurance types (Lien vs. Workers' Comp) and benchmarking provider performance based on actual collection rates.

## 📊 Dashboard Overview (Screenshots)

*Note: Due to data confidentiality, the full .pbix file is available upon request. Below are the key pages representing the solution.*

### 1. Home Page & Strategic Insights
This page provides an executive overview of the network's financial portfolio and identifies key revenue risks.

![Home Page Screenshot]

**Key Insight:** Identified that the Lien segment, despite high billing volume, has a critically low **6% Collection Rate**, representing a major revenue leak.

### 2. Operational Flow & "Wednesday Peak" Analysis
This page analyzes capacity and patient visit dynamics to optimize clinic workflow.

![Operational Analytics Screenshot]

**Key Insight:** Discovered a recurring operational bottleneck on **Wednesday mornings (7 AM - 12 PM)**, causing administrative strain and faster visit times.

---

## 🛠️ Tech Stack & Technical Implementation

* **Tools:** Power BI Desktop, DAX, SQL.
* **Key Technique:** Implemented a **Bridge Table architecture** to eliminate "Double Counting" across 30+ locations, ensuring a **"Single Version of Truth."**

### 🛠️ Key DAX Implementation Highlights

To ensure data integrity and solve complex business logic, I implemented several advanced DAX measures:

#### 1. Advanced Data Modeling (Bridge Table & Inactive Relationships)
This measure is the core of the "Single Version of Truth" architecture. It activates a specific relationship in the model to correctly map billing data across multiple practices without double-counting.

```dax
Billed by Practice = 
CALCULATE(
    [Total_Billed],
    USERELATIONSHIP(Bridge_Cases_Practice[cases_id], Dim_Cases[case_id])
)
\```

#### 2. Business Logic Efficiency
Using the `DIVIDE` function to safely handle calculations and measure real-world collection performance.

```dax
Net_Collection_Rate = 
DIVIDE(
    [Total_Paid], 
    ([Total_Billed] - [Total Adjustment]), 
    0
)
\```

## 📖 Methodology & Glossary

# Financial KPIs
* **Billed Amount**: Total gross revenue invoiced to insurance partners.
* **Paid Amount**: Actual cash collected (Net Revenue).
* **Adjustment**: Contractual write-offs. High adjustments often indicate billing errors or poor insurance contracts.
* **Collection Rate**: Efficiency metric calculated as Paid / (Billed - Adjustment). It shows how much of the "collectible" money actually reached the bank.
* **Financial Risk Zone**: Any balance aged over 90 days.

# Insurance Categories:
* **WC (Workers' Comp)**: Coverage for work-related injuries. This is our most stable segment with the highest collection efficiency.
* **No-Fault (NF)**: Claims from auto accidents, paid regardless of who caused the crash.
* **PIP (Personal Injury Protection)**: Similar to No-Fault, it covers medical expenses after vehicle accidents.
* **Major Medical**: Standard health insurance. It shows high billing volume but requires careful monitoring due to significant contractual adjustments.
* **Lien**: Cases involving legal action. While billing volume is the highest here, payments are often delayed until legal settlements are reached.

# Data Integrity & Methodology
* **Bridge Table Architecture**: A structural model that eliminates "Double Counting," ensuring a Single Version of Truth across 30+ locations.
* **Efficiency Benchmark**: Comparing providers (like Dr. Steele or Dr. Dorri) against their Specialty Average, not just a flat list.
* **USERELATIONSHIP**: A DAX technique used to precisely map every dollar to the correct provider-practice intersection.
