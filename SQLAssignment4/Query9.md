## 9. Shipping Revenue (Last Month)
## Business Problem:
### Finance also needs to know how much was earned from shipping charges in the same period, often a subset of overall revenue.

## Fields to Retrieve:

1.TOTAL ORDER
2.TOTAL_SHIPPING_REVENUE
3.MONTH
```sql
Solution:-
select count(oa.order_id) as TotalOrders,
       sum(oa.amount) as TotalShippingRevenue,
       DATE_FORMAT(CURDATE() - INTERVAL 1 MONTH, '%M') as Month
from Order_Adjustment oa 
JOIN Order_Header oh on oh.order_id = oa.order_id
where oa.order_adjustment_type_id = 'SHIPPING_CHARGES' and
      oh.order_date BETWEEN DATE_FORMAT(CURDATE() - INTERVAL 1 MONTH, '%Y-%m-01') and
	  LAST_DAY(CURDATE() - INTERVAL 1 MONTH)
group by oa.order_adjustment_type_id;


```
