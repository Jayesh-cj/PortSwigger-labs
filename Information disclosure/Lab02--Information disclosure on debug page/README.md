# lab-2: [Information disclosure on debug page](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-on-debug-page)

This lab contains a debug page that discloses sensitive information about the application. 

**Aim :-** To solve the lab, obtain and submit the ``` SECRET_KEY ``` environment variable. 



## Solution
- View source code of the home page, in the bottom of the page there is a link to **Debug** page.

- Go to that **Debug** page (``` /cgi-bin/phpinfo.php ``` ).

- Search for ``` SECRET_KEY ```.

- Copy the key and submit as solution.