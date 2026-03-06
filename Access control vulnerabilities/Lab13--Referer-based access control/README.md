# Lab-13: [Referer-based access control](https://portswigger.net/web-security/access-control/lab-referer-based-access-control)

This lab controls access to certain admin functionality based on the Referer header. You can familiarize yourself with the admin panel by logging in using the credentials ``` administrator:admin ```. 

**Aim :-** To solve the lab, log in using the credentials ``` wiener:peter ``` and exploit the flawed access controls to promote yourself to become an administrator. 



## Solution
- Login as ``` administrator ```.
    - Username : ``` administrator ```.
    - Password : ``` admin ```.

- Upgrade ``` carlos ``` as admin, observe the request and response.

- The client makes a ``` GET ``` request to ``` /admin-roles?username=carlos&action=upgrade ```.

- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Make a ``` GET ``` request to ``` /admin-roles?username=carlos&action=upgrade ```.

- The server respond with ``` Unauthorized ```.

- In the request header change the ``` Referer ``` to ``` /admin ```, forward the request.