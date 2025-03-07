## 8. Items Where QOH and ATP Differ
## Business Problem:
### Sometimes the Quantity on Hand (QOH) doesn’t match the Available to Promise (ATP) due to pending orders, reservations, or data discrepancies. This needs review for accurate fulfillment planning.

## Fields to Retrieve:

1. PRODUCT_ID
2. FACILITY_ID
3. QOH (Quantity on Hand)
4. ATP (Available to Promise)
5. DIFFERENCE (QOH - ATP)

## Solution:-
```sql
select ii.product_id,
       ii.facility_id,
       ii.quantity_on_hand_total,
       ii.available_to_promise_total,
       (ii.quantity_on_hand_total - ii.available_to_promise_total) as Difference
from Inventory_Item ii;

```
![image](https://github.com/user-attachments/assets/041f53a1-7e65-4205-93b2-13ecc9926589)
