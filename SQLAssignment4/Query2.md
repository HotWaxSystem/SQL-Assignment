## 2. Shipments by Tracking Number
## Business Problem:
### Customer Service often needs to look up shipments by tracking number to answer delivery queries quickly.

## Fields to Retrieve:

1.SHIPMENT_ID
2.ORDER_ID
3.TRACKING_NUMBER
4.SHIPMENT_DATE
5.CARRIER_PARTY_ID
6.SHIPMENT_STATUS

## Solution:-
```sql
select distinct s.shipment_id,
       s.primary_order_id as OrderId,
       srs.tracking_id_number as TrackingNumber,
       ss.status_date as ShipmentDate,
       srs.carrier_party_id,
       s.status_id as ShipmentStatus
from Shipment s 
JOIN Shipment_Status ss on ss.shipment_id = s.shipment_id
JOIN Shipment_Route_Segment srs on srs.shipment_id = s.shipment_id
where srs.TRACKING_ID_NUMBER = '794681786648';

```
