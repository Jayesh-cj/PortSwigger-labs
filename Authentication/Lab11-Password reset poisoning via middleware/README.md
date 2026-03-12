# Lab-11: [Password reset poisoning via middleware](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-poisoning-via-middleware)

This lab is vulnerable to password reset poisoning. The user ``` carlos ``` will carelessly click on any links in emails that he receives.

To solve the lab, log in to Carlos's account. You can log in to your own account using the following credentials: ``` wiener:peter ```. Any emails sent to this account can be read via the email client on the exploit server. 



## Solution
- Make a forgot password request for ``` wiener ```.

- Make a forgot password request for ``` carlos ``` and intercept it using **Burp suite**.

- Go to **Exploit Server** and copy the **URL**.

- Add ``` X-Forwarded-Host: ``` in the forgot password request and place the **Exploit server URL** as value.

- Forward the request.

- From **Exploit Server** go to **Access Log** and check for a request with forgot password **token**. Copy that token.

- Go to **Email Client** from **Exploit Server** open the forgot password link replace the token.

- Change the password and login as ``` carlos ``` using the new password.