`12 January 2023`
## **Day 26 What I Have Learned**
***
## **CRLF Injection**
- CRLF (Carriage Return Line Feed) is a sequence that is used to terminate a line in HTTP Protocol. CR (\r) LF (\n) is used for this purpose.
- CRLF Injection is a software application coding vulnerability that occurs when an attacker injects a CRLF character sequence where it is not expected.
- \r\n signifies End of the Line in HTTP Protocol.
- In a CRLF injection vulnerability attack the attacker inserts both the carriage return and linefeed characters into user input to trick the server, the web application or the user into thinking that an object is terminated and another one has started. As such the CRLF sequences are not malicious characters, however they can be used for malicious intend.
- There are two main malicious uses for CRLF injections: log poisoning (also called log injection, log splitting, or log forging) and HTTP response splitting.
- e.g
``` js
GET /advanced%0D%0ASet-Cookie:test2=test;domain=.
```
Response
``` js 
HTTP/1.1 302 Found
Date: Mon, 03 Jul 2017 08:55:53 GMT
Server: Apache
Location: http://www.Robin:80/advanced
Content-Length: 267
Content-Type: text/html; charset=iso-8859-1
my_cache-control: no-cache
my_pragma: no-cache
Connection: close
Set-Cookie: test2=test;domain=.

```
***
## **Attack Vector**:
1. Cross-Site Scripting
- Assume the application is vulnerable to CRLF Injection and allows an attacker to inject an arbitrary Request Header which is reflected in response as well. 
Ex: 
``` js
www.blame.me/somepage%0d%0aContent-Length:%200%0d%0a%0d%0aHTTP/1.1%20200%20OK%0d%0aContent-Type:%20text/html%0d%0aContent-Length:%2025%0d%0a%0d%0a%3Cscript%3Ealert(1)%3C/script%3E
```
- This may result into a Cross-Site Scripting
2. Injecting Arbitrary Cookies
- Similar method can be used to inject arbitrary cookies in the applicaiton and cause unexpected behaviours. 
3. HTTP Response Splitting
- Example: https://book.hacktricks.xyz/pentesting-web/crlf-0d-0a#an-example-of-http-response-splitting-leading-to-xss
4. Log Poisoning
- An attacker can input fake log entries and try to mess up the logs by injecting various CRLF sequences.
5. Web Cache Poisoning
- This attack can also be used to add arbitrary headers and cause cache posining. I'll discuss this more during Web Cache Poisoning Series.
***
## **Resources**
- [CRLF Injection OWASP](https://owasp.org/www-community/vulnerabilities/CRLF_Injection).
- [Examples of Http Response splitting](https://book.hacktricks.xyz/pentesting-web/crlf-0d-0a#an-example-of-http-response-splitting-leading-to-xss).
- [Exploiting CRLF Injection](https://medium.com/bugbountywriteup/bugbounty-exploiting-crlf-injection-can-lands-into-a-nice-bounty-159525a9cb62).
- [CRLF injection](https://www.invicti.com/learn/crlf-injection/).
- [Email Injection](https://www.invicti.com/learn/email-injection/).
- [HTTP Response Splitting](https://blog.innerht.ml/overflow-trilogy/).
- [Carriage Return Line Feed (PayloadOfAllThings)](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/CRLF%20Injection).
## **Reports**
- [CRLF injection](https://hackerone.com/reports/446271) ($2,940).
- [HTTP Response Splitting (CRLF injection) in report_story](https://hackerone.com/reports/52042) ($3,500).
- [HTTP Response Splitting (CRLF injection)](https://hackerone.com/reports/53843) ($2,800).
- [[dl.beepcar.ru] CRLF Injection](https://hackerone.com/reports/332708).
- [CRLF Injection in urllib](https://hackerone.com/reports/590020) ($1,000).
- [CRLF Injection](https://hackerone.com/reports/245485).
- [CRLF injection in info.hacker.one](https://hackerone.com/reports/217058).
- [CRLF Injection at vpn.bitstrips.com](https://hackerone.com/reports/237357) ($500).
- [CRLF injection on www.starbucks.com](https://hackerone.com/reports/858650) ($250).
## **Lab**
- [HTTP/2 request splitting via CRLF injection](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-splitting-via-crlf-injection).
***
## **The End**
