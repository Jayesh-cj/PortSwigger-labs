# Lab-2: [JWT authentication bypass via flawed signature verification](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-flawed-signature-verification)
>  APPRENTICE

This lab uses a JWT-based mechanism for handling sessions. The server is insecurely configured to accept unsigned JWTs. 

**Aim :-** To solve the lab, modify your session token to gain access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```.

You can log in to your own account using the following credentials: ``` wiener:peter ```.

> **Tip:-** We recommend familiarizing yourself with how to work with JWTs in Burp Suite before attempting this lab. 



## Solution
- Log in as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to ``` /admin ``` page, this page is only accessible to ``` administrator ```.

- **Intercept** the request using burp suite and send it to **repeater**.

- In burp go to the **JSON Web Tokens** tab. Here can see the decoded form of the **JWT** token.

- In the header section can see the signing algorithm used.

- In header change ``` "alg": "RS256" ``` to ``` "alg": "none" ``` ( use the **Alg None Attack** dropdown to change the alg parameter value ).

- In the payload section change ``` "sub": "wiener" ``` to ``` "sub": "administrator" ```.

- Now the administrator panel will be accessible.

- Find the endpoint to delete user ``` carlos ```, make the request to that endpoint (``` /admin/delete?username=carlos ```).