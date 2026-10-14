# Lab-6:- [JWT authentication bypass via kid header path traversal](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-kid-header-path-traversal)
>  PRACTITIONER 

This lab uses a JWT-based mechanism for handling sessions. In order to verify the signature, the server uses the ``` kid ``` parameter in JWT header to fetch the relevant key from its filesystem. 

**Aim :-** To solve the lab, forge a JWT that gives you access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.

> **Tip:-** We recommend familiarizing yourself with [how to work with JWTs in Burp Suite](https://portswigger.net/burp/documentation/desktop/testing-workflow/vulnerabilities/session-management/jwts) before attempting this lab. 



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to ```/admin ```, the page is only accessible to administrator.

- Intercept the request using **burp suite** then send it to repeater.

- Go to the **JWT Editor** tab in burp and generate a **New Symmetric Key**.

- Replace the generated value for the ``` k ``` property with an empty string, click **OK** and save the key.

- In burp open the **JSON Web Token** tab in **repeater**.

- In the Header section change the ``` kid ``` value to ``` /dev/null ```.

- In Payload section change the ``` sub ``` value to ``` administrator ```.

- Sign the token with the newly generated **Symmetric Key**, and send the request.

- Add file traversal sequence (``` ../ ```) in front of the ``` /dev/null ``` until the admin panel is accessible.

- After the admin panel is accessible find the endpoint to delete the user ``` carlos ``` ( ``` /admin/delete?username=carlos ```).

- Make a request to that endpoint to delete the user ``` carlos ```.