## 6. Low Stock or Out of Stock Items Report
## Business Problem:
### Avoiding out-of-stock situations is critical. This report flags items that have fallen below a certain reorder threshold or have zero available stock.

## Fields to Retrieve:

1. PRODUCT_ID
2. PRODUCT_NAME
3. FACILITY_ID
4. QOH (Quantity on Hand)
5. ATP (Available to Promise)
6. REORDER_THRESHOLD
7. DATE_CHECKED

## Solution:
```sql
select p.product_id,
       p.product_name,
       ii.facility_id,
       ii.quantity_on_hand_total as QOH,
       ii.available_to_promise_total as ATP,
       pf.reorder_quantity as Reorder_Threshold,
       pf.last_updated_stamp as Date_Checked
from product p
JOIN Inventory_Item ii on ii.product_id = p.product_id
JOIN Product_facility pf on pf.product_id = p.product_id
where pf.minimum_stock > ii.quantity_on_hand_total;

```
![image](https://github.com/user-attachments/assets/44b4de8d-f880-459b-a52f-ad7e75fba416)
