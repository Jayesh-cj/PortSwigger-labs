# Lab-8: [Stored XSS into anchor href attribute with double quotes HTML-encoded](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded) 

This lab contains a stored cross-site scripting vulnerability in the comment functionality. 

**Aim :-** To solve this lab, submit a comment that calls the alert function when the comment author name is clicked. 



## Solution
- Put a random comment on a post

- In the response source code the website link that submitted in the comment reflected in ``` href ``` attribute.

- Submit a new comment with ``` javascript:alert(123) ``` payload as website link.
    - This will reflect as ``` href ``` attribute value in the response.

    - By clicking the name the webpage will popup an alert box with 123 value.
