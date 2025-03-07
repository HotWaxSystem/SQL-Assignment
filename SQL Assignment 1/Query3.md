## 3.Products Missing NetSuite ID
## Business Problem:
### A product cannot sync to NetSuite unless it has a valid NetSuite ID. The OMS needs a list of all products that still need to be created or updated in NetSuite.

## Fields to Retrieve:

1. PRODUCT_ID
2. INTERNAL_NAME
3. PRODUCT_TYPE_ID
4. NETSUITE_ID (or similar field indicating the NetSuite ID; may be NULL or empty if missing)

## Solution:-

```sql
select p.product_id,
       p.internal_name,
       p.product_type_id,
       gi.id_value AS NetSuite_Id
FROM PRODUCT p
LEFT JOIN GOOD_IDENTIFICATION gi on p.product_id = gi.product_id 
where gi.id_value is null OR gi.id_value='' and gi.good_identification_type_id='ERP_ID';

```
