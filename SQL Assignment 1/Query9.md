## 9. Orders Completed Hourly
## Business Problem:
### Operations teams may want to see how orders complete across the day to schedule staffing.

## Fields to Retrieve:

1. TOTAL ORDERS
2. HOUR

## Solution:-
```sql
select count(order_id) as total_order,
       hour(Status_Datetime) as hr
from Order_Status os 
where status_id = 'Order_Completed' group by hr ORDER BY HR;

```

![image](https://github.com/user-attachments/assets/b7598098-edb1-485e-ac0c-2b2e9f53fec0)
