# Lab-2: [Modifying serialized data types](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-data-types)

This lab uses a serialization-based session mechanism and is vulnerable to authentication bypass as a result. 

**Aim :-** To solve the lab, edit the serialized object in the session cookie to access the ``` administrator ``` account. Then, delete the user ``` carlos ```.

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Intercept the ``` /my-account ``` request using **burp suite** send it to **repeater**.

- Select the **session Cookie** from the request body, right click and send it **decoder**.

- The **cookie** is in **base64** encode format, go to decoder tab in **burp suite** and decode the cookie.

- Modify the session cookie as follows: 
    - Change the username from ``` wiener ``` to ``` administrator ```.
    
    - Change the length of the username from ``` s:6 ``` to ``` s:13 ```.

    - Change the access token to the integer ``` 0 ```.

    - Update the data type label for the access token by replacing ``` s ``` with ``` i ```. 

    - The updated deserialized cookie will look like the follow :
        - ``` O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;} ```.

- Encode it using **base64** encode format.

- Copy the encoded token and go back to repeater paste the token in session cookie then make request to ``` /admin ```.

- Sever will respond with admin panel, find the endpoint to delete user ``` carlos ```.

- Copy the endpoint and make a request to that endpoint with the new **session cookie** ( ``` /delete?username=carlos ``` ). 