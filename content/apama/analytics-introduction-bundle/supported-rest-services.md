---
weight: 25
title: Supported REST services
layout: redirect
---

Apama EPL Apps is designed to listen for REST (Representational State Transfer) services and supports all GET, POST, PUT and DELETE operations. Example requests for the different operations are listed below.

To perform these operations, you must have READ and ADMIN permissions for "CEP management" (see also [Managing permissions](/users-guide/administration/#managing-permissions) in the *User guide*).

> **Info**: This API requires version 10.6.0 or above of the Apama-ctrl microservice.

### Request headers for all operations

Each request must be authenticated to Cumulocity IoT.

| Name   | Description                                        |
| ------ | -------------------------------------------------- |
| Accept | "application/json". This is a mandatory parameter. |

### Common response codes

The following common error response codes can be expected for all requests:

| Code | Description                                                  |
| ---- | ------------------------------------------------------------ |
| 401  | Unauthorized.                                                |
| 403  | Forbidden. Apama EPL Apps is not available with Apama Starter. |

Any other response codes that can be expected from a specific request are given below.

### Common field descriptions

The following common fields are available with the responses, depending on the operation:

| Field       | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| contents    | The full contents of the EPL file.                           |
| description | A description of the file.                                   |
| errors      | A list of all compilation errors in the file, if any, with line numbers and text. |
| id          | A unique identifier of the file.                             |
| name        | The name provided for this bit of EPL.                       |
| state       | Whether the EPL is injected into the correlator and running. This can either be `active` or `inactive`. |
| warnings    | A list of all compilation warnings in the file, if any, with line numbers and text. |

### GET - Retrieve all available EPL files

Endpoint: `/service/cep/eplfiles`

#### Example request

`GET /service/cep/eplfiles`

#### Responses

| Code | Description                                             |
| ---- | ------------------------------------------------------- |
| 200  | Successful operation. See also the example value below. |
| 400  | Bad request. Header contents has unexpected value.      |

Example value for response code 200:

```
{
  "eplfiles":[
    {
      "description":"",
      "errors":[
 
      ],
      "id":"39615",
      "name":"Ordinal1",
      "state":"active",
      "warnings":[
 
      ]
    }
  ]
}
```

### GET - Retrieve all available EPL files with their contents

Endpoint: `/service/cep/eplfiles`

#### Request parameters

| Name     | Description                                                  |
| -------- | ------------------------------------------------------------ |
| contents | Boolean type. Fetches the EPL files with their contents. This is an optional query parameter. |

#### Example request

`GET /service/cep/eplfiles?contents=true`

#### Responses

| Code | Description                                             |
| ---- | ------------------------------------------------------- |
| 200  | Successful operation. See also the example value below. |

Example value for response code 200:

```
{
  "eplfiles":[
    {
      "contents":"monitor M0 { action onload() { on wait(1.0) { log \"Hello\" at INFO; }}}",
      "description":"",
      "errors":[
      ],
      "id":"39615",
      "name":"Ordinal1",
      "state":"active",
      "warnings":[
      ]
    }
  ]
}
```

### GET - Retrieve EPL file by identifier

Endpoint: `/service/cep/eplfiles/{id}`

#### Request parameters

| Name | Description                                                  |
| ---- | ------------------------------------------------------------ |
| id   | Identifier of the EPL file to be fetched. This is a mandatory parameter. |

#### Example request

`GET /service/cep/eplfiles/{{id}}`

#### Responses

| Code | Description                                                  |
| ---- | ------------------------------------------------------------ |
| 200  | Successful operation. See also the example value below.      |
| 404  | File with identifier not found. See also the [example value for this response code](#example-404) at the end of this section. |

Example value for response code 200:

```
{
      "contents":"monitor M0 { action onload() { on wait(1.0) { log \"Hello\" at INFO; }}}",
      "description":"",
      "errors":[
      ],
      "id":"39615",
      "name":"Ordinal1",
      "state":"active",
      "warnings":[
      ]
}
```

### POST - Create a new EPL application

Endpoint: `/service/cep/eplfiles`

#### Example request

`POST /service/cep/eplfiles`

#### Example response

```
{
  "name": "Ordinal1",
  "contents": "monitor M1 { action onload() { on wait(1.0) { log \"Hello\" at INFO; }}}",
  "state": "active",
  "description": ""
}
```

Note the following:

- To avoid a clash with other files, the `name` is used for the package of the file (rather than a user-provided package). It must be valid to use as an EPL identifier which consists of letters and numbers only. The name must be unique across all EPL files. 
- Make sure to provide safely escaped `contents`.
- `description` is optional and can be empty.


#### Responses

| Code | Description                                                  |
| ---- | ------------------------------------------------------------ |
| 201  | Successfully created / Created with errors in file / Created with warnings in file. See also the examples below. |
| 405  | Invalid input.                                               |

Example for response code 201 when successfully created:

```
{
  "description":"",
  "errors":[
 
  ],
  "id":"39615",
  "name":"Ordinal1",
  "state":"active",
  "warnings":[
 
  ]
}
```

Example for response code 201 when created with warnings or errors:

```
{
  "description":"",
  "errors":[
    {
      "line":5,
      "text":"assigning a float to an integer variable"
    }
  ],
  "id":"39651",
  "name":"Ordinal1",
  "state":"inactive",
  "warnings":[
    {
      "line":10,
      "text":"\"assert\" may become a reserved word in future versions of EPL"
    }
  ]
}
```

### PUT - Update EPL file by identifier

Endpoint: `/service/cep/eplfiles/{id}`

#### Request parameters

| Name | Description                                                  |
| ---- | ------------------------------------------------------------ |
| id   | Identifier of the EPL file to be updated. The identifier has to be included in the path. This is a mandatory parameter. |

#### Example request

`PUT /service/cep/eplfiles/{id}`

#### Example response

```
{
  "name": "Ordinal1",
  "contents": "monitor M1 { action onload() { on wait(1.0) { log \"Hello\" at INFO; }}}",
  "state": "active",
  "description": ""
}
```

See also the information given for the POST request.

#### Responses

| Code | Description                                                  |
| ---- | ------------------------------------------------------------ |
| 200  | Successfully updated. See also the example values below.     |
| 404  | File with identifier not found. See also the [example value for this response code](#example-404) at the end of this section. |

Example value for response code 200 when successfully updated with no errors:

```
{
  "description":"",
  "errors":[
 
  ],
  "id":"39615",
  "name":"Ordinal1",
  "state":"active",
  "warnings":[
 
  ]
}
```

Example value for response code 200 when updated with errors or warnings:

```
{
  "description":"",
  "errors":[
    {
      "line":5,
      "text":"assigning a float to an integer variable"
    }
  ],
  "id":"39651",
  "name":"Ordinal1",
  "state":"inactive",
  "warnings":[
    {
      "line":10,
      "text":"\"assert\" may become a reserved word in future versions of EPL"
    }
  ]
}
```

### DELETE - Delete EPL file by identifier

Endpoint: `/service/cep/eplfiles/{id}`

#### Request parameters

| Name | Description                                                  |
| ---- | ------------------------------------------------------------ |
| id   | Identifier of the EPL file to be deleted. The identifier has to be included in the path. This is a mandatory parameter. |

#### Example request

`DELETE /service/cep/eplfiles/{{id}}`

#### Responses

| Code | Description                                                  |
| ---- | ------------------------------------------------------------ |
| 200  | Successfully deleted.                                        |
| 404  | File with identifier not found. See also the [example value for this response code](#example-404) at the end of this section. |

### Example value for response code 404<a name="example-404"></a>

The response code 404 indicates that a file with a specific identifier was not found. 

```
{
  "error":"Not Found",
  "exception":"com.apama.in_c8y.FileNotFoundException",
  "message":"File with id 39613 not found",
  "path":"/eplfiles/39613",
  "status":404,
  "timestamp":"2020-01-17T12:21:42.457+0000"
}
```

where 

- `error` is the error message.
- `exception` specifies the exception that was raised.
- `message` is a description of the exception message.
- `path` is the path that was requested.
- `status` is the status of the application.
- `timestamp` is the timestamp in ISO format.