# Lab-14: [2FA bypass using a brute-force attack](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-bypass-using-a-brute-force-attack)

This lab's two-factor authentication is vulnerable to brute-forcing. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code.

**Aim :-** To solve the lab, brute-force the 2FA code and access Carlos's account page. 

   - Victim's credentials: ``` carlos:montoya ```.



## Solution
- With **burp suite** running login as ``` carlos ```.
   - Username : ``` carlos ```.
   - Password : ``` montoya ```.

- Experiment with **2FA** page.
   - After two failed login attempts users will be logged out.

- In **burp** open **Settings** and select **Sessions**.

- In **Session Handling Rules** panel, click Add. 

- Go to **Scope** tab. Under **URL Scope**, select the option **Include all URLs**.

- Go back to the **Details** tab and under **Rule Actions**, add **Run a macro**.

- Under **Select macro** click Add to open the **Macro Recorder**. Select the following 3 requests then click ok.
```bash
GET /login
POST /login
GET /login2
```

- Click **Test macro**. Close all tabs by clicking **ok**.

- Send the ``` POST /login2 ``` request to **intruder**.

- Select ``` mfa-code ``` and click **Add §** button.

- Select the payload type as **Numbers**.

- Configure the payload to start **from 0000 to 9999**, Set the **maximum and minimum** integer to **4**.

- In **Resource Pool** set the **Maximum concurrent requests** to **1**.

- Start the attack.

- From responses check for a response with **302** status code.

- Right click on the the response and click **Open response in browser**.

- Copy the **URL**. Go back to the browser and make the request.