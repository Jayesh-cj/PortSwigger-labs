# Lab-28: [Reflected XSS in a JavaScript URL with some characters blocked](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-url-some-characters-blocked)

This lab reflects your input in a JavaScript URL, but all is not as it seems. This initially seems like a trivial challenge; however, the application is blocking some characters in an attempt to prevent XSS attacks. 

To solve the lab, perform a cross-site scripting attack that calls the ``` alert``` function with the string ``` 1337 ``` contained somewhere in the ``` alert ``` message. 



## Solution
- Append the following payload to the end of the web **URL** and make the request.
```javascript
/post?postId=5&%27},x=x=%3E{throw/**/onerror=alert,1337},toString=x,window%2b%27%27,{x:%27
```

- Click on the **Back to Blog** link for alert.


The exploit uses exception handling to call the ``` alert ``` function with arguments. The ``` throw ``` statement is used, separated with a blank comment in order to get round the no spaces restriction. The ``` alert ``` function is assigned to the ``` onerror ``` exception handler.

As ``` throw ``` is a statement, it cannot be used as an expression. Instead, we need to use arrow functions to create a block so that the ``` throw ``` statement can be used. We then need to call this function, so we assign it to the ``` toString ``` property of ``` window ``` and trigger this by forcing a string conversion on ``` window ```. 