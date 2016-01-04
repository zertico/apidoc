---
title: Horus API

language_tabs:
  - shell: cURL
  - ruby: CLI

includes:
  - errors

search: true
---

# Horus API

Welcome to the Horus API!

Horus is an API that enables a Company to distribute and manage Cloud Services more simply, this API is mainly focused on Softlayer.

The Horus API simplifies the manage of resources and give liberty to integrate with your internal infrastructure.

Depending on the level of involvement with the system, users can be categorized as manager, admin or user.

## User (End Customer)

End Customer is the last layer in this API, it is responsible only for consume products and services Softlayer.

Authentication as user allows an End Customer to list and update information about his account.

## Admin (Reseller)

Reseller is responsible for selling product and services SoftLayer to users.

Authentication as admin allows a Reseller list and update his own information.

Authentication as admin allows a Reseller to list, create and update information about users.

## Manager (Distributor)

Distributor is responsible for distributing product and services SoftLayer to Companies.

Authentication as manager allows a Distributor list and update his own information.

Authentication as manager allows a Distributor to list, create and update information about Companies.

# Current Version

By default, all requests receive the v1 version of the API.

> Current Version

```shell
Not implemented
```

```ruby
horus-cli version
```

# Installation

# Identification

All system identification is a UUID type and it begins with a substring "id + resource + function".

exemple: id-user-profile: 03b829d7-bbe6-5556-ae91-e480c27a28ee

For more information about UUID access *`https://en.wikipedia.org/wiki/Universally_unique_identifier`*

# Login

The user is authenticated using a username, a password and your level of involvement with a system.

There are three ways to authenticate through Horus API, like explained above.

Route: *`POST "/oauth/token"`*

## User

> Authentication

```shell
curl -X POST -H "Content-Type: application/json" -d 
'{
  "username":"user@smart.com", 
  "password":"pass1234", 
  "grant_type": "password"
}' 
http://smart.lvh.me:3000/oauth/token

# Return
{
  "access_token":"id-access-token", 
  "token_type":"bearer", 
  "expires_in":6166, 
  "refresh_token":"id-refresh-token", 
  "created_at":1446428109
}
```

```ruby
horus-cli login --user --domain smart.lvh.me:3000
 
Login: user@smart.com 
Password: pass1234

# Return
You are logged!
```

Variable | Type | Value
-------- | ---- | ----- 
login | String | user@smart.com
password | String | pass1234
authentication | String | user
domain | String | smart.lvh.me:3000

## Admin

> Authentication

```shell
curl -X POST -H "Content-Type: application/json" -d 
'{
  "username":"admin@smart.com", 
  "password":"pass1234", 
  "grant_type": "password"
}' 
http://smart.lvh.me:3000/oauth/token

# Return
{
  "access_token":"id-access-token",
  "token_type":"bearer",
  "expires_in":5408,
  "refresh_token":"id-refresh-token",
  "created_at":1447376731
}
```

```ruby
horus-cli login --admin --domain smart.lvh.me:3000
 
Login: admin@smart.com
Password: pass1234

# Return
You are logged!
```

Variable | Type | Value
-------- | ---- | ----- 
login | String | admin@smart.com
password | String | pass1234
authentication | String | admin
domain | String | smart.lvh.me:3000

## Manager

> Authentication

```shell
curl -X POST -H "Content-Type: application/json" -d
'{
  "username":"manager@example.com", 
  "password":"pass1234", 
  "grant_type":"password"
}'
http://localhost:3000/oauth/token

# Return
{
  "access_token":"id-access-token", 
  "token_type":"bearer", 
  "expires_in":6166, 
  "refresh_token":"id-refresh-token", 
  "created_at":1446428109
}
```

```ruby
horus-cli login --manager

Login: manager@example.com
Password: pass1234

# Return
You are logged!
```

Variable | Type | Value
---------- | ---- | ----- 
login | String | manager@example.com
password | String | pass1234
authentication | String | manager

# User Profile Account

When logged in, the user can access his own profile. This access allows him to show and update information about his account.

## Show

> Show Profile Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' 
http://smart.lvh.me:3000/api/v1/profile

# OUTPUT
{
  "data":
  {
    "id":"id-user-profile",
    "type":"profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/profile"
    },
    "attributes":
    {
      "email":"user@smart.com",
      "first-name":"Cool",
      "last-name":"User"
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize his profile account by accessing the route below.

Route: *`GET "/api/v1/profile"`*

## Update

> Update Profile Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data": 
  { 
    "type":"profiles", 
    "id":"id-user-profile", 
    "attributes":
    { 
      "first-name":"Super", 
      "last-name":"User" 
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/profile

# OUTPUT
{
  "data":
  {
    "id":"id-user-profile",
    "type":"profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/profile"
    },
    "attributes":
    {
      "email":"user@smart.com",
      "first-name":"Super",
      "last-name":"User"
    }
  }
}
```

```ruby
Not implemented
```

The user can edit the information contained in his own profile account by accessing the route below.

Route: *`GET "/api/v1/profile"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Super
last-name | String | User
email | String | user@smart.com

# User Organization Profile

When logged in, the user can access his own profile. This access allows him to show and update information about his account.

## Show

> Show Organization Profile

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"organization-profiles" 
  }
}' 
http://acme.lvh.me:3000/api/v1/organization-profile

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile",
    "type":"organization-profiles",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile"
    },
    "attributes":
    {
      "name":"Fulano da Silva",
      "nickname":"Fulano",
      "organization-type":"person",
      "email":"fulano@dasilva.com"
    },
    "relationships":
    {
      "organization-profile-address":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile/relationships/organization-profile-address",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile/organization-profile-address"
        },
        "data":
        {
          "type":"organization-profile-addresses",
          "id":"id-user-organization-profile"
        }
      },
      "organization-profile-telephones":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile/relationships/organization-profile-telephones",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile/organization-profile-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize his own profile by accessing the route below.

Route: *`GET "/api/v1/organization-profile"`*

## Update

> Update Organization Profile

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "type":"organization-profiles", 
    "id":"id-user-organization-profile", 
    "attributes":
    {
      "name":"Umbrella Corporation",
      "nickname":"Umbrella",
      "organization-type":"person",
      "email":"umbrella@corp.com"
    }
  }
}' 
http://acme.lvh.me:3000/api/v1/organization-profile

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile",
    "type":"organization-profiles",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile"
    },
    "attributes":
    {
      "name":"Umbrella Corporation",
      "nickname":"Umbrella",
      "organization-type":"person",
      "email":"umbrella@corp.com"
    },
    "relationships":
    {
      "organization-profile-address":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile/relationships/organization-profile-address",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile/organization-profile-address"
        },
        "data":
        {
          "type":"organization-profile-addresses",
          "id":"id-user-organization-profile"
        }
      },
      "organization-profile-telephones":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile/relationships/organization-profile-telephones",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile/organization-profile-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can edit the information contained in his own profile by accessing the route below.

Route: *`PATCH "/api/v1/organization-profile"`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | Umbrella Corporation
nickname | String | Umbrella
organization-type | String | person
email | String | umbrella@corp.com

# User Organization Profile Telephone

When logged in, the user can access information about his telephones. This access allows him to create, update, show and list them.

## Create

> Create Organization Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"organization-profile-telephones", 
    "relationships":
    {
      "organization-profile":
      {
        "data":
        {
          "type":"organization-profiles", 
          "id":"id-user-organization-profile"
        }
      }
    }, 
    "attributes":
    {
      "country-code":"31", 
      "number":"1112223334"
    }
  }
}'  
http://acme.lvh.me:3000/api/v1/organization-profile-telephones

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile-telephone",
    "type":"organization-profile-telephones",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone"
    },
    "attributes":
    {
      "country-code":"31",
      "number":"1112223334"
    },
    "relationships":
    {
      "organization-profile":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/relationships/organization-profile",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/organization-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can create a telephone by accessing the route below.

Route: *`POST "/api/v1/organization-profile-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 31 
number | String | 1112223334

## Update

> Update Organization Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-user-organization-profile-telephone",
    "type":"organization-profile-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile-telephone",
    "type":"organization-profile-telephones",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "organization-profile":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/relationships/organization-profile",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/organization-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can edit the information contained in telephone by accessing the route below.

Route: *`PATCH "/api/v1/organization-profile-telephones/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Organization Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"organization-profile-telephones"
  }
}' 
http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile-telephone",
    "type":"organization-profile-telephones",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "organization-profile":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/relationships/organization-profile",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/organization-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize a specific telephone by accessing the route below.

Route: *`GET "/api/v1/organization-profile-telephones/:id"`*

## List

> List Organization Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"organization-profile-telephones"
  }
}' 
http://acme.lvh.me:3000/api/v1/organization-profile-telephones

# OUTPUT
{
  "data":
  [
    {
      "id":"id-user-organization-profile-telephone",
      "type":"organization-profile-telephones",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone"
      },
      "attributes":
      {
        "country-code":"12",
        "number":"789890888"
      },
      "relationships":
      {
        "organization-profile":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/relationships/organization-profile",
            "related":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/organization-profile"
          }
        }
      }
    },
    {
      "id":"id-user-organization-profile-telephone",
      "type":"organization-profile-telephones",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone"
      },
      "attributes":
      {
        "country-code":"55",
        "number":"1132578900"
      },
      "relationships":
      {
        "organization-profile":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/relationships/organization-profile",
            "related":"http://acme.lvh.me:3000/api/v1/organization-profile-telephones/id-user-organization-profile-telephone/organization-profile"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can visualize all telephones by accessing the route below.

Route: *`GET "/api/v1/organization-profile-telephones"`*

# User Organization Profile Address

When logged in, the user can access information about his address. This access allows him to create, update and show them.

## Create

> Create Organization Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"organization-profile-addresses", 
    "relationships":
    {
      "organization-profile":
      {
        "data":
        {
          "type":"organization-profiles", 
          "id":"id-user-organization-profile"
        }
      }
    }, 
    "attributes":
    {
      "street":"Jericho Tpke Suite 344", 
      "number":"2417", 
      "complement":"Apartment", 
      "zipcode":"11040", 
      "neighborhood":"Commack", 
      "city":"Garden City Park", 
      "state":"NY", 
      "country":"US"
    }
  }
}'  
http://acme.lvh.me:3000/api/v1/organization-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile-address",
    "type":"organization-profile-addresses",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile-address"
    },
    "attributes":
    {
      "street":"Jericho Tpke Suite 344",
      "number":"2417",
      "complement":"Apartment",
      "zipcode":"11040",
      "neighborhood":"Commack",
      "city":"Garden City Park",
      "state":"NY",
      "country":"US"
    },
    "relationships":
    {
      "organization-profile":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile-address/relationships/organization-profile",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile-address/organization-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can create an address by accessing the route below.

Route: *`POST "/api/v1/organization-profile-address"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Jericho Tpke Suite 344
number | String | 2417
complement | String | Apartment
zipcode | String | 11040
neighborhood | String | Commack
city | String | Garden City Park
state | String | NY
country | String | US

## Update

> Update Organization Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data": 
  { 
    "type":"organization-profile-addresses", 
    "id":"id-user-organization-profile-address", 
    "attributes":
    { 
      "street":"Baker Street", 
      "number":"221B", 
      "complement":"Apartament", 
      "zipcode":"5150117", 
      "neighborhood":"unknown", 
      "city":"Westminster", 
      "state":"London", 
      "country":"UK"
    }
  }
}' 
http://acme.lvh.me:3000/api/v1/organization-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile-address",
    "type":"organization-profile-addresses",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "organization-profile":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile-address/relationships/organization-profile",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile-address/organization-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can edit the information contained in address by accessing the route below.

Route: *`PATCH "/api/v1/organization-profile-address"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Baker Street
number | String | 221B
complement | String | Apartment
zipcode | String | 5150117
neighborhood | String | unknown
city | String | Westminster
state | String | London
country | String | UK

## Show

> Show Organization Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"organization-profile-addresses" 
  }
}' 
http://acme.lvh.me:3000/api/v1/organization-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-user-organization-profile-address",
    "type":"organization-profile-addresses",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/organization-profile-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "organization-profile":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/organization-profile-address/relationships/organization-profile",
          "related":"http://acme.lvh.me:3000/api/v1/organization-profile-address/organization-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize a specific address by accessing the route below.

Route: *`GET "/api/v1/organization-profile-address"`*

# User Select Products and Add them to His Shopping Cart

When logged in, the user can access the shop. This allows him to select products and add them to his shopping cart, to do it, the user need to create a shop cart with a relationship with a plan and after  select the product order.

## Create Shop Cart

> Create Shop Cart

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"shop-carts", 
    "relationships":
    {
      "shop-plans":
      {
        "data":
        [
          {
            "type":"shop-plans", 
            "id":"id-shop-plans"
          }
        ]
      }
    }
  }
}'  
http://smart.lvh.me:3000/api/v1/shop-carts

# OUTPUT
{
  "data":
  {
    "id":"id-user-shop-cart",
    "type":"shop-carts",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/shop-carts/id-user-shop-cart"
    },
    "relationships":
    {
      "shop-plans":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/shop-carts/id-user-shop-cart/relationships/shop-plans",
          "related":"http://smart.lvh.me:3000/api/v1/shop-carts/id-user-shop-cart/shop-plans"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can create a shop cart by accessing the route below.

Route: *`POST "/api/v1/shop-carts"`

## Create Shop Product Order

> Create Shop Product Order

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"shop-product-orders", 
    "attributes":
    { 
      "shop-cart-id":"id-user-shop-cart" 
    }
  }
}' 
http://acme.lvh.me:3000/api/v1/shop-product-orders

# OUTPUT
{
  "data":
  {
    "id":"id-user-shop-product-order",
    "type":"shop-product-orders",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/shop-product-orders/id-user-shop-product-order"
    },
    "attributes":
    {
      "period":"monthly",
      "price":0,
      "created-at":"2015-12-14T03:38:16.499Z"
    },
    "relationships":
    {
      "shop-plans":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/shop-product-orders/id-user-shop-product-order/relationships/shop-plans",
          "related":"http://acme.lvh.me:3000/api/v1/shop-product-orders/id-user-shop-product-order/shop-plans"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can create a shop product order by accessing the route bellow.

Route: *`POST "/api/v1/shop-product-orders"`*

Variable | Type | Value
-------- | ---- | ----- 
shop-cart-id | String | id-user-shop-cart

# User Shop Category

When logged in, the user can access information about the shop. This access allows him to show and list shop categories.

## Show

> Show Shop Category

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"shop-categories" 
  }
}' 
http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category

# OUTPUT
{
  "data":
  {
    "id":"id-shop-category",
    "type":"shop-categories",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category"
    },
    "attributes":
    {
      "name":"Smart Email",
      "enabled":true,
      "description":"Smart Email",
      "long-description":"Smart Email Description",
      "slug":"email",
      "icon":"fa fa-envelope-o"
    },
    "relationships":
    {
      "shop-groups":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category/relationships/shop-groups",
          "related":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category/shop-groups"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize a specific category created by accessing the route below.

Route: *`GET "/api/v1/shop-categories/:id"`*

## List

> List Shop Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"shop-categories" 
  }
}' 
http://smart.lvh.me:3000/api/v1/shop-categories

# OUTPUT
{
  "data":
  [
    {
      "id":"id-shop-category",
      "type":"shop-categories",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category"
      },
      "attributes":
      {
        "name":"Smart Email",
        "enabled":true,
        "description":"Smart Email",
        "long-description":"Smart Email Description",
        "slug":"email",
        "icon":"fa fa-envelope-o"
      },
      "relationships":
      {
        "shop-groups":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category/relationships/shop-groups",
            "related":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category/shop-groups"
          }
        }
      }
    },
    {
      "id":"id-shop-category",
      "type":"shop-categories",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category"
      },
      "attributes":
      {
        "name":"Smart Server",
        "enabled":true,
        "description":"Smart IaaS",
        "long-description":"Smart IaaS Description",
        "slug":"server",
        "icon":"fa fa-cloud"
      },
      "relationships":
      {
        "shop-groups":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category/relationships/shop-groups",
            "related":"http://smart.lvh.me:3000/api/v1/shop-categories/id-shop-category/shop-groups"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can visualize all shop categories created by accessing the route below.

Route: *`GET "/api/v1/shop-categories"`*

# User Shop Group

When logged in, the user can access information about the shop. This access allows him to show and list shop groups.

## Show

> Show Shop Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json"
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"shop-groups" 
  }
}' 
http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group

# OUTPUT
{
  "data":
  {
    "id":"id-shop-group",
    "type":"shop-groups",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group"
    },
    "attributes":
    {
      "name":"Smart Cloud Servers",
      "enabled":true,
      "description":"Smart Cloud Servers Desc",
      "long-description":"Smart Cloud Servers Long Desc",
      "slug":"cloud-server",
      "icon":"fa fa-cloud"
    },
    "relationships":
    {
      "shop-category":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/relationships/shop-category",
          "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/shop-category"
        },
        "data":
        {
          "type":"shop-categories",
          "id":"id-shop-category"
        }
      },
      "shop-plans":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/relationships/shop-plans",
          "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/shop-plans"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize a specific group created by accessing the route below.

Route: *`GET "/api/v1/shop-groups/:id"`*

## List

> List Shop Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json"
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"shop-groups" 
  }
}' 
http://smart.lvh.me:3000/api/v1/shop-groups

# OUTPUT
{
  "data":
  [
    {
      "id":"id-shop-group",
      "type":"shop-groups",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group"
      },
      "attributes":
      {
        "name":"Smart Cloud Servers",
        "enabled":true,
        "description":"Smart Cloud Servers Desc",
        "long-description":"Smart Cloud Servers Long Desc",
        "slug":"cloud-server",
        "icon":"fa fa-cloud"
      },
      "relationships":
      {
        "shop-category":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/relationships/shop-category",
            "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/shop-category"
          },
          "data":
          {
            "type":"shop-categories",
            "id":"id-shop-category"
          }
        },
        "shop-plans":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/relationships/shop-plans",
            "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/shop-plans"
          }
        }
      }
    },
    {
      "id":"id-shop-group",
      "type":"shop-groups",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group"
      },
      "attributes":
      {
        "name":"Smart Email Hotmail",
        "enabled":true,
        "description":"Smart Email Hotmail Desc",
        "long-description":"Smart Email Hotmail Long Desc",
        "slug":"email-hotmail",
        "icon":"fa fa-windows"
      },
      "relationships":
      {
        "shop-category":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/relationships/shop-category",
            "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/shop-category"
          },
          "data":
          {
            "type":"shop-categories",
            "id":"id-shop-category"
          }
        },
        "shop-plans":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/relationships/shop-plans",
            "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-shop-group/shop-plans"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can visualize all shop groups created by accessing the route below.

Route: *`GET "/api/v1/shop-groups"`*

# User Shop Plan

When logged in, the user can access information about the shop. This access allows him to list shop plans.

## List

> List Shop Plan

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-plans"
  }
}' 
http://acme.lvh.me:3000/api/v1/shop-plans

# OUTPUT
{
  "data":
  [
    {
      "id":"id-shop-plan",
      "type":"shop-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Small)",
        "enabled":true,
        "values":
        {
          "disk_1_san":"25 GB (SAN)",
          "disk_2_san":null,
          "disk_3_san":null,
          "disk_4_san":null,
          "disk_5_san":null,
          "disk_1_local":null,
          "disk_2_local":null,
          "disk_type":"san",
          "datacenter":"wdc01",
          "memory":"2 GB",
          "processor":"4 x 2.0 GHz Cores",
          "operating_system":"Debian - Latest (64 bit)",
          "network_component":"1 Gbps Public \u0026 Private Network Uplinks"
        },
        "description":"Acme Cloud Server Small Desc",
        "long-description":"Acme Cloud Server Small Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "product-name":"cloud_server",
        "product-provider":"softlayer",
        "hourly-price":"0.48",
        "monthly-price":"300.0"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-group"
          }
        }
      }
    },
    {
      "id":"id-shop-plan",
      "type":"shop-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Large)",
        "enabled":true,
        "values":
        {
          "disk_1_san":"100 GB (SAN)",
          "disk_2_san":null,
          "disk_3_san":null,
          "disk_4_san":null,
          "disk_5_san":null,
          "disk_1_local":null,
          "disk_2_local":null,
          "disk_type":"san",
          "datacenter":"wdc01",
          "memory":"6 GB",
          "processor":"8 x 2.0 GHz Cores",
          "operating_system":"Debian - Latest (64 bit)",
          "network_component":"1 Gbps Public \u0026 Private Network Uplinks"
        },
        "description":"Acme Cloud Server Large Desc",
        "long-description":"Acme Cloud Server Large Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "product-name":"cloud_server",
        "product-provider":"softlayer",
        "hourly-price":"0.972",
        "monthly-price":"624.87"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-group"
          }
        }
      }
    },
    {
      "id":"id-shop-plan",
      "type":"shop-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Medium)",
        "enabled":true,
        "values":
        {
          "disk_1_san":"25 GB (SAN)",
          "disk_2_san":null,
          "disk_3_san":null,
          "disk_4_san":null,
          "disk_5_san":null,
          "disk_1_local":null,
          "disk_2_local":null,
          "disk_type":"san",
          "datacenter":"wdc01",
          "memory":"4 GB",
          "processor":"8 x 2.0 GHz Cores",
          "operating_system":"Debian - Latest (64 bit)",
          "network_component":"1 Gbps Public \u0026 Private Network Uplinks"
        },
        "description":"Acme Cloud Server Medium Desc",
        "long-description":"Acme Cloud Server Medium Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "product-name":"cloud_server",
        "product-provider":"softlayer",
        "hourly-price":"0.843",
        "monthly-price":"540.0"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/shop-plans/id-shop-plan/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-group"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can visualize all shop plans created by accessing the route below.

Route: *`GET "/api/v1/shop-plans"`*

# User Shop Plan Softlayer Cloud Server

When logged in, the user can access information about the shop. This access allows him to create, show and list shop plans Softlayer cloud server.

## Create

> Create Shop Plan Softlayer Cloud Server

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"shop-softlayer-cloud-server-plans", 
    "attributes":
    { 
      "description":"Small", 
      "long-description":"Cloud Server Small", 
      "disk-1-san":"25 GB (SAN)", 
      "disk-2-san":"10 GB (SAN)", 
      "disk-3-san":"10 GB (SAN)", 
      "disk-type":"san", 
      "datacenter":"wdc01", 
      "memory":"2 GB", 
      "processor":"4 x 2.0 GHz Cores", 
      "operating-system":"Debian - Latest (64 bit)", 
      "network-component":"1 Gbps Public & Private Network Uplinks" 
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans

# OUTPUT
{
  "data":
  {
    "id":"id-plan-softlayer-cloud-server",
    "type":"shop-softlayer-cloud-server-plans",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server"
    },
    "attributes":
    {
      "name":null,
      "enabled":true,
      "description":"Small",
      "long-description":"Cloud Server Small",
      "allow-custom":false,
      "can-customize":[],
      "disk-1-san":"25 GB (SAN)",
      "disk-2-san":"10 GB (SAN)",
      "disk-3-san":"10 GB (SAN)",
      "disk-4-san":null,
      "disk-5-san":null,
      "disk-1-local":null,
      "disk-2-local":null,
      "disk-type":"san",
      "datacenter":"wdc01",
      "memory":"2 GB",
      "processor":"4 x 2.0 GHz Cores",
      "operating-system":"Debian - Latest (64 bit)",
      "network-component":"1 Gbps Public \u0026 Private Network Uplinks",
      "hourly-price":"0.522",
      "monthly-price":"327.42",
      "product-name":"cloud_server",
      "product-provider":"softlayer"
    },
    "relationships":
    {
      "shop-group":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/relationships/shop-group",
          "related":"http://smart.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/shop-group"
        },
        "data":null
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can create a Softlayer Cloud Server plan accessing the route below.

Route: *`POST "/api/v1/shop-softlayer-cloud-server-plans"`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | name
enabled | String | true
description | String | Small
long-description | String | Cloud Server Small
allow-custom | String | false
can-customize | String | [ ]
disk-1-san | String | 25 GB (SAN)
disk-2-san | String | 10 GB (SAN)
disk-3-san | String | 10 GB (SAN)
disk-4-san | String | 10 GB (SAN)
disk-5-san | String | 10 GB (SAN)
disk-1-local | String | 10 GB (SAN)
disk-2-local | String | 10 GB (SAN)
disk-type | String | san
datacenter | String | wdc01
memory | String | 2 GB
processor | String | 4 x 2.0 GHz Cores
operating-system | String | Debian - Latest (64 bit)
network-component | String | 1 Gbps Public \u0026 Private Network Uplinks

## Show

> Show Shop Plan Softlayer Cloud Server

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-softlayer-cloud-server-plans"
  }
}' 
http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server

# OUTPUT
{
  "data":
  {
    "id":"id-plan-softlayer-cloud-server",
    "type":"shop-softlayer-cloud-server-plans",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server"
    },
    "attributes":
    {
      "name":null,
      "enabled":true,
      "description":"Small",
      "long-description":"Cloud Server Small",
      "allow-custom":false,
      "can-customize":[],
      "disk-1-san":"25 GB (SAN)",
      "disk-2-san":"10 GB (SAN)",
      "disk-3-san":"10 GB (SAN)",
      "disk-4-san":null,
      "disk-5-san":null,
      "disk-1-local":null,
      "disk-2-local":null,
      "disk-type":"san",
      "datacenter":"wdc01",
      "memory":"2 GB",
      "processor":"4 x 2.0 GHz Cores",
      "operating-system":"Debian - Latest (64 bit)",
      "network-component":"1 Gbps Public \u0026 Private Network Uplinks",
      "hourly-price":"0.522",
      "monthly-price":"327.42",
      "product-name":"cloud_server",
      "product-provider":"softlayer"
    },
    "relationships":
    {
      "shop-group":
      {
        "links":
        {
          "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/relationships/shop-group",
          "related":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/shop-group"
        },
        "data":null
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can get information for a specific SoftLayer Cloud Server plan accessing the route bellow.

Route: *`GET "/api/v1/shop-softlayer-cloud-server-plans/:id"`*

## List

> List Shop Plan Softlayer Cloud Server

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-softlayer-cloud-server-plans"
  }
}' 
http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans

# OUTPUT
{
  "data":
  [
    {
      "id":"id-plan-softlayer-cloud-server",
      "type":"shop-softlayer-cloud-server-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Small)",
        "enabled":true,
        "description":"Acme Cloud Server Small Desc",
        "long-description":"Acme Cloud Server Small Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "disk-1-san":"25 GB (SAN)",
        "disk-2-san":null,
        "disk-3-san":null,
        "disk-4-san":null,
        "disk-5-san":null,
        "disk-1-local":null,
        "disk-2-local":null,
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"2 GB",
        "processor":"4 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public \u0026 Private Network Uplinks",
        "hourly-price":"0.48",
        "monthly-price":"300.0",
        "product-name":"cloud_server",
        "product-provider":"softlayer"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-group"
          }
        }
      }
    },
    {
      "id":"id-plan-softlayer-cloud-server",
      "type":"shop-softlayer-cloud-server-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Large)",
        "enabled":true,"description":"Acme Cloud Server Large Desc",
        "long-description":"Acme Cloud Server Large Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "disk-1-san":"100 GB (SAN)",
        "disk-2-san":null,
        "disk-3-san":null,
        "disk-4-san":null,
        "disk-5-san":null,
        "disk-1-local":null,
        "disk-2-local":null,
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"6 GB",
        "processor":"8 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public \u0026 Private Network Uplinks",
        "hourly-price":"0.972",
        "monthly-price":"624.87",
        "product-name":"cloud_server",
        "product-provider":"softlayer"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-group"
          }
        }
      }
    },
    {
      "id":"id-plan-softlayer-cloud-server",
      "type":"shop-softlayer-cloud-server-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Medium)",
        "enabled":true,
        "description":"Acme Cloud Server Medium Desc",
        "long-description":"Acme Cloud Server Medium Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "disk-1-san":"25 GB (SAN)",
        "disk-2-san":null,
        "disk-3-san":null,
        "disk-4-san":null,
        "disk-5-san":null,
        "disk-1-local":null,
        "disk-2-local":null,
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"4 GB",
        "processor":"8 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public \u0026 Private Network Uplinks",
        "hourly-price":"0.843",
        "monthly-price":"540.0",
        "product-name":"cloud_server",
        "product-provider":"softlayer"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/shop-softlayer-cloud-server-plans/id-plan-softlayer-cloud-server/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-group"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```
The user can list all SoftLayer Cloud Server plans accessing the route bellow.

Route: *`GET "/api/v1/shop-softlayer-cloud-server-plans"`*

# User Shop Price

When logged in, the user can access information about the shop. This access allows him to verify a price for the custom plan.

## Create

> Create Shop Price

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"shop-prices", 
    "attributes":
    { 
      "components":
      {
        "disk-1-san":"25 GB (SAN)",
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"2 GB",
        "processor":"4 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public & Private Network Uplinks"
      },
      "product":"cloud-server",
      "provider":"softlayer"
    }
  }
}' 
http://acme.lvh.me:3000/api/v1/shop-price

# OUTPUT
{
  "data":
  {
    "id":null,
    "type":"shop-prices",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/shop-prices/"
    },
    "attributes":
    {
      "components":
      {
        "disk-1-san":"25 GB (SAN)",
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"2 GB",
        "processor":"4 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public \u0026 Private Network Uplinks"
      },
      "hourly-price":"0.48",
      "monthly-price":"300.0",
      "product":"cloud-server",
      "provider":"softlayer"
    }
  }
}
```

```ruby
Not implemented
```

The user can create a Shop Price accessing the route below.

Route: *`POST "/api/v1/shop-price"`*

Variable | Type | Value
-------- | ---- | ----- 
disk-1-san | String | 25 GB (SAN)
disk-type | String | san
datacenter | String | wdc01
memory | String | 2 GB
processor | String | 4 x 2.0 GHz Cores
operating-system | String | Debian - Latest (64 bit)
network-component | String | 1 Gbps Public & Private Network Uplinks
product | String | product_example_cloud-server
provider | String | provider_example_softlayer

# User Shop Catalog Provider

When logged in, the user can access information about the catalog. This access allows him to list his catalog provider availables.

## Show

> Show Shop Catalog Provider

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-providers" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider

# OUTPUT
{
  "data":
  {
    "id":"id-catalog-provider",
    "type":"catalog-providers",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider"
    },
    "attributes":
    {
      "name":"Provider",
      "provider-name":"provider"
    },
    "relationships":
    {
      "catalog-products":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider/relationships/catalog-products",
          "related":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider/catalog-products"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

When logged in, the user can access information about the catalog. This access allows him to show catalog provider availables.

route: *`GET "/api/v1/catalog-providers/:id"`*

## List

> List Shop Catalog Provider

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-providers" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-providers

# OUTPUT
{
  "data":
  [
    {
      "id":"id-catalog-provider",
      "type":"catalog-providers",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider"
      },
      "attributes":
      {
        "name":"Provider",
        "provider-name":"provider"
      },
      "relationships":
      {
        "catalog-products":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider/relationships/catalog-products",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider/catalog-products"
          }
        }
      }
    },
    {
      "id":"id-catalog-provider",
      "type":"catalog-providers",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider"
      },
      "attributes":
      {
        "name":"SoftLayer",
        "provider-name":"softlayer"
      },
      "relationships":
      {
        "catalog-products":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider/relationships/catalog-products",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-providers/id-catalog-provider/catalog-products"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

When logged in, the user can access information about the catalog. This access allows him to list catalog provider availables.

route: *`GET "/api/v1/catalog-providers"`*

# User Shop Catalog Provider Product

When logged in, the user can access information about the catalog. This access allows him to show and list catalog provider products.

## Show

> Show Shop Catalog Provider Product

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-products" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product

# OUTPUT
{
  "data":
  {
    "id":"id-catalog-provider-product",
    "type":"catalog-products",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product"
    },
    "attributes":
    {
      "name":"Bare Metal",
      "slug":"bare-metal",
      "dynamic":true,
      "hourly":true,
      "version":1,
      "allow-custom":true,
      "product-name":"bare_metal",
      "provider-name":"softlayer"
    },
    "relationships":
    {
      "catalog-provider":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-provider",
          "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-provider"
        },
        "data":
        {
          "type":"catalog-providers",
          "id":"id-catalog-provider"
        }
      },
      "catalog-components":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-components",
          "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-components"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize a specific provider products by accessing the route below.

route: *`GET "/api/v1/catalog-products/:id"`*

## List

> List Shop Catalog Provider Product

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-products" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-products

# OUTPUT
{
  "data":
  [
    {
      "id":"id-catalog-provider-product",
      "type":"catalog-products",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product"
      },
      "attributes":
      {
        "name":"Bare Metal",
        "slug":"bare-metal",
        "dynamic":true,
        "hourly":true,
        "version":1,
        "allow-custom":true,
        "product-name":"bare_metal",
        "provider-name":"softlayer"
      },
      "relationships":
      {
        "catalog-provider":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-provider",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-provider"
          },
          "data":
          {
            "type":"catalog-providers",
            "id":"id-catalog-provider"
          }
        },
        "catalog-components":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-components",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-components"
          }
        }
      }
    },
    {
      "id":"id-catalog-provider-product",
      "type":"catalog-products",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product"
      },
      "attributes":
      {
        "name":"Cloud Server",
        "slug":"cloud-server",
        "dynamic":true,
        "hourly":true,
        "version":1,
        "allow-custom":true,
        "product-name":"cloud_server",
        "provider-name":"softlayer"
      },
      "relationships":
      {
        "catalog-provider":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-provider",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-provider"
          },
          "data":
          {
            "type":"catalog-providers",
            "id":"id-catalog-provider"
          }
        },
        "catalog-components":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-components",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-components"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can visualize all providers products by accessing the route below.

route: *`GET "/api/v1/catalog-products"`*

# User Shop Catalog Provider Product Attribute

When logged in, the user can access information about the catalog. This access allows him to show and list catalog products attributes.

## Show

> Show Shop Catalog Provider Product Attributes

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-components" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-components

# OUTPUT
{
  "data":
  {
    "id":"id-catalog-provider-product-attribute",
    "type":"catalog-components",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute"
    },
    "attributes":
    {
      "name":"Disk 1 (Local)",
      "system":false,
      "allow-upgrade":true,
      "allow-downgrade":false
    },
    "relationships":
    {
      "catalog-product":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/relationships/catalog-product",
          "related":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/catalog-product"
        },
        "data":
        {
          "type":"catalog-products",
          "id":"id-catalog-provider-product"
        }
      },
      "catalog-component-options":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/relationships/catalog-component-options",
          "related":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/catalog-component-options"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize a specific product attributes by accessing the route below.

route: *`GET "/api/v1/catalog-components/:id"`*

## List

> List Shop Catalog Provider Product Attributes

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-components" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute

# OUTPUT
{
  "data":
  [
    {
      "id":"id-catalog-provider-product-attribute",
      "type":"catalog-components",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute"
      },
      "attributes":
      {
        "name":"Disk 1 (Local)",
        "system":false,
        "allow-upgrade":true,
        "allow-downgrade":false
      },
      "relationships":
      {
        "catalog-product":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/relationships/catalog-product",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/catalog-product"
          },
          "data":
          {
            "type":"catalog-products",
            "id":"id-catalog-provider-product"
          }
        },
        "catalog-component-options":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/relationships/catalog-component-options",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/catalog-component-options"
          }
        }
      }
    },
    {
      "id":"id-catalog-provider-product-attribute",
      "type":"catalog-components",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute"
      },
      "attributes":
      {
        "name":"Datacenter",
        "system":false,
        "allow-upgrade":false,
        "allow-downgrade":false
      },
      "relationships":
      {
        "catalog-product":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/relationships/catalog-product",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/catalog-product"
          },
          "data":
          {
            "type":"catalog-products",
            "id":"id-catalog-provider-product"
          }
        },
        "catalog-component-options":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/relationships/catalog-component-options",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-components/id-catalog-provider-product-attribute/catalog-component-options"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can visualize all providers products attributes by accessing the route below.

route: *`GET "/api/v1/catalog-components"`*

# User Shop Catalog Provider Product Option

When logged in, the user can access information about the catalog. This access allows him to list catalog products options.

## List

> List Shop Catalog Provider Product Options

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-component-options" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-components/id-admin-catalog-provider-product-attribute/catalog-component-options

# OUTPUT
{
  "data":
  [
    {
      "id":"id-catalog-provider-product-option",
      "type":"catalog-component-options",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-component-options/id-catalog-provider-product-option"
      },
      "attributes":
      {
        "name":"1 Gbps Private Network Uplink",
        "value":"1 Gbps Private Network Uplink",
        "hourly-price":null,
        "monthly-price":null,
        "dynamic-hourly-price":"0.02",
        "dynamic-monthly-price":"10.0"
      },
      "relationships":
      {
        "catalog-component":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-component-options/id-catalog-provider-product-option/relationships/catalog-component",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-component-options/id-catalog-provider-product-option/catalog-component"
          },
          "data":
          {
            "type":"catalog-components",
            "id":"id-catalog-provider-product-attribute"
          }
        }
      }
    },
    {
      "id":"id-catalog-provider-product-option",
      "type":"catalog-component-options",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-component-options/id-catalog-provider-product-option"
      },
      "attributes":
      {
        "name":"10 Mbps Public \u0026 Private Network Uplinks",
        "value":"10 Mbps Public \u0026 Private Network Uplinks",
        "hourly-price":null,
        "monthly-price":null,
        "dynamic-hourly-price":"0.0",
        "dynamic-monthly-price":"0.0"
      },
      "relationships":
      {
        "catalog-component":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-component-options/id-catalog-provider-product-option/relationships/catalog-component",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-component-options/id-catalog-provider-product-option/catalog-component"
          },
          "data":
          {
            "type":"catalog-components",
            "id":"id-catalog-provider-product-attribute"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can visualize all providers products options by accessing the route below.

route: *`GET "/api/v1/catalog-components/id-catalog-provider-product-attribute/catalog-component-options"`*

# User Filter

When logged in, the user can access information about the shop. This access allows him list a specific group through a filter in the end of the url.

*`?filter%5Bvariable%5D=value`*

## Group

> Filter Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-groups"
  }
}' 
http://smart.lvh.me:3000/api/v1/shop-groups?filter%5Bslug%5D=cloud-server

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-shop-group",
      "type":"shop-groups",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-admin-shop-group"
      },
      "attributes":
      {
        "name":"Smart Cloud Servers",
        "enabled":true,
        "description":"Smart Cloud Servers Desc",
        "long-description":"Smart Cloud Servers Long Desc",
        "slug":"cloud-server",
        "icon":"fa fa-cloud"
      },
      "relationships":
      {
        "shop-category":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-admin-shop-group/relationships/shop-category",
            "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-admin-shop-group/shop-category"
          },
          "data":
          {
            "type":"shop-categories",
            "id":"id-admin-shop-category"
          }
        },
        "shop-plans":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-groups/id-admin-shop-group/relationships/shop-plans",
            "related":"http://smart.lvh.me:3000/api/v1/shop-groups/id-admin-shop-group/shop-plans"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can filter a group by accessing the route below.

Route: *`GET "/api/v1/shop-groups?filter%5Bslug%5D=cloud-server"`*

* slug

## Category

> Filter Category

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-categories"
  }
}' 
http://smart.lvh.me:3000/api/v1/shop-categories?filter%5Bslug%5D=email

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-shop-category",
      "type":"shop-categories",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-admin-shop-category"
      },
      "attributes":
      {
        "name":"Smart Email",
        "enabled":true,
        "description":"Smart Email",
        "long-description":"Smart Email Description",
        "slug":"email",
        "icon":"fa fa-envelope-o"
      },
      "relationships":
      {
        "shop-groups":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/shop-categories/id-admin-shop-category/relationships/shop-groups",
            "related":"http://smart.lvh.me:3000/api/v1/shop-categories/id-admin-shop-category/shop-groups"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can filter a category by accessing the route below.

Route: *`GET "/api/v1/shop-categories?filter%5Bslug%5D=email"`*

* slug

## Shop Catalog Provider Product

> Filter Shop Catalog Provider Product

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-products" 
  }
}' 
http://smart.lvh.me:3000/api/v1/catalog-products?filter%5Bprovider_name%5D=softlayer

# OUTPUT
{
  "data":
  [
    {
      "id":"id-catalog-provider-product",
      "type":"catalog-products",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product"
      },
      "attributes":
      {
        "name":"Bare Metal",
        "slug":"bare-metal",
        "dynamic":true,
        "hourly":true,
        "version":1,
        "allow-custom":true,
        "product-name":"bare_metal",
        "provider-name":"softlayer"
      },
      "relationships":
      {
        "catalog-provider":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-provider",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-provider"
          },
          "data":
          {
            "type":"catalog-providers",
            "id":"id-catalog-provider"
          }
        },
        "catalog-components":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/relationships/catalog-components",
            "related":"http://smart.lvh.me:3000/api/v1/catalog-products/id-catalog-provider-product/catalog-components"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The user can filter a provider products by accessing the route below.

Route: *`GET "/api/v1/catalog-products?filter%5Bprovider_name%5D=softlayer"`*

* product_name
* provider_name

# Admin Profile Account

When logged in, the user admin access his own profile. This access allows him to show and update information about his account.

## Show

> Show Profile Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/profile

# OUTPUT
{
  "data":
  {
    "id":"id-admin-profile",
    "type":"profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/profile"
    },
    "attributes":
    {
      "email":"admin@smart.com",
      "first-name":"Power",
      "last-name":"Admin"
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize his profile account by accessing the route below.

Route: *`GET "/api/v1/admin/profile"`*

## Update

> Update Profile Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  { 
    "type":"profiles", 
    "id":"id-admin-profile", 
    "attributes":
    { 
      "first-name":"Admin", 
      "last-name":"Nice"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/profile

# OUTPUT
{
  "data":
  {
    "id":"id-admin-profile",
    "type":"profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/profile"
    },
    "attributes":
    {
      "email":"admin@smart.com",
      "first-name":"Admin",
      "last-name":"Nice"
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit the information contained in his own profile account by accessing the route below.

Route: *`GET "/api/v1/admin/profile"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Admin
last-name  | String | Nice
email | String | admin@smart.com

# Admin Company Profile

When logged in, the admin can access his own profile. This access allows him to show and update information about his account.

## Show

> Show Company Profile

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profiles"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company",
    "type":"company-profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile"
    },
    "attributes":
    {
      "corporate-name":"Smart Inc.",
      "trade-name":"Smart",
      "email":"hello@smart.com"
    },
    "relationships":
    {
      "company-profile-address":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile/relationships/company-profile-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile/company-profile-address"
        },
        "data":
        {
          "type":"company-profile-addresses",
          "id":"id-admin-company"
        }
      },
      "company-profile-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile/relationships/company-profile-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile/company-profile-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize his own profile by accessing the route below.

Route: *`GET "/api/v1/admin/company-profile"`*

## Update

> Update Company Profile

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "type":"company-profiles", 
    "id":"id-admin-company", 
    "attributes":
    {
      "corporate-name":"Umbrella Corporation",
      "trade-name":"Umbrella",
      "email":"umbrella@corp.com"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company",
    "type":"company-profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile"
    },
    "attributes":
    {
      "corporate-name":"Umbrella Corporation",
      "trade-name":"Umbrella",
      "email":"umbrella@corp.com"
    },
    "relationships":
    {
      "company-profile-address":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile/relationships/company-profile-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile/company-profile-address"
        },
        "data":
        {
          "type":"company-profile-addresses","id":"id-admin-company"
        }
      },
      "company-profile-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile/relationships/company-profile-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile/company-profile-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit the information contained in his own profile by accessing the route below.

Route: *`PATCH "/api/v1/admin/company-profile"`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | Umbrella Corporation
trade-name | String | Umbrella
email | String | umbrella@corp.com

# Admin Company Profile Telephone

When logged in, the admin can access information about his telephones. This access allows him to create, update, show and list them.

## Create

> Create Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"company-profile-telephones", 
    "relationships":
    {
      "company-profile":
      {
        "data":
        {
          "type":"company-profiles", 
          "id":"id-admin-company"
        }
      }
    }, 
    "attributes":
    {
      "country-code":"55", 
      "number":"1112223334"
    }
  }
}'  
http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company-telephone",
    "type":"company-profile-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone"
    },
    "attributes":
    {
      "country-code":"55",
      "number":"1112223334"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone/relationships/company-profile",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can create a telephone by accessing the route below.

Route: *`POST "/api/v1/admin/company-profile-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 55 
number | String | 1112223334

## Update

> Update Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-admin-company-telephone",
    "type":"company-profile-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company-telephone",
    "type":"company-profile-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone/relationships/company-profile",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit the information contained in telephone by accessing the route below.

Route: *`PATCH "/api/v1/admin/company-profile-telephones/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company-telephone",
    "type":"company-profile-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone/relationships/company-profile",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone/company-profile"
        }
      }
    }
  }
} 
```

```ruby
Not implemented
```

The admin can visualize a specific telephone by accessing the route below.

Route: *`GET "/api/v1/admin/company-profile-telephones/:id"`*

## List

> List Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-telephones

# OUTPUT
{
  "data":
  [
    {
      "id":"id-manager-company-telephone",
      "type":"company-profile-telephones",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone"
      },
      "attributes":
      {
        "country-code":"55",
        "number":"1112223334"
      },
      "relationships":
      {
        "company-profile":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/relationships/company-profile",
            "related":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/company-profile"
          }
        }
      }
    },
    {
      "id":"id-manager-company-telephone",
      "type":"company-profile-telephones",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone"
      },
      "attributes":
      {
        "country-code":"89",
        "number":"1222333444"
      },
      "relationships":
      {
        "company-profile":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/relationships/company-profile",
            "related":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/company-profile"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all telephones by accessing the route below.

Route: *`GET "/api/v1/manager/company-profile-telephones"`*

# Admin Company Profile Address

When logged in, the admin can access information about his address. This access allows him to create, update and show them.

## Create

> Create Company Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"company-profile-addresses", 
    "relationships":
    {
      "company-profile":
      {
        "data":
        {
          "type":"company-profiles", 
          "id":"id-admin-company"
        }
      }
    }, 
    "attributes":
    {
      "street":"Jericho Tpke Suite 344", 
      "number":"2417", 
      "complement":"Apartment", 
      "zipcode":"11040", 
      "neighborhood":"Commack", 
      "city":"Garden City Park", 
      "state":"NY", 
      "country":"US"
    }
  }
}'  
http://smart.lvh.me:3000/api/v1/admin/company-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company-address",
    "type":"company-profile-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address"
    },
    "attributes":
    {
      "street":"Jericho Tpke Suite 344",
      "number":"2417",
      "complement":"Apartment",
      "zipcode":"11040",
      "neighborhood":"Commack",
      "city":"Garden City Park",
      "state":"NY",
      "country":"US"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address/relationships/company-profile",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can create an address by accessing the route below.

Route: *`POST "/api/v1/admin/company-profile-address"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Baker Street
number | String | 221B
complement | String | Apartment
zipcode | String | 5150117
neighborhood | String | unknown
city | String | Westminster
state | String | London
country | String | UK

## Update

> Update Company Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data": 
  { 
    "type":"company-profile-addresses", 
    "id":"id-admin-company-address", 
    "attributes":
    { 
      "street":"Baker Street", 
      "number":"221B", 
      "complement":"Apartament", 
      "zipcode":"5150117", 
      "neighborhood":"unknown", 
      "city":"Westminster", 
      "state":"London", 
      "country":"UK"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company-address",
    "type":"company-profile-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address/relationships/company-profile",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit the information contained in address by accessing the route below.

Route: *`PATCH "/api/v1/admin/company-profile-address"`*

Variable | Type | Value
---------- | ---- | ----- 
street | String | Jericho Tpke Suite 344 
number | String | 2417
complement | String | Apartment
zipcode | String | 11040 
neighborhood | String | Commack
city | String | Garden City Park
state | String | NY  
country | String | US

## Show

> Show Company Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"company-profile-addresses" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-admin-company-address",
    "type":"company-profile-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address/relationships/company-profile",
          "related":"http://smart.lvh.me:3000/api/v1/admin/company-profile-address/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific address by accessing the route below.

Route: *`GET "/api/v1/admin/company-profile-address"`*

# Admin Client User Account

When logged in, the admin can access information about users account. This access allows him to create, update, show and list them.

## Create

> Create Client User Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"client-users", 
    "attributes":
    { 
      "first-name":"My",
      "last-name":"User",
      "email":"my@user.com",
      "password":"pass1234",
      "password-confirmation":"pass1234" 
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-users

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-client-user-profile"
    },
    "attributes":
    {
      "first-name":"My",
      "last-name":"User",
      "email":"my@user.com"
    }
  }
}
```

```ruby
Not implemented
```

The admin can create an user account by accessing the route below.

Route: *`POST "/api/v1/admin/client-users"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | My
last-name | String | User
email | String | my@user.com
password | String | pass1234
password-confirmation | String | pass1234

## Update

> Update Client User Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  { 
    "type":"client-users", 
    "id":"id-admin-client-user-profile", 
    "attributes":
    { 
      "first-name":"Admin", 
      "last-name":"Nice",
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-client-user-profile

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-client-user-profile"
    },
    "attributes":
    {
      "first-name":"Admin",
      "last-name":"Nice",
      "email":"my@user.com"
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit information contained in an user account by accessing the route below.

Route: *`GET "/api/v1/admin/client-users/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Admin 
last-name | String | Nice

## Show

> Show Client User Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-client-user-profile

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-client-user-profile"
    },
    "attributes":
    {
      "first-name":"Admin",
      "last-name":"Nice",
      "email":"my@user.com"
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific user account by accessing the route below.

Route: *`GET "/api/v1/admin/client-users/:id"`*

## List

> List Client User Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-users

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-client-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-client-user-profile"
      },
      "attributes":
      {
        "first-name":"Super",
        "last-name":"User",
        "email":"user@smart.com"
      }
    },
    {
      "id":"id-admin-client-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-client-user-profile"
      },
      "attributes":
      {
        "first-name":"Admin",
        "last-name":"Nice",
        "email":"my@user.com"
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all users accounts by accessing the route below.

Route: *`GET "/api/v1/admin/client-users"`*

# Admin Client User

When logged in, the admin can access information about Users. This access allows him to create, update, show and list them.

## Create

> Show Client User

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"clients", 
    "attributes":
    { 
      "name":"Apple Inc",
      "nickname":"Apple",
      "organization-type":"company",
      "email":"contact@apple.com",
      "owner-id": "id-admin-profile"
    }
  }
}' 
http://smart.lvh.me:3000//api/v1/admin/clients

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user",
    "type":"clients",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user"
    },
    "attributes":
    {
      "name":"Apple Inc",
      "nickname":"Apple",
      "organization-type":"company",
      "email":"contact@apple.com",
      "created-at":"2015-11-13T13:16:19.972Z",
      "updated-at":"2015-11-13T13:16:19.972Z"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/relationships/client-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/client-address"
        },
        "data":null
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/relationships/client-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can create a User by accessing the route below.

Route: *`POST "/api/v1/admin/clients"`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | Apple Inc
nickname | String | Apple
organization-type | String | company
email | String | contact@apple.com
owner-id | UUID | id-admin-profile

## Update

> Update Client User

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "id":"id-admin-client-user", 
    "type":"clients", 
    "attributes":
    { 
      "name":"Wayne Enterprise",
      "nickname":"Wayne"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user",
    "type":"clients",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user"
    },
    "attributes":
    {
      "name":"Wayne Enterprise",
      "nickname":"Wayne",
      "organization-type":"company",
      "email":"contato@empresasmart.com.br",
      "created-at":"2015-11-13T01:05:31.000Z",
      "updated-at":"2015-11-13T13:33:47.644Z"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/relationships/client-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-admin-client-user"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/relationships/client-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit an information contained in an user by accessing the route below.

Route: *`PATCH "/api/v1/admin/clients/:id`*

Variable | Type | Value
-------- | ---- | ----- 
name | String |Wayne Enterprise
nickname | String | Wayne

## Show

> Show Client User

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user",
    "type":"clients",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user"
    },
    "attributes":
    {
      "name":"Wayne Enterprise",
      "nickname":"Wayne",
      "organization-type":"company",
      "email":"contato@empresasmart.com.br",
      "created-at":"2015-11-13T01:05:31.000Z",
      "updated-at":"2015-11-13T13:33:47.644Z"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/relationships/client-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-admin-client-user"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/relationships/client-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-client-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific User by accessing the route below.

Route: *`GET "/api/v1/admin/clients/:id"`*

## List

> List Client User

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://smart.lvh.me:3000//api/v1/admin/clients

# OUTPUT
{
  "data":
  [
    {
      "id":"4be57074-5fc6-5942-bb62-c882fb2b4eff",
      "type":"clients",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/clients/4be57074-5fc6-5942-bb62-c882fb2b4eff"
      },
      "attributes":
      {
        "name":"Empresa Smart",
        "nickname":"EmpresaSma",
        "organization-type":"company",
        "email":"contato@empresasmart.com.br",
        "created-at":"2015-11-13T01:05:31.000Z",
        "updated-at":"2015-11-13T01:05:31.000Z"
      },
      "relationships":
      {
        "client-address":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/clients/4be57074-5fc6-5942-bb62-c882fb2b4eff/relationships/client-address",
            "related":"http://smart.lvh.me:3000/api/v1/admin/clients/4be57074-5fc6-5942-bb62-c882fb2b4eff/client-address"
          },
          "data":
          {
            "type":"client-addresses",
            "id":"4be57074-5fc6-5942-bb62-c882fb2b4eff"
          }
        },
        "client-telephones":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/clients/4be57074-5fc6-5942-bb62-c882fb2b4eff/relationships/client-telephones",
            "related":"http://smart.lvh.me:3000/api/v1/admin/clients/4be57074-5fc6-5942-bb62-c882fb2b4eff/client-telephones"
          }
        }
      }
    },
    {
      "id":"de72f9fb-fece-5d16-807b-776039512ff6",
      "type":"clients",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/clients/de72f9fb-fece-5d16-807b-776039512ff6"
      },
      "attributes":
      {
        "name":"Fulano da Smart",
        "nickname":"FulanoSmart",
        "organization-type":"person",
        "email":"fulanosmart@dasilva.com",
        "created-at":"2015-11-13T01:05:31.000Z",
        "updated-at":"2015-11-13T01:05:31.000Z"
      },
      "relationships":
      {
        "client-address":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/clients/de72f9fb-fece-5d16-807b-776039512ff6/relationships/client-address",
            "related":"http://smart.lvh.me:3000/api/v1/admin/clients/de72f9fb-fece-5d16-807b-776039512ff6/client-address"
          },
          "data":
          {
            "type":"client-addresses",
            "id":"de72f9fb-fece-5d16-807b-776039512ff6"
          }
        },
        "client-telephones":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/clients/de72f9fb-fece-5d16-807b-776039512ff6/relationships/client-telephones",
            "related":"http://smart.lvh.me:3000/api/v1/admin/clients/de72f9fb-fece-5d16-807b-776039512ff6/client-telephones"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all Users by accessing the route below.

Route: *`GET "/api/v1/admin/clients"`*

# Admin Client User Telephone

When logged in, the admin can access information about users' telephones. This access allows him to create, update, show and list them.

## Create

> Create Client User Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"client-telephones", 
    "relationships":
    {
      "client":
      {
        "data":
        {
          "type":"clients", 
          "id":"id-admin-client-user"
        }
      }
    }, 
    "attributes":
    {
      "country-code":"34", 
      "number":"7777777777"
    }
  }
}'  
http://smart.lvh.me:3000/api/v1/admin/client-telephones

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone"
    },
    "attributes":
    {
      "country-code":"34",
      "number":"7777777777"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can create a telephone by accessing the route below.

Route: *`POST "/api/v1/admin/client-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 34
number | String | 7777777777

## Update

> Update Client User Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-admin-client-user-telephone",
    "type":"client-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit the information contained in telephone by accessing the route below.

Route: *`PATCH "/api/v1/admin/client-telephones/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Client User Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific telephone by accessing the route below.

Route: *`GET "/api/v1/admin/client-telephones/:id"`*

## List

> List Client User Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-telephones

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-client-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone"
      },
      "attributes":
      {
        "country-code":"12",
        "number":"789890888"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/client"
          }
        }
      }
    },
    {
      "id":"id-admin-client-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone"
      },
      "attributes":
      {
        "country-code":"21",
        "number":"789890899"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-client-user-telephone/client"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all telephones by accessing the route below.

Route: *`GET "/api/v1/admin/client-telephones"`*

# Admin Client User Address

When logged in, the admin can access information about users' address. This access allows him to create, update, show and list them.

## Create

> Create Client User Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"client-addresses", 
    "relationships":
    {
      "client":
      {
        "data":
        {
          "type":"clients", 
          "id":"id-admin-client-user"
        }
      }
    }, 
    "attributes":
    {
      "street":"Jericho Tpke Suite 344", 
      "number":"2417", 
      "complement":"Apartment", 
      "zipcode":"11040", 
      "neighborhood":"Commack", 
      "city":"Garden City Park", 
      "state":"NY", 
      "country":"US"
    }
  }
}'  
http://smart.lvh.me:3000/api/v1/admin/client-addresses

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address"
    },
    "attributes":
    {
      "street":"Jericho Tpke Suite 344",
      "number":"2417",
      "complement":"Apartment",
      "zipcode":"11040",
      "neighborhood":"Commack",
      "city":"Garden City Park",
      "state":"NY",
      "country":"US"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can create an address by accessing the route below.

Route: *`POST "/api/v1/admin/client-addresses"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Jericho Tpke Suite 344 
number | String | 2417
complement | String | Apartment
zipcode | String | 11040 
neighborhood | String | Commack
city | String | Garden City Park
state | String | NY  
country | String | US

## Update

> Update Client User Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-admin-client-user-address",
    "type":"client-addresses",
    "attributes":
    {
      "street":"Baker Street", 
      "number":"221B", 
      "complement":"Apartament", 
      "zipcode":"5150117", 
      "neighborhood":"unknown", 
      "city":"Westminster", 
      "state":"London", 
      "country":"UK"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit the information contained in address by accessing the route below.

Route: *`PATCH "/api/v1/admin/client-addresses/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Baker Street
number | String | 221B
complement | String | Apartment
zipcode | String | 5150117
neighborhood | String | unknown
city | String | Westminster
state | String | London
country | String | UK

## Show

> Show Client User Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address

# OUTPUT
{
  "data":
  {
    "id":"id-admin-client-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific address by accessing the route below.

Route: *`GET "/api/v1/admin/client-addresses/:id"`*

## List

> List Client User Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-addresses

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-client-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address"
      },
      "attributes":
      {
        "street":"Baker Street",
        "number":"221B",
        "complement":"Apartament",
        "zipcode":"5150117",
        "neighborhood":"unknown",
        "city":"Westminster",
        "state":"London",
        "country":"UK"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/client"
          }
        }
      }
    },
    {
      "id":"id-admin-client-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/4id-admin-client-user-address"
      },
      "attributes":
      {
        "street":"Av. Empresa Smart",
        "number":"1000",
        "complement":"Sala 100",
        "zipcode":"13024091",
        "neighborhood":"Bairro",
        "city":"São Paulo",
        "state":"SP",
        "country":"BR"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-client-user-address/client"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all addresses by accessing the route below.

Route: *`GET "/api/v1/admin/client-addresses"`*

# Admin Shop Category

When logged in, the admin can access information about the shop. This access allows him to create, update, show and list shop categories.

## Create

> Create Shop Category

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"shop-categories", 
    "attributes":
    { 
      "name":"Category",
      "enabled":"true",
      "description":"My New Category is Nice",
      "long-description":"My New Category is Very Nice",
      "slug":"new-category",
      "icon":"fa fa-cloud"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-categories

# OUTPUT
{
  "data":
  {
    "id":"id-admin-shop-category",
    "type":"shop-categories",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/
      id-admin-shop-category"
    },
    "attributes":
    {
      "name":"Category",
      "enabled":true,
      "description":"My New Category is Nice",
      "long-description":My New Category is Very Nice,
      "slug":"new-category",
      "icon":"fa fa-cloud"
    },
    "relationships":
    {
      "shop-groups":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/relationships/shop-groups",
          "related":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/shop-groups"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can create a category by accessing the route below.

Route: *`POST "/api/v1/admin/shop-categories"`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | Category
enabled | String | true
description | String | My New Category is Nice"
long-description | String | My New Category is Very Nice"
slug | String | new-category
icon | String | fa fa-cloud

## Update

> Update Shop Category

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "id":"id-admin-shop-category", 
    "type":"shop-categories", 
    "attributes":
    { 
      "name":"New Category",
      "enabled":true,
      "description":"My New Category is Bad",
      "long-description":"Lie, My Category is Very Nice",
      "slug":"new-category",
      "icon":"fa fa-cloud"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category

# OUTPUT
{
  "data":
  {
    "id":"id-admin-shop-category",
    "type":"shop-categories",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category"
    },
    "attributes":
    {
      "name":"New Category",
      "enabled":true,
      "description":"My New Category is Bad",
      "long-description":"Lie, My Category is Very Nice",
      "slug":"new-category",
      "icon":"fa fa-cloud"
    },
    "relationships":
    {
      "shop-groups":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/relationships/shop-groups",
          "related":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/shop-groups"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit a category by accessing the route below.

Route: *`PATCH "/api/v1/admin/shop-categories/:id`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | New Category
enabled | String | true
description | String | My New Category is Bad
long-description | String | Lie, My Category is Very Nice
slug | String | new-category
icon | String | fa fa-cloud

## Show

> Show Shop Category

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category 

# OUTPUT
{
  "data":
  {
    "id":"id-admin-shop-category",
    "type":"shop-categories",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category"
    },
    "attributes":
    {
      "name":"New Category",
      "enabled":true,
      "description":"My New Category is Bad",
      "long-description":null,
      "slug":"new-category",
      "icon":"fa fa-cloud"
    },
    "relationships":
    {
      "shop-groups":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/relationships/shop-groups",
          "related":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/shop-groups"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific category created by accessing the route below.

Route: *`GET "/api/v1/admin/shop-categories/:id"`*

## List

> List Shop Category

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-categories"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-categories

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-shop-category",
      "type":"shop-categories",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category"
      },
      "attributes":
      {
        "name":"Smart Email",
        "enabled":true,
        "description":"Smart Email",
        "long-description":"Smart Email Description",
        "slug":"email",
        "icon":"fa fa-envelope-o"
      },
      "relationships":
      {
        "shop-groups":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category5/relationships/shop-groups",
            "related":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/shop-groups"
          }
        }
      }
    },
    {
      "id":"id-admin-shop-category",
      "type":"shop-categories",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category"
      },
      "attributes":
      {
        "name":"New Category",
        "enabled":true,
        "description":"My New Category is Bad",
        "long-description":null,
        "slug":"new-category",
        "icon":"fa fa-cloud"
      },
      "relationships":
      {
        "shop-groups":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/relationships/shop-groups",
            "related":"http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category/shop-groups"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all categories created by accessing the route below.

Route: *`GET "/api/v1/admin/shop-categories"`*

# Admin Shop Group

When logged in, the admin can access information about the shop. This access allows him to create, update, show and list shop groups.

## Create

> Create Shop Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"shop-groups", 
    "relationships":
    {
      "shop-category":
      {
        "data":
        {
          "type":"shop-categories", 
          "id":"id-admin-shop-category"
        }
      }
    }, 
    "attributes":
    {
        "name":"My New Group",
        "enabled":true,
        "description":"My New Group Description",
        "long-description":"My New Group is Very Nice",
        "slug":"new-group",
        "icon":"fa fa-cloud"
    }
  }
}'  
http://smart.lvh.me:3000/api/v1/admin/shop-groups

# OUTPUT
{
  "data":
  {
    "id":"id-admin-shop-group",
    "type":"shop-groups",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group"
    },
    "attributes":
    {
      "name":"My New Group",
      "enabled":true,
      "description":"My New Group Description",
      "long-description":"My New Group is Very Nice",
      "slug":"new-group",
      "icon":"fa fa-cloud"
    },
    "relationships":
    {
      "shop-category":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/relationships/shop-category",
          "related":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/shop-category"
        },
        "data":
        {
          "type":"shop-categories",
          "id":"id-admin-shop-category"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can create a group by accessing the route below.

Route: *`POST "/api/v1/admin/shop-groups"`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | My new Group
enabled | String | true
description | String | My New Group Description"
long-description | String | My New Group is Very Nice"
slug | String | new-group
icon | String | fa fa-cloud

## Update

> Update Shop Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-admin-shop-group",
    "type":"shop-groups",
    "attributes":
    {
      "name":"Group",
      "enabled":true,
      "description":"My Group Description",
      "long-description":"My Group Long Description",
      "slug":"new-group",
      "icon":"fa fa-cloud"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group

# OUTPUT
{
  "data":
  {
    "id":"id-admin-shop-group",
    "type":"shop-groups",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group"
    },
    "attributes":
    {
      "name":"Group",
      "enabled":true,
      "description":"My Group Description",
      "long-description":"My Group Long Description",
      "slug":"new-group",
      "icon":"fa fa-cloud"
    },
    "relationships":
    {
      "shop-category":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/relationships/shop-category",
          "related":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/shop-category"
        },
        "data":
        {
          "type":"shop-categories","id":"id-admin-shop-category"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit a group by accessing the route below.

Route: *`PATCH "/api/v1/admin/shop-groups/:id`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | Group
enabled | String | true
description | String | My Group Description
long-description | String | My Group Long Description
slug | String | new-group
icon | String | fa fa-cloud

## Show

> Show Shop Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-groups"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group

# OUTPUT
{
  "data":
  {
    "id":"id-admin-shop-group","
    type":"shop-groups",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group"
    },
    "attributes":
    {
      "name":"Group",
      "enabled":true,
      "description":"My Group Description",
      "long-description":"My Group Long Description",
      "slug":"new-group",
      "icon":"fa fa-cloud"
    },
    "relationships":
    {
      "shop-category":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/relationships/shop-category",
          "related":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/4id-admin-shop-group/shop-category"
        },
        "data":
        {
          "type":"shop-categories",
          "id":"id-admin-shop-category"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific group created by accessing the route below.

Route: *`GET "/api/v1/admin/shop-groups/:id"`*

## List

> List Shop Group

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-groups"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-groups

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-shop-group",
      "type":"shop-groups",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group"
      },
      "attributes":
      {
        "name":"Smart Cloud Servers",
        "enabled":true,
        "description":"Smart Cloud Servers Desc",
        "long-description":"Smart Cloud Servers Long Desc",
        "slug":"cloud-server",
        "icon":"fa fa-cloud"
      },
      "relationships":
      {
        "shop-category":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/relationships/shop-category",
            "related":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/shop-category"
          },
          "data":
          {
            "type":"shop-categories",
            "id":"id-admin-shop-category"
          }
        }
      }
    },
    {
      "id":"id-admin-shop-group",
      "type":"shop-groups",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group"
      },
      "attributes":
      {
        "name":"Smart Email Google",
        "enabled":true,
        "description":"Smart Email Google Desc",
        "long-description":"Smart Email Google Long Desc",
        "slug":"email-google",
        "icon":"fa fa-google"
      },
      "relationships":
      {
        "shop-category":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/relationships/shop-category",
            "related":"http://smart.lvh.me:3000/api/v1/admin/shop-groups/id-admin-shop-group/shop-category"
          },
          "data":
          {
            "type":"shop-categories",
            "id":"id-admin-shop-category"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all shop groups created by accessing the route below.

Route: *`GET "/api/v1/admin/shop-groups"`*

# Admin Shop Plan

When logged in, the admin can access information about the shop. This access allows him to list shop plans.

## List

> List Shop Plan

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-plans"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-plans

# OUTPUT
{
  "data":
  [
    {
      "id":"id-shop-plans",
      "type":"shop-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Small)",
        "enabled":true,
        "values":
        {
          "disk_1_san":"25 GB (SAN)",
          "disk_2_san":null,
          "disk_3_san":null,
          "disk_4_san":null,
          "disk_5_san":null,
          "disk_1_local":null,
          "disk_2_local":null,
          "disk_type":"san",
          "datacenter":"wdc01",
          "memory":"2 GB",
          "processor":"4 x 2.0 GHz Cores",
          "operating_system":"Debian - Latest (64 bit)",
          "network_component":"1 Gbps Public \u0026 Private Network Uplinks"
        },
        "description":"Acme Cloud Server Small Desc",
        "long-description":"Acme Cloud Server Small Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "product-name":"cloud_server",
        "product-provider":"softlayer"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans/shop-group"
          },
          "data":
          {
            "type":"shop-groups","id":"id-shop-groups"
          }
        }
      }
    },
    {
      "id":"id-shop-plans",
      "type":"shop-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Large)",
        "enabled":true,
        "values":
        {
          "disk_1_san":"100 GB (SAN)",
          "disk_2_san":null,
          "disk_3_san":null,
          "disk_4_san":null,
          "disk_5_san":null,
          "disk_1_local":null,
          "disk_2_local":null,
          "disk_type":"san",
          "datacenter":"wdc01",
          "memory":"6 GB",
          "processor":"8 x 2.0 GHz Cores",
          "operating_system":"Debian - Latest (64 bit)",
          "network_component":"1 Gbps Public \u0026 Private Network Uplinks"
        },
        "description":"Acme Cloud Server Large Desc",
        "long-description":"Acme Cloud Server Large Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "product-name":"cloud_server",
        "product-provider":"softlayer"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-groups"
          }
        }
      }
    },
    {
      "id":"id-shop-plans",
      "type":"shop-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Medium)",
        "enabled":true,
        "values":
        {
          "disk_1_san":"25 GB (SAN)",
          "disk_2_san":null,
          "disk_3_san":null,
          "disk_4_san":null,
          "disk_5_san":null,
          "disk_1_local":null,
          "disk_2_local":null,
          "disk_type":"san",
          "datacenter":"wdc01",
          "memory":"4 GB",
          "processor":"8 x 2.0 GHz Cores",
          "operating_system":"Debian - Latest (64 bit)",
          "network_component":"1 Gbps Public \u0026 Private Network Uplinks"
        },
        "description":"Acme Cloud Server Medium Desc",
        "long-description":"Acme Cloud Server Medium Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "product-name":"cloud_server",
        "product-provider":"softlayer"
      },
      "relationships":
      {
        "shop-group":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans/relationships/shop-group",
            "related":"http://acme.lvh.me:3000/api/v1/admin/shop-plans/id-shop-plans/shop-group"
          },
          "data":
          {
            "type":"shop-groups",
            "id":"id-shop-groups"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all shop plans created by accessing the route below.

Route: *`GET "/api/v1/admin/shop-plans"`*

# Admin Shop Plan Softlayer Cloud Server

When logged in, the admin can access information about the shop. This access allows him to create, update, show and list shop plans Softlayer cloud server.

## Create

> Create Shop Plan Softlayer Cloud Server

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"shop-softlayer-cloud-server-plans", 
    "attributes":
    { 
      "description":"Small",
      "long-description":"Cloud Server Small",
      "disk-1-san":"25 GB (SAN)",
      "disk-2-san":"10 GB (SAN)",
      "disk-3-san":"10 GB (SAN)",
      "disk-type":"san",
      "datacenter":"wdc01",
      "memory":"2 GB",
      "processor":"4 x 2.0 GHz Cores",
      "operating-system":"Debian - Latest (64 bit)",
      "network-component":"1 Gbps Public & Private Network Uplinks"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans

# OUTPUT
{
  "data":
  {
    "id":"id-admin-plan-softlayer-cloud-server",
    "type":"shop-softlayer-cloud-server-plans",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans/id-admin-plan-softlayer-cloud-server"
    },
    "attributes":
    {
      "name":null,
      "enabled":true,
      "description":"Small",
      "long-description":"Cloud Server Small",
      "allow-custom":false,
      "can-customize":[],
      "disk-1-san":"25 GB (SAN)",
      "disk-2-san":"10 GB (SAN)",
      "disk-3-san":"10 GB (SAN)",
      "disk-4-san":null,
      "disk-5-san":null,
      "disk-1-local":null,
      "disk-2-local":null,
      "disk-type":"san",
      "datacenter":"wdc01",
      "memory":"2 GB",
      "processor":"4 x 2.0 GHz Cores",
      "operating-system":"Debian - Latest (64 bit)",
      "network-component":"1 Gbps Public \u0026 Private Network Uplinks"
    }
  }
}
```

```ruby
Not implemented
```

The admin can create a Softlayer Cloud Server plan accessing the route below.

Route: *`POST "/api/v1/admin/shop-softlayer-cloud-server-plans"`*

Variable | Type | Value
-------- | ---- | ----- 
name | String | name
enabled | String | true
description | String | Small
long-description | String | Cloud Server Small
allow-custom | String | false
can-customize | String | [ ]
disk-1-san | String | 25 GB (SAN)
disk-2-san | String | 10 GB (SAN)
disk-3-san | String | 10 GB (SAN)
disk-4-san | String | 10 GB (SAN)
disk-5-san | String | 10 GB (SAN)
disk-1-local | String | 10 GB (SAN)
disk-2-local | String | 10 GB (SAN)
disk-type | String | san
datacenter | String | wdc01
memory | String | 2 GB
processor | String | 4 x 2.0 GHz Cores
operating-system | String | Debian - Latest (64 bit)
network-component | String | 1 Gbps Public \u0026 Private Network Uplinks

## Update

> Update Shop Plan Softlayer Cloud Server

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "id":"id-admin-plan-softlayer-cloud-server", 
    "type":"shop-softlayer-cloud-server-plans", 
    "attributes":
    { 
      "description":"Boom",
      "long-description":"Cloud Server Boom",
      "disk-1-san":"10 GB (SAN)",
      "disk-2-san":"5 GB (SAN)",
      "disk-3-san":"5 GB (SAN)",
      "memory":"4 GB",
      "processor":"16 x 2.0 GHz Cores",
      "operating-system":"Ubunto - Latest (64 bit)",
      "network-component":"2 Gbps Public & Private Network Uplinks"
    }
  }
}' 
http://acme.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans/id-admin-plan-softlayer-cloud-server

# OUTPUT
{
  "data":
  {
    "id":"id-admin-plan-softlayer-cloud-server",
    "type":"shop-softlayer-cloud-server-plans",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans/id-admin-plan-softlayer-cloud-server"
    },
    "attributes":
    {
      "name":"Acme Cloud Server (Small)",
      "enabled":true,
      "description":"Boom",
      "long-description":"Cloud Server Boom",
      "allow-custom":true,
      "can-customize":["datacenter"],
      "disk-1-san":"10 GB (SAN)",
      "disk-2-san":"5 GB (SAN)",
      "disk-3-san":"5 GB (SAN)",
      "disk-4-san":null,
      "disk-5-san":null,
      "disk-1-local":null,
      "disk-2-local":null,
      "disk-type":"san",
      "datacenter":"wdc01",
      "memory":"4 GB",
      "processor":"16 x 2.0 GHz Cores",
      "operating-system":"Ubunto - Latest (64 bit)",
      "network-component":"2 Gbps Public \u0026 Private Network Uplinks"
    }
  }
} 
```

```ruby
Not implemented
```

The admin can edit a SoftLayer Cloud Server plan accessing the route below.

Route: *`PATCH "/api/v1/admin/shop-softlayer-cloud-server-plans/:id`*

Variable | Type | Value
-------- | ---- | ----- 
description | String | Boom
long-description | String | Cloud Server Boom
allow-custom | String | false
can-customize | String | [ ]
disk-1-san | String | 10 GB (SAN)
disk-2-san | String | 5 GB (SAN)
disk-3-san | String | 5 GB (SAN)
memory | String | 4 GB
processor | String | 16 x 2.0 GHz Cores
operating-system | String | Ubunto - Latest (64 bit)
network-component | String | 2 Gbps Public \u0026 Private Network Uplinks

## Show

> Show Shop Plan Softlayer Cloud Server

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-softlayer-cloud-server-plans"
  }
}' 
http://acme.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans/id-admin-plan-softlayer-cloud-server

# OUTPUT
{
  "data":
  {
    "id":"48c178e6-d4e7-5b2e-8dba-47d7e7b2265a",
    "type":"shop-softlayer-cloud-server-plans",
    "links":
    {
      "self":"http://acme.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans/48c178e6-d4e7-5b2e-8dba-47d7e7b2265a"
    },
    "attributes":
    {
      "name":"Acme Cloud Server (Small)",
      "enabled":true,
      "description":"Boom",
      "long-description":"Cloud Server Boom",
      "allow-custom":true,
      "can-customize":["datacenter"],
      "disk-1-san":"10 GB (SAN)",
      "disk-2-san":"5 GB (SAN)",
      "disk-3-san":"5 GB (SAN)",
      "disk-4-san":null,
      "disk-5-san":null,
      "disk-1-local":null,
      "disk-2-local":null,
      "disk-type":"san",
      "datacenter":"wdc01",
      "memory":"4 GB",
      "processor":"16 x 2.0 GHz Cores",
      "operating-system":"Ubunto - Latest (64 bit)",
      "network-component":"2 Gbps Public \u0026 Private Network Uplinks"
    }
  }
}
```

```ruby
Not implemented
```

The admin can get information for a specific SoftLayer Cloud Server plan accessing the route bellow.

Route: *`GET "/api/v1/admin/shop-softlayer-cloud-server-plans/:id"`*

## List

> List Shop Plan Softlayer Cloud Server

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-softlayer-cloud-server-plans"
  }
}' 
http://acme.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-plan-softlayer-cloud-server",
      "type":"shop-softlayer-cloud-server-plans",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/admin/shop-softlayer-cloud-server-plans/id-admin-plan-softlayer-cloud-server"
      },
      "attributes":
      {
        "name":"Acme Cloud Server (Small)",
        "enabled":true,
        "description":"Acme Cloud Server Small Desc",
        "long-description":"Acme Cloud Server Small Long Desc",
        "allow-custom":true,
        "can-customize":["datacenter"],
        "disk-1-san":"25 GB (SAN)",
        "disk-2-san":null,
        "disk-3-san":null,
        "disk-4-san":null,
        "disk-5-san":null,
        "disk-1-local":null,
        "disk-2-local":null,
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"2 GB",
        "processor":"4 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public \u0026 Private Network Uplinks"
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can list all SoftLayer Cloud Server plans accessing the route bellow.

Route: *`GET "/api/v1/admin/shop-softlayer-cloud-server-plans"`*

# Admin Shop Price

When logged in, the admin can access information about the shop. This access allows him to verify a price for the custom plan.

## Create

> Create Shop Price

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"shop-prices", 
    "attributes":
    { 
      "components":
      {
        "disk-1-san":"25 GB (SAN)",
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"2 GB",
        "processor":"4 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public & Private Network Uplinks"
      },
      "product":"cloud-server",
      "provider":"softlayer"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-price

# OUTPUT
{
  "data":
  {
    "id":null,
    "type":"shop-prices",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/shop-prices/"
    },
    "attributes":
    {
      "components":
      {
        "disk-1-san":"25 GB (SAN)",
        "disk-type":"san",
        "datacenter":"wdc01",
        "memory":"2 GB",
        "processor":"4 x 2.0 GHz Cores",
        "operating-system":"Debian - Latest (64 bit)",
        "network-component":"1 Gbps Public \u0026 Private Network Uplinks"
      },
      "hourly-price":"0.48",
      "monthly-price":"300.0",
      "product":"cloud-server",
      "provider":"softlayer"
    }
  }
}
```

```ruby
Not implemented
```

The admin can create a Shop Price accessing the route below.

Route: *`POST "/api/v1/admin/shop-price"`*

Variable | Type | Value
-------- | ---- | ----- 
disk-1-san | String | 25 GB (SAN)
disk-type | String | san
datacenter | String | wdc01
memory | String | 2 GB
processor | String | 4 x 2.0 GHz Cores
operating-system | String | Debian - Latest (64 bit)
network-component | String | 1 Gbps Public & Private Network Uplinks
product | String | product_example_cloud-server
provider | String | provider_example_softlayer

# Admin Shop Catalog Provider

When logged in, the admin can access information about the catalog. This access allows him to show and list his catalog provider availables.

## Show

> Show Shop Catalog Provider

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-providers" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-providers/id-catalog-provider

# OUTPUT
{
  "data":
  {
    "id":"id-catalog-provider",
    "type":"catalog-providers",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-providers/id-catalog-provider"
    },
    "attributes":
    {
      "name":"Provider",
      "provider-name":"provider"
    },
    "relationships":
    {
      "catalog-products":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-providers/id-catalog-provider/relationships/catalog-products",
          "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-providers/id-catalog-provider/catalog-products"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

When logged in, the admin can access information about the catalog. This access allows him to show catalog provider availables.

route: *`GET "/api/v1/admin/catalog-providers/:id"`*

## List

> List Shop Catalog Provider

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-providers" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-providers

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-catalog-provider",
      "type":"catalog-providers",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-providers/id-admin-catalog-provider"
      },
      "attributes":
      {
        "name":"SoftLayer"
      },
      "relationships":
      {
        "catalog-products":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-providers/id-admin-catalog-provider/relationships/catalog-products",
            "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-providers/id-admin-catalog-provider/catalog-products"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

When logged in, the admin can access information about the catalog. This access allows him to show and list catalog provider availables.

route: *`GET "/api/v1/admin/catalog-providers"`*

# Admin Shop Catalog Provider Product

When logged in, the admin can access information about the catalog. This access allows him to list catalog provider products.

## Show

> Show Shop Catalog Provider Product

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-products" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-product

# OUTPUT
{
  "data":
  {
    "id":"id-catalog-product",
    "type":"catalog-products",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-product"
    },
    "attributes":
    {
      "name":"Bare Metal",
      "slug":"bare-metal",
      "dynamic":true,
      "hourly":true,
      "version":1,
      "allow-custom":true,
      "product-name":"bare_metal",
      "provider-name":"softlayer"
    },
    "relationships":
    {
      "catalog-provider":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-product/relationships/catalog-provider",
          "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-product/catalog-provider"
        },
        "data":
        {
          "type":"catalog-providers",
          "id":"id-catalog-provider"
        }
      },
      "catalog-components":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-product/relationships/catalog-components",
          "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-product/catalog-components"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can visualize a specific provider products by accessing the route below.

route: *`GET "/api/v1/admin/catalog-products/:id"`*

## List

> List Shop Catalog Provider Product

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-products" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-products

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-catalog-provider-product",
      "type":"catalog-products",
      "links":{"self":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-admin-catalog-provider-product"
    },
    "attributes":
    {
      "name":"Bare Metal",
      "slug":"bare-metal",
      "dynamic":true,
      "hourly":true,
      "version":1,
      "allow-custom":true
    },
    "relationships":
    {
      "catalog-provider":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-admin-catalog-provider-product/relationships/catalog-provider",
          "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-admin-catalog-provider-product/catalog-provider"
        },
        "data":
        {
          "type":"catalog-providers",
          "id":"id-admin-catalog-provider"
        }
      },
      "catalog-components":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-admin-catalog-provider-product/relationships/catalog-components",
          "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-products/id-admin-catalog-provider-product/catalog-components"
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all providers products by accessing the route below.

route: *`GET "/api/v1/admin/catalog-products"`*

# Admin Shop Catalog Provider Product Attribute

When logged in, the admin can access information about the catalog. This access allows him to show and list catalog products attributes.

## Show

> Show Shop Catalog Provider Product Attributes

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-components" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-catalog-components

# OUTPUT
{
  "data":
  {
    "id":"id-catalog-components",
    "type":"catalog-components",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-catalog-components"
    },
    "attributes":
    {
      "name":"Disk 1 (Local)",
      "system":false,
      "allow-upgrade":true,
      "allow-downgrade":false
    },
    "relationships":
    {
      "catalog-product":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-catalog-components/relationships/catalog-product",
          "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-catalog-components/catalog-product"
        },
        "data":
        {
          "type":"catalog-products",
          "id":"id-catalog-product"
        }
      },
      "catalog-component-options":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-catalog-components/relationships/catalog-component-options",
          "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-catalog-components/catalog-component-options"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific product attributes by accessing the route below.

route: *`GET "/api/v1/admin/catalog-components/:id"`*

## List

> List Shop Catalog Provider Product Attributes

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-components" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-components

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-catalog-provider-product-attribute",
      "type":"catalog-components",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute"
      },
      "attributes":
      {
        "name":"Disk 1 (Local)",
        "system":false,
        "allow-upgrade":true,
        "allow-downgrade":false
      },
      "relationships":
      {
        "catalog-product":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/relationships/catalog-product",
            "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/catalog-product"
          },
          "data":
          {
            "type":"catalog-products",admin-
            "id":"id-admin-catalog-provider-product"
          }
        },
        "catalog-component-options":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/relationships/catalog-component-options",
            "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/catalog-component-options"
          }
        }
      }
    },
    {
      "id":"id-admin-catalog-provider-product-attribute",
      "type":"catalog-components",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute"
      },
      "attributes":
      {
        "name":"Disk 2 (Local)",
        "system":false,
        "allow-upgrade":true,
        "allow-downgrade":false
      },
      "relationships":
      {
        "catalog-product":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/relationships/catalog-product",
            "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/catalog-product"
          },
          "data":
          {
            "type":"catalog-products",
            "id":"id-admin-catalog-provider-product"
          }
        },
        "catalog-component-options":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/relationships/catalog-component-options",
            "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/catalog-component-options"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all providers products attributes by accessing the route below.

route: *`GET "/api/v1/admin/catalog-components"`*

# Admin Shop Catalog Provider Product Option

When logged in, the admin can access information about the catalog. This access allows him to list catalog products options.

## List

> List Shop Catalog Provider Product Options

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-component-options" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/catalog-component-options

# OUTPUT
{
  "data":
  [
    {
      "id":"id-admin-catalog-provider-product-option",
      "type":"catalog-component-options",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-component-options/id-admin-catalog-provider-product-option"
      },
      "attributes":
      {
        "name":"25 GB (LOCAL)",
        "value":"25 GB (LOCAL)",
        "hourly-price":null,
        "monthly-price":null,
        "dynamic-hourly-price":"0.0",
        "dynamic-monthly-price":"0.0"
      },
      "relationships":
      {
        "catalog-component":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-component-options/id-admin-catalog-provider-product-option/relationships/catalog-component",
            "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-component-options/id-admin-catalog-provider-product-option/catalog-component"
          },
          "data":
          {
            "type":"catalog-components",
            "id":"id-admin-catalog-provider-product-attribute"
          }
        }
      }
    },
    {
      "id":"id-admin-catalog-provider-product-option",
      "type":"catalog-component-options",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-component-options/id-admin-catalog-provider-product-option"
      },
      "attributes":
      {
        "name":"100 GB (LOCAL)",
        "value":"100 GB (LOCAL)",
        "hourly-price":null,
        "monthly-price":null,
        "dynamic-hourly-price":"0.006",
        "dynamic-monthly-price":"4.0"
      },
      "relationships":
      {
        "catalog-component":
        {
          "links":
          {
            "self":"http://smart.lvh.me:3000/api/v1/admin/catalog-component-options/id-admin-catalog-provider-product-option/relationships/catalog-component",
            "related":"http://smart.lvh.me:3000/api/v1/admin/catalog-component-options/id-admin-catalog-provider-product-option/catalog-component"
          },
          "data":
          {
            "type":"catalog-components",
            "id":"id-admin-catalog-provider-product-attribute"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all providers products options by accessing the route below.

route: *`GET "/api/v1/admin/catalog-components/id-admin-catalog-provider-product-attribute/catalog-component-options"`*

# Admin Filter

When logged in, the admin can access information about the shop. This access allows him list a specific group through a filter in the end of the url.

*`?filter%5Bvariable%5D=value`*

## Shop Catalog Provider Product

> Filter Shop Catalog Provider Product

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"catalog-products" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/catalog-products?filter%5Bprovider_name%5D=softlayer

# OUTPUT
{
  "data":
  [
    {
      "id":"id-catalog-products",
      "type":"catalog-products",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products"
      },
      "attributes":
      {
        "name":"Bare Metal",
        "slug":"bare-metal",
        "dynamic":true,
        "hourly":true,
        "version":1,
        "allow-custom":true,
        "product-name":"bare_metal",
        "provider-name":"softlayer"
      },
      "relationships":
      {
        "catalog-provider":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products/relationships/catalog-provider",
            "related":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products/catalog-provider"
          },
          "data":
          {
            "type":"catalog-providers",
            "id":"id-catalog-provider"
          }
        },
        "catalog-components":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products/relationships/catalog-components",
            "related":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products/catalog-components"
          }
        }
      }
    },
    {
      "id":"id-catalog-products",
      "type":"catalog-products",
      "links":
      {
        "self":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products"
      },
      "attributes":
      {
        "name":"Cloud Server",
        "slug":"cloud-server",
        "dynamic":true,
        "hourly":true,
        "version":1,
        "allow-custom":true,
        "product-name":"cloud_server",
        "provider-name":"softlayer"
      },
      "relationships":
      {
        "catalog-provider":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products/relationships/catalog-provider",
            "related":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products9/catalog-provider"
          },
          "data":
          {
            "type":"catalog-providers",
            "id":"id-catalog-provider"
          }
        },
        "catalog-components":
        {
          "links":
          {
            "self":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products/relationships/catalog-components",
            "related":"http://acme.lvh.me:3000/api/v1/admin/catalog-products/id-catalog-products/catalog-components"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The admin can filter a provider products by accessing the route below.

Route: *`GET "/api/v1/admin/catalog-products?filter%5Bprovider_name%5D=softlayer"`*

* product_name
* provider_name

# Manager Profile Account

When logged in, the user admin access his own profile. This access allows him to show and update information about his account.

## Show

> Show Profile Account 

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"profile"
  }
}' 
http://localhost:3000/api/v1/manager/profile

# OUTPUT
{
  "data":
  {
    "id":"id-manager-profile",
    "type":"profiles", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/profiles/id-manager-profile"
    }, 
    "attributes":
    {
      "email":"manager@example.com", 
      "first-name":"Godlike", 
      "last-name":"Manager"
    }
  }
}
```

```ruby
# INPUT
horus-cli profile show

# OUTPUT
{
  "id":"id-manager-profile", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"Godlike", 
  "last-name":"Manager"
}
```

The manager can visualize his profile account by accessing the route below.

Route: *`GET "/api/v1/manager/profile"`*

## Update

> Update Profile Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "type":"profiles", 
    "id":"id-manager-profile", 
    "attributes":
    {
      "first-name":"New Company", 
      "last-name":"Corp"
    }
  }
}' 
http://localhost:3000/api/v1/manager/profile

# OUTPUT
{
  "data":
  {
    "id":"id-manager-profile", 
    "type":"profiles", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/profiles/id-manager-profile"
    },
    "attributes":
    {
      "email":"manager@example.com",
      "first-name":"New Company",
      "last-name":"Corp"
    }
  }
}
```

```ruby
# INPUT
horus-cli profile update '"first-name":"New Company","last-name":"Corp"'

# OUTPUT
{
  "id":"id-manager-profile", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"New Company", 
  "last-name":"Corp"
}
```

The manager can edit the information contained in his own profile account by accessing the route below.

Route: *`PATCH "/api/v1/manager/profile"`*

Variable | Type | Value
---------- | ---- | ----- 
first-name | String | New Company 
last-name  | String | Corp

# Manager Company Profile

When logged in, the manager can access his own profile. This access allows him to create, update and show information about himself.

## Create

> Create Company Profile

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"company-profiles", 
    "attributes":
    { 
      "corporate-name":"Wayne Enterprises",
      "trade-name":"Wayne",
      "email":"wayne@enterprises.com"
    }
  }
}' 
http://localhost:3000/api/v1/manager/company-profile

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company",
    "type":"company-profiles",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile"
    },
    "attributes":
    {
      "corporate-name":"Wayne Enterprises",
      "trade-name":"Wayne",
      "email":"wayne@enterprises.com"
    },
    "relationships":
    {
      "company-profile-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile/relationships/company-profile-address",
          "related":"http://localhost:3000/api/v1/manager/company-profile/company-profile-address"
        },
        "data":null
      },
      "company-profile-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile/relationships/company-profile-telephones",
          "related":"http://localhost:3000/api/v1/manager/company-profile/company-profile-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```
When the manager connects for the first time, he has to create a profile by accessing the route below.

Route: *`POST "/api/v1/manager/company-profile"`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | Wayne Enterprises
trade-name | String | Wayne
email | String | wayne@enterprises.com

## Update

> Update Company Profile

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "type":"company-profiles", 
    "id":"id-manager-company", 
    "attributes":
    {
      "corporate-name":"Umbrella Corporation",
      "trade-name":"Umbrella",
      "email":"umbrella@corp.com"
    }
  }
}' 
http://localhost:3000/api/v1/manager/company-profile

# OUTPUT
{
  "data":
  {
    "id":"id-company-profiles",
    "type":"company-profiles",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile"
    },
    "attributes":
    {
      "corporate-name":"Umbrella Corporation",
      "trade-name":"Umbrella",
      "email":"umbrella@corp.com"
    },
    "relationships":
    {
      "company-profile-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile/relationships/company-profile-address",
          "related":"http://localhost:3000/api/v1/manager/company-profile/company-profile-address"
        },
        "data":
        {
          "type":"company-profile-addresses",
          "id":"id-company-profiles"
        }
      },
      "company-profile-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile/relationships/company-profile-telephones",
          "related":"http://localhost:3000/api/v1/manager/company-profile/company-profile-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can edit the information contained in his own profile accessing the route below.

Route: *`PATCH "/api/v1/manager/company-profile"`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | Umbrella Corporation
trade-name | String | Umbrella
email | String | umbrella@corp.com

## Show

> Show Company Profile

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profiles"
  }
}' 
http://localhost:3000/api/v1/manager/company-profile

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company",
    "type":"company-profiles",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile"
    },
    "attributes":
    {
      "corporate-name":"Zertico Tecnologias de Internet LTDA",
      "trade-name":"Zertico",
      "email":"contato@zertico.com"
    },
    "relationships":
    {
      "company-profile-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile/relationships/company-profile-address",
          "related":"http://localhost:3000/api/v1/manager/company-profile/company-profile-address"
        },
        "data":
        {
          "type":"company-profile-addresses",
          "id":"id-manager-company"
        }
      },
      "company-profile-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile/relationships/company-profile-telephones",
          "related":"http://localhost:3000/api/v1/manager/company-profile/company-profile-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can visualize his own profile account by accessing the route below.

Route: *`GET "/api/v1/manager/company-profile"`*

# Manager Company Profile Telephone

When logged in, the manager can access information about his telephones. This access allows him to create, update, show and list them.

## Create

> Create Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"company-profile-telephones", 
    "relationships":
    {
      "company-profile":
      {
        "data":
        {
          "type":"company-profiles", 
          "id":"id-manager-company"
        }
      }
    }, 
    "attributes":
    {
      "country-code":"55", 
      "number":"1112223334"
    }
  }
}'  
http://localhost:3000/api/v1/manager/company-profile-telephones

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company-telephone",
    "type":"company-profile-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone"
    },
    "attributes":
    {
      "country-code":"55",
      "number":"1112223334"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/relationships/company-profile",
          "related":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can create a telephone by accessing the route below.

Route: *`POST "/api/v1/manager/company-profile-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 55 
number | String | 1112223334

## Update

> Update Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-manager-company-telephone",
    "type":"company-profile-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company-telephone",
    "type":"company-profile-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/relationships/company-profile",
          "related":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can edit the information contained in a telephone by accessing the route below.

Route: *`PATCH "/api/v1/manager/company-profile-telephones/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company-telephone",
    "type":"company-profile-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/relationships/company-profile",
          "related":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can visualize a specific telephone by accessing the route below.

Route: *`GET "/api/v1/manager/company-profile-telephones/:id"`*

## List

> List Company Profile Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company-telephone",
    "type":"company-profile-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/relationships/company-profile",
          "related":"http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can visualize all telephones by accessing the route below.

Route: *`GET "/api/v1/manager/company-profile-telephones/:id"`*

# Manager Company Profile Address

When logged in, the manager can access information about his on address. This access allows him to create, update and show them.

## Create

> Create Company Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"company-profile-addresses", 
    "relationships":
    {
      "company-profile":
      {
        "data":
        {
          "type":"company-profiles", 
          "id":"id-manager-company"
        }
      }
    }, 
    "attributes":
    {
      "street":"Jericho Tpke Suite 344", 
      "number":"2417", 
      "complement":"Apartment", 
      "zipcode":"11040", 
      "neighborhood":"Commack", 
      "city":"Garden City Park", 
      "state":"NY", 
      "country":"US"
    }
  }
}'  
http://localhost:3000/api/v1/manager/company-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company-address",
    "type":"company-profile-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile-address"
    },
    "attributes":
    {
      "street":"Jericho Tpke Suite 344",
      "number":"2417",
      "complement":"Apartment",
      "zipcode":"11040",
      "neighborhood":"Commack",
      "city":"Garden City Park",
      "state":"NY",
      "country":"US"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile-address/relationships/company-profile",
          "related":"http://localhost:3000/api/v1/manager/company-profile-address/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can create an address by accessing the route below.

Route: *`POST "/api/v1/manager/company-profile-address"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Jericho Tpke Suite 344 
number | String | 2417
complement | String | Apartment
zipcode | String | 11040 
neighborhood | String | Commack
city | String | Garden City Park
state | String | NY  
country | String | US

## Update

> Update Company Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data": 
  { 
    "type":"company-profile-addresses", 
    "id":"id-manager-company-address", 
    "attributes":
    { 
      "street":"Baker Street", 
      "number":"221B", 
      "complement":"Apartament", 
      "zipcode":"5150117", 
      "neighborhood":"unknown", 
      "city":"Westminster", 
      "state":"London", 
      "country":"UK"
    }
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company-address",
    "type":"company-profile-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile-address/relationships/company-profile",
          "related":"http://localhost:3000/api/v1/manager/company-profile-address/company-profile"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can edit the information contained his own address by accessing the route below.

Route: *`PATCH "/api/v1/manager/company-profile-address"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Baker Street
number | String | 221B
complement | String | Apartment
zipcode | String | 5150117
neighborhood | String | unknown
city | String | Westminster
state | String | London
country | String | UK

## Show

> Show Company Profile Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-address

# OUTPUT
{
  "data":
  {
    "id":"id-manager-company-address",
    "type":"company-profile-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/company-profile-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "company-profile":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/company-profile-address/relationships/company-profile",
          "related":"http://localhost:3000/api/v1/manager/company-profile-address/company-profile"
        }
      }
    }
  }
} 
```

```ruby
Not implemented
```

The manager can visualize a specific address by accessing the route below.

Route: *`GET "/api/v1/manager/company-profile-address"`*

# Manager Client Company Account

When logged in, the manager can access information about companies account. This access allows him to create, update, show and list them.

## Create

> Create Client Company Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"client-users", 
    "attributes":
    { 
      "first-name":"My",
      "last-name":"User",
      "email":"my@manager.com",
      "password":"pass1234",
      "password-confirmation":"pass1234" 
    }
  }
}' 
http://localhost:3000/api/v1/manager/client-users

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-client-user-profile"
    },
    "attributes":
    {
      "first-name":"My",
      "last-name":"User",
      "email":"my@manager.com"
    }
  }
}
```

```ruby
# INPUT
horus-cli create users '"first-name":"My", "last-name":"User", "email":"my@manager.com", "password":"pass1234", "password-confirmation":"pass1234"'

# OUTPUT
{
  "first-name":"My", 
  "last-name":"User", 
  "email":"my@manager.com", 
  "password":"pass1234", 
  "password-confirmation":"pass1234"
}
```

The manager can create a company account by accessing the route below.

Route: *`POST "/api/v1/manager/client-users"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | My
last-name | String | User
email | String | my@manager.com
password | String | pass1234
password-confirmation | String | pass1234 

## Update

> Update Client Company Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  { 
    "type":"client-users", 
    "id":"id-manager-client-user-profile", 
    "attributes":
    { 
      "first-name":"Manager", 
      "last-name":"Cool"
    }
  }
}' 
http://localhost:3000/api/v1/manager/client-users/id-manager-client-user-profile 

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-client-user-profile"
    },
    "attributes":
    {
      "first-name":"Manager","last-name":"Cool","email":"my@manager.com"
    }
  }
}
```

```ruby
# INPUT
horus-cli update users "id-manager-client-user-profile" '"first-name":"Manager", "last-name":"Cool"'

# OUTPUT
{
  "id":"id-manager-client-user-profile", 
  "type":"client-users", 
  "first-name":"Manager", 
  "last-name":"Cool", 
  "email":"my@manager.com"
}
```

The manager can edit information contained in an user account by accessing the route below.

Route: *`GET "/api/v1/manager/client-users/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Manager 
last-name | String | Cool

## Show

> Show Client Company Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://localhost:3000/api/v1/manager/client-users/id-manager-client-user-profile

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-client-user-profile"
    },
    "attributes":
    {
      "first-name":"Manager",
      "last-name":"Cool",
      "email":"my@manager.com"
    }
  }
}
```

```ruby
# INPUT
horus-cli show users "id-manager-client-user-profile"

# OUTPUT
{
  "id":"id-manager-client-user-profile", 
  "type":"client-users", 
  "first-name":"Godlike", 
  "last-name":"Manager", 
  "email":"manager@example.com"
}
```

The manager can visualize a specific company account by accessing the route below.

Route: *`GET "/api/v1/manager/client-users/:id"`*

## List

> List Client Company Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://localhost:3000/api/v1/manager/client-users

# OUTPUT
{
  "data":
  [
    {
      "id":"id-manager-client-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-client-user-profile"
      },
      "attributes":
      {
        "first-name":"Manager",
        "last-name":"Cool",
        "email":"my@manager.com"
      }
    },
    {
      "id":"id-manager-client-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-client-user-profile"
      },
      "attributes":
      {
        "first-name":"Power",
        "last-name":"Admin",
        "email":"admin@acme.com"
      }
    }
  ]
}
```

```ruby
# INPUT
horus-cli list users

# OUTPUT
[
  {
    "id":"id-manager-client-user-profile", 
    "type":"client-users", 
    "first-name":"Godlike", 
    "last-name":"Manager", 
    "email":"manager@example.com"
  },
  {
    "id":"id-manager-client-user-profile", 
    "type":"client-users", 
    "first-name":"Power", 
    "last-name":"Admin", 
    "email":"admin@smart.com"
  }
]
```

The manager can visualize all companies accounts by accessing the route below.

Route: *`GET "/api/v1/manager/client-users"`*

# Manager Client Company

When logged in, the manager can access information about companies. This access allows him to create, update, show and list them.

## Create

> Create Client Company

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"clients", 
    "attributes":
    { 
      "corporate-name":"Corporacao", 
      "trade-name":"Umbrella", 
      "key-name":"umbrella", 
      "email":"umbrella@example.com", 
      "owner-id":"id-profile" 
    }
  }
}' 
http://localhost:3000/api/v1/manager/clients

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user"
    },
    "attributes":
    {
      "corporate-name":"Corporacao",
      "trade-name":"Umbrella",
      "key-name":"umbrella",
      "email":"umbrella@example.com",
      "created-at":"2015-11-12T16:22:52.399Z",
      "updated-at":"2015-11-12T16:22:52.399Z"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-address"
        },
        "data":null
      },
      "provider-softlayer-profile-client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/provider-softlayer-profile-client",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/provider-softlayer-profile-client"
        },
        "data":null
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-telephones",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli create clients '"corporate-name":"Corporacao", "trade-name":"Umbrella", "key-name":"umbrella", "email":"umbrella@example.com", "owner-id":"id-profile"'

# OUTPUT
{
  "corporate-name":"Corporacao", 
  "trade-name":"Umbrella", 
  "key-name":"umbrella", 
  "email":"umbrella@example.com", 
  "owner-id":"id-profile"
}
```

The manager can create a company by accessing the route below.

Route: *`POST "/api/v1/manager/clients"`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | Corporacao 
trade-name | String | Umbrella
key-name | String | umbrella 
email | String | umbrella@example.com

## Update

> Update Client Company

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "id":"id-manager-client-user", 
    "type":"clients", 
    "attributes":
    { 
      "corporate-name":"New Corporate", 
      "trade-name":"New Trade", 
      "email":"client_02@example.com"
    }
  }
}' 
http://localhost:3000/api/v1/manager/clients/client-id

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user"
    },
    "attributes":
    {
      "corporate-name":"New Corporate",
      "trade-name":"New Trade",
      "key-name":"key",
      "email":"client_02@example.com",
      "created-at":"2015-11-12T11:36:45.000Z",
      "updated-at":"2015-11-12T14:12:11.493Z"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-manager-client-user"
        }
      },
      "provider-softlayer-profile-client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/provider-softlayer-profile-client",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/provider-softlayer-profile-client"
        },
        "data":
        {
          "type":"provider-softlayer-profile-clients",
          "id":"id-provider-softlayer-reseller"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-telephones",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli update clients "id-manager-client-user" '"corporate-name":"New Corporate", "trade-name":"New Trade", "key-name":"key", "email":"client_02@example.com"'

# OUTPUT
{
  "id":"id-manager-client-user", 
  "type":"clients", 
  "corporate-name":"New Corporate", 
  "trade-name":"New Trade", 
  "key-name":"key", 
  "email":"client_02@example.com"
}
```

The manager can edit an information contained in a company by accessing the route below.

Route: *`PATCH "/api/v1/manager/clients/:id`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | New Corporate 
trade-name | String | New Trade
key-name | String | key 
email | String | client_02@example.com

## Show

> Show Client Company

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://localhost:3000/api/v1/manager/clients/id-manager-client-user

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user"
    },
    "attributes":
    {
      "corporate-name":"Acme Inc.",
      "trade-name":"Acme",
      "key-name":"acme",
      "email":"newclient@acme.com",
      "created-at":"2015-11-12T11:36:45.000Z",
      "updated-at":"2015-11-12T11:37:30.899Z"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-manager-client-user"
        }
      },
      "provider-softlayer-profile-client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/provider-softlayer-profile-client",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/provider-softlayer-profile-client"
        },
        "data":
        {
          "type":"provider-softlayer-profile-clients",
          "id":"id-provider-softlayer-reseller"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-telephones",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli show clients "id-manager-client-user"

# OUTPUT
{
  "id":"id-manager-client-user", 
  "type":"clients", 
  "corporate-name":"Acme Inc.", 
  "trade-name":"Acme", 
  "key-name":"acme", 
  "email":"newclient@acme.com"
}
```

The manager can visualize a specific company by accessing the route below.

Route: *`GET "/api/v1/manager/clients/:id"`*

## List

> List Client Company

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://localhost:3000/api/v1/manager/clients

# OUTPUT
{
  "data":
  [
    {
      "id":"id-manager-client-user",
      "type":"clients",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user"
      },
      "attributes":
      {
        "corporate-name":"Acme Inc.",
        "trade-name":"Acme",
        "key-name":"acme",
        "email":"newclient@acme.com",
        "created-at":"2015-11-12T11:36:45.000Z",
        "updated-at":"2015-11-12T11:37:30.899Z"
      },
      "relationships":
      {
        "client-address":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-address",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-address"
          },
          "data":
          {
            "type":"client-addresses",
            "id":"id-manager-client-user"
          }
        },
        "provider-softlayer-profile-client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/provider-softlayer-profile-client",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/provider-softlayer-profile-client"
          },
          "data":
          {
            "type":"provider-softlayer-profile-clients",
            "id":"id-provider-softlayer-reseller"
          }
        },
        "client-telephones":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-telephones",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-telephones"
          }
        }
      }
    },
    {
      "id":"id-manager-client-user",
      "type":"clients",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user"
      },
      "attributes":
      {
        "corporate-name":"Smart Inc.",
        "trade-name":"Smart",
        "key-name":"smart",
        "email":"hello@smart.com",
        "created-at":"2015-11-12T11:36:45.000Z",
        "updated-at":"2015-11-12T11:36:45.000Z"
      },
      "relationships":
      {
        "client-address":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-address",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-usert/client-address"
          },
          "data":
          {
            "type":"client-addresses",
            "id":"id-manager-client-user"
          }
        },
        "provider-softlayer-profile-client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/provider-softlayer-profile-client",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/provider-softlayer-profile-client"
          },
          "data":null
        },
        "client-telephones":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/relationships/client-telephones",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-client-user/client-telephones"
          }
        }
      }
    }
  ]
}
```

```ruby
# INPUT
horus-cli list clients

# OUTPUT
[
  {
    "id":"id-manager-client-user", 
    "type":"clients", 
    "corporate-name":"Acme Inc.", 
    "trade-name":"Acme", 
    "key-name":"acme", 
    "email":"newclient@acme.com"
  },
  {
    "id":"id-manager-client-user", 
    "type":"clients", 
    "corporate-name":"Smart Inc.", 
    "trade-name":"Smart", 
    "key-name":"smart", 
    "email":"hello@smart.com"
  }
]
```

The manager can visualize all companies by accessing the route below.

Route: *`GET "/api/v1/manager/clients"`*

# Manager Client Company Telephone

When logged in, the manager can access information about company's telephones. This access allows him to create, update, show and list them.

## Create

> Create Client Company Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"client-telephones", 
    "relationships":
    {
      "client":
      {
        "data":
        {
          "type":"clients", 
          "id":"id-manager-client-user"
        }
      }
    }, 
    "attributes":
    {
      "country-code":"34", 
      "number":"7777777777"
    }
  }
}'  
http://localhost:3000/api/v1/manager/client-telephones

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone"
    },
    "attributes":
    {
      "country-code":"34",
      "number":"7777777777"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli create telephones '"country-code":"55", "number":"7578889890"' clients "id-manager-client-user"

# OUTPUT
{
  "country-code":"55", 
  "number":"7578889890", 
  "type":"client-telephones", 
  "id":"id-manager-client-user-telephone"
}
```

The manager can create a telephone by accessing the route below.

Route: *`POST "/api/v1/manager/client-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 55 
number | String | 7578889890

## Update

> Update Client Company Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-manager-client-user-telephone",
    "type":"client-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone"
    },
    "attributes":
    {
      "country-code":"12",
      "number":"789890888"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli update telephones "id-manager-client-user-telephone" '"country-code":"12", "number":"789890888"'

# OUTPUT
{
  "id":"id-manager-client-user-telephone", 
  "type":"client-telephones", 
  "country-code":"21", 
  "number":"899890888"
}
```

The manager can edit the information contained in a telephone by accessing the route below.

Route: *`PATCH "/api/v1/manager/client-telephones/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Client Company Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone"
    },
    "attributes":
    {
      "country-code":"21",
      "number":"899890888"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli show telephones "id-manager-client-user-telephone"

# OUTPUT
{
  "id":"id-manager-client-user-telephone", 
  "type":"client-telephones", 
  "country-code":"55", 
  "number":"7578889890"
}
```

The manager can visualize a specific telephone by accessing the route below.

Route: *`GET "/api/v1/manager/client-telephones/:id"`*

## List

> List Client Company Telephone

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones

# OUTPUT
{
  "data":
  [
    {
      "id":"id-manager-client-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone"
      },
      "attributes":
      {
        "country-code":"55",
        "number":"7578889890"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/client"
          }
        }
      }
    },
    {
      "id":"id-manager-client-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone"
      },
      "attributes":
      {
        "country-code":"11",
        "number":"18889473627"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-client-user-telephone/client"
          }
        }
      }
    }
  ]
}
```

```ruby
# INPUT
horus-cli list telephones

# OUTPUT
[
  {
    "id":"id-manager-client-user-telephone", 
    "type":"client-telephones", 
    "country-code":"55", 
    "number":"7578889890"
  }, 
  {
    "id":"id-manager-client-user-telephone", 
    "type":"client-telephones", 
    "country-code":"34", 
    "number":"7777777777"
  }
}
```

The manager can visualize all telephones by accessing the route below.

Route: *`GET "/api/v1/manager/client-telephones"`*

# Manager Client Company Address

When logged in, the manager can access information about company's address. This access allows him to create, update, show and list them.

## Create

> Create Client Company Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d  
'{
  "data":
  {
    "type":"client-addresses", 
    "relationships":
    {
      "client":
      {
        "data":
        {
          "type":"clients", 
          "id":"id-manager-client-user-address"
        }
      }
    }, 
    "attributes":
    {
      "street":"Jericho Tpke Suite 344", 
      "number":"2417", 
      "complement":"Apartment", 
      "zipcode":"11040", 
      "neighborhood":"Commack", 
      "city":"Garden City Park", 
      "state":"NY", 
      "country":"US"
    }
  }
}'  
http://localhost:3000/api/v1/manager/client-addresses

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address"
    },
    "attributes":
    {
      "street":"Jericho Tpke Suite 344",
      "number":"2417",
      "complement":"Apartment",
      "zipcode":"11040",
      "neighborhood":"Commack",
      "city":"Garden City Park",
      "state":"NY",
      "country":"US"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/client"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli create addresses '"street":"Jericho Tpke Suite 344", "number":"2417", "complement":"Apartment", "zipcode":"11040", "neighborhood":"Commack", "city":"Cidade", "state":"Estado", "country":"Pais"' clients "id-manager-client-user"

# OUTPUT
{
  "street":"Jericho Tpke Suite 344", 
  "number":"2417", 
  "complement":"Apartment", 
  "zipcode":"11040", 
  "neighborhood":"Commack", 
  "city":"Garden City Park", 
  "state":"NY", 
  "country":"US", 
  "type":"client-addresses", 
  "id":"id-manager-client-user-address"
}
```

The manager can create an address by accessing the route below.

Route: *`POST "/api/v1/manager/client-addresses"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Jericho Tpke Suite 344 
number | String | 2417
complement | String | Apartment
zipcode | String | 11040 
neighborhood | String | Commack
city | String | Garden City Park
state | String | NY  
country | String | US

## Update

> Update Client Company Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-manager-client-user-address",
    "type":"client-addresses",
    "attributes":
    {
      "street":"Baker Street", 
      "number":"221B", 
      "complement":"Apartament", 
      "zipcode":"5150117", 
      "neighborhood":"unknown", 
      "city":"Westminster", 
      "state":"London", 
      "country":"UK"
    }
  }
}' 
http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartament",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/client"
        }
      }
    }
  }
} 
```

```ruby
# INPUT
horus-cli update addresses "id-manager-client-user-address" '"street":"Baker Street", "number":"221B", "complement":"Apartment", "zipcode":"5150117", "neighborhood":"unknown", "city":"Westminster", "state":"London", "country":"UK"'

# OUTPUT
{
  "id":"id-manager-client-user-address", 
  "type":"client-addresses", 
  "street":"Baker Street", 
  "number":"221B", 
  "complement":"Apartment", 
  "zipcode":"5150117", 
  "neighborhood":"unknown", 
  "city":"Westminster", 
  "state":"London", 
  "country":"UK"
}
```

The manager can edit the information contained in address by accessing the route below.

Route: *`PATCH "/api/v1/manager/client-addresses/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
street | String | Baker Street
number | String | 221B
complement | String | Apartment
zipcode | String | 5150117
neighborhood | String | unknown
city | String | Westminster
state | String | London
country | String | UK

## Show

> Show Client Company Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address

# OUTPUT
{
  "data":
  {
    "id":"id-manager-client-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"Apartment",
      "zipcode":"5150117",
      "neighborhood":"unknown",
      "city":"Westminster",
      "state":"London",
      "country":"UK"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/client"
        }
      }
    }
  }
}
```

```ruby
# INPUT
horus-cli show addresses "id-manager-client-user-address"

# OUTPUT
{
  "id":"id-manager-client-user-address", 
  "type":"client-addresses",  
  "street":"Jericho Tpke Suite 344", 
  "number":"2417", 
  "complement":"Apartment", 
  "zipcode":"11040", 
  "neighborhood":"Commack", 
  "city":"Garden City Park", 
  "state":"NY", 
  "country":"US"
}
```

The manager can visualize a specific address by accessing the route below.

Route: *`GET "/api/v1/manager/client-addresses/:id"`*

## List

> List Client Company Address

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
-H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://localhost:3000/api/v1/manager/client-addresses

# OUTPUT
{
  "data":
  [
    {
      "id":"id-manager-client-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address"
      },
      "attributes":
      {
        "street":"Baker Street",
        "number":"221B",
        "complement":"Apartment",
        "zipcode":"5150117",
        "neighborhood":"unknown",
        "city":"Westminster",
        "state":"London",
        "country":"UK"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/client"
          }
        }
      }
    },
    {
      "id":"id-manager-client-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address"
      },
      "attributes":
      {
        "street":"Hawthorne Lane",
        "number":"3771",
        "complement":null,
        "zipcode":"78023",
        "neighborhood":"nil",
        "city":"Helotes",
        "state":"TX",
        "country":"US"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-client-user-address/client"
          }
        }
      }
    }
  ]
}
```

```ruby
# INPUT
horus-cli list addresses

# OUTPUT
[
  {
    "id":"id-manager-client-user-address", 
    "type":"client-addresses", 
    "street":"Baker Street", 
    "number":"221B", 
    "complement":"Apartment", 
    "zipcode":"5150117", 
    "neighborhood":"unknown", 
    "city":"Westminster", 
    "state":"London", 
    "country":"UK"
  },
  {
    "id":"id-manager-client-user-address", 
    "type":"client-addresses",  
    "street":"Jericho Tpke Suite 344", 
    "number":"2417", 
    "complement":"Apartment", 
    "zipcode":"11040", 
    "neighborhood":"Commack", 
    "city":"Garden City Park", 
    "state":"NY", 
    "country":"US"
  }
]
```

The manager can visualize all addresses by accessing the route below.

Route: *`GET "/api/v1/manager/client-addresses"`*

# Manager Provider Softlayer Profile Clients

When logged in, the manager can access information about softlayer clients account. This access allows him to create, update, show and list them.

## Create

> Create Softlayer Clients Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X POST -d 
'{ 
  "data":
  { 
    "type":"provider-softlayer-profile-clients", 
    "attributes":
    { 
      "company-name":"Apple Inc"
    }
  }
}' 
http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients

# OUTPUT
{
  "data":
  {
    "id":"id-softlayer-clients",
    "type":"provider-softlayer-profile-clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients"
    },
    "attributes":
    {
      "softlayer-id":null,
      "brand-id":null,
      "account-status-id":null,
      "is-reseller":null,
      "company-name":"Apple Inc",
      "email":null,
      "office-phone":null,
      "first-name":null,
      "last-name":null,
      "address1":null,
      "address2":null,
      "postal-code":null,
      "city":null,
      "state":null,
      "country":null,
      "create-date":null,
      "modify-date":null
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/client"
        },
        "data":null
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can create a softlayer client account by accessing the route below.

Route: *`POST "/api/v1/manager/provider-softlayer-profile-clients"`*

Variable | Type | Value
-------- | ---- | ----- 
company-name | String | Apple Inc

## Update

> Update Softlayer Clients Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  { 
    "type":"provider-softlayer-profile-clients", 
    "id":"id-softlayer-clients", 
    "attributes":
    { 
      "company-name":"Boom"
    }
  }
}' 
http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients

# OUTPUT
{
  "data":
  {
    "id":"id-softlayer-clients",
    "type":"provider-softlayer-profile-clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients"
    },
    "attributes":
    {
      "softlayer-id":null,
      "brand-id":null,
      "account-status-id":null,
      "is-reseller":null,
      "company-name":"Boom",
      "email":null,
      "office-phone":null,
      "first-name":null,
      "last-name":null,
      "address1":null,
      "address2":null,
      "postal-code":null,
      "city":null,
      "state":null,
      "country":null,
      "create-date":null,
      "modify-date":null
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/client"
        },
        "data":null
      }
    }
  }
} 
```

```ruby
Not implemented
```

The manager can edit information contained in a softlayer client account by accessing the route below.

Route: *`GET "/api/v1/manager/provider-softlayer-profile-clients/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
company-name | String | Boom

## Show

> Show Softlayer Clients Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"provider-softlayer-profile-clients"
  }
}' 
http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients

# OUTPUT
{
  "data":
  {
    "id":"id-softlayer-clients",
    "type":"provider-softlayer-profile-clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients"
    },
    "attributes":
    {
      "softlayer-id":null,
      "brand-id":null,
      "account-status-id":null,
      "is-reseller":null,
      "company-name":"Boom",
      "email":null,
      "office-phone":null,
      "first-name":null,
      "last-name":null,
      "address1":null,
      "address2":null,
      "postal-code":null,
      "city":null,
      "state":null,
      "country":null,
      "create-date":null,
      "modify-date":null
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/client"
        },
        "data":null
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can visualize a specific softlayer client account by accessing the route below.

Route: *`GET "/api/v1/manager/provider-softlayer-profile-clients/:id"`*

## List

> List Softlayer Clients Account

```shell
# INPUT
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"provider-softlayer-profile-clients"
  }
}' 
http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients

# OUTPUT
{
  "data":
  [
    {
      "id":"id-softlayer-clients",
      "type":"provider-softlayer-profile-clients",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients"
      },
      "attributes":
      {
        "softlayer-id":null,
        "brand-id":null,
        "account-status-id":null,
        "is-reseller":null,
        "company-name":"Boom",
        "email":null,
        "office-phone":null,
        "first-name":null,
        "last-name":null,
        "address1":null,
        "address2":null,
        "postal-code":null,
        "city":null,
        "state":null,
        "country":null,
        "create-date":null,
        "modify-date":null
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/client"
          },
          "data":null
        }
      }
    },
    {
      "id":"id-softlayer-clients",
      "type":"provider-softlayer-profile-clients",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients"
      },
      "attributes":
      {
        "softlayer-id":760935,
        "brand-id":64603,
        "account-status-id":1001,
        "is-reseller":0,
        "company-name":"Test Example",
        "email":"test@example.com",
        "office-phone":"35 3623-9833",
        "first-name":"Test First Name",
        "last-name":"Test Last Name",
        "address1":"Test Street",
        "address2":null,
        "postal-code":"0000-000",
        "city":"Test City",
        "state":"TO",
        "country":"BR",
        "create-date":"2015-10-22T16:45:10.000Z",
        "modify-date":"2015-10-22T16:50:41.000Z"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/provider-softlayer-profile-clients/id-softlayer-clients/client"
          },
          "data":
          {
            "type":"clients",
            "id":"id-client"
          }
        }
      }
    }
  ]
}
```

```ruby
Not implemented
```

The manager can visualize all softlayer clients account by accessing the route below.

Route: *`GET "/api/v1/manager/provider-softlayer-profile-clients"`*

# License

Copyright 2015 Zertico Tecnologias de Internet LTDA
