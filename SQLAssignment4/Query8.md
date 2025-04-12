## 8. Shipping Refunds (Last Month)
## Business Problem:
### The finance department needs to confirm the total value of shipping refunds processed last month to measure potential overages or carrier-related service issues.

## Fields to Retrieve:

1.RETURN_ADJUSTMENT_ID
2.ORDER_ID
3.REFUND_AMOUNT
4.REFUND_REASON_CODE
5.REFUND_DATE
6.CUSTOMER_ID
```sql
Solution:-
select distinct ra.return_adjustment_id,
       ri.order_id,
       ra.amount as RefundAmount,
       ri.return_reason_id as ReturnReasonCode,
       rs.status_datetime as RefundDate,
       rh.from_party_id
from Return_Adjustment ra 
JOIN Return_Header rh on rh.return_id = ra.return_id
JOIN Return_Item ri on ri.return_id = rh.return_id
JOIN return_status rs on rs.return_id = rh.return_id
where rh.status_id = 'RETURN_COMPLETED' and (rs.status_datetime >= DATE_FORMAT(CURDATE() - INTERVAL 1 MONTH, '%Y-%m-01')
AND rs.status_datetime < DATE_FORMAT(CURDATE(), '%Y-%m-01'));
```
![image](https://github.com/user-attachments/assets/8e4ebc2c-522c-4fba-a909-625d2691322a)
