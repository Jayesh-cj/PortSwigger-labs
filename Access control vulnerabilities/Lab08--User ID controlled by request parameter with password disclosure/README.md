# Lab-8: [User ID controlled by request parameter with password disclosure](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-password-disclosure)

This lab has user account page that contains the current user's existing password, prefilled in a masked input. 

**Aim :-** To solve the lab, retrieve the administrator's password, then use it to delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```



## Solution
- Login with the given credentials
    - Username : ``` wiener ```
    - Password : ``` peter ```

- Go to ``` /my-account?id=administrator ```.

- Copy the password of ``` administrator ```.

- Log out and then log in as ``` administrator ```.

- Go to ``` /admin ``` delete the user ``` carlos ```.