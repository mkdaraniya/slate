---
title : FOCUS

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - php: PHP

search: true
---

#Introduction

Welcome to the Focus API! You can use our API to access Focus API endpoints.

In this section we’ll go over the elements that make up the eCommerce system, and how you can start integrating with the FOCUS API.

Our API is REST-based. This means:

1. It make use of standard HTTP verbs like GET, POST, DELETE.
2. The API uses standard HTTP error responses(status codes) to indicate status of your requests – success and error codes.
3. Authentication is specified with HTTP Basic Authentication.

#Environment
Each FOCUS collection will have it's environment set up.

Each environment has following components</br>
Base URL - Base URL where the API is hosted</br>
Authentication Token - A unique Authentication Token for each environment

Set up the below headers exactly for all requests. Only JSON requests will be accepted

### Request Headers

Header     |   Sample Value   |   Description
--------   |   ------------   |   -----------
Token | {token} | Authentication Token
Content-Type | application/json | JSON request

<aside class="notice">
Note: You must replace <token> with your personal API Token.
</aside>


#Configuration

Configuration apis use to basic mobile app home, category, search related apis.

## Get Groups

Get Groups API is used to fetch list of all Websites, Stores and Languages

> Definition

```php

$request = new HttpRequest();
$request->setUrl('{Base URL}/connector/config/get_groups');
$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Token' => 'fjswe98w9wjkd23jsd23'
));

```

```shell 

curl -X GET \
  {Base URL}/connector/config/get_groups \
  -H 'Content-Type: application/json' \
  -H 'Token: fjswe98w9wjkd23jsd23' \
  
```

Request :
<span class="post">GET</span><span class="prettyprint">{Base URL}/connector/config/get_groups</span>

> Response 

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "group_id": "1",
            "website_id": "1",
            "name": "KSA",
            "root_category_id": "2",
            "default_store_id": "1",
            "country_flag": "http://shop.arabianoud.com/focus/flag/sa.png",
            "is_selected": "1",
            "storeviews": [
                {
                    "store_id": "2",
                    "code": "ksa_ar",
                    "website_id": "1",
                    "group_id": "1",
                    "name": "العربية",
                    "sort_order": "0",
                    "is_active": "1",
                    "use_store": "0",
                    "lang_flag": "http://shop.arabianoud.com/focus/flag/ar.png"
                },
                {
                    "store_id": "1",
                    "code": "ksa_en",
                    "website_id": "1",
                    "group_id": "1",
                    "name": "English",
                    "sort_order": "0",
                    "is_active": "1",
                    "use_store": "0",
                    "lang_flag": "http://shop.arabianoud.com/focus/flag/en.png"
                }
            ]
        }
    ]
}
```

## Get store view

Get Store View is used to Set the store view. For e.g. Set store view as 
{KSA and English} or {UAE and Arabic}

> Definition

```
{Base URL}/connector/config/get_store_view
```

> Request Body

```php
$request->setBody('{
  "store_id":1
}');

```

```curl
  -d '{
  "store_id":1
}'
```

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "store_config": {
                "country_code": "SA",
                "country_name": "Saudi Arabia",
                "locale_identifier": "en_US",
                "currency_symbol": null,
                "currency_code": "SAR",
                "store_id": "1",
                "store_name": "English"
            },
            "category_version": "v556",
            "algolia": {
                "search_index": "ksa_en_products",
                "currency": "SAR"
            },
            "theme_version": "674",
            "sorting_options": [
                {
                    "title": "None",
                    "value": 0
                },
                {
                    "title": "Name : A To Z",
                    "value": 3
                },
                {
                    "title": "Name : Z To A",
                    "value": 4
                },
                {
                    "title": "Price : Low To High",
                    "value": 1
                },
                {
                    "title": "Price : High To Low",
                    "value": 2
                }
            ],
            "offers": {
                "offer_version": "v"
            }
        }
    ]
}
```

###Request
<span class="post">POST</span><span class="prettyprint">{Base URL}/connector/config/get_store_view</span>

###Request Parameter

Parameter | Data Type | Length | Required | Description
--------- | --------- | ------ | -------- | -----------
store_id | Integer | 32 | Mandatory | Store id associated with the website. 
 
 
#Catalog

List of product apis.

> Definition

```
{Base URL}/connector/config/get_home_dataV2
```

##Get Home Data
 
Get Home Data is an independent API which renders the content for Home page. Home page has many different sections and the data for all these are segregated into pre-defined components.
Based on the request, the content of these components is just merged and provided in this API

For e.g. a Home screen can have components like:

1) Header Banner </br>
2) Trending category</br>
3) Category List</br>
4) Seasonal products</br>
5) Trending products</br>
6) Best Seller products</br>

> Request

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "{Base URL}/connector/config/get_home_dataV2",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_http_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "{ \"limit\":7, \"offset\":0, \"store_id\":1 }",
  CURLOPT_HTTPHEADER => array(
    "Content-Type: application/json",
    "Token: fjswe98w9wjkd23jsd23",
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}

```

```curl
   curl -X POST \
     {Base URL}/connector/config/get_home_dataV2 \
     -H 'Content-Type: application/json' \
     -H 'Token: fjswe98w9wjkd23jsd23' \
     -d '{ "limit":7, "offset":0, "store_id":1 }'
}'
```

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "type": "banners",
            "data": {
                "aspectRatio": 1.13,
                "title": "banner1",
                "NumberernalItemAspectratio": 1,
                "welcomeImage": "http://52.77.143.184/focus/home/images/banner.png",
                "type": "fullwidth",
                "items": [
                    {
                        "image_url": "http://52.77.143.184/media/focus/focus/banner/1/AO_99_SAR_banner_-_English.png",
                        "redirection_url": "arabianoud://products?category_id=93"
                    },
                    {
                        "image_url": "http://52.77.143.184/media/focus/focus/banner/1/WOW_offers_-_English.png",
                        "redirection_url": null
                    }
                ]
            }
        },
        {
            "type": "categories",
            "data": {
                "aspectRatio": 1.13,
                "title": "products",
                "NumberernalItemAspectratio": 1,
                "welcomeImage": "http://52.77.143.184/focus/home/images/banner.png",
                "type": "horizontallist",
                "items": [
                    {
                        "category_name": null,
                        "category_id": "87",
                        "category_image": null,
                        "image_thumbnail": null,
                        "children": [],
                        "products": []
                    },
                    {
                        "category_name": "العود والبخور",
                        "category_id": "34",
                        "category_image": "http://52.77.143.184/media/catalog/category/oud_incense_1.jpg",
                        "image_thumbnail": "http://52.77.143.184/media/catalog/category/oud.png",
                        "children": [],
                        "products": []
                    }
                ]
            }
        },
        {
            "type": "categories",
            "data": {
                "aspectRatio": 1.13,
                "title": "categories",
                "NumberernalItemAspectratio": 1,
                "welcomeImage": "http://52.77.143.184/focus/home/images/banner.png",
                "type": "complex_grid",
                "items": [
                    {
                        "category_name": "عطور",
                        "category_id": "32",
                        "category_image": "http://52.77.143.184/media/catalog/category/perfumes_1.jpg",
                        "image_thumbnail": "http://52.77.143.184/media/catalog/category/perfume.png",
                        "children": [
                            {
                                "category_name": "عطور للرجال",
                                "category_id": "27",
                                "category_image": "http://52.77.143.184/media/catalog/category/Artboard_73.png",
                                "image_thumbnail": null,
                                "children": null,
                                "products": []
                            }
                        ]
                    },
                    {
                        "category_name": "العود والبخور",
                        "category_id": "34",
                        "category_image": "http://52.77.143.184/media/catalog/category/oud_incense_1.jpg",
                        "image_thumbnail": "http://52.77.143.184/media/catalog/category/oud.png",
                        "children": [
                            {
                                "category_name": "العود",
                                "category_id": "36",
                                "category_image": "http://52.77.143.184/media/catalog/category/Artboard_81.png",
                                "image_thumbnail": null,
                                "children": null,
                                "products": []
                            }
                        ]
                    },
                    {
                        "category_name": "شنط واكسسورات",
                        "category_id": "44",
                        "category_image": "http://52.77.143.184/media/catalog/category/gifts_accessories_1.jpg",
                        "image_thumbnail": "http://52.77.143.184/media/catalog/category/gift.png",
                        "children": null
                    },
                    {
                        "category_name": " زيوت عطرية",
                        "category_id": "35",
                        "category_image": "http://52.77.143.184/media/catalog/category/oil_perfumes_1.jpg",
                        "image_thumbnail": "http://52.77.143.184/media/catalog/category/oil.png",
                        "children": [
                            {
                                "category_name": "دهن العود ",
                                "category_id": "7",
                                "category_image": "http://52.77.143.184/media/catalog/category/Artboard_88.png",
                                "image_thumbnail": null,
                                "children": null,
                                "products": []
                            }
                        ]
                    },
                    {
                        "category_name": "منتجات حصرية",
                        "category_id": "61",
                        "category_image": "http://52.77.143.184/media/catalog/category/Exclusives_Banner_1_.png",
                        "image_thumbnail": "http://52.77.143.184/media/catalog/category/exclusive_1.png",
                        "children": null
                    }
                ]
            }
        },
        {
            "type": "category",
            "data": {
                "aspectRatio": 1.13,
                "title": "category",
                "NumberernalItemAspectratio": 1,
                "welcomeImage": "http://52.77.143.184/focus/home/images/banner.png",
                "type": "horizontallistwithproducts",
                "items": [
                    {
                        "category_name": "منتجات حصرية",
                        "category_id": "61",
                        "category_image": "http://52.77.143.184/media/catalog/category/Exclusives_Banner_1_.png",
                        "image_thumbnail": "http://52.77.143.184/media/catalog/category/exclusive_1.png",
                        "children": [],
                        "products": [
                            {
                                "product_id": "791",
                                "product_name": "حياتي، 100 مل",
                                "product_type": "بخاخ",
                                "type": "simple",
                                "product_regular_price": 113.4,
                                "product_price": 40.5,
                                "product_rate": 0,
                                "discount_percentage": 64,
                                "stock_status": false,
                                "product_review_number": 0,
                                "product_image": "http://52.77.143.184/media/catalog/product/cache/5/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/images/catalog/product/placeholder/thumbnail.jpg",
                                "manufacturer_name": "",
                                "brand": ""
                            },
                            {
                                "product_id": "1188",
                                "product_name": "مجموعة سحر الكلمات و غرام بخاخ",
                                "product_type": "بخاخ",
                                "type": "simple",
                                "product_regular_price": 232.2,
                                "product_price": 86.4,
                                "product_rate": 0,
                                "discount_percentage": 63,
                                "stock_status": false,
                                "product_review_number": 0,
                                "product_image": "http://52.77.143.184/media/catalog/product/cache/5/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/images/catalog/product/placeholder/thumbnail.jpg",
                                "manufacturer_name": "",
                                "brand": ""
                            }
                        ]
                    }
                ]
            }
        },
        {
            "type": "products",
            "data": {
                "aspectRatio": 1.13,
                "title": "products",
                "NumberernalItemAspectratio": 1,
                "welcomeImage": "http://52.77.143.184/focus/home/images/banner.png",
                "type": "carousellist",
                "items": [
                    {
                        "product_id": "1268",
                        "product_sku": "Test1",
                        "product_name": "Test1",
                        "product_type": "دهن عود",
                        "product_regular_price": 32.4,
                        "product_price": 16.2,
                        "discount_percentage": 50,
                        "product_rate": 0,
                        "stock_status": true,
                        "product_review_number": 0,
                        "product_image": null,
                        "manufacturer_name": "Itcan",
                        "brand": " "
                    },
                    {
                        "product_id": "1267",
                        "product_sku": "Test124",
                        "product_name": "Test",
                        "product_type": "دهن عود",
                        "product_regular_price": 32.4,
                        "product_price": 16.2,
                        "discount_percentage": 50,
                        "product_rate": 0,
                        "stock_status": true,
                        "product_review_number": 0,
                        "product_image": null,
                        "manufacturer_name": "Itcan",
                        "brand": " "
                    }
                ]
            }
        },
        {
            "type": "banners",
            "data": {
                "aspectRatio": 1.13,
                "title": "banner",
                "NumberernalItemAspectratio": 1,
                "welcomeImage": "http://52.77.143.184/focus/home/images/banner.png",
                "type": "fullwidth",
                "items": [
                    {
                        "image_url": "http://52.77.143.184/media/focus/focus/banner/1/AO_99_SAR_banner_-_English.png",
                        "redirection_url": "arabianoud://products?category_id=93"
                    },
                    {
                        "image_url": "http://52.77.143.184/media/focus/focus/banner/1/WOW_offers_-_English.png",
                        "redirection_url": null
                    }
                ]
            }
        },
        {
            "type": "products",
            "data": {
                "title": "products",
                "aspectRatio": 1.13,
                "NumberernalItemAspectratio": 1,
                "welcomeImage": "http://52.77.143.184/focus/home/images/banner.png",
                "type": "grid",
                "items": [
                    {
                        "product_id": "784",
                        "product_sku": "301020398",
                        "product_name": "جنتل مان سيكريت، 100 مل",
                        "product_type": "بخاخ",
                        "product_regular_price": 78.3,
                        "product_price": 24.3,
                        "discount_percentage": 69,
                        "product_rate": 0,
                        "stock_status": false,
                        "product_review_number": 0,
                        "product_image": null,
                        "manufacturer_name": "Itcan",
                        "brand": " "
                    },
                    {
                        "product_id": "1201",
                        "product_sku": "301020435",
                        "product_name": "رويال بلو ، 100 مل ",
                        "product_type": "بخاخ",
                        "product_regular_price": 102.6,
                        "product_price": 26.73,
                        "discount_percentage": 74,
                        "product_rate": 0,
                        "stock_status": false,
                        "product_review_number": 0,
                        "product_image": null,
                        "manufacturer_name": "Itcan",
                        "brand": " "
                    }
                ]
            }
        }
    ]
}
```

###Request

<span class="post">POST</span><span class="prettyprint">{Base URL}/connector/config/get_home_dataV2</span>

 
###Request Parameters
 
Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
limit | Int | 0-7 | Mandatory | 0-7 types of screen data
offset | Int | 0-6 | Mandatory | Set first Screen example : Trending product you display first then you set "offset":1
store_id | Int | 2 | Mandatory | Set store id
 

##Get Products

This is one of the most important and most used API's
It is a multipurpose api as it performs:</br></br>
1> Fetches all products for a particular category</br>
2> Fetches all products based on a search keyword</br>
3> Apply sort on the requested products</br>
4> Apply Filter on the requested products</br>

> Definition

```
{Base URL}/connector/catalog/get_all_productsV2
```

###Request

<span class="post">POST</span><span class="prettyprint">{Base URL}/connector/catalog/get_all_productsV2</span>

> Request Body Without Filter

```php
    $request->setBody('{
      "category_id":32,
      "offset":0,
      "limit":10,
      "filter":[] ,
      "width":110,
      "height":110
    }');
```

```curl
     -d '{
     "category_id":32,
     "offset":0,
     "limit":10,
     "filter":[] ,
     "width":110,
     "height":110
   }'
```

> Response Without Filter

```
    "status": "SUCCESS",
        "message": [
            40
        ],
        "data": {
            "products": [
                {
                    "product_id": "80",
                    "product_sku": "3607347336914",
                    "product_name": "Chopard Oud Malaki - Eau de Parfum 80ml",
                    "product_type": "simple",
                    "product_regular_price": 485,
                    "special_price_time_left": 0,
                    "product_price": 485,
                    "product_rate": 0,
                    "discount_percentage": 0,
                    "stock_status": true,
                    "max_qty": 3,
                    "available_quantity": 3,
                    "product_review_number": 0,
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/110x110/040ec09b1e35df139433887a97daa66f/1/7/17.png",
                    "manufacturer_name": "",
                    "brand": "CHOPARD"
                },
                {
                    "product_id": "117",
                    "product_sku": "3386460058728",
                    "product_name": "Mont Blanc Emblem Eau de Toilette",
                    "product_type": "simple",
                    "product_regular_price": 336,
                    "special_price_time_left": 0,
                    "product_price": 336,
                    "product_rate": 0,
                    "discount_percentage": 0,
                    "stock_status": true,
                    "max_qty": 1,
                    "available_quantity": 1,
                    "product_review_number": 0,
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/110x110/040ec09b1e35df139433887a97daa66f/5/4/54.png",
                    "manufacturer_name": "",
                    "brand": "MONT BLANC"
                }
            ],
        },
        "applied_filters": []
    }
```
 
###Request Parameters
 
Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
category_id | Int | 100 | Optional | If Set category id then remove key-word parameter
key_word | String | 100 | Optional | If set key_word parameter then remove category_id
offset | Int | 100 | Mandatory | default '0' , Set product start position
limit | Int | 2 | Mandatory | Set the product list limit 10 to 100
filter | String | 255 | Optional | get-filter api gives list of filters. Set product Filter like price, category etc.
width | Int | 100 | Mandatory | Set product image width
height | Int | 100 | Mandatory | Set product image height



> Request Body With Filter

```php
$request->setBody('{
  "category_id":11,
  "offset":0,
  "limit":10,
  "filter":[{ "key":"price", "value":"15-300" }, {"key":"category","value":["157"]} ] ,
  "width":110,
  "height":110
}');
```

```curl
  -d '{
  "category_id":11,
  "offset":0,
  "limit":10,
  "filter":[{ "key":"price", "value":"15-300" }, {"key":"category","value":["157"]} ] ,
  "width":110,
  "height":110
}'
```

>Response With Filter

```
    {
        "status": "SUCCESS",
        "message": [
            2
        ],
        "data": {
            "products": [
                {
                    "product_id": "325",
                    "product_sku": "8411061081600",
                    "product_name": "Carolina Herrera Chic Eau de Toilette For Men 100m",
                    "product_type": "simple",
                    "product_regular_price": 296,
                    "special_price_time_left": 0,
                    "product_price": 296,
                    "product_rate": 0,
                    "discount_percentage": 0,
                    "stock_status": true,
                    "max_qty": 2,
                    "available_quantity": 2,
                    "product_review_number": 0,
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/110x110/040ec09b1e35df139433887a97daa66f/2/6/266.png",
                    "manufacturer_name": "",
                    "brand": "CAROLINA HERRERA"
                },
                {
                    "product_id": "528",
                    "product_sku": "3607344163773",
                    "product_name": "Davidoff Hot Water Eau de Toilette For Men - 110ml",
                    "product_type": "simple",
                    "product_regular_price": 280,
                    "special_price_time_left": 0,
                    "product_price": 280,
                    "product_rate": 0,
                    "discount_percentage": 0,
                    "stock_status": true,
                    "max_qty": 1,
                    "available_quantity": 1,
                    "product_review_number": 0,
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/110x110/040ec09b1e35df139433887a97daa66f/4/7/474.png",
                    "manufacturer_name": "",
                    "brand": "FENDI"
                }
            ]
        },
        "applied_filters": [
            {
                "key": "price",
                "value": "15-300"
            },
            {
                "key": "category",
                "value": [
                    "157"
                ]
            }
        ]
    }
```


##Get Filters

This Api Gives list of product filters for a specific product collection.
Request for this api is same as the one for previous API - <a href="#get-products">Get All Products</a>.

> Definition

```
{Base URL}/connector/catalog/get_all_filters
```

###Request

<span class="post">POST</span><span class="prettyprint">{Base URL}/connector/catalog/get_all_filters</span>


> Request Body

```php
    $request->setBody('{
      "category_id":4,
      "offset":0,
      "limit":10,
      "filter":[] ,
      "width":110,
      "height":110
    }');
```

```curl
     -d '{
     "category_id":4,
     "offset":0,
     "limit":10,
     "filter":[] ,
     "width":110,
     "height":110
   }'
```
> Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": {
        "filter": [
            {
                "title": "Type",
                "code": "type",
                "type": 4,
                "is_multiselect": true,
                "value": [
                    {
                        "image": "https://shop.arabianoud.com/focus/images/type6.png",
                        "label": "Incense",
                        "id": "20"
                    },
                    {
                        "image": "https://shop.arabianoud.com/focus/images/type4.png",
                        "label": "Spray",
                        "id": "19"
                    }
                ]
            },
            {
                "title": "Origins",
                "code": "origins",
                "type": 5,
                "is_multiselect": true,
                "value": [
                    {
                        "image": "https://shop.arabianoud.com/focus/images/origin1.png",
                        "label": "Mix (Oriental & Western)",
                        "id": "24"
                    },
                    {
                        "image": "https://shop.arabianoud.com/focus/images/origin2.png",
                        "label": "Oriental",
                        "id": "22"
                    },
                    {
                        "image": "https://shop.arabianoud.com/focus/images/origin3.png",
                        "label": "Western",
                        "id": "23"
                    }
                ]
            },
            {
                "title": "Sizes",
                "code": "size",
                "type": 2,
                "is_multiselect": true,
                "value": [
                    {
                        "image": "",
                        "label": "3 FL OZ - 90ml",
                        "id": "33"
                    },
                    {
                        "image": "",
                        "label": "30 ml",
                        "id": "64"
                    },
                    {
                        "image": "",
                        "label": "35 gm",
                        "id": "102"
                    },
                    {
                        "image": "",
                        "label": "95 Ml",
                        "id": "105"
                    },
                    {
                        "image": "",
                        "label": "40 gm",
                        "id": "39"
                    },
                    {
                        "image": "",
                        "label": "50 ml",
                        "id": "61"
                    },
                    {
                        "image": "",
                        "label": "75 ml",
                        "id": "62"
                    },
                    {
                        "image": "",
                        "label": "90 ml",
                        "id": "70"
                    },
                    {
                        "image": "",
                        "label": "100 ml",
                        "id": "59"
                    },
                    {
                        "image": "",
                        "label": "110 ml",
                        "id": "69"
                    },
                    {
                        "image": "",
                        "label": "250 ml",
                        "id": "72"
                    }
                ]
            },
            {
                "title": "Price",
                "code": "price",
                "type": 1,
                "is_multiselect": false,
                "value": [
                    {
                        "min": 0,
                        "max": 600,
                        "id": "0-600"
                    }
                ]
            },
            {
                "title": "Fragrance",
                "code": "fragrance",
                "type": 3,
                "is_multiselect": true,
                "value": [
                    {
                        "image": "",
                        "label": "For Kids",
                        "id": "80"
                    },
                    {
                        "image": "",
                        "label": "For Men",
                        "id": "14"
                    },
                    {
                        "image": "",
                        "label": "For Women",
                        "id": "15"
                    },
                    {
                        "image": "",
                        "label": "Unisex",
                        "id": "16"
                    }
                ]
            }
        ]
    }
}
```

###Request Parameters
 
Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
category_id | Int | 100 | Optional | If Set category id then remove key-word parameter
key_word | String | 100 | Optional | If set key_word parameter then remove category_id
offset | Int | 100 | Mandatory | default '0' , Set product start position
limit | Int | 2 | Mandatory | Set the product list limit 10 to 100
filter | String | 255 | Optional | get-filter api gives list of filters. Set product Filter like price, category etc.
width | Int | 100 | Mandatory | Set product image width
height | Int | 100 | Mandatory | Set product image height


##Get Product Detail

This Api is user to get all details for a specific product. 
It provides all images, meta data, prices and stock for a product.

For a configurable product, it also provides all data for it's associated products

###Request

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/catalog/get_product_detail</span>

> Definition

```
{Base URL}/connector/catalog/get_product_detail
```

> Request Body

```php
    $request->setBody('{
      "product_id":789
    }');
```

```curl
    -d '{
      "product_id":789
    }'
```
 
###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
product_id | Int | 100 | Mandatory | Set product id

> Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "product_id": 789,
            "product_name": "Lara, 100 ml",
            "product_type": "Spray",
            "type": "simple",
            "product_regular_price": 200,
            "product_price": 200,
            "special_price_start_date": "2017-09-22 00:00:00",
            "special_price_end_date": "",
            "product_description": "<p>\r\nLara by Arabian Oud is a Floral fragrance for unisex. A new and distinct language in the world of perfumes that represents you in an elegant and wonderful way. \r\nOnce you apply Lara by Arabian Oud you will notice a lingering quality of warmer and softer hints that hide an essence of elegant and calming feelings.\r\nWith the unique mixture of the floral fresh flowers, Lilies of the valley, Musk, Chocolate and Litchi<br/> \r\n</p>",
            "product_short_description": "<p>\r\nLara by Arabian Oud is a Floral fragrance for unisex. A new and distinct language in the world of perfumes that represents you in an elegant and wonderful way. \r\nOnce you apply Lara by Arabian Oud you will notice a lingering quality of warmer and softer hints that hide an essence of elegant and calming feelings.\r\nWith the unique mixture of the floral fresh flowers, Lilies of the valley, Musk, Chocolate and Litchi<br/> \r\n</p>",
            "product_sku": "301020107",
            "discount_percentage": 0,
            "max_qty": 10,
            "product_rate": 5,
            "product_images": [
                "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020107_4.png",
                "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020107-1_4.png",
                "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020107-2_4.png"
            ],
            "product_image": "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020107-2_4.png",
            "manufacturer_name": "",
            "brand": "",
            "product_review_number": 1,
            "star_number_5": 1,
            "star_number_4": 0,
            "star_number_3": 0,
            "star_number_2": 0,
            "star_number_1": 0,
            "stock_status": true,
            "configurable_attribute": "",
            "options": [],
            "review": [
                {
                    "review_id": "4519",
                    "customer_name": "lara",
                    "review_title": "",
                    "review_body": "love ",
                    "review_time": "2018-05-14 10:37:13",
                    "rate_point": 5
                },
                {
                    "review_id": "5622",
                    "customer_name": "",
                    "review_title": "",
                    "review_body": "Perfect gift and attractive smell for women",
                    "review_time": "2018-05-02 05:12:27",
                    "rate_point": 0
                },
                {
                    "review_id": "183",
                    "customer_name": "Umar",
                    "review_title": "Good",
                    "review_body": "Good fragrance, and i like the presentation for gifts",
                    "review_time": "2014-07-06 11:26:05",
                    "rate_point": 0
                }
            ],
            "product_attributes": [
                {
                    "title": "Sizes",
                    "value": "100 ml"
                },
                {
                    "title": "Origins",
                    "value": "Mix (Oriental & Western)"
                },
                {
                    "title": "Fragrance",
                    "value": "Unisex"
                },
                {
                    "title": "Type",
                    "value": "Spray"
                }
            ],
            "related_products": [
                {
                    "product_id": "862",
                    "product_name": "Kingdom Mabthoth Incense, 120 gm",
                    "brand": "",
                    "product_image": "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/302010334_4.png",
                    "product_regular_price": 290,
                    "product_price": 290,
                    "discount_percentage": 0,
                    "stock_status": true
                },
                {
                    "product_id": "878",
                    "product_name": "Resala for Unisex, 100 ml",
                    "brand": "",
                    "product_image": "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020426_3.png",
                    "product_regular_price": 480,
                    "product_price": 480,
                    "discount_percentage": 0,
                    "stock_status": true
                }
            ],
            "gift_products": []
        }
    ]
}
```

##Get Product Reviews

This Api is used to get reviews of product. 
Get the list of current product reviews like rate, comment, name etc.

###Request

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/catalog/get_product_review</span>

> Definition

```
{Base URL}/connector/catalog/get_product_review
```

> Request Body

```php
    $request->setBody('{
      "product_id":789,
      "star":0,
      "offset":0,
      "limit":10
    }');

```

```curl
    -d '{
      "product_id":789,
      "star":0,
      "offset":0,
      "limit":10
    }'
```
 
###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
product_id | Int | 100 | Mandatory | Set product id
star | Int | 0-5 | Optional | Default '0', Get specific rate reviews
offset | Int | 100 | Optional | Default '0', Set start review number
limit | Int | 100 | Mandatory | set list of reviews 10 to 100

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": {
        "review": [
            {
                "review_id": "4519",
                "customer_name": "lara",
                "review_title": "",
                "review_body": "love ",
                "review_time": "2018-05-14 10:37:13",
                "rate_point": 5
            },
            {
                "review_id": "5622",
                "customer_name": "",
                "review_title": "",
                "review_body": "Perfect gift and attractive smell for women",
                "review_time": "2018-05-02 05:12:27",
                "rate_point": 4
            },
            {
                "review_id": "183",
                "customer_name": "Umar",
                "review_title": "Good",
                "review_body": "Good fragrance, and i like the presentation for gifts",
                "review_time": "2014-07-06 11:26:05",
                "rate_point": 4
            }
        ],
        "count": {
            "1_star": 0,
            "2_star": 0,
            "3_star": 0,
            "4_star": 2,
            "5_star": 1
        }
    }
}
```


##Set Product Review

This Api is used to set the product review like comment,rate etc.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/catalog/set_product_rate</span>

> Definition

```
{Base URL}/connector/catalog/set_product_rate
```


> Request Body

```php
    $request->setBody('{
      "product_id":677,
      "title":"Great Product now",
      "description":"This best product for me",
      "nickname":"devangi",
      "ratting_star":4,
      "type":"price"
    }');

```

```curl
    -d '{
      "product_id":677,
      "title":"Great Product now",
      "description":"This is best product for me",
      "nickname":"devangi",
      "ratting_star":4,
      "type":"price"
    }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
product_id | Int | 100 | Mandatory | Set product id
title | String | 100 | Mandatory | Set review title
description | String | 255 | Mandatory | Add product review in detail
nickname | Int | 100 | Mandatory | Add name of reviewer
ratting_star | Int | 1-5 |  Mandatory | Set 1 to 5 Ratting Star
type | String | 20 | Mandatory | Set review type this : "price", "quality", "quantity"


>Response

```
{
    "status": "SUCCESS",
    "message": [
        "Your review has been accepted for moderation."
    ],
    "data": []
}
```

#Checkout

Checkout is a collection of API's use to place order on website.

##Add to cart

This api adds one or more products to cart. 
In this api 2 different request: </br>
1) Simple Product </br>
2) Configurable product

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/checkout/add_to_cart_bulk</span>

> Definition

```
{Base URL}/connector/checkout/add_to_cart_bulk
```

> Request Body For Simple Product

```php
    $request->setBody('{
      "products": [
        {
          "product_id": 791,
          "product_qty": 1
        }
      ]
    }');
```

```curl
    -d '{
      "products": [
        {
          "product_id": 791,
          "product_qty": 1
        }
      ]
    }'
```

###Request Parameters For Simple Product

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
product_id | Int | 100 | Mandatory | Set product id
product_qty | Int | 10 | Mandatory | Set Quantity minimum 1 quantity Required


>Response Body For Simple Product

```
    {
        "status": "SUCCESS",
        "message": [
            "SUCCESS"
        ],
        "data": {
            "cart": [
                {
                    "cart_item_id": "2233550",
                    "product_id": "791",
                    "product_sku": "301020261",
                    "stock_status": true,
                    "product_name": "Hayati, 100 ml",
                    "product_type": "Spray",
                    "type": "simple",
                    "product_regular_price": 420,
                    "product_price": 420,
                    "discount_percentage": 0,
                    "brand": "Spray",
                    "product_image": "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020261-2_5.png",
                    "product_qty": 1,
                    "product_max_qty": 10,
                    "options": [],
                    "selected_options": [],
                    "is_gift": false
                }
            ],
            "gift_rules_id": "",
            "is_cart_change": 1,
            "fee": {
                "discount": 0,
                "discount_percentage": "0%",
                "grand_total": 420,
                "sub_total": 420,
                "sub_total_after_discount": 420,
                "subtotal_after_discount": 420,
                "v2": {
                    "subtotal": 420,
                    "grand_total": 420
                },
                "shipping_hand": 0,
                "cod_fee": 0,
                "tax": 0,
                "coupon_code": "",
                "is_coupon_applied": false
            },
            "shipping_hand": 0,
            "cod_fee": 0,
            "items_in_cart": 1,
            "discount": 0,
            "discount_percentage": "0%",
            "coupon_code": "",
            "is_coupon_applied": false,
            "subtotal": 420,
            "sub_total_after_discount": 420,
            "subtotal_after_discount": 420,
            "out_of_stock": [],
            "tax": 0,
            "grand_total": 420
        }
    }
```

>Request Body For Configurable Product

```php
    $request->setBody('{
      "products": [
        {
          "product_id": 225617,
          "product_qty": 1,
           "options":  [
                        {
                            "option_id": "41",
                            "option_value": "#BB3467",
                            "option_price": 0,
                            "option_title": "Color",
                            "position": "0",
                            "option_type_id": "93",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        },{
                            "option_id": "347",
                            "option_value": "1 Tola",
                            "option_price": 0,
                            "option_title": "Size",
                            "position": "0",
                            "option_type_id": "160",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        }
                    ]
                
        }
      ]
    }');
```

```curl
    -d '{
      "products": [
        {
          "product_id": 225617,
          "product_qty": 1,
           "options":  [
                        {
                            "option_id": "41",
                            "option_value": "#BB3467",
                            "option_price": 0,
                            "option_title": "Color",
                            "position": "0",
                            "option_type_id": "93",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        },{
                            "option_id": "347",
                            "option_value": "1 Tola",
                            "option_price": 0,
                            "option_title": "Size",
                            "position": "0",
                            "option_type_id": "160",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        }
                    ]
                
        }
      ]
    }'
```

>Response For Configurable product

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": {
        "cart": [
            {
                "cart_item_id": "32375",
                "product_id": "225617",
                "product_sku": "pp-#BB3467-1 Tola",
                "stock_status": true,
                "product_name": "Pen Pen",
                "product_type": "configurable",
                "product_regular_price": 200,
                "product_price": 200,
                "discount_percentage": 0,
                "brand": " ",
                "product_image": "http://fanos.ae/media/catalog/product/cache/1/image/600x600/9df78eab33525d08d6e5fb8d27136e95/placeholder/default/Group_4685_2x.png",
                "product_qty": 1,
                "product_max_qty": 0,
                "options": {
                    "Color": [
                        {
                            "option_id": "41",
                            "option_value": "#BB3467",
                            "option_price": 0,
                            "option_title": "Color",
                            "position": "0",
                            "option_type_id": "93",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        },
                        {
                            "option_id": "40",
                            "option_value": "#BB3499",
                            "option_price": 0,
                            "option_title": "Color",
                            "position": "0",
                            "option_type_id": "93",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225619"
                            ]
                        }
                    ],
                    "Size": [
                        {
                            "option_id": "347",
                            "option_value": "1 Tola",
                            "option_price": 0,
                            "option_title": "Size",
                            "position": "0",
                            "option_type_id": "160",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        },
                        {
                            "option_id": "351",
                            "option_value": "125 gm",
                            "option_price": 0,
                            "option_title": "Size",
                            "position": "0",
                            "option_type_id": "160",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225619"
                            ]
                        }
                    ]
                },
                "selected_options": {
                    "Color": [
                        {
                            "option_id": "41",
                            "option_value": "#BB3467",
                            "option_price": 0,
                            "option_title": "Color",
                            "position": "0",
                            "option_type_id": "93",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        }
                    ],
                    "Size": [
                        {
                            "option_id": "347",
                            "option_value": "1 Tola",
                            "option_price": 0,
                            "option_title": "Size",
                            "position": "0",
                            "option_type_id": "160",
                            "option_type": "single",
                            "is_required": "YES",
                            "dependence_option_ids": [
                                "225618"
                            ]
                        }
                    ]
                },
                "is_gift": false
            }
        ],
        "fee": {
            "discount": 0,
            "discount_percentage": "0%",
            "grand_total": 200,
            "sub_total": 200,
            "sub_total_after_discount": 200,
            "subtotal_after_discount": 200,
            "shipping_hand": 0,
            "cod_fee": 0,
            "tax": 0,
            "coupon_code": "",
            "is_coupon_applied": false
        },
        "items_in_cart": 1,
        "discount": 0,
        "discount_percentage": "0%",
        "coupon_code": "",
        "is_coupon_applied": false,
        "subtotal": 200,
        "subtotal_after_discount": 200,
        "sub_total_after_discount": 200,
        "cod_fee": 0,
        "shipping_hand": 0,
        "tax": 0,
        "grand_total": 200
    }
}
```


##Get Cart

This Api is used to get the list of cart products.
If product is out of stock then product moved to wishlist.

<code class="post">GET</code>
<span class="prettyprint">{Base URL}/connector/customer/get_cart</span>

> Definition

```
{Base URL}/connector/customer/get_cart
```

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": {
        "cart": [
            {
                "cart_item_id": "1410397",
                "product_id": "791",
                "product_sku": "301020261",
                "stock_status": true,
                "product_name": "Hayati, 100 ml",
                "product_type": "Spray",
                "type": "simple",
                "product_regular_price": 420,
                "product_price": 420,
                "discount_percentage": 0,
                "brand": "Spray",
                "product_max_qty": 10,
                "product_image": "https://dev93.arabianoud.com/media/catalog/product/cache/1/small_image/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020261_5.png",
                "product_qty": 1,
                "options": [],
                "selected_options": [],
                "is_gift": false
            }
        ],
        "out_of_stock": [],
        "fee": {
            "discount": 0,
            "discount_percentage": "0%",
            "grand_total": 420,
            "sub_total": 420,
            "sub_total_after_discount": 420,
            "subtotal_after_discount": 420,
            "v2": {
                "subtotal": 420,
                "grand_total": 420
            },
            "shipping_hand": 0,
            "cod_fee": 0,
            "tax": 0,
            "coupon_code": "",
            "is_coupon_applied": false
        },
        "shipping_hand": 0,
        "cod_fee": 0,
        "items_in_cart": 1,
        "discount": 0,
        "discount_percentage": "0%",
        "coupon_code": "",
        "is_coupon_applied": false,
        "sub_total_after_discount": 420,
        "subtotal_after_discount": 420,
        "subtotal": 420,
        "tax": 0,
        "grand_total": 420
    }
}
```

##Edit Cart [Not in Use]

This Api is for remove product from cart and update quantity.Set **0** value for remove product from cart in **product_qty** parameter.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/checkout/edit_cart</span>

> Definition

```
{Base URL}/connector/checkout/edit_cart
```

>Request Body


```php
$request->setBody('{
      "cart_items": [ 
        {
          "cart_item_id":"1410397",
          "product_qty": 0
      }
    ]  
}');

```

```curl
    -d '{
          "cart_items": [ 
            {
              "cart_item_id":"1410397",
              "product_qty": 0
          }
        ]  
    }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
cart_item_id | Int | 100 | Mandatory | Set cart item id
product_qty | Int | 10 | Mandatory | Set Quantity **0** for remove product


>Response

```
    {
        "status": "SUCCESS",
        "message": [
            "SUCCESS"
        ],
        "data": {
            "cart": [],
            "out_of_stock": [],
            "fee": {
                "discount": 0,
                "discount_percentage": "0%",
                "grand_total": 0,
                "sub_total": 0,
                "sub_total_after_discount": 0,
                "subtotal_after_discount": 0,
                "v2": {
                    "subtotal": 0,
                    "grand_total": 0
                },
                "shipping_hand": 0,
                "cod_fee": 0,
                "tax": 0,
                "coupon_code": "",
                "is_coupon_applied": false
            },
            "shipping_hand": 0,
            "cod_fee": 0,
            "items_in_cart": 0,
            "discount": 0,
            "discount_percentage": "0%",
            "coupon_code": "",
            "is_coupon_applied": false,
            "sub_total_after_discount": 0,
            "subtotal_after_discount": 0,
            "subtotal": 0,
            "tax": 0,
            "grand_total": 0
        }
    }
```


##Get Order Configuration

This api is used to get all order configuration settings like payment method, shipping method, order line items etc.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/checkout/get_order_config</span>

> Definition

```
{Base URL}/connector/checkout/get_order_config
```

>Request Body


```php
$request->setBody('{
  "customer_email":"test.ios@test.com",
  "billingAddress":{
      "name":"Test Test",
      "company":"SW",
      "street":"Test Street",
      "city":"Riyadh",
      "zip":"12222",
      "country_code":"SA",
      "phone":"4512000339"
    },
  "shippingAddress":{
      "prefix":"Mrs",
      "name":"Test Test",
      "company":"SW",
      "street":"Test Street",
      "city":"Riyadh",
      "zip":"12222",
      "country_code":"SA",
      "email":"test.ios@test.com",
      "phone":"4512000339"
    }
}');
```

```curl
    -d '{
      "customer_email":"test.ios@test.com",
      "billingAddress":{
          "name":"Test Test",
          "company":"SW",
          "street":"Test Street",
          "city":"Riyadh",
          "zip":"12222",
          "country_code":"SA",
          "phone":"4512000339"
        },
      "shippingAddress":{
          "prefix":"Mrs",
          "name":"Test Test",
          "company":"SW",
          "street":"Test Street",
          "city":"Riyadh",
          "zip":"12222",
          "country_code":"SA",
          "email":"test.ios@test.com",
          "phone":"4512000339"
        }
    }'
```

>Response

```
    {
        "status": "SUCCESS",
        "message": [
            "Save Success"
        ],
        "data": [
            {
                "fee": {
                    "sub_total": 420,
                    "grand_total": 441,
                    "discount": 0,
                    "tax": 21,
                    "coupon_code": "",
                    "discount_percentage": "0%",
                    "subtotal_after_discount": 420,
                    "sub_total_after_discount": 420,
                    "is_coupon_applied": false,
                    "shipping_hand": 0,
                    "cod_fee": 0,
                    "v2": {
                        "subtotal": 420,
                        "grand_total": 441,
                        "tax": 21
                    },
                    "cache_data": {
                        "sub_total": 420,
                        "grand_total": 441,
                        "discount": 0,
                        "tax": 21,
                        "coupon_code": "",
                        "discount_percentage": "0%",
                        "subtotal_after_discount": 420,
                        "sub_total_after_discount": 420,
                        "is_coupon_applied": false,
                        "shipping_hand": 0,
                        "cod_fee": 0,
                        "v2": {
                            "subtotal": 420,
                            "grand_total": 441,
                            "tax": 21
                        },
                        "condition": []
                    }
                },
                "payment_method_list": [
                    {
                        "content": "",
                        "payment_method": "cashondelivery",
                        "title": "Cash On Delivery",
                        "show_type": 0,
                        "short_description": "",
                        "description": "",
                        "icon_payment": "https://dev93.arabianoud.com/focus/payment_icons/cod.png"
                    },
                    {
                        "content": "",
                        "payment_method": "hyperpay_mobile",
                        "title": "Credit Card",
                        "show_type": 0,
                        "short_description": "",
                        "description": "",
                        "icon_payment": "https://dev93.arabianoud.com/focus/payment_icons/visa.png"
                    }
                ],
                "payment_info": [],
                "order_line_items": [
                    {
                        "product_id": "791",
                        "stock_status": true,
                        "product_name": "Hayati, 100 ml",
                        "product_regular_price": 420,
                        "product_price": 420,
                        "product_image": "https://dev93.arabianoud.com/media/catalog/product/cache/1/small_image/600x600/6b9ffbf72458f4fd2d3cb995d92e8889/3/0/301020261_5.png",
                        "product_qty": 1
                    }
                ],
                "gifting_items": [],
                "shipping_method_list": []
            }
        ]
    }
```



###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
customer_email | String | 100 | Mandatory | Set customer email address
billingAddress | String | 255 | Mandatory | Set billing Address json array
shippingAddress | String | 255 | Mandatory | Set Shipping Address json array
prefix | String | 10 | Mandatory | Set name prefix like **Mr.** , **Mrs**, **Miss**
name | String | 20 | Mandatory | Name of customer
company | String | 50 | Optional | Set company name if company address
street | String | 100 | Mandatory | Set street address
city | String | 30 | Mandatory | Set city name
zip | Int | 10 | Mandatory | Set pin/zip code 
country_code | String | 10 | Mandatory | Set country short code
email | String | 255 | Mandatory | Set customer billing/shipping email address
phone | Number | 10 | Mandatory | Set 10 digit phone number like **1234567890**

##Save Payment Method

This Api is set payment method in current order. List of payment method available in **get-order-config** api response.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/checkout/save_payment_method</span>

> Definition

```
{Base URL}/connector/checkout/save_payment_method
```

>Request Body

```php
$request->setBody('{
 "payment_method":"cashondelivery"
}');
```

```curl
    -d '{
     "payment_method":"cashondelivery"
    }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
payment_method | String | 100 | Mandatory | Set current order payment method like **cashondelivery**

>Response

```
    {
        "status": "SUCCESS",
        "message": [
            "SUCCESS"
        ],
        "data": [
            {
                "fee": {
                    "sub_total": 420,
                    "grand_total": 441,
                    "discount": 0,
                    "tax": 21,
                    "coupon_code": "",
                    "discount_percentage": "0%",
                    "sub_total_after_discount": 420,
                    "subtotal_after_discount": 420,
                    "is_coupon_applied": false,
                    "shipping_hand": 0,
                    "cod_fee": 0,
                    "v2": {
                        "subtotal": 420,
                        "grand_total": 441,
                        "cod_fee": null,
                        "tax": 21,
                        "shipping_hand": 0,
                        "payment_name": "COD",
                        "payment_fee": null
                    }
                },
                "payment_info": {
                }
            }
        ]
    }
```


##Place Order

This api is used to place final order with all details.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/checkout/place_order</span>

> Definition

```
{Base URL}/connector/checkout/place_order
```

>Request Body

```php
$request->setBody('{   
  "customer_email":"test.ios@test.com",
  "payment_method":"cashondelivery"
}');
```

```curl
  -d '{   
  "customer_email":"test.ios@test.com",
  "payment_method":"cashondelivery"
}'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
customer_email | String | 255 | Mandatory | Set Current customer email address
payment_method | String | 100 | Mandatory | Set current order payment method like **cashondelivery**


>Response

```
    {
        "status": "SUCCESS",
        "message": [
            "Thank you for your purchase!"
        ],
        "data": {
            "order_number": "110005955",
            "billing_phone": "3412000339",
            "shipping_phone": "3412000339",
            "payment_method": "cashondelivery",
            "contact_config": {
                "email": "support@arabianoud.com",
                "contact_phone": "8001242030",
                "whatsapp_contact_phone": "966559774497",
                "contact_message": "Please fill the contact form for any queries"
            },
            "order_status": "Waiting for confirmation"
        }
    }
```


#Customer

Customer Api's are used for user login, address, order history etc.

##Registration

API used for user registration

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/customer/register</span>

> Definition

```
{Base URL}/connector/customer/register
```

>Request Body

```php
$request->setBody('{
    "user_prefix": "Mr.",
    "user_email": "tedev@mail.com",
    "user_password": "Pass@1234",
    "user_name": "test dev"
}');
```

```curl
  -d '{
      "user_prefix": "Mr.",
      "user_email": "tedev@mail.com",
      "user_password": "Pass@1234",
      "user_name": "test dev"
  }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
user_prefix | String | 100 | Mandatory | Set prefix like Mr., Miss etc
user_email | String | 255 | Mandatory | Set Your email address
user_password | String | 100 | Mandatory | Set your Password
user_name | String | 255 | Mandatory | Set User name string ex. <first name> <middle name> <last name>


>Response

```
{
    "status": "SUCCESS",
    "message": [
        "Thank you for registering with English store"
    ],
    "data": [
        {
            "user_id": "165",
            "user_prefix": "Mr.",
            "user_name": "test dev",
            "first_name": "test",
            "middle_name": null,
            "last_name": "dev",
            "user_email": "tedev@mail.com",
            "login_type": 2
        }
    ]
}
```

##Sign In

This Api is used to customer login.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/customer/sign_in</span>

> Definition

```
{Base URL}/connector/customer/sign_in
```

>Request Body

```php
$request->setBody('{
  "user_email":"test.ios@test.com",
  "user_password":"Pass@123"
}');
```

```curl
  -d '{
    "user_email":"test.ios@test.com",
    "user_password":"password"
  }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
user_email | String | 255 | Mandatory | Set login email address
user_password | String | 100 | Mandatory | Set login Password


>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "user_id": "12163",
            "user_email": "test.ios@test.com",
            "user_name": "Test Test",
            "user_prefix": "Test Test",
            "first_name": "Test",
            "middle_name": null,
            "last_name": "Test",
            "login_type": "2",
            "user_profile": "http://shop.arabianoud.com/focus/customer/1543491946image:13716",
            "cart_qty": null
        }
    ]
}
```

##Change User

This Api is used for update user current account detail.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/customer/change_user</span>

> Definition

```
{Base URL}/connector/customer/change_user
```

>Request Body

```php
$request->setBody('{
  "user_name":"Test test",
  "user_email":"test.ios@test.com",
  "user_prefix":"Ms"
}');
```

```curl
  -d '{
    "user_name":"Test12 Dev",
    "user_email":"test.ios@test.com",
    "user_prefix":"Ms"
  }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
user_email | String | 255 | Mandatory | Set login email address
user_name | String | 100 | Mandatory | Set user name
user_prefix | String | 20 | Optional | Update prefix
first_name | String | 100 | Optional | Update First name
middle_name | String | 100 | Optional | Update Middle Name
last_name | String | 100 | Optional | Update last name
phone | int | 20 | Optional | Update phone number


>Response

```
{
    "status": "SUCCESS",
    "message": [
        "The account information has been saved."
    ],
    "data": [
        {
            "token": "be8892019f3db1cd3523428ea3cf5c8125:wFw96HtSi4HLUu2EVHCS0eTGwtzDz6jv",
            "user_name": "app1 birds1",
            "user_prefix": "MS",
            "first_name": "app1",
            "middle_name": null,
            "last_name": "birds1",
            "phone": "125646767",
            "user_email": "test.ios@test.com",
            "user_profile": "http://shop.arabianoud.com/focus/customer/1543491946image:13716",
            "login_type": "2",
            "cart_qty": 0
        }
    ]
}
```

##Get Profile

This Api is used to get current user profile detail.

<code class="post">GET</code>
<span class="prettyprint">{Base URL}/connector/customer/get_profile</span>

> Definition

```
{Base URL}/connector/customer/get_profile
```

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "user_id": "121612",
            "user_name": "Test Test",
            "user_prefix": "MS",
            "first_name": "Test",
            "middle_name": null,
            "phone": "3235646767",
            "last_name": "birds1",
            "user_email": "test.ios@test.com",
            "user_profile": "http://shop.arabianoud.com/focus/customer/1543491946image:13716",
            "login_type": "2"
        }
    ]
}
```

##Get User Addresses

This Api is get list of user saved addresses.

<code class="post">GET</code>
<span class="prettyprint">{Base URL}/connector/customer/get_user_addresses</span>

> Definition

```
{Base URL}/connector/customer/get_user_addresses
```

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "address_id": "26627",
            "prefix": null,
            "name": "Test Test",
            "first_name": "Test",
            "last_name": "Test",
            "firstname": "Test",
            "middlename": null,
            "lastname": "Test",
            "street": "New Street",
            "city": "Riyadh",
            "state_name": null,
            "state_id": 0,
            "state_code": null,
            "zip": "12222",
            "country_name": "Saudi Arabia",
            "country_code": "SA",
            "country_flag": "http://shop.arabianoud.com/focus/flag/sa.png",
            "phone": "123456789",
            "address_city_code": "",
            "address_country_code": "+966",
            "country_calling_code": "+966",
            "is_verified": "0",
            "latitude": "0.0000",
            "longitude": "0.0000",
            "address_type": 1,
            "email": "test.ios@test.com",
            "other_title": null
        },
        {
            "address_id": "26713",
            "prefix": null,
            "name": "Test Testing",
            "first_name": "Developers",
            "last_name": "Testing",
            "firstname": "Developers",
            "middlename": null,
            "lastname": "Testing",
            "street": "testing",
            "city": "Makkah",
            "state_name": null,
            "state_id": 0,
            "state_code": null,
            "zip": null,
            "country_name": "Saudi Arabia",
            "country_code": "SA",
            "country_flag": "http://shop.arabianoud.com/focus/flag/sa.png",
            "phone": "812265233",
            "address_city_code": "56",
            "address_country_code": "+966",
            "country_calling_code": "+966",
            "is_verified": "0",
            "latitude": "0.0000",
            "longitude": "0.0000",
            "address_type": 1,
            "email": "test.ios@test.com",
            "other_title": null
        }
    ]
}
```

##Save Address

This api is used to create new address for current login user.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/customer/save_address</span>

> Definition

```
{Base URL}/connector/customer/save_address
```

>Request Body

```php
$request->setBody('{"name":"last new","city":"Jeddah","other_title":"test","street":"test new","address_city_code":"50","last_name":"test","country_code":"SA","first_name":"new","address_type":1,"user_prefix":"Ms.","zip":"8966","phone":"+91505555553","address_country_code":"+91","state_name":"","company":""}
');
```

```curl
  -d '{"name":"last new","city":"Jeddah","other_title":"test","street":"test new","address_city_code":"50","last_name":"test","country_code":"SA","first_name":"new","address_type":1,"user_prefix":"Ms.","zip":"8966","phone":"+91505555553","address_country_code":"+91","state_name":"","company":""}
  '
```

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "firstname": "new",
            "lastname": "test",
            "company": "",
            "street": "test new",
            "city": "Jeddah",
            "region_id": null,
            "region": "",
            "postcode": "8966",
            "country_id": "SA",
            "country_name": null,
            "latitude": null,
            "longitude": null,
            "address_type": 1,
            "telephone": "+91505555553",
            "address_city_code": "",
            "country_calling_code": "+91",
            "fax": "",
            "taxvat": "",
            "prefix": "Ms.",
            "suffix": "",
            "dob": "",
            "gender": "1",
            "month": "",
            "day": "",
            "year": "",
            "email": null,
            "other_title": "test",
            "id": null,
            "first_name": "new",
            "last_name": "test",
            "name": "new test",
            "address_id": "32996",
            "state_name": "",
            "state_code": null,
            "zip": "8966",
            "country_code": "SA",
            "phone": "5555553"
        }
    ]
}
```


###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
name | String | 100 | Mandatory | Set username
city | String | 50 | Mandatory | Set city
other_title | String | 20 | Mandatory | Set Address Title
street | String | 100 | Mandatory | Set Street address
address_city_code | Int | 100 | Mandatory | Set Address city code
last_name | String | 100 | Mandatory | Update last name
country_code | Int | 20 | Mandatory | Update Country code
first_name | String | 100 | Mandatory | Set First name
address_type | Int | 10 | Mandatory | Set address type **'1'** for default address
user_prefix | String | 10 | Optional | Set User prefix like Mr., Mrs etc
zip | Int | 10 | Mandatory | Set zip code
phone | String | 10 | Mandatory | Set phone number
address_country_code | String | 10 | Mandatory | Set country code
state_name | String | 100 | Optional | Set State name
company | String | 100 | Optional | Set company name


##Update Address

This Api is used to update address by address id.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/customer/update_address</span>

> Definition

```
{Base URL}/connector/customer/update_address
```

>Request Body

```php
$request->setBody('{
  "address_id":"27307",
  "street":"asd Doshi"
}');
```

```curl
 -d '{
   "address_id":"27307",
   "street":"asd Doshi"
 }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
address_id | Int | 10 | Mandatory | Set address id
first_name | String | 100 | Optional | Update First name
last_name | String | 100 | Optional | Update last name
street | String | 255 | Optional | Update Street
city | String | 100 | Optional | Update City
country_code | String | 10 | Optional | Update country code
phone | String | 20 | Optional | Update Phone number

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": {
        "address_id": "27307",
        "prefix": null,
        "name": "test testing",
        "first_name": "test",
        "last_name": "testing",
        "firstname": "test",
        "middlename": null,
        "lastname": "testing",
        "street": "asd Doshi",
        "city": "Jeddah",
        "state_name": null,
        "state_id": 0,
        "state_code": null,
        "zip": null,
        "country_name": "Saudi Arabia",
        "country_code": "SA",
        "country_flag": "http://shop.arabianoud.com/focus/flag/sa.png",
        "phone": "5252525255",
        "address_city_code": "",
        "address_country_code": "+966",
        "country_calling_code": "+966",
        "is_verified": "0",
        "latitude": "0.0000",
        "longitude": "0.0000",
        "address_type": 1,
        "email": "test.ios@test.com",
        "other_title": null
    }
}
```

##Get Order History

This Api is get list of current user order history.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/customer/get_order_history</span>

> Definition

```
{Base URL}/connector/customer/get_order_history
```

>Request Body

```php
$request->setBody('{
	"offset":0,
	"limit":10
}');
```

```curl
  -d '{
  	"offset":0,
  	"limit":10
  }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
offset | Int | 10 | Mandatory | Set Default **'0'** offset
limit | Int | 10 | Mandatory | Set order list limit

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "order_id": "100001142",
            "order_status": "Pending",
            "order_date": "2019-02-27 12:16:33",
            "order_date_formatted": "Feb 27, 2019 12:16 PM",
            "order_total": 128.95,
            "recipient": "Test Test",
            "order_items": [
                {
                    "product_name": "Missha BB Cream 27 Honey Beige",
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/7/./7.png",
                    "product_price": "99.0000",
                    "brand": "Missha"
                },
                {
                    "product_name": "عطر كرافيت 30 مل",
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/s/i/single-cup.png",
                    "product_price": "0.0000",
                    "brand": false
                }
            ]
        },
        {
            "order_id": "100001138",
            "order_status": "Pending",
            "order_date": "2019-02-25 10:27:06",
            "order_date_formatted": "Feb 25, 2019 10:27 AM",
            "order_total": 203.5,
            "recipient": "Test Test",
            "order_items": [
                {
                    "product_name": "Laura Mercier Powder",
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/3/3/33.png",
                    "product_price": "170.0000",
                    "brand": "Laura mercier"
                },
                {
                    "product_name": "عطر كرافيت 30 مل",
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/s/i/single-cup.png",
                    "product_price": "0.0000",
                    "brand": false
                }
            ]
        }
    ]
}
```

##Get Order Detail

This Api is get detail of single order by order id.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/customer/get_order_detail</span>

> Definition

```
{Base URL}/connector/customer/get_order_history
```

>Request Body

```php
$request->setBody('{
	"order_id":"100001142"
}');
```

```curl
-d '{
	"order_id":"100001142"
}'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
order_id | Int | 100 | Mandatory | Set order id

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "order_id": "100001142",
            "order_date": "2019-02-27 12:16:33",
            "order_status": "Pending",
            "order_date_formatted": "Feb 27, 2019 12:16 PM",
            "order_code": "100001142",
            "order_total": 128.95,
            "order_subtotal": 99,
            "tax": "4.9500",
            "s_fee": "25.0000",
            "order_gift_code": null,
            "discount": 0,
            "order_note": null,
            "order_items": [
                {
                    "product_id": "70",
                    "product_sku": "8806150614485",
                    "product_name": "Missha BB Cream 27 Honey Beige",
                    "product_price": "99.0000",
                    "product_brand": "MISSHA",
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/7/./7.png",
                    "product_qty": 1,
                    "options": []
                },
                {
                    "product_id": "819",
                    "product_sku": "3333",
                    "product_name": "عطر كرافيت 30 مل",
                    "product_price": "0.0000",
                    "product_brand": "",
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/s/i/single-cup.png",
                    "product_qty": 1,
                    "options": []
                }
            ],
            "payment_method": "Cash On Delivery",
            "shipping_method": "Fetchr - Next Day Delivery",
            "card_4digits": "",
            "track_info": [],
            "shippingAddress": {
                "name": "Test Test",
                "street": "B-17 Rameshwaram",
                "city": "Riyadh",
                "state_name": null,
                "state_code": null,
                "zip": "12222",
                "country_name": "Saudi Arabia",
                "country_code": "SA",
                "country_flag": "http://shop.arabianoud.com/focus/flag/sa.png",
                "phone": "+966123456789",
                "email": "test.ios@test.com"
            },
            "billingAddress": {
                "name": "Test Test",
                "street": "B-17 Rameshwaram",
                "city": "Riyadh",
                "state_name": null,
                "state_code": null,
                "zip": "12222",
                "country_name": "Saudi Arabia",
                "country_code": "SA",
                "country_flag": "http://shop.arabianoud.com/focus/flag/sa.png",
                "phone": "+966123456789",
                "email": "test.ios@test.com"
            }
        }
    ]
}
```

#Wishlist

Using bellow api's user can perform actions like:
</br>
1) Add To Wishlist Product </br>
2) Remove Product from wishlist </br>
3) Product moved Wishlist to cart.


##Get Wishlist Products

This api is used to get all product from current login user wishlist.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/wishlist/get_wishlist_products</span>

> Definition

```
{Base URL}/connector/wishlist/get_wishlist_products
```

>Request Body

```php
$request->setBody('{
  "offset":0,
  "limit":20
}');
```

```curl
  -d '{
  "offset":0,
  "limit":20
}'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
offset | Int | 10 | Mandatory | Set Default **'0'**
limit | Int | 10 | Mandatory | Set product list limit

>Response

```
{
    "status": "SUCCESS",
    "message": [
        2
    ],
    "data": {
        "wishlist_products": [
            {
                "product_id": "791",
                "product_sku": "6297909444545",
                "product_name": "لوكسري 30 مل",
                "product_type": "simple",
                "product_regular_price": 150,
                "product_price": 45,
                "discount_percentage": 70,
                "product_rate": 0,
                "stock_status": true,
                "product_review_number": 0,
                "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/placeholder/default/new8_2.png",
                "manufacturer_name": "",
                "brand": " ",
                "is_show_price": true,
                "wishlist_item_id": "5497",
                "options": [],
                "selected_all_required_options": true,
                "product_qty": "1.0000",
                "available_quantity": 55,
                "product_sharing_message": " http://shop.arabianoud.com/index.php/30-1157.html",
                "product_sharing_url": "http://shop.arabianoud.com/index.php/30-1157.html",
                "show_price_v2": {
                    "product_regular_price": 150,
                    "special_price_label": "Special Price",
                    "product_price": 45
                }
            },
            {
                "product_id": "790",
                "product_sku": "3388714256102",
                "product_name": "inspir me Gold 100ml",
                "product_type": "simple",
                "product_regular_price": 360,
                "product_price": 108,
                "discount_percentage": 70,
                "product_rate": 0,
                "stock_status": true,
                "product_review_number": 0,
                "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/placeholder/default/new8_2.png",
                "manufacturer_name": "",
                "brand": " ",
                "is_show_price": true,
                "wishlist_item_id": "5498",
                "options": [],
                "selected_all_required_options": true,
                "product_qty": "1.0000",
                "available_quantity": 36,
                "product_sharing_message": " http://shop.arabianoud.com/index.php/100-9726.html",
                "product_sharing_url": "http://shop.arabianoud.com/index.php/100-9726.html",
                "show_price_v2": {
                    "product_regular_price": 360,
                    "special_price_label": "Special Price",
                    "product_price": 108
                }
            }
        ],
        "wishlist_info": [
            {
                "wishlist_items_qty": 2,
                "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                "cart_qty": 1,
                "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
            }
        ],
        "other": [
            {
                "wishlist_items_qty": 2,
                "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                "cart_qty": 1,
                "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
            }
        ]
    }
}
```

##Add Product To Wishlist

This Api is used to add product in wishlist.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/wishlist/add_products_to_wishlist</span>

> Definition

```
{Base URL}/connector/wishlist/add_products_to_wishlist
```

>Request Body

```php
$request->setBody('{
  "products":[
    {
      "product_id":790
    }
  ]
}');
```

```curl
-d '{
  "products":[
    {
      "product_id":790
    }
  ]
}'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
product_id | Int | 10 | Mandatory | Set product id

>Response

```
    {
        "status": "SUCCESS",
        "message": [
            2
        ],
        "data": {
            "wishlist_products": [
                {
                    "product_id": "790",
                    "product_sku": "3388714256102",
                    "product_name": "inspir me Gold 100ml",
                    "product_type": "simple",
                    "product_regular_price": 360,
                    "product_price": 108,
                    "discount_percentage": 70,
                    "product_rate": 0,
                    "stock_status": true,
                    "product_review_number": 0,
                    "product_image": "http://shop.arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/placeholder/default/new8_2.png",
                    "manufacturer_name": "",
                    "brand": " ",
                    "is_show_price": true,
                    "wishlist_item_id": "5498",
                    "options": [],
                    "selected_all_required_options": true,
                    "product_qty": "2.0000",
                    "available_quantity": 36,
                    "product_sharing_message": " http://shop.arabianoud.com/index.php/100-9726.html",
                    "product_sharing_url": "http://shop.arabianoud.com/index.php/100-9726.html",
                    "show_price_v2": {
                        "product_regular_price": 360,
                        "special_price_label": "Special Price",
                        "product_price": 108
                    }
                }
            ],
            "wishlist_info": [
                {
                    "wishlist_items_qty": 2,
                    "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                    "cart_qty": 1,
                    "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
                }
            ],
            "other": [
                {
                    "wishlist_items_qty": 2,
                    "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                    "cart_qty": 1,
                    "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
                }
            ]
        }
    }
```

##Remove Product From Wishlist

This Api is used to remove product from wishlist.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/wishlist/remove_product_from_wishlist</span>

> Definition

```
{Base URL}/connector/wishlist/remove_product_from_wishlist
```

>Request Body

```php
$request->setBody('{
  "wishlist_item_id":"5499"
}');
```

```curl
-d '{
  "wishlist_item_id":"5499"
}'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
wishlist_item_id | Int | 10 | Mandatory | Set wishlist item id

>Response

```
    {
        "status": "SUCCESS",
        "message": [
            0
        ],
        "data": {
            "wishlist_products": [],
            "wishlist_info": [
                {
                    "wishlist_items_qty": 0,
                    "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                    "cart_qty": 1,
                    "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
                }
            ],
            "other": [
                {
                    "wishlist_items_qty": 0,
                    "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                    "cart_qty": 1,
                    "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
                }
            ]
        }
    }
```

##Add Wishlist Product To Cart

This Api is used to add product to cart.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/wishlist/add_wishlist_product_to_cart</span>

> Definition

```
{Base URL}/connector/wishlist/add_wishlist_product_to_cart
```

>Request Body

```php
$request->setBody('{
  "wishlist_item_id":"5500"
}');
```

```curl
-d '{
  "wishlist_item_id":"5500"
}'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
wishlist_item_id | Int | 10 | Mandatory | Set wishlist item id

```
{
    "status": "SUCCESS",
    "message": [
        0
    ],
    "data": {
        "wishlist_products": [],
        "wishlist_info": [
            {
                "wishlist_items_qty": 0,
                "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                "cart_qty": 2,
                "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
            }
        ],
        "other": [
            {
                "wishlist_items_qty": 0,
                "sharing_message": " http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/",
                "cart_qty": 2,
                "sharing_url": "http://shop.arabianoud.com/index.php/wishlist/shared/index/code/cfa3f0cfe630657bb9e2eeedf65afc25/"
            }
        ]
    }
}
```


#Fragrance Finder [Use in AO]

Fragrance finder api's are used to find product from different search functionality.

This Fragrance finder api's are used only in **AO**

##Get Refine Fragrance [Use in AO]

This Api is used to get all refine fragrance list.

<code class="post">GET</code>
<span class="prettyprint">{Base URL}/connector/catalog/get_refine_fragrance</span>

> Definition

```
{Base URL}/connector/catalog/get_refine_fragrance
```

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "id": 1,
            "backgroundColor": "#C0009A",
            "title": "SPICES"
        },
        {
            "id": 2,
            "backgroundColor": "#EFE816",
            "title": "CITRUS"
        },
        {
            "id": 3,
            "backgroundColor": "#E8E8E8",
            "title": "FRESH"
        },
        {
            "id": 4,
            "backgroundColor": "#FF8181",
            "title": "FLORAL"
        },
        {
            "id": 5,
            "backgroundColor": "#FFC859",
            "title": "FRUITY"
        },
        {
            "id": 6,
            "backgroundColor": "#00FF97",
            "title": "GREEN"
        },
        {
            "id": 7,
            "backgroundColor": "#97FFF1",
            "title": "MUSK"
        },
        {
            "id": 8,
            "backgroundColor": "#616161",
            "title": "WOODY"
        }
    ]
}
```

##Get Fragrance Note [Use in AO]

This Api is used to get all fragrance note list.

<code class="post">GET</code>
<span class="prettyprint">{Base URL}/connector/catalog/get_fragrance_notes</span>

> Definition

```
{Base URL}/connector/catalog/get_fragrance_notes
```

```
    {
        "status": "SUCCESS",
        "message": [
            "SUCCESS"
        ],
        "data": [
            {
                "id": "MEN",
                "notes": [
                    {
                        "id": 1,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_1.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_1.png",
                        "title": "WOODY"
                    },
                    {
                        "id": 2,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_2.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_2.png",
                        "title": "FRESH"
                    },
                    {
                        "id": 3,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_3.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_3.png",
                        "title": "FLORAL"
                    },
                    {
                        "id": 4,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_4.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_4.png",
                        "title": "ORIENTAL"
                    }
                ]
            },
            {
                "id": "WOMEN",
                "notes": [
                    {
                        "id": 1,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_1.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_1.png",
                        "title": "WOODY"
                    },
                    {
                        "id": 2,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_2.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_2.png",
                        "title": "FRESH"
                    },
                    {
                        "id": 3,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_3.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_3.png",
                        "title": "FLORAL"
                    },
                    {
                        "id": 4,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_4.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_4.png",
                        "title": "ORIENTAL"
                    }
                ]
            },
            {
                "id": "UNISEX",
                "notes": [
                    {
                        "id": 1,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_1.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_1.png",
                        "title": "WOODY"
                    },
                    {
                        "id": 2,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_2.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_2.png",
                        "title": "FRESH"
                    },
                    {
                        "id": 3,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_3.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_3.png",
                        "title": "FLORAL"
                    },
                    {
                        "id": 4,
                        "backgroundImage": "https://shop.arabianoud.com/focus/fragrance/images/notes_4.png",
                        "icon": "https://shop.arabianoud.com/focus/fragrance/images/notes_icon_4.png",
                        "title": "ORIENTAL"
                    }
                ]
            }
        ]
    }
```

##Get Fragrance Finder [Use in AO]

This Api is used to find fragrance product.

<code class="post">POST</code>
<span class="prettyprint">{Base URL}/connector/catalog/get_fragrance_notes</span>

> Definition

```
{Base URL}/connector/catalog/get_fragrance_notes
```

>Request Body

```php
$request->setBody('{ "gender_id":"UNISEX", "fragrance_id":[4], "fragrance_note_id":4 }');
```

```curl
-d '{ "gender_id":"UNISEX", "fragrance_id":[4], "fragrance_note_id":4 }'
```

###Request Parameters

Parameter | DataType | Length | Required | Description
--------- | -------- | ------ | -------- | -----------
gender_id | Int | 10 | Mandatory | Set Gender id: 1) UNISEX 2) MEN 3) WOMEN
fragrance_id | Int | 10 | Mandatory | Set fragrance id using get-refine-fragrance api
fragrance_note_id | Int | 10 | Mandatory | Set fragrance note id using get-fragrance-note api

>Response

```
{
    "status": "SUCCESS",
    "message": [
        "SUCCESS"
    ],
    "data": [
        {
            "product_id": "783",
            "product_name": "Sehr Al Kalemat, 100 ml",
            "product_type": "Spray",
            "type": "simple",
            "product_regular_price": 440,
            "product_price": 440,
            "product_rate": 0,
            "discount_percentage": 0,
            "stock_status": true,
            "product_review_number": 0,
            "product_image": "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/3/0/301020262-2_6.png",
            "manufacturer_name": "",
            "brand": ""
        },
        {
            "product_id": "785",
            "product_name": "Special Nights for Women , 100 ml",
            "product_type": "Spray",
            "type": "simple",
            "product_regular_price": 250,
            "product_price": 80,
            "product_rate": 0,
            "discount_percentage": 68,
            "stock_status": true,
            "product_review_number": 0,
            "product_image": "https://media.cdn-arabianoud.com/media/catalog/product/cache/1/thumbnail/600x600/040ec09b1e35df139433887a97daa66f/3/0/301020148-2_4.png",
            "manufacturer_name": "",
            "brand": ""
        }
        ]
        
    }

```











