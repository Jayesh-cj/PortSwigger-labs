# Lab-1: [JWT authentication bypass via unverified signature](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-unverified-signature)
> APPRENTICE

This lab uses a JWT-based mechanism for handling sessions. Due to implementation flaws, the server doesn't verify the signature of any JWTs that it receives. 

**Aim :-** To solve the lab, modify your session token to gain access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```.

You can log in to your own account using the following credentials: ``` wiener:peter ```.

> **Tip:-** We recommend familiarizing yourself with [how to work with JWTs in Burp Suite](https://portswigger.net/burp/documentation/desktop/testing-workflow/vulnerabilities/session-management/jwts) before attempting this lab. 



## Solution
- Log in as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to ``` /admin ``` page, this page is only accessible to ``` administrator ```.

- **Intercept** the request using burp suite and send it to **repeater**.

- In burp go to the **JSON Web Tokens** tab. Here can see the decoded form of the JWT token.

- In the **Payload** section, ``` sub ``` will be the username. Change it to ``` administrator ```.

- Forward the request. The administrator panel will be accessible.

- Find the endpoint to delete the user ``` carlos ``` and make a request to that endpoint ( ``` /admin/delete?username=carlos ```).