# Charts

Static exports of the visualizations from `Sadıqov_Ədalət_project.ipynb`, rendered as PNG.

> Why static images? The notebook was built with interactive Plotly charts (`plotly.express` / `graph_objects`). GitHub's built-in notebook viewer does not execute JavaScript, so Plotly outputs display as blank cells when the notebook is opened on GitHub. These PNGs give a permanent, viewable record of every chart regardless of where the repo is viewed.

## Chart Index

| File | Chart | Key Takeaway |
|---|---|---|
| `01_orders_by_hour.png` | Order count by hour of day | Orders peak 10 AM–4 PM, minimal overnight activity |
| `02_orders_by_day_of_week.png` | Order count by day of week | Sunday & Saturday highest volume, midweek (Wed/Thu) lowest |
| `03_days_since_prior_order.png` | Days until the next order | Spike at 30 (top-coding); secondary spikes at 7/14/21/28 (weekly rhythm) |
| `04_wednesday_vs_saturday.png` | Wednesday vs Saturday hourly overlay | Both peak 10 AM–4 PM; Saturday flatter, Wednesday shows sharper 9–11 AM ramp-up |
| `05_orders_per_customer.png` | Total orders per customer | Right-skewed long tail — most customers order only a handful of times |
| `06_top20_ordered_products.png` | Top 20 most ordered products | Dominated by fresh produce (bananas, spinach, strawberries, avocado) |
| `07_items_per_order.png` | Distribution of items per order | Right-skewed, median basket size ≈ 8 items |
| `08_top20_reordered_products.png` | Top 20 most reordered products | Near-identical ranking to most-ordered — produce staples drive both volume and loyalty |
| `09_reorder_proportion_by_product.png` | Reorder proportion by product (50+ orders) | Most products cluster between 0.3–0.7 reorder rate |
| `10_reorder_proportion_by_customer.png` | Reorder proportion by customer | Wide spread — splits customers into "loyal repeaters" vs. "explorers" |
| `11_top20_first_added.png` | Top 20 items added to cart first | Banana leads by an even wider margin than in overall order count |

## Regenerating

These images are generated from `generate_charts.py` (not included in this repo by default — ask if you want the script added) using the raw CSVs in `../data/`. Re-run it any time the underlying data or notebook logic changes, so the images stay in sync with the analysis.

Full written interpretation of each chart is in the root [`README.md`](../README.md#key-findings).
