# Lab-3: [Blind SSRF with out-of-band detection](https://portswigger.net/web-security/ssrf/blind/lab-out-of-band-detection)

This site uses analytics software which fetches the URL specified in the Referer header when a product page is loaded.

**Aim :-** To solve the lab, use this functionality to cause an HTTP request to the public Burp Collaborator server. 



## Solution
- View a product and intercept the request using **burp suite**. Send the request to **repeater**.

- Select the ``` Referer : ``` value right click and select **Insert Collaborator Payload** to replace the link with collaborator domain link.

- Forward the request.

- Go to **collaborator** click **Poll now**. This will show the requests that are made to the collaborator.