## 11. Transfer Orders Without Inventory Reservation
## Business Problem:
### When transferring stock between facilities, the system should reserve inventory. If it isn’t reserved, the transfer may fail or oversell.

## Fields to Retrieve:

1. TRANSFER_ORDER_ID
2. FROM_FACILITY_ID
3. TO_FACILITY_ID
4. PRODUCT_ID
5. REQUESTED_QUANTITY
6. RESERVED_QUANTITY
7. TRANSFER_DATE
8. STATUS

## Solution:-
```sql
select it.inventory_transfer_id as TransferOrderId,
       it.facility_id as FromFacilityId,
       it.facility_id_to as ToFacilityId,
       it.product_id,
       it.quantity as REQUESTED_QUANTITY,
       oisgir.quantity as RESERVED_QUANTITY,
       it.send_date as TransferDate,
       it.status_id as Status
FROM Inventory_Transfer it 
JOIN inventory_item ii ON ii.inventory_item_id=it.inventory_item_id
JOIN order_item_ship_grp_inv_res oisgir ON oisgir.inventory_item_id=it.inventory_item_id;

```
