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

meta:
  - name: description
    content: Documentation for the Patten OEP API
---

# Introduction

Welcome to the Patten One Platform Student Management API document! You can use these APIs to access student registry API endpoints, which can get information on student enrollment information, grades, and so on in our database.

Request base url(baseUrl) for test: 

`https://test.api.partner.patten.edu/`

Request base url(baseUrl) for production: 

`https://api.partner.patten.edu/`


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
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \
  -d '{"first_name":"xyz","last_name":"xyz",...}'
```

This endpoint create a new application.

### HTTP Request

`POST baseUrl/application/create`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
first_name | Required | String | Only alphabet (a~z) allowed with first letter capitalized | 'Jack' | The first name of the student to be added
last_name | Required | String | Only alphabet (a~z) allowed with first letter capitalized | 'Ma' | The last name of the student to be added
major | Required | String | 'Master of Business Administration - General Management'(Or other registered major full name with all first letters capitalized) | 'Master of Business Administration - General Management' | The major of the student to be added
birthday | Required |  String | Date format in 'MM/DD/YYYY'| '02/15/1976' | The birthday of the student to be added
country | Required | String | Country official name in English | 'China' | The country of citizenship for the student to be added 
email | Required | String | Student's confirmed email address with all lower case | 'jm@patten.edu' | The email of the student to be added 
phone | Required | String | Student's personal phone number with country code ('+1: USA/Canada; +86: China; ...') | '+12012312' | The phone number of the student to be added 

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "app_id" : "62"
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
app_id | String | '62' | Unique number.

## Retrieve a specific application

```shell
curl "<baseUrl>/application/62" \
  -H "Authorization: JWT <token>" \ 
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint retrieve an application

### HTTP Request

`GET baseUrl/application/0000000016`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
app_id | Required | String | Valid application ID | '0000000016' | The app_id of the application to retrieve


### Response Body

> The above command returns JSON structured like this:

```json
{
    "application": {
        "app_id": "0000000016",
        "sid": "20221117000000001671",
        "first_name": "Ethan",
        "last_name": "Ma",
        "email": "jm@patten.edu",
        "phone": "+12012312232",
        "major": "Master of Business Administration - General Management",
        "birthday": "01/02/1991",
        "country": "China",
        "status": "accepted",
        "finalized": "True",
        "edit_by": "STG-test4-API",
        "edit_at": "2022-11-18T08:55:08.000Z",
        "org": "STG",
        "committee_comment": "need transcript"
    }
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
application | Object | '{}' | If the application with the app_id is not exist, return status 400

## Retrieve all applications created by the client

```shell
curl "<baseUrl>/application/all" \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
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
{
    "applications": [
        {
            "app_id": "0000000016",
            "sid": "20221117000000001671",
            "first_name": "Two",
            "last_name": "Ma",
            "email": "jm@patten.edu",
            "phone": "+12012312232",
            "major": "Master of Business Administration - General Management",
            "birthday": "01/02/1991",
            "country": "China",
            "status": "accepted",
            "finalized": "True",
            "edit_by": "STG-test4-API",
            "edit_at": "2022-11-18T08:55:08.000Z",
            "org": "STG",
            "committee_comment": "need transcript"
        },
        {
            "app_id": "0000000018",
            "sid": null,
            "first_name": "One",
            "last_name": "Ma",
            "email": "jm@patten.edu",
            "phone": "+12012312232",
            "major": "Master of Business Administration - General Management",
            "birthday": "01/02/1991",
            "country": "China",
            "status": "rejected",
            "finalized": "True",
            "edit_by": "STG-partner-test1-API",
            "edit_at": "2022-11-19T05:05:55.000Z",
            "org": "STG",
            "committee_comment": "need transcript"
        }
    ]
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
applications | Array of Object | '[]' | If no exist applications, return an empty array

## Update a specific application

```shell
curl "<baseUrl>/application/update" \
  -X POST \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint update a specific application info.

### HTTP Request

`POST baseUrl/application/update`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
app_id | Required | String | Valid application ID | '62' | The app_id of the application to be updated
first_name | Optional | String | Only alphabet (a~z) allowed with first letter capitalized | 'Jack' | The first name of the student to be updated
last_name | Optional | String | Only alphabet (a~z) allowed with first letter capitalized | 'Ma' | The last name of the student to be updated
major | Optional | String | 'Master of Business Administration - General Management'(Or other registered major full name with all first letters capitalized) | 'Master of Business Administration - General Management' | The major of the student to be updated
birthday | Optional |  String | Date format in 'MM/DD/YYYY'| '02/15/1976' | The birthday of the student to be updated
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
  -F "file_type=photo_id" \
  -F "file=@/path/to/file"
```

This endpoint update a specific student enrollment info.

### HTTP Request

`POST baseUrl/application/fileupload`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
app_id | Required | String | Valid application ID | '62' | The app_id of the application to be updated
file_type | Required | String | Allowed predefined type: 'resume'/'photo_id'/'english_language_proficiency'/'undergraduate_degree'/'undergraduate_transcript' | 'photo_id' | The type of the uploaded file
file | Required | String | Available file local path. File must in fomart of pdf only. File size must be less than 5M. | 'example.pdf' | The local path of file to be uploaded

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

# Course Enrollment

## List courses open for enrollment

```shell
curl "<baseUrl>/course/list" \
  -X GET \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data; boundary="----arbitrary boundary"" \ 
  -d '{...}'
```

This endpoint list currently available courses that are open for enrollment.

### HTTP Request

`GET baseUrl/course/list`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------


### Response Body

> The above command returns JSON structured like this:


```json
{
    "courses": [
        {
            "course_id": "mba600-2029win-STG",
            "course_name": "Decision Analysis",
            "semester": "2023 Spring",
            "enrollment_open_at": "2021-01-26T08:00:00.000Z",
            "enrollment_close_at": "2023-02-26T08:00:00.000Z",
            "course_start_at": "2021-03-01T08:00:00.000Z",
            "course_end_at": "2023-06-26T07:00:00.000Z",
            "instructor": "Jess",
            "org": "STG",
            "stg_ta_email": "stg@patten.edu",
            "course_created_by": null,
            "course_created_at": null
        },
        {
            "course_id": "mba600-2030win-STG",
            "course_name": "Decision Analysis",
            "semester": "2023 Spring",
            "enrollment_open_at": "2021-01-26T08:00:00.000Z",
            "enrollment_close_at": "2023-02-26T08:00:00.000Z",
            "course_start_at": "2022-11-10T08:00:00.000Z",
            "course_end_at": "2023-06-26T07:00:00.000Z",
            "instructor": "Jess",
            "org": "STG",
            "stg_ta_email": "stg@patten.edu",
            "course_created_by": null,
            "course_created_at": null
        }
    ]
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
courses | Array of Object | '[]' | If no available courses, return an empty array

## Enroll student into courses

```shell
curl "<baseUrl>/course/enroll" \
  -X POST \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint enroll a new student.

### HTTP Request

`POST baseUrl/course/enroll`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
sid | Required | String | Valid 14-digit student ID | '000-A600861002' | The sid of the student grade to be inserted 
course_id | Required | String | Valid course_id (e.g.: mba500-2023spring, mba600-2023spring...) | 'mba500-2023spring' | The course ID of the student grade to be inserted

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

## Get enrollment by course ID

```shell
curl "<baseUrl>/course/enrollment" \
  -X GET \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint get course enrollment detail info.

### HTTP Request

`GET baseUrl/course/enrollment`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
sid | Required | String | Valid 14-digit student ID | '000-A600861002' | The sid of the student grade to be inserted 
course_id | Required | String | Valid course_id (e.g.: mba500-2023spring, mba600-2023spring...) | 'mba500-2023spring' | The course ID of the student grade to be inserted

### Response Body

> The above command returns JSON structured like this:

```json
  {
      "enrollment": {
          "id": 1,
          "sid": "000-A600861002",
          "course_id": "mba600-2030win-STG",
          "status": "drop",
          "edit_at": "2022-11-19T08:53:08.000Z",
          "edit_by": "STG-partner-test1-API",
          "org": "STG"
      }
  }
```
Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
enrollment | Object | {} | Json object of course enrollment info

## Drop/Withdraw/Extend

```shell
curl "<baseUrl>/course/change" \
  -X POST \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint change a course enrollment status.

### HTTP Request

`POST baseUrl/course/change`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
sid | Required | String | Valid 14-digit student ID | '000-A600861002' | The sid of the student grade to be inserted 
course_id | Required | String | Valid course_id (e.g.: mba500-2023spring, mba600-2023spring...) | 'mba500-2023spring' | The course ID of the student grade to be inserted
status | Required | String | Valid status ('drop'/'withdraw'/'extend') | 'drop' | The change of a course registration status (all changes are final).

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

## Create new question

```shell
curl "<baseUrl>/grade/newquestion" \
  -X POST \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint create new question.

### HTTP Request

`POST baseUrl/grade/newquestion`

### Request Body Parameters


Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | ----------- 
course_id | Required | String | Valid course_id (e.g.: mba500-2023spring, mba600-2023spring...) | 'mba500-2023spring' | The course ID of the student grade to be inserted
unit_id | Required | String | Valid unit_id (e.g.: u1, u2...) | 'u1' | The unit ID of the student grade to be inserted
question_body | Required | String | Any string that is not empty | 'what is your name?' | Text body of the question

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "question_id": "1123"
}
```
Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
question_id | String | '1123' | Return generated unique ID of question

## Insert new grade record

```shell
curl "<baseUrl>/grade/create" \
  -X POST \
  -H "Authorization: JWT <token> Content-Type: multipart/form-data;" \
  -F "sid=000-A600861002" \
  -F "course_id=mba500-2023spring" \
  -F "file=@/path/to/file"
```

This endpoint save a student grade record.

### HTTP Request

`POST baseUrl/grade/create`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
sid | Required | String | Valid 14-digit student ID | '000-A600861002' | The sid of the student grade to be inserted 
course_id | Required | String | Valid course_id (e.g.: mba500-2023spring, mba600-2023spring...) | 'mba500-2023spring' | The course ID of the student grade to be inserted
unit_id | Required | String | Valid unit_id (e.g.: u1, u2...) | 'u1' | The unit ID of the student grade to be inserted
question_id | Required | String | Valid unique global question ID (1123, 1134...) | '000101' | The unique question ID of the student grade to be inserted
answer_text | Optional | String | Any String | '' | The answer from student
file | Optional | String | Available file local path. File must in fomart of pdf only. File size must be less than 5M. | 'example.pdf' | The local path of student file to be uploaded
grade | Required | Number | Integer in range 0~100 | 87 | The grade of the question to be inserted
note | Optional | String | Any String | '' | The comment left by grader

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

## Get student course grade record

```shell
curl "<baseUrl>/grade" \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint fetch a specific grade record by using sid, course_id.

### HTTP Request

`GET baseUrl/grade`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
sid | Required | String | Valid 14-digit student ID | '000-A600861002' | The sid of the student grade to be fetched 
course_id | Required | String | Valid course_id (e.g.: mba500-2023spring, mba600-2023spring...) | 'mba500-2023spring' | The course ID of the student grade to be fetched

### Response Body

> The above command returns JSON structured like this:

```json
{
    "grades": [
        {
            "id": 5,
            "sid": "20221117000000001726",
            "course_id": "mba600-2029win-STG",
            "unit_id": "u1",
            "question_id": 1,
            "answer_text": null,
            "answer_attachment": null,
            "grade": null,
            "note": null,
            "edit_by": "STG-partner-test1-API",
            "edit_at": "2022-12-05T02:42:03.000Z"
        },
        {
            "id": 9,
            "sid": "20221117000000001726",
            "course_id": "mba600-2029win-STG",
            "unit_id": "u1",
            "question_id": 4,
            "answer_text": null,
            "answer_attachment": null,
            "grade": null,
            "note": null,
            "edit_by": "STG-partner-test1-API",
            "edit_at": "2022-12-05T02:58:16.000Z"
        },
        {
            "id": 10,
            "sid": "20221117000000001726",
            "course_id": "mba600-2029win-STG",
            "unit_id": "u1",
            "question_id": 3,
            "answer_text": null,
            "answer_attachment": null,
            "grade": null,
            "note": null,
            "edit_by": "STG-partner-test1-API",
            "edit_at": "2022-12-05T02:58:20.000Z"
        },
        {
            "id": 14,
            "sid": "20221117000000001726",
            "course_id": "mba600-2029win-STG",
            "unit_id": "u1",
            "question_id": 5,
            "answer_text": "D",
            "answer_attachment": null,
            "grade": null,
            "note": null,
            "edit_by": "STG-partner-test1-API",
            "edit_at": "2022-12-05T03:50:48.000Z"
        }
    ]
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
grades | Array of Object | '[]' | Array of grade records

# Academic Admin

## Finalize application status

```shell
curl "<baseUrl>/admin/application/finalize" \
  -X POST \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint finalize status of a new application.

### HTTP Request

`POST baseUrl/admin/application/finalize`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
app_id | Required | String | Valid application ID | '62' | The unique number of the application to be updated
status | Required | String | Allowed predefined status: 'pending_review'/'more_materials_needed'/ 'accepted'/'rejected' | 'accepted' | The final decision of the application by admission comittee
committee_comment | Optional | String | maximum word length: 1024 bytes | 'need photo id' | The comment added by admission comittee

### Response Body

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "sid": null
}
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
sid |  String | '000-A600861002' |  14-digit student ID or return null if not accepted

## Retrieve uploaded files of a specific student

```shell
curl "<baseUrl>/admin/application/62" \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint retrieves uploaded files of  a specific student.

### HTTP Request

`GET baseUrl/admin/application/62`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
app_id | Required | String | Valid app_id | '62' | The app_id of the application to retrieve


### Response Body

> The above command returns JSON structured like this:

```json
  [{
    "app_id": "62",
    "photo_id": null,
    "resume": null,
    "english_language_proficiency": null
  }]
```

Parameter | Type | Example | Possible Return Type
--------- | ----------- | ----------- | -----------
status | Number | 200 | 200: success; 400: request url not accessible; ... (See other error codes explanation in Errors sections)
files | Array of Object | '[]' | File Blob; If the student upload file is not exist, return null

## Register a course

```shell
curl "<baseUrl>/admin/course/register" \
  -X POST \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint opens new courses for enrollment.

### HTTP Request

`POST baseUrl/admin/course/register`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
course_id | Required | String | Valid course_id | 'mba600-2023spring' | The course_id
course_name | Required | String | Valid course name | 'Decision Analysis' | The name of the course to register
semester | Required | String | Valid semester | '2023 Spring' | The course open semester
enrollment_open_at | Required | String | Date format in 'YYYY-MM-DD' | '2023-01-26' | The enrollment start date
enrollment_close_at | Required | String | Date format in 'YYYY-MM-DD' | '2023-02-26' | The enrollment end date
course_start_at | Required | String | Date format in 'YYYY-MM-DD' | '2023-03-01' | The course start date
course_end_at | Required | String | Date format in 'YYYY-MM-DD' | '2023-06-26' | The course end date
instructor | Required | String | Valid name | 'Jesse' | The instructor name
stg_ta_email | Required | String | Valid email | 'stg@patten.edu' | The TA's email address to receive notification
org | Required | String | Valid string | 'STG' | The partner organization ID

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

## Review and verify student's gradebook

```shell
curl "<baseUrl>/admin/grade/review" \
  -X POST \
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
```

This endpoint review and verify a specific student gradebook.

### HTTP Request

`POST baseUrl/admin/grade/review`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
sid | Required | String | Valid 14-digit student ID | '000-A600861002' | The sid of the student to be updated
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
  -H "Authorization: JWT <token>" \
  -H "Content-Type: multipart/form-data" \ 
  -d '{...}'
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

`POST <baseUrl>/student/delete/<sid>`

### Request Body Parameters

Parameter | Required | Type | Validation | Example | Description
--------- | ----------- | ----------- | ----------- | ----------- | -----------
sid | Required | String | Valid 14-digit student ID | '000-A600861002' | The sid of the student to be updated

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
