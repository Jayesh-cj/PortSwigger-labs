# Lab-7: [JWT authentication bypass via algorithm confusion](https://portswigger.net/web-security/jwt/algorithm-confusion/lab-jwt-authentication-bypass-via-algorithm-confusion)
> EXPERT

This lab uses a JWT-based mechanism for handling sessions. It uses a robust RSA key pair to sign and verify tokens. However, due to implementation flaws, this mechanism is vulnerable to algorithm confusion attacks. 

**Aim :-** To solve the lab, first obtain the server's public key. This is exposed via a standard endpoint. Use this key to sign a modified session token that gives you access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.

> **Tip:-** We recommend familiarizing yourself with [how to work with JWTs in Burp Suite](https://portswigger.net/burp/documentation/desktop/testing-workflow/vulnerabilities/session-management/jwts) before attempting this lab. 

> **Hint:-** You can assume that the server stores its public key as an X.509 PEM file. 



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to ```/admin ```, the page is only accessible to administrator.

- Intercept the request using **burp suite** then send it to repeater.

- Go to ``` /jwks.json ``` a standard endpoint which exposes a JWK Set containing a single public key. 

- Copy the key from the response.

- Go to **JWT Editor** tab in burp then click **New RSA Key**, in the dialog make sure the **JWK** is selected then paste the copied key then click **OK** to save the key.

- Right click on the newly generated key then click on **Copy Public Key as PEM**.

- Go to the **Decoder** tab in burp then encode the key as **base64**. Copy the base64 encoded PEM.

- Go to the **JWT Editor** tab, generate a **New Symmetric Key**, replace the value of ``` k ``` with the new base64 encoded PEM.

- Go to the **repeater** tab, open the **JSON Web Token** then change the ``` alg ``` to ``` HS256 ``` in the Header section.

- Change the ``` sub ``` name to ``` administrator ``` in the Payload section.

- Sign the token with the **New Symmetric key** then send the request, server will respond with the admin panel.

- Find the endpoint to delete the user ``` carlos ``` ( ``` /admin/delete?username=carlos ```) then make a request to that endpoint.