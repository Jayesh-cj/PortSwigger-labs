# Lab-4: [DOM XSS in innerHTML sink using source location.search](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink)

This lab contains a DOM-based cross-site scripting vulnerability in the search blog functionality. It uses an ``` innerHTML ``` assignment, which changes the HTML contents of a div element, using data from ``` location.search ```. 

**Aim :-** To solve this lab, perform a cross-site scripting attack that calls the alert function. 



### Solution
- The source code of the webpage reveals that the search query displayed in the webpage using ``` innerHTML ```, So the ``` <script> ``` tag won't work.

- Use the payload ``` <img src="x" onerror=alert(123)> ```

- The payload will append a ``` <img> ``` tag and try to display an image. The source is not valid so it will force to trigger an ``` onerror ``` event.

- The event forces the server to show an alert box with 123 message in it. 
