# Q3 - Total Monthly Revenue for 2023 (Delivered Orders Only)

## Question
Show the total revenue for each month in 2023, considering only orders with status 'Delivered'.

## Your Initial Query
```sql
SELECT DATE_TRUNC('month', o.order_date)::date AS date, SUM(oi.total_price) AS total_revenue
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
WHERE o.status = 'Delivered'
AND order_date >= '2023-01-01'
AND order_date < '2024-01-01'
GROUP BY o.order_date
ORDER BY o.order_date;
```

**Issue:**  
You grouped by `o.order_date` instead of the truncated month, which caused the result to show daily rows instead of monthly totals.

---

## Corrected Query
```sql
SELECT DATE_TRUNC('month', o.order_date)::date AS month, SUM(oi.total_price) AS total_revenue
FROM orders o
JOIN order_items oi ON o.order_id = oi.order_id
WHERE o.status = 'Delivered'
AND o.order_date >= '2023-01-01'
AND o.order_date < '2024-01-01'
GROUP BY DATE_TRUNC('month', o.order_date)
ORDER BY month;
```

---

## Notes
- Used `DATE_TRUNC('month', o.order_date)` in both **SELECT** and **GROUP BY** to aggregate correctly per month.
- Casting to `::date` makes the output cleaner without timestamp.
- Ensured the `WHERE` clause filters the year 2023 only.
- This query gives a single row per month with the total revenue for delivered orders.
