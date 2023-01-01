`1 January 2023`
## **Day 15 What I Have Learned**:
***
## **Session Puzzling Attack**:
- An app-level issue that may allow an attacker to bypass authentication, elevate privileges, skip MFA, or exploit any related issues.
- Also known as Session Variable Overloading Attack.
- When an application utilizes the same session variable for multiple purposes, this can be abused by an attacker to trick the application and perform the action as an authenticated or privileged user.
- In Simple Words, For example, if the application generates a session identifier at an unauthenticated page and later that can be used to access the authenticated page, it is a session puzzling vulnerability.
## **Used For**:
- To Bypass efficient authentication enforcement mechanisms, and impersonate legitimate users.
- Elevate the privileges of a malicious user account, in an environment that would otherwise be considered foolproof.
- Skip over qualifying phases in multi-phase processes, even if the process includes all the commonly recommended code level restrictions.
- Manipulate server-side values in indirect methods that cannot be predicted or detected.
- Execute traditional attacks in locations that were previously unreachable, or even considered secure.
## **Scenario**:
1. An attacker navigates to the /forget_pass page of the application.
2. He provides the username of the victim user and initiate a password reset request and observes the application assigns a session identifier by looking at the cookies.
3. Now, the attacker utilizes the same session identifier in cookies to access an authenticated page /my_profile and the page is accessed successfully with the victim user's information.
4. This is Session Puzzling/Session Variable Overloading Attack.
5. Always check for the session identifier generation at various unauthenticated or lower privileged pages and see if they can be used to access authenticated or higher privileged pages.
***
## **Reference**:
- [Session Puzzling To Bypass 2fa](https://dzone.com/articles/using-session-puzzling-to-bypass-two-factor-authen).
- [Hunting Session Overloading Vulnerability](https://infosecwriteups.com/hunting-session-overloading-d2ec860c49c0).
- [Session Puzzling Attack: an artistic way of bypassing authentication](https://medium.com/@maheshlsingh8412/session-puzzling-attack-bypassing-authentication-29f4ff2fd4f5).
- [PuzzleMail](https://code.google.com/archive/p/puzzlemall/downloads).
***
## **The End**