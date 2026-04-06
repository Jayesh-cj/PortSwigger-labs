# Lab-4: [Arbitrary object injection in PHP](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-arbitrary-object-injection-in-php)

This lab uses a serialization-based session mechanism and is vulnerable to arbitrary object injection as a result.

**Aim :-** To solve the lab, create and inject a malicious serialized object to delete the ``` morale.txt ``` file from Carlos's home directory. You will need to obtain source code access to solve this lab. 

You can log in to your own account using the following credentials: ``` wiener:peter ```.

**Hint :-** You can sometimes read source code by appending a tilde ( ``` ~ ```)  to a filename to retrieve an editor-generated backup file. 



## Solution
- With burp running login as ``` wiener:peter ```.
    - Username : ``` wiener ```.
    - Password : ``` peter ```.

- In **burp suite** go to **Site map** in **targets** tab, check the files of the lab.

- There will be a ``` /CustomTemplate.php ``` file in the ``` /lib ``` folder.

- Make a request to ``` /libs/CustomTemplate.php~ ```, this will reveal the source code of ``` CustomTemplate.php ``` file.

- In the ``` CustomTemplate ``` class there is a ``` __destruct() ``` and it does the following:
```php 
function __destruct() {
        // Carlos thought this would be a good idea
        if (file_exists($this->lock_file_path)) {
            unlink($this->lock_file_path);
        }
    }
```
   - This says that when the object is destroyed, it deletes whatever file is in ``` $lock_file_path ```.

- Make a request to ``` /my-account ``` and intercept the request using **burp suite** then forward it to **repeater**.

- Go to the **decoder** tab in **burp suite**, encode the following in **base64**.
    - ``` O:14:"CustomTemplate":1:{s:14:"lock_file_path";s:23:"/home/carlos/morale.txt";} ```

- Copy the new **Cookie** replace the new **Cookie** in the request in **repeater** then forward the request.