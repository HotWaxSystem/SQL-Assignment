## 1. Shipping Addresses for October 2023 Orders
## Business Problem:
### Customer Service might need to verify addresses for orders placed or completed in October 2023. This helps ensure shipments are delivered correctly and prevents address-related issues.

## Fields to Retrieve:

1. ORDER_ID
2. PARTY_ID (Customer ID)
3. CUSTOMER_NAME (or FIRST_NAME / LAST_NAME)
4. STREET_ADDRESS
5. CITY
6. STATE_PROVINCE
7. POSTAL_CODE
8. COUNTRY_CODE
9. ORDER_STATUS
10. ORDER_DATE

## Solution:
```sql
SELECT oh.order_id,
       pcm.party_id,
       per.first_name || ' ' || per.LAST_NAME as customer_name ,
       pad.address1,
       pad.address2,
       pad.city,
       pad.state_province_geo_id,
       pad.postal_code,
       pad.country_geo_id,
       oh.status_id,
       oh.order_date 
FROM order_header oh
JOIN order_contact_mech ocm ON ocm.order_id = oh.order_id 
JOIN party_contact_mech pcm ON pcm.contact_mech_id = ocm.contact_mech_id
JOIN postal_address pad ON pad.contact_mech_id = ocm.contact_mech_id
JOIN person per ON per.party_id = pcm.party_id
WHERE CAST(oh.order_date AS DATE)>='2023-10-01' AND CAST(oh.order_date AS DATE)<='2023-10-31'
AND (oh.status_id='ORDER_CREATED' OR oh.status_id='ORDER_COMPLETED' ) AND ocm.CONTACT_MECH_PURPOSE_TYPE_ID='SHIPPING_LOCATION';

```
![image](https://github.com/user-attachments/assets/93a7f7e6-429e-4f04-8d25-c89ec74e0d8b)

