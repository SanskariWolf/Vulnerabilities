# Description
GraphQL Injection is a vulnerability that occurs when an application processes untrusted user input inside GraphQL queries, mutations, resolvers, or backend operations without proper validation, authorization, or query restrictions.

GraphQL allows clients to request specific data structures through flexible queries. If user-controlled input is improperly handled, attackers may manipulate query execution to access unauthorized data or trigger unintended backend behavior.

GraphQL-based applications commonly expose:
- Queries
- Mutations
- Subscriptions
- Resolvers
- Schema introspection

Common causes include:
- Unsanitized user input
- Dynamic query construction
- Missing authorization checks
- Excessive query complexity
- Enabled introspection in production
- Backend injection through resolvers

GraphQL Injection may result in behavior similar to:
- [[SQL Injection]]
- [[NoSQL Injection]]
- [[Authorization Bypass]]
- [[Sensitive Data Exposure]]
# Steps to Reproduce
### 1. Identify GraphQL Endpoint
Locate GraphQL endpoints.
Common examples:
```text
/graphql
/api/graphql
/query
```
### 2. Inspect Schema Exposure
Determine whether schema discovery is enabled.
Example query:
```graphql
query {
  __schema {
    types {
      name
    }
  }
}
```
Observe whether schema details are returned.
### 3. Identify User-Controlled Parameters
Locate variables accepted by:
- Queries
- Mutations
- Search functionality
- Filters
Example:
```graphql
query {
  user(id:"1") {
    email
  }
}
```
### 4. Manipulate Input
Test whether input affects backend behavior.
Example:
```graphql
query {
  user(id:"unexpected_input") {
    id
  }
}
```
Observe:
- Error responses
- Unauthorized data exposure
- Query manipulation behavior
### 5. Test Nested Query Abuse
Attempt to request unauthorized or excessive data.
Example:
```graphql
query {
  users {
    posts {
      comments {
        author {
          email
        }
      }
    }
  }
}
```
Check whether excessive relationships are exposed.
### 6. Review Authorization Enforcement
Determine whether:
- Access controls apply consistently
- Objects are filtered correctly 
- Hidden fields remain inaccessible
### 7. Verify Exploitation
If the application:
- Executes unintended queries
- Exposes unauthorized data
- Accepts malicious query manipulation
-> vulnerability confirmed
# Impact
GraphQL Injection can lead to:
- Unauthorized data access
- Information disclosure    
- Authorization bypass
- Backend query manipulation
- Data extraction at scale
- Increased attack surface
Impact depends on resolver implementation and backend integrations.
# Remediation
1. Validate and sanitize all user input
2. Avoid constructing backend queries dynamically
3. Disable introspection in production where appropriate
4. Enforce authorization at resolver level
5. Implement query depth and complexity limits
6. Restrict excessive nesting and batching
7. Apply allowlists for operations where possible
8. Monitor abnormal GraphQL query patterns
# Severity
**Medium to Critical**
# CVSS (v3.1)
```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L
```
**Score:** 9.1 (Critical)