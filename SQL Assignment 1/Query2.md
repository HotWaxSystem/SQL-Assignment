## 2. List All Active Physical Products
## Business Problem:
### Merchandising teams often need a list of all physical products to manage logistics, warehousing, and shipping.

## Fields to Retrieve:

1. PRODUCT_ID
2. PRODUCT_TYPE_ID
3. INTERNAL_NAME
## Solution:-

```sql

select p.product_id, 
       p.product_type_id, 
       p.internal_name
FROM PRODUCT p 
JOIN PRODUCT_TYPE pt ON p.product_type_id = pt.product_type_id
where pt.is_physical='Y' and p.sales_discontinuation_date is null;

```
