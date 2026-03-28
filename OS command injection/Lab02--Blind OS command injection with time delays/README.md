# Lab-2 [Blind OS command injection with time delays](https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays)

This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. 

**Aim :-** To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay. 



## Solution
- Submit a feedback and intercept the request using **burp suite** then send it to **repeater**.

- Append the following payload with the value of **email**.
    ``` ||ping+-c+10+127.0.0.1|| ``` this will make 10 ping request to the **localhost**.
    
- Forward the request and wait for 10 seconds to get the response.