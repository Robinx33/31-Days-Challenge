`28 December 2022`

## **Day 11 What i Have Learned**

* * *

## **Web Cache Poisoning**:

- Web cache poisoning is an advanced technique whereby an attacker exploits the behavior of a web server and cache so that a harmful HTTP response is served to other users.
- Poisoned web cache can potentially be a devastating means of distributing numerous different attacks, exploiting vulnerabilities such as XSS, JavaScript injection, open redirection, and so on.
***
## **Caches Types**:

1.  Basic Poisoning

- Adding or editing X-Forwarded-Host to something,If it shows in the metadata you can use XSS to trigger it.
- Cache poisoning is often very easy to exploit.

2.  Discreet Poisoning:

- In order to actually poison the blog's homepage and deliver our exploit to all subsequent visitors.
- This could be attempted using a tool like Burp Intruder or a custom script to send a large number of requests
- e.g GET / HTTP/1.1
    Host: unity3d.com
    X-Host: portswigger-labs.net
    <script src="https://portswigger-labs.net/sites/files/foo.js">&lt;/script&gt;
- Taken together, these tell us the precise second we should send our payload to ensure our response gets cached.
3.  Selective Poisoning:
- Its Like The Second Cache Type.You need To deliver The Exploit,But Wont work On all Users.
    e.g GET / HTTP/1.1
    Host: redacted.com
    User-Agent: Mozilla/5.0 … Firefox/60.0
    X-Forwarded-Host: a">&lt;iframe onload=alert(1)&gt;
- However, the Vary header tells us that our User-Agent may be part of the cache key, and manual testing confirms this. This means that because we've claimed to be using Firefox 60, our exploit will only be served to other Firefox 60 users. We could use a list of popular user agents to ensure most visitors receive our exploit, but this behaviour has given us the option of more selective attacks
 4. DOM Poisoning   
 - Create a match and replace rule in Burp to add an 'X-Forwarded-Host: id.burpcollaborator.net' header to all requests, then browsed the site. When certain pages loaded, Firefox sent a JavaScript-generated request to Your server.
5. [Pratical Web Cache Poisoning](https://portswigger.net/research/practical-web-cache-poisoning).
- More Types Of Caches and Information On This Website.

## **Extra**:

1.  Cache Keys

- The concept of caching might sound clean and simple, but it hides some risky assumptions. Whenever a cache receives a request for a resource, it needs to decide whether it has a copy of this exact resource already saved and can reply with that, or if it needs to forward the request to the application server.
- e.g GET /blog/post.php?mobile=1 HTTP/1.1
    Host: example.com
    User-Agent: Mozilla/5.0 … Firefox/57.0
    Cookie: language=`en`;
    Connection: close
- As a result, the page will be served in the wrong language to the second visitor.
***
## **Labs**:

- [Web Cache Poisoning](https://portswigger.net/web-security/web-cache-poisoning).
- [Web Cache Entanglement](https://portswigger.net/research/web-cache-entanglement).

## **Reports**:

1.  [Denial of service via cache poisoning](https://hackerone.com/reports/409370) ($2500).
2.  [Cache poisoning DoS to various TTS assets](https://hackerone.com/reports/728664) ($750).
3.  [Denial-of- service By Cache Poisoning The Cross-Origin Resource](https://hackerone.com/reports/921704) ($200).
4.  [DoS through cache poisoning using invalid HTTP parameters](https://hackerone.com/reports/326639) ($500).
5.  [Denial of service to WP-JSON API by cache poisoning the CORS allow origin header](https://hackerone.com/reports/591302) ($550).
																					   
***
## **The End**
