## 2. Completed Return Items
## Business Problem:
### Customer service and finance often need insights into returned items to manage refunds, replacements, and inventory restocking.

## Fields to Retrieve:

1. RETURN_ID
2. ORDER_ID
3. PRODUCT_STORE_ID
4. STATUS_DATETIME
5. ORDER_NAME
6. FROM_PARTY_ID
7. RETURN_DATE
8. ENTRY_DATE
9. RETURN_CHANNEL_ENUM_ID

## Solution:-
```sql
SELECT ri.return_id,
       ri.order_id,
       oh.product_store_id,
       (SELECT os.status_datetime FROM order_status os WHERE os.order_id=ri.order_id
       ORDER BY os.status_datetime desc limit 1) as status_datetime,
       oh.order_name,
       rh.from_party_id,
       rh.return_date,
       rh.entry_date,
       rh.return_channel_enum_id
FROM return_header rh
JOIN return_item ri ON rh.return_id=ri.return_id 
JOIN order_header oh ON oh.order_id=ri.order_id
where ri.status_id='RETURN_COMPLETED';

```
![image](https://github.com/user-attachments/assets/924e672c-6bfd-4672-8b74-cf687dfac4c3)
