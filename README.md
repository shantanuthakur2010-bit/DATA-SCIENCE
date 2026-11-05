# Olist E-Commerce Analysis: Why Do Orders Get Bad Reviews?

A pandas project on the Brazilian Olist marketplace data. The question: **what drives bad customer reviews, and how can the operations team reduce them?**

## Dataset
[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) on Kaggle. The raw files are not included in this repo, so download them from Kaggle and place them in a `data/` folder.

## What I did
1. **Cleaning:** converted date columns to datetime, kept only delivered orders, dropped delivered orders with no delivery date (99,441 → 96,470 orders).
2. **Key checks:** found the unique key of each table and found which tables have many rows per order.
3. **Fixing duplicates:** reduced reviews, items and payments to one row per order (median review score, total price and shipping, total payment) to avoid row duplication when merging.
4. **Merging:** joined customers, items, payments and reviews onto the delivered orders, checking the row count after every merge. Dropped orders with no review or no payment (final: 95,823 orders).
5. **New columns:** delivery days, delay days, delay status (early / on time / late), order value, freight ratio.
6. **Analysis:** groupby, named aggregations, percentage change, and difference between months.

## Key findings
1. **Late delivery is concentrated in the northeast.** AL, MA, SE, PI and CE have late rates of about 14% to 21%, against 6.7% overall.
2. **Late orders are strongly linked to bad reviews.** They are only 6.7% of orders but 32% of bad reviews (about 5 times their share). Average review score is about 4.2 for early or on-time orders and about 2 for late orders.
3. **Revenue grew through 2017 and then levelled off in 2018.** Biggest growth in percentage: Feb 2017 (+113.8% over Jan 2017). Biggest growth in amount: Nov 2017 (about +399k, Black Friday).
4. **Growth came from the number of orders, not bigger orders.** Monthly orders grew from [741] to over [6,000], while the average order value stayed around [155 to 170]. The top 10 customers make up under 0.5% of revenue, and most of them bought only once.

## Recommendation
Set up fulfillment hubs or carrier partnerships near the northeast, and set more realistic estimated delivery dates for those states. Distance from the southeast sellers is the likely reason, but this data alone does not prove it.

## Notes and limitations
- The analysis covers only delivered orders that have a review and a payment record.
- Delay is measured in whole calendar days, so an order delivered on the estimated day counts as on time.
- Currency is Brazilian reais (BRL).
- Months with very few orders (late 2016) were excluded from the growth comparison.

## Tools
Python, pandas, NumPy, Jupyter

## Files
- `1_cleaning_and_merging.ipynb`
- `2_analysis.ipynb`
