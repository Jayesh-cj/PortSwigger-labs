# Lab-4: [Flawed enforcement of business rules](https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-flawed-enforcement-of-business-rules)

This lab has a logic flaw in its purchasing workflow. 

**Aim :-** To solve the lab, exploit this flaw to buy a "**Lightweight l33t leather jacket**". 

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login as ``` wiener ```
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Add "**Lightweight l33t leather jacket**" in the cart.

- Apply the coupon code that showed in the banner (``` NEWCUST5 ```).

- Try applying the coupon again, it won't work.

- Go to home, scroll down there will be a signup option.

- Signing up will give you a new coupon code ( ``` SIGNUP30 ``` ).

- Use this new code ( ``` SIGNUP30 ``` ).

- Using a coupon code twice in a raw is rejected by the server.

- So use the code ``` NEWCUST5 ``` first then use ``` SIGNUP30 ```.

- Repeat this until the total price is lesser that the Store credit, then buy the **jacket**.


---

> This happens because the server only tracks the last-used coupon and it stores coupon state incorrectly.