# Data

Raw source files used by `Sadıqov_Ədalət_project.ipynb`. All files are semicolon-delimited (`;`) CSVs from the Instacart online grocery ordering dataset.

## Files

### `instacart_orders.csv`
One row per order.

| Column | Type | Description |
|---|---|---|
| `order_id` | int | Unique order identifier |
| `user_id` | int | Customer identifier |
| `order_number` | int | Sequence number of this order for the customer (1 = first order) |
| `order_dow` | int | Day of week the order was placed (0–6) |
| `order_hour_of_day` | int | Hour of day the order was placed (0–23) |
| `days_since_prior_order` | float | Days since the customer's previous order. `NaN` for a customer's first order (`order_number == 1`) — capped at 30 |

478,967 rows (before duplicate removal — see main README for cleaning notes).

### `products.csv`
Product catalog.

| Column | Type | Description |
|---|---|---|
| `product_id` | int | Unique product identifier |
| `product_name` | str | Product name. Missing for 1,258 rows, all under `aisle_id=100` / `department_id=21` ("missing" bucket) |
| `aisle_id` | int | Foreign key → `aisles.csv` |
| `department_id` | int | Foreign key → `departments.csv` |

49,694 rows.

### `departments.csv`
Department lookup table.

| Column | Type | Description |
|---|---|---|
| `department_id` | int | Unique department identifier |
| `department` | str | Department name (e.g. `frozen`, `produce`, `alcohol`) |

21 rows.

### `aisles.csv`
Aisle lookup table.

| Column | Type | Description |
|---|---|---|
| `aisle_id` | int | Unique aisle identifier |
| `aisle` | str | Aisle name (e.g. `prepared soups salads`, `energy granola bars`) |

134 rows.

### `order_products.csv`
One row per product within an order (order line items).

| Column | Type | Description |
|---|---|---|
| `order_id` | int | Foreign key → `instacart_orders.csv` |
| `product_id` | int | Foreign key → `products.csv` |
| `add_to_cart_order` | int | Position in which the item was added to the cart. Sentinel value `999` used for 836 rows where the true position exceeded the source system's cap (min 65 items in those orders) |
| `reordered` | int | 1 if the customer has ordered this product before, 0 otherwise |

4,545,007 rows.

## Entity Relationships

```
departments ──┐
              ├──< products >── order_products ──< instacart_orders
aisles ───────┘
```

- `products.department_id` → `departments.department_id`
- `products.aisle_id` → `aisles.aisle_id`
- `order_products.product_id` → `products.product_id`
- `order_products.order_id` → `instacart_orders.order_id`

## Notes

- Delimiter is `;`, not `,` — use `sep=";"` when loading with pandas.
- `order_products.csv` is ~86 MB. GitHub allows files up to 100 MB via normal `git push`, but shows a warning above 50 MB. If it ever needs to grow past 100 MB (e.g. a larger data pull), switch to [Git LFS](https://git-lfs.com) instead of committing it directly.
- See the root [`README.md`](../README.md) for cleaning steps, missing-value handling, and analysis findings derived from these files.
