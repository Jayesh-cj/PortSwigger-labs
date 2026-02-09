# Lab-12: [Reflected DOM XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-reflected)

This lab demonstrates a reflected DOM vulnerability. Reflected DOM vulnerabilities occur when the server-side application processes data from a request and echoes the data in the response. A script on the page then processes the reflected data in an unsafe way, ultimately writing it to a dangerous sink. 

**Aim :-** To solve this lab, create an injection that calls the ``` alert() ``` function.



## Solution
- Check the source code there is a javaScript file in ``` /resources/js/searchResults.js ```.

- Check the script from ``` /resources/js/searchResults.js ```.

- The script reveals that ``` eval() ``` function is used for JSON response.

- Use ``` \"-alert(123)}// ``` payload for search. The server will popup with an alert box.