# Q1 - Total Orders per Customer

**Question:**
Show each customer name, email, and the total number of orders they placed, ordered by total orders descending and then by name ascending.

**User Answer:**
```sql
SELECT c.name, c.email, COUNT(o.order_id) AS total_orders
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
ORDER BY total_orders DESC, c.name ASC;
```

**Notes & Corrections:**
✅ Correct JOIN logic.
⚠️ Missing `c.email` in GROUP BY clause (PostgreSQL requires all non-aggregated columns in SELECT to be grouped).
🔹 Suggested fix:
```sql
SELECT c.name, c.email, COUNT(o.order_id) AS total_orders
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name, c.email
ORDER BY total_orders DESC, c.name ASC;
```

