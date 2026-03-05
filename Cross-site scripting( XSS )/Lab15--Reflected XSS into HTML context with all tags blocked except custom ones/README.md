# Lab-15: [Reflected XSS into HTML context with all tags blocked except custom ones](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-all-standard-tags-blocked) 

This lab blocks all HTML tags except custom ones. 

**Aim :-** To solve the lab, perform a cross-site scripting attack that injects a custom tag and automatically alerts ``` document.cookie ```. 



## Solution
- Try searching with ``` <img src=x onerror=alert(123)> ```, this returns with **Tag is not allowed** error message.

- It confirms default tags are not allowed.

- Try with a custom tag, for example ``` <xss> ``` it returns with **200 OK** response.

- Confirms that **custom made tags are allowed**.

- Search with a custom ``` <xss id=x onfocus=alert(document.cookie) tabindex=1> ```.

- Copy the search response **URL**.

- Go to the **exploit server** and in the body section paste the following payload.
```
<script>
location = 'SEARCH-RESPONSE-URL';
</script>
```
  deliver the exploit.
