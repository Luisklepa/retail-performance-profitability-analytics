# Project Notes

- **Dataset assumptions**
  - This portfolio project may use a **synthetic dataset** (common for portfolio work). If your dataset is real, update this note accordingly.
  - Grain assumed: **one row per transaction line** (or transaction event) in `FactSales`.

- **Modeling notes**
  - Model follows a **star schema**: `FactSales` at the center with `DimDate`, `DimProduct`, `DimCustomer`.
  - `DimDate` is marked as the **Date table** in Power BI and is used for all time slicing/time intelligence.
  - Relationships are **1-to-many** from dimensions to fact with **single-direction filtering** (dimensions → fact).

- **Measure notes**
  - **Repeat Customers**: customers with **more than one transaction** (repeat logic based on transaction count per customer).
  - **Weighted Discount**: revenue-weighted discount rate to avoid small transactions skewing results.
  - **Discount-Weighted Profit**: profit weighted by discount pressure to summarize the net discount effect.

- **How insights were validated**
  - Discount impact was checked by comparing profit totals across discount bands:
    - **Low Discount Profit (≤20%)** vs **High Discount Profit (>40%)**
  - The product-level scatter was used to validate outliers where high discounting correlates with lower profit.
