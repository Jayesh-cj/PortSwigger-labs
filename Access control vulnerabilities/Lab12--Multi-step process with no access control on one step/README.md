# Lab-12: [Multi-step process with no access control on one step](https://portswigger.net/web-security/access-control/lab-multi-step-process-with-no-access-control-on-one-step)

This lab has an admin panel with a flawed multi-step process for changing a user's role. You can familiarize yourself with the admin panel by logging in using the credentials ``` administrator:admin ```. 

**Aim :-** To solve the lab, log in using the credentials ``` wiener:peter ``` and exploit the flawed access controls to promote yourself to become an administrator. 



## Solution
- Login as ``` administrator ```.
    - Username : ``` administrator ```.
    - Password : ``` admin ```.

- Upgrade ``` carlos ``` as admin.

- The server respond with a Confirmation page, so the upgrade only done after click yes in the confirmation page.

- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- Make a ``` POST ``` request to ``` /admin-roles ``` with ``` action=upgrade&confirmed=true&username=wiener ``` in the body.