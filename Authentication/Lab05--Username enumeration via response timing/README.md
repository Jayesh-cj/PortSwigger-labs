# Lab-5: [Username enumeration via response timing](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-response-timing)

This lab is vulnerable to username enumeration using its response times.

**Aim :-** To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page. 

   - Your credentials: ``` wiener:peter ```.
   - [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

**Hint :-** To add to the challenge, the lab also implements a form of IP-based brute-force protection. However, this can be easily bypassed by manipulating HTTP request headers. 



## Solution
- Try to login as ``` wiener ``` and intercept the request then send to **Repeater**.
   - Username : ``` wiener ```.
   - Password : ``` peter ```.

- Experiment with different usernames and passwords, and find out how the application behaves.
   - After some try the application blocks the ip for 30 minutes. But using ``` X-Forwarded-For ``` heder can bypass this block.

   - When using a invalid username the response time is same.

   - When using a valid username and a valid password ( ``` wiener : peter ``` ) the response time is same.

   - When using a valid username ( ``` wiener ``` ) and a invalid password the response time differs depends on the length of the password.

- Send the login request to **Intruder**.

- Select attack type **Pitchfork attack**.

- Add ``` X-Forwarded-For: ``` in the header and place the cursor on the right of the ``` : ``` then click **Add §** to create **payload position 1**.

- Select username and click **Add §** button to create **payload position 2**.

- Select payload type as **Numbers** for **payload position 1** and configure the payload to start from 1 to 100.

- Select payload type as **Simple list** for **Payload position 2** and configure the payload with [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames).

- Set the password to a very long string of characters ( about 100 characters should do it ). 

- Start the attack.

- After the attack finished click Columns and select the **Response received** and **Response completed** options. These two columns are now displayed in the results table. 

- Check for a response that took long time to respond.

- Copy the username, back to **Intruder** paste the username.

- Select the password and click **Add §** to make the password as the **payload position 2**.

- Configure with [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords) in **payload position 2**.

- Start the attack.

- Check for a response that returns **302** status code.

- Copy the username and password and login with that.