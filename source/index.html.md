---
title: CforGood API Reference

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
  "id": 2,
  "authentication_token": "ARIDO3557Z0Z0Z"
}
```

### HTTPS Request

`POST https://app.cforgood.com/api/v1/`


### Request headers

Parameter | Description
--------- | -----------
email | "allan@cforgood.com"
password | "mot de passe"
access_token | "uid facebbok"


`password` or `access_token` are optional but one of both is mandatory.

If user never signin via facebook, the API return an error `402` to signin once via facebook on the web app.

This endpoint signin a specific user.


# Users

Users is an API allowing retrieve informations about an user.

For information:

- user_member = false -> popup not_member_dashboard
- businesses_around < 0 -> popup no_perks_dashboaard
- uses_without_feedback present(s) -> form feedback_dashboard
- user_trial_done = true
  - si code_partner = [GIFT3MONTH, GIFT6MONTH, GIFT12MONTH] -> popup welcome_member_trial_gift
  - sinon -> popup welcome_member_trial

## Get a Specific User

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "first_name": "Allan",
  "last_name": "Cforgood",
  "name": "Allan Cforgood",
  "picture": "https://...",
  "member": true,
  "trial_done": false,
  "trial_attributes":
    {
      "date_end_partner": "Mon, 06 Jun 2017 10:27:36 CET +01:00",
      "partner_name": "Cforgood"
    },
  "gift_attributes":
    {
      "code_partner": "GIFT3MONTH",
      "user_offering_first_name": "Mathilde",
      "user_offering_last_name": "Cforgood",
      "nb_month_beneficiary": 3
    },
  "uses_without_feedback": [
    {
      "id": 10,
      "perk_name": "Un cookie offert",
      "business_name": "Label Terre",
      "created_at": "Mon, 06 Feb 2017 10:27:36 CET +01:00"
    },
     {
      "id": 11,
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

`GET https://app.cforgood.com/api/v1/users/{id}`

### URL Parameters

Parameter | Format | Description
--------- | ------ | -----------
id | integer | The id of the user to retrieve

<aside class="success">
Remember — need authenticated user!
</aside>


# Uses

Uses is an API allowing create and update an use.


## Post a New Use

> Request

```json
  { "use":
    {
      "perk_id": "39"
    }
  }
```

> The above command returns JSON structured like this:

```json
  {
    "id": 67
  }
```

This endpoint creates a new use.


### HTTPS Request

`Post https://app.cforgood.com/api/v1/uses`

### Parameters

Parameter | Format | Description
--------- | ------ | -----------
perk_id | integer | The id of the perk to create the corresponding use



<aside class="success">
Remember — need authenticated user!
</aside>


## Patch a Specific Use

> Request

```json
  { "use":
    {
      "feedback": "like"
    }
  }
```


This endpoint updates a specific use.


### HTTPS Request

`Patch https://app.cforgood.com/api/v1/uses/{id}`


### URL Parameters

Parameter | Format | Description
--------- | ------ | -----------
id | integer | The id of the use to update


### Parameters

Parameter | Format | Description
--------- | ------ | -----------
feedback | string | like/unlike/unused

Once of the optional feedback is mandatory.

<aside class="success">
Remember — need authenticated user!
</aside>


# Businesses

Businesses is an API allowing retrieve some businesses with their addresses and perks.

## Get Some Businesses


> The above command returns JSON structured like this:

```json
[
  {
    "id": 7,
    "name": "Maison Hegara",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761830/v66jvtnvzp0cra5apc6u.jpg",
    "business_category_id": 12,
    "like": 0,
    "addresses": [
      {
        "id": 27,
        "latitude": 44.8525244,
        "longitude": -0.5731832
      }
    ],
    "perks": [
      {
        "id": 9,
        "name": "DEUX CONTENANTS OFFERTS ! ",
        "flash": false,
        "picture": null,
        "offer": "Offert"
      }
    ]
  },
  {
    "id": 15,
    "name": "Koken",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761875/rulrjfzylc8yxkqsc6r5.jpg",
    "business_category_id": 13,
    "like": 0,
    "addresses": [
      {
        "id": 32,
        "latitude": 44.8414224,
        "longitude": -0.5755607
      }
    ],
    "perks": [
      {
        "id": 18,
        "name": "BIENVENUE! UN KDO éTHIQUE OFFERT...",
        "flash": false,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761878/sixs97hb7bpio5exlqmk.jpg",
        "offer": "Offert"
      },
      {
        "id": 20,
        "name": "-15% SUR L'ARTICLE DE VOTRE CHOIX..",
        "flash": false,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761882/lh3lqeuomsw8crkyidws.jpg",
        "offer": "Offert"
      }
    ]
  },
  {
    "id": 4,
    "name": "INSPIRESELF",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761809/yfz18ahljkatmdpmsovp.jpg",
    "business_category_id": 10,
    "like": 0,
    "addresses": [
      {
        "id": 20,
        "latitude": 44.839438,
        "longitude": -0.5803727
      },
      {
        "id": 38,
        "latitude": 44.8772685,
        "longitude": -0.554149
      }
    ],
    "perks": [
      {
        "id": 4,
        "name": "25% SUR LE PREMIER PRODUIT ACHETé !",
        "flash": false,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761814/lhc1bxpwlliscwth3kma.jpg",
        "offer": "Offert"
      }
    ]
  }
]
```

This endpoint retrieves businesses with online shop or not, in the 10km around.

### HTTP Request

`GET https://app.cforgood.com/api/v1/businesses?online=true&lat={lat}&lng={lng}`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
online | false | true : online businesses are also return
 | | false : only shop and itinerant businesses are selected
 lat | latitude | latitude of user position or map center
 lng | longitude | longitude of user position or map center

<aside class="success">
Remember — need authenticated user!
</aside>

## Get a Specific Business


> The above command returns JSON structured like this:

```json
{
  "id": 4,
  "name": "INSPIRESELF",
  "activity": "Pour votre inspiration",
  "url": "http://www.inspireself.org/",
  "telephone": "+33663075090",
  "email": "info@inspireself.com",
  "description": "Nous offrons des produits efficaces, réduisant considérablement les effets nocifs (chaleur, maux de têtes, migraines, baisse d'énergie, perte d'équilibre, manque d'ancrage, stress ) générés par les pollutions éléctromagnétiques des téléphones portables, ordinateurs, box wifi, tablettes, montres connectées, DECT, écoutes -bébés, tv en fait tous appareils émettant des ondes éléctromagnétiques de très hautes ou très basses fréquences....",
  "business_category_id": 10,
  "facebook": null,
  "twitter": null,
  "instagram": null,
  "leader_first_name": "Patrice",
  "leader_last_name": "Buyle",
  "leader_description": null,
  "online": true,
  "shop": true,
  "itinerant": true,
  "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761809/yfz18ahljkatmdpmsovp.jpg",
  "leader_picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761810/fphwrhdgl0yh1zty9j2x.jpg",
  "like": 0,
  "unlike": 0,
  "link_video": null,
  "address": {
    "id": 20,
    "street": "rue de la Boétie",
    "zipcode": "33300",
    "city": "Bordeaux",
    "latitude": 44.839438,
    "longitude": -0.5803727,
    "main": true,
    "timetables": [
      {
        "day": "lundi",
        "start_at": "05:00",
        "end_at": "07:00"
      },
      {
        "day": "dimanche",
        "start_at": "15:00",
        "end_at": "19:00"
      }
    ]
  },
  "labels": [
    {
      "name": "Produits éco-responsables",
      "picture": "labels/produits_eco-responsables.svg"
    },
    {
      "name": "Politique anti-gaspillage",
      "picture": "labels/politique_anti-gaspillage.svg"
    }
  ],
  "perks": [
    {
      "id": 4,
      "name": "25% SUR LE PREMIER PRODUIT ACHETé !",
      "description": "Pour vous accueillir en tant que nouveau client, nous vous offrons 25% sur le premier produit acheté :-)",
      "times": 0,
      "start_date": null,
      "end_date": null,
      "active": true,
      "perk_code": "CFORGOOD",
      "nb_views": 2,
      "appel": true,
      "durable": false,
      "flash": false,
      "perk_detail_id": 2,
      "all_day": false,
      "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761814/lhc1bxpwlliscwth3kma.jpg",
      "offer": "Offert"
    }
  ]
}
```

This endpoint retrieves a specific business with its perks in detail.

### HTTP Request

`GET https://app.cforgood.com/api/v1/businesses/{id}&address={address_id}`

### URL Parameters

Parameter | Format | Description
--------- | ------ | -----------
id | integer | The id of the business to retrieve
address_id | integer | The id of the business address



### Perk Detail

This is the way the perk can be used

Parameter | Description
--------- | -----------
1 | Carte : Show member card at the shop
2 | Email : Send an email
3 | Online : Connect to the service (websebsite)


<aside class="success">
Remember — need authenticated user!
</aside>

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

