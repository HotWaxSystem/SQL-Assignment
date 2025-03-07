## 5. Completed Orders in August 2023
## Business Problem:
### After running similar reports for a previous month, you now need all completed orders in August 2023 for analysis.

## Fields to Retrieve:

1. PRODUCT_ID
2. PRODUCT_TYPE_ID
3. PRODUCT_STORE_ID
4. TOTAL_QUANTITY
5. INTERNAL_NAME
6. FACILITY_ID
7. EXTERNAL_ID
8. FACILITY_TYPE_ID
9. ORDER_HISTORY_ID
10. ORDER_ID
11. ORDER_ITEM_SEQ_ID
12. SHIP_GROUP_SEQ_ID

## Solution:-
```sql

select p.product_id,
       p.product_type_id,
       oh.product_store_id,
       oi.quantity AS TotalQuantity,
       p.internal_name,
       f.facility_id,
       f.external_id,
       f.facility_type_id,
       orh.order_history_id,
       orh.order_id,
       orh.order_item_seq_id,
       orh.ship_group_seq_id
from Order_Header oh JOIN order_item oi ON oi.order_id=oh.order_id
JOIN product p ON p.product_id=oi.product_id 
JOIN order_history orh ON orh.order_id=oh.order_id
JOIN order_item_ship_group oisg ON oisg.ship_group_seq_id=orh.ship_group_seq_id and oisg.order_id=oh.order_id
JOIN facility f ON f.facility_id=oisg.facility_id 
JOIN order_status os ON os.order_id=oh.order_id
WHERE os.status_id='ORDER_COMPLETED' and date(os.status_datetime)>=date('2023-08-01') AND date(os.status_datetime)<=date('2023-08-31');   

```

