# Lab-7: [SSRF with whitelist-based input filter](https://portswigger.net/web-security/ssrf/lab-ssrf-with-whitelist-filter)

This lab has a stock check feature which fetches data from an internal system. 

**Aim :-** To solve the lab, change the stock check URL to access the admin interface at ``` http://localhost/admin ``` and delete the user ``` carlos ```.

The developer has deployed an anti-SSRF defense you will need to bypass. 



## Solution
- Intercept a **check stock** request using **burp suite** and send it to **repeater**.

- There is a ``` stockApi ``` request is making to get the stock.

- Replace the ``` stockApi ``` with ``` http://localhost:80%2523@stock.weliketoshop.net/admin ``` and forward the request.

- Server will respond with the admin panel.

- Find the endpoint to delete the user ``` carlos ```.

- Use that endpoint in ``` stockApi ``` **(** ``` http://localhost:80%2523@stock.weliketoshop.net/admin/delete?username=carlos ``` **)** and forward the request to delete user ``` carlos ```.