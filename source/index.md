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

Horus is an API that enables a Company to distribute and manage Cloud Services more simply, this API is mainly focused on SoftLayer.

The Horus API simplifies the manage of resources and give liberty to integrate with your internal infrastructure.

Depending on the level of involvement with a system, users can be categorized as manager, reseller or user.

## Distributor (Manager)

Distributor is responsible for distributing product and services SoftLayer to Companies.

Authentication as manager allows a Distributor to list, create and update information about Companies.

Authentication as manager allows a Distributor list and update your own information.

## Reseller (Admin)

Reseller is responsible for selling product and services SoftLayer to Users.

Authentication as admin allows a Reseller to list, create and update information about Users.

Authentication as sdmin allows a Reseller list and update your own information.

## End Customer (User)

End Customer is the last layer in this API, it is responsible only for consume products and services Softlayer.

Authentication as User allows an End Customer to list and update information about his account.

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

UUID | Value
---- | ----- 
id-access-token | 22222c3b9ce6eef158104ba4d99e7f9f849682c9c55df737d6e208220f5868d7
id-refresh-token | 222254129c800c05bf40cab02b0c03f481b489d426bd06b5a32439e969df364c
id-user-profile | 03b829d7-bbe6-5556-ae91-e480c27a28ee
id-admin-profile | dab41f5f-a40c-54d8-a2f3
id-admin-company | 918ba9c6-bde4-543a-a280-afbc1bf698ad
id-admin-company-telephone | 924e8f38-369f-41e6-92f3-71d2f9e83884
id-admin-company-address | c4f5337b-bd74-4e60-9f90-7ce5c4cba782
id-admin-clint-user-profile | 56facbbe-a59d-4743-99fd-ff9936411efd
id-admin-clint-user | 4be57074-5fc6-5942-bb62-c882fb2b4eff
id-admin-clint-user-telephone | 87d3c3a2-0cd2-4667-8fc9-3c3487133061
id-admin-clint-user-address | 0778b605-36ca-4a4e-8f54-d38f830d226c
id-manager-profile | 1c9dcbb4-758d-55c0-874a-da7a8285a814
id-manager-company | 78473988-b021-4864-aa48-f3b7bc4a06f6
id-manager-company-telephone | 7915969d-e949-4066-b264-8d5bdcdf2d5c
id-manager-company-address | 1906c99a-8d54-42e1-a035-cc425553f1fd
id-manager-clint-user-profile | 1b5c1105-360c-418c-8362-385749ec5746
id-manager-clint-user | 03b829d7-bbe6-5556-ae91-e480c27a28ee
id-manager-clint-user-telephone | 690c7235-59b3-5a4e-9c04-e1aa98cc6e38
id-manager-clint-user-address | 0778b605-36ca-4a4e-8f54-d38f830d226c

# Login

The user is authenticated using a username, a password and your level of involvement with a system.

There are three ways to authenticate through Horus API, how already explained above.

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
---------- | ---- | ----- 
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

# User - Profile Account

When logged in, the user can access his own profile, it allows him to show and update information about yout account.

## Show

> Show Profile Account

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' 
http://smart.lvh.me:3000/api/v1/profile

# Return
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

The user can visualize your own profile account accessing the route described below.

Route: *`GET "api/v1/profile"`*

## Update

> Update Profile Account

```shell
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

# Return
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

The user can edit the information contained in your own profile account accessing the route described below.

Route: *`GET "api/v1/profile"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Super
last-name | String | User
email | String | user@smart.com

# Admin - Profile Account

When logged in, the user admin access his own profile, it allows him to show and update information about yout account.

## Show

> Show Profile Account

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/profile

# Return
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

The admin can visualize your own profile account accessing the route described below.

Route: *`GET "api/v1/admin/profile"`*

## Update

> Update Profile Account

```shell
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

# Return
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

The admin can edit the information contained in your own profile account accessing the route described below.

Route: *`GET "api/v1/admin/profile"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Admin
last-name  | String | Nice
email | String | admin@smart.com

# Admin - Company Profile

When logged in, the admin can access his own profile, it allows him to update and show information about himself.

## Show

> Show Company Profile

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profiles"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile

# Return
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

The admin can visualize your own profile accessing the route described below.

Route: *`GET "api/v1/admin/company-profile"`*

## Update

> Update Company Profile

```shell
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

# Return
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

The admin can edit the information contained in your own profile accessing the route described below.

Route: *`PATCH "/api/v1/admin/company-profile"`*

Variable | Type | Value
---------- | ---- | ----- 
corporate-name | String | Umbrella Corporation
trade-name | String | Umbrella
email | String | umbrella@corp.com

# Admin - Company Profile Telephone

When logged in, the admin can access information about your telephones, it allows him to create, update, show and list them.

## Create

> Create Company Profile Telephone

```shell
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

# Return
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

The admin can create a telephone accessing the route described below.

Route: *`POST "/api/v1/admin/company-profile-telephones"`*

Variable | Type | Value
---------- | ---- | ----- 
country-code | String | 55 
number | String | 1112223334

## Update

> Update Company Profile Telephone

```shell
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

# Return
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

The admin can edit the information contained in telephone accessing the route described below.

Route: *`PATCH "api/v1/admin/company-profile-telephones/:id"`*

Variable | Type | Value
---------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Company Profile Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone

# Return
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

The admin can visualize a specific telephone created for him accessing the route described below.

Route: *`GET "/api/v1/admin/company-profile-telephones/:id"`*

## List

> List Company Profile Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones

# Return
{
  "data":
  [
    {
      "id":"id-admin-company-telephone",
      "type":"company-profile-telephones",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/company-profile-telephones/id-admin-company-telephone"
      },
      "attributes":
      {
        "country-code":"1",
        "number":"18889473627"
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
    },
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
  ]
}
```

```ruby
Not implemented
```

The admin can visualize all telephones created for him accessing the route described below.

Route: *`GET "/api/v1/admin/company-profile-telephones"`*

# Admin - Company Profile Address

When logged in, the admin can access information about your address, it allows him to create, update and show them.

## Create

> Create Company Profile Address

```shell
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

# Return
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

The admin can create a address accessing the route described below.

Route: *`POST "/api/v1/admin/company-profile-address"`*

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

## Update

> Update Company Profile Address

```shell
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

# Return
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

The admin can edit the information contained in your address accessing the route described below.

Route: *`PATCH "/api/v1/admin/company-profile-address"`*

Variable | Type | Value
---------- | ---- | ----- 
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
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/company-profile-address

# Return
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

The admin can visualize your address accessing the route described below.

Route: *`GET "/api/v1/admin/company-profile-address"`*

# Admin - Client User Account

When logged in, the admin can access information about your users account, it allows him to create, update, show and list them.

## Create

> Create Client User Account

```shell
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

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-clint-user-profile"
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

The admin can create a user account accessing the route described below.

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
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  { 
    "type":"client-users", 
    "id":"id-admin-clint-user-profile", 
    "attributes":
    { 
      "first-name":"Admin", 
      "last-name":"Nice",
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-clint-user-profile

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-clint-user-profile"
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

The admin can edit the information contained in a user account accessing the route described below.

Route: *`GET "/api/v1/admin/client-users/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Admin 
last-name | String | Nice

## Show

> Show Client User Account

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-clint-user-profile

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-clint-user-profile"
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

The admin can visualize a specific user account created for him accessing the route described below.

Route: *`GET "/api/v1/admin/client-users/:id"`*

## List

> List Client User Account

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-users

# Return
{
  "data":
  [
    {
      "id":"id-admin-clint-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-clint-user-profile"
      },
      "attributes":
      {
        "first-name":"Super",
        "last-name":"User",
        "email":"user@smart.com"
      }
    },
    {
      "id":"id-admin-clint-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-users/id-admin-clint-user-profile"
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

The admin can visualize all users account created for him accessing the route described below.

Route: *`GET "/api/v1/admin/client-users"`*

# Admin - Client User

When logged in, the admin can access information about your Users, it allows him to create, update, show and list them.

## Create

> Show Client User

```shell
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

# Return
{
  "data":
  {
    "id":"id-admin-clint-user",
    "type":"clients",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/relationships/client-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/client-address"
        },
        "data":null
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/relationships/client-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/client-telephones"
        }
      }
    }
  }
} 
```

```ruby
Not implemented
```

The admin can create a User accessing the route described below.

Route: *`POST "/api/v1/admin/clients"`*

Variable | Type | Value
---------- | ---- | ----- 
name | String | Apple Inc
nickname | String | Apple
organization-type | String | company
email | String | contact@apple.com
owner-id | UUID | id-admin-profile

## Update

> Update Client User

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "id":"id-admin-clint-user", 
    "type":"clients", 
    "attributes":
    { 
      "name":"Wayne Enterprise",
      "nickname":"Wayne"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user

# Return
{
  "data":
  {
    "id":"id-admin-clint-user",
    "type":"clients",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/relationships/client-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-admin-clint-user"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/relationships/client-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/client-telephones"
        }
      }
    }
  }
} 
```

```ruby
Not implemented
```

The admin can edit the information contained in a User accessing the route described below.

Route: *`PATCH "/api/v1/admin/clients/:id`*

Variable | Type | Value
-------- | ---- | ----- 
name | String |Wayne Enterprise
nickname | String | Wayne

## Show

> Show Client User

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user

# Return
{
  "data":
  {
    "id":"id-admin-clint-user",
    "type":"clients",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/relationships/client-address",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-admin-clint-user"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/relationships/client-telephones",
          "related":"http://smart.lvh.me:3000/api/v1/admin/clients/id-admin-clint-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific User created for him accessing the route described below.

Route: *`GET "/api/v1/admin/clients/:id"`*

## List

> List Client User

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://smart.lvh.me:3000//api/v1/admin/clients

# Return
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

The admin can visualize all Users created for him accessing the route described below.

Route: *`GET "/api/v1/admin/clients"`*

# Admin Client User Telephone

When logged in, the admin can access information about Users' telephones, it allows him to create, update, show and list them.

## Create

> Create Client User Telephone

```shell
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
          "id":"id-admin-clint-user"
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

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/client"
        }
      }
    }
  }
} 
```

```ruby
Not implemented
```

The admin can create a telephone accessing the route described below.

Route: *`POST "/api/v1/admin/client-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 34
number | String | 7777777777

## Update

> Update Client User Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-admin-clint-user-telephone",
    "type":"client-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can edit the information contained in telephone accessing the route described below.

Route: *`PATCH "/api/v1/admin/client-telephones/:id"`*

Variable | Type | Value
---------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Client User Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/client"
        }
      }
    }
  }
} 
```

```ruby
Not implemented
```

The user can visualize a specific telephone created for him accessing the route described below.

Route: *`GET "/api/v1/admin/client-telephones/:id"`*

## List

> List Client User Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-telephones

# Return
{
  "data":
  [
    {
      "id":"id-admin-clint-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone"
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
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/client"
          }
        }
      }
    },
    {
      "id":"id-admin-clint-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone"
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
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-telephones/id-admin-clint-user-telephone/client"
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

The user can visualize all telephones created for him accessing the route described below.

Route: *`GET "/api/v1/admin/client-telephones"`*

# Admin Client User Address

When logged in, the admin can access information about Users' address, it allows him to create, update, show and list them.

## Create

> Create Client User Address

```shell
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
          "id":"id-admin-clint-user"
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

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user user create a address accessing the route described below.

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
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-admin-clint-user-address",
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
http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The user can edit the information contained in address accessing the route described below.

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
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address

# Return
{
  "data":
  {
    "id":"id-admin-clint-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address"
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
          "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/relationships/client",
          "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/client"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The admin can visualize a specific address created for him accessing the route described below.

Route: *`GET "/api/v1/admin/client-addresses/:id"`*

## List

> List Client User Address

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/client-addresses

# Return
{
  "data":
  [
    {
      "id":"id-admin-clint-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address"
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
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/client"
          }
        }
      }
    },
    {
      "id":"id-admin-clint-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/4id-admin-clint-user-address"
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
            "self":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/relationships/client",
            "related":"http://smart.lvh.me:3000/api/v1/admin/client-addresses/id-admin-clint-user-address/client"
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

The admin can visualize all addresses created for him accessing the route described below.

Route: *`GET "/api/v1/admin/client-addresses"`*

# Admin - Shop Category

When logged in, the admin can access information about the shop, it allows him to create, update, show and list your categories.

## Create

> Create Shop Category

```shell
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

# Return
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

The admin can create a category accessing the route described below.

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

# Return
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

The admin can edit a category accessing the route described below.

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
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-categories/id-admin-shop-category 

# Return
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

The admin can visualize a specific category created for him accessing the route described below.

Route: *`GET "/api/v1/admin/shop-categories/:id"`*

## List

> List Shop Category

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"shop-categories"
  }
}' 
http://smart.lvh.me:3000/api/v1/admin/shop-categories

# Return
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

The admin can visualize all Categories created for him accessing the route described below.

Route: *`GET "/api/v1/admin/shop-categories"`*

# Manager - Profile Account

When logged in, the manager can access his own profile, it allows him to show and update information about yout account.

## Show

> Show Profile Account 

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"profile"
  }
}' 
http://localhost:3000/api/v1/manager/profile

# Return
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
horus-cli profile show

# Return
{
  "id":"id-manager-profile", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"Godlike", 
  "last-name":"Manager"
}

The manager can visualize your own profile account accessing the route described below.

Route: *`GET "api/v1/manager/profile"`*
```

## Update

> Update Profile Account

```shell
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

# Return
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
horus-cli profile update '"first-name":"New Company","last-name":"Corp"'

# Return
{
  "id":"id-manager-profile", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"New Company", 
  "last-name":"Corp"
}
```

The manager can edit the information contained in your own profile account accessing the route described below.

Route: *`PATCH "api/v1/manager/profile"`*

Variable | Type | Value
---------- | ---- | ----- 
first-name | String | New Company 
last-name  | String | Corp


# Manager - Company Profile

When logged in, the manager can access his own profile, it allows him to create, update and show information about himself.

## Create

> Create Company Profile

```shell
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

# Return
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

Always that a manager is logged by first again is necessary that he create a profile accessing the route described below.

Route: *`POST "/api/v1/manager/company-profile"`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | Wayne Enterprises
trade-name | String | Wayne
email | String | wayne@enterprises.com

## Update

> Update Company Profile

```shell
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

# Return
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

The manager can edit the information contained in your own profile accessing the route described below.

Route: *`PATCH "/api/v1/manager/company-profile"`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | Umbrella Corporation
trade-name | String | Umbrella
email | String | umbrella@corp.com

## Show

> Show Company Profile

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profiles"
  }
}' 
http://localhost:3000/api/v1/manager/company-profile

# Return
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

The manager can visualize your own profile account accessing the route described below.

Route: *`GET "api/v1/manager/company-profile"`*

# Manager - Company Profile Telephone

When logged in, the manager can access information about your telephones, it allows him to create, update, show and list them.

## Create

> Create Company Profile Telephone

```shell
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

# Return
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

The manager can create a telephone accessing the route described below.

Route: *`POST "/api/v1/manager/company-profile-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 55 
number | String | 1112223334

## Update

> Update Company Profile Telephone

```shell
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

# Return
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

The manager can edit the information contained in telephone accessing the route described below.

Route: *`PATCH "api/v1/manager/company-profile-telephones/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Company Profile Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-telephones/id-manager-company-telephone

# Return
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

The manager can visualize a specific telephone created for him accessing the route described below.

Route: *`GET "/api/v1/manager/company-profile-telephones/:id"`*

## List

> List Company Profile Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"company-profile-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-telephones

# Return
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

The manager can visualize all telephones created for him accessing the route described below.

Route: *`GET "/api/v1/manager/company-profile-telephones"`*

# Manager - Company Profile Address

When logged in, the manager can access information about your address, it allows him to create, update and show them.

## Create

> Create Company Profile Address

```shell
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

# Return
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

The manager can create a address accessing the route described below.

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

# Return
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

The manager can edit the information contained in your address accessing the route described below.

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
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' 
http://localhost:3000/api/v1/manager/company-profile-address

# Return
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

The manager can visualize your address accessing the route described below.

Route: *`GET "/api/v1/manager/company-profile-address"`*

# Manager - Client User Account

When logged in, the manager can access information about your users account, it allows him to create, update, show and list them.

## Create Client User Account

> Create Client User Account

```shell
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

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-clint-user-profile"
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
Not implemented
```

The manager can create a user account accessing the route described below.

Route: *`POST "/api/v1/manager/client-users"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | My
last-name | String | User
email | String | my@manager.com
password | String | pass1234
password-confirmation | String | pass1234 

## Update

> Update Client User Account

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  { 
    "type":"client-users", 
    "id":"id-manager-clint-user-profile", 
    "attributes":
    { 
      "first-name":"Manager", 
      "last-name":"Cool"
    }
  }
}' 
http://localhost:3000/api/v1/manager/client-users/id-manager-clint-user-profile 

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-clint-user-profile"
    },
    "attributes":
    {
      "first-name":"Manager","last-name":"Cool","email":"my@manager.com"
    }
  }
}
```

```ruby
Not implemented
```

The manager can edit the information contained in a user account accessing the route described below.

Route: *`GET "/api/v1/manager/client-users/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
first-name | String | Manager 
last-name | String | Cool

## Show

> Show Client User Account

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://localhost:3000/api/v1/manager/client-users/id-manager-clint-user-profile

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-profile",
    "type":"client-users",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-clint-user-profile"
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
Not implemented
```

The manager can visualize a specific user account created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-users/:id"`*

## List

> List Client User Account

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-users"
  }
}' 
http://localhost:3000/api/v1/manager/client-users

# Return
{
  "data":
  [
    {
      "id":"id-manager-clint-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-clint-user-profile"
      },
      "attributes":
      {
        "first-name":"Manager",
        "last-name":"Cool",
        "email":"my@manager.com"
      }
    },
    {
      "id":"id-manager-clint-user-profile",
      "type":"client-users",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-users/id-manager-clint-user-profile"
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
Not implemented
```

The manager can visualize all users account created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-users"`*

# Manager - Client User

When logged in, the manager can access information about your Company, it allows him to create, update, show and list them.

## Create

> Show Client User

```shell
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

# Return
{
  "data":
  {
    "id":"id-manager-clint-user",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user"
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
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-address"
        },
        "data":null
      },
      "provider-softlayer-profile-client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/provider-softlayer-profile-client",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/provider-softlayer-profile-client"
        },
        "data":null
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-telephones",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
Not implemented
```

The manager can create a Company accessing the route described below.

Route: *`POST "/api/v1/manager/clients"`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | Corporacao 
trade-name | String | Umbrella
key-name | String | umbrella 
email | String | umbrella@example.com

## Update

> Update Client User

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{
  "data":
  {
    "id":"id-manager-clint-user", 
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

# Return
{
  "data":
  {
    "id":"id-manager-clint-user",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user"
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
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-manager-clint-user"
        }
      },
      "provider-softlayer-profile-client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/provider-softlayer-profile-client",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/provider-softlayer-profile-client"
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
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-telephones",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
horus-cli update clients "id-manager-clint-user" '"corporate-name":"New Corporate", "trade-name":"New Trade", "key-name":"key", "email":"client_02@example.com"'

# Return
{
  "id":"id-manager-clint-user", 
  "type":"clients", 
  "corporate-name":"New Corporate", 
  "trade-name":"New Trade", 
  "key-name":"key", 
  "email":"client_02@example.com", 
  "created-at":"2015-11-12T11:36:45.000Z", 
  "updated-at":"2015-11-12T13:29:20.003Z"
}
```

The manager can edit the information contained in a Company accessing the route described below.

Route: *`PATCH "/api/v1/manager/clients/:id`*

Variable | Type | Value
-------- | ---- | ----- 
corporate-name | String | New Corporate 
trade-name | String | New Trade
key-name | String | key 
email | String | client_02@example.com

## Show

> Show Client User

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://localhost:3000/api/v1/manager/clients/id-manager-clint-user

# Return
{
  "data":
  {
    "id":"id-manager-clint-user",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user"
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
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id-manager-clint-user"
        }
      },
      "provider-softlayer-profile-client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/provider-softlayer-profile-client",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/provider-softlayer-profile-client"
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
          "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-telephones",
          "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-telephones"
        }
      }
    }
  }
}
```

```ruby
horus-cli show clients "id-manager-clint-user"

# Return
{
  "id":"id-manager-clint-user", 
  "type":"clients", 
  "corporate-name":"Acme Inc.", 
  "trade-name":"Acme", 
  "key-name":"acme", 
  "email":"newclient@acme.com", 
  "created-at":"2015-11-12T11:36:45.000Z", 
  "updated-at":"2015-11-12T11:37:30.899Z"
}
```

The manager can visualize a specific Company created for him accessing the route described below.

Route: *`GET "/api/v1/manager/clients/:id"`*

## List

> List Client User

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://localhost:3000/api/v1/manager/clients

# Return
{
  "data":
  [
    {
      "id":"id-manager-clint-user",
      "type":"clients",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user"
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
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-address",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-address"
          },
          "data":
          {
            "type":"client-addresses",
            "id":"id-manager-clint-user"
          }
        },
        "provider-softlayer-profile-client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/provider-softlayer-profile-client",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/provider-softlayer-profile-client"
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
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-telephones",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-telephones"
          }
        }
      }
    },
    {
      "id":"id-manager-clint-user",
      "type":"clients",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user"
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
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-address",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-usert/client-address"
          },
          "data":
          {
            "type":"client-addresses",
            "id":"id-manager-clint-user"
          }
        },
        "provider-softlayer-profile-client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/provider-softlayer-profile-client",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/provider-softlayer-profile-client"
          },
          "data":null
        },
        "client-telephones":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/relationships/client-telephones",
            "related":"http://localhost:3000/api/v1/manager/clients/id-manager-clint-user/client-telephones"
          }
        }
      }
    }
  ]
}
```

```ruby
horus-cli list clients

# Return
[
  {
    "id":"id-manager-clint-user", 
    "type":"clients", 
    "corporate-name":"Acme Inc.", 
    "trade-name":"Acme", 
    "key-name":"acme", 
    "email":"newclient@acme.com", 
    "created-at":"2015-11-12T11:36:45.000Z", 
    "updated-at":"2015-11-12T11:37:30.899Z"
  },
  {
    "id":"id-manager-clint-user", 
    "type":"clients", 
    "corporate-name":"Smart Inc.", 
    "trade-name":"Smart", 
    "key-name":"smart", 
    "email":"hello@smart.com", 
    "created-at":"2015-11-12T11:36:45.000Z", 
    "updated-at":"2015-11-12T11:36:45.000Z"
  }
]
```

The manager can visualize all Companies created for him accessing the route described below.

Route: *`GET "/api/v1/manager/clients"`*

# Manager Client User Telephone

When logged in, the manager can access information about Company's telephones, it allows him to create, update, show and list them

## Create

> Create Client User Telephone

```shell
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
          "id":"id-manager-clint-user"
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

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/client"
        }
      }
    }
  }
}
```

```ruby
horus-cli create telephones '"country-code":"55", "number":"7578889890"' clients "id-manager-clint-user"

# Return
{
  "country-code":"55", 
  "number":"7578889890", 
  "type":"client-telephones", 
  "id":"id-manager-clint-user-telephone"
}
```

The manager can create a telephone accessing the route described below.

Route: *`POST "/api/v1/manager/client-telephones"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 55 
number | String | 7578889890

## Update

> Update Client User Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-manager-clint-user-telephone",
    "type":"client-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/client"
        }
      }
    }
  }
} 
```

```ruby
horus-cli update telephones "id-manager-clint-user-telephone" '"country-code":"12", "number":"789890888"'

# Return
{
  "id":"id-manager-clint-user-telephone", 
  "type":"client-telephones", 
  "country-code":"21", 
  "number":"899890888"
}
```

The manager can edit the information contained in telephone accessing the route described below.

Route: *`PATCH "/api/v1/manager/client-telephones/:id"`*

Variable | Type | Value
-------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## Show

> Show Client User Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/client"
        }
      }
    }
  }
} 
```

```ruby
horus-cli show telephones "id-manager-clint-user-telephone"

# Return
{
  "id":"id-manager-clint-user-telephone", 
  "type":"client-telephones", 
  "country-code":"55", 
  "number":"7578889890"
}
```

The manager can visualize a specific telephone created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-telephones/:id"`*

## List

> List Client User Telephone

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones

# Return
{
  "data":
  [
    {
      "id":"id-manager-clint-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone"
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
            "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/client"
          }
        }
      }
    },
    {
      "id":"id-manager-clint-user-telephone",
      "type":"client-telephones",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone"
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
            "self":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-telephones/id-manager-clint-user-telephone/client"
          }
        }
      }
    }
  ]
} 
```

```ruby
horus-cli list telephones

# Return
[
  {
    "id":"id-manager-clint-user-telephone", 
    "type":"client-telephones", 
    "country-code":"55", 
    "number":"7578889890"
  }, 
  {
    "id":"id-manager-clint-user-telephone", 
    "type":"client-telephones", 
    "country-code":"34", 
    "number":"7777777777"
  }
}
```

The manager can visualize all telephones created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-telephones"`*

# Manager - Company Address

When logged in, the manager can access information about Company's address, it allows him to create, update, show and list them.

## Create

> Create Client User Address

```shell
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
          "id":"id-manager-clint-user-address"
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

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address"
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
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/client"
        }
      }
    }
  }
}
```

```ruby
horus-cli create addresses '"street":"Jericho Tpke Suite 344", "number":"2417", "complement":"Apartment", "zipcode":"11040", "neighborhood":"Commack", "city":"Cidade", "state":"Estado", "country":"Pais"' clients "id-manager-clint-user"

# Return
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
  "id":"id-manager-clint-user-address"
}
```

The user manager create a address accessing the route described below.

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

Update Client User Address

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X PATCH -d 
'{ 
  "data":
  {
    "id":"id-manager-clint-user-address",
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
http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address"
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
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/client"
        }
      }
    }
  }
} 
```

```ruby
horus-cli update addresses "id-manager-clint-user-address" '"street":"Baker Street", "number":"221B", "complement":"Apartment", "zipcode":"5150117", "neighborhood":"unknown", "city":"Westminster", "state":"London", "country":"UK"'

# Return
{
  "id":"id-manager-clint-user-address", 
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

The manager can edit the information contained in address accessing the route described below.

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

Show Client User Address

```shell
curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address

# Return
{
  "data":
  {
    "id":"id-manager-clint-user-address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address"
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
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/client"
        }
      }
    }
  }
}
```

```ruby
horus-cli show addresses "id-manager-clint-user-address"

# Return
{
  "id":"id-manager-clint-user-address", 
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

The manager can visualize a specific address created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-addresses/:id"`*

## List

List Client User Address

```shell
curl --header "Content-Type: application/vnd.api+json" 
-H "Authorization: Bearer id-access-token" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://localhost:3000/api/v1/manager/client-addresses

# Return
{
  "data":
  [
    {
      "id":"id-manager-clint-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address"
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
            "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/client"
          }
        }
      }
    },
    {
      "id":"id-manager-clint-user-address",
      "type":"client-addresses",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address"
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
            "self":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/id-manager-clint-user-address/client"
          }
        }
      }
    }
  ]
}
```

```ruby
horus-cli list addresses

# Return
[
  {, 
    "id":"id-manager-clint-user-address", 
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
    "id":"id-manager-clint-user-address", 
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

The manager can visualize all addresses created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-addresses"`*

# License

Copyright 2015 Zertico Tecnologias de Internet LTDA
