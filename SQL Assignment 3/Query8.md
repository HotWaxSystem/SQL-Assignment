## 8. List of Warehouse Pickers
## Business Problem:
### Warehouse managers need a list of employees responsible for picking and packing orders to manage shifts, productivity, and training needs.

## Fields to Retrieve:

1. PARTY_ID (or Employee ID)
2. NAME (First/Last)
3. ROLE_TYPE_ID (e.g., “WAREHOUSE_PICKER”)
4. FACILITY_ID (assigned warehouse)
5. STATUS (active or inactive employee)

## Solution:-
```sql
select distinct pr.party_id,
       pe.first_name,
       pr.role_type_id,
       pl.facility_id,
       pty.status_id as Status
from picklist pl
JOIN picklist_role pr on pr.picklist_id = pl.picklist_id
JOIN person pe on pe.party_id = pr.party_id
JOIN Party pty on pty.party_id = pr.party_id
where pty.status_id is not null;

```
![image](https://github.com/user-attachments/assets/2615e485-20d1-4642-bf6c-c054e6e0f804)
