## 11. Canceled Orders (Last Month)
## Business Problem:
### The merchandising team needs to know how many orders were canceled in the previous month and their reasons.

## Fields to Retrieve:

1. TOTAL ORDERS
2. CANCELATION REASON

## Solution:-
```sql
select count(os.order_id) as total_order,
	   os.change_reason as cancellation_reason
from order_status os 
where os.STATUS_ID = 'ORDER_CANCELLED' 
AND os.status_datetime >= DATE_FORMAT(CURDATE() - INTERVAL 1 MONTH, '%Y-%m-01')
AND os.status_datetime < DATE_FORMAT(CURDATE(), '%Y-%m-01')
group by os.CHANGE_REASON;

```
