Title

Insecure Direct Object Reference (IDOR) in Basket Items API allowing unauthorized modification of other users' shopping carts.

DESCRIPTION

The application is vulnerable to an Insecure Direct Object Reference (IDOR) in the /api/BasketItems/{id} endpoint.

An authenticated user can modify the quantity of items in another user's shopping basket by changing the BasketItem ID in the request.

The application fails to properly validate whether the authenticated user owns the targeted resource, allowing unauthorized access and modification.

STEPS TO REPRODUCE

1. Register and log in as User A.
2. Add a product to the shopping basket.
3. Capture the request POST /api/BasketItems and note the returned "id" value (BasketItem ID).

4. Log out and log in as User B.
5. Intercept or capture a request to /api/BasketItems.
6. Send the request to Burp Repeater.

7. Modify the request:
   - Change the HTTP method to PUT
   - Change the endpoint to /api/BasketItems/{id} using the ID obtained from User A
   - Set the request body to:
     {
       "quantity": 99
     }

8. Send the request.

9. Log back in as User A and observe that the quantity of the item has been modified.

IMPACT

This vulnerability allows attackers to modify other users' shopping carts without authorization.

An attacker could manipulate product quantities, disrupt purchases, or potentially abuse the system for financial gain or denial of service.

This represents a critical violation of access control mechanisms.

FIX

The application should enforce proper authorization checks on all resource access.

Specifically, the backend must verify that the authenticated user owns the BasketItem before allowing any modification.

Access control should not rely solely on client-provided identifiers.
