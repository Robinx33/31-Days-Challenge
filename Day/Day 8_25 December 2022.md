`25 December 2022`

## **Day 7 What I have Learned**:

* * *

## **Json Padding (JSONP)**:

- JSONP stands for JavaScript Object Notation with Padding which allows sending JSON data across domains without worrying about Cross-Domain Issues.
- Is a Historical JavaScript technique for requesting data by loading a &lt;script&gt; , which is an element intended to load ordinary JavaScript.
- JSONP is an insecure communication technique and it should only be used when no personal or sensitive data is involved and sanitizing the callback function.
- There are multiple attacks affecting the JSONP implementation as it doesn't have a pre-implemented security feature.

## **Requirements to Perform JSONP Attack**:

1.  Determine whether the given API endpoint is a cookie-based endpoint.
2.  Second check is made to ensure that the request does not contain any CSRF tokens or Authorization tokens.
3.  Third, assign callback equal to a some function and check if it returns json wrap data. Then we can develop Js programmes and steal data across multiple sites with ease.

## **Security Risk with JSONP**:

- It is possible to access data cross-domains which makes it possible to steal sensitive information of an authenticated user which other domains should not have access to. JSONP attack makes it possible to retrieve the data in a CSRF-style attack.
- Usually the JSONP endpoint will be visible by looking at the various GET/POST calls. Alternatively you can search your HTTP History to search for endpoints like ?callback=somedata, etc.
- JSONP might be supported at the API level and might not be visible directly or acts as a hidden parameter. You can try following:
> Adding a callback parameter to a JSON URL, by appending ?callback=something to the URL    
 > When a format type is provided, change it to JSONP. Change ?format=json to ?format=jsonp.
 ***
## **Tools**:
- Find Hidden Jsonp endpoints
[Here](https://github.com/kapytein/jsonp).
- [JSONBee](https://github.com/zigoo0/JSONBee).
 ## **Resources**:
1.  [JSONP Attacks](https://payatu.com/blog/arjuns/Jsonp-attack).
2.  [Practical Jsonp Injection](https://securitycafe.ro/2017/01/18/practical-jsonp-injection/).
3.  [Exploiting Jsonp](https://infosecwriteups.com/exploiting-jsonp-and-bypassing-referer-check-2d6e40dfa24).
4.  Sample JSONP Page to Practice the Retrieval of data using Script through Other Domain
[Here](https://demo.sjoerdlangkemper.nl/jsonp.php).

## **Reports**:
1. [Bypassing Same Origin Policy With JSONP APIs and Flash](https://hackerone.com/reports/10373) ($3000).
2. [XSS through `__e2e_action_id` delivered by JSONP](https://hackerone.com/reports/259100) ($600).