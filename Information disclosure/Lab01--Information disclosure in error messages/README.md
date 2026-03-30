# Lab-1: [Information disclosure in error messages](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-error-messages)

This lab's verbose error messages reveal that it is using a vulnerable version of a third-party framework.

**Aim :-** To solve the lab, obtain and submit the version number of this framework.



## Solution
- View a product in the lab.

- The **URL** will contain a ``` productId ```, change the number to a random string and make the request ( ``` /product?productId=abc ``` ).

- The server will respond with a error page.

- Copy the Apache version and submit as solution.