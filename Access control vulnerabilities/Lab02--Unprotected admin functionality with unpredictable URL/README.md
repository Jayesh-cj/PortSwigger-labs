# Lab-2: [Unprotected admin functionality with unpredictable URL](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url)

This lab has an unprotected admin panel. It's located at an unpredictable location, but the location is disclosed somewhere in the application. 

**Aim :-** Solve the lab by accessing the admin panel, and using it to delete the user ``` carlos ```. 



## Solution
- Go to ``` /login ``` and view the source code.

- In the source code there is a script that reveals the admin panel.
```javascript
<script>
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-dw26b1');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}
</script>
```

- Go to ``` /admin-dw26b1 ```, this will reveal the admin panel.

- Delete the user ``` carlos ```.