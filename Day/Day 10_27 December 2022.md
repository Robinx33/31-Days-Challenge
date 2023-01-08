`27 December 2022`

## **Day 10 What I have Learned**

* * *

## **HTTP hop-by-hop request headers**:

- A hop-by-hop header is a header which is designed to be processed and consumed by the proxy currently handling the request.
- the HTTP/1.1 spec treats the following headers as hop-by-hop by default: `Keep-Alive`, `Transfer-Encoding`, `TE`, `Connection`, `Trailer`, `Upgrade`, `Proxy-Authorization` and `Proxy-Authenticate`.
- Hop-by-hop headers are meaningful only for a single transport-level connection, and are not stored by caches or forwarded by proxies.
    Only H-b-H headers may be set using the Connection header

## **Cache poisoning DoS**:

- One of a kind of Web Cache Poisoning attack that affects the resources used by an application to create a denial of service situation.
- Cache-Poisoned Denial-of-Service (CPDoS) is a new class of web cache poisoning attacks aimed at disabling web resources and websites
- More Information [Here](https://cpdos.org).

* * *

## **Hop-By-Hop Section**:
## **Attacks by Abusing Hop-by-Hop Header**:
1. Fingerprinting Services.
2. Accessing Authenticated Endpoint or Protected Information.
3. Masking the Source IP. 
4. Cache Poisoned Denial of Service (CPDoS).
5. SSRF.
6. WAF Bypass.
## **Resources**:

1.  [Abusing Http hop by hop](https://nathandavison.com/blog/abusing-http-hop-by-hop-request-headers).

## **Tips**:

- `<attacker spoofed ip>, <real attacker ip>`, so the app can safely handle spoof attempts and this request would grant access to /admin
- Another thing to keep in mind is XFF is only one header used for passing on the real IP address of a user - depending on the system being targeted, you may also have Forwarded, X-Real-IP, and a bunch of others that are less common.
***
## **Cache poisoning DoS Section**:
## **Resources**:
1. [CPDoS: Cache Poisoned Denial of Service](https://cpdos.org/).
## **Types of CPDoS Attacks**:
1. HTTP Header Oversize.
- HHO CPDoS attacks work in scenarios where a web application uses a cache that accepts a larger header size limit than the origin server
2. HTTP Meta Character.
- Meta characters can be ,e.g., control characters such as line break/carriage return (\n), line feed (\r) or bell (\a)
3. HTTP Method Override.
- The X-HTTP-Method-Override HTTP header works somewhat similar to a hack. You can add the header with a value of either PUT or DELETE.
***
## **The End**
