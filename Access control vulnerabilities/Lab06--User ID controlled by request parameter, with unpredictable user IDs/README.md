# Lab-6: [User ID controlled by request parameter, with unpredictable user IDs](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-unpredictable-user-ids)

This lab has a horizontal privilege escalation vulnerability on the user account page, but identifies users with GUIDs. 

To solve the lab, find the GUID for ``` carlos ```, then submit his API key as the solution.

You can log in to your own account using the following credentials: ``` wiener:peter ```



## Solution
- Login with given credentials.
    - Username : ``` wiener ```
    - Password : ``` peter ```

- View a post that is posted by user ``` carlos ```.

- There will be a link with name ``` carlos ```, to show posts of ``` carlos ```. Click  on the link.

- The response the **URL** will contain the user id of ``` carlos ```.

- Copy the user id and make a request to ``` /my-account?id=<CARLOS-USER-ID> ```.

- ``` carlos ``` my account page will be accessible, copy the **API Key** and submit as solution.