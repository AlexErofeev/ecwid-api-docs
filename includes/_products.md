## Products

Using the methods below you can search/create/modify/delete products in an Ecwid store. In the [Ecwid Help Center](https://support.ecwid.com/hc/en-us/articles/208078855-Products) you can learn more about the products in Ecwid.

### Search products

Search or filter products in a store catalog. The response provides full details of found products.

<aside class='notice'>
To get products from Store Front Page, specify <strong>&category=0</strong> in your request.
</aside>

#### Request

> Request examples

```http
GET /api/v3/4870020/products?limit=2&keyword=fruit&token=1234567890qwqeertt HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

`GET https://app.ecwid.com/api/v3/{storeId}/products?keyword={keyword}&priceFrom={priceFrom}&priceTo={priceTo}&category={category}&withSubcategories={withSubcategories}&sortBy={sortBy}&offset={offset}&limit={limit}&createdFrom={createdFrom}&createdTo={createdTo}&updatedFrom={updatedFrom}&updatedTo={updatedTo}&enabled={enabled}&inStock={inStock}&field{attributeName}={attributeValues}&field{attributeId}={attributeValues}&sku={sku}&productId={productId}&baseUrl={baseUrl}&cleanUrls={cleanUrls}&token={token}`

<aside class="notice">
Parameters in <strong>bold</strong> are mandatory
</aside>

Name | Type | Description
---- | ---- | -----------
**storeId** |  number | Ecwid store ID
**token** |  string | oAuth token
keyword |  string | Search term. Use quotes to search for exact match. Ecwid searches products over multiple fields: <ul><li>title</li><li>description</li><li>SKU</li><li>product options</li><li>category name</li><li>gallery image descriptions</li><li>attribute values (except for hidden attributes)
priceFrom |  number | Minimum product price
priceTo | number | Maximum product price
category | number | Category ID. To get Store Front Page products, specify `&category=0` in the request
withSubcategories |  boolean | `true`/`false`: defines whether Ecwid should search in subcategories of the category you set in `category` field. Ignored if `category` field is not set . `false` is the default value
sortBy |  string | Sort order. Supported values: <ul><li>`RELEVANCE` *default*</li> <li>`ADDED_TIME_DESC`</li> <li>`ADDED_TIME_ASC`</li> <li>`NAME_ASC`</li> <li>`NAME_DESC`</li> <li>`PRICE_ASC`</li> <li>`PRICE_DESC`</li><li>`UPDATED_TIME_ASC`</li><li>`UPDATED_TIME_DESC`</li></ul>
offset | number | Offset from the beginning of the returned items list (for paging)
limit | number | Maximum number of returned items. Maximum allowed value: `100`. Default value: `100`
createdFrom | string | Product creation date/time (lower bound). Supported formats: <ul><li>*UNIX timestamp*</li> <li>*yyyy-MM-dd HH:mm:ss Z*</li> <li>*yyyy-MM-dd HH:mm:ss*</li> <li>*yyyy-MM-dd*</li> </ul> Examples: <ul><li>`1447804800`</li> <li>`2015-04-22 18:48:38 -0500`</li> <li>`2015-04-22` (this is 2015-04-22 00:00:00 UTC)</li></ul>
createdTo | string | Product creation date/time (upper bound). Supported formats: <ul><li>*UNIX timestamp*</li> <li>*yyyy-MM-dd HH:mm:ss Z*</li> <li>*yyyy-MM-dd HH:mm:ss*</li> <li>*yyyy-MM-dd*</li> </ul>
updatedFrom | string | Product last update date/time (lower bound). Supported formats: <ul><li>*UNIX timestamp*</li> <li>*yyyy-MM-dd HH:mm:ss Z*</li> <li>*yyyy-MM-dd HH:mm:ss*</li> <li>*yyyy-MM-dd*</li> </ul>
updatedTo | string | Product last update date/time (upper bound). Supported formats: <ul><li>*UNIX timestamp*</li> <li>*yyyy-MM-dd HH:mm:ss Z*</li> <li>*yyyy-MM-dd HH:mm:ss*</li> <li>*yyyy-MM-dd*</li> </ul>
enabled | boolean | `true` to get only enabled products, `false` to get only disabled products
inStock | boolean | `true` to get only products in stock, `false` to get out of stock products
field{attributeName} | string | Filter by product attribute values. Format: field{attributeName}=param[,param], where "attributeName" is the attribute name and "param" is the attribute value. You can place several values separated by comma. In that case values will be connected through logical "OR", and if the product has at least one of them it will get to the search results. Example:<br /> `fieldBrand=Apple&fieldCapacity=32GB,64GB` 
field{attributeId} | string | Filter by product attribute values. Works the same as the filter by `field{attributeName}` but attribute IDs are used instead of attribute names. This way is insensitive to attributes renaming.
sku | string | Product or combination SKU. Ecwid will return details of a product containing that SKU, if SKU value is an exact match. If SKU is specified, other search parameters are ignored, except for product ID.
productId | number | Internal Ecwid product ID or multiple productIds separated by a comma. If this field is specified, other search parameters are ignored.
baseUrl | string | Storefront URL for Ecwid to use when returning product URLs in the `url` field. If not specified, Ecwid will use the storefront URL specified in the [store settings](#get-store-profile)
cleanUrls | boolean | If `true`, Ecwid will return the SEO-friendly clean URL (without hash `'#'`) in the `url` field. If `false`, Ecwid will return URL in the old format (with hash `'#'`). We recommend using `true` value if merchant's website supports clean [SEO-friendly URL feature](#seo-friendly-urls)

<aside class="notice">
If no filters are set in the URL, API will return all products
</aside>

<aside class="notice">
To search for exact match, put the keyword in quotes like this: "ABC123". For example, you can use this to get a product by SKU. 
</aside>

<aside class="notice">
To get all products from the store, use the <strong>offset</strong> parameter. I.e. after you got first 100 products, set <strong>offset</strong> to 100 and retrieve the next 100 products. Continue this loop to get all products in a store.
</aside>

#### Response

> Response example (JSON)

```json
{
    "total": 5,
    "count": 2,
    "offset": 0,
    "limit": 2,
    "items": [
        {
          "id": 37208339,
          "sku": "00099",
          "thumbnailUrl": "http://app.ecwid.com/default-store/00011-232-sq.jpg",
          "quantity": 11,
          "unlimited": false,
          "inStock": true,
          "name": "Orange",
          "price": 10,
          "priceInProductList": 10,
          "wholesalePrices": [
            {
              "quantity": 2,
              "price": 9
            },
            {
              "quantity": 4,
              "price": 8
            }
          ],
          "compareToPrice": 23,
          "isShippingRequired": true,
          "weight": 0,
          "url": "http://app.ecwid.com#!/Orange/p/37208339",
          "created": "2015-10-05 07:26:14 +0000",
          "updated": "2016-02-03 10:01:02 +0000",
          "createTimestamp": 1444029974,
          "updateTimestamp": 1454493662,
          "productClassId": 0,
          "enabled": true,
          "options": [],
          "warningLimit": 0,
          "fixedShippingRateOnly": true,
          "fixedShippingRate": 0,
          "defaultCombinationId": 0,
          "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/397690775.jpg",
          "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341234.jpg",
          "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341232.jpg",
          "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/461717703.jpg",
          "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124125.jpg",
          "originalImage": {
              "url": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124125.jpg",
              "width": 123,
              "height": 456
          },
          "description": "<p>It's a tasty fruit!</p>",
          "galleryImages": [
            {
              "id": 18481471,
              "alt": "AdditionalImage",
              "url": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/312058848.jpg",
              "thumbnail": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/351433814.jpg",
              "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/397690771.jpg",
              "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412312.jpg",
              "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341235.jpg",
              "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/461717705.jpg",
              "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124121.jpg",
              "width": 473,
              "height": 545,
              "orderBy": 0
            },
            {
              "id": 18481472,
              "alt": "AdditionalImage",
              "url": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/312058850.jpg",
              "thumbnail": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/351433815.jpg",
              "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/397690775.jpg",
              "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412311.jpg",
              "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341238.jpg",
              "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/4617177879.jpg",
              "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124179.jpg",
              "width": 247,
              "height": 545,
              "orderBy": 1
            }
          ],
          "categoryIds": [
            19563207,
            19976005,
            19976006
          ],
          "categories": [
            {
              "id": 19976006,
              "enabled": true
            },
            {
              "id": 19976005,
              "enabled": true
            },
            {
              "id": 19563207,
              "enabled": false
            }
          ],
          "seoTitle": "Orange",
          "seoDescription": "It's a tasty orange for you and your family!",
          "defaultCategoryId": 0,
          "favorites": {
            "count": 0,
            "displayedCount": "0"
          },
          "attributes": [
            {
              "id": 8258226,
              "name": "Width",
              "value": "61.47 mm",
              "type": "CUSTOM",
              "show": "DESCR"
            },
            {
              "id": 8258231,
              "name": "Height",
              "value": "117.09 mm",
              "type": "CUSTOM",
              "show": "DESCR"
            },
            {
              "id": 8258249,
              "name": "Depth",
              "value": "15.49 mm",
              "type": "CUSTOM",
              "show": "DESCR"
            },
            {
              "id": 8258255,
              "name": "Net weight",
              "value": "153.2 g",
              "type": "CUSTOM",
              "show": "DESCR"
            }
          ],
          "files": [],
          "relatedProducts": {
            "productIds": [],
            "relatedCategory": {
              "enabled": false,
              "categoryId": 0,
              "productCount": 1
            }
          },
          "combinations": [],
          "dimensions": {
            "length": 0,
            "width": 0,
            "height": 0
          },
          "showOnFrontpage": 1
        },
        {
            "id": 37208340,
            "sku": "00007",
            "thumbnailUrl": "http://app.ecwid.com/default-store/00007-230-sq.jpg",
            "quantity": 67,
            "inStock": true,
            "name": "Radish",
            "price": 1.15,
            "priceInProductList": 1.15,
            "wholesalePrices": [
                {
                    "quantity": 10,
                    "price": 1.05
                }
            ],
            "compareToPrice": 1.34,
            "isShippingRequired": true,
            "weight": 0.31,
            "url": "http://app.ecwid.com/store/4870020#!/~/product/id=37208339",
            "created": "2009-07-23 17:22:37 +0000",
            "updated": "2014-07-30 10:32:37 +0000",
            "createTimestamp": 1248340746,
            "updateTimestamp": 1428313104,
            "productClassId": 0,
            "enabled": false,
            "options": [
                {
                    "type": "RADIO",
                    "name": "Size",
                    "choices": [
                        {
                            "text": "Small",
                            "priceModifier": 0,
                            "priceModifierType": "ABSOLUTE"
                        },
                        {
                            "text": "Large",
                            "priceModifier": 0.5,
                            "priceModifierType": "ABSOLUTE"
                        }
                    ],
                    "defaultChoice": 0,
                    "required": false
                },
                {
                    "type": "SELECT",
                    "name": "Color",
                    "choices": [
                        {
                            "text": "Red",
                            "priceModifier": 0,
                            "priceModifierType": "ABSOLUTE"
                        },
                        {
                            "text": "White",
                            "priceModifier": 0,
                            "priceModifierType": "ABSOLUTE"
                        }
                    ],
                    "defaultChoice": 0,
                    "required": false
                }
            ],
            "warningLimit": 0,
            "fixedShippingRateOnly": false,
            "fixedShippingRate": 0,
            "defaultCombinationId": 7084076,
            "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/3976907712.jpg",
            "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412311.jpg",
            "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341239.jpg",
            "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/4617177031.jpg",
            "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124114.jpg",
            "originalImage": {
              "url": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124114.jpg",
              "width": 123,
              "height": 456
            },
            "description": "<h5>Radish</h5>\n<p>The radish (Raphanus sativus) is an edible root vegetable of the Brassicaceae family that was domesticated in Europe in pre-Roman times. They are grown and consumed throughout the world. Radishes have numerous varieties, varying in size, color and duration of required cultivation time. There are some radishes that are grown for their seeds; oilseed radishes are grown, as the name implies, for oil production.</p>\n<p> </p>\n<div style=\"padding: 24px 24px 24px 21px; display: block; background-color: #ececec;\">From <a style=\"color: #1e7ec8; text-decoration: underline;\" title=\"Wikipedia\" href=\"http://en.wikipedia.org\">Wikipedia</a>, the free encyclopedia</div>",
            "galleryImages": [
                {
                    "id": 18276483,
                    "alt": "Radish with friends",
                    "url": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124118.jpg",
                    "thumbnail": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341231.jpg",
                    "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/3976907714.jpg",
                    "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412315.jpg",
                    "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341231.jpg",
                    "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/4617177035.jpg",
                    "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124118.jpg",
                    "width": 220,
                    "height": 293,
                    "orderby": 10
                }
            ],
            "categoryIds": [
                9691095
            ],
            "categories": [
              {
                "id": 9691095,
                "enabled": true
              }
            ],
            "seoTitle": "Radish",
            "seoDescription": "It's an awesome radish just for you!",            
            "defaultCategoryId": 9691095,
            "attributes": [
                {
                    "id": 5029057,
                    "name": "Brand",
                    "value": "SuperVegetables",
                    "type": "BRAND",
                    "show": "DESCR"
                },
                {
                    "id": 5029059,
                    "name": "Hidden Attribute",
                    "value": "Secret Value",
                    "type": "CUSTOM",
                    "show": "NOTSHOW"
                }
            ],
            "files": [
                {
                    "id": 7215101,
                    "name": "pic_200_200.jpg",
                    "description": "",
                    "size": 54492,
                    "adminUrl": "https://app.ecwid.com/api/v3/4870020/products/37208340/files/7215101"
                },
                {
                    "id": 7215102,
                    "name": "14293004.zip",
                    "description": "Files archive",
                    "size": 18955,
                    "adminUrl": "https://app.ecwid.com/api/v3/4870020/products/37208340/files/7215102"
                }
            ],
            "relatedProducts": {
                "productIds": [
                    37208340
                ],
                "relatedCategory": {
                    "enabled": true,
                    "categoryId": 9691095,
                    "productCount": 1
                }
            },
            "combinations": [
                {
                    "id": 7084071,
                    "combinationNumber": 6,
                    "options": [
                        {
                            "name": "Color",
                            "value": "White"
                        },
                        {
                            "name": "Size",
                            "value": "Large"
                        }
                    ],
                    "sku": "000076",
                    "quantity": 1,
                    "unlimited": false,
                    "weight": 0.41,
                    "warningLimit": 1
                },
                {
                    "id": 7084072,
                    "combinationNumber": 5,
                    "options": [
                        {
                            "name": "Color",
                            "value": "Red"
                        },
                        {
                            "name": "Size",
                            "value": "Large"
                        }
                    ],
                    "sku": "000075",
                    "quantity": 0,
                    "unlimited": false,
                    "weight": 0.41,
                    "warningLimit": 0
                },
                {
                    "id": 7084075,
                    "combinationNumber": 2,
                    "options": [
                        {
                            "name": "Size",
                            "value": "Small"
                        },
                        {
                            "name": "Color",
                            "value": "White"
                        }
                    ],
                    "sku": "000072",
                    "quantity": 67,
                    "unlimited": true,
                    "warningLimit": 0
                },
                {
                    "id": 7084076,
                    "combinationNumber": 1,
                    "options": [
                        {
                            "name": "Size",
                            "value": "Small"
                        },
                        {
                            "name": "Color",
                            "value": "Red"
                        }
                    ],
                    "sku": "000071",
                    "quantity": 61,
                    "smallThumbnailUrl": "https://app.ecwid.com/images/1003/397690841.jpg",
                    "hdThumbnailUrl": "https://app.ecwid.com/images/1003/397690842.jpg",
                    "thumbnailUrl": "https://app.ecwid.com/images/1003/397690811.jpg",
                    "imageUrl": "https://app.ecwid.com/images/1003/397690844.jpg",
                    "originalImageUrl": "https://app.ecwid.com/images/1003/397690845jpg",
                    "unlimited": false,
                    "warningLimit": 0
                }
            ],
          "dimensions": {
            "length": 14,
            "width": 6,
            "height": 3
          }
        }
    ]
}
```

> Public token request example

```http
GET /api/v3/4870020/products?limit=2&keyword=fruit&token=public_123abcdaASasdASjndasAnsdu HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

> Response example (JSON)

```json
{
    "total": 5,
    "count": 2,
    "offset": 0,
    "limit": 2,
    "items": [
        {
          "id": 37208339,
          "sku": "00099",
          "thumbnailUrl": "http://app.ecwid.com/default-store/00011-232-sq.jpg",
          "quantity": 11,
          "unlimited": false,
          "inStock": true,
          "name": "Orange",
          "price": 10,
          "priceInProductList": 10,
          "wholesalePrices": [
            {
              "quantity": 2,
              "price": 9
            },
            {
              "quantity": 4,
              "price": 8
            }
          ],
          "compareToPrice": 23,
          "isShippingRequired": true,
          "weight": 0,
          "url": "http://app.ecwid.com#!/Orange/p/37208339",
          "created": "2015-10-05 07:26:14 +0000",
          "updated": "2016-02-03 10:01:02 +0000",
          "createTimestamp": 1444029974,
          "updateTimestamp": 1454493662,
          "productClassId": 0,
          "enabled": true,
          "options": [],
          "warningLimit": 0,
          "fixedShippingRateOnly": true,
          "fixedShippingRate": 0,
          "defaultCombinationId": 0,
          "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/397690775.jpg",
          "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341234.jpg",
          "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341232.jpg",
          "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/461717703.jpg",
          "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124125.jpg",
          "originalImage": {
              "url": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124125.jpg",
              "width": 123,
              "height": 456
          },
          "description": "<p>It's a tasty fruit!</p>",
          "galleryImages": [
            {
              "id": 18481471,
              "alt": "AdditionalImage",
              "url": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/312058848.jpg",
              "thumbnail": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/351433814.jpg",
              "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/397690771.jpg",
              "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412312.jpg",
              "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341235.jpg",
              "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/461717705.jpg",
              "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124121.jpg",
              "width": 473,
              "height": 545,
              "orderBy": 0
            },
            {
              "id": 18481472,
              "alt": "AdditionalImage",
              "url": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/312058850.jpg",
              "thumbnail": "https://dpbfm6h358sh7.cloudfront.net/images/5035009/351433815.jpg",
              "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/397690775.jpg",
              "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412311.jpg",
              "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341238.jpg",
              "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/4617177879.jpg",
              "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124179.jpg",
              "width": 247,
              "height": 545,
              "orderBy": 1
            }
          ],
          "categoryIds": [
            19563207,
            19976005,
            19976006
          ],
          "categories": [
            {
              "id": 19976006,
              "enabled": true
            },
            {
              "id": 19976005,
              "enabled": true
            },
            {
              "id": 19563207,
              "enabled": false
            }
          ],
          "seoTitle": "Orange",
          "seoDescription": "It's a tasty orange for you and your family!",
          "defaultCategoryId": 0,
          "favorites": {
            "count": 0,
            "displayedCount": "0"
          },
          "attributes": [
            {
              "id": 8258226,
              "name": "Width",
              "value": "61.47 mm",
              "type": "CUSTOM",
              "show": "DESCR"
            },
            {
              "id": 8258231,
              "name": "Height",
              "value": "117.09 mm",
              "type": "CUSTOM",
              "show": "DESCR"
            },
            {
              "id": 8258249,
              "name": "Depth",
              "value": "15.49 mm",
              "type": "CUSTOM",
              "show": "DESCR"
            },
            {
              "id": 8258255,
              "name": "Net weight",
              "value": "153.2 g",
              "type": "CUSTOM",
              "show": "DESCR"
            }
          ],
          "files": [],
          "relatedProducts": {
            "productIds": [],
            "relatedCategory": {
              "enabled": false,
              "categoryId": 0,
              "productCount": 1
            }
          },
          "combinations": [],
          "dimensions": {}
        },
        {
            "id": 37208339,
            "enabled": false
        }
    ]
}
```


A JSON object of type 'SearchResult' with the following fields:

#### SearchResult
Field | Type | Description
----- | ---- | -----------
total | number | The total number of found items (might be more than the number of returned items)
count | number | The total number of the items returned in this batch
offset | number | Offset from the beginning of the returned items list (for paging)
limit | number | Maximum possible number of returned items in this request. 
items | Array<ProductEntry> | The items list

#### ProductEntry
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Unique integer product identifier
sku | string |  Product SKU. Items with options can have several SKUs specified in the product combinations.
quantity |  number | Amount of product items in stock. *This field is omitted for the products with unlimited stock*
unlimited | boolean | `true` if the product has unlimited stock
inStock | boolean | `true` if the product or any of its combinations is in stock (quantity is more than zero) or has unlimited quantity. `false` otherwise.
name |  string |  Product title
price | number |  Base product price
priceInProductList | number |  Product price displayed in a storefront. May differ from the *price* value when the product has options and combinations and the default combination's price is different from the base product price
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend *Omitted if empty*
isShippingRequired | boolean | `true` if product requires shipping, `false` otherwise
weight |  number | Product weight in the units defined in store settings. *Omitted for intangible products*
url | string |  URL of the product's details page in the store. [Learn more](#q-how-to-get-urls-for-products)
created | string | Date and time of the product creation. Example: `2014-07-30 10:32:37 +0000`
updated |  string | Product last update date/time
createTimestamp | number | The date of product creation in UNIX Timestamp format, e.g `1427268654`
updateTimestamp | number | Product last update date in UNIX Timestamp format, e.g `1427268654`
productClassId |  number | Id of the class (type) that this product belongs to. `0` value means the product is of the default 'General' class. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` if product is enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<*ProductOption*\> | A list of the product options. Empty (`[]`) if no options are specified for the product. 
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
defaultCombinationId |  number |  Identifier of the default product combination, which is defined by the default values of product options.
thumbnailUrl |  string | URL of the product thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. Default size of the biggest dimension is 400px. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product image resized to fit 1500x1500px. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product thumbnail resized to fit 160x160px. *The original uploaded product image is available in the `originalImageUrl` field.*
hdThumbnailUrl | string  | Product HD thumbnail URL resized to fit 800x800px
originalImageUrl |  string  | URL of the original not resized product image
originalImage | \<ImageDetails\> | Details of the product image
description | string  | Product description *in HTML*
galleryImages | Array\<*GalleryImage*\> |  List of the product gallery images
categoryIds | Array\<number\> | List of the categories, which the product belongs to. If no categories provided, product will be displayed on the store front page, see `showOnFrontpage` field
categories | Array\<CategoriesInfo\> | List of the categories, which the product belongs to, with brief details. If no categories provided, product belogs to store front page, see `showOnFrontpage` field
seoTitle | string | Page title to be displayed in search results on the web. Recommended length is under 55 characters
seoDescription | string | Page description to be displayed in search results on the web. Recommended length is under 160 characters
defaultCategoryId | number  | Identifier of the default category of the product
favorites | \<FavoritesStats\>  | Product favorites stats
attributes | Array\<*AttributeValue*\> | Product attributes and their values
files | Array\<*ProductFile*\> | Downloadable files (E-goods) attached to the product
relatedProducts | \<*RelatedProducts*\>  | Related or "You may also like" products of the product
combinations | Array\<*Combination*\> | List of the product combinations
dimensions | \<ProductDimensions\> | Product dimensions info
showOnFrontpage | number | A positive number indicates the position (index) of a product in the store front page – the smaller the number, the higher the product is displayed on a page. A negative value means the product is not shown in the store front page

#### FavoritesStats
Field | Type  | Description
----- | ----- | -----------
count | number | The actual number of 'likes' of this product
displayedCount | string | The displayed number of likes. May differ from the `count` if, for example, the value is more than 1000, than it will show 1K instead of the precise number

#### WholesalePrice
Field | Type  | Description
----- | ----- | -----------
quantity |  number |  Number of product items on this wholesale tier
price | number |  Product price on the tier

#### ProductOption
Field | Type  | Description
----- | ----- | -----------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
name |  string |  Product option name, e.g. `Color`
choices | Array\<*ProductOptionChoice*\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *This field is omitted for the product option with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection. Only presents if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`

#### ImageDetails 
Field | Type  | Description
----- | ----- | -----------
url | string | Image URL
width | integer | Image width
height | integer | Image height

#### GalleryImage
Field | Type  | Description
----- | ----- | -----------
id | number | Internal gallery image ID
alt | string |  Image description, displayed in the image tag's *alt* attribute
url | string |  **Deprecated**. Original image URL. Equals `originalImageUrl`
thumbnail | string  | **Deprecated**. Image thumbnail URL resized to fit 160x160px. Equals `smallThumbnailUrl`
thumbnailUrl |  string | URL of the product thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. Default size of the biggest dimension is 400px. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product image resized to fit 1500x1500px. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product thumbnail resized to fit 160x160px. *The original uploaded product image is available in the `originalImageUrl` field.*
hdThumbnailUrl | string  | Product HD thumbnail URL resized to fit 800x800px
originalImageUrl |  string  | URL of the original not resized product image
width | number |  Image width
height |  number |  Image height
orderby |  number |  The sort weight of the image in the gallery images list. The less the number, the closer the image to the beginning of the gallery

#### CategoriesInfo
Field | Type  | Description
----- | ----- | -----------
id | number | Category ID
enabled | boolean | `true` if category is enabled, `false` otherwise

#### AttributeValue
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Unique attribute ID. See [Product Classes](#product-types) for the information on attribute IDs
name |  string |  Attribute displayed name
value | string  | Attribute value
type | string | Attribute type. There are user-defined attributes, general attributes and special 'price per unit’ attributes. The 'type’ field contains one of the following: `CUSTOM`, `UPC`, `BRAND`, `GENDER`, `AGE_GROUP`, `COLOR`, `SIZE`, `PRICE_PER_UNIT`, `UNITS_IN_PRODUCT`
show | string | Defines where to display the product attribute value:. Supported values: `NOTSHOW`, `DESCR`, `PRICE` 

#### ProductFile
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Internal ID of the file 
name |  string |  File name
description | string |  File description defined by the store administrator
size |  number |  File size, bytes (64-bit integer)
adminUrl | string | Direct link to the file. **Important**: to download the file, add your API token to this URL like this: `https://app.ecwid.com/api/v3/4870020/products/37208340/files/7215102?token=YOUR-API-TOKEN` 

#### RelatedProducts
Field | Type  | Description
-------------- | -------------- | --------------
productIds | Array\<number\>  | IDs of the related products
relatedCategory | *RelatedCategory*  | Describes the "N random related products from a category" option

#### RelatedCategory
Field | Type  | Description
-------------- | -------------- | --------------
enabled | boolean | `true` if the "N random related products from a category" option is enabled. `false` otherwise
categoryId |  number |  Id of the related category. Zero value means "any category", that is, random products from the whole store.
productCount |  number |  Number of random products from the given category to be shown as related

#### Combination
Field | Type  | Description
------| ----- | -----------
id |  number |  Combination ID
combinationNumber | number |  Combination # number, which is displayed in the combinations table in Control panel
options | Array\<*OptionValue*\> | Set of options that identifies this combination. An array of name-value pairs
sku | string  | Combination SKU. Omitted if the combination inherits the base product's SKU
thumbnailUrl |  string | URL of the product combination thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. Default size of biggest dimension is 400px. Omitted if the combination inherits the base product's image. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product combination image resized to fit 1500x1500px. Omitted if the combination inherits the base product's image. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product combination thumbnail resized to fit 160x160px. Omitted if the combination inherits the base product's image. *The original uploaded product image is available in the `originalImageUrl` field.*
hdThumbnailUrl | string  | Product combination HD thumbnail URL resized to fit 800x800px. Omitted if the combination inherits the base product's image.
originalImageUrl |  string  | URL of the original not resized product combination image. Omitted if the combination inherits the base product's image.
quantity | number | Amount of the combination items in stock. Omitted if the combination inherits the base product's quantity.
unlimited | boolean | `true` if the combination has unlimited stock (that is, never runs out)
price | number | Combination price. Omitted if the combination inherits the base product's price.
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of the combination's wholesale price tiers (quantity limit and price). Omitted if the combination inherits the base product's tiered price settings. 
weight | number | Combination weight in the units defined in store settings. Omitted if the combination inherits the base product's weight.
warningLimit | number | The minimum 'warning' amount of the product items in stock for this combination, if set. When the combination in stock amount reaches this level, the store administrator gets an email notification. Omitted if the combination inherits the base product's settings.

#### OptionValue
Field | Type  | Description
-------------- | -------------- | --------------
name |  string |  Option name
value | string |  Option value

#### ProductOptionChoice
Field | Type  | Description
-------------- | -------------- | --------------
text |  string | Option selection text, e.g. 'Green'.
priceModifier | number | Percent or absolute value of the option's price markup. Positive, negative and zero values are allowed. Default is `0`
priceModifierType | string | Option markup calculation type. `PERCENT` or `ABSOLUTE`. Default is `ABSOLUTE`.

#### ProductDimensions
Field | Type  | Description
-------------- | -------------- | --------------
length | number | Length of a product
width | number | Width of a product
height | number | Height of a product

#### Errors

> Error response example

```http
HTTP/1.1 400 Wrong parameter 'inStock' value: expected one of 'true', 'false', 'yes', 'no', 'on', 'off', '1', '0
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Meaning | Code (optional)
------------|--------|-----------
400 | Request parameters are malformed | 
400 | The cleanUrls value is invalid. It must be either `true` or `false` | `CLEAN_URLS_PARAMETER_IS_INVALID`
415 | Unsupported content-type: expected `application/json` or `text/json` | 
500 | Cannot get the product because of an error on the server | 

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message

#### Q: How to get URLs for products?

Direct URL for each product is always available in the `url` field once you make a request to the Ecwid REST API. 

In any Ecwid store there is a [storefront URL](#get-store-profile) field, where store owners can specify their storefront location. In case if it's empty, Ecwid will use their starter site URL to provide product URLs in the REST API and other connected services.

**When a store is embedded into multiple websites**

For this situation you may need to generate a product feed for each of those websites (building a sitemap, etc.), hence there will be multiple storefront URLs to process. In this case you can use `baseUrl` request parameter to get a working product URL in a response from the Ecwid REST API. 

Let's see how it works: 

If `baseUrl` request parameter is specified, then the `url` field will be generated according to that URL as a storefront URL. 

**Examples**

Ecwid store has a storefront URL set in store settings as: `"https://mdemo.ecwid.com"`:

- `baseUrl` parameter is not set in a request:

Example product URL in the `url` field will be: `"https://mdemo.ecwid.com#!/apple/p/70445445"`

- `baseUrl` parameter is set as `"https://mycoolstore.com"`:

Example product URL in the `url` field will be: `"https://mycoolstore.com#!/apple/p/70445445"`

As you can see, the product URL in a response from Ecwid API changes based on the value of the `baseUrl` request parameter. So now you can use it to get product URLs of the same store for any number of storefront URLs.

It is possible to use the `baseUrl` parameter together with the `cleanUrls` parameter. See below for more details on the `cleanUrls` parameter.

**Receiving SEO-friendly (clean) URLs from the Ecwid REST API**

By default, Ecwid's product URLs use hash-based format: `"https://mdemo.ecwid.com#!/apple/p/70445445"`. In case if a website supports the [SEO-friendly (clean) URLs](https://developers.ecwid.com/api-documentation/seo#seo-friendly-urls), you will need to use the `cleanUrls` request parameter in order to get URLs in that format.

<aside>
  In order for SEO-friendly (clean) URLs to be enabled on your website, please follow the instructions in the <a href="https://developers.ecwid.com/api-documentation/seo#seo-friendly-urls">SEO-friendly URLs section</a>.
</aside>

Let's see how it works: 

If `cleanUrls` request parameter is set to `true`, then `url` field will have the SEO-friendly format in the response (clean URL, no hash "#").

**Examples**

Ecwid store has a storefront URL set in store settings as: `"https://mdemo.ecwid.com"`

- `cleanUrls` parameter is set to `false` or not set

Example product URL in the `url` field will be: `"https://mdemo.ecwid.com#!/apple/p/70445445"`

- `cleanUrls` parameter is set to `true`

Example product URL in the `url` field will be: `"https://mdemo.ecwid.com/apple-p70445445"`

As you can see, the format of a product URL returned from the Ecwid API changes based on the `cleanUrls` request parameter. So now you can use it to get URLs of any of the two supported URL formats - SEO-friendly (clean) URLs or hash-based URLs. 

It is possible to use the `cleanUrls` parameter together with the `baseUrl` parameter. See above for more details on the `baseUrl` parameter.

### Get a product

Get all details of a specific product in an Ecwid store by its ID.

#### Q: How can I request details of several products at once?

If you need to do this operation for multiple products at once (batch request), you can use the [Search products](https://developers.ecwid.com/api-documentation/products#search-products) method: provide the productIds you have in the `productId` parameter separating them with a comma. 

This way your app will save some time as you will be performing less requests to the Ecwid API and they will be much more efficient.

#### Request

> Request example

```http
GET /api/v3/4870020/products/123123?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

`GET https://app.ecwid.com/api/v3/{storeId}/products/{productId}?token={token}&baseUrl={baseUrl}&cleanUrls={cleanUrls}`

Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token
baseUrl | string | Storefront URL for Ecwid to use when returning product URLs in the `url` field. If not specified, Ecwid will use the storefront URL specified in the [store settings](https://developers.ecwid.com/api-documentation/store-information#get-store-profile)
cleanUrls | boolean | If `true`, Ecwid will return the SEO-friendly clean URL (without hash `'#'`) in the `url` field. If `false`, Ecwid will return URL in the old format (with hash `'#'`). We recommend using `true` value if merchant's website supports clean [SEO-friendly URL feature](#seo-friendly-urls)

<aside class="notice">
Parameters in <strong>bold</strong> are mandatory
</aside>

#### Response

> Response example (JSON)

```json
{
    "id": 37208339,
    "sku": "00007",
    "thumbnailUrl": "http://app.ecwid.com/default-store/00007-230-sq.jpg",
    "quantity": 67,
    "inStock": true,
    "name": "Radish",
    "price": 1.15,
    "priceInProductList": 1.15,
    "wholesalePrices": [
        {
            "quantity": 10,
            "price": 1.05
        }
    ],
    "compareToPrice": 1.34,
    "isShippingRequired": true,
    "weight": 0.31,
    "url": "http://app.ecwid.com/store/4870020#!/~/product/id=37208339",
    "created": "2009-07-23 17:22:37 +0000",
    "updated": "2014-07-30 10:32:37 +0000",
    "createTimestamp": 1248340746,
    "updateTimestamp": 1428313104,
    "productClassId": 0,
    "enabled": true,
    "options": [
        {
            "type": "RADIO",
            "name": "Size",
            "choices": [
                {
                    "text": "Small",
                    "priceModifier": 0,
                    "priceModifierType": "ABSOLUTE"
                },
                {
                    "text": "Large",
                    "priceModifier": 0.5,
                    "priceModifierType": "ABSOLUTE"
                }
            ],
            "defaultChoice": 0,
            "required": false
        },
        {
            "type": "SELECT",
            "name": "Color",
            "choices": [
                {
                    "text": "Red",
                    "priceModifier": 0,
                    "priceModifierType": "ABSOLUTE"
                },
                {
                    "text": "White",
                    "priceModifier": 0,
                    "priceModifierType": "ABSOLUTE"
                }
            ],
            "defaultChoice": 0,
            "required": false
        }
    ],
    "warningLimit": 0,
    "fixedShippingRateOnly": false,
    "fixedShippingRate": 0,
    "defaultCombinationId": 7084076,
    "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/3976907712.jpg",
    "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412311.jpg",
    "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341239.jpg",
    "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/4617177031.jpg",
    "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124114.jpg",
    "originalImage": {
      "url": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124114.jpg",
      "width": 123,
      "height": 456
    },
    "description": "<h5>Radish</h5>\n<p>The radish (Raphanus sativus) is an edible root vegetable of the Brassicaceae family that was domesticated in Europe in pre-Roman times. They are grown and consumed throughout the world. Radishes have numerous varieties, varying in size, color and duration of required cultivation time. There are some radishes that are grown for their seeds; oilseed radishes are grown, as the name implies, for oil production.</p>\n<p> </p>\n<div style=\"padding: 24px 24px 24px 21px; display: block; background-color: #ececec;\">From <a style=\"color: #1e7ec8; text-decoration: underline;\" title=\"Wikipedia\" href=\"http://en.wikipedia.org\">Wikipedia</a>, the free encyclopedia</div>",
    "galleryImages": [
      {
        "id": 18276483,
        "alt": "Radish with friends",
        "url": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124118.jpg",
        "thumbnail": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341231.jpg",
        "hdThumbnailUrl": "https://dpbfm6h358sh7.cloudfront.net/images/1003/3976907714.jpg",
        "thumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/1234123412315.jpg",
        "smallThumbnailUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/123412341231.jpg",
        "imageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/images/1003/4617177035.jpg",
        "originalImageUrl": "https://dqzrr9k4bjpzk.cloudfront.net/1003/124124118.jpg",
        "width": 220,
        "height": 293,
        "orderby": 10
      }
    ],
    "categoryIds": [
        9691095
    ],
    "categories": [
      {
        "id": 9691095,
        "enabled": true
      }
    ],
    "seoTitle": "Radish",
    "seoDescription": "It's an awesome radish just for you!",     
    "defaultCategoryId": 9691095,
    "attributes": [
        {
            "id": 5029057,
            "name": "Brand",
            "value": "SuperVegetables",
            "type": "BRAND",
            "show": "DESCR"
        },
        {
            "id": 5029059,
            "name": "Hidden Attribute",
            "value": "Secret Value",
            "type": "CUSTOM",
            "show": "NOTSHOW"
        }
    ],
    "files": [
        {
            "id": 7215101,
            "name": "pic_200_200.jpg",
            "description": "",
            "size": 54492,
            "adminUrl": "https://app.ecwid.com/api/v3/4870020/products/37208340/files/7215101"
        },
        {
            "id": 7215102,
            "name": "14293004.zip",
            "description": "Files archive",
            "size": 18955,
            "adminUrl": "https://app.ecwid.com/api/v3/4870020/products/37208340/files/7215102"
        }
    ],
    "relatedProducts": {
        "productIds": [
            37208340
        ],
        "relatedCategory": {
            "enabled": true,
            "categoryId": 9691095,
            "productCount": 1
        }
    },
    "combinations": [
        {
            "id": 7084071,
            "combinationNumber": 6,
            "options": [
                {
                    "name": "Color",
                    "value": "White"
                },
                {
                    "name": "Size",
                    "value": "Large"
                }
            ],
            "sku": "000076",
            "quantity": 1,
            "unlimited": false,
            "weight": 0.41,
            "warningLimit": 1
        },
        {
            "id": 7084072,
            "combinationNumber": 5,
            "options": [
                {
                    "name": "Color",
                    "value": "Red"
                },
                {
                    "name": "Size",
                    "value": "Large"
                }
            ],
            "sku": "000075",
            "quantity": 0,
            "unlimited": false,
            "weight": 0.41,
            "warningLimit": 0
        },
        {
            "id": 7084075,
            "combinationNumber": 2,
            "options": [
                {
                    "name": "Size",
                    "value": "Small"
                },
                {
                    "name": "Color",
                    "value": "White"
                }
            ],
            "sku": "000072",
            "quantity": 67,
            "unlimited": true,
            "warningLimit": 0
        },
        {
            "id": 7084076,
            "combinationNumber": 1,
            "options": [
                {
                    "name": "Size",
                    "value": "Small"
                },
                {
                    "name": "Color",
                    "value": "Red"
                }
            ],
            "sku": "000071",
            "quantity": 61,
            "unlimited": false,
            "warningLimit": 0
        }
    ],
    "dimensions": {
      "length": 0,
      "width": 0,
      "height": 0
    },
    "showOnFrontpage": 2
}
```

> Public token request example for disabled product

```http
GET /api/v3/4870020/products/66722482?token=public_123abcdaASasdASjndasAnsdu HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

> Response example (JSON)

```json
{
  "id": 66722482,
  "enabled": false
}
```

A JSON object of type 'Product' with the following fields:

#### Product
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Unique integer product identifier
sku | string |  Product SKU. Items with options can have several SKUs specified in the product combinations.
quantity |  number | Amount of product items in stock. *This field is omitted for the products with unlimited stock*
unlimited | boolean | `true` if the product has unlimited stock
inStock | boolean | `true` if the product or any of its combinations is in stock (quantity is more than zero) or has unlimited quantity. `false` otherwise.
name |  string |  Product title
price | number |  Base product price
priceInProductList | number |  Product price displayed in a storefront. May differ from the *price* value when the product has options and combinations and the default combination's price is different from the base product price
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend *Omitted if empty*
isShippingRequired | boolean | `true` if product requires shipping, `false` otherwise
weight |  number | Product weight in the units defined in store settings. *Omitted for intangible products*
url | string |  URL of the product's details page in the store. [Learn more](#q-how-to-get-urls-for-products)
created | string | Date and time of the product creation. Example: `2014-07-30 10:32:37 +0000`
updated |  string | Product last update date/time
createTimestamp | number | The date of product creation in UNIX Timestamp format, e.g `1427268654`
updateTimestamp | number | Product last update date in UNIX Timestamp format, e.g `1427268654`
productClassId |  number | Id of the class (type) that this product belongs to. `0` value means the product is of the default 'General' class. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` if product is enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<*ProductOption*\> | A list of the product options. Empty (`[]`) if no options are specified for the product. 
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
defaultCombinationId |  number |  Identifier of the default product combination, which is defined by the default values of product options.
thumbnailUrl |  string | URL of the product thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. Default size of biggest dimension is 400px. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product image resized to fit 1500x1500px. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product thumbnail resized to fit 160x160px. *The original uploaded product image is available in the `originalImageUrl` field.*
hdThumbnailUrl | string  | Product HD thumbnail URL resized to fit 800x800px
originalImageUrl |  string  | URL of the original not resized product image
originalImage | \<ImageDetails\> | Details of the product image
description | string  | Product description *in HTML*
galleryImages | Array\<*GalleryImage*\> |  List of the product gallery images
categoryIds | Array\<number\> | List of the categories, which the product belongs to. If no categories provided, product will be displayed on the store front page, see `showOnFrontpage` field
categories | Array\<CategoriesInfo\> | List of the categories, which the product belongs to, with brief details. If no categories provided, product belogs to store front page, see `showOnFrontpage` field
seoTitle | string | Page title to be displayed in search results on the web. Recommended length is under 55 characters
seoDescription | string | Page description to be displayed in search results on the web. Recommended length is under 160 characters
defaultCategoryId | number  | Identifier of the default category of the product
favorites | \<FavoritesStats\>  | Product favorites stats
attributes | Array\<*AttributeValue*\> | Product attributes and their values
files | Array\<*ProductFile*\> | Downloadable files (E-goods) attached to the product
relatedProducts | \<*RelatedProducts*\>  | Related or "You may also like" products of the product
combinations | Array\<*Combination*\> | List of the product combinations
dimensions | \<ProductDimensions\> | Product dimensions info
showOnFrontpage | number | A positive number indicates the position (index) of a product in the store front page – the smaller the number, the higher the product is displayed on a page. A negative value means the product is not shown in the store front page

#### FavoritesStats
Field | Type  | Description
----- | ----- | -----------
count | number | The actual number of 'likes' of this product
displayedCount | string | The displayed number of likes. May differ from the `count` if, for example, the value is more than 1000, than it will show 1K instead of the precise number

#### WholesalePrice
Field | Type  | Description
----- | ----- | -----------
quantity |  number |  Number of product items on this wholesale tier
price | number |  Product price on the tier

#### ProductOption
Field | Type  | Description
----- | ----- | -----------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
name |  string |  Product option name, e.g. `Color`
choices | Array\<*ProductOptionChoice*\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *This field is omitted for the product option with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection. Only presents if the type is `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`

#### ImageDetails 
Field | Type  | Description
----- | ----- | -----------
url | string | Image URL
width | integer | Image width
height | integer | Image height

#### GalleryImage
Field | Type  | Description
----- | ----- | -----------
id | number | Internal gallery image ID
alt | string |  Image description, displayed in the image tag's *alt* attribute
url | string |  **Deprecated**. Original image URL. Equals `originalImageUrl`
thumbnail | string  | **Deprecated**. Image thumbnail URL resized to fit 160x160px. Equals `smallThumbnailUrl`
thumbnailUrl |  string | URL of the product thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. Default size of biggest dimension is 400px. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product image resized to fit 1500x1500px. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product thumbnail resized to fit 160x160px. *The original uploaded product image is available in the `originalImageUrl` field.*
hdThumbnailUrl | string  | Product HD thumbnail URL resized to fit 800x800px
originalImageUrl |  string  | URL of the original not resized product image
width | number |  Image width
height |  number |  Image height
orderby |  number |  The sort weight of the image in the gallery images list. The less the number, the closer the image to the beginning of the gallery

#### CategoriesInfo
Field | Type  | Description
----- | ----- | -----------
id | number | Category ID
enabled | boolean | `true` if category is enabled, `false` otherwise

#### AttributeValue
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Unique attribute ID. See [Product Classes](#product-types) for the information on attribute IDs
name |  string |  Attribute displayed name
value | string  | Attribute value
type | string | Attribute type. There are user-defined attributes, general attributes and special 'price per unit’ attributes. The 'type’ field contains one of the following: `CUSTOM`, `UPC`, `BRAND`, `GENDER`, `AGE_GROUP`, `COLOR`, `SIZE`, `PRICE_PER_UNIT`, `UNITS_IN_PRODUCT`
show | string | Defines where to display the product attribute value:. Supported values: `NOTSHOW`, `DESCR`, `PRICE` . 

#### ProductFile
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Internal ID of the file 
name |  string |  File name
description | string |  File description defined by the store administrator
size |  number |  File size, bytes (64-bit integer)
adminUrl | string | Direct link to the file. **Important**: to download the file, add your API token to this URL like this: `https://app.ecwid.com/api/v3/4870020/products/37208340/files/7215102?token=YOUR-API-TOKEN` 

#### RelatedProducts
Field | Type  | Description
-------------- | -------------- | --------------
productIds | Array\<number\>  | IDs of the related products
relatedCategory | *RelatedCategory*  | Describes the "N random related products from a category" option

#### RelatedCategory
Field | Type  | Description
-------------- | -------------- | --------------
enabled | boolean | `true` if the "N random related products from a category" option is enabled. `false` otherwise
categoryId |  number |  Id of the related category. Zero value means "any category", that is, random products from the whole store.
productCount |  number |  Number of random products from the given category to be shown as related

#### Combination
Field | Type  | Description
------| ----- | -----------
id |  number |  Combination ID
combinationNumber | number |  Combination # number, which is displayed in the combinations table in Control panel
options | Array\<*OptionValue*\> | Set of options that identifies this combination. An array of name-value pairs
sku | string  | Combination SKU. Omitted if the combination inherits the base product's SKU
thumbnailUrl |  string | URL of the product combination thumbnail displayed on the product list pages. Thumbnails size is defined in the store settings. Default size of biggest dimension is 400px. Omitted if the combination inherits the base product's image. *The original uploaded product image is available in the `originalImageUrl` field.*
imageUrl |  string  | URL of the product combination image resized to fit 1500x1500px. Omitted if the combination inherits the base product's image. *The original uploaded product image is available in the `originalImageUrl` field.*
smallThumbnailUrl | string  | URL of the product combination thumbnail resized to fit 160x160px. Omitted if the combination inherits the base product's image. *The original uploaded product image is available in the `originalImageUrl` field.*
hdThumbnailUrl | string  | Product combination HD thumbnail URL resized to fit 800x800px. Omitted if the combination inherits the base product's image.
originalImageUrl |  string  | URL of the original not resized product combination image. Omitted if the combination inherits the base product's image.
quantity | number | Amount of the combination items in stock. Omitted if the combination inherits the base product's quantity.
unlimited | boolean | `true` if the combination has unlimited stock (that is, never runs out)
price | number | Combination price. Omitted if the combination inherits the base product's price.
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of the combination's wholesale price tiers (quantity limit and price). Omitted if the combination inherits the base product's tiered price settings. 
weight | number | Combination weight in the units defined in store settings. Omitted if the combination inherits the base product's weight.
warningLimit | number | The minimum 'warning' amount of the product items in stock for this combination, if set. When the combination in stock amount reaches this level, the store administrator gets an email notification. Omitted if the combination inherits the base product's settings.

#### OptionValue
Field | Type  | Description
-------------- | -------------- | --------------
name |  string |  Option name
value | string |  Option value

#### ProductOptionChoice
Field | Type  | Description
-------------- | -------------- | --------------
text |  string | Option selection text, e.g. 'Green'.
priceModifier | number | Percent or absolute value of the option's price markup. Positive, negative and zero values are allowed. Default is `0`
priceModifierType | string | Option markup calculation type. `PERCENT` or `ABSOLUTE`. Default is `ABSOLUTE`.

#### ProductDimensions
Field | Type  | Description
-------------- | -------------- | --------------
length | number | Length of a product
width | number | Width of a product
height | number | Height of a product

#### Errors

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Meaning | Code (optional)
------------|--------|-----------
400 | The cleanUrls value is invalid. It must be either `true` or `false` | `CLEAN_URLS_PARAMETER_IS_INVALID`
404 | Product is not found | 
500 | Cannot get the product because of an error on the server | 

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message

#### Q: How to get URLs for products?

Direct URL for each product is always available in the `url` field once you make a request to the Ecwid REST API. 

In any Ecwid store there is a [storefront URL](https://developers.ecwid.com/api-documentation/store-information#get-store-profile) field, where store owners can specify their storefront location. In case if it's empty, Ecwid will use their starter site URL to provide product URLs in the REST API and other connected services.

**When a store is embedded into multiple websites**

For this situation you may need to generate a product feed for each of those websites (building a sitemap, etc.), hence there will be multiple storefront URLs to process. In this case you can use `baseUrl` request parameter to get a working product URL in a response from the Ecwid REST API. 

Let's see how it works: 

If `baseUrl` request parameter is specified, then the `url` field will be generated according to that URL as a storefront URL. 

**Examples**

Ecwid store has a storefront URL set in store settings as: `"https://mdemo.ecwid.com"`:

- `baseUrl` parameter is not set in a request:

Example product URL in the `url` field will be: `"https://mdemo.ecwid.com#!/apple/p/70445445"`

- `baseUrl` parameter is set as `"https://mycoolstore.com"`:

Example product URL in the `url` field will be: `"https://mycoolstore.com#!/apple/p/70445445"`

As you can see, the product URL in a response from Ecwid API changes based on the value of the `baseUrl` request parameter. So now you can use it to get product URLs of the same store for any number of storefront URLs.

It is possible to use the `baseUrl` parameter together with the `cleanUrls` parameter. See below for more details on the `cleanUrls` parameter.

**Receiving SEO-friendly (clean) URLs from the Ecwid REST API**

By default, Ecwid's product URLs use hash-based format: `"https://mdemo.ecwid.com#!/apple/p/70445445"`. In case if a website supports the [SEO-friendly (clean) URLs](https://developers.ecwid.com/api-documentation/seo#seo-friendly-urls), you will need to use the `cleanUrls` request parameter in order to get URLs in that format.

<aside>
  In order for SEO-friendly (clean) URLs to be enabled on your website, please follow the instructions in the <a href="https://developers.ecwid.com/api-documentation/seo#seo-friendly-urls">SEO-friendly URLs section</a>.
</aside>

Let's see how it works: 

If `cleanUrls` request parameter is set to `true`, then `url` field will have the SEO-friendly format in the response (clean URL, no hash "#").

**Examples**

Ecwid store has a storefront URL set in store settings as: `"https://mdemo.ecwid.com"`

- `cleanUrls` parameter is set to `false` or not set

Example product URL in the `url` field will be: `"https://mdemo.ecwid.com#!/apple/p/70445445"`

- `cleanUrls` parameter is set to `true`

Example product URL in the `url` field will be: `"https://mdemo.ecwid.com/apple-p70445445"`

As you can see, the format of a product URL returned from the Ecwid API changes based on the `cleanUrls` request parameter. So now you can use it to get URLs of any of the two supported URL formats - SEO-friendly (clean) URLs or hash-based URLs. 

It is possible to use the `cleanUrls` parameter together with the `baseUrl` parameter. See above for more details on the `baseUrl` parameter.

### Add a product

Create a new product in an Ecwid store. 

#### Request

> Request body

```http
POST /api/v3/4870020/products?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

{
  "sku": "000012199",
  "quantity": 10,
  "name": "New Product",
  "price": 20.99,
  "compareToPrice": 24.99,
  "isShippingRequired": false,
  "categoryIds": [
    9691094
  ],
  "weight": 10,
  "enabled": true,
  "description": "A <b>new</b> product description",
  "productClassId": 0,
  "created":"2014-01-01",
  "fixedShippingRateOnly": false,
  "fixedShippingRate": 1.2
}
```


`POST https://app.ecwid.com/api/v3/{storeId}/products?token={token}`


Name | Type    | Description
---- | ------- | --------------
**storeId** |  number | Ecwid store ID
**token** |  string |  oAuth token


#### Request body

A JSON object of type 'Product' with the following fields:

#### Product
Field | Type |  Description
------| ---- | ------------
**name** |  string |  Product title
sku | string |  Product SKU. If this field is empty, Ecwid will generate new unique SKU automatically.
quantity |  number | Amount of product items in stock. 
unlimited | boolean | Set as `true` to make Unlimited stock for the product and to not track product inventory. 
price | number |  Base product price
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend
isShippingRequired | boolean | `true` if product requires shipping, `false` otherwise
weight |  number | Product weight in the units defined in store settings. *Leave empty for intangible products*
productClassId |  number | Id of the class (type) that this product belongs to. `0` value means the product is of the default 'General' class. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` to make product enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<*ProductOption*\> | List of the product options. 
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
description | string  | Product description *in HTML*
categoryIds | Array\<number\> | List of the categories, which the product belongs to. If no categories provided, product will be displayed on the store front page, see `showOnFrontpage` field
seoTitle | string | Page title to be displayed in search results on the web. Recommended length is under 55 characters
seoDescription | string | Page description to be displayed in search results on the web. Recommended length is under 160 characters
defaultCategoryId | number  | Identifier of the default category of the product
attributes | Array\<*AttributeValue*\> | Product attributes and their values
relatedProducts | \<*RelatedProducts*\>  | Related or "You may also like" products of the product
dimensions | \<ProductDimensions\> | Product dimensions info
showOnFrontpage | number | A positive number indicates the position (index) of a product in the store front page – the smaller the number, the higher the product is displayed on a page. A negative value means the product is not shown in the store front page. If no categories are assigned to product in `categoryIds` field, the `showOnFrontPage` will be `1`

#### WholesalePrice
Field | Type  | Description
-------------- | -------------- | --------------
**quantity** |  number |  Number of product items on this wholesale tier
**price** | number |  Product price on the tier


#### ProductOption
Field | Type  | Description
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
**name** |  string |  Product option name, e.g. `Color`
choices | Array\<*ProductOptionChoice*\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *Omit this field for product options with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection for the options types `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is required, `false` otherwise. Default is `false`

#### AttributeValue
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Unique attribute ID. See [Product Classes](#product-types) for the information on attribute IDs. 
alias | string | One of `UPC` , `BRAND` . This can be used instead of id to quickly set the basic product attributes values without numeric id: UPC and brand 
value | string  | Attribute value

#### RelatedProducts
Field | Type  | Description
-------------- | -------------- | --------------
**productIds** | Array\<number\>  | IDs of the related products, sort order is taken into the account
relatedCategory | *RelatedCategory*  | Describes the "N random related products from a category" option

#### RelatedCategory
Field | Type  | Description
-------------- | -------------- | --------------
enabled | boolean | `true` if the "N random related products from a category" option is enabled. `false` otherwise
**categoryId** |  number |  Id of the related category. Zero value means "any category", that is, random products from the whole store.
productCount |  number |  Number of random products from the given category to be shown as related

#### OptionValue
Field | Type |  Description
-------------- | -------------- | --------------
**name** |  string |  Option name, as in Product.options[i].name
value | string |  Option value one of Product.options[i].choices[j].text

#### ProductOptionChoice
Field | Type  | Description
-------------- | -------------- | --------------
**text** |  string | Option selection text, e.g. 'Green'.
priceModifier | number | Percent or absolute value of the option's price markup. Positive, negative and zero values are allowed. Default is `0`
priceModifierType | string | Option markup calculation type. `PERCENT` or `ABSOLUTE`. Default is `ABSOLUTE`.

#### ProductDimensions
Field | Type  | Description
-------------- | -------------- | --------------
length | number | Length of a product
width | number | Width of a product
height | number | Height of a product

<aside class="notice">
Parameters in bold are mandatory
</aside>


#### Response


> Response example

```json
{
    "id": 39766764
}
```

A JSON object of type 'CreateStatus' with the following fields:

#### CreateStatus
Field | Type |  Description
-------------- | -------------- | --------------
id | number | ID of the created product

#### Errors

```http
HTTP/1.1 409 Conflict
Content-Type application/json; charset=utf-8

{
 errorMessage: "WhosalePrice cannot be null",
 errorCode: "WHOLESALE_PRICES_CANT_BE_NULL"
}
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Description | Code (optional)
-------------- | -------------- | ---------------
400 | Request parameters are malformed | 
402 | The functionality/method is not available on the merchant plan | 
402 | The merchant plan product limit is reached | 
404 | Some of the linked entities in the request doesn't exist. For example, the product class is not found | 
409 | The product with such SKU already exists | `SKU_ALREADY_EXISTS`
409 | Specified wholesale price can't be `null` | `WHOLESALE_PRICES_CANT_BE_NULL`
409 | Specified wholesale price can't be negative | `WHOLESALE_PRICES_CANT_BE_NEGATIVE` 
409 | Specified wholesale price is too big | `WHOLESALE_PRICES_TOO_BIG`
409 | Specified wholesale price quantity is too small | `WHOLESALE_PRICES_QUANTITY_TOO_SMALL`
415 | Unsupported content-type: expected `application/json` or `text/json` | 

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message
errorCode | string | Error code


### Update a product

Update an existing product in an Ecwid store referring to its ID.

> Request example

```http
PUT /api/v3/4870020/products/39766764?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

{
  "compareToPrice": 24.99,
  "categoryIds": [
    9691094
  ],
  "attributes": [
    {
      "id": 12974019,
      "name": "Brand",
      "value": "Apple",
      "show": "DESCR"
    }
  ]
}
```

`PUT https://app.ecwid.com/api/v3/{storeId}/products/{productId}?token={token}`


Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token


#### Request body

A JSON object of type 'Product' with the following fields:

#### Product
Field | Type |  Description
------| ---- | ------------
sku | string |  Product SKU
name |  string |  Product title
quantity |  number | Amount of product items in stock.
unlimited | boolean | Set as `true` to make Unlimited stock for the product and to not track product inventory. 
price | number |  Base product price
wholesalePrices | Array\<*WholesalePrice*\> |  Sorted array of wholesale price tiers (quantity limit and price pairs)
compareToPrice |  number | Product's sale price displayed strike-out in the customer frontend
isShippingRequired | boolean | `true` if product requires shipping, `false` otherwise
weight |  number | Product weight in the units defined in store settings. *Leave empty for intangible products*
productClassId |  number | Id of the product type that this product belongs to. `0` value means the product is of the default 'General' type. See also: [Product types and attributes in Ecwid](http://help.ecwid.com/customer/portal/articles/1167365-product-types-and-attributes)
enabled | boolean | `true` to make product enabled, `false` otherwise. Disabled products are not displayed in the store front.
options | Array\<*ProductOption*\> | List of the product options. 
warningLimit | number | The minimum 'warning' amount of the product items in stock, if set. When the product quantity reaches this level, the store administrator gets an email notification.
fixedShippingRateOnly | boolean | `true` if shipping cost for this product is calculated as *'Fixed rate per item'* (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). `false` otherwise. With this option on, the `fixedShippingRate` field specifies the shipping cost of the product
fixedShippingRate | number |  When `fixedShippingRateOnly` is `true`, this field sets the product fixed shipping cost per item. When `fixedShippingRateOnly` is `false`, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping
description | string  | Product description *in HTML*
categoryIds | Array\<number\> | List of the categories, which the product belongs to. If no categories provided, product will be displayed on the store front page, see `showOnFrontpage` field
seoTitle | string | Page title to be displayed in search results on the web. Recommended length is under 55 characters
seoDescription | string | Page description to be displayed in search results on the web. Recommended length is under 160 characters
defaultCategoryId | number  | Identifier of the default category of the product
attributes | Array\<*AttributeValue*\> | Product attributes and their values
relatedProducts | \<*RelatedProducts*\>  | Related or "You may also like" products of the product
galleryImages | Array\<*GalleryImage*\> |  List of the product gallery images (for updating alt tags and sort order)
dimensions | \<ProductDimensions\> | Product dimensions info
showOnFrontpage | number | A positive number indicates the position (index) of a product in the store front page – the smaller the number, the higher the product is displayed on a page. A negative value means the product is not shown in the store front page

<aside class="notice">
All fields are optional
</aside>


#### WholesalePrice
Field | Type  | Description
-------------- | -------------- | --------------
**quantity** |  number |  Number of product items on this wholesale tier
**price** | number |  Product price on the tier


#### ProductOption
Field | Type  | Description
-------------- | -------------- | --------------
type |  string | One of `SELECT`, `RADIO`, `CHECKBOX`, `TEXTFIELD`, `TEXTAREA`, `DATE`, `FILES`
**name** |  string |  Product option name, e.g. `Color`
choices | Array\<*ProductOptionChoice*\> | All possible option selections for the types `SELECT`, `CHECKBOX` or `RADIO`. *Omit this field for product options with no selection (e.g. text, datepicker or upload file options)*
defaultChoice | number  | The number, starting from `0`, of the option's default selection for the options types `SELECT`, `CHECKBOX` or `RADIO`.
required |  boolean | `true` if this option is mandatory, `false` otherwise. Default is `false`


#### AttributeValue
Field | Type  | Description
-------------- | -------------- | --------------
id |  number |  Unique attribute ID. See [Product Types](#product-types) for the information on attribute IDs. 
alias | string | One of `UPC` , `BRAND` . This can be used instead of id to quickly update the basic product attributes without numeric id: UPC and brand 
value | string  | Attribute value

<aside class='notice'>To add a new attribute to a product, first <a href="#product-types">add it to product type</a> it belongs to. Then you can set a value for this new attribute by updating a product.</aside>

#### RelatedProducts
Field | Type  | Description
-------------- | -------------- | --------------
**productIds** | Array\<number\>  | IDs of the related products, sort order is taken into the account
relatedCategory | *RelatedCategory* | Describes the "N random related products from a category" option


#### RelatedCategory
Field | Type  | Description
-------------- | -------------- | --------------
enabled | boolean | `true` if the "N random related products from a category" option is enabled. `false` otherwise
**categoryId** |  number |  Id of the related category. Zero value means "any category", that is, random products from the whole store.
productCount |  number |  Number of random products from the given category to be shown as related


#### OptionValue
Field | Type |  Description
-------------- | -------------- | --------------
**name** |  string |  Option name, as in Product.options[i].name
value | string |  Option value one of Product.options[i].choices[j].text

#### ProductOptionChoice
Field | Type  | Description
-------------- | -------------- | --------------
**text** |  string | Option selection text, e.g. 'Green'.
priceModifier | number | Percent or absolute value of the option's price markup. Positive, negative and zero values are allowed. Default is `0`
priceModifierType | string | Option markup calculation type. `PERCENT` or `ABSOLUTE`. Default is `ABSOLUTE`.

#### GalleryImage
Field | Type  | Description
----- | ----- | -----------
id | number | Internal gallery image ID
alt | string |  Image description, displayed in the image tag's *alt* attribute
orderby |  number |  The sort weight of the image in the gallery images list. The less the number, the closer the image to the beginning of the gallery

#### ProductDimensions
Field | Type  | Description
-------------- | -------------- | --------------
length | number | Length of a product
width | number | Width of a product
height | number | Height of a product

#### Response

> Response example (JSON)

```json
{
  "updateCount": 1
}
```

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus

Field | Type |  Description
-------------- | -------------- | --------------
updateCount | number | The number of updated products (`1` or `0` depending on whether the update was successful)

#### Errors

```http
HTTP/1.1 409 Conflict
Content-Type application/json; charset=utf-8

{
 errorMessage: "WhosalePrice cannot be null",
 errorCode: "WHOLESALE_PRICES_CANT_BE_NULL"
}
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Description | Code (optional)
-------------- | -------------- | ---------------
400 | Request parameters are malformed | 
400 | Attribute `showOnFrontpage` was specified as a negative number when there are no categories assigned to product | Attribute `showOnFrontpage` can’t be negative, because the product has no categories
402 | The functionality/method is not available on the merchant plan | 
402 | The merchant plan product limit is reached | 
404 | Some of the linked entities in the request doesn't exist. For example, the product class is not found | 
409 | The product with such SKU already exists | `SKU_ALREADY_EXISTS`
409 | Specified wholesale price can't be `null` | `WHOLESALE_PRICES_CANT_BE_NULL`
409 | Specified wholesale price can't be negative | `WHOLESALE_PRICES_CANT_BE_NEGATIVE` 
409 | Specified wholesale price is too big | `WHOLESALE_PRICES_TOO_BIG`
409 | Specified wholesale price quantity is too small | `WHOLESALE_PRICES_QUANTITY_TOO_SMALL`
415 | Unsupported content-type: expected `application/json` or `text/json` | 

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message
errorCode | string | Error code

### Adjust product inventory

> Request example

```http
PUT /api/v3/4870020/products/39766764/inventory?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

{
    "quantityDelta": -10
}
```

When your integration changes in stock quantity of products in a store pretty often, it becomes harder and harder to keep track of how many items are actually in stock. For example, when at one point of time you have 3 items in stock and 5 in the very next second, then using the specific values can result in incorrect stock quantity.

This method solves this very problem: you can increase or decrease the product's stock quantity by a delta quantity. For example, if you need to decrease quantity by 10 items, you can use this method. 

This method is also available for the [product combinations](https://developers.ecwid.com/api-documentation/product-combinations#adjust-combination-inventory).

`PUT https://app.ecwid.com/api/v3/{storeId}/products/{productId}/inventory?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

#### Request body

A JSON object of type 'Inventory' with the following fields:

#### Inventory
Field | Type |  Description
------| ---- | ------------
**quantityDelta** | number | Delta value used to update product quantity. Negative value will decrease quantity, positive one will increase it.

#### Response

> Response example (JSON)

```json
{
  "updateCount": 1
}
```

A JSON object of type 'InventoryAdjustmentStatus' with the following fields:

#### InventoryAdjustmentStatus

Field | Type |  Description
-------------- | -------------- | --------------
updateCount | number | The number of updated products (`1` or `0` depending on whether the update was successful)
warning | string | Inventory update warning(optional). For example, the warning will display if the stock became negative

#### Errors

```http
HTTP/1.1 400 Bad Request
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

HTTP Status | Description
-------------- | --------------
400 | Request parameters are malformed
404 | Product not found
415 | Unsupported content-type: expected `application/json` or `text/json`
500 | Could not process the request, internal server error

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message

### Delete a product

Delete a product from an Ecwid store referring to its ID.

> Request example

```http
DELETE /api/v3/4870020/products/39847403?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

#### Response

> Response example

```json
{
    "deleteCount":1
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted products (`1` or `0` depending on whether the request was successful)


#### Errors

> Error response example

```http
HTTP/1.1 400 Bad request
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description.

#### HTTP codes

**HTTP Status** | **Response JSON** | Description
-------------- | -------------- | --------------
400 | Request parameters are malformed
500 | The delete request failed because of an error on the server

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message


### Upload product image

Upload product image: if the product already has an image attached, the uploaded image will replace the existing one. Maximum allowed file size is 20Mb.

> Request example

```http
POST /api/v3/4870020/products/1234657/image?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: image/jpeg
Cache-Control: no-cache

binary data
```

> PHP Example

```php
$file = file_get_contents('image.jpg');
$url = 'https://app.ecwid.com/api/v3/1003/products/123456/image?token=abcdefg123456';

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,$url);
curl_setopt($ch, CURLOPT_POST,1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $file);
curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: image/jpeg;'));

$result = curl_exec($ch);
curl_close ($ch);
```

> Python Example

```python
import requests

request_url = "https://app.ecwid.com/api/v3/1003/products/123456/image?token=abcdefg123456"

image_file_data = open('image.jpg', 'rb').read()

result = requests.post(request_url,data=image_file_data)

print(result.status_code)
```

`POST https://app.ecwid.com/api/v3/{storeId}/products/{productId}/image?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token
externalUrl | string | External file URL available for public download. If specified, Ecwid will ignore any binary file data sent in a request

When uploading an image for a product, the image itself needs to be sent in the body of your request in a form of binary data. The file that you wish to upload needs to be prepared for that format and then sent to Ecwid API endpoint. 

Alternatively, you can specify an `externalURL` to your file as a request parameter and Ecwid will download it from there.

#### Response

> Response example

```json
{
    "id": 240198557
}
```

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
Field | Type |  Description
----- | -----| ------------
id | number | Internal image ID


#### Errors

> Error response example 

```http
HTTP/1.1 500 Server Error
Content-Type application/json; charset=utf-8

{
    "errorMessage": "Internal server error"
}
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
400 | Request parameters are malformed
402 | The functionality/method is not available on the merchant plan
404 | Product is not found
413 | The image file is too large (Maximum allowed size is 20Mb)
415 | Unsupported content-type: expected `application/octet-stream`
422 | The uploaded file is not an image
500 | Uploading of the image file failed or there was an internal server error while processing a file

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message


### Delete product image

Delete the main image of a product in an Ecwid store.

> Request example

```http
DELETE /api/v3/4870020/products/1234657/image?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache
```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/image?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

#### Response

> Response example

```json
{
    "deleteCount": 1
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted images (`1` or `0` depending on whether the request was successful)

#### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
404 | Product is not found
500 | Deleting of the image file failed or there was an internal server error

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message



### Upload gallery image

Add image to the product images gallery. Request parameters specify which product should be updated and what title should the uploaded image have. Request body is the image file itself (binary data). Maximum allowed file size is 20Mb.

> Request example

```http
POST /api/v3/4870020/products/1234657/gallery?fileName=Extra%20Image&token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: image/jpeg
Cache-Control: no-cache

binary data
```

> PHP Example

```php
$file = file_get_contents('image.jpg');
$url = 'https://app.ecwid.com/api/v3/1003/products/123456/gallery?token=abcdefg123456';

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,$url);
curl_setopt($ch, CURLOPT_POST,1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $file);
curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: image/jpeg;'));

$result = curl_exec($ch);
curl_close ($ch);
```

> Python Example

```python
import requests

request_url = "https://app.ecwid.com/api/v3/1003/products/123456/gallery?token=abcdefg123456"

image_file_data = open('image.jpg', 'rb').read()

result = requests.post(request_url,data=image_file_data)

print(result.status_code)
```

`POST https://app.ecwid.com/api/v3/{storeId}/products/{productId}/gallery?fileName={fileName}token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token
fileName |  string |  Image title
externalUrl | string | External file URL available for public download. If specified, Ecwid will ignore any binary file data sent in a request

When uploading an image for a product gallery, the image itself needs to be sent in the body of your request in a form of binary data. The file that you wish to upload needs to be prepared for that format and then sent to Ecwid API endpoint. 

Alternatively, you can specify an `externalURL` to your file as a request parameter and Ecwid will download it from there.

#### Response

> Response example

```json
{
    "id": 240198557
}
```

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
Field | Type |  Description
--------- | ---------| -----------
id | number | Internal image file ID

#### Errors

> Error response example 

```http
HTTP/1.1 500 Server Error
Content-Type application/json; charset=utf-8

{
    "errorMessage": "Internal server error"
}
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
400 | Request parameters are malformed
402 | The functionality/method is not available on the merchant plan
404 | Product is not found
413 | The image file is too large (Maximum allowed size is 20Mb)
415 | Unsupported content-type: expected `application/octet-stream`
422 | The uploaded file is not an image
500 | Uploading of the image file failed or there was an internal server error while processing a file

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message



### Delete gallery image

Delete an image from a product gallery in an Ecwid store. 

> Request example

```http
DELETE /api/v3/4870020/products/1234657/gallery/1234657345/?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache
```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/gallery/{fileId}/?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token
**fileId** | number | Internal image file ID

#### Response

> Response example

```json
{
    "deleteCount": 1
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted images (`1` or `0` depending on whether the request was successful)

#### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
400 | Request parameters are malformed
404 | Product is not found
500 | Deleting of the image file failed or there was an internal server error

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message







### Delete all gallery images

Remove all gallery images attached to the product

> Request example

```http
DELETE /api/v3/4870020/products/39847403/gallery?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/gallery?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

#### Response

> Response example

```json
{
    "deleteCount": 4
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted gallery images

#### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
400 | Request parameters are malformed
404 | Product is not found
500 | Deleting of the files failed or there was an internal server error

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message






### Download product file

Download a product file referring to its file ID. 

> Request example

```http
GET /api/v3/4870020/products/1234657/files/193639?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache
```

`GET https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files/{fileId}?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**fileId** | number | Internal file ID
**token** |  string |  oAuth token

#### Response

Response is the file in binary format. 


#### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
500 | Request failed or there was an internal server error
404 | Product or file is not found

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message







### Upload product file

Upload a file to a product in an Ecwid store ([E-goods](https://support.ecwid.com/hc/en-us/articles/207100559-E-goods)).

> Request example

```http
POST /api/v3/4870020/products/1234567/files?token=123456789abcd&fileName=photo+large.psd&description=Item+photo+in+psd+format HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

binary data
```

> PHP Example

```php
$file = file_get_contents('cool.jpg');
$url = 'https://app.ecwid.com/api/v3/1003/products/123456/files?fileName=cool.jpg&token=abcdefgh123456';

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL,$url);
curl_setopt($ch, CURLOPT_POST,1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $file);
curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: image/jpeg'));

$result = curl_exec($ch);
curl_close ($ch);
```

> Python Example

```python
import requests

request_url = "https://app.ecwid.com/api/v3/1003/products/123456/files?fileName=cool.jpg&token=abcdefgh123456"

image_file_data = open('image.jpg', 'rb').read()

result = requests.post(request_url,data=image_file_data)

print(result.status_code)
```

`POST https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files?token={token}&fileName={fileName}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token
**fileName** | string | Name of the file that customers will see
description | string | A short description of the uploaded file
externalUrl | string | External file URL available for public download. If specified, Ecwid will ignore any binary file data sent in a request

When uploading an file for a product, the file itself needs to be sent in the body of your request in a form of binary data. The file you wish to upload needs to be prepared for that format and then sent to Ecwid API endpoint. 

Alternatively, you can specify an `externalURL` to your file as a request parameter and Ecwid will download it from there.

#### Response

> Response example

```json
{
    "id": 6738222
}
```

A JSON object of type 'UploadStatus' with the following fields:

#### UploadStatus
Field | Type |  Description
--------- | ---------| -----------
id | number | Internal file ID

#### Errors

> Error response example 

```http
HTTP/1.1 500 Server Error
Content-Type application/json; charset=utf-8

{
    "errorMessage": "Internal server error"
}
```

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
400 | Request parameters are malformed
402 | The functionality/method is not available on the merchant plan
404 | Product is not found
413 | The file is too large (Maximum allowed size is 100Mb)
415 | Unsupported content-type: expected `application/octet-stream`
500 | Uploading of the file failed or there was an internal server error while processing a file

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message






### Update product file description

This request allows to edit the file description that is shown to customer when they purchase the product

> Request example

```http
PUT /api/v3/4870020/products/1234567/files/4838228377?token=123456789abcd&fileName=photo+large.psd&description=Item+photo+in+psd+format HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache

{
    "description": "new description"
}
```

`PUT https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files/{fileId}?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**fileId** | string | Internal file ID
**token** |  string |  oAuth token

#### Request body

Name | Type    | Description
---- | ------- | -----------
description | string | New file description

#### Response

> Response example

```json
{
    "updateCount": 1
}
```

A JSON object of type 'UpdateStatus' with the following fields:

#### UpdateStatus
Field | Type |  Description
----- | ---- | --------------
updateCount | number | The number of updated entities (`1` or `0` depending on whether the request was successful)

#### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
400 | Request parameters are malformed
404 | Product is not found
415 | Unsupported content-type: expected `application/json` or `text/json`

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message






### Delete product file

Delete product's file (e-goods) by the file ID

> Request example

```http
DELETE /api/v3/4870020/products/1234657/files/193639?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache
```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files/{fileId}?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**fileId** | number | Internal file ID
**token** |  string |  oAuth token

#### Response

> Response example

```json
{
    "deleteCount": 1
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus
Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted files (`1` or `0` depending on whether the request was successful)

#### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
404 | Product is not found
500 | Deleting of the file failed or there was an internal server error

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message


### Delete all product files

Remove all downloadable files attached to the product (e-goods)

> Request example

```http
DELETE /api/v3/4870020/products/39847403/files?token=123456789abcd HTTP/1.1
Host: app.ecwid.com
Content-Type: application/json;charset=utf-8
Cache-Control: no-cache
```

`DELETE https://app.ecwid.com/api/v3/{storeId}/products/{productId}/files?token={token}`

Name | Type    | Description
---- | ------- | -----------
**storeId** |  number | Ecwid store ID
**productId** | number | Product ID
**token** |  string |  oAuth token

#### Response

> Response example

```json
{
    "deleteCount": 3
}
```

A JSON object of type 'DeleteStatus' with the following fields:

#### DeleteStatus

Field | Type |  Description
----- | ---- | --------------
deleteCount | number | The number of deleted files

#### Errors

> Error response example 

```http
HTTP/1.1 404 Not Found
Content-Type application/json; charset=utf-8
```

In case of error, Ecwid responds with an error HTTP status code and JSON-formatted body containing error description

#### HTTP codes

**HTTP Status** | Description
--------- | -----------| -----------
404 | Product is not found
500 | Deleting of the files failed or there was an internal server error

#### Error response body (optional)

Field | Type |  Description
--------- | ---------| -----------
errorMessage | string | Error message
