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
--------- | ------ |-----------
id | integer |The of the user to retrieve

<aside class="success">
Remember — need authenticated user!
</aside>


# Uses

Uses is an API allowing update feedback of an use.


## Patch a Specific Use

> Request

```json
  {
    "id": 2,
    "feedback": "like"
  }
```


This endpoint updates a specific use.


### HTTPS Request

`Patch https://app.cforgood.com/api/v1/uses`

### Parameters

Parameter | Format | Description
--------- | ------ | -----------
id | interger |The id of the use to update
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
    "id": 2,
    "name": "Label Terre",
    "picture": "http://...",
    "category_id": 9,
    "like": 63,
    "addresses":
    [
      {
        "i":2,
        "latitude": 44.8420852,
        "longitude": -0.5824325
      },
      {
        "i":3,
        "latitude": 44.8420852,
        "longitude": -0.5824325
      }
    ],
    "perks":
    [
      {
        "id": 10,
        "name": "Un cookie offert",
        "flash": false,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/v1468850769/production/webo2yeqaojpin7jgkpt.jpg",
        "offer": "Offert"
      }
    ]
  },
  {
    "id": 3,
    "name": "Nature et potager en ville",
    "picture": "http://...",
    "category_id": 7,
    "like": 22,
    "addresses":
    [
      {
        "id": 4,
        "latitude": 44.8420852,
        "longitude": -0.5824325
      }
    ],
    "perks":
    [
      {
        "id": 64,
        "name": "1 atelier pour 1 mini-potager :-)",
        "flash": false,
        "picture": "",
        "offer": "Offert"
      },
      {
        "id": 65,
        "name": "-50% ATELIER CRéATION MINI-POTAGER☻",
        "flash": false,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/v1468850748/production/ojbmbpjvq6nk57xfk7gj.jpg",
        "offer": "-50%"
      },
      {
        "id": 66,
        "name": "Qu'est ce qu'on S'ÈME !",
        "flash": false,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/v1468850767/production/xzgcgy3rdaothu2okcjt.jpg",
        "offer": "-10%"
      }
    ]
  }
]
```

This endpoint retrieves businesses with online shop or bot.

### HTTP Request

`GET https://app.cforgood.com/api/v1/businesses?online=true`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
online | false | true : online businesses are return
 | | false : only shop and itinerant businesses are selected

<aside class="success">
Remember — need authenticated user!
</aside>

## Get a Specific Business


> The above command returns JSON structured like this:

```json
{
  "id": 36,
  "name": "Nature et potager en ville",
  "url": "http://www.natureetpotagerenville.fr/",
  "telephone": "0 609 725 765",
  "email": "contact@natureetpotagerenville.fr",
  "description": "Cultivez la biodiversité en ville en jardinant 100% éco-responsable ! Aménagements comestibles & Agriculture urbaine Mini-potagers - Semences bio - Arrosage économe&autonome - Vermicompost - Sac de culture en géotextile ",
  "business_category_id": 5,
  "facebook"  : "natureetpotagerenville/?fref=ts",
  "twitter": "",
  "instagram": "",
  "leader_first_name": "Marie-Dominique",
  "leader_last_name": "Pivetaud",
  "leader_description": "",
  "online": false,
  "shop": true,
  "itinerant": true,
  "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1468850474/production/aysgflagktkv5hk0j1jv.jpg",
  "leader_picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_100,w_100/v1468850578/production/x3xbk1elnn8po8uge97z.jpg",
  "like": 0,
  "unlike": 0,
  "link_video": null,
  "addresses": {
    "id": 4,
    "street": "87, quai des Queyries",
    "zipcode": "33000",
    "city": "Bordeaux",
    "latitude": 44.8420852,
    "longitude": -0.5824325
  },
  "perks":
  [
    {
      "id": 64,
      "name": " 1 atelier pour 1 mini-potager :-)",
      "description": "Parmi 4 formats on vous offre une réduction proportionnelle sur 1 atelier de jardinage de 50€: Format 12L - 20% de réduc, Format 19L -30% de réduc, Format 26L -40% de réduc et Format 41L -50% de réduc ",
      "times": 0,
      "start_date": null,
      "end_date": null,
      "active": false,
      "perk_code": "UBDQ3",
      "nb_views": 1,
      "appel": true,
      "durable": false,
      "flash": false,
      "perk_detail_id": 2,
      "all_day": false,
      "picture": "",
      "offer": "Offert"
    },
    {
      "id": 63,
      "name": "-50% ATELIER CRéATION MINI-POTAGER☻",
      "description": "Découvrez - Jardinez - Profitez - 50 % sur un atelier de création d'un mini-potager hors-sol Venez créer votre mini écosystème grâce à notre savoir-faire ! Contactez-nous pour nous donner vos disponibilités.",
      "times": 0,
      "start_date": null,
      "end_date": null,
      "active": true,
      "perk_code": "DYWI6",
      "nb_views": 105,
      "appel": true,
      "durable": false,
      "flash": false,
      "perk_detail_id": 2,
      "all_day": false,
      "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1468850748/production/ojbmbpjvq6nk57xfk7gj.jpg",
      "offer": "-50%"
    },
    {
      "id": 62,
      "name": "Qu'est ce qu'on S'ÈME !",
      "business_id": 36,
      "description": "Préparez votre mini-potager pour l'été ! ☀ - 10 % sur la Mâche, Tournesol Nain Jaune et Tomate Lime Green Présentez votre carte au marché pour en profiter ;-)",
      "times": 25,
      "start_date": "2016-03-15T00:00:00+01:00",
      "end_date": "2016-03-28T23:00:00+02:00",
      "active": false,
      "perk_code": "WPOS1",
      "nb_views": 15,
      "appel": false,
      "durable": false,
      "flash": true,
      "perk_detail_id": 1,
      "all_day": false,
      "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_600,w_800/v1468850767/production/xzgcgy3rdaothu2okcjt.jpg",
      "offer": "-10%"
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
id | interger | The id of the business to retrieve
address_id | integer | The id of the business address



### Perk Detail

This is the way the park can be used

Parameter | Description
--------- | -----------
1 | Carte : Show member card at the shop
2 | Email : Send an email
3 | Online : Connect to the service (websebsite)


<aside class="success">
Remember — need authenticated user!
</aside>

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

