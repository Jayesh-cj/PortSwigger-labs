# Lab-20: [Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-onclick-event-angle-brackets-double-quotes-html-encoded-single-quotes-backslash-escaped) 

This lab contains a stored cross-site scripting vulnerability in the comment functionality. 

**Aim :-** To solve this lab, submit a comment that calls the ``` alert ``` function when the comment author name is clicked. 



## Solution
- Post a comment on a random post.

- In the response code, the website link that provided is reflected inside the ``` onclick ``` event of the anchor tag ( ``` <a > ``` ).

- Use ``` ?&apos;-alert(1)-&apos; ``` to search and in the response click on the link (username posted in the comment) to perform the ``` alert ``` operation.
