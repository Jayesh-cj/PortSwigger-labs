# Lab-7: [Reflected XSS into attribute with angle brackets HTML-encoded](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-attribute-angle-brackets-html-encoded) 

This lab contains a reflected cross-site scripting vulnerability in the search blog functionality where angle brackets are HTML-encoded.

**Aim :-**  To solve this lab, perform a cross-site scripting attack that injects an attribute and calls the ``` alert ``` function. 

**Hint :-** Just because you're able to trigger the ``` alert() ``` yourself doesn't mean that this will work on the victim. You may need to try injecting your proof-of-concept payload with a variety of different attributes before you find one that successfully executes in the victim's browser. 



## Solution
- Search a random string on the page and analyze the request and response in **Burp Suite**.

- In the response the string used to search is displayed in the search box as value.

- Search with ``` "onmouseover="alert(123) ``` payload.
    - ``` " ``` in the payload will break the ``` value ``` attribute of the searchbox.

    - ``` onmouseover ``` will act as a new **HTML event handler attribute**.
    
    - When hover the mouse over searchbox the webpage will popup with an alert box with 123.
