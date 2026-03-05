# Lab-11: [Method-based access control can be circumvented](https://portswigger.net/web-security/access-control/lab-method-based-access-control-can-be-circumvented)

This lab implements access controls based partly on the HTTP method of requests. You can familiarize yourself with the admin panel by logging in using the credentials ``` administrator:admin ```. 

**Aim :-** To solve the lab, log in using the credentials ``` wiener:peter ``` and exploit the flawed access controls to promote yourself to become an administrator. 



## Solution
- Login as ``` administrator ```
    - Username : ``` administrator ```
    - Password : ``` admin ```

- Upgrade user carlos as admin and check the request.

- The client makes a ``` POST ``` request to ``` /admin-roles ``` with ``` username=carlos&action=upgrade ``` in the body.

- Login as ``` wiener ```
    - Username : ``` wiener ```
    - Password : ``` peter ```

- Make a ``` POST ``` request to ``` /admin-roles ```. The sever respond with ``` Unauthorized ```.

- Change the ``` POST ``` request to ```POSTX ``` and make the request. Server now respond with ``` "Missing parameter 'username'" ```

- Add ``` username=wiener&action=upgrade ``` in the request body.

- In the burp suite repeater right click and **Change request method**. The request will change to ``` GET /admin-roles?username=wiener&action=upgrade ```, make the request.