## 3. Average Shipments per Month (Q1 2022)
## Business Problem:
### Operations wants to find the average number of shipments from all stores for each month in Q1 2022 (January, February, March).

## Fields to Retrieve:

1.MONTH
2.AVERAGE_SHIPMENTS

## Solution:-
```sql
select extract(month from ss.status_date) as Month,
       count(s.shipment_id) / count(distinct s.origin_facility_id) as AverageShipments
from Shipment s 
JOIN Shipment_Status ss on ss.shipment_id = s.shipment_id
where ss.status_id = 'SHIPMENT_SHIPPED' and ss.status_date BETWEEN '2022-01-01' AND '2022-03-31'
group by extract(month from ss.status_date);

```
![image](https://github.com/user-attachments/assets/05ed5ff7-ca64-4a1a-b0fc-034bab89574d)
