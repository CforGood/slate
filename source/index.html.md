---
title: API Reference

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the CforGood API! You can use our API to access CforGood API <endpoints class=""></endpoints>


# Authentication


Cforgood expects to be included in all API requests to the server in a header the email and token that looks like the following:

### Request headers

Parameter | Description
--------- | -----------
X-User-Email | "allan@cforgood.com"
X-User-Token | "1G8_s7P-V-4MGojaKD7a"


# Signin

Signin is an API allowing signin user via email and password or facebook access_token.

> Response JSON structured like this:

```json
{
  "id": "2",
  "authentication_token": "ARIDO3557Z0Z0Z"
}
```

### HTTPS Request

`POST https://app.cforgood.com/api/v1/signin`


### Request headers

Parameter | Description
--------- | -----------
email | "allan@cforgood.com"
password | "mot de passe"
access_token | "uid facebbok"


`password` or `access_token` are optional but one of both is mandatory.

If user never signin via facebook, the API return an error `402` to signin once via facebook on the web app.

This endpoint signin a specific user.


# User

User is an API allowing retrieve informations about an user.

For information:

- user_member = false -> popup not_member_dashboard
- user_trial_done = true -> popup welcome_member_trial
- businesses_around < 0 -> popup o_perks_dashboaard
- uses_without_feedback present(s) -> form feedback_dashboard

## Get a Specific User

> The above command returns JSON structured like this:

```json
{
  "id": "2",
  "first_name": "Allan",
  "last_name": "Cforgood",
  "name": "Allan Cforgood",
  "member": "true",
  "trial_done": "false",
  "uses": [
    {
      "id": "10",
      "perk_name": "Un cookie offert",
      "business_name": "Label Terre",
      "created_at": "Mon, 06 Feb 2017 10:27:36 CET +01:00"
    },
     {
      "id": "11",
      "perk_name": "1 ATELIER POUR 1 MINI-POTAGER :-)",
      "business_name": "Nature et potager en ville",
      "created_at": "Mon, 02 Feb 2017 17:20:02 CET +01:00"
    }
  ]
}
```

This endpoint retrieves a specific user.

If perk uses without feedback (like, unlike or unused) present, they are return also.


### HTTPS Request

`GET https://app.cforgood.com/api/v1/user/2`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the user to retrieve

<aside class="success">
Remember — need authenticated user!
</aside>

# Use

Use is an API allowing update feedback of use.


## Patch a Specific Use

> No specific return


This endpoint updates a specific use.


### HTTPS Request

`Patch https://app.cforgood.com/api/v1/use/2/`

### URL Parameters

Parameter | Description
--------- | -----------
id | The id of the use to update
like | True (optional)
unlike | True (optional)
unused | True (optional)

Once of the optional feedback is mandatory.


<aside class="success">
Remember — need authenticated user!
</aside>


# Businesses

Businesses is a simple API allowing retrieve some businesses.

## Get Some Businesses


> The above command returns JSON structured like this:

```json
[
  {
    "id": 2,
    "name": "Label Terre",
    "picture": "http://...",
    "category": "Bar et restaurant",
    "address":
    [
      {
        "id": "2",
        "latitude": ,
        "longitude":
      },
      {
        "id": "3",
        "latitude": ,
        "longitude":
      }
    ]
  },
  {
    "id": 3,
    "name": "Nature et potager en ville",
    "picture": "http://...",
    "category": "Maison et jardin",
    "address":
    [
      {
        "id": "3",
        "latitude": ,
        "longitude":
      }
    ]
  },
]
```

This endpoint retrieves all businesses.

### HTTP Request

`GET https://app.cforgood.com/api/v1/businesses?online=true`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
Online | true | true : online businesses are return
 | | false : only shop and itinerant businesses are selected

<aside class="success">
Remember — need authenticated user!
</aside>

## Get a Specific business


> The above command returns JSON structured like this:

```json
{
  "id": ,
  "name": ""
}
```

This endpoint retrieves a specific business.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://app.cforgood.com/api/v1/businesses/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the business to retrieve

