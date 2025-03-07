## 3. Top-Selling Product in New York
## Business Problem:
### Merchandising teams need to identify the best-selling product(s) in a specific region (New York) for targeted restocking or promotions.

## Fields to Retrieve:

1. PRODUCT_ID
2. INTERNAL_NAME
3. TOTAL_QUANTITY_SOLD
4. CITY / STATE (within New York region)
5. REVENUE (optionally, total sales amount)

## Solution:-
```sql
select p.product_Id,
       p.internal_name,
       sum(oi.quantity) as Total_Quantity_Sold,
       pa.city,
       pa.state_province_geo_id,
       sum(oi.unit_price * oi.quantity) as Revenue
from Product p 
JOIN Order_Item oi on oi.product_id = p.product_id
JOIN Order_Contact_Mech ocm on ocm.order_id = oi.order_id
JOIN postal_address pa ON pa.contact_mech_id = ocm.contact_mech_id
where pa.state_province_geo_id = 'NY' 
AND oi.status_id = 'ITEM_COMPLETED' 
GROUP BY p.product_id,pa.city;
