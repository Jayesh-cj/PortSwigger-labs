# Lab-1: [Username enumeration via different responses](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)

This lab is vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists: 

   - [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

**Aim :-** To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 



## Solution
- Try to login with a random username and password.

- The server respond with ``` Invalid username ``` error message.

- Make a login request and intercept it using **burp suite**. Right click and send the request to **Intruder**.

- In the **intruder** select the username and click **Add §** button.

- Configure the payload with [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames).

- Start the attack.

- In the responses check for a response that does'nt have ``` Invalid username ``` error message ( The response will have ``` Incorrect password ``` error message ).

- Back to the **Intruder** change the username. Select the password and click **Add §** button.

- Configure the payload with [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords).

- Start the attack.

- In the responses check for a response that does'nt have ``` Incorrect password ``` error message.

- Copy the username and password then login.