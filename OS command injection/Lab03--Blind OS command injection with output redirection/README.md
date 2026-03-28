# Lab-3: [Blind OS command injection with output redirection](https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection)

This lab contains a blind OS command injection vulnerability in the feedback function. 

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at: 

```bash
/var/www/images/
```

The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file. 

**Aim :-** To solve the lab, execute the ``` whoami ``` command and retrieve the output. 



## Solution
- Submit a feedback and intercept the request using **burp suite** and send it to **repeater**.

- Append the following command to the value of **email**
    ``` ||whoami>/var/www/images/output.txt||``` this will execute the command ``` whoami ``` and store the output in ``` /var/www/images/output.txt ```.

- Forward the request.

- Open a product's image in new tab.

- In the **URL** change the ``` filename ``` to ``` output.txt ``` and make the request.