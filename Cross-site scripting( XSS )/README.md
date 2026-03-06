# Cross-site scripting (XSS) 
Cross-site scripting (also known as XSS) is a web security vulnerability that allows an attacker to compromise the interactions that users have with a vulnerable application. It allows an attacker to circumvent the same origin policy, which is designed to segregate different websites from each other. Cross-site scripting vulnerabilities normally allow an attacker to masquerade as a victim user, to carry out any actions that the user is able to perform, and to access any of the user's data. If the victim user has privileged access within the application, then the attacker might be able to gain full control over all of the application's functionality and data. 


## Types of XSS attacks

### 1.Reflected cross-site scripting
**Reflected XSS** is the simplest variety of cross-site scripting. It arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way. 

### 2.Stored cross-site scripting
**Stored Cross-Site Scripting(XSS)**, also called **Persistent XSS**, is a dangerous web vulnerability where attackers inject malicious scripts (payloads) into a website, which then permanently stores the script (e.g., in a database) and serves it to unsuspecting users' browsers when they visit the affected page, executing the code with the user's privileges, allowing session hijacking, data theft, or defacement.

### 3.DOM-based cross-site scripting
DOM-based XSS (also known as DOM XSS) arises when an application contains some client-side JavaScript that processes data from an untrusted source in an unsafe way, usually by writing the data back to the DOM. 




### How to prevent XSS attacks

Preventing cross-site scripting is trivial in some cases but can be much harder depending on the complexity of the application and the ways it handles user-controllable data.

In general, effectively preventing XSS vulnerabilities is likely to involve a combination of the following measures: 

   - **Filter input on arrival**. At the point where user input is received, filter as strictly as possible based on what is expected or valid input. 

   - **Encode data on output**. At the point where user-controllable data is output in HTTP responses, encode the output to prevent it from being interpreted as active content. Depending on the output context, this might require applying combinations of HTML, URL, JavaScript, and CSS encoding. 

   - **Use appropriate response headers**. To prevent XSS in HTTP responses that aren't intended to contain any HTML or JavaScript, you can use the Content-Type and X-Content-Type-Options headers to ensure that browsers interpret the responses in the way you intend. 

   - **Content Security Policy**. As a last line of defense, you can use Content Security Policy (CSP) to reduce the severity of any XSS vulnerabilities that still occur. 