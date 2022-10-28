---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <p>© 2022 Oxygen</p>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Patten One Platform Student Management API document! You can use these APIs to access student registry API endpoints, which can get information on student enrollment information, grades, and so on in our database.

Request base url(baseUrl): 

`https://1.1.1.1/api/`


# Authentication


One Platform uses session token to allow access to the API. You can register a new One Platform client ID and client secret pair by contacting our tech support team: [support@sv.patten.edu](support@sv.patten.edu).

## Get token

```shell
curl "<baseUrl>/auth/token" \
  -X POST \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H 'cache-control: no-cache' \
```

This endpoint retrieves a api token.

### HTTP Request

`POST baseUrl/auth/token`

### Request Query Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
client_id | Required | String | Valid official client id | 'STG38RC' | The Id of the client
client_secret | Required | String | Valid client secret | 'dBTqGQRvA8HHx6D36Ovq' | The secret key of the client
grant_type | Required | String | 'client_credentials' | 'client_credentials' | Must be "client_credentials"

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "token": "HHx6D36OvqJ0QIYfbvDQ",
  "expire": 78000
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
token | String | 'HHx6D36OvqJ0QIYfbvDQ' | API access token
expire | Number | 78000 | Token get expired in seconds.

We expect the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: JWT <token>`

<aside class="notice">
You must replace <code>token</code> with your personal API token.
</aside>

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: JWT <token>"
```

> Make sure to replace `token` with your API key.

# Application

## Create new application

```shell
curl "<baseUrl>/application/create" \
  -X POST \
  -H "Authorization: JWT <token>"
```

This endpoint create a new application.

### HTTP Request

`POST baseUrl/application/create`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
first_name | Required | String | Only alphabet (a~z) allowed with first letter capitalized | 'Jack' | The first name of the student to be added
last_name | Required | String | Only alphabet (a~z) allowed with first letter capitalized | 'Ma' | The last name of the student to be added
major | Required | String | 'Master of Business Administration'(Or other registered major full name with all first letters capitalized) | 'Master of Business Administration' | The major of the student to be added
concentration | Required | String | 'Finance'/'Sales Management'/... (Or other allowed concentration full name with all first letters capitalized) | 'Finance' | The concentration of the student to be added
birthday | Required |  String | Date format in 'MM/DD/YY'| '02/15/76' | The birthday of the student to be added
country | Required | String | Country official name in English | 'China' | The country of citizenship for the student to be added 
email | Required | String | Student's confirmed email address with all lower case | 'jm@patten.edu' | The email of the student to be added 
phone | Required | String | Student's personal phone number with country code ('+1: USA/Canada; +86: China; ...') | '+12012312' | The phone number of the student to be added 

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "appID" : "62"
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
appID | String | '62' | Unique number.

## Retrieve a specific application

```shell
curl "<baseUrl>/application/62" \
  -H "Authorization: JWT <token>"
```

This endpoint retrieve an application

### HTTP Request

`GET baseUrl/application/62`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
appID | Required | String | Valid application ID | '62' | The appID of the application to retrieve


### Response Body

> The above command returns JSON structured like this:

```json
  [{
    "appID": "62",
    "first_name": "Yu",
    "last_name": "Dong",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "12/05/93",
    "status": "pending_review",
    "committee_comment": "",
    "create_timestamp": "2020-07-26T23:47:59.598Z"
  }]
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
student | Array of Object | '[]' | If the application with the appID is not exist, return value will be an empty array

## Retrieve all applications created by the client

```shell
curl "<baseUrl>/application/all" \
  -H "Authorization: JWT <token>"
```

This endpoint retrieve an application

### HTTP Request

`GET baseUrl/application/all`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------


### Response Body

> The above command returns JSON structured like this:

```json
  [{
    "appID": "62",
    "first_name": "Yu",
    "last_name": "Dong",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "12/05/93",
    "status": "pending_review",
    "committee_comment": "",
    "create_timestamp": "2020-07-26T23:47:59.598Z"
  },
  {
    "appID": "63",
    "first_name": "Ma",
    "last_name": "Jack",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "01/03/92",
    "status": "accepted",
    "committee_comment": "",
    "create_timestamp": "2020-07-26T23:47:59.598Z"
  },
  ]
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
student | Array of Object | '[]' | If no exist applications, return an empty array

## Update a specific application

```shell
curl "<baseUrl>/application/update" \
  -X POST \
  -H "Authorization: JWT <token>"
```

This endpoint update a specific application info.

### HTTP Request

`POST baseUrl/application/update`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
appID | Required | String | Valid application ID | '62' | The appID of the application to be updated
first_name | Optional | String | Only alphabet (a~z) allowed with first letter capitalized | 'Jack' | The first name of the student to be updated
last_name | Optional | String | Only alphabet (a~z) allowed with first letter capitalized | 'Ma' | The last name of the student to be updated
major | Optional | String | 'Master of Business Administration'(Or other registered major full name with all first letters capitalized) | 'Master of Business Administration' | The major of the student to be updated
concentration | Optional | String | 'Finance'/'Sales Management'/... (Or other allowed concentration full name with all first letters capitalized) | 'Finance' | The concentration of the student to be updated
birthday | Optional |  String | Date format in 'MM/DD/YY'| '02/15/76' | The birthday of the student to be updated
country | Optional | String | Country official name in English | 'China' | The country of citizenship for the student to be updated 
email | Optional | String | Student's confirmed email address with all lower case | 'jm@patten.edu' | The email of the student to be updated 
phone | Optional | String | Student's personal phone number with country code ('+1: USA/Canada; +86: China; ...') | '+12012312' | The phone number of the student to be updated

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)

## Upload required documents

```shell
curl "<baseUrl>/application/fileupload" \
  -X POST \
  -H "Authorization: JWT <token> Content-Type: multipart/form-data;" \
  -F "file[]=/path/to/file"
```

This endpoint update a specific student enrollment info.

### HTTP Request

`POST baseUrl/application/fileupload`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
appID | Required | String | Valid application ID | '62' | The appID of the application to be updated
file_type | Required | String | Allowed predefined type: 'resume'/'photo_id'/'english_language_proficiency' | 'photo_id' | The type of the uploaded file

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)

# Grades

## Insert new grade record

```shell
curl "<baseUrl>/grade" \
  -X POST \
  -H "Authorization: JWT <token>"
```

This endpoint enroll a new student.

### HTTP Request

`POST baseUrl/grade`

### Request Body Parameters


Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
SID | Required | String | Valid 14-digit student ID | '000-A600861002' | The SID of the student grade to be inserted 
courseId | Required | String | Valid courseId (e.g.: mba500, mba600...) | 'mba500' | The course ID of the student grade to be inserted
unitId | Required | String | Valid unitId (e.g.: u1, u2...) | 'u1' | The unit ID of the student grade to be inserted
questionId | Required | String | Valid unique global question ID (1123, 1134...) | '000101' | The unique question ID of the student grade to be inserted
grade | Required | Number | Integer in range 0~100 | 87 | The grade of the question to be inserted

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200
}
```
Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)

## Get a specific grade record

```shell
curl "<baseUrl>/grade" \
  -H "Authorization: JWT <token>"
```

This endpoint fetch a specific grade record by using SID, courseID, unitID and questionID.

### HTTP Request

`GET baseUrl/grade`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
SID | Required | String | Valid 14-digit student ID | '000-A600861002' | The SID of the student grade to be fetched 
courseId | Required | String | Valid courseId (e.g.: mba500, mba600...) | 'mba500' | The course ID of the student grade to be fetched
unitId | Required | String | Valid unitId (e.g.: u1, u2...) | 'u1' | The unit ID of the student grade to be fetched
questionId | Required | String | Valid unique global question ID (1123, 1134...) | '000101' | The unique question ID of the student grade to be fetched

### Response Body

> The above command returns JSON structured like this:

```json
  [{
    "SID": "000-A600861002",
    "courseId": "mba500",
    "unitId": "u1",
    "questionID": "000101",
    "grade": 87,
    "lastUpdateTimestamp": 1618729540,
  }]
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
grades | Array of Object | '[]' | If the grade with the SID,unitId, questionId does not exist, return value will be an empty array

## Get all grade records of a specific student

```shell
curl "<baseUrl>/grade/all" \
  -H "Authorization: JWT <token>"
```

This endpoint fetch all grade records by using SID.

### HTTP Request

`GET baseUrl/grade/all`

### Request Body Parameters


Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
SID | Required | String | Valid 14-digit student ID | '000-A600861002' | The SID of the student grade to be fetched

### Response Body

> The above command returns JSON structured like this:

```json
  [{
    "SID": "000-A600861002",
    "courseId": "mba500",
    "unitId": "u1",
    "questionID": "000101",
    "grade": 87,
    "lastUpdateTimestamp": 1618729540,
  },
  {
    "SID": "000-A600861002",
    "courseId": "mba500",
    "unitId": "u2",
    "questionID": "000201",
    "grade": 90,
    "lastUpdateTimestamp": 1618733649,
  },
  ]
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
grades | Array of Object | '[]' | If the grade with the SID,unitId, questionId does not exist, return value will be an empty array

## Update a specific grade record

```shell
curl "<baseUrl>/grade/update" \
  -X POST \
  -H "Authorization: JWT <token>"
```

This endpoint update a specific grade record.

### HTTP Request

`POST <baseUrl>/grade/update`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
SID | Required | String | Valid 14-digit student ID | '000-A600861002' | The SID of the student grade to be fetched 
courseId | Required | String | Valid courseId (e.g.: mba500, mba600...) | 'mba500' | The course ID of the student grade to be fetched
unitId | Required | String | Valid unitId (e.g.: u1, u2...) | 'u1' | The unit ID of the student grade to be fetched
questionId | Required | String | Valid unique global question ID (1123, 1134...) | '000101' | The unique question ID of the student grade to be fetched
grade | Required | Number | Integer in range 0~100 | 87 | The grade of the question to be inserted

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200
}
```
Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)

## Upload final paper

```shell
curl "<baseUrl>/grade/finalpaper" \
  -X POST \
  -H "Authorization: JWT <token> Content-Type: multipart/form-data;" \
  -F "file[]=/path/to/file"
```

This endpoint upload final paper for a specific course.

### HTTP Request

`POST <baseUrl>/grade/finalpaper`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
SID | Required | String | Valid 14-digit student ID | '000-A600861002' | The SID of the student grade to be fetched 
courseId | Required | String | Valid courseId (e.g.: mba500, mba600...) | 'mba500' | The course ID of the student grade to be fetched
file | Required | String | Available file local path. File must in fomart of doc, docx or pdf. File size must be less than 5M. | 'example.pdf' | The local path of file to be uploaded

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200
}
```
Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)

# Academic Admin

## Finalize application status

```shell
curl "<baseUrl>/admin/application/finalize" \
  -X POST \
  -H "Authorization: JWT <token>"
```

This endpoint finalize status of a new application.

### HTTP Request

`POST baseUrl/admin/application/finalize`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
appID | Required | String | Valid application ID | '62' | The unique number of the application to be updated
status | Required | String | Allowed predefined status: 'pending_review'/'more_materials_needed'/ 'accepted'/'rejected' | 'accepted' | The final decision of the application by admission comittee
committee_comment | Optional | String | maximum word length: 1024 bytes | 'need photo id' | The comment added by admission comittee

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "SID": null
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
SID |  String | '000-A600861002' |  14-digit student ID or return null if not accepted

## Retrieve uploaded files of  a specific student

```shell
curl "<baseUrl>/admin/application/62" \
  -H "Authorization: JWT <token>"
```

This endpoint retrieves uploaded files of  a specific student.

### HTTP Request

`GET baseUrl/admin/application/62`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
appID | Required | String | Valid appID | '62' | The appID of the application to retrieve


### Response Body

> The above command returns JSON structured like this:

```json
  [{
    "appID": "62",
    "photo_id": null,
    "resume": null,
    "english_language_proficiency": null
  }]
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
files | Array of Object | '[]' | File Blob; If the student upload file is not exist, return null

## Review and verify student's gradebook

```shell
curl "<baseUrl>/admin/grade/review" \
  -X POST \
  -H "Authorization: JWT <token>"
```

This endpoint review and verify a specific student gradebook.

### HTTP Request

`POST baseUrl/admin/grade/review`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
SID | Required | String | Valid 14-digit student ID | '000-A600861002' | The SID of the student to be updated
verify | Required | String | 'True'/'False' | 'True' | The verify status of the whole gradebook
comment | Optional | String | maximum word length: 1024 bytes | '' | The comment added by the grade reviewer

### Response Body

> The above command returns JSON structured like this:

```json
  [{
    "status": 200,
  }]
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)

## Delete a Specific Student

```shell
curl "<baseUrl>/student/delete" \
  -X POST \
  -H "Authorization: JWT <token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "success" : "True"
}
```

This endpoint deletes a specific student.

### HTTP Request

`POST <baseUrl>/student/delete/<SID>`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
SID | Required | String | Valid 14-digit student ID | '000-A600861002' | The SID of the student to be updated

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200
}
```
Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
