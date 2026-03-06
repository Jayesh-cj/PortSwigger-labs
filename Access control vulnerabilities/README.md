# Access control vulnerabilities

Access control is the application of constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management: 
   
   - **Authentication** confirms that the user is who they say they are.
   - **Session management** identifies which subsequent HTTP requests are being made by that same user.
   - **Access control** determines whether the user is allowed to carry out the action that they are attempting to perform.

Broken access controls are common and often present a critical security vulnerability. Design and management of access controls is a complex and dynamic problem that applies business, organizational, and legal constraints to a technical implementation. Access control design decisions have to be made by humans so the potential for errors is high. 


### Vertical privilege escalation

If a user can gain access to functionality that they are not permitted to access then this is vertical privilege escalation. For example, if a non-administrative user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation. 



### Horizontal privilege escalation

Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of that type. For example, if an employee can access the records of other employees as well as their own, then this is horizontal privilege escalation. 



### How to prevent access control vulnerabilities

Access control vulnerabilities can be prevented by taking a defense-in-depth approach and applying the following principles:

   - Never rely on obfuscation alone for access control.
   
   - Unless a resource is intended to be publicly accessible, deny access by default.
   
   - Wherever possible, use a single application-wide mechanism for enforcing access controls.
   
   - At the code level, make it mandatory for developers to declare the access that is allowed for each resource, and deny access by default.
    
   - Thoroughly audit and test access controls to ensure they work as designed.
