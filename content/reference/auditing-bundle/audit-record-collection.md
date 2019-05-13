---
weight: 30
title: Audit record collection
layout: redirect
---


### AuditRecordCollection [application/vnd.com.nsn.cumulocity.auditRecordCollection+json]

|Name|Type|Occurs|Description|
|:---|:---|:-----|:----------|
|self|URI|1|Link to this resource.|
|auditRecords|AuditRecord|0..n|List of audit records, see below.|
|statistics|PagingStatistics|1|Information about paging statistics.|
|prev|URI|0..1|Link to a potential previous page of audit records.|
|next|URI|0..1|Link to a potential next page of audit records.|

The "source" object of an audit record contains the properties "id" and "self".

### POST - create a new audit record

Request body: AuditRecord

Response body: AuditRecord
  
Required role: ROLE\_AUDIT\_ADMIN

Example request:

    POST /audit/auditRecords
    Host: ...
    Authorization: Basic ...
    Content-Length: ...
    Content-Type: application/vnd.com.nsn.cumulocity.auditRecord+json;ver=...
    {
      "type" : "com_cumulocity_audit_LoginFailure",
      "time" : "2011-09-06T12:03:27.845Z",
      "text" : "Login failed after 3 attempts.",
      "user" : "Spock",
      "application" : "Omniscape",
      "activity" : "login",
      "severity" : "warning"
    }

Example response:

    HTTP/1.1 201 Created
    Content-Type: application/vnd.com.nsn.cumulocity.auditRecord+json;ver=...
    Content-Length: ...
    Location: <<URL of new audit record>>
    {
      "id" : "123",
      "self" : "<<URL of new audit record>>",
      "creationTime" : "2011-09-06T12:03:27.927Z",
      "type" : "com_cumulocity_audit_LoginFailure",
      "time" : "2011-09-06T12:03:27.845Z",
      "text" : "Login failed after 3 attempts.",
      "user" : "Spock",
      "application" : "Omniscape",
      "activity" : "login",
      "severity" : "warning"
    }

The "id" and "creationTime" of the new audit record are generated by the server and returned in the response to the POST operation.

### GET audit records

Response body: AuditRecordCollection
  
Required role: ROLE\_AUDIT\_READ

Example request: Retrieve audit records

	GET /audit/auditRecords
	Host: ...
	Authorization: Basic ...
	Accept: application/vnd.com.nsn.cumulocity.auditRecordCollection+json;

Example response:

    HTTP/1.1 200 OK
    Content-Type: application/vnd.com.nsn.cumulocity.auditRecordCollection+json;ver=...
    Content-Length: ...
    {
      "self" : "",
      "auditRecords" : [
        {
          "id" : "123",
          "self" : "<<AuditRecord 123 URL>>",
          "creationTime" : "2011-09-06T12:03:27.927Z",
          "type" : "com_cumulocity_audit_LoginFailure",
          "time" : "2011-09-06T12:03:27.845Z",
          "text" : "Login failed after 3 attempts.",
          "user" : "Spock",
          "application" : "Omniscape",
          "activity" : "login",
          "severity" : "warning"
        }
      ],
      "statistics" : {
        "totalPages" : 3,
        "pageSize" : 5,
        "currentPage" : 1
      }
    }
    
In case of executing range queries on audit logs API, like query by dateFrom and dateTo, audits are returned in order from the last to the latest. 
It is possible to change the order by adding query parameter "revert=true" to the request URL.

### DELETE - delete an collection of auditRecords

The DELETE method allows for deletion of auditRecords collections. Applicable query parameters are equivalent to GET method.

Request body: N/A

Response body: N/A
  
Required role: ROLE\_AUDIT\_ADMIN

Example request:

     DELETE: /audit/auditRecords ....
     Host: ...
     Authorization: Basic ...
     
Example response:

    HTTP/1.1  204 NO CONTENT
    