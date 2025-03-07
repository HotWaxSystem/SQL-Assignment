## 7. Retrieve the Current Facility (Physical or Virtual) of Open Orders
## Business Problem:
### The business wants to know where open orders are currently assigned, whether in a physical store or a virtual facility (e.g., a distribution center or online fulfillment location).

## Fields to Retrieve:

1. ORDER_ID
2. ORDER_STATUS
3. FACILITY_ID
4. FACILITY_NAME
5. FACILITY_TYPE_ID

## Solution:-
```sql
SELECT oh.order_id,
       oh.status_id AS order_status,
       oisg.facility_id,
       f.facility_name,
       ft.parent_type_id as FacilityTypeId
FROM order_header oh
JOIN order_item_ship_group oisg ON oisg.order_id = oh.order_id
JOIN facility f ON oisg.facility_id = f.facility_id
JOIN facility_type ft ON ft.facility_type_id = f.facility_type_id
WHERE oh.status_id !='ORDER_COMPLETED' AND oh.status_id !='ORDER_CANCELLED';

```
![image](https://github.com/user-attachments/assets/f198bb95-e90c-48fc-a1a5-5db4495dc6db)
