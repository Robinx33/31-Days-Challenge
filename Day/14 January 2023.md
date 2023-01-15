`14 January 2023`
## **Day 28 What I Have Learned**
***
## **Cookie Based Authentication**
- Cookie based session identification is a way to allow application to provide authentication mechanism for it's users.
- However, these days Token based authentication is being widely used over Cookie Based Authentication due to a large attack surface that Cookie Based Authentication leaves open. 
- Everyone working in the domain of penetration testing or application security is familiar to cookies and how they are being used.
***
## **Cookie Based Authentication Vulnerabilities**
1. Cross-Site Scripting
- Assume that value of the Cookie Parameter "Name" is reflected in the application.
- Change the "Name" value to "XSS Payload" and it may result into a XSS.
2. Insufficient Session Management
- Session Doesn't Expire on Logout
- Long Session Expiry
- Session Doesn't Expire on Password Reset/Change
- Concurrent Session/Parallel Login.
3. Session Fixation
- An attacker tricks the victim user to use a Session Identifier which is known to the attacker. 
- Example
  1. Attacker Log In on The Vulnerable Website Which is `example.com`
  2. Gets a Session Id `sessionid=xyz`
  3. Sends A Crafted link to the Victim `example.com/login?sessionid=xyz`
  4. The Victim Log In his/her Credentials Using Your Crafted Link With Your cookie.
  5. Then The Attacker uses The session id to login into the victim acoount `sessionid=xyz`
4. Privilege Escalation
- Horizontal Privilege
  1. Assume that the application uses Multi-Organization Model.
  2. Cookies are used to define which organization a user can access.
  3. Alter the Cookies in order to Access some other Organization.
 - Vertical Privilege Escalation
   1. Assume that the cookies are used to determine the "Role" of the User.
   2. Alter the Cookies in order to Elevate the "Role" of the User.
5. Insecure Direct Object Reference
- If the cookies are using some access defining parameter such as "user_id"
- Change the value of these parameter in order to check if you can access other user's data.
6. Missing Cookie Security Attributes
- Missing HTTPOnly Flag,Secure Flag and Same-Site Flag
7. Guessable/Weak Cookie
- Check if the cookies are not generated Randomly by issues multiple cookies and analyzing them.
- Check if some weak/known cryptography is used. Let's assume the cookies are using Base64 Encoding and can be decoded/forged easily.
- e.g Forge The Cookie Then Place `Role: User` to `Role: Admin`
8. File Inclusion
 - If a cookie is used to define some server-side attribute that can be controlled by a user, try for File Inclusion Attacks.
9. Session Puzzling
- When an application utilizes the same session variable for multiple purposes, this can be abused by an attacker to trick the application and perform the action as an authenticated or privileged user.
10. Padding Oracle Attack
11. ECB Encryption
- Create 2 users with almost the same data (username, password, email, etc.) and try to discover some pattern inside the given cookie.
- There should be a pattern (with the size of a used block). So, knowing how are a bunch of "a" encrypted you can create a username: "a"*(size of the block)+"admin". Then, you could delete the encrypted pattern of a block of "a" from the cookie. And you will have the cookie of the username "admin".
- There should be a pattern (with the size of a used block). So, knowing how are a bunch of "a" encrypted you can create a username: "a"*(size of the block)+"admin". Then, you could delete the encrypted pattern of a block of "a" from the cookie. And you will have the cookie of the username "admin".
12. Authentication Bypass
- Try accessing a protected resource by removing cookies.
- If the resource is accessible via GET Request, try for Direct Request (Forceful Browsing) with unauthenticated user.
13. SQL Injection
- The cookie contains base64 encoded form identifier, a field that is unknown and a password. If we use as a cookie 12345 ‘UNION SELECT’ mypass ‘:: mypass base64 encoded, the SQL query becomes:
``` js
SELECT user_password FROM nk_users WHERE user_id=’12345′ UNION SELECT ‘mypass’
```
- This query returns the password mypass, the same password as we have to provide. So we are connected.
14. Denial of Service - Cookie Bomb
- Forcing the server to process cookies larger than the restricted cookie size defined by the server may cause Denial of Service Attack.
-  Cookie Bomb is the capability of adding a large number of large cookies to a user for a domain and its subdomains with the goal that the victim will always send large HTTP requests to the server (due to the cookies) the server won't accept the request. Therefore, this will cause a DoS over a user in that domain and subdomains.

15. Parameter Pollution
- Assume that the cookies utilize a parameter called `user_id=` to retrieve some data.
- However, the application is not vulnerable to IDOR and changing `user_id=` to victim value, doesn't help out.
- Attacker, add an additional `user_id=` parameter value to the cookie with victim's user ID. Like: `user_id=attacker&user_id=victim` 
- Three things can happen here:
   1. The application may retrieve data of Victim User. 
    2. The Application may retrieve data of both Attacker & Victim User.
    3. The Application is not vulnerable and doesn't return anything.
16. Mass Assignment
- Similar to the Parameter Pollution, However, in this, Attacker tried to Inject multiple User ID in same user_id parameter.
17. Arbitrary Cookie Injection
- Try Injecting some Arbitrary Cookies using Attacks such as CRLF Injection.
- Sometimes it can be used to escalate privilege or if the application malfunction, it can reveal sensitive information through Stack Traces.
18. Insecure Deserialization
- It cookies are using Serialized Objects, try performing Insecure Deserialization Checks.
19. Cookie Length Violation
- It may cause attacks such as Buffer Overflows
20. Session Donation
- The attacker sends his own session to the victim. The victim will see that he is already logged in and will suppose that he is inside his account but the actions will be performed inside the attacker's account.
21. Sensitive Data Stored in Cookies
- Check if any PII or Other Sensitive Information Stored in Cookies
- This information usually includes: Email, Date of Birth, Mobile, Address, SSN, Etc.

A Map Of types of Cookie Based Vulnerability
[here](http://www.xmind.net/m/2FwJ7D)
***
## **Resources**
- [Session Vs Token Authentication](http://www.youtube.com/watch?v=UBUNrFtufWo).
- [Session Fixation Attack](https://secureteam.co.uk/articles/web-application-security-articles/understanding-session-fixation-attacks/).
- [OWASP Session Fixation](https://owasp.org/www-community/attacks/Session_fixation).
- [Cookie Based Php File Inclusion](https://medium.com/@tehmezovismayil/cookie-based-php-local-file-inclusion-bug-bounty-553f8b38d4dc).
- [Session Puzzling Bothra Day 17](https://github.com/harsh-bothra/learn365/blob/main/days/day17.md).
- [Hacking With Cookies](https://book.hacktricks.xyz/pentesting-web/hacking-with-cookies).
- [Cookie Based SQL Injection](https://resources.infosecinstitute.com/topic/cookie-based-sql-injection/).
- [Deserialization](https://portswigger.net/web-security/deserialization/exploiting).
- [Cookie Value Length Violation](https://docs.imperva.com/bundle/on-premises-knowledgebase-reference-guide/page/cookie_value_length_violation.htm).
- [Got Cookies?](http://www.youtube.com/watch?v=CE4w8uUi0Mw).

## **Reports**
- [DOM based cookie bomb](https://hackerone.com/reports/57356) ($280).

***