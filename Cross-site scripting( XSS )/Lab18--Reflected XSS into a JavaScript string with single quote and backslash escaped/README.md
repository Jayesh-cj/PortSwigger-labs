# Lab-18: [Reflected XSS into a JavaScript string with single quote and backslash escaped](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-single-quote-backslash-escaped) 

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality. The reflection occurs inside a JavaScript string with single quotes and backslashes escaped. 

**Aim :-** To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the ``` alert ``` function. 



## Solution
- Try searching with a random string.

- In the response page the random string used to search is reflected in the script.

- Try searching with ``` </script> ``` tag.

- In the response the js script is broken and the remaining part of the script is shown in the webpage.

- Search with ``` </script><script>alert(123)</script> ```.

- This will break the script and append the new script with ``` alert ``` function in the response.
