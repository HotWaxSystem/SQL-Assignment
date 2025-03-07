## 10. Total Items in Various Virtual Facilities
## Business Problem:
### Virtual facilities (such as online-only fulfillment centers) handle a different inventory process. The company wants a snapshot of total stock across these virtual locations.

## Fields to Retrieve:

1. PRODUCT_ID
2. FACILITY_ID
3. FACILITY_TYPE_ID
4. QOH (Quantity on Hand)
5. ATP (Available to Promise)

## Solution:-
```sql
select ii.product_id,
       ii.facility_id,
       f.facility_type_id,
       ii.quantity_on_hand_total,
       ii.available_to_promise_total
from Inventory_Item ii
JOIN facility f on f.facility_id = ii.facility_id
JOIN facility_type ft on ft.facility_type_id = f. facility_type_id
where ft.parent_type_id = 'VIRTUAL_FACILITY';

```
![image](https://github.com/user-attachments/assets/8d809194-ffa6-454a-8e9f-9479c3a9ece0)
