# Lab-8: [JWT authentication bypass via algorithm confusion with no exposed key](https://portswigger.net/web-security/jwt/algorithm-confusion/lab-jwt-authentication-bypass-via-algorithm-confusion-with-no-exposed-key)
> EXPERT

This lab uses a JWT-based mechanism for handling sessions. It uses a robust RSA key pair to sign and verify tokens. However, due to implementation flaws, this mechanism is vulnerable to algorithm confusion attacks. 

**Aim :-** To solve the lab, first obtain the server's public key. Use this key to sign a modified session token that gives you access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.

> **Tip :-** We recommend familiarizing yourself with [how to work with JWTs in Burp](https://portswigger.net/burp/documentation/desktop/testing-workflow/vulnerabilities/session-management/jwts) Suite before attempting this lab.
> We have also provided a simplified version of the ``` jwt_forgery.py ``` tool to help you. For details on how to use this, see [Deriving public keys from existing tokens](https://portswigger.net/web-security/jwt/algorithm-confusion#deriving-public-keys-from-existing-tokens). 

> **Hint :-** You can assume that the server stores its public key as an X.509 PEM file. 



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to ```/admin ```, the page is only accessible to administrator.

- Intercept the request using burp suite and copy the **JWT session cookie** and save it somewhere.

- Log out and login again then copy and save that **JWT session cookie** also.

- Run the following command in the terminal
```  docker run --rm -it portswigger/sig2n <token1> <token2> ```.

- Copy the tampered JWT from the first X509 entry.

- Intercept a ``` /my-account ``` request then replace the **JWT Session Cookie** with the tampered JWT.

- Forward the request,
    - if server respond with **200 success** and successfully access the ``` /my-account ``` page then this is the correct X509 key.
    - if the server respond with **302 found** and redirect to the ``` /login ``` page then this was the wrong X509 key. In this case, repeat this step using the tampered JWT for each X509 key that was output by the script. 

- From your terminal window, copy the **Base64-encoded X509** key that identified as being correct in the previous step.

- Go to **JWT Editor** tab in burp suite generate a **New Symmetric Key**, replace the value of ``` k ``` with the **Base64-encoded X509** key.

- Go to ``` /admin ``` in the lab, intercept the request using burp then send it to repeater.

- Open the **JSON Web Token** tab in **repeater**, in the payload section change the value of ``` sub ``` to ``` administrator ```.

- In the header section change the value of ``` alg ``` to ``` HS256 ``` then **Sign** the token with newly generated key.

- Find the endpoint to delete the user ``` carlos ``` then make a request to that endpoint ( ``` /admin/delete?username=carlos ```).