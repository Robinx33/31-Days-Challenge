`23 December 2022`
## **Cross-Site Leaks (XS-Leaks)**:
- Cross-site leak (XS-Leak) refers to a family of browser side-channel techniques that can be used to infer and gather information about users, often based upon network timing of the responses.
- Cross-Site Leaks/XS-Leaks is a less explored security issue that usually comes from Side-Channel Attacks.
- This basically utilizes the web's core principle of composability in order to determine & extract useful information.
- XS-Leaks take advantage of small pieces of information which are exposed during interactions between websites.
## **Cheat Sheet**:
- [XS Leaks Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XS_Leaks_Cheat_Sheet.html).
## **Cross-Site Oracle**:
-  This can be considered as a querying mechanism. The information used for this attack is of binary form and called Oracles. They usually have an answer of "Yes" or "No". You can say True or False. 
-  For Example: Does User Harsh Exists in the Application. Yes, means that the user is there in the application. 
- An attacker requires to smartly form queries in order to successfully execute this attack and gain hold of sensitive information.
## **Example**:
1. Suppose that bank.com has an API endpoint that returns data about a user’s receipt for a given type of transaction.
2. evil.com can attempt to load the URL bank.com/my_receipt?q=groceries as a script. By default, the browser attaches cookies when loading resources, so the request to bank.com will carry the user’s credentials.
3. If the user has recently bought groceries, the script loads successfully with an HTTP 200 status code. If the user hasn’t bought groceries, the request fails to load with an HTTP 404 status code, which triggers an Error Event.
4. By listening to the error event and repeating this approach with different queries, the attacker can infer a significant amount of information about the user’s transaction history.
***
## **Attacks using XS-Leaks**:
1. XS-Search: An attacker try to abuse the query mechanism such as search functionality to leak and get hold of user's inforamtion.
2. Error Events: Based on the Error Message returned by the application, it may be possible to enumerate sensitive information. This is similar to user enumeration techniques.
3. Frame Counting: window.length which provides the number of frames in the window. This attribute can provide valuable information about a page to an attacker.
4. Navigation Attacks: To detect if any kind of navigation occurred in order to know specific information about the victim.
5. Cache Probing: Workes based on detecting whether the web page was cached or not.
6. Performance API: The Performance API is used to access the performance information of the current page. Their entries include detailed network timing data for the document and every resource loaded by the page.
7. Abusing Browser Features Abusing Browser Features 
    - CORB (Cross-Origin Read Blocking)
    - CORP (Cross-Origin Resource Policy)
8. Timing Attacks
    - Clock Based 
    - Network Timing
    - Execution Timing
    - Hybrid Timing 
    - Connection Pool
## **Attacker's Goal**:
- In a Cross-Origin State Inference (COSI) attack, the attacker’s goal is to determine the state of a victim visiting an attack page (e.g., attack.com/index.html), in a target web site
not controlled by the attacker (e.g., linkedin.com). The state of the victim in a target web site is defined, among others, by login status, account, and content properties. Determining
the victim’s state can have important security implications.
For example, determining that a victim is logged into a
target web site implies that the victim owns an account in
that site. This is problematic for privacy-sensitive web sites
such as those related to post-marital affairs and pornography.
## **References**:
- https://xsleaks.com/
- https://arxiv.org/pdf/1908.02204.pdf
- https://github.com/xsleaks/xsleaks/wiki/Browser-Side-Channels
- http://sirdarckcat.blogspot.com/2019/03/http-cache-cross-site-leaks.html
- https://polict.net/blog/web-tracking-via-http-cache-xs-leaks/
- https://xsleaks.dev/category/attack/
- https://owasp.org/www-community/attacks/Cross_Site_History_Manipulation_(XSHM)
- https://portswigger.net/research/xs-leak-leaking-ids-using-focus
- https://medium.com/@terjanq/massive-xs-search-over-multiple-google-products-416e50dd2ec6
- https://owasp.org/www-pdf-archive/AppSecIL2015_Cross-Site-Search-Attacks_HemiLeibowitz.pdf
- https://www.imperva.com/blog/facebook-privacy-bug/
## **Reports**:
- [De-anonymization Attack: Cross Site Information Leakage](https://hackerone.com/reports/723175) ($250).
- [Twitter ID exposure via error-based side-channel attack](https://hackerone.com/reports/505424) ($1,470).
- [Protected tweets exposure through the URL](https://hackerone.com/reports/491473) ($560).
***
## **The End**