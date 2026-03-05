# Lab-3: [DOM XSS in document.write sink using source location.search](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink)

This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript ``` document.write ``` function, which writes data out to the page. The ``` document.write ``` function is called with data from ``` location.search ```, which you can control using the website URL. 

**Aim :-** To solve this lab, perform a cross-site scripting attack that calls the ``` alert ``` function. 



### Solution
- The source code of the server reveals that the search query is displayed in the website by ``` document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">'); ```

- Use the following payload ``` "><script>alert(123)</script> ```

- The ``` "> ``` will break the ``` src ``` and append the script to the source code, It will force the server to show an alert box with 123 value. 
