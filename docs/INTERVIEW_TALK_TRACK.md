# Interview Talk Track (60–90 seconds)

I built a Power BI report to evaluate retail **performance and profitability**, with a specific focus on **repeat customer behavior** and **discount effectiveness**.  
The model uses a clean **star schema** with `FactSales` at the transaction grain and conformed dimensions for **Date**, **Product**, and **Customer** to keep slicing consistent and avoid ambiguous filters.

On top of the model, I created a small set of reusable DAX measures—revenue, profit, margin, customer counts, repeat rate, and discount metrics like **Weighted Discount**. Weighted Discount is revenue-weighted so the discount rate reflects business impact rather than being skewed by small orders.

The key insight is that discounting is not uniformly beneficial: profit is strong at low discount levels but becomes negative at aggressive discounting. For example, **≤20% discount profit is ≈ +$421.77K**, while **>40% discount profit is ≈ -$99.56K**, and **Discount-Weighted Profit is ≈ -$61.34K**.  
Business recommendation: use this view to set guardrails—protect margin by limiting deep discounting to specific products or scenarios where it’s justified by volume, and monitor product outliers using the discount scatter (Weighted Discount vs Profit, sized by Revenue).

## Likely Interview Questions (with short answers)

1) **Why a star schema instead of a flatter model?**
- Clear grain and relationships, fewer ambiguous filter paths, faster measures, and easier maintenance as dimensions grow.

2) **How did you define “Repeat Customer”?**
- Distinct customers with **>1 transaction** within the selected context (time filters apply via `DimDate`).

3) **Why use Weighted Discount rather than average discount?**
- A simple average can overemphasize small orders; revenue-weighting aligns the metric with financial impact.

4) **How did you validate the discount insight?**
- Compared profit totals across discount bands (≤20%, 20–40%, >40%) and checked product-level outliers in the scatter view.

5) **What would you do next if this were a live business report?**
- Add a promotion dimension, incorporate inventory/cogs details if available, track cohorts/retention over time, and evaluate elasticity by category.

6) **What are the limitations of the forecast shown?**
- It uses **Power BI native forecasting**, which is a built-in feature—not a custom statistical/ML model—and should be treated as directional.
