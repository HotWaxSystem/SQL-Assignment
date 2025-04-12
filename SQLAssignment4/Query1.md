## 1. Total Shipments in January 2022
## Business Problem:
### Logistics managers want to see how many shipments went out at the start of 2022. This helps assess shipping volumes and plan for post-holiday periods.

## Fields to Retrieve:

1.SHIPMENT_ID
2.SHIPMENT_DATE
3.FACILITY_ID
4.ORDER_ID

## Solution:-
```sql
select s.shipment_id,
       ss.status_date as ShipmentDate,
       s.origin_facility_id as FacilityId,
       s.primary_order_id as OrderId
from Shipment s 
JOIN Shipment_Status ss on ss.shipment_id = s.shipment_id
where ss.status_id = 'SHIPMENT_SHIPPED' and ss.status_date BETWEEN '2022-01-01' AND '2022-01-31';

```
![image](https://github.com/user-attachments/assets/3f7a2c22-3390-4100-b181-3750e8375261)
