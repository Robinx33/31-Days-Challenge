---
title: 18 December 2022
updated: 2022-12-19 05:16:40Z
created: 2022-12-18 06:31:43Z
---

`18 December 2022`

## **Day 1: What I have Learned**

* * *

## **Two Factor Authentication**:

- It is a additional authentication required after you have successfully put your Username/Email address and Password.
- It Protects Your Account From Being accessed by a malicious user e.g *if they have access to your Username/Email Address and Password* It will ask for 2FA(Two Factor Authentication)

## **Authorization Token**:

- A Token a website Gives you That has bunch of Numbers And Letters Generated to help the website to remember you next time you visit the website on your computer so that you wont go through the process again
- If an Attacker get that Token, They Can impersonate You.

## **Types of Two Factor Authentication**:

- SMS(Through Your Mobile Phone)
- Email(Through Your Mail e.g *Gmail*)
- Physical(Through USB Key)
- Many More

* * *

## **2FA Bypass Techniques**

1.  2FA Code Leakage in Response:

- At 2FA Code Triggering request, such as Send OTP functionality, capture the request
- See the response of this request and analyze if the 2FA Code is leaked

2.  JS File Analysis:

- While triggering the 2FA Code Request, Analyze all the JS Files that are referred in the response to see if any JS file contains information that can help bypass 2FA code

3.  Lack of brute-Force Protection:

- Repeat this request for 100–200 times and if there is no limitation set, that’s a rate limit issue.
- At 2FA Code Verification page, try to brute-force for valid 2FA and see if there is any success.
- You can also try to initiate, requesting OTP’s at one side and brute-forcing at another side. At some point, the OTP will coincide and may give you a quick result.

4.  Password Reset / Email Change — 2FA Disable:

- Assuming that you are able to perform sophisticated phishing campaigns, force the end user to do change the password
- 2FA is disabled after the email is changed or the password is reset. This could be an issue for some organizations. However, it depends on case by case basis

5.  Direct Request:

- Directly navigate to the page which comes after 2FA or any other authenticated page of the application and see if this bypasses the 2FA restrictions.
- If there is no success, change the refer header to the 2FA page URL. This may fool application to pretend as if the request came after satisfying 2FA condition.

6.  Backup Code Abuse:

- Apply same techniques used on 2FA such as Response/Status Code Manipulation, brute-force, etc. to bypass backup codes and disable/reset 2FA

8.  Enabling 2FA Doesn’t Expire Previous Session:

- Login to the application in two different browsers and enable 2FA from 1st session.
- Use 2nd session and if it is not expired, it could be an issue if there is an insufficient session expiration issue. In this scenario, if an attacker hijacks an active session before 2FA, it is possible to carry out all functions without a need for 2FA.

9.  Clickjacking on 2FA Disable Feature:

- Try to iframe the page where the application allows a user to disable 2FA.
- If iframe attack vector is successful, try to perform a social engineering attack to manipulate the victim to fall in to your trap

10. Response Manipulation:

- Check response of the 2FA Request.
    If you observe \[“Success”:false\], change this to \[Success”:true\] and see if it bypasses the 2FA

11. Status Code Manipulation:

- If the Response Status Code is 4xx like 401, 402, etc.
    Change the response Status Code to “200 OK” and see if it bypasses the 2FA

12. 2FA Code Reusability:

- Request a 2FA code and use it.
- Now, re-use the same 2FA code in another session and if it authenticated successfully, that’s a potential issue
- Also, try requesting multiple 2FA codes, and see if previously requested codes expire or not when a new code is requested
- Also, try to re-use the previously used code after long time duration i.e 1 day or more. If it is successful, that is an issue since 1 day is more than enough for a sophisticated hacker to either brute-force or crack a 6-digit 2FA Code.

13. CSRF on 2FA Disable Feature:

- Navigate to 2FA Page and click on “Disable 2FA” and capture this request with Burp Suite & generate a CSRF PoC
- Send this PoC to the victim, and check if CSRF happens successfully and remove the 2FA from the victim account
- Also, check if there is any authentication confirmation such as password or 2FA code required before disabling 2FA

14. Two seperate domain:

- if 2FA is enabled on Domain(A) and you can login on Domain(B) without 2FA,But only if you created an account in Domain(A)
- Open Burp and intercept request after entering a password and change Host header to Domain(B) to bypass 2FA

A Map Of types of Techniques to bypass 2FA
[here](https://xmind.app/m/8Hkymg/)

* * *

## **The End**
