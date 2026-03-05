# Lab-13: [Stored DOM XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored) 

This lab demonstrates a stored DOM vulnerability in the blog comment functionality.

**Aim :-** To solve this lab, exploit this vulnerability to call the ``` alert() ``` function. 



## Solution
- The source code reveals that ``` /resources/js/loadCommentsWithVulnerableEscapeHtml.js ``` contains javaScript code.

- Check the script from ``` /resources/js/loadCommentsWithVulnerableEscapeHtml.js ```.

- In the script ``` replace() ``` function is used to encode angle brackets.

- Use ``` <><img src=x onerror=alert(123)> ``` payload for popup the alert box.
    - The ``` replace() ``` function will only replaces the first sting.
