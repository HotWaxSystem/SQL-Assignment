## 4. Brokered but Not Shipped Orders
## Business Problem:
### Merchandising teams need to track orders that have been brokered (allocated to a facility) but not shipped. They also want to know how long it has been since the order was brokered.

## Fields to Retrieve:

1.ORDER_ID
2.BROKERED_DATE
3.BROKERED_FACILITY_ID
4.SHIPMENT_STATUS
5.TIME_SINCE_BROKERING
```sql
Solution:-
select oisgir.order_id,
       ii.datetime_received as BrokeredDate,
       ii.facility_id as BrokeredFacilityId,
       s.status_id as ShipmentStatus,
       DATEDIFF(CURDATE(), ii.datetime_received) as TimeSinceBrokering
from Order_Item_Ship_Grp_Inv_Res oisgir
JOIN Inventory_Item ii on ii.inventory_item_id = oisgir.inventory_item_id
JOIN Order_Shipment os on os.order_id = oisgir.order_id
JOIN Shipment s on s.shipment_id = os.shipment_id
where s.status_id != 'SHIPMENT_SHIPPED';

```
