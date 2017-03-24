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

This endpoint allow signin user via email and password or facebook access_token.

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

Users is an API allowing retrieve informations about an user and update it.

For information:

- user_member = false -> popup not_member_dashboard
- businesses_around = 0 -> popup no_perks_dashboaard
- uses_without_feedback present(s) -> form feedback_dashboard
- user_trial_done = true
  - si code_partner = [GIFT3MONTH, GIFT6MONTH, GIFT12MONTH] -> popup welcome_member_trial_gift
  - sinon -> popup welcome_member_trial
- first_perk_offer = true - popup first_perk_offer


## Get a Specific User

> The above command returns JSON structured like this:

```json
{
  "id": 127,
  "email": "frederique.petris@gmail.com",
  "first_name": "Fred",
  "last_name": "Pétris",
  "name": "Frédérique Pétris",
  "ambassador": true,
  "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1487241398/tx3rxpmcq7je7he7qsnw.jpg",
  "member": true,
  "trial_done": false,
  "birthday": "1981-01-01T00:00:00+01:00",
  "subscription": "M",
  "amount": 12,
  "street": "Rue Marsan",
  "zipcode": "33300",
  "city": "Bordeaux",
  "code_partner": "GIFT3MONTH",
  "status": "Abonné depuis le 16 mars 2017",
  "logo_member_card": null,
  "cause_attributes": {
    "name": "Ecolo Info",
    "city": "National",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761753/yq5xhyxsbyy9rkxa4h6t.jpg",
    "total_donation": 32.14
  },
  "donation_attributes": [
    {
      "cause_name": "Ecolo Info",
      "created_at": "2017-03-16T16:48:07+01:00",
      "subscription": "M",
      "amount": 45,
      "donation": 37.5
    },
    {
      "cause_name": "Ecolo Info",
      "created_at": "2017-03-16T16:49:28+01:00",
      "subscription": "M",
      "amount": 12,
      "donation": 7
    }
  ],
  "trial_attributes": {
    "date_end_partner": "Mon, 06 Jun 2017 10:27:36 CET +01:00",
    "partner_name": "Cforgood"
  },
  "gift_attributes": {
    "user_offering_first_name": "Mathilde",
    "user_offering_last_name": "Cforgood",
    "nb_month_beneficiary": 3
  },
  "first_perk_offer":
  {
    "business_id": 23,
    "address_id": 41,
    "perk_id": 40
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


## Patch a Specific User

> Request

```json
{
  "user": {
    "email": "allan@cforgood",
    "first_name": "Allan",
    "last_name": "Floury",
    "birthday": "1981-01-01T00:00:00+01:00",
    "subscription": "M",
    "amount": 10,
    "street": "Rue Marsan",
    "zipcode": "33300",
    "city": "Bordeaux",
    "cause_id": 9,
    "picture": "https..."
  }
}
```


This endpoint updates a specific user.
Each field is optional.
If subscription = "X", stop subscription is activated and no other fields will be updated !


### HTTPS Request

`Patch https://app.cforgood.com/api/v1/users/{id}`


### URL Parameters

Parameter | Format | Description
--------- | ------ | -----------
id | integer | The id of the use to update


### Parameters

Parameter | Format | Description
--------- | ------ | -----------
email | email | with @
first_name | string |
last_name | string |
birthday | datetime |
subscription | string | "M" (monthly), "Y" (yearly), "X" (stop subscription)
amount | integer |
code_partner | string |
street | string |
zipcode | string |
city | string |
cause_id | integer | Id of the supported cause
picture | url | Url of  the picture loaded on Cloudinary


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

Once of the feedback is mandatory.

<aside class="success">
Remember — need authenticated user!
</aside>



# BusinessCategories

BusinessCategories is an API allowing retreive all the business categories.

## Get all business categories


> The above command returns JSON structured like this:

```json
[
  {
    "id": 19,
    "name": "Mobilité",
    "color": "#867486",
    "marker_symbol": "marker-mobilite",
    "picture": "business_categories/mobilite"
  },
  {
    "id": 10,
    "name": "Développement personnel",
    "color": "#36d3da",
    "marker_symbol": "marker-developpement",
    "picture": "business_categories/yoga"
  },
  {
    "id": 11,
    "name": "Santé & Fitness",
    "color": "#c386be",
    "marker_symbol": "marker-forme",
    "picture": "business_categories/santeetbienetre.svg"
  }
]
```

This endpoint list all business categories.


### HTTPS Request

`Get https://app.cforgood.com/api/v1/business_categories`


<aside class="success">
Remember — need authenticated user!
</aside>


# Businesses

Businesses is an API allowing retrieve some businesses with their addresses and perks.

## Get Businesses around 10km


> The above command returns JSON structured like this:

```json
[
  {
    "id": 10,
    "name": "La ruche des Chartrons",
    "activity": null,
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761848/xuhtfu5osbuttyhmfx3b.jpg",
    "business_category_id": 12,
    "like": 0,
    "addresses": [
      {
        "id": 28,
        "latitude": 44.8561327,
        "longitude": -0.576172
      }
    ],
    "perks": [
      {
        "id": 13,
        "name": "UN CADEAU DE BIENVENUE ",
        "flash": false,
        "times_remaining": 0,
        "picture": null,
        "offer": "Offert"
      }
    ]
  },
  {
    "id": 6,
    "name": "Origines Tea & Coffee",
    "activity": null,
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761822/cc8ilkgti3avgssyxnrg.jpg",
    "business_category_id": 16,
    "like": 0,
    "addresses": [
      {
        "id": 23,
        "latitude": 44.8518459,
        "longitude": -0.5718565
      }
    ],
    "perks": [
      {
        "id": 7,
        "name": "-50% SUR L'ATELIER DéGUSTATION",
        "flash": false,
        "times_remaining": 0,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761827/jqh5qtvzp2er33wotfyf.jpg",
        "offer": "-50 %"
      },
      {
        "id": 8,
        "name": "RAMENEZ VOS EMBALLAGES !",
        "flash": false,
        "times_remaining": 0,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761828/exqxpb9ngtoqtgnmulay.jpg",
        "offer": "Offert"
      },
      {
        "id": 6,
        "name": "UN THé OFFERT !",
        "flash": false,
        "times_remaining": 0,
        "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761825/uoesswsh288blhxqxgco.jpg",
        "offer": "Offert"
      },
      {
        "id": 35,
        "name": "OFFRE FLASH DU MOMENT à NE PAS MANQ",
        "flash": true,
        "times_remaining": 15,
        "picture": null,
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
      "perk_detail_name": 2,
      "all_day": false,
      "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761814/lhc1bxpwlliscwth3kma.jpg",
      "times_remaining": 0,
      "offer": "Offert",
      "usable_for_user": true
    }
  ]
}
```

This endpoint retrieves a specific business with its perks in detail.
The field "usable_for_user" specifies if the perk is available or unavailable for the user.

### HTTP Request

`GET https://app.cforgood.com/api/v1/businesses/{id}?address_id={address_id}`

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

# Perks

Perks is an API allowing retreive a specific perk.

## Get a specific perk


> The above command returns JSON structured like this:

```json
{
  "id": 13,
  "name": "UN CADEAU DE BIENVENUE ",
  "description": "Pour chaque première commande, un cadeau de bienvenue offert ! ",
  "times": 0,
  "start_date": null,
  "end_date": null,
  "active": true,
  "perk_code": "ZESI7",
  "nb_views": 39,
  "appel": true,
  "durable": false,
  "flash": false,
  "perk_detail_id": 3,
  "perk_detail_name": "carte",
  "all_day": false,
  "picture": null,
  "times_remaining": 0,
  "offer": "Offert",
  "usable_for_user": true
}
```

This endpoint retrieve a specific perk.


### HTTPS Request

`Get https://app.cforgood.com/api/v1/perks/{id}`


### URL Parameters

Parameter | Format | Description
--------- | ------ | -----------
id | integer | The id of the perk to retrieve


<aside class="success">
Remember — need authenticated user!
</aside>



# CauseCategories

CauseCategories is an API allowing retreive all the cause categories.

## Get all cause categories

> The above command returns JSON structured like this:

```json
[
[
  {
    "id": 1,
    "name": "Humanitaire",
    "color": "#ff9e00",
    "picture": {
      "picture": {
        "url": "https://res.cloudinary.com/dktivbech/image/upload/v1479761700/nj0gbkqzoe7gwtnkbw22.png",
        "thumb": {
          "url": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_100,w_100/v1479761700/nj0gbkqzoe7gwtnkbw22.png"
        }
      }
    }
  },
  {
    "id": 2,
    "name": "Culturel",
    "color": "#8e513a)",
    "picture": {
      "picture": {
        "url": "https://res.cloudinary.com/dktivbech/image/upload/v1479761701/quy11yy9oj5emwsx8hah.png",
        "thumb": {
          "url": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_100,w_100/v1479761701/quy11yy9oj5emwsx8hah.png"
        }
      }
    }
  }
]
```

This endpoint list all cause categories.


### HTTPS Request

`Get https://app.cforgood.com/api/v1/cause_categories`


<aside class="success">
Remember — need authenticated user!
</aside>


# Causes

Causes is an API allowing retrieve a list of causes, a specific cause and permit to create a cause.

## Get Some Causes

> The above command returns JSON structured like this:

```json
[
  {
    "id": 9,
    "name": "Surfrider Foundation Europe",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761780/kerdxyjb7uvbqzfhwq0i.jpg",
    "like": 0,
    "city": "Bordeaux"
  },
  {
    "id": 4,
    "name": "Osons Ici et Maintenant",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761735/lxnjjnsgljonbq89oifv.jpg",
    "like": 0,
    "city": "Bègles"
  },
  {
    "id": 2,
    "name": "Etu-Récup",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761717/wvb36vhdecivgmdsixez.jpg",
    "like": 0,
    "city": "Pessac"
  },
  {
    "id": 3,
    "name": "MakeSense",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761726/onvq0xsqiznclyv8y5ou.jpg",
    "like": 0,
    "city": "National"
  },
  {
    "id": 6,
    "name": "Ecolo Info",
    "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761753/yq5xhyxsbyy9rkxa4h6t.jpg",
    "like": 0,
    "city": "National"
  }
]
```

This endpoint retrieves causes, order by distance.

### HTTP Request

`GET https://app.cforgood.com/api/v1/causes?lat={lat}&lng={lng}`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
 lat | latitude | latitude of user position
 lng | longitude | longitude of user position

<aside class="success">
Remember — need authenticated user!
</aside>

## Get a Specific Cause


> The above command returns JSON structured like this:

```json
{
  "id": 5,
  "name": "Keep A Breast Europe",
  "impact": "25€ permettent de financer un atelier éducatif, créatif et ludique pour sensibiliser les 5/11 ans",
  "picture": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_350,w_450/v1479761743/drftnjctv9peeqcjdcq4.jpg",
  "logo": "https://res.cloudinary.com/dktivbech/image/upload/c_fill,dpr_2.0,h_100,w_100/v1479761745/pl56rirwnzuymh6famoh.jpg",
  "like": 0,
  "description": "Créée en 2008, Keep A Breast Foundation Europe est une association à but non lucratif et reconnue d’intérêt général dont la mission est d'apporter aux jeunes du monde entier l'éducation indispensable à la bonne connaissance de l’impact de leur environnement sur leur santé en général et leur poitrine en particulier.",
  "link_video": "https://www.youtube.com/embed/ykB-Ue_i7y8?list=PLzx8g_q3cJgzGmP1aW3evd3XgGmTLOz4q",
  "facebook": "KeepABreastFrance",
  "twitter": "keepabreastEU",
  "instagram": "keepabreasteu",
  "telephone": null,
  "email": "europe@keep-a-breast.org",
  "url": "http://www.keep-a-breast.fr",
  "street": "15, rue Francis Garnier",
  "zipcode": " 33000 ",
  "city": "Bordeaux",
  "representative_first_name": "Keep",
  "representative_last_name": "Breast",
  "representative_testimonial": null,
  "user_cause": false
}
```

This endpoint retrieves a specific cause.

### HTTP Request

`GET https://app.cforgood.com/api/v1/causes/{id}`

### URL Parameters

Parameter | Format | Description
--------- | ------- | -----------
 id | integer | id of the cause to retreive


<aside class="success">
Remember — need authenticated user!
</aside>

## Post a Cause

> Request

```json
{ "cause":
  {
    "civility": 1,
    "representative_first_name": "Keep",
    "representative_last_name": "Breast",
    "email": "europe@keep-a-breast.org",
    "cause_category_id": 2,
    "name": "Keep A Breast Europe",
    "impact": "25€ permettent de financer un atelier éducatif, créatif et ludique pour sensibiliser les 5/11 ans",
    "description": "Créée en 2008, Keep A Breast Foundation Europe est une association à but non lucratif et reconnue d’intérêt général dont la mission est d'apporter aux jeunes du monde entier l'éducation indispensable à la bonne connaissance de l’impact de leur environnement sur leur santé en général et leur poitrine en particulier.",
    "street": "15, rue Francis Garnier",
    "zipcode": "33000",
    "city": "Bordeaux"
  }
}
```

> The above command returns JSON structured like this:

```json
{
  "id": 9
}
```

This endpoint creates a specific cause.

### HTTP Request

`POST https://app.cforgood.com/api/v1/causes`

### Parameters

Parameter | Format | Description
--------- | ------ | -----------
civility | integer | 1 : M
 | | 2 : Mme
representative_first_name | string |
representative_last_name | string |
email | string |
cause_category_id | integer | id of cause category (cf: index cause_categories)
name | string |
impact | string |
description | string |
street | string |
zipcode | string |
city | string |


<aside class="success">
Remember — need authenticated user!
</aside>


<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

