# Product Demand Segmentation & Time-Window Merchandising (Grocery eCommerce)

## Project Background
**Instacart** is an online grocery marketplace where repeat behavior and timing drive revenue. Stakeholders lacked clarity on **when** customers order and which items to market. This project **segmented customers** by purchase cadence, identified **peak ordering windows**, and uncovered reliable **product complements** to guide merchandising and messaging. Scope: BigQuery + Tableau on **~3.3M orders** (day/hour × product × segment) with market-basket analysis.

[links to the technical parts, including ERD - intent to separate it from the main ReadMe]

The interactive dashboard can be seen [here] 

## Executive Summary
We aim to grow weekly orders **without discounts** by showing the right products to the right customers at the right time. Using **SQL (BigQuery)** and **Tableau Public**, I built an interactive dashboard (orders by **segment, hour, day, product, and KPIs**) and quantified **peak windows**. 42% of orders come from **Bi-weekly shoppers**, with most activity **8am–6pm** on **Sun/Mon/Tue**, concentrated in **Produce**.

## Business Problem
Grocery demand is routine-driven and time-sensitive. Treating every shopper and hour the same leaves revenue on the table. This work pinpoints when orders cluster, what products dominate, and who (by frequency segment) is most responsive—so marketing and operations can act where it matters most.

## Methodology
- **Build clean views**: Two BigQuery tables—(1) **orders_core**: order_id, user_id, day, hour, and frequency_segment; (2) **order_products_core**: order_id, product_name, department_name. Segmented users by avg days-since-prior-order (**Weekly ≤7**, **Bi-weekly ≤14**, else **Monthly**).
- **Analyze & visualize**: Counted distinct orders by **day×hour×segment**, and ranked top products in a Tableau dashboard where all charts cross-filter and update shared KPIs (**Users, Orders, Avg Orders/User**).
- **Prioritize actions**: Identified **peak windows** and **universal complements** to inform placements, and lifecycle and in-cart suggestions; outlined a simple A/B to measure lift (quantify the increase from time-boxed placements + cohort-timed nudges + cart complements).

## Skills
- **Tableau Public**: Relationships on order_id, interactive filter actions, KPIs, heatmaps/lines/bars, and basic table calculations.
- **Analytics & Communication**: KPI definition, experiment framing (A/B with holdout), stakeholder-ready storytelling.

## Results
The self-serve dashboard (segment × day × hour × product + KPIs) gives instant visibility and reduces ad-hoc tasks. Analysis shows **Bi-weekly shoppers** drive 42% of orders, with peaks **Sun/Mon/Tue 8am–6pm** in Produce. A simple what-if indicates that a +7–12% uplift inside that window yields **~+3–5%** overall weekly orders.

## Recommendations
<img width="1190" height="853" alt="image (3)" src="https://github.com/user-attachments/assets/622c1130-cefb-4c6f-a1a8-b134e1551dd1" />

Feature **Produce** leaders during the peak hours, send timed **suggestions** to routine shoppers, and emphasize **cart complements** (notably **Organic Baby Spinach** and **Organic Strawberries**) at add-to-cart/checkout. **Expected impact: ~3–5% lift in weekly orders** over 4–6 weeks, to be validated with an A/B (holdout) test.
1. **Time-boxed merchandising (no discounts)**:
   - On Sun/Mon/Tue 8:00–18:00, feature Produce leaders on homepage/search/category.
   - Promote two universal complements alongside the most popular items: Organic Baby Spinach and Organic Strawberries.
2. **Lifecycle suggestions (cohort-timed, no discounts)**:
   - Weekly cohort: send T+7 (late morning) with last-order staples prefilled.
   - Bi-weekly cohort: send T+14 (late morning), same prefill approach.
3. **Cart complements (in-cart & checkout)**:
   - When an anchor (e.g., Banana, Bag of Organic Bananas, or Organic Hass Avocado) is added, suggest Organic Baby Spinach and/or Organic Strawberries (suppress if already in cart; respect stock).
   - Cap suggestions at two to reduce banner fatigue.
4. **Ops alignment**:
   - Staff picking and prioritizing inventory checks for highlighted departments during Sun/Mon/Tue afternoons.

## KPIs to monitor (A/B)
1. **Primary**: Orders per user per week.
2. **Secondary**: 
   - Attach rate on suggested items, 
   - Reorder rate on targeted SKUs, and
   - Items/order, CTR (click-through rate)→ conversion within 24h of suggestion.

**Next Steps**
- Run a 4–6 week A/B across 2–3 regions comparing time-boxed placements + cohort nudges vs. holdout (control group).
- Extend segmentation to RFM-style scores; optionally add a simple reorder propensity model to prioritize targets.
- Broaden complement rules (market-basket associations).
- If price/cost becomes available, track AOV and margin impact; otherwise use item count as proxy.
- Note limitations (public dataset; no price/cost/geo). Consider a pipeline with dbt/Snowflake.

[here]: https://public.tableau.com/app/profile/pedro.vinhais/viz/Instacart-CustomerSegmentationandSalesAnalysis/Dashboard1
