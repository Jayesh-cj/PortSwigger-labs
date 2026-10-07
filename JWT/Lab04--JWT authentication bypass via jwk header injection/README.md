# Lab-4:- [JWT authentication bypass via jwk header injection](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-jwk-header-injection)
> PRACTITIONER

This lab uses a JWT-based mechanism for handling sessions. The server supports the jwk parameter in the ``` JWT ``` header. This is sometimes used to embed the correct verification key directly in the token. However, it fails to check whether the provided key came from a trusted source. 

**Aim :-** To solve the lab, modify and sign a JWT that gives you access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```

> **Tip:-** We recommend familiarizing yourself with [how to work with JWTs in Burp Suite](https://portswigger.net/burp/documentation/desktop/testing-workflow/vulnerabilities/session-management/jwts) before attempting this lab. 



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to ```/admin ```, the page is only accessible to administrator.

- Intercept the request using **burp suite** then send it to repeater.

- Go to **JWT Editor** tab in burp suite generate a **New RSA Key**.

- Go to **repeater** tab in burp, open **JSON Web Token** tab in repeater.

- In the payload section change the sub name to ``` administrator ```.

- At the bottom of the **JSON Web Token** tab, click **Attack**, then select **Embedded JWK**. When prompted, select your newly generated **RSA** key and click OK.

- In the header of the JWT, a ``` jwk ``` parameter has been added containing the public key. 
    - A **JSON Web Key** or **JWK** is a JSON data structure that represents a set of public keys.

- Send the request now the admin panel will be accessible.

- Find the endpoint to delete user ``` carlos ``` and make request to that endpoint (```/admin/delete?username=carlos ```).