## 3.Single-Return Orders (Last Month)
## Business Problem:
### The mechandising team needs a list of orders that only have one return.

## Fields to Retrieve:

1. PARTY_ID
2. FIRST_NAME

## Solution:-
```sql
SELECT per.first_name,
       rh.FROM_PARTY_ID
FROM return_item ri
JOIN return_header rh ON ri.return_id=rh.return_id
JOIN person per ON per.party_id=rh.FROM_PARTY_ID
WHERE (rh.return_date >= DATE_FORMAT(CURDATE() - INTERVAL 1 MONTH, '%Y-%m-01')
AND rh.return_date < DATE_FORMAT(CURDATE(), '%Y-%m-01')) AND ri.order_id IN(select order_id FROM return_item GROUP BY order_id HAVING count(*)=1)
order by rh.FROM_PARTY_ID;

```
