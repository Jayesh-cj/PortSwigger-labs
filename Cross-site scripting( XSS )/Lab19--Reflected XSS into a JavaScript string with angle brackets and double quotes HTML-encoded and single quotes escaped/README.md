# Lab-19: [Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-double-quotes-encoded-single-quotes-escaped) 

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets and double are HTML encoded and single quotes are escaped. 

**Aim :-** To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the ``` alert ``` function. 



## Solution
- The server encodes angle brackets ( ``` < ```,``` > ``` ) and double quotes ( ``` " ``` ).

- Search with ``` \'-alert(1)// ```, this will break the script and force the webpage to perform an alert function.
