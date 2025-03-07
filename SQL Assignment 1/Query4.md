## 4. Product IDs Across Systems
## Business Problem:
### To sync an order or product across multiple systems (e.g., Shopify, HotWax, ERP/NetSuite), the OMS needs to know each system’s unique identifier for that product. This query retrieves the Shopify ID, HotWax ID, and ERP ID (NetSuite ID) for all products.

## Fields to Retrieve:

1. PRODUCT_ID (internal OMS ID)
2. SHOPIFY_ID
3. HOTWAX_ID
4. ERP_ID or NETSUITE_ID (depending on naming)

## Solution:- 
```sql
SELECT 
    p.PRODUCT_ID as PRODUCT_ID,
    gi.ID_VALUE AS ERP_ID,
    p.PRODUCT_ID as Hotwax_ID,
    sp.shopify_product_id AS SHOPIFY_ID
FROM product p
LEFT JOIN good_identification gi ON p.PRODUCT_ID = gi.PRODUCT_ID 
JOIN shopify_product sp ON sp.product_id = p.product_id
where gi.id_value is not null and gi.good_identification_type_id='ERP_ID';

```

