# Lab-5:- [JWT authentication bypass via jku header injection](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-jku-header-injection)
> PRACTITIONER

This lab uses a JWT-based mechanism for handling sessions. The server supports the ``` jku ``` parameter in the JWT header. However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key. 

**Aim:-** To solve the lab, forge a JWT that gives you access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```.

You can log in to your own account using the following credentials: ``` wiener:peter ```

> **Tip:-** We recommend familiarizing yourself with how to work with JWTs in Burp Suite before attempting this lab. 



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to ```/admin ```, the page is only accessible to administrator.

- Intercept the request using **burp suite** then send it to repeater.

- Go to the **JWT Editor** tab in burp and generate a **New RSA Key**.

- Right click the newly generated key then **Copy Public Key as JWK**.

- Paste the public key inside the key section of the following
```
{
    "keys": [

    ]
}
```

- Copy everything and go to the exploit server in the browser then paste it on the body section and store it.

- Copy the ``` kid ``` of the newly generated **RSA Key** then go to the burp, open the **JSON Web Token** tab in **repeater** replace the ``` kid ``` in the **Header** section.

- Add a new ``` jku ``` parameter to the header, set it's value as the exploit server's **URL**.
    - The **jku (JSON Web Key Set URL)** is an optional header parameter in a **JSON Web Token (JWT)** that points to a resource containing a set of **JSON Web Keys (JWKs)** used to verify the token's digital signature

- In the payload section change the value of ``` sub ``` to ``` administrator ```, sign the token then send the request.

- Now the admin panel is accessible, find the endpoint to delete the user ``` carlos ```, make the request to that endpoint ( ``` /admin/delete?username=carlos ``` ).