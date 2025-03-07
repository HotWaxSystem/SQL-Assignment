## 9. Total Facilities That Sell the Product
## Business Problem:
### Retailers want to see how many (and which) facilities (stores, warehouses, virtual sites) currently offer a product for sale.

## Fields to Retrieve:

1. PRODUCT_ID
2. PRODUCT_NAME (or INTERNAL_NAME)
3. FACILITY_COUNT (number of facilities selling the product)
4. (Optionally) a list of FACILITY_IDs if more detail is needed

## Solution:-
```sql
SELECT p.product_id,
       p.internal_name,
       count(pf.facility_id) as FACILITY_COUNT
FROM product p JOIN product_facility pf ON pf.product_id=p.product_id
Group by p.product_id;
```
![image](https://github.com/user-attachments/assets/0c65868e-1603-4319-9421-9e0b0c6e4f16)
