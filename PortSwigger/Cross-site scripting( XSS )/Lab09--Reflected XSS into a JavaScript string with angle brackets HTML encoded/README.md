# Lab-9: [Reflected XSS into a JavaScript string with angle brackets HTML encoded](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded)

This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets are encoded. The reflection occurs inside a JavaScript string.

**Aim :-** To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the ``` alert ``` function. 



## Solution
- Search with a random string.

- View the source code of the search result.
    ```
    <script>
        var searchTerms = 'abc';
        document.write('<img src="/resources/images/tracker.gif?searchTerms='+encodeURIComponent(searchTerms)+'">');
    </script>
    ```
    - The source code reveals that the search string (``` abc ```) is displayed in the script directly.


- Use ``` '-alert(123)-' ``` payload to search.
    - ``` ' ``` will break the script.

    - ``` - ``` used as separators to avoid syntax errors or bypass weak filters.


- The payload will force the webpage to perform an alert with 123 value.