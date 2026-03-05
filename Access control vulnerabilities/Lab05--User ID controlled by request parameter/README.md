# Lab-5: [User ID controlled by request parameter ](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter)

This lab has a horizontal privilege escalation vulnerability on the user account page. 

**Aim :-** To solve the lab, obtain the API key for the user ``` carlos ``` and submit it as the solution. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login to the lab using credentials
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- In ``` /my-account ``` there is a parameter and value ( ``` ?id=wiener ``` ).

- Make a request to ``` /my-account?id=carlos ``` this will reveal user ``` carlos ``` **API Key**, copy it and submit as solution.