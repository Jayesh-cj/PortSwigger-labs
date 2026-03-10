# Lab-6: [Broken brute-force protection, IP block](https://portswigger.net/web-security/authentication/password-based/lab-broken-bruteforce-protection-ip-block)

This lab is vulnerable due to a logic flaw in its password brute-force protection.

**Aim :-** To solve the lab, brute-force the victim's password, then log in and access their account page. 

   - Your credentials: ``` wiener:peter ```.
   - Victim's username: ``` carlos ```.
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)



## Solution
- Try login as ``` carlos ``` using random passwords and find out how the website respond for each attempt.
    - When login attempt is failed for **3** times then the ip is blocked for 1 minute.

    - After **2** failed login attempts use valid credentials to login, it will reset the number of failed login attempts to block the ip.

- Create a usernames list in the order where username ``` wiener ``` appears every third request, while ``` carlos ``` appears in the other two positions.

- The password list must contain all the [candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords), but they are arranged in a specific order to avoid triggering the account lockout mechanism.
    - Two passwords are used to attempt login for ``` carlos ``` (likely to fail).
    - The third password is the valid password ``` peter ``` for the user ``` wiener ```, which results in a successful login.

- Intercept a login request and send it to **intruder**.

- Select username and click **Add §** button. Configure the payload with custom made usernames.

- Select password and click **Add §** button. Configure the payload with custom made passwords.

- Click **Resource pool** to open the Resource pool side panel and set **maximum concurrent request** to **1**.

- Start the attack.

- In the responses check for response that returned **302** status code for ``` carlos ```.

- Use that password to login as ``` carlos ```.