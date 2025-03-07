## 2. Orders from New York
## Business Problem:
### Companies often want region-specific analysis to plan local marketing, staffing, or promotions in certain areas—here, specifically, New York.

## Fields to Retrieve:

1. ORDER_ID
2. CUSTOMER_NAME
3. STREET_ADDRESS (or shipping address detail)
4. CITY
5. STATE_PROVINCE
6. POSTAL_CODE
7. TOTAL_AMOUNT
8. ORDER_DATE
9. ORDER_STATUS

## Solution:-
```sql
select oh.order_id,
       per.first_name || ' ' || per.last_name  AS Customer_Name,
       pa.address1 AS street_address,
       pa.address2,
       pa.city,
       pa.state_province_geo_id AS state_province,
       pa.postal_code,
       oh.grand_total as total_amount,
       oh.order_date,
       oh.status_id as Order_status
from Order_Header oh
JOIN order_contact_mech ocm ON ocm.order_id = oh.order_id AND ocm.CONTACT_MECH_PURPOSE_TYPE_ID='SHIPPING_LOCATION'
JOIN party_contact_mech pcm ON pcm.contact_mech_id = ocm.contact_mech_id
JOIN postal_address pa ON pa.contact_mech_id = ocm.contact_mech_id
JOIN person per ON per.party_id = pcm.party_id
WHERE pa.state_province_geo_id = 'NY';

```
![image](https://github.com/user-attachments/assets/2373e6a3-7ad5-49e9-b1e3-7bd4d9a5d2e4)

