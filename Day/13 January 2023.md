`13 January 2023`
## **Day 27 What I Have Learned**
***
## **OpenID Connect Issues**:
- OIDC (Open ID Connect) is an authentication layer on top of OAuth 2.0, an authorization framework. The standard is controlled by the OpenID Foundation.
- It allows Clients to verify the identity of the End-User based on the authentication performed by an Authorization Server, as well as to obtain basic profile information about the End-User in an interoperable and REST-like manner.
- While OAuth 2.0 is about resource access and sharing, OIDC is about user authentication
- Its purpose is to give you one login for multiple sites
- For example, if you chose to sign in to Auth0 using your Google account then you used OIDC. Once you successfully authenticate with Google and authorize Auth0 to access your information.
***
## **Attack Vectors**
1. Login Confusion Attack
- The victim visits an attacker-controlled website and is redirected to `https://bitbucket.test/login?next=/plugins/servlet/external-login`.
- Bitbucket serves a regular Login Form, the victim authenticates using her credentials for user A .
- After successful authentication, Bitbucket redirects the victim to the Login Initialization Endpoint, as this was the previously provided destination 
- Bitbucket receives the GET request to the Login Initiation Endpoint and launches a new OpenID Connect Login flow accordingly.
- The victim has, per our prerequisites, an active session at the Identity Provider. As a result, there is a silent redirect with the Authentication Response to the redirect_uri endpoint including valid code and state parameters.
- Bitbucket validates the state and redeems the code at the Identity Provider’s Token Endpoint. The Identity Provider responds with an id_token and access_token.
- After validating the identity of user B, the victim is logged in as user B, although she entered her credentials for user A and did not perform any additional interactions.
- [Video](https://security.lauritz-holtmann.de/videos/advisories/ma20200016.mp4)
2. SSRF
- A straight forward PoC to trigger the SSRF issue is given with the following URL (Authentication Response)
- e.g 
` 
https://keycloak.local/auth/realms/master/protocol/openid-connect/auth?scope=openid&response_type=code&redirect_uri=%5BValid-RedirectURI%5D&state=aaaa&nonce=bbbb&client_id=%5BValid-ClientID%5D&request_uri=http://127.0.0.1:1234`
- Thus, to launch the SSRF in a real-life scenario, an attacker would obtain an Authentication Request (to get the valid client_id and redirect_uri).
- Keycloak sends a GET request to 127.0.0.1:1234 to fetch the Request Object resulting in blind SSRF.
- a malicious actor may additionally perform a port scan of localhost or internally accessible hosts.
3. Redirect URI
- Register a new client and configure the following redirect_uri: data:text/html,%3Cscript%3Ealert%281%29%3C%2Fscript
- Visit the Authentication Endpoint of the created Client
`https://keycloak.local:8443/auth/realms/master/protocol/openid-connect/auth?scope=openid&state=a&response_type=code&client_id=test&redirect_uri=data%3Atext%2Fhtml%2C%253Cscript%253Ealert%25281%2529%253C%252Fscript%253E&nonce=b`
- After successful authentication there is a redirect to the registered redirect_uri:
``` js
HTTP/1.1 302 Found
Location: data:text/html,%3Cscript%3Ealert%281%29%3C%2Fscript%3E?state=a&session_state=b&code=c
[...]
```
***
## **Resources**
- [Real-life OIDC Security (II): Login Confusion](https://security.lauritz-holtmann.de/post/sso-security-login-confusion/).
- [Real-life OIDC Security (III): CRLF Injections](https://security.lauritz-holtmann.de/post/sso-security-crlf-injection/).
- [Real-life OIDC Security (IV): Server-Side-Request-Forgery](https://security.lauritz-holtmann.de/post/sso-security-ssrf/).
- [Real-life OIDC Security (V): Redirect URI](https://security.lauritz-holtmann.de/post/sso-security-redirect-uri/).
- [Real-life OIDC Security (VI): Reusable state leads to DoS Amplification](https://security.lauritz-holtmann.de/post/sso-security-state/).
***
## **The End**