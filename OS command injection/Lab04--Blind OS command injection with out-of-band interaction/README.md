# Lab-4: [Blind OS command injection with out-of-band interaction](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band)

This lab contains a blind OS command injection vulnerability in the feedback function. 

The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain.

**Aim :-** To solve the lab, exploit the blind OS command injection vulnerability to issue a **DNS lookup to Burp Collaborator**. 



## Solution
- Submit a feedback and intercept the request using **burp suite** then send it to **intruder**.

- Go to collaborator tab in **burp suite**, Start a collaborator subdomain and copy the domain.

- Append the following in the **email** and forward the request
    ``` ||ping+BURP-COLLABORATOR-SUBDOMAIN|| ``` replace the collaborator subdomain.

- Go to the collaborator tab in **burp suite** click **Poll now**.