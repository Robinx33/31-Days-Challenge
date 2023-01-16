`16 January 2023`

## **Day 30 What I Have Learned**
***
## **CORS Misconfiguration**
-  A cross-origin resource-sharing misconfiguration occurs when the web server allows third-party domains to perform privileged tasks through the browsers of legitimate users.
- For example, consider an application that receives the following request:
``` js
GET /sensitive-victim-data HTTP/1.1
Host: vulnerable-website.com
Origin: https://malicious-website.com
Cookie: sessionid=...
```
- It then responds with:
``` js
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://malicious-website.com
Access-Control-Allow-Credentials: true
...
```
- These headers state that access is allowed from the requesting domain `malicious-website.com` and that the cross-origin requests can include cookies `Access-Control-Allow-Credentials: true` and so will be processed in-session.
- An attacker might be able to gain access using the domain:
`normal-website.com.evil-user.net`
***
## **Exploitation**
1. Arbitrary Origin Reflected & Credentials set to True.
- An attacker supplied "Origin" header is reflected in the Response Headers.
-  Access-Control-Allow-Credentials is set to "true".
-  This is the exploitable case and easily be exploited. 
2. Misconfigured Whitelisting
- Assume that the "origin" header defined by the target allows any domain ending with `goodweb.net`
- As a result of poorly implemented whitelist, an attacker can try providing following domain in the "origin" header like `attacker-goodweb.net` and if it reflects successfully, there's an issue with the implemented whitelist.
3. Null Origin 
- If "Null" is accepted in the "Origin" header and is reflected back, this can be abused by an attacker. 
- Example:
***
## **Resources**
- [CORS Misconfigurations For Bitcoin and Bounties](https://portswigger.net/research/exploiting-cors-misconfigurations-for-bitcoins-and-bounties).
- [CORS Exploitation](https://infosecwriteups.com/think-outside-the-scope-advanced-cors-exploitation-techniques-dad019c68397).
## **Reports**
- [Cross-origin resource sharing misconfig](https://hackerone.com/reports/235200) ($1,000).
- [CORS Misconfiguration](https://hackerone.com/reports/426165) ($550).
- [CORS misconfig | Account Takeover](https://hackerone.com/reports/426147).
- [CORS misconfiguration which leads to the disclosure of certain data](https://hackerone.com/reports/769058) ($100).
- [(CORS) Cross-origin resource sharing misconfiguration](https://hackerone.com/reports/896093).
- [Cross-origin resource sharing misconfiguration](https://hackerone.com/reports/470298).
- [CORS Misconfiguration Leads to Exposing User Data](https://hackerone.com/reports/733017).
## **Labs**
- [PortSwigger CORS Labs](https://portswigger.net/web-security/cors).
## **Tools**
- [CORS Scanner](https://github.com/chenjj/CORScanner).
- [Corsy](https://github.com/s0md3v/Corsy).
***
## **The End**
