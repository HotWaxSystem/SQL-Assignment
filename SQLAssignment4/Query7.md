## 7. Single-Item Orders Fulfilled from Warehouses (Last Month)
## Business Problem:
### Identify how many single-item orders were fulfilled from warehouse facilities in the previous month, to assess picking/packing efficiency.

## Fields to Retrieve:

1.ORDER_ID
2.TOTAL_ORDER_ITEMS
3.FACILITY_ID
4.SHIPMENT_ID
5.SHIPMENT_DATE
6.ORDER_COMPLETION_DATE

```sql
Solution:-

select distinct os.order_id,
       oisg.facility_id,
       os.shipment_id,
       ss.status_date as ShipmentDate,
       ors.status_datetime as OrderCompletionDate
from Order_Shipment os
JOIN Order_Item_Ship_Group oisg on oisg.order_id = os.order_id
JOIN Facility f on f.facility_id = oisg.facility_id
JOIN Shipment_Status ss on ss.shipment_id = os.shipment_id
JOIN Order_Status ors on ors.order_id = os.order_id
where ss.status_id = 'SHIPMENT_SHIPPED' and 
      ors.status_id = 'ORDER_COMPLETED' and 
      f.facility_type_id LIKE '%WAREHOUSE';

```
