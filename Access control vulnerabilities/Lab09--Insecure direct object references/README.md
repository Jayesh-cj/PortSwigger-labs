# Lab-9: [Insecure direct object references](https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references)

This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs. 

**Aim :-** Solve the lab by finding the password for the user carlos, and logging into their account. 



## Solution
- Go to ``` /chat ``` and view the source code.

- When click on the **View transcript** button it redirect to ``` /download-transcript ```.

- Make a request to ```  /download-transcript/1.txt ```.

- This will reveal a chat that contains password.

- Copy that password and login as ``` carlos ```.