# Lab-1: [OS command injection, simple case](https://portswigger.net/web-security/os-command-injection/lab-simple)

This lab contains an OS command injection vulnerability in the product stock checker.

The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response. 

**Aim :-** To solve the lab, execute the ``` whoami ``` command to determine the name of the current user. 



## Solution
- Intercept the **check stock** request using **burp suite** and then send it to **repeater**.

- The request contains product and store IDs.

- Append ``` |whoami ``` with the storeId and forward the request.
    - Pipe **(**``` | ```**)** allows commands to run simultaneously and data to be transferred between them directly in memory.

- Server will respond with the current user name.