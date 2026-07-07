# Эталонные запросы

## 1. Покажи всех клиентов

### SQL

```sql
SELECT *
FROM customers;
```

### Ожидаемый результат

Список всех клиентов компании.

---

## 2. Сколько заказов было оформлено за май 2026 года?

### SQL

```sql
SELECT COUNT(*)
FROM orders
WHERE order_date BETWEEN '2026-05-01' AND '2026-05-31';
```

### Ожидаемый результат

Количество заказов за май 2026 года.

---

## 3. Кто из клиентов сделал больше всего заказов?

### SQL

```sql
SELECT
    c.company_name,
    COUNT(o.id) AS orders_count
FROM customers c
JOIN orders o ON c.id = o.customer_id
GROUP BY c.company_name
ORDER BY orders_count DESC;
```

### Ожидаемый результат

Рейтинг клиентов по количеству заказов.

---

## 4. Какие товары продаются лучше всего?

### SQL

```sql
SELECT
    p.name,
    SUM(oi.quantity) AS total_sold
FROM products p
JOIN order_items oi ON p.id = oi.product_id
GROUP BY p.name
ORDER BY total_sold DESC;
```

### Ожидаемый результат

Список товаров по объёму продаж.

---

## 5. Какие товары продаются хуже всего?

### SQL

```sql
SELECT
    p.name,
    SUM(oi.quantity) AS total_sold
FROM products p
JOIN order_items oi ON p.id = oi.product_id
GROUP BY p.name
ORDER BY total_sold ASC;
```

### Ожидаемый результат

Товары с наименьшим количеством продаж.

---

## 6. Какая категория товаров самая прибыльная?

### SQL

```sql
SELECT
    c.name,
    SUM(oi.quantity * oi.price) AS revenue
FROM categories c
JOIN products p ON c.id = p.category_id
JOIN order_items oi ON p.id = oi.product_id
GROUP BY c.name
ORDER BY revenue DESC;
```

### Ожидаемый результат

Категории товаров, отсортированные по выручке.

---

## 7. Кто из сотрудников принёс наибольшую выручку?

### SQL

```sql
SELECT
    u.full_name,
    SUM(pay.amount) AS revenue
FROM employees e
JOIN users u ON e.user_id = u.id
JOIN orders o ON e.id = o.employee_id
JOIN payments pay ON o.id = pay.order_id
GROUP BY u.full_name
ORDER BY revenue DESC;
```

### Ожидаемый результат

Рейтинг сотрудников по объёму продаж.

---

## 8. Какие товары заканчиваются на складе?

### SQL

```sql
SELECT
    p.name,
    i.quantity
FROM inventory i
JOIN products p ON p.id = i.product_id
WHERE i.quantity < 10;
```

### Ожидаемый результат

Товары с остатком менее 10 единиц.

---

## 9. На каком складе больше всего товаров?

### SQL

```sql
SELECT
    w.name,
    SUM(i.quantity) AS total_stock
FROM warehouses w
JOIN inventory i ON w.id = i.warehouse_id
GROUP BY w.name
ORDER BY total_stock DESC;
```

### Ожидаемый результат

Рейтинг складов по количеству товаров.

---

## 10. Выполнил ли сотрудник KPI?

### SQL

```sql
SELECT
    u.full_name,
    kt.target_sales,
    kr.actual_sales
FROM employees e
JOIN users u ON e.user_id = u.id
JOIN kpi_targets kt ON e.id = kt.employee_id
JOIN kpi_results kr
ON e.id = kr.employee_id
AND kt.month = kr.month;
```

### Ожидаемый результат

Сравнение плановых и фактических показателей.

---

## 11. Какие поставщики поставляют больше всего товаров?

### SQL

```sql
SELECT
    s.name,
    COUNT(p.id) AS products_count
FROM suppliers s
JOIN products p ON s.id = p.supplier_id
GROUP BY s.name
ORDER BY products_count DESC;
```

### Ожидаемый результат

Рейтинг поставщиков.

---

## 12. Покажи все товары категории "Laptops"

### SQL

```sql
SELECT p.name
FROM products p
JOIN categories c ON p.category_id = c.id
WHERE c.name = 'Laptops';
```

### Ожидаемый результат

Список ноутбуков.

---

## 13. Какие клиенты принесли наибольшую выручку?

### SQL

```sql
SELECT
    c.company_name,
    SUM(pay.amount) AS revenue
FROM customers c
JOIN orders o ON c.id = o.customer_id
JOIN payments pay ON o.id = pay.order_id
GROUP BY c.company_name
ORDER BY revenue DESC;
```

### Ожидаемый результат

Рейтинг клиентов по выручке.

---

## 14. Какие запросы чаще всего задают пользователи AI?

### SQL

```sql
SELECT
    question,
    COUNT(*)
FROM ai_query_history
GROUP BY question
ORDER BY COUNT(*) DESC;
```

### Ожидаемый результат

Наиболее популярные вопросы пользователей.

---

## 15. Какие сотрудники получили AI-уведомления?

### SQL

```sql
SELECT *
FROM ai_alerts;
```

### Ожидаемый результат

Список уведомлений, сформированных системой.
