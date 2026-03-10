# Lab-7: [Username enumeration via account lock](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock)

This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. 

**Aim :-** To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 
    
   - [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)



## Solution
- Intercept a login request with random username and password, then send to **intruder**.

- Select the attack type as **Cluster Bombing Attack**.

- Select the username and click **Add §** button. Configure the payload with [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames).

- Place the cursor to the right side of the password and click **Add §** button.

- Set the payload type as **Null Payloads**. Configure the payload to **Generate 5** payloads.
    - This will cause each username to repeat **5** times.

- Start the attack.

- Check for a response that contain ``` You have made too many incorrect login attempts. Please try again in 1 minute(s). ``` error message.
    - IP is blocked only if multiple login attempts failed with valid username and invalid password.

    - If the username is ont valid then the ip will not be blocked.

- Copy the username.

- Go back to intruder and paste the username. 

- Select attack type as **Sniper attack**.

- Select the password and click **Add §** button. Configure the password with [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords).

- Start the attack.

- There will be different type of responses, check for response that have no error message.

- Copy the username and password, then login after 1 minute.