# Lab-5: [Information disclosure in version control history](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-version-control-history)

This lab discloses sensitive information via its version control history. 

**Aim :-** To solve the lab, obtain the password for the ``` administrator ``` user then log in and delete the user ``` carlos ```. 



## Solution
- Go to ``` /.git ```. It reveals the git version control data.

- Open a terminal and run ``` wget -r "LAB-URL/.git" ```. This will download the entire git folder.

- Move to that folder ``` cd LAB-URL ```

- Check the git logs ``` git logs ```.

- There is a commit with message ``` Remove admin password from config ```. Copy that commit id.

- Check that commit ``` git show COMMIT-ID ```.

- This will show the details of that commit. There will be the password for **administrator** user copy it.

- Login as **administrator** delete user ``` carlos ```.