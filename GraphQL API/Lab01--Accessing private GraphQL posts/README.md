# Lab-1:- [Accessing private GraphQL posts](https://portswigger.net/web-security/graphql/lab-graphql-reading-private-posts)
> APPRENTICE

The blog page for this lab contains a hidden blog post that has a secret password.

**Aim :-** To solve the lab, find the hidden blog post and enter the password. 



## Solution
- By burp suite running in the background access the blog page.

- In burp go to **Proxy > HTTP history**.

- Find the request to **GraphQL** endpoint (``` /graphql/v1 ``` ), right click then send it to repeater.

- Send the request the server respond with all the blog posts.

- In the response post number 3 is missing.

- Send the following query in the request
```
{"query": "{__schema{types{name,fields{name}}}}"}
```

- The server respond with the API schema, it shows that there is a field named ``` postPassword ```.

- If gone to the bottom of the response can see the querys also.
```
{
    "name": "query",
    "fields": [
    {
        "name": "getBlogPost"
    },
    {
        "name": "getAllBlogPosts"
    }
    ]
}
```

- To get the 3rd post send the following query in the request
```
{"query": "{getBlogPost(id:3){title,postPassword}}"}
```

- Server will respond with post password copy the password and submit as solution.