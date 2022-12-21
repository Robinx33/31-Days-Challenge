`20 December 2022`

## **Day 3: What I have Learned**

* * *

## **Security Assertion Markup Language**:

- It is widely used for authentication.
- It uses XML schema and is prone to multiple security vulnerabilities
- Its primary role in online security is that it enables you to access multiple web applications using one set of login credentials

## **SAML 3-Way Handshake**:
1. A user attempts to access an application (Service Provider).
2. The service provider sends via a SAML Authentication Request to the Identity Provider.
3. The identity provider sends a Signed Assertion back to the service provider (SP) identifying the user and allowing the SP to log them in.

* * *

## **Techniques**:

**Signature Wrapping (XSW) Attacks**:

- XSW Attacks happen when the XML Digital Signature (XML DSig) is not validated which is used to establish a trust b/w IDPs & Service Providers.
- This attack can lead to situations like Privilege Escalation, Authentication Abuse & Denial of Service as well.

**Resources**:

1.  [Bypassing-Saml20-SSO](https://research.aurainfosec.io/bypassing-saml20-SSO/).
2.  There are multiple variants of XSW attacks from XSW1 to XSW8 (Way of exploitation varies a bit). You can read more about them here in little details
    [Here](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SAML%20Injection/README.md).

* * *

**XML Attacks**:
- Due to the improper input validation and DTD processing
The SAML implementation might be Vulnerable to XXE and XML DoS Attacks like Billian Laugh Attack.

**Resources**:
1. [Saml-XML-Injection](https://research.nccgroup.com/2021/03/29/saml-xml-injection/).
***

 **SAML Message Integrity Abuse**:
 - Using the SAML Message from other users or forged SAML message to bypass the restriction or may lead to bypass the authentication.
***
**Missing / Invalid Signature**:
- Missing or Invalid Signature may allow an attacker to forge a signature and abuse the implementation.
***
**SAML Message Replay**:
- Assertion ID should be unique and one ID should be accepted only once.
**Resorces**:
1. [The Dangers Of SAML Replay Attacks](https://www.idm-360.com/idm360/the-dangers-of-saml-replay-attacks/).
***
**CSRF**:
- Due to improper validation it is possible to carry out CSRF in SAML Implementation.
***
**XML Comment Handling**:
- A threat actor who already has authenticated access into an SSO system can authenticate as another user without that individual’s SSO password.
***
**XSLT**:
- XSLT (eXtensible Stylesheet Transformation Language) Attack can also be leverage against SAML Implementation.

**Resources**:
1. [XSLT Attack](http://sso-attacks.org/XSLT_Attack).
***
**Token Recipient Confusion**:
- Attacker Token is used to login to Victim Account.

**Resources**:
1. [Token Recipient Confusion](http://sso-attacks.org/Token_Recipient_Confusion).
***
## **Labs & Resources**:
1. [SSO Attacks](http://sso-attacks.org/Category:Attack_Categorisation_By_Attack_on_SAML).
2. [Methodology 1](https://epi052.gitlab.io/notes-to-self/blog/2019-03-07-how-to-test-saml-a-methodology/).
3. [Methodology 2]().
4. [Methodology 3]().
5. [Cheatsheet](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/SAML_Security_Cheat_Sheet.md).
## **Reports**:
1. [SAML Response Reuse on hackerone.com/users/saml/auth](https://hackerone.com/reports/888930) ($500).
2. [SAML authentication bypass](https://hackerone.com/reports/812064).
***
## **The End**
