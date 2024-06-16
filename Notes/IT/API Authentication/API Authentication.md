

### 1. API Key

- A simple method where an API key is passed in the HTTP request to authenticate.
- Key can be included in the header or query parameters.
- Simple to implement but requires protection to prevent unauthorized access.
### 2. BASIC Authentication

- Not secured because the keys are exposed on each request (unless used over HTTPS)
- Transmits username and password with each HTTP request.
- Credentials are Base64 encoded and sent in the `Authorization` header.

```
Authorization: Basic <base64-encoded-credentials>
```
### 3. Digest Authentication

- More secure than Basic Authentication:
	- Server sends a nonce (one-time-number) to the client.
	- Client use the nonce to hash the password and other information.
	- Client sends the hashed password to the Server
	- Server performs the hashing too and compares the results. If they match the authentication is successful.

### 4. OAuth 2.0

- Robust security
- 'Open Authorization'. It allows a website or application to access resources hosted by other web apps on behalf of a user **without ever sharing the user's credentials**
- It is an authorization protocol and not an authentication protocol.

Roles
	Resource Owner:
		The user or system that owns the protected resource.
	Client:
		The application that wants to access that Resource Owner protected resource.
		To access the resources the Client must hold the Access Token.
	Authorization Server:
		Receives requests from the Client for Access Tokens.
		Issues the tokens upon successful authentication and consent by the Resource Owner
		Emits:
			Access Token.
			Refresh Token.
	Resource Server:
		Stores the protected resource that we want to access.