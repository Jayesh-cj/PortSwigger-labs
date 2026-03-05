# Lab-3: [User role controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)

This lab has an admin panel at ``` /admin ```, which identifies administrators using a forgeable cookie. 

**Aim :-** Solve the lab by accessing the admin panel and using it to delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login to the lab using given credentials.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- In the response there is a cookie ``` admin : false ```, this defines the access control.

- Change the cookie to ``` admin : true ``` and make a request to ``` /admin ```.

- Now the admin panel is revealed delete the user ``` carlos ```.