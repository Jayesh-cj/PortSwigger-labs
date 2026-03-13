# Lab-12: [Password brute-force via password change](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-brute-force-via-password-change)

This lab's password change functionality makes it vulnerable to brute-force attacks.

**Aim :-** To solve the lab, use the list of candidate passwords to brute-force Carlos's account and access his "My account" page. 

   - Your credentials: ``` wiener:peter ```.
   - Victim's username: ``` carlos ```.
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)



## Solution
- Login as ``` wiener ```.
   - Username : ``` wiener ```.
   - Password : ``` peter ```.

- Change the password and intercept the request using **burp suite** then send it to **repeater**.

- Find the logic flow.
   - When the request is success server returns a success message.

   - If the **current password** is **true** and **new passwords** mismatched then server returns a error message ``` New passwords do not match ```.

   - If the **current password** is **wrong** and **new passwords** match then the account is locked.

   - If the **current password** is **wrong** and **new passwords** mismatched then server returns a error message ``` Current password is incorrect ```.

- Send the request to **intruder**.

- Select **current password value** and click **Add §** button.

- Configure the payload with [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords).

- Change the **username** to ``` carlos ``` and add different passwords in **new password**.

- In **intruder** open settings from side panel add **Grep - Match** as ``` New passwords do not match ```.

- Start the attack.

- In the responses one response will be different.

- Copy the password and login as ``` carlos ```.