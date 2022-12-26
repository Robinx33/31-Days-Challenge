`26 December 2022`
## **Day 9 What I Have Learned**:
***
## **JSON Attacks**:
- JSON is widely used in modern web applications and often most of the API requests are observed using JSON as data type. Some applications use it for communicate data where some applications use it to store data.
- Use of JSON is mostly observed in REST APIs and AJAX applications.
- JSON is however considered to be secure than traditional data exchange formats like text/plain but it also comes with multiple security issues if not implemented properly. 
- Most of the Server Side JSON attack happens when an attacker is able to supply untrusted data and the server without performing sanitization, writes it directly to JSON Stream.
- On the other hand, In case of Client-Side JSON attacks are a result of user supplied data getting parsed using JavaScript eval() function without any sanitization. 

## **BlackHat**:
- [Friday The 13TH - Json Attacks](https://www.youtube.com/watch?v=oUAeWhW5b8c).
***
## **Ways to Attack JSON**:
1. JSON Deserialization Attack
- It is possible to perform and exploit deserialization attack in JSON implementation. The following Research Paper is the goldmine to learn about it: https://www.blackhat.com/docs/us-17/thursday/us-17-Munoz-Friday-The-13th-JSON-Attacks-wp.pdf
- Video Showing How JSON Deserialization Works [Here](https://www.youtube.com/watch?v=SKqWXCips1Y).
2. JSONP (JSON Padding) Attack
- JSONP stands for JavaScript Object Notation with Padding which allows sending JSON data across domains without worrying about Cross-Domain Issues.
3. Brute-Forcing Attacks
- It is possible to perform attacks that fall under brute-force category such as testing for No Rate Limiting, Lockout Policy, etc. in JSON. The steps are similar to traditional web app approaches. 
4. XXE
- By changing the content-type to XML, it might be possible to perform XXE if the application doesn't sanitize and validate user supplied Input.
- Steps: 1. Capture a Request with JSON Body
    2. Change content type to application/xml and insert a XML payload 
    3. Also, you can use Burp's Content Type Convertor plugin.
    4. Observe how application responds and perform attack based on response. 
5. Injection Attacks
- Again, if there is a lack of input validation and application doesn't perform proper checks, it is possible to perform any sort of inject attacks such as SQL Injection, Command Injection, etc. based on how application works. 
- It's always a good idea to check how the application reacts upon supplying different payloads. 
6. File Inclusion/File Read
- If the application utilize a weakly implemented function that let a user read files, it can be abused to perform Local File Read. 
For Ex: Original Request Body

    {"user":"admin", "path"="/admin.html"}
- If the path parameter is not getting validaed, it can be abused to perform local file read like: 

    {"user":"admin", "path"="../../../../../../../../../../../etc/passwd"}
	
## **References**:
- [Deserialization Attack](https://owasp.org/www-pdf-archive/Marshaller_Deserialization_Attacks.pdf.pdf).
- [Attacking JSON](https://www.websecgeeks.com/2015/10/attacking-json-application-pentesting.html).
- [JSON Based XSS](https://medium.com/@koumudi.garikipati/json-based-xss-84089141c136).
***
## **The End**
