---
title: Salvio API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Salvio API</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Salvio intervention API!

You can use our API to access user and treatment data, as well as publishing
treatment progress data.

Our examples are currently given using curl requests.

# Authentication

> Example OAuth2 authentication mechanism:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Token: [your_oauth2_token]"
```

Salvio authentication follows the [OAuth2](https://oauth.net/2/) authentication specification.

`Authorization: [to be expanded]`

# User

## Get a specific users details

```shell
curl "http://salv.io/api/user/<userId>"
  -H "Token: [your_oauth2_token]"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "first_name": "Richard",
  "last_name": "Denton",
  "email": "richard@somedomain.com",
  "created_at": "1970/01/01 00:00:00"
}
```

This endpoint retrieves the user details for the given userId. The userId must
have granted your application basic account information access. If this has
not occurred, an empty json response will be received with the HTTP status
403.

### HTTP Request

`GET http://salv.io/api/user/<userId>`

### URL Parameters

Parameter | Description
--------- | -----------
userId | The ID of the user to fetch details for


# Treatment

## Create treatment

```shell
curl "http://sal.vio/api/treatment/create"
  -X POST
  -H "Token: [your_oauth2_token]"
  --data "userId=1"
```

> The above command returns JSON structured like this:

```json
{
  "treatmentId": 201
}
```

This endpoint creates a treatment for a specified user.

### HTTP Request

`PUT http://salv.io/api/treatment/create`

### URL Parameters

Parameter | Description
--------- | -----------
userId | The ID of the user to create the treatment for.


## Start treatment

```shell
curl "http://sal.vio/api/treatment/activate"
  -X POST
  -H "Token: [your_oauth2_token]"
  --data "treatmentId=1"
```

> The above command returns JSON structured like this:

```json
{
  "status": "OK"
}
```

This endpoint ensures that a treatment is flagged as active in Salvio.

### HTTP Request

`PUT http://salv.io/api/treatment/activate`

### URL Parameters

Parameter | Description
--------- | -----------
treatmentId | The ID of the treatment to activate

## Set treatment progress

```shell
curl "http://sal.vio/api/treatment/progress"
  -X POST
  -H "Token: [your_oauth2_token]"
  --data "treatmentId=1&progressNumerator=5&progressDenominator=10"
```

> The above command returns JSON structured like this:

```json
{
  "status": "OK"
}
```

This endpoint updates the progress of a given treatment.

### HTTP Request

`PUT http://salv.io/api/treatment/progress`

### URL Parameters

Parameter | Description
--------- | -----------
treatmentId | The ID of the treatment to insert data to
dataNumerator | The numerator of the percentile fraction
dataDenominator | The denominator of the percentile fraction
dataTime | The time that data was collected (format: YYYY-MM-DD HH:MM:SS)


## Insert treatment data

```shell
curl "http://sal.vio/api/treatment/percentile"
  -X PUT
  -H "Token: [your_oauth2_token]"
  --data "treatmentId=1&dataNumerator=2&dataDenominator=6&dataTime=2018-03-03 10:33:33"
```

> The above command returns JSON structured like this:

```json
{
  "status": "OK"
}
```

This endpoint inserts percentile treatment data into the relative treatment set.

### HTTP Request

`PUT http://salv.io/api/treatment/percentile`

### URL Parameters

Parameter | Description
--------- | -----------
treatmentId | The ID of the treatment to insert data to
dataNumerator | The numerator of the percentile fraction
dataDenominator | The denominator of the percentile fraction
dataTime | The time that data was collected (format: YYYY-MM-DD HH:MM:SS)


## End treatment

```shell
curl "http://sal.vio/api/treatment/deactivate"
  -X POST
  -H "Token: [your_oauth2_token]"
  --data "treatmentId=1"
```

> The above command returns JSON structured like this:

```json
{
  "status": "OK"
}
```

This endpoint ensures that a treatment is flagged as inactive in Salvio.

### HTTP Request

`PUT http://salv.io/api/treatment/deactivate`

### URL Parameters

Parameter | Description
--------- | -----------
treatmentId | The ID of the treatment to deactivate


