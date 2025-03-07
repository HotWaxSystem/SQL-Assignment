## 1. Completed Sales Orders (Physical Items)
## Business Problem:
### Merchants need to track only physical items (requiring shipping and fulfillment) for logistics and shipping-cost analysis.

## Fields to Retrieve:

1. ORDER_ID
2. ORDER_ITEM_SEQ_ID
3. PRODUCT_ID
4. PRODUCT_TYPE_ID
5. SALES_CHANNEL_ENUM_ID
6. ORDER_DATE
7. ENTRY_DATE
8. STATUS_ID
9. STATUS_DATETIME
10. ORDER_TYPE_ID
11. PRODUCT_STORE_ID

## Solution:-
```sql
SELECT DISTINCT oi.order_id,
       oi.order_item_seq_id,
       oi.product_id,
       p.product_type_id,
       oh.sales_channel_enum_id,
       oh.order_date,
       oh.entry_date,
       oh.status_id,
       CAST(os.status_datetime AS DATE) AS status_date_time,
       oh.order_type_id,
       oh.product_store_id
FROM order_header oh 
JOIN order_item oi ON oh.order_id = oi.order_id
JOIN product p ON p.product_id = oi.product_id
JOIN order_status os ON os.order_id = oh.order_id
JOIN product_type pt ON p.product_type_id = pt.product_type_id
WHERE pt.is_physical = 'Y' 
AND oh.status_id = 'ORDER_COMPLETED' 
AND oh.order_type_id = 'SALES_ORDER';

```
