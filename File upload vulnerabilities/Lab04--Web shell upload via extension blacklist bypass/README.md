# Lab-4: [Web shell upload via extension blacklist bypass](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-extension-blacklist-bypass)

This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist. 

**Aim :-** To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.

**Hint :-** You need to upload two different files to solve this lab. 



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- There will be a option to upload image.

- Copy the following code and save it in a file, name it as ``` exploit.php ```.
    - ``` <?php echo file_get_contents('/home/carlos/secret'); ?> ```.

- Try uploading the ``` exploit.php ``` file.

- Server will respond with ``` Sorry, php files are not allowed Sorry, there was an error uploading your file. ``` message.

- Intercept upload request using **burp suite**.

- Change the file name to ``` .htaccess ```, change the value of ``` Content-Type: ``` to ``` text/plain ```. Replace the php code with ``` AddType application/x-httpd-php .htm ```. Then send the request.

- This will upload a file named ``` .htaccess ``` with ``` AddType application/x-httpd-php .htm ``` as it's content.
    - The ``` .htaccess ``` (Hypertext Access) file is a powerful, hidden configuration file used by Apache web servers to manage settings on a per-directory basis, allowing customization without modifying the main server configuration.

    - The directive ``` AddType application/x-httpd-php .htm ``` is used in Apache configuration files (like .htaccess) to instruct the server to process files with a .html extension as PHP scripts

- Copy the php code of ``` exploit.php ``` into ``` exploit.htm ```.

- Upload the ``` exploit.htm ```.

- View the image by going to ``` /files/avatars/exploit.htm ```, the server will respond with a secret code.

- Copy the code and submit as solution.