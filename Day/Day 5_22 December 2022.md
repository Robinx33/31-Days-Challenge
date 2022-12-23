`22 December 2022`
## **Day 5: What I have Learned**:
***
## **Client-Side Template Injection (CSTI)**:
- This occurs at the client-side like other JS attacks such as XSS.
- This is mainly seen in the various JS libraries like AngularJS, VueJS etc which utilize the template engines at the client-side.
- The presence of "ng-app" in the page source identifies the use of templates. 
- If the application directly accepts the input and process it without any validation, it may be vulnerable to CSTI. 
- CSTI leads to perform cross-site scripting attacks by escaping.
- Testing this issue is similar to Server-Side Template Injection. 
## **Methods**:
- In the suspected field, provide a payload like {{11*5}}.
- If the response reflected is 55, this tells that there is the use of the template and further you can try performing CSTI to XSS.
## **Writeup**:
- [November XSS Challenge Writeup Video (CSTI)](https://www.youtube.com/watch?v=-_7uL7l0qZk).
***
## **Server-Side Template Injection**:
- Server-side template injection is when an attacker is able to use native template syntax to inject a malicious payload into a template, which is then executed server-side.
- [Server-Side Template Injections Explained](https://www.youtube.com/watch?v=SN6EVIG4c-0).
- [Server-Side Template Injection Explained PortSwigger](https://portswigger.net/web-security/server-side-template-injection).
- [Server-Side Template Injection Payloads ](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection).
## **Labs**:
- [Portswigger Labs](https://portswigger.net/web-security/server-side-template-injection/exploiting).
