# Lab-4: [User role can be modified in user profile](https://portswigger.net/web-security/access-control/lab-user-role-can-be-modified-in-user-profile)

This lab has an admin panel at ``` /admin ```. It's only accessible to logged-in users with a ``` roleid ``` of 2. 

**Aim :-** Solve the lab by accessing the admin panel and using it to delete the user ``` carlos ```. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login to the account using the credentials.
    - Username : ``` wiener ```
    - Password : ``` peter ```

- Update the email

- In response of update email there is a **JSON** parameter ``` roleid ``` and value of it is ``` 1 ```.

- Intercept the update email request and add ``` "roleid" : 2 ``` in the **JSON**, this will update the user's ``` roleid ``` into ``` 2 ```.

- The user with role id 2 have admin privilege, go to ``` /admin ```.

- Delete the user ``` carlos ```