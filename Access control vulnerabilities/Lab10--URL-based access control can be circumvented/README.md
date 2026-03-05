# Lab-10: [URL-based access control can be circumvented](https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented)

This website has an unauthenticated admin panel at ``` /admin ```, but a front-end system has been configured to block external access to that path. However, the back-end application is built on a framework that supports the ``` X-Original-URL ``` header. 

**Aim :-** To solve the lab, access the admin panel and delete the user carlos. 



## Solution
- Go to ``` /admin ```, the server respond with **Access denied**.

- Intercept the request, add ``` X-Original-URL: /admin ``` in the request header and make request to ``` / ```.

- The server respond with admin panel.

- Make request to ``` /?username=carlos ``` with ``` X-Original-URL: /admin/delete ``` as request header.

- This will delete the user carlos.