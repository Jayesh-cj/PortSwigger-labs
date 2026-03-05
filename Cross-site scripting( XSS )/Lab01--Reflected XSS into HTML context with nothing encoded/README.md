# Lab-1: [Reflected XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded)

This lab contains a simple reflected cross-site scripting vulnerability in the search functionality. 

**Aim :-** To solve the lab, perform a cross-site scripting attack that calls the alert function. 



### Solution
- Search using the following payload : ``` <script>alert(123)</script> ``` 

- The payload will force the webpage to show an alert box with **123**. 
