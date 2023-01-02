`2 January 2023`
## **Mass Assignment Attack**:
- Mass assignment vulnerabilites occur when a user is able to initialize or overwrite server-side variables for which are not intended by the application
- Occurs when an app allows a user to manually add parameters in an HTTP Request & the app process value of these parameters when processing the HTTP Request & it affects the response that is returned to the user. 
- Attackers can sometimes use this methodology to create new parameters that the developer never intended which in turn creates or overwrites new variable or objects in program code that was not intended.
## **Steps**:
1. Capture the Request and Observe its response.
2. Include the parameters present in Response to the HTTP Request with the modified values.
3. Observe if the values in response are changed as Modified values.
4. Navigate to the application and observe if the changes are also reflected on the UI level.
## **What can be achieved**:
- Authentication Bypass (2FA) - Adding "Success":true parameter in the request with the wrong OTP.
- Privilege Escalation - Changing the Role/Access Level.
- Modifying/Overwriting Sensitive Information.
- Client-Side/Server-Side validation might be missing in the parameters that are not editable by the user from the UI level and if can be abused through mass assignment, it can lead to exposure to some serious issues.
- Premium Feature Abuse/Bypass Payment Restrictions.
***
## **Reports**:
- [Users can enable API access for free via mass assignment](https://hackerone.com/reports/267781).
- [Mass Assignment Vulnerability in partners.uber.com](https://hackerone.com/reports/99424) ($1000).

## **References**:
- [Mass Assignment Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html).
- [Api Mass Assignment](https://www.virtuesecurity.com/kb/api-mass-assignment/).

***
## **The End**