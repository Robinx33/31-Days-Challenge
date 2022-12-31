`30 December 2022`

## **Day 13 What I Have Learned**

* * *
## **Websockets Part 2**
***
## **IDOR**:

1.  Intercept WebSocket Communication.
2.  Look for any pattern/trace of ID/UUID/user/role and another similar parameter that may uniquely define an object/entity.
3.  Assume the WebSocket communication is of a chatting application and consists of a request, where the Attacker is sending a message to the victim. There is a parameter called "sid" which is the attacker's user id.
4.  Now, change this "sid" to some victim B's "sid" and if Victim A receives a message from Victim B. That's an issue.

- Look for all IDORs cases that you look for in normal HTTP workflow

## **Denial of Service**:

- WS allows any number of connections to the target server.
- This behavior can be abused by an attacker to exhaust resources and perform a Denial of Service Attack.
- Try sending multiple requests to initiate a WS connection in a short time, this may trigger some lagging in the app processing which can be lead to App Level DoS.

## **Insecure WS Connection**:

- If the WS is using WS:// instead of WSS://, this is like using HTTP:// instead of HTTPS://.
- The WSS:// sends the traffic over SSL/TLS & prevents MiTM attacks.
- If any sensitive action is happening through WebSocket over WS://, try traffic intercepts, and create a proof of concept to show the impact.
- If the WebSocket is using WSS://, try degrading it to WS:// and see if the WS:// is supported.

## **Cross-Site Scripting**:

- Check if the WebSocket is sending data that is displayed back on the application interface or somewhere in another panel (if you have access to it).
- Also, if the data is reflecting somewhere else say admin panel, always try to perform Blind XSS.
- Send XSS payloads in interesting parameters & if the app fails to perform Input Validation in WS, it can allow an attacker to trigger XSS.

## **Sensitive Information in WS**:

- Read the Message sent through WS & keep an eye for any sensitive information that can be utilized.
- Just like reading response or JavaScript files in the usual web workflow.

## **Server-Side Injections**:

- Check all the WebSocket Parameters for potential Server Side Injection like SQLi.
- Fuzz the Parameters based on how various payloads and inputs are handled.

## **Other Server-Side issues**:

- It is always a good idea to test the interesting parameters for all potential security vulnerabilities that are usually tested in normal HTTP Workflow.

* * *

## **Resources**:

- [Cross-Site WebSocket Hijacking](https://christian-schneider.net/CrossSiteWebSocketHijacking.html).
- [Testing WebSockets](https://wiki.owasp.org/index.php/Testing\_WebSockets\_(OTG-CLIENT-010)).

## **Tool**:

- [Cross-Site WebSocket Hijacking Tester](https://cm2.pw/websocket).

## **Labs**:

- [Portswigger Lab (WebSocket)](https://portswigger.net/web-security/websockets).

## **Reports**:

- [The websocket traffic is not secure enough](https://hackerone.com/reports/178990).
- [XSS in steam react chat client](https://hackerone.com/reports/409850) ($7500).
- [`socket` command allows sending data over WebSockets to arbitrary origins from Grammarly Extension](https://hackerone.com/reports/395729) ($1,500).
- [User Information sent to client through websockets](https://hackerone.com/reports/163464) ($120).
- [DOM XSS triggered in secure support desk](https://hackerone.com/reports/512065) ($500).
- [Staff with no permissions can listen to Shopify Ping conversations by registering to its different WebSocket Events](https://hackerone.com/reports/1023669) ($800).
***
## **The End**
