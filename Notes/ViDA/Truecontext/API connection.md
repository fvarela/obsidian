
[HTTP Connection (truecontext.com)](https://docs.truecontext.com/1374411/Content/Published/217500628_HTTPConnection.html#Authenticationoptions)

[TrueContext API (prontoforms.com)](https://live.prontoforms.com/api-docs)

[TrueContext API (prontoforms.com)](https://live.prontoforms.com/api-docs#section/Error-Handling/Response-codes)

![[truecontext.jpg]]

OAuth connection:

Resource Owner (TrueContext):
	The user who grants permission to access their data.
Client (Azure Function):
	The application that request access tokens from the authorization server and makes API calls to the Resource Server (TrueContext)
Authorization Server (Azure Active Directory):
	Authenticates the resource owner
	Generates access token to the client after authorization
Resource Server (TrueContext):
	Where the resources reside

OAuth2 Flow:

- **Step 1: Client Request** - The Azure Function (client) starts the process, perhaps triggered by an internal requirement or an external request, by directing a request to TrueContext.
    
- **Step 2: Redirect to Authorization Server** - TrueContext, upon receiving the request, determines that authentication is required and redirects the request to Azure Active Directory (AAD). This redirection includes the necessary OAuth parameters such as client ID, scope, response type, and redirect URI.
    
- **Step 3: User Authentication and Consent** - The user (resource owner) interacts with AAD to authenticate (login) and grant consent for the requested scopes. This step typically involves entering credentials and approving access permissions that the Azure Function is requesting.
    
- **Step 4: Authorization Response** - Upon successful authentication and consent, AAD redirects back to the TrueContext specified redirect URI (which was part of the OAuth configuration), including an authorization code.
    
- **Step 5: Token Exchange** - TrueContext, receiving the authorization code, makes a request to the AAD token endpoint to exchange the authorization code for an access token.
    
- **Step 6: Token Use to Access Resource** - TrueContext, now in possession of an access token, accepts subsequent requests from the Azure Function that include this access token, granting access based on the allowed scopes associated with the token.


