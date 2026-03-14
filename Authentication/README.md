# Authentication

Conceptually, authentication vulnerabilities are easy to understand. However, they are usually critical because of the clear relationship between authentication and security. 

Authentication vulnerabilities can allow attackers to gain access to sensitive data and functionality. They also expose additional attack surface for further exploits. For this reason, it's important to learn how to identify and exploit authentication vulnerabilities, and how to bypass common protection measures. 


### What is authentication?
Authentication is the process of verifying the identity of a user or client. Websites are potentially exposed to anyone who is connected to the internet. This makes robust authentication mechanisms integral to effective web security.

There are three main types of authentication: 
   - **Something you know**, such as a password or the answer to a security question. These are sometimes called **"knowledge factors"**. 
   
   - **Something you have**, This is a physical object such as a mobile phone or security token. These are sometimes called **"possession factors"**. 

   - **Something you are or do**. For example, your biometrics or patterns of behavior. These are sometimes called **"inherence factors"**. 

Authentication mechanisms rely on a range of technologies to verify one or more of these factors. 


### What is the difference between authentication and authorization?
**Authentication** is the process of verifying that a user is who they claim to be. 
**Authorization** involves verifying whether a user is allowed to do something. 


### How do authentication vulnerabilities arise?
Most vulnerabilities in authentication mechanisms occur in one of two ways: 
   - The authentication mechanisms are weak because they fail to adequately protect against brute-force attacks. 

   - Logic flaws or poor coding in the implementation allow the authentication mechanisms to be bypassed entirely by an attacker. This is sometimes called "broken authentication". 


## Prevent Authentication Vulnerabilities
- **Use strong password handling**
    - Store passwords with a strong one-way hash
    - Never store plain-text passwords
    - Use unique salts

- **Add MFA**
    - Multi-factor authentication blocks a lot of damage even if passwords are stolen
    - Prefer authenticator apps, passkeys, or hardware keys over SMS when possible

- **Prevent brute force and credential stuffing**
    - Rate limit login attempts
    - Add account lockout carefully, or better, temporary delays / progressive throttling
    - Detect repeated failed logins from same IP, device, or account
    - Monitor for credential stuffing patterns

- **Stop username enumeration**
    - Use the same error message for:
        - wrong username
        - wrong password
        - locked account
        - reset requests
    - Keep response timing as similar as possible

- **Secure session management**
    - Generate strong random session IDs
    - Regenerate session ID after login
    - Expire sessions on logout
    - Use short session lifetimes for sensitive apps

- **Protect password reset**
    - Use single-use, random, time-limited reset tokens
    - Do not expose whether an email exists
    - Invalidate reset tokens after use
    - Send reset links only over HTTPS
    - Require re-authentication for sensitive account changes