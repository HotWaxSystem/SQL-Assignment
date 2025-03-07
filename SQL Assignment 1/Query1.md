## New Customers Acquired in June 2023
## Business Problem:
### The marketing team ran a campaign in June 2023 and wants to see how many new customers signed up during that period.

## Fields to Retrieve:

1.PARTY_ID
2.FIRST_NAME
3.LAST_NAME
4.EMAIL
5.PHONE
6.ENTRY_DATE


### Solution:-
```sql
select p.party_id, p.first_name, p.last_name,
       cm.info_string AS EmailAddress,
       t.contact_number AS Phone,
       p.created_stamp
FROM PERSON p
JOIN PARTY_ROLE pr ON pr.party_id = p.party_id
JOIN PARTY_CONTACT_MECH pcm ON pcm.party_id = p.party_id
JOIN CONTACT_MECH cm ON cm.contact_mech_id = pcm.contact_mech_id
LEFT JOIN TELECOM_NUMBER t ON t.contact_mech_id = pcm.contact_mech_id
where pr.role_type_id = 'CUSTOMER' 
AND p.created_stamp BETWEEN '2023-06-01' AND '2023-06-30';

```
![image](https://github.com/user-attachments/assets/26ed00b4-7bd7-48b8-80c1-97916bc69f2d)
