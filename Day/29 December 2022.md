`29 December 2022`
## **Day 12 What I Have Learned**
***
## **WebSocket Vulns**:
- WebSocket is a network protocol that enables 2-way communication b/w client & server.
- In the HTTP standard, where the one-party has to wait for the req./res from another party before performing the next action.
- Websockets use wss:// and ws:// as the protocol scheme.
- This is similar to HTTPS and HTTP. Here, the WSS:// is a secure channel where WS:// is an insecure channel.
- [Beginners Guide To Websockets](https://www.youtube.com/watch?v=8ARodQ4Wlf4).
## **WebSocket Connection Process**:
1. The application will send an HTTP request with two additional Headers: Upgrade: WebSocket & Connection: Upgrade to the server. 
2. This request basically initiates the Web Socket connection process.
3. In return the server will return 101 Switching Protocols status code.
4. After this, WebSocket communication will start to take place. 
## **Extra**:
- Burp Suite allows an option to capture the WebSocket Traffic, modify it, and replay it.
- You can use the Simple Web Socket browser extension to check for some test cases and communicating with the Web Socket. 
***
## **Security Implications**:
1. Denial of Service 
- WebSockets let an unlimited number of connections reach the server. This lets an attacker flood the server with a DOS attack.
2. Insecure Communication
- Another issue with WebSockets is that they can be used over an unencrypted TCP channel. This leads to all kinds of issues that are listed in the OWASP Top 10 A6-Sensitive Data Exposure.
3. Missing Access Controls & Authorization Checks
- Without proper authorization checks, the program may allow an unauthorized user to start a restricted transaction.
4. Missing Input Validation in User-Controlled Data 
-  This data needs validation as well as any other that comes from a client before it gets processed. Why? Because injection attacks like OS, SQL, Blind SQL are possible via WebSockets.
5. Lack of/Improper Authentication 
- A big flaw of WebSocket protocols is that they don’t handle authorization/authentication. Any application-level protocols need to handle this separately. Especially in cases when sensitive data gets transferred.
6. Tunneling 
- WebSockets let anyone tunnel an arbitrary TCP service.
- An example is tunneling a database connection directly through and reaching the browser.
7. Cross-Site Web Socket Hijacking 
- The problem here is that the WebSocket protocol doesn’t let a server authenticate the client during the handshake process.
- Perform unauthorized actions masquerading as the victim user And Retrieve sensitive data that the user can access.

## **References**:
1. [WebSocket Top Vulnerabilities](https://www.neuralegion.com/blog/websocket-security-top-vulnerabilities/).