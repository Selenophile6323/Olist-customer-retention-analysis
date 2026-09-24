# Olist Customer Retention Analysis

## Business Problem
Olist is a Brazilian e-commerce marketplace connecting small sellers to
customers. This project investigates customer retention: how many
customers return for a second purchase, and what distinguishes
repeat buyers from one-time buyers.

## Data
Public Olist e-commerce dataset (Sept 2016 – Oct 2018), 9 relational
tables covering ~99K orders, customers, products, payments, and reviews.

## Key Findings
- Of 99,441 order-level customer records, only 96,096 correspond to
  unique people (`customer_unique_id`) — some customers placed
  multiple orders.
- Of those, only **2.9% ever placed a second order.** Retention at
  Olist is not a "some customers churn" problem — it's a structural
  one-time-purchase pattern across the marketplace.
- Repeat customers who do return typically do so within ~34 days
  (median), with a 90th-percentile gap of 265 days — this was used
  as the churn threshold for classifying "active" vs "lapsed" repeat
  customers.
- RFM segmentation (Recency, Frequency, Monetary) confirmed this:
  only 122 customers qualify as "Champions" and 69 as "At Risk
  (was loyal)" out of 93,358 — consistent with the recency-based
  status classification done independently.

## Methodology
1. Filtered to delivered orders only (96,478 of 99,441 — excluded
   canceled/unavailable orders as non-completed purchases)
2. Merged orders, order items, and payments to get order-level value,
   then rolled up to one row per unique customer
3. Calculated Recency, Frequency, Monetary metrics per customer
4. Classified customers into Active Repeat / Churned Repeat /
   One-time (Recent) / One-time (Lapsed) using a data-driven
   recency threshold (90th percentile of repeat-purchase gaps)
5. Built RFM scores (1–5) and mapped them to named segments
   (Champions, At Risk, Lost, etc.) — Frequency was scored manually
   rather than by quintile, since ~93% of customers share the same
   order count, which breaks quintile-based binning
6. Exported the customer-level table for dashboarding in Power BI

## Tools
Python (pandas, matplotlib) for data cleaning and analysis, Power BI
for the interactive dashboard *(in progress)*.

## Limitations
- One-time buyers were classified as "recent" vs "lapsed" using a
  threshold derived from repeat-buyer behavior, as a simplifying
  assumption — this may not perfectly reflect their actual return
  likelihood.
- "Churn" here is a recency-based proxy, not a true cancellation
  event, since Olist has no subscription/membership structure.

## Status
Data cleaning, segmentation, and Python analysis complete.
Power BI dashboard in progress.