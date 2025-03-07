## 8. Payment Captured but Not Shipped
## Business Problem:
### Finance teams want to ensure revenue is recognized properly. If payment is captured but no shipment has occurred, it warrants further review.

## Fields to Retrieve:

1. ORDER_ID
2. ORDER_STATUS
3. PAYMENT_STATUS
4. SHIPMENT_STATUS

## Solution:-
```sql
select oh.order_id, 
       oh.status_id AS Order_Status,
       opp.status_id AS Payment_Status,
       s.status_id AS Shipment_Status
from Order_Header oh 
JOIN order_payment_preference opp on opp.order_id = oh.order_id
JOIN order_shipment os on os.order_id = oh.order_id
JOIN shipment s on s.shipment_id = os.shipment_id
where s.status_id != 'SHIPMENT_SHIPPED' AND opp.status_id = 'PAYMENT_SETTLED' or s.status_id is null;

```
