---
title: API Reference

language_tabs:
  - shell
  - ruby
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the CforGood API! You can use our API to access CforGood API <endpoints class=""></endpoints>



# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```ruby
require 'cforgood'

api = Cforgood::APIClient.authorize!('meowmeowmeow')
```

```javascript
const cforgood = require('cforgood');

let api = cforgood.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

<!-- cforgood uses API keys to allow access to the API. You can register a new cforgood API key at our [developer portal](https://app.cforgood.com/developers). -->

cforgood expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Login

Login is an API allowing login user.

There are two different ways to authenticate when performing API requests:

- E-Mail and password
- Oauth Access Token

For information:

- user_member | false | render popup not_member_dashboard
- user_trial_done | true |render popup welcome_memebr_trial (update > trial_done)
- businesses_around | < 0 | render popup o_perks_dashboaard
- uses_without_feedback | > 0 | render form/feedback_dashboard

## Login a Specific User via facebook

```shell
curl "https://app.cforgood.com/api/v1/auth_facebook/<ACCESS_TOKEN>"
  -H "Authorization: meowmeowmeow"
```

```ruby
require 'cforgood'

api = cforgood::APIClient.authorize!('meowmeowmeow')
api.auth_facebook.get(<ACCESS_TOKEN>)
```

```javascript
const cforgood = require('cforgood');

let api = cforgood.authorize('meowmeowmeow');
let max = api.auth_facebook.get(<ACCESS_TOKEN>);
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "",
    "token": ""
  }
]
```

This endpoint retrieves a specific user.


### HTTPS Request

`GET https://app.cforgood.com/api/v1/auth_facebook/<ACCESS_TOKEN>`

### URL Parameters

Parameter | Description
--------- | -----------
ACCES_TOKEN | The ACCESS_TOKEN return by Facebook SDK


## Login a Specific User via email + password

```shell
curl "https://app.cforgood.com/api/v1/login/email=<EMAIL>&password=<PASSWORD>""
  -H "Authorization: meowmeowmeow"
```

```ruby
require 'cforgood'

api = cforgood::APIClient.authorize!('meowmeowmeow')
api.login.get(<EMAIL>, <PASSWORD>)
```

```javascript
const cforgood = require('cforgood');

let api = cforgood.authorize('meowmeowmeow');
let max = api.login.get(<EMAIL>, <PASSWORD>);
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "",
    "token": ""
  }
]
```

This endpoint retrieves a specific user.


### HTTPS Request

`GET https://app.cforgood.com/api/v1/login/email=<EMAIL>&password=<PASSWORD>`

### URL Parameters

Parameter | Description
--------- | -----------
EMAIL | The EMAIL of the user to retrieve
PASSWORD | The PASSWORD of the user to retrieve


# User

User is an API allowing retrieve informations about an user.


## Get a Specific User

```shell
curl "https://app.cforgood.com/api/v1/user/<ID>"
  -H "Authorization: meowmeowmeow"
```

```ruby
require 'cforgood'

api = cforgood::APIClient.authorize!('meowmeowmeow')
api.user.get(<ID>)
```

```javascript
const cforgood = require('cforgood');

let api = cforgood.authorize('meowmeowmeow');
let max = api.user.get(<ID>);
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "",
    "first_name": "",
    "last_name": "",
    "name": "",
    "member": "",
    "trial_done": ""
  }
]
```

This endpoint retrieves a specific user.


### HTTPS Request

`GET https://app.cforgood.com/api/v1/user/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve


# Businesses

Businesses is a simple API allowing user to view businesses ans perks.

## Get All Businesses

```ruby
require 'cforgood'

api = cforgood::APIClient.authorize!('meowmeowmeow')
api.businesses.get
```

```shell
curl "https://app.cforgood.com/api/v1/businesses"
  -H "Authorization: meowmeowmeow"
```

```javascript
const cforgood = require('cforgood');

let api = cforgood.authorize('meowmeowmeow');
let businesses = api.businesses.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 2,
    "name": ""
  },
  {
    "id": 2,
    "name": ""
  }
]
```

This endpoint retrieves all businesses.

### HTTP Request

`GET https://app.cforgood.com/api/v1/businesses`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------


<aside class="success">
Remember — need authenticated user!
</aside>

## Get a Specific business

```ruby
require 'cforgood'

api = cforgood::APIClient.authorize!('meowmeowmeow')
api.businesses.get(<ID>)
```

```shell
curl "https://app.cforgood.com/api/v1/businesses/<ID>"
  -H "Authorization: meowmeowmeow"
```

```javascript
const cforgood = require('cforgood');

let api = cforgood.authorize('meowmeowmeow');
let max = api.businesses.get(<ID>);
```

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

