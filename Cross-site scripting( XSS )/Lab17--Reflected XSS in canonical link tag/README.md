# Lab-17: [Reflected XSS in canonical link tag](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag) 

This lab reflects user input in a canonical link tag and escapes angle brackets. 

**Aim :-** To solve the lab, perform a cross-site scripting attack on the home page that injects an attribute that calls the ``` alert ``` function. 

Please note that the intended solution to this lab is only possible in Chrome. 



## Solution
- Right click and **inspect** page there will be a link with ``` rel="canonical" ``` which refers to the webpage it self. ( ``` <link rel="canonical" href="LAB-URL"> ```)

- Add ``` /?1234 ``` in the end of the **web url** then make the request.

- In the response check for any changes in the link, the link changes according to the request url. ( ``` <link rel="canonical" href="LAB-URL/?1234"> ```)

- Add ``` /?'accesskey='x'onclick='alert(123) ``` in the end of the url and make the request.
    - ``` accesskey ``` defines a keyboard shortcut for an element.

- This will make the link like the following
``` <link rel="canonical" href="LAB-URL/?" accesskey="x" onclick="alert(123)"> ```
so when the victim press ``` ALT+x ``` on the keyboard webpage will pop up an alert box with value 123.
