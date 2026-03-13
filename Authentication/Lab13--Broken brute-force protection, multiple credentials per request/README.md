# Lab-13: [Broken brute-force protection, multiple credentials per request](https://portswigger.net/web-security/authentication/password-based/lab-broken-brute-force-protection-multiple-credentials-per-request)

This lab is vulnerable due to a logic flaw in its brute-force protection. 

**Aim :-** To solve the lab, brute-force Carlos's password, then access his account page. 

   - Victim's username: ``` carlos ```
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)



## Solution
- Try login as ``` carlos ``` using a random password.

- Intercept the request then send it to **repeater**.

- In the request the username and password are sent in **JSON** format.

- Copy all the [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords) and add it in the request like the following.
```json
{
    "username":"carlos",
    "password":[
        "123456",
        "password",
        "12345678",
        "qwerty",
        "123456789",
        "12345",
        "1234",
        "111111",
        "1234567",
        ........
        ........
    ]
}
```

- The server will respond with **302**. 

- Right click on the response click **Open response in browser**, copy the **URL**.

- Go to the browser paste the **URL** and make the request.