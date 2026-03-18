# Lab-2: [Basic SSRF against another back-end system](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-backend-system)

This lab has a stock check feature which fetches data from an internal system. 

**Aim :-** To solve the lab, use the stock check functionality to scan the internal ``` 192.168.0.X ``` range for an admin interface on port ``` 8080 ```, then use it to delete the user carlos.



## Solution
- Intercept a **Check stock** request using **burp suite** and send the request to **intruder**.

- Change the value of ``` stockApi ``` to ``` http://192.168.0.1:8080/admin ``` and select 1 then click **Add §** button.

- Configure the payload to start **from 1 to 255**.

- Start the attack.

- From the responses find the response with **200 status code**.

- Right click on the request and send it to **repeater**. Forward the request.

- From the response source code find the endpoint to delete user ``` carlos ```.

- Replace that link in ``` stockApi ``` and forward the request. ( ``` stockApi=http://192.168.0.176:8080/admin/delete?username=carlos ```).