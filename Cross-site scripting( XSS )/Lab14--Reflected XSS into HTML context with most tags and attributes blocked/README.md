# Lab-14: [Reflected XSS into HTML context with most tags and attributes blocked](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked)

This lab contains a reflected XSS vulnerability in the search functionality but uses a **web application firewall (WAF)** to protect against common XSS vectors. 

**Aim :-** To solve the lab, perform a cross-site scripting attack that bypasses the **WAF** and calls the print() function. 



## Solution
- Check **WAF**
    - Use a simple **XSS** payload like ``` <img src="x" onerror=alert(123)> ``` for search.

    - The sever responds with ``` 400 Bad Request ``` response and a ``` "Tag is not allowed" ``` error message.

    - Confirms **WAF**

- Find the **tag**
    - Intercept the search request with **Burp Suite** and send it to **Intruder**. Replace the search query with ``` <> ``` and place the cursor in between the angle brackets (``` <> ```) and click the **Add §** button to create payload position. The position will look like ``` <§§> ```

    - Configure the payload with tags, use [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)

    - Start attack.

    - In the responses most of the tags returns ``` 400 Bad Request ``` but the ``` <body> ``` tag returns ``` 200 Ok ```, confirms that ``` <body> ``` tag can be used in the search query.


- Find the **attribute**
    - Intercept another search request with ``` <body =""> ``` as search query and send it to **Intruder**. Place the cursor on left side of the ``` = ``` sign and click the **Add §** button to create payload position. The position will look like ``` <body §§=""> ```

    - Configure the payload with events, use [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)

    - Start attack.

    - In the responses most of the events returns ``` 400 Bad Request ``` but the ``` onresize ``` event returns ``` 200 Ok ```, confirms that ``` <body onresize=""> ``` can be used in the search query.


- Perform **XSS**
    - Search with ``` <body onresize="print()"> ``` and copy the response URL.

    - Use the URL in an ``` <iframe > ``` and craft the payload, The payload will look like the following  
        ``` <iframe src="SEARCH-RESPONSE-URL" onload=this.style.width='500px'> ```.
        - The payload will create a ``` <iframe > ``` with the search response and when that page loads width of that ``` <iframe > ``` will automatically set to ``` 500px ```.

        - This will trigger ``` <body onresize="print()"> ``` payload.

    - Go to the exploit server.

    - Paste the payload on the body section and deliver it to the victim.
