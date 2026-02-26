# Lab-11: [DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression)

This lab contains a DOM-based cross-site scripting vulnerability in a AngularJS expression within the search functionality. 

AngularJS is a popular JavaScript library, which scans the contents of HTML nodes containing the ``` ng-app ``` attribute (also known as an AngularJS directive). When a directive is added to the HTML code, you can execute JavaScript expressions within double curly braces. This technique is useful when angle brackets are being encoded. 

**Aim :-** To solve this lab, perform a cross-site scripting attack that executes an AngularJS expression and calls the alert function.



## Solution
- Search with ``` {{ 7*7 }} ```, the webpage will respond with **49** value confirms that **XSS** is possible.

- Search with ``` {{constructor.constructor('alert(1)')()}} ``` payload, it will force the webpage to show a popup box with 123 value.