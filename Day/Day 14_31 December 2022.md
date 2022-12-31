`31 December 2022`
## **Day 14 What I Have Learned**
***
## **Web Cache Deception Attack**:
- This is a type of attack that affects web frameworks and caching mechanisms. Simply understand this as an attack, where an attacker can expose the private information of a user or even leverage the attack to Account takeover.
- This attack mainly happens when the Cache-Control directives are misconfigured and can be leveraged by an attacker to get hold of sensitive information.
## **Files that are Commonly cached**:
1. Style sheets (css)
2. Scripts (js)
3. Text Files (txt)
4. Images (bmp,gif,png etc.)
## **Path confusion attacks**:
- Many Web Applications have URL Rewriting Rules.
- In such scenarios depending upon the configuration of the webserver, both of these URLs will be considered as (http://harshbothra.tech/myprofile).
- http://harshbothra.tech/myprofile
- http://harshbothra.tech/myprofile/test.css
***
## **Resources**:
- [Behind The Scenes Web Cache Deception Attack](https://infosecwriteups.com/behind-the-scene-web-cache-deception-attack-c10bd301cf15).
- [Path confusion: Web cache deception threatens user information online](https://portswigger.net/daily-swig/path-confusion-web-cache-deception-threatens-user-information-online).
- [Web Cache Deception](https://beaglesecurity.com/blog/article/web-cache-deception.html).

## **How to Test**:
1. Navigate to an application and look for a page that may contain sensitive information such as http://harshbothra.tech/myprofile
2. Now add any static file after /myprofile such as test.css, test.jpg, etc. For Ex: http://harshbothra.tech/myprofile/test.jpg
3. Now, if the app displays the same /myprofile page, it might be cached. 
4. Now, From another session (where this user is not logged in), navigate to the same URL: http://harshbothra.tech/myprofile/test.jpg
5. If you can see the information about the victim user. The attack is successful.
***
## **The End**
