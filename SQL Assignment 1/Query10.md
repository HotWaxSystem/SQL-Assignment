## 10. BOPIS Orders Revenue (Last Year)
## Business Problem:
### BOPIS (Buy Online, Pickup In Store) is a key retail strategy. Finance wants to know the revenue from BOPIS orders for the previous year.

## Fields to Retrieve:

1. TOTAL ORDERS
2. TOTAL REVENUE

## Solution:

```sql
select count(oh.order_id) as total_order, 
       sum(oh.grand_total) as total_Revenue
from order_header oh
JOIN order_item_ship_group oisg  on oisg.order_id = oh.order_id
where oisg.shipment_method_type_id = 'STOREPICKUP' 
and YEAR(oh.order_date)=YEAR(current_date())-1;

```
