## 10. Total Orders by Sales Channel
## Business Problem:
### Marketing and sales teams want to see how many orders come from each channel (e.g., web, mobile app, in-store POS, marketplace) to allocate resources effectively.

## Fields to Retrieve:

1. SALES_CHANNEL
2. TOTAL_ORDERS
3. TOTAL_REVENUE
4. REPORTING_PERIOD

## Solution:-
```sql
select oh.sales_channel_enum_id,
       count(oh.order_id) as total_orders,
       sum(oh.grand_total) as total_revenue,
       concat(MIN(DATE(oh.ORDER_DATE)), ' to ', MAX(DATE(oh.ORDER_DATE))) as reporting_period
from order_header oh
group by oh.sales_channel_enum_id;

```
![image](https://github.com/user-attachments/assets/9749bf23-dabe-4bae-93ef-2cba75185072)
