# Lab-9: [Brute-forcing a stay-logged-in cookie](https://portswigger.net/web-security/authentication/other-mechanisms/lab-brute-forcing-a-stay-logged-in-cookie)

This lab allows users to stay logged in even after they close their browser session. The cookie used to provide this functionality is vulnerable to brute-forcing. 

**Aim :-** To solve the lab, brute-force Carlos's cookie to gain access to his **My account** page.

   - Your credentials: ``` wiener:peter ```
   - Victim's username: ``` carlos ```
   - [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)



## Solution
- Login as ``` wiener ``` leave the **stay logged in check box ticked**.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- After login there will be a cookie named ``` stay-logged-in ```, and value of this cookie will be in **base64** encoded format.

- After decoding the **base64** cookie will look like ``` wiener:51dc30ddc473d43a6011e9ebba6ca770 ```.

- The cookie consist of username and a hash value use [Hash Analyzer](https://www.tunnelsup.com/hash-analyzer/) to find the hash type. The hash type is **MD5**.

- Use [Crack Station](https://crackstation.net/) to find the plain text. The hash value is the password of user ``` wiener ```.

- Intercept ``` GET /my-account?id=wiener ``` request and send to **intruder**.

- Change value of ``` ?id= ``` to ``` carlos ```.

- Select the ``` stay-logged-in ``` cookie, click **Add §** button.

- Configure the payload with [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords).

- In **Payload Processing** add the following rules.
    - **Hash**: ``` MD5 ```.
    - **Add prefix**: ``` carlos: ```.
    - **Encode**: ``` Base64-encode ```.

- Remove the ``` session ``` from the request header.

- The response page will have a **Update email** button use this to filter the valid response.

- Select **settings** from the side panel of intruder. Add ``` Update email ``` in **Gep Match**.

- Start the attack.

- In responses only one of the response will have the **Update email** button.

- Lab will be solved.