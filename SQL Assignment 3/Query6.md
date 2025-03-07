## 6. Orders with Multiple Returns
## Business Problem:
### Analyzing orders with multiple returns can identify potential fraud, chronic issues with certain items, or inconsistent shipping processes.

## Fields to Retrieve:

1. ORDER_ID
2. RETURN_ID
3. RETURN_DATE
4. RETURN_REASON
5. RETURN_QUANTITY

## Solution:-
```sql
SELECT distinct ri.order_id,
       ri.return_id,
       rh.return_date,
       ri.return_reason_id,
       ri.return_quantity
FROM return_item ri
JOIN return_header rh ON rh.return_id=ri.return_id
WHERE ri.order_id in(
SELECT order_id FROM return_item GROUP by order_id having count(order_id)>1)
ORDER BY ri.order_id,rh.return_date;

```
![image](https://github.com/user-attachments/assets/702e6f51-cbd6-4c45-ba02-9967d3047abc)
