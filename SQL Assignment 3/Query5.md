## 5. Detailed Return Information
## Business Problem:
### Certain teams need granular return data (reason, date, refund amount) for analyzing return rates, identifying recurring issues, or updating policies.

## Fields to Retrieve:

1. RETURN_ID
2. ENTRY_DATE
3. RETURN_ADJUSTMENT_TYPE_ID (refund type, store credit, etc.)
4. AMOUNT
5. COMMENTS
6. ORDER_ID
7. ORDER_DATE
8. RETURN_DATE
9. PRODUCT_STORE_ID

## Solution:-
```sql
select distinct rh.return_id,
       rh.entry_date,
       ra.return_adjustment_type_id,
       ra.amount,
       ra.comments,
       ri.order_id,
       oh.order_date,
       rh.return_date,
       oh.product_store_id
from return_header rh
JOIN return_item ri on ri.return_id = rh.return_id
JOIN Order_header oh on oh.order_id = ri.order_id
JOIN return_adjustment ra on ra.return_id = rh.return_id;

```
![image](https://github.com/user-attachments/assets/dee407eb-987d-43c3-acef-0088baff4d4e)
