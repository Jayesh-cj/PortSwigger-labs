# Lab-4: [Authentication bypass via information disclosure](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-authentication-bypass)

This lab's administration interface has an authentication bypass vulnerability, but it is impractical to exploit without knowledge of a custom HTTP header used by the front-end.

**Aim :-** To solve the lab, obtain the header name then use it to bypass the lab's authentication. Access the admin interface and delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Make a ``` GET ``` request to ``` /admin ```.

- The server respond with ``` Admin interface only available to local users ``` error message.

- Intercept the ``` /admin ``` request using **burp suite** and send it to **repeater**.

- Change the ``` GET ``` method to ``` TRACE ``` and send the request.
    - The **HTTP TRACE** method is a diagnostic tool designed to perform a message loop-back test, allowing a client to see what is received at the end of the request chain. The server echoes the exact request, including headers, in the 200 OK response body.

- In the response there is a ``` X-Custom-IP-Authorization ``` header with client ip.
    - ``` X-Custom-IP-Authorization ```  is a non-standard HTTP header often used to misconfigure access control by relying on client-supplied IP addresses.

- Add ``` X-Custom-IP-Authorization: 127.0.0.1 ``` in the request header and make a ``` GET ``` request to ``` /admin ```.

- Server will respond with admin panel, find the endpoint to delete user ``` carlos ``` ( ``` /admin/delete?username=carlos ``` ).

- Make a request to ``` /admin/delete?username=carlos ``` with ``` X-Custom-IP-Authorization: 127.0.0.1 ``` in the header.