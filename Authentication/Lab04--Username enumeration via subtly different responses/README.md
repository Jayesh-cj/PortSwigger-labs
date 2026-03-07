# Lab-4: [Username enumeration via subtly different responses](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses)

This lab is subtly vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists: 

   - [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

**Aim :-** To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 



## Solution
- Login using a dummy username and password.

- Intercept the request and send it to **Intruder**.

- Select the username and click on **Add §** button. Configure the usernames with [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames).

- From the right side panel click on **settings** Go to **Grep - Extract**.

- Click add then a dialog box will appear with login response code. 

- Select the error message ``` Invalid username or password. ``` ( include the full stop also ( ``` . ``` ) ). Click ok.

- Start the attack.

- In the responses there will be a additional column with the error message, sort it.

- There will be a response that will be subtly different ( the error message may not have full stop (``` . ``` ) ). Copy the username.

- Go back to **Intruder** paste the username.

- Select the password and click on **Add §** button.

- Configure the passwords with [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords).

- Start the attack.

- In the responses one response will return **302** status code.

- Copy that username and password and login.