# Lab-2: [2FA simple bypass](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass)

This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code.

**Aim :-** To solve the lab, access Carlos's account page. 

   - Your credentials: ``` wiener:peter ```.
   - Victim's credentials ``` carlos:montoya ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- The server respond with a page to enter security code. 

- Go to **Email client** to get the security code, copy the code and login.

- After verification page redirect to ``` /my-account ```.

- Try to login as ``` carlos ```.
    - Username : ``` carlos ```.
    - Password : ``` montoya ```.

- When the server respond make a request to ``` /my-account ```.