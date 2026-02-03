# Lab-2: [Stored XSS into HTML context with nothing encoded](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded)

This lab contains a stored cross-site scripting vulnerability in the comment functionality. 

**Aim :-** To solve this lab, submit a comment that calls the alert function when the blog post is viewed. 



### Solution
- View a post in the application

- Post a comment with the payload ``` <script>alert(123)</script> ```

- The payload will save in the database and display as comment, so whenever that post is viewed the server will show an alert box with 123 value.