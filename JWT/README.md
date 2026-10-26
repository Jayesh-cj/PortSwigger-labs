# JWT (JSON web tokens)

### What are JWTs?
JSON web tokens (JWTs) are a standardized format for sending cryptographically signed JSON data between systems. They can theoretically contain any kind of data, but are most commonly used to send information ("claims") about users as part of authentication, session handling, and access control mechanisms.

Unlike with classic session tokens, all of the data that a server needs is stored client-side within the JWT itself. This makes JWTs a popular choice for highly distributed websites where users need to interact seamlessly with multiple back-end servers. 


### JWT format
A JWT consists of 3 parts: a **header**, a **payload**, and a **signature**. These are each separated by a dot. The header and payload parts of a JWT are just base64url-encoded JSON objects. The header contains metadata about the token itself, while the payload contains the actual "claims" about the user. In most cases, this data can be easily read or modified by anyone with access to the token. Therefore, the security of any JWT-based mechanism is heavily reliant on the cryptographic signature. 


### JWT signature

The server that issues the token typically generates the signature by hashing the header and payload. In some cases, they also encrypt the resulting hash. Either way, this process involves a secret signing key. This mechanism provides a way for servers to verify that none of the data within the token has been tampered with since it was issued:

   - As the signature is directly derived from the rest of the token, changing a single byte of the header or payload results in a mismatched signature.

   - Without knowing the server's secret signing key, it shouldn't be possible to generate the correct signature for a given header or payload.


### JWT vs JWS vs JWE
The JWT specification is actually very limited. It only defines a format for representing information ("claims") as a JSON object that can be transferred between two parties. In practice, JWTs aren't really used as a standalone entity. The JWT spec is extended by both the JSON Web Signature (JWS) and JSON Web Encryption (JWE) specifications, which define concrete ways of actually implementing JWTs. In other words, a JWT is usually either a JWS or JWE token. When people use the term "JWT", they almost always mean a JWS token. JWEs are very similar, except that the actual contents of the token are encrypted rather than just encoded. 



## How to prevent JWT attacks
You can protect your own websites against many of the attacks we've covered by taking the following high-level measures:

   - Use an up-to-date library for handling JWTs and make sure your developers fully understand how it works, along with any security implications. Modern libraries make it more difficult for you to inadvertently implement them insecurely, but this isn't foolproof due to the inherent flexibility of the related specifications.

   - Make sure that you perform robust signature verification on any JWTs that you receive, and account for edge-cases such as JWTs signed using unexpected algorithms.

   - Enforce a strict whitelist of permitted hosts for the jku header.

   - Make sure that you're not vulnerable to path traversal or SQL injection via the kid header parameter.

### Additional best practice for JWT handling
Although not strictly necessary to avoid introducing vulnerabilities, we recommend adhering to the following best practice when using JWTs in your applications:

   - Always set an expiration date for any tokens that you issue.

   - Avoid sending tokens in URL parameters where possible.

   - Include the aud (audience) claim (or similar) to specify the intended recipient of the token. This prevents it from being used on different websites.

   - Enable the issuing server to revoke tokens (on logout, for example).
