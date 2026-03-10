# Lab-8: [2FA broken logic](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic)

This lab's two-factor authentication is vulnerable due to its flawed logic.

**Aim :-** To solve the lab, access Carlos's account page. 

   - Your credentials: ``` wiener:peter ```.
   - Victim's username: ``` carlos ```.

You also have access to the email server to receive your 2FA verification code. 



## Solution
- Login as ``` wiener ``` and find out how the application works.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- After making the login request the server will respond with a page to enter the security code ( ``` /login2 ``` page ).

- When the ``` GET /login2 ``` request is made there will be a cookie named ``` verify= ```.

- The value of ``` verify= ``` cookie is what defines which users **2FA** code should send.

- Intercept a ``` GET /login2 ``` request and add ``` carlos ``` as the value of ``` verify= ```. Then forward the request.

- When the server respond with page to enter the **2FA** code enter a random 4 digit number and intercept the request and send to intruder.

- Change the name to ``` carlos ``` in ``` verify= ``` cookie.

- Select the 4 digit number and select payload type as **Numbers**.

- Configure the payload to start **from 0000 to 9999**.

- Start the attack.

- Check for a response that responded with **302** status code.

- Use that number in **2FA**, change the name to ``` carlos ``` in **cookie**.