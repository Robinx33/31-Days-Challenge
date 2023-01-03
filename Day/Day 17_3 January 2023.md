`3 January 2023`
## **Day 17 I Have Learned**:
***
## **HTTP Parameter Pollution**:
- HTTP Parameter Pollution (HPP) is a Web attack evasion technique that allows an attacker to craft a HTTP request in order to manipulate or retrieve hidden information
- HTTP Parameter Pollution attack tries to pollute or override the parameters in order to perform a malicious action or achieve a desired result.
- The main reason why this attack happens is lack of proper input sanitization and how various application server treats the parameters. 
- HTTP Parameter Pollution tests the applications response to receiving multiple HTTP parameters with the same name; for example, if the parameter username is included in the GET or POST parameters twice.
## **HTTP Parameters**:
1. GET parameters.
- GET /somePage.jsp
2. POST parameters.
- POST /somePage.asp 
3. Using the COOKIE header.
***
## **Can Be Used To**:
- Bypass WAFs rules.
- Access and potentially exploit variables that are not been controlled properly.
- Business Logic Abuse.
- Filter Bypass
- Authentication Bypass
- Server/Client-Side Attacks
## **How to Test**:
1. Suppose a banking application has the following URL to receive an amount: https://t.co/qeNtjtqZol?amp=1.
2. Now an attacker add an additional parameter to pollute the url like following: https://t.co/t3wObY8jDS?amp=1&amp=1.
3. Now if the payment is sent to both the users, it is an issue.
- Try doing the following:
  1. Adding parameters with the same key:value pairs like: to=123&to=12345
  2. Adding parameter with incremental key:value pairs like: u1=harsh&u2=hbothra
***
## **Resources**:
- [Parameter tampering method](https://medium.com/geekculture/http-parameter-pollution-981af7894c6e).
- [HTTP Parameter Pollution](https://www.imperva.com/learn/application-security/http-parameter-pollution/).
- [Testing for HTTP Parameter Pollution](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/04-Testing_for_HTTP_Parameter_Pollution).
- [Client side Http Parameter Pollution - Yahoo! Classic Mail Video Poc](https://blog.mindedsecurity.com/2009/05/client-side-http-parameter-pollution.html).
- [How to Detect HTTP Parameter Pollution Attacks](https://www.acunetix.com/blog/whitepaper-http-parameter-pollution/).
- [Compromising User Account- ”How I was able to compromise user account via HTTP Parameter Pollution(HPP)”](https://logicbomb.medium.com/bugbounty-compromising-user-account-how-i-was-able-to-compromise-user-account-via-http-4288068b901f).
- [HTTP Parameter Pollution - It’s Contaminated](https://shahjerry33.medium.com/http-parameter-pollution-its-contaminated-85edc0805654).
- [HTTP Parameter Pollution - It’s Contaminated Again](https://shahjerry33.medium.com/http-parameter-pollution-its-contaminated-again-95c75b0295e1).
## **Reports**:
- [Parameter pollution in social sharing buttons](https://hackerone.com/reports/105953) ($500).
- [HTTP Parameter Pollution using semicolons in iframe element](https://hackerone.com/reports/298265) ($500).
- [`owncloud.com`: Parameter pollution in social sharing buttons](https://hackerone.com/reports/106024)

***
## **The End**
