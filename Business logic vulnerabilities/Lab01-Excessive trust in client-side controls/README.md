# Lab-1: [Excessive trust in client-side controls](https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls)

This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price.

**Aim :-** To solve the lab, buy a "**Lightweight l33t leather jacket**". 

You can log in to your own account using the following credentials: ``` wiener:peter ```.


## Solution
- Login as ``` wiener ```
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Add the product "**Lightweight l33t leather jacket**" in the cart and intercept the request using **burp suite**. 

- In the **POST** request jacket's price also passed to the server.

- Change the price and forward the request.

- Go to cart, the price will be changed.

- Place the order.

---
<div>

> In here the server blindly trust the client so there is no server side validation for the request parameters.

</div>