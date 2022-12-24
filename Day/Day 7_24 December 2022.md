`24 December 2022`
## **Cross-Site Script Inclusion**:
- Cross Site Script Inclusion (XSSI) vulnerability allows sensitive data leakage across-origin or cross-domain boundaries. Sensitive data could include authentication-related data (login states, cookies, auth tokens, session IDs, etc.) or user’s personal or sensitive personal data (email addresses, phone numbers, credit card details, social security numbers, etc.)
- [More](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/11-Client-side_Testing/13-Testing_for_Cross_Site_Script_Inclusion).
## **Types Of XSSI**:
1. Regular XSSI - Static Javascript
- This is similar to looking for the hardcoded data in a javascript file.
- Since the javascript file is static, an attacker can try to embed it a page in order to extract information. 
2. Authenticated Access to Static Javascript.
3. Dynamic Javascript.
4. Non-Script Attack.
***
## **Tool**:
1. Detect Dynamic JavaScript Files(burp extension) 
[Here](https://github.com/luh2/DetectDynamicJS).
- Use Detect DynamicJS Burp Plugin
- This works on the same principle. Passively scanning all JS files and than scanning those files without authentication identifier like cookies. 
- If issue is found, it will be seen under Target Tab as Informational severity finding.
## **Conference Talk**:
1. [Your Scripts In My Page - What Could Possibly Go Wrong?](https://www.youtube.com/watch?v=Mnkgg3q51Ps).
## **Labs**:
1. [ Web Application Exploits and Defenses (Part 3)](https://google-gruyere.appspot.com/start).
 - [Walkthrough](https://www.youtube.com/watch?v=z7i8lM2khHE).
 ## **Write-Ups**:
 - [Effortlessly finding Cross Site Script Inclusion (XSSI)](https://medium.com/bugbountywriteup/effortlessly-finding-cross-site-script-inclusion-xssi-jsonp-for-bug-bounty-38ae0b9e5c8a).
 - [Two XSSi vulnerabilities chained to steal user information](https://medium.com/@0xHyde/yahoo-two-xssi-vulnerabilities-chained-to-steal-user-information-750-bounty-e9bc6a41a40a).
 - [The Bug That Exposed Your PayPal Password](https://medium.com/@alex.birsan/the-bug-that-exposed-your-paypal-password-539fc2896da9).
 ## **Reports**:
 - [XSSI (Cross Site Script Inclusion)](https://hackerone.com/reports/118631).
 - [XSSI: Quick Navigation Interface - leak of private page/post titles](https://hackerone.com/reports/495525).
 ***
 ## **The End**