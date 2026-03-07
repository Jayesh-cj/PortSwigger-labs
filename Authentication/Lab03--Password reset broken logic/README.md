# Lab-3: [Password reset broken logic](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-broken-logic)

This lab's password reset functionality is vulnerable. 

**Aim :-** To solve the lab, reset Carlos's password then log in and access his "My account" page. 

   - Your credentials: ``` wiener:peter ```.
   - Victim's username: ``` carlos  ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Copy wiener's email and logout.

- Go to login page click forgot password and request reset password link for ``` wiener ```.

- Reset the password of ``` wiener ``` and intercept the request using **burp suite**.

- In the request body there will be a token, username, new-password-1 and new-password-2.

- Change the username to ``` carlos ``` and forward the request. This will reset the password of ``` carlos ```.

- Login as ``` carlos ``` using the password.