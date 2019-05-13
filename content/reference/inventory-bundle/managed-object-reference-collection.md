---
weight: 40
title: Managed object reference collection
layout: redirect
---

### ManagedObjectReferenceCollection [application/vnd.com.nsn.cumulocity.managedObjectReferenceCollection+json]

|Name|Type|Occurs|Description|
|:---|:---|:-----|:----------|
|self|URI|1|Link to this resource.|
|references|ManagedObjectReference|0..n|List of managed object references, see below.|
|statistics|PagingStatistics|1|Information about paging statistics.|
|prev|URI|0..1|Link to a potential previous page of managed objects.|
|next|URI|0..1|Link to a potential next page of managed objects.|

### GET a managed object reference collection

Response body: ManagedObjectReferenceCollection

Example Request: Get reference collection of a certain managed object

Note that a "404 Not Found" error will appear if the object has no references.

    GET /inventory/managedObjects/<<deviceId>>/<<references>>
    Host: ...
    Authorization: Basic
    Accept: application/vnd.com.nsn.cumulocity.managedObjectReferenceCollection+json;ver=...

> Please note that references can be either **childDevices** or **childAssets**.

Example Response:

    HTTP/1.1 200 OK
    Content-Type: application/vnd.com.nsn.cumulocity.managedObjectReferenceCollection+json;ver=...
    Content-Length: ...

    {
      "self" : "<<This ManagedObjectReferenceCollection URL>>",
      "references" : [
        {
          "self" : "<<ManagedObjectReference URL>>",
          "managedObject" : {
            "self" : "<<ManagedObject 1 URL>>",
            "name" : "Meter1",
            "id" : "1",
            ...
          }
        },
        {
          "self" : "<<ManagedObjectReference URL>>",
          "managedObject" : {
            "self" : "<<ManagedObject 2 URL>>",
            "name" : "Meter2",
            "id" : "2",
            ...
          }
        }
      ],
      "statistics" : {
        "pageSize" : 5,
        "currentPage : 1
      },
      "next": "...",
      "prev": "..."
    }

### POST - add a managed object reference to the collection

Request body: ManagedObjectReference

Response body: ManagedObjectReference

Required role: ROLE\_INVENTORY\_ADMIN or parent and child owner

Example Request: Add a ManagedObjectReference

    POST /inventory/managedObjects/<<deviceId>>/<<references>>
    Host: ...
    Authorization: Basic ...
    Content-Length: ...
    Content-Type: application/vnd.com.nsn.cumulocity.managedObjectReference+json;ver=...

    {
      "managedObject" : { "self" :"<<ManagedObject URL>>" }
    }

Example Response:

    HTTP/1.1 201 Created
    Content-Type: application/vnd.com.nsn.cumulocity.managedObjectReference+json;ver=...
    Content-Length: ...
    Location: <<This ManagedObjectReference URL>>
    {
      "self" : "<<This ManagedObjectReference URL>>,
      "managedObject" : {
        "id" : "2",
        "self" : <<ManagedObject 2 URL>>,
        "name" : "Meter2",
        ...
      }
    }

As an alternative it is also allowed to pass the following reference object in the request body when adding to the collection:

    {
      "managedObject" : { "id" :"<<ManagedObject id>>" }
    }