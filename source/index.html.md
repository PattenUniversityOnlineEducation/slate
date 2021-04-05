---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <p>© 2021 Oxygen</p>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Patten One Platform third party organization API! You can use our API to access student registry API endpoints, which can get information on student enrollment information, grades, and so on in our database.

Request base url(baseUrl): 

`https://app.patten.edu:4000/api/`


# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: Bear <token>"
```

> Make sure to replace `token` with your API key.

One Platform uses API token to allow access to the API. You can register a new One Platform API token by contacting our tech support team: [support@sv.patten.edu](support@sv.patten.edu).

Kittn expects for the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bear <token>`

<aside class="notice">
You must replace <code>token</code> with your personal API token.
</aside>

# Students

## Enroll new student

```shell
curl "<baseUrl>/student/enroll" \
  -X POST \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "success" : "True"
}
```

This endpoint enroll a new student.

### HTTP Request

`POST baseUrl/student/enroll`

### URL Parameters

Parameter | Example | Description
--------- | ----------- | -----------
first_name | 'Jack' | The first name of the student to be added
last_name | 'Ma' | The last name of the student to be added
major | 'Master of Business Administration' | The major of the student to be added
concentration | 'Finance' | The concentration of the student to be added
birthday | '02/15/76' | The birthday of the student to be added
country | 'China' | The country of citizenship of the student to be added 
email | 'jm@patten.edu' | The email of the student to be added 
phone | '+12012312' | The phone number of the student to be added 

## Get All Students

```shell
curl "<baseUrl>/student/all" \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "SID": "000-A600861001",
    "first_name": "Jack",
    "last_name": "Ma",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "02/15/76",
    "enroll_date": "07/28/20",
    "status": "Registered"
  },
  {
    "SID": "000-A600861002",
    "first_name": "Yu",
    "last_name": "Dong",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "12/05/93",
    "enroll_date": "07/28/20",
    "status": "Registered"
  }
]
```

This endpoint retrieves all students registered by this organization account.

### HTTP Request

`GET baseUrl/student/all`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
status | 'Registered' | The result will include kittens that have the same register status.


## Get a Specific Student

```shell
curl "<baseUrl>/student/000-A600861002" \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
  [{
    "SID": "000-A600861002",
    "first_name": "Yu",
    "last_name": "Dong",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "12/05/93",
    "enroll_date": "07/28/20",
    "status": "Registered"
  }]
```

This endpoint retrieves a specific student.

### HTTP Request

`GET http://example.com/student/<SID>`

### URL Parameters

Parameter | Description
--------- | -----------
SID | The SID of the student to retrieve

## Update specific student

```shell
curl "<baseUrl>/student/enroll" \
  -X UPDATE \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "success" : "True"
}
```

This endpoint update a specific student enrollment info.

### HTTP Request

`UPDATE baseUrl/student/enroll`

### URL Parameters

Parameter | Example | Description
--------- | ----------- | -----------
first_name | 'Jack' | The first name of the student to be added
last_name | 'Ma' | The last name of the student to be added
major | 'Master of Business Administration' | The major of the student to be added
concentration | 'Finance' | The concentration of the student to be added
birthday | '02/15/76' | The birthday of the student to be added
country | 'China' | The country of citizenship of the student to be added 
email | 'jm@patten.edu' | The email of the student to be added 
phone | '+12012312' | The phone number of the student to be added 

## Delete a Specific Student

```shell
curl "<baseUrl>/student/000-A600861002" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
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

`DELETE <baseUrl>/student/<SID>`

### URL Parameters

Parameter | Description
--------- | -----------
SID | The SID of the student to delete

# Grades

## Insert new grade record

```shell
curl "<baseUrl>/student/enroll" \
  -X POST \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "success" : "True"
}
```

This endpoint enroll a new student.

### HTTP Request

`POST baseUrl/grade`

### URL Parameters

Parameter | Example | Description
--------- | ----------- | -----------
first_name | 'Jack' | The first name of the student to be added
last_name | 'Ma' | The last name of the student to be added
major | 'Master of Business Administration' | The major of the student to be added
concentration | 'Finance' | The concentration of the student to be added
birthday | '02/15/76' | The birthday of the student to be added
country | 'China' | The country of citizenship of the student to be added 
email | 'jm@patten.edu' | The email of the student to be added 
phone | '+12012312' | The phone number of the student to be added 

## Get All Students's Grades

```shell
curl "<baseUrl>/grade/all" \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "SID": "000-A600861001",
    "first_name": "Jack",
    "last_name": "Ma",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "02/15/76",
    "enroll_date": "07/28/20",
    "status": "Registered"
  },
  {
    "SID": "000-A600861002",
    "first_name": "Yu",
    "last_name": "Dong",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "12/05/93",
    "enroll_date": "07/28/20",
    "status": "Registered"
  }
]
```

This endpoint retrieves all students registered by this organization account.

### HTTP Request

`GET baseUrl/grade`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
status | 'Registered' | The result will include kittens that have the same register status.


## Get a Specific Student

```shell
curl "<baseUrl>/grade/000-A600861002" \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
  [{
    "SID": "000-A600861002",
    "first_name": "Yu",
    "last_name": "Dong",
    "major": "Master of Business Administration",
    "concentration": "Finance",
    "birthday": "12/05/93",
    "enroll_date": "07/28/20",
    "status": "Registered"
  }]
```

This endpoint retrieves a specific student.

### HTTP Request

`GET http://example.com/grade/<SID>`

### URL Parameters

Parameter | Description
--------- | -----------
SID | The SID of the student to retrieve

## Update specific student

```shell
curl "<baseUrl>/grade/<SID>" \
  -X UPDATE \
  -H "Authorization: Bear <token>"
```

> The above command returns JSON structured like this:

```json
{
  "status": 200,
  "success" : "True"
}
```

This endpoint update a specific student enrollment info.

### HTTP Request

`UPDATE <baseUrl>/grade/<SID>`

### URL Parameters

Parameter | Example | Description
--------- | ----------- | -----------
first_name | 'Jack' | The first name of the student to be added
last_name | 'Ma' | The last name of the student to be added
major | 'Master of Business Administration' | The major of the student to be added
concentration | 'Finance' | The concentration of the student to be added
birthday | '02/15/76' | The birthday of the student to be added
country | 'China' | The country of citizenship of the student to be added 
email | 'jm@patten.edu' | The email of the student to be added 
phone | '+12012312' | The phone number of the student to be added 

## Delete a Specific grade record

```shell
curl "<baseUrl>/grade/000-A600861002" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
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

`DELETE <baseUrl>/student/<SID>`

### URL Parameters

Parameter | Description
--------- | -----------
SID | The SID of the student to delete

## Upload final paper

```shell
curl "<baseUrl>/grade/000-A600861002" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
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

`DELETE <baseUrl>/student/<SID>`

### URL Parameters

Parameter | Description
--------- | -----------
SID | The SID of the student to delete
