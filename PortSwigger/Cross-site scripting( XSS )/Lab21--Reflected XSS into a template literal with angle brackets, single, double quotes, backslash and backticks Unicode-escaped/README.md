# Lab-21: [Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-template-literal-angle-brackets-single-double-quotes-backslash-backticks-escaped)

This lab contains a reflected cross-site scripting vulnerability in the search blog functionality. The reflection occurs inside a template string with angle brackets, single, and double quotes HTML encoded, and backticks escaped.

**Aim :-** To solve this lab, perform a cross-site scripting attack that calls the ``` alert ``` function inside the template string. 



## Solution
- This lab encodes angle brackets ( ``` <, > ``` ), single quotes ( ``` ' ``` ) and double quotes ( ``` " ``` ).

- Try searching with a random string and check the response source code.

- In the response the search string is displayed inside the backticks ( ``` ` ``` ).

- Use ``` ${ alert(123) } ``` to search, this payload will be inside the backticks ( ``` ` ``` ).
    - Anything inside backticks ( ``` ` ``` ) executes as javascript.