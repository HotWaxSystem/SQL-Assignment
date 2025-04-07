## 5. Multi-Item Orders (Single Ship Group)
## Business Problem:
### For analyzing shipping efficiency, some businesses want to know which multi-item orders (more than one product) were fulfilled in one shipment (same ship group).

## Fields to Retrieve:

1.ORDER_ID
2.TOTAL_ITEMS_IN_ORDER
3.SHIP_GROUP_SEQ_ID
4.SHIPMENT_ID
5.FACILITY_ID
6.SHIPMENT_DATE

```sql
Solution:-
select os.order_id,
       count(os.ship_group_seq_id) as TotalItemsInOrders,
       os.ship_group_seq_id as ShipGroupSeqId,
       os.shipment_id,
       oisg.facility_id,
       ss.status_date as ShipmentDate
from Order_Shipment os
JOIN Order_Item_Ship_Group oisg on oisg.order_id = os.order_id
JOIN Shipment_Status ss on ss.shipment_id = os.shipment_id
where ss.status_id = 'SHIPMENT_SHIPPED'
group by os.order_id, os.ship_group_seq_id,os.shipment_id,oisg.facility_id,ss.status_date;

```
