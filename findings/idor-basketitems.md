# Insecure Direct Object Reference (IDOR) in Basket Items API

## Description

The application is vulnerable to an Insecure Direct Object Reference (IDOR) in the `/api/BasketItems/{id}` endpoint.

An authenticated user can modify the quantity of items in another user's shopping basket by changing the BasketItem ID in the request.

The application fails to properly validate whether the authenticated user owns the targeted resource, allowing unauthorized access and modification.

---

## Steps to Reproduce

1. Register and log in as User A.
2. Add a product to the shopping basket.
3. Capture the request `POST /api/BasketItems` and note the returned `id` value.

4. Log out and log in as User B.
5. Capture a request to `/api/BasketItems`.
6. Send the request to Burp Repeater.

7. Modify the request:
   - Change the HTTP method to `PUT`
   - Change the endpoint to `/api/BasketItems/{id}` using User A's ID
   - Set the request body to:
     ```json
     {
       "quantity": 99
     }
     ```

8. Send the request.

9. Log back in as User A and observe that the quantity has been modified.

---

## Impact

This vulnerability allows attackers to modify other users' shopping carts without authorization.

An attacker could manipulate product quantities, disrupt purchases, or abuse the system.

---

## Remediation

The application must enforce proper authorization checks.

The backend should verify that the authenticated user owns the BasketItem before allowing any modification.

Access control must not rely on user-controlled input.


## Proof of Concept

### Before Attack
<img width="1145" height="377" alt="before" src="https://github.com/user-attachments/assets/a3dd2926-f837-4532-9da0-f6dca520fcd4" />


### Burp Request (Exploit)
<img width="1207" height="628" alt="burp" src="https://github.com/user-attachments/assets/8f7f39f2-7c3a-4d77-9754-0e752fe6feaf" />


### After Attack
<img width="1151" height="381" alt="after" src="https://github.com/user-attachments/assets/83d87eb3-78cd-4f2e-82b5-8996239791e3" />
