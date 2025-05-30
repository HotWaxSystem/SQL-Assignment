## 9. Order Item Current Status Changed Date-Time
## Business Problem:
### Operations teams need to audit when an order item’s status (e.g., from “Pending” to “Shipped”) was last changed, for shipment tracking or dispute resolution.

## Fields to Retrieve:

1. ORDER_ID
2. ORDER_ITEM_SEQ_ID
3. CURRENT_STATUS_ID
4. STATUS_CHANGE_DATETIME
5. CHANGED_BY

## Solution:-
```sql
select os.order_id,
    os.order_item_seq_id,
    os.status_id as Current_status_id,
    os.status_datetime as Status_change_datetime,
    os.status_user_login as Changed_by
FROM order_status os WHERE os.order_item_seq_id is not null;

```
![image](https://github.com/user-attachments/assets/c98471c2-8e15-4463-9b4a-329b30cbcfb6)
