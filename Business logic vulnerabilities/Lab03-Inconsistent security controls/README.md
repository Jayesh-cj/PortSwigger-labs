# Lab-3: [Inconsistent security controls](https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-inconsistent-security-controls)

This lab's flawed logic allows arbitrary users to access administrative functionality that should only be available to company employees.

**Aim :-** To solve the lab, access the **admin panel** and delete the user ``` carlos ```.



## Solution
- Go to **Email client** and copy the attacker email id.

- Go to **register** and create a user with attacker email id.
    - The registration page also says that ``` If you work for DontWannaCry, please use your @dontwannacry.com email address ```.

- There will be a registration link in the mail click and complete the registration.

- Login as the new user.

- Go to ``` /admin ```.

- The page returns with a message ```Admin interface only available if logged in as a DontWannaCry user  ```

- Go to ``` /my-account ``` and update the email with DontWannaCry user mail id ( name@dontwannacry.com ).

- After updating the email **Admin Panel** link will be available, go to the **Admin Panel** ( ``` /admin ```).

- Delete the user ``` carlos ```.

---
<div>

> The email update functionality does not verify the email ID.

</div>