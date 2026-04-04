# Lab-7: [Web shell upload via race condition](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-race-condition)

This lab contains a vulnerable image upload function. Although it performs robust validation on any files that are uploaded, it is possible to bypass this validation entirely by exploiting a race condition in the way it processes them.

**Aim :-** To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file ``` /home/carlos/secret ```. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: wiener:peter 

**Hint :-**  The vulnerable code that introduces this race condition is as follows:
```php
<?php
$target_dir = "avatars/";
$target_file = $target_dir . $_FILES["avatar"]["name"];

// temporary move
move_uploaded_file($_FILES["avatar"]["tmp_name"], $target_file);

if (checkViruses($target_file) && checkFileType($target_file)) {
    echo "The file ". htmlspecialchars( $target_file). " has been uploaded.";
} else {
    unlink($target_file);
    echo "Sorry, there was an error uploading your file.";
    http_response_code(403);
}

function checkViruses($fileName) {
    // checking for viruses
    ...
}

function checkFileType($fileName) {
    $imageFileType = strtolower(pathinfo($fileName,PATHINFO_EXTENSION));
    if($imageFileType != "jpg" && $imageFileType != "png") {
        echo "Sorry, only JPG & PNG files are allowed\n";
        return false;
    } else {
        return true;
    }
}
?>
```



## Solution
- Login as ``` wiener ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- There will be a option to upload image.

- Copy the following code and save it in a file, name it as ``` exploit.php ```.
    - ``` <?php echo file_get_contents('/home/carlos/secret'); ?> ```.

- Try uploading the file.

- The server will respond with ``` Sorry, only JPG & PNG files are allowed Sorry, there was an error uploading your file. ```.

- As per the vulnerable code server first moves the file to specified location then checks for virus and file type, then removes it if there is any issue. So the file will be in the server for a small amount of time.

- Upload ``` exploit.php ``` and intercept the request using **burp suite** then send it to **repeater**.

- Make a ``` GET ``` request to ``` /files/avatars/exploit.php ``` and intercept it using **burp suite** then send it to **repeater**.

- Go to **repeater** tab in **burp suite** right click on a request tab click **add tab to group** and **create a tab group with both of the request**.

- Click the drop down right side of the send button select **Send group in parallel**.

- Send the request multiple times and check the ``` GET /files/avatars/exploit.php ``` request. Server may return with the secret code. If not send the request again.

- Copy the code and submit as solution.