## 7. Store with Most One-Day Shipped Orders (Last Month)
## Business Problem:
### Identify which facility (store) handled the highest volume of “one-day shipping” orders in the previous month, useful for operational benchmarking.

## Fields to Retrieve:

1. FACILITY_ID
2. FACILITY_NAME
3. TOTAL_ONE_DAY_SHIP_ORDERS
4. REPORTING_PERIOD

## Solution:-
```sql
SELECT oisg.facility_id,
      f.facility_name,
      count(oisg.order_id) as TOTAL_ONE_DAY_SHIP_ORDERS,
      concat(min(oh.entry_date), ' to ', max(oh.entry_date)) as date_range
FROM order_header oh JOIN order_item_ship_group oisg ON oh.order_id=oisg.order_id 
JOIN facility f ON f.facility_id=oisg.facility_id
JOIN order_shipment os ON os.order_id=oisg.order_id
JOIN shipment s ON s.SHIPMENT_ID=os.SHIPMENT_ID
WHERE month(oh.entry_date)=month(current_Date)-1
AND year(oh.entry_date)=year(current_date)-1
AND oisg.shipment_method_type_id='NEXT_DAY'
AND s.STATUS_ID='SHIPMENT_SHIPPED'
Group by oisg.facility_id
order by TOTAL_ONE_DAY_SHIP_ORDERS desc;

```
![image](https://github.com/user-attachments/assets/0a5a8335-bae1-4960-bacb-cca554d600f9)
