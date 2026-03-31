# Lab-3: [Source code disclosure via backup files](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-via-backup-files)

This lab leaks its source code via backup files in a hidden directory.

**Aim :-** To solve the lab, identify and submit the database password, which is hard-coded in the leaked source code. 


## Solution
- Go to ``` /robots.txt ``` in the lab.

- There will be the path to backup folder, go to ``` /backup ```.

- Backup shows a file open it ( ``` /backup/ProductTemplate.java.bak ``` ).

- It's the source code. In the source code, notice that the **connection builder contains** the hard-coded password for a Postgres database. 

- Copy the password and submit as solution.