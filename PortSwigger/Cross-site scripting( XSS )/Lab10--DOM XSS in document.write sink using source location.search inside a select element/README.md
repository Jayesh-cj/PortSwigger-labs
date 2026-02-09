# Lab-10: [DOM XSS in document.write sink using source location.search inside a select element](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element)

This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality. It uses the JavaScript ``` document.write ``` function, which writes data out to the page. The ``` document.write ``` function is called with data from ``` location.search ``` which you can control using the website URL. The data is enclosed within a select element. 

**Aim :-** To solve this lab, perform a cross-site scripting attack that breaks out of the select element and calls the alert function. 



## Solution
- The product page source code reveals that the javaScrip extract a ``` storeId ``` from the URL using ``` var store = (new URLSearchParams(window.location.search)).get('storeId'); ``` script and add it into the dropdown using ```  document.write ```

- Add ``` &storeId=123 ``` in the URL after ``` /product?productId=1 ```, notice that in the response the dropdown contains the value ``` 123 ```.

- Use the payload ``` &storeId=123'<script>alert(123)</script> ``` after the ``` /product?productId=1 ``` to force the webpage to perform an alert with 123 value.