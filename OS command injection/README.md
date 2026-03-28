# OS command injection

OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data. Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure, and exploit trust relationships to pivot the attack to other systems within the organization. 


## How to prevent OS command injection attacks
The most effective way to prevent OS command injection vulnerabilities is to never call out to OS commands from application-layer code. In almost all cases, there are different ways to implement the required functionality using safer platform APIs. 

If you have to call out to OS commands with user-supplied input, then you must perform strong input validation. Some examples of effective validation include: 
   
   - Validating against a whitelist of permitted values. 
   - Validating that the input is a number. 
   - Validating that the input contains only alphanumeric characters, no other syntax or whitespace. 

