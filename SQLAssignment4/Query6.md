## 6. Orders Shipped from Stores (25 Days Before New Year)
## Business Problem:
### Retailers often run holiday promos in late December and need visibility into orders shipped from stores (as opposed to warehouses) for the final 25 days of the year.

## Fields to Retrieve:

1.ORDER_ID
2.SHIPMENT_ID
3.FACILITY_ID (store ID)
4.SHIPMENT_DATE
5.ORDER_DATE
6.TOTAL_ITEMS
7.CUSTOMER_STATE
```sql
Solution:-
select oh.order_id,
       os.shipment_id,
       oisg.facility_id,
       ss.status_date as ShipmentDate,
       oh.order_date,
       count(os.ship_group_seq_id) as TotalItems,
       pa.state_province_geo_id as CustomerState
from Order_header oh
JOIN Order_Shipment os on os.order_id = oh.order_id
JOIN Order_item_ship_group oisg on oisg.order_id = os.order_id
JOIN Shipment_status ss on ss.shipment_id = os.shipment_id
JOIN Order_Contact_Mech ocm on ocm.order_id = os.order_id
JOIN Postal_Address pa on pa.contact_mech_id = ocm.contact_mech_id
JOIN Facility f on f.facility_id = oisg.facility_id
where ss.status_id = 'SHIPMENT_SHIPPED' and
      ss.status_date BETWEEN '2024-12-06' AND '2024-12-31' and
      f.facility_type_id LIKE '%STORE'
group by oh.order_id,
         os.shipment_id,
         oisg.facility_id,
         ss.status_date,
         oh.order_date,
         pa.state_province_geo_id;

```
![image](https://github.com/user-attachments/assets/0b98a920-93ad-46ef-8994-6e708f52d1fa)
