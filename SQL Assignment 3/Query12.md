## 12. Orders Without Picklist
## Business Problem:
### A picklist is necessary for warehouse staff to gather items. Orders missing a picklist might be delayed and need attention.

## Fields to Retrieve:

1. ORDER_ID
2. ORDER_DATE
3. ORDER_STATUS
4. FACILITY_ID
5. DURATION (How long has the order been assigned at the facility)

## Solution:-
```sql
select oh.order_id,
       oh.order_date,
       oh.status_id,
       oisg.facility_id,
       datediff(DATE(oh.entry_date),DATE(oh.entry_date)) as Duration
from Order_Header oh
JOIN Order_Item_Ship_Group oisg on oisg.order_id = oh.order_id
JOIN Picklist pi on pi.facility_id = oisg.facility_id
where pi.status_id is null;
```
![image](https://github.com/user-attachments/assets/9a6cf9ad-6ecb-452e-8329-8ef679b6c555)
