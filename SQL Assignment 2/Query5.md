## 5. Lost and Damaged Inventory
## Business Problem:
### Warehouse managers need to track “shrinkage” such as lost or damaged inventory to reconcile physical vs. system counts.

## Fields to Retrieve:

1. INVENTORY_ITEM_ID
2. PRODUCT_ID
3. FACILITY_ID
4. QUANTITY_LOST_OR_DAMAGED
5. REASON_CODE (Lost, Damaged, Expired, etc.)
6. TRANSACTION_DATE

## Solution:-
```sql
select ii.inventory_item_id,
       ii.product_id,
       ii.facility_id,
       iiv.variance_reason_id as reason_code,
       iiv.created_tx_stamp as Transaction_Date
from inventory_item_variance iiv
JOIN inventory_item ii on ii.inventory_item_id = iiv.inventory_item_id
where iiv.variance_reason_id = 'VAR_LOST' or iiv.variance_reason_id = 'VAR_DAMAGED';

```
![image](https://github.com/user-attachments/assets/47d57a30-91f4-40f8-b936-15c3f96d6499)
