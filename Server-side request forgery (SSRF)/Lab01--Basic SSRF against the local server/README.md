# Lab-1: [Basic SSRF against the local server](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost)

This lab has a stock check feature which fetches data from an internal system. 

**Aim :-** To solve the lab, change the stock check URL to access the admin interface at ``` http://localhost/admin ``` and delete the user ``` carlos ```.



## Solution
- Go to ``` /admin ``` in the lab.

- Server respond with ``` Admin interface only available if logged in as an administrator, or if requested from loopback ``` message.

- Intercept a **Check stock** request and send it to **repeater**.

- The check stock request makes a api request to another end point which mentioned in ``` stockApi ``` parameter in the body.

- Change the ``` stockApi ``` value to ``` http://localhost/admin ```. The server will respond with admin panel.

- From the source code of admin panel find the endpoint to delete user ``` carlos ```.

- In **Check stock** request change the ``` stockApi ``` value to ``` http://localhost/admin/delete?username=carlos ``` and make the request.