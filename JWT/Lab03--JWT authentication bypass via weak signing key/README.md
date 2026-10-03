# Lab-3:- [JWT authentication bypass via weak signing key](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-weak-signing-key)
> PRACTITIONER

This lab uses a JWT-based mechanism for handling sessions. It uses an extremely weak secret key to both sign and verify tokens. This can be easily brute-forced using a [wordlist of common secrets. ](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list)

**Aim :-** To solve the lab, first brute-force the website's secret key. Once you've obtained this, use it to sign a modified session token that gives you access to the admin panel at ``` /admin ```, then delete the user ``` carlos ```.

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login as ``` wiener ```
    - Username : ``` wiener ```.
    - Password : ``` peter ```

- Go to ```/admin ```, the page is only accessible to administrator.

- Intercept the request using **burp suite** then send it to repeater.

- Copy the **JWT Token** and use the following command to brute-force the secret key. ( use this [wordlist](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list) )
    - If using **Hashcat**
    ``` hashcat -a 0 -m 16500 <JWT-TOKEN> <PATH-TO-JWT-WORDLIST-FILE> ```.

    - If using **John The Ripper**
    ``` john --wordlist=<PATH-TO-WORDLIST-FILE> <PATH-TO-JWT-TOKEN-FILE> ```.

- Install the **JWT Editor** extension then go to the **JWT Editor** tab in burp.

- Generate a new **symmetric key**, replace the value of ``` k ``` with the **base64** encoded secret key.

- Go to the **repeater**, open the **JSON Web Token** tab to edit the token.

- Change the username ``` wiener ``` to ``` administrator ``` then **Sign** the token.

- Send the request the server will respond with the **admin panel**.

- Find the endpoint to delete user ``` carlos ```.

- Send a request to that endpoint to delete the user ``` carlos ``` ( ``` /admin/delete?username=carlos ```).