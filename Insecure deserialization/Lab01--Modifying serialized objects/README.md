# Lab-1: [Modifying serialized objects](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-objects)

This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. 

**Aim :-** To solve the lab, edit the serialized object in the session cookie to exploit this vulnerability and gain administrative privileges. Then, delete the user `` carlos ``.

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Intercept ``` /my-account ``` request using **burp suite**.

- In the request header there will be a **session** cookie, it is base64 encoded, decode it.

- Notice that the **admin** attribute contains ``` b:0 ```, indicating the boolean value **false**. Send this request to **burp repeater**. 

- Change the ``` b:0 ``` to ``` b:1 ``` and encode the **cookie** in base64.

- Paste the **cookie** in the request header and make request to ``` /admin ```.

- Server will respond with admin panel with admin privilege.

- Find endpoint to delete user ``` carlos ```.

- Make request to that end point to delete ``` carlos ``` ( ``` /delete?username=carlos ``` ).