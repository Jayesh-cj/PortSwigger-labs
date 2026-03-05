# Lab-7: [User ID controlled by request parameter with data leakage in redirect](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-data-leakage-in-redirect)

This lab contains an access control vulnerability where sensitive information is leaked in the body of a redirect response

**Aim :-** To solve the lab, obtain the API key for the user ``` carlos ``` and submit it as the solution. 

You can log in to your own account using the following credentials: ``` wiener:peter ```



## Solution
- Login with given credentials.
    - Username : ``` wiener ```
    - Password : ``` peter ```

- Intercept the request to ``` /my-account?id=wiener ```.

- Change the ``` id ``` to ``` carlos ``` and forward the request.

- Before redirecting the server respond with ``` carlos ``` my account page.

- Copy the **API Key** and submit as result.