
# Q2 - Total Quantity Sold per Product (2023 Only)

## Question
**Show each product and the total quantity sold in 2023 for delivered orders only.**

## User's Answer
```sql
SELECT p.product_name, SUM(oi.quantity) AS total_quantity_sold 
FROM products p
JOIN order_items oi ON p.product_id = oi.product_id
JOIN orders o ON oi.order_id = o.order_id AND o.status = 'Delivered'
WHERE o.order_date >= '2023-01-01' AND o.order_date < '2024-01-01'
GROUP BY p.product_id, p.product_name
ORDER BY total_quantity_sold DESC;
```

## Notes
- The query correctly:
  - Filters for **Delivered** orders only.
  - Restricts to the **year 2023**.
  - Aggregates quantity sold per product.
  - Orders results by total quantity sold (descending).

- Good use of **GROUP BY** on both `product_id` and `product_name` to ensure uniqueness.
- Clear and clean SQL structure.

## Status
✅ Correct
