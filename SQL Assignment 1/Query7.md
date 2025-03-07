## 7. Newly Created Sales Orders and Payment Methods
## Business Problem:
### Finance teams need to see new orders and their payment methods for reconciliation and fraud checks.

## Fields to Retrieve:

1. ORDER_ID
2. TOTAL_AMOUNT
3. PAYMENT_METHOD
4. Shopify Order ID (if applicable)

## Solution:-
```sql
select oh.order_id,
       oh.grand_total AS TotalAmount,
       opp.payment_method_type_id AS PaymentMethod,
       oh.external_id AS Shopify_Order_Id
from Order_Header oh
JOIN order_payment_preference opp on opp.order_id = oh.order_id
where oh.status_id = 'ORDER_CREATED' and oh.order_type_id='SALES_ORDER';

```
![image](https://github.com/user-attachments/assets/22fbdd91-a04f-40eb-af57-f7763db5e55c)
