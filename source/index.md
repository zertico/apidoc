---
title: Horus API

language_tabs:
  - ruby: CLI
  - shell: cURL

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

```ruby
horus-cli version
```

```shell
Not implemented
```

# Installation

# Login

The user is authenticated via a username, a password and your level of involvement with a system.

There are three ways to authenticate through Horus API, how already explained above.

Route: *`POST "/oauth/token"`*

## Manager

> Authentication

```ruby
horus-cli login --manager

Login: manager@example.com
Password: pass1234

# Return
You are logged!
```

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
  "access_token":"id_access_token", 
  "token_type":"bearer", 
  "expires_in":6166, 
  "refresh_token":"id_refresh_token", 
  "created_at":1446428109
}
```
Variable | Type | Value
---------- | ---- | ----- 
login | String | manager@example.com
password | String | pass1234
authentication | String | manager

## Admin

> Authentication

```ruby
horus-cli login --admin --domain smart.lvh.me:3000
 
Login: admin@smart.com
Password: pass1234

# Return
You are logged!
```

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
  "access_token":"id_access_token", 
  "token_type":"bearer", 
  "expires_in":6166, 
  "refresh_token":"id_refresh_token", 
  "created_at":1446428109
}
```

Variable | Type | Value
---------- | ---- | ----- 
login | String | admin@smart.com
password | String | pass1234
authentication | String | admin
domain | String | smart.lvh.me:3000

## User

> Authentication

```ruby
horus-cli login --user --domain smart.lvh.me:3000
 
Login: user@smart.com 
Password: pass1234

# Return
You are logged!
```

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
  "access_token":"id_access_token", 
  "token_type":"bearer", 
  "expires_in":6166, 
  "refresh_token":"id_refresh_token", 
  "created_at":1446428109
}
```

Variable | Type | Value
---------- | ---- | ----- 
login | String | user@smart.com
password | String | pass1234
authentication | String | user
domain | String | smart.lvh.me:3000

# User-Profile

When logged in, the user can access his own profile, it allows him to show and update information about himself.

## Show

> Show Profile

```ruby
Not implemented
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer access_token" -X GET -d 
'{ 
  "data": 
  { 
    "type":"profile" 
  } 
}' http://smart.lvh.me:3000/api/v1/profile

# Return
{
  "data":
  {
    "id":"id_profile", 
    "type":"profiles", 
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/profiles/id_profile"
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

The user can visualize your own profile accessing the route described below.

Route: *`GET "api/v1/profile"`*

## Update

> Update Profile

```ruby
Not implemented
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer access_token" -X PATCH -d
'{ 
  "data": 
  { 
    "type":"profiles", 
    "id":"id_profile", 
    "attributes":
    { 
      "first-name":"Super", 
      "last-name":"User" 
    } 
  } 
}' http://smart.lvh.me:3000/api/v1/profile

# Return
{
  "data":
  {
    "id":"id_profile", 
    "type":"profiles", 
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/profiles/id_profile"
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

The user can edit the information contained in your own profile accessing the route described below.

Route: *`GET "api/v1/profile"`*

Variable | Type | Value
---------- | ---- | ----- 
first-name | String | Super
last-name  | String | User

# Admin-Profile

When logged in, the admin can access his own profile, it allows him to show and update information about himself.

## Show

> Show Profile

```ruby
Not implemented
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer access_token" -X GET -d 
'{ 
  "data":
  { 
    "type":"profile" 
  }
}' http://smart.lvh.me:3000/api/v1/admin/profile

# Return
{
  "data":
  {
    "id":"id_profile",
    "type":"profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/profiles/id_profile"
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

The admin can visualize your own profile accessing the route described below.

Route: *`GET "api/v1/admin/profile"`*

## Update

> Update Profile

```ruby
Not implemented
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer access_token" -X PATCH -d 
'{ 
  "data":
  { 
    "type":"profiles", 
    "id":"id_profile", 
    "attributes":
    { 
      "first-name":"Admin", 
      "last-name":"Nice"
    }
  }
}' http://smart.lvh.me:3000/api/v1/admin/profile

# Return
{
  "data":
  {
    "id":"id_profile",
    "type":"profiles",
    "links":
    {
      "self":"http://smart.lvh.me:3000/api/v1/admin/profiles/id_profile"
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

The admin can edit the information contained in your own profile accessing the route described below.

Route: *`GET "api/v1/admin/profile"`*

Variable | Type | Value
---------- | ---- | ----- 
first-name | String | Admin
last-name  | String | Nice

# Manager-Profile

When logged in, the manager can access his own profile, it allows him to show and update information about himself.

## Show

> Show Profile

```ruby
horus-cli profile show

# Return
{
  "id":"id_profile", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"Godlike", 
  "last-name":"Manager"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer access_token" -X GET -d 
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
    "id":"id_profile",
    "type":"profiles", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/profiles/id_profile"
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

The user can visualize your own profile accessing the route described below.

Route: *`GET "api/v1/manager/profile"`*

## Update

> Update Profile

```ruby
horus-cli profile update '"first-name":"New Company","last-name":"Corp"'

# Return
{
  "id":"id_profile", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"New Company", 
  "last-name":"Corp"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer access_token" -X PATCH -d 
'{
  "data":
  {
    "type":"profiles", 
    "id":"profile_id", 
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
    "id":"id_profile", 
    "type":"profiles", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/profiles/id_profile"
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

The user can edit the information contained in your own profile accessing the route described below.

Route: *`GET "api/v1/manager/profile"`*

Variable | Type | Value
---------- | ---- | ----- 
first-name | String | New Company 
last-name  | String | Corp

# Manager-Company

When logged in, the manager can access information about your Companies, it allows him to create, update, show and list them.

## Create

> Create Company

```ruby
horus-cli create clients '"corporate-name":"Corporate_name", "trade-name":"Trade_name", "key-name":"key", "email":"client@example.com"'

# Return
{
  "corporate-name":"Corporate", 
  "trade-name":"Trade", 
  "key-name":"key", 
  "email":"client@example.com", 
  "type":"clients", 
  "id":"id_client"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X POST -d  
'{
  "data":
  {
    "type":"clients", 
    "attributes":
    {
      "corporate-name":"Corporate", 
      "trade-name":"Trade", 
      "key-name":"key", 
      "email":"client@example.com"
    }
  }
}'  
http://localhost:3000/api/v1/manager/clients

# Return
{
  "data":
  {
    "id":"id_client", 
    "type":"clients", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id_client"
    }, 
    "attributes":
    {
      "corporate-name":"Corporate", 
      "trade-name":"Trade", 
      "key-name":"key", 
      "email":"client@example.com"
    }, 
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id_client/relationships/client-address", 
          "related":"http://localhost:3000/api/v1/manager/clients/id_client/client-address"
        }, 
        "data":null
      }, 
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id_client/relationships/client-telephones", 
          "related":"http://localhost:3000/api/v1/manager/clients/id_client/client-telephones"
        }
      }
    }
  }
}
```

The manager can create a Company accessing the route described below.

Route: *`POST "/api/v1/manager/clients"`*

Variable | Type | Value
---------- | ---- | ----- 
corporate-name | String | Corporate 
trade-name | String | Trade
key-name | String | key 
email | String | client@example.com

## Update

> Update Company

```ruby
horus-cli update clients "id_client" '"corporate-name":"New Corporate", "New Trade":"Trade_01", "key-name":"key", "email":"client_02@example.com"'

# Return
{
  "id":"id_client", 
  "type":"clients", 
  "corporate-name":"New Corporate", 
  "trade-name":"New Trade", 
  "key-name":"key", 
  "email":"client_02@example.com"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X PATCH -d 
'{
  "data":
  {
    "id":"client_id", 
    "type":"clients", 
    "attributes":
    { 
      "corporate-name":"New Corporate", 
      "trade-name":"New Trade", 
      "email":"client_02@example.com"
    }
  }
}' 
http://localhost:3000/api/v1/manager/clients/client_id

# Return
{
  "data":
  {
    "id":"id_client", 
    "type":"clients", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id_client"
    },
    "attributes":
    {
      "corporate-name":"New Corporate",
      "trade-name":"New Trade",
      "key-name":"key",
      "email":"client_02@example.com"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id_client/relationships/client-address", 
          "related":"http://localhost:3000/api/v1/manager/clients/id_client/client-address"
        },
        "data":
        {
          "type":"client-addresses","id":"id_client"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id_client/relationships/client-telephones", 
          "related":"http://localhost:3000/api/v1/manager/clients/id_client/client-telephones"
        }
      }
    }
  }
}
```

The manager can edit the information contained in a Company accessing the route described below.

Route: *`PATCH "/api/v1/manager/clients/:id`*

Variable | Type | Value
---------- | ---- | ----- 
corporate-name | String | New Corporate 
trade-name | String | New Trade
key-name | String | key 
email | String | client_02@example.com

## List

> List Company

```ruby
horus-cli list clients

# Return
[
  {
    "id":"id_client_01", 
    "type":"clients", 
    "corporate-name":"Corporate", 
    "trade-name":"Trade", 
    "key-name":"key", 
    "email":"client@example.com"
  },
  {
    "id":"id_client_02", 
    "type":"clients", 
    "corporate-name":"Acme Inc.", 
    "trade-name":"Acme", 
    "key-name":"acme", 
    "email":"contact@acme.com"
  }
]
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X GET -d 
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
      "id":"id_client_01", 
      "type":"clients", 
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/clients/id_client_01"
      }, 
      "attributes": 
      {
        "corporate-name":"Corporate", 
        "trade-name":"Trade", 
        "key-name":"key", 
        "email":"client@example.com"
        }, 
        "relationships": 
        {
          "client-address":
          {
            "links":
            {
              "self":"http://localhost:3000/api/v1/manager/clients/id_client_01/relationships/client-address", 
              "related":"http://localhost:3000/api/v1/manager/clients/id_client_01/client-address"
            },
            "data":null
          },
          "client-telephones":
          {
            "links":
            {
              "self":"http://localhost:3000/api/v1/manager/clients/id_client_01/relationships/client-telephones", 
              "related":"http://localhost:3000/api/v1/manager/clients/id_client_01/client-telephones"
            }
          }
        }
      },
      {
        "id":"id_client_02",
        "type":"clients", 
        "links": 
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id_client_02"
        }, 
        "attributes":
        {
          "corporate-name":"Acme Inc.", 
          "trade-name":"Acme", 
          "key-name":"acme", 
          "email":"contact@acme.com"
        }, 
        "relationships":
        {
          "client-address":
          {
            "links":
            {
              "self":"http://localhost:3000/api/v1/manager/clients/id_client_02/relationships/client-address", 
              "related":"http://localhost:3000/api/v1/manager/clients/id_client_02/client-address"
            },
            "data":
            {
              "type":"client-addresses", 
              "id":"id_address"
            }
          }, 
          "client-telephones":
          {
            "links": 
            {
              "self":"http://localhost:3000/api/v1/manager/clients/id_client_02/relationships/client-telephones", 
              "related":"http://localhost:3000/api/v1/manager/clients/id_client_02/client-telephones"
            }
          }
        }
      }
    }
  ]
}
```

The manager can visualize all Companies created for him accessing the route described below.

Route: *`GET "/api/v1/manager/clients"`*

## Show

> Show Company

```ruby
horus-cli show clients "id_client"

# Return
{
  "id":"id_client", 
  "type":"clients", 
  "corporate-name":"Corporate", 
  "trade-name":"Trade", 
  "key-name":"key", 
  "email":"client@example.com"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X GET -d 
'{
  "data":
  {
    "type":"clients"
  }
}' 
http://localhost:3000/api/v1/manager/clients/'id_client'

# Return
{
  "data":
  {
    "id":"id_client",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/id_client"
    },
    "attributes":
    {
      "corporate-name":"Corporate",
      "trade-name":"Trade",
      "key-name":"key",
      "email":"client@example.com"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id_client/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/id_client/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"id_address"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/id_client/relationships/client-telephones",
          "related":http://localhost:3000/api/v1/manager/clients/id_client/client-telephones"
        }
      }
    }
  }
}
```

The manager can visualize a specific Company created for him accessing the route described below.

Route: *`GET "/api/v1/manager/clients/:id"`*

# Manager-Company-Telephone

When logged in, the manager can access information about Company's telephones, it allows him to create, update, show and list them

## Create

> Create Telephone

```ruby
horus-cli create telephones '"country-code":"55", "number":"7578889890"' clients "id_client"

# Return
{
  "country-code":"55", 
  "number":"7578889890", 
  "type":"client-telephones", 
  "id":"id_telephone"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X POST -d  
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
          "id":"id_client"
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
    "id":"id_telephone", 
    "type":"client-telephones", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone/relationships/client", 
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone/client"
        }
      }
    }
  }
} 
```

The manager can create a telephone accessing the route described below.

Route: *`POST "/api/v1/manager/client-telephones"`*

Variable | Type | Value
---------- | ---- | ----- 
country-code | String | 55 
number | String | 7578889890

## Update

> Update Telephone

```ruby
horus-cli update telephones "id_telephone" '"country-code":"12", "number":"789890888"'

# Return

{
  "id":"id_telephone", 
  "type":"client-telephones", 
  "country-code":"12", 
  "number":"789890888"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X PATCH -d 
'{ 
  "data":
  {
    "id":"telephone_id",
    "type":"client-telephones",
    "attributes":
    {
      "country-code":"12", 
      "number":"789890888"
    }
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones/telephone_id

# Return
{
  "data":
  {
    "id":"id_telephone",
    "type":"client-telephones",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone/client"
        }
      }
    }
  }
}
```

The manager can edit the information contained in telephone accessing the route described below.

Route: *`PATCH "/api/v1/manager/client-telephones/:id"`*

Variable | Type | Value
---------- | ---- | ----- 
country-code | String | 12 
number | String | 789890888

## List

> List Telephone

```ruby
horus-cli list telephones

# Return
[
  {
    "id":"id_telephone_01", 
    "type":"client-telephones", 
    "country-code":"55", 
    "number":"7578889890"
  }, 
  {
    "id":"id_telephone_02", 
    "type":"client-telephones", 
    "country-code":"34", 
    "number":"7777777777"
  }
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X GET -d 
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
      "id":"id_telephone_01", 
      "type":"client-telephones", 
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone_01"
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
            "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone_01/relationships/client", 
            "related":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone_01/client"
          }
        }
      }
    }, 
    {
      "id":"id_telephone_02", 
      "type":"client-telephones", 
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone_02"
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
            "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone_02/relationships/client", 
            "related":"http://localhost:3000/api/v1/manager/client-telephones/id_telephone_02/client"
          }
        }
      }
    }
  ]
}
```

The manager can visualize all telephones created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-telephones"`*

## Show

> Show Telephone

```ruby
horus-cli show telephones "id_telefone"

# Return
{
  "id":"id_telephone", 
  "type":"client-telephones", 
  "country-code":"55", 
  "number":"7578889890"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X GET -d 
'{
  "data":
  {
    "type":"client-telephones"
  }
}' 
http://localhost:3000/api/v1/manager/client-telephones/id_telefone

# Return
{
  "data":
  {
    "id":"id_telefone", 
    "type":"client-telephones", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telefone"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/id_telefone/relationships/client", 
          "related":"http://localhost:3000/api/v1/manager/client-telephones/id_telefone/client"
        }
      }
    }
  }
} 
```

The manager can visualize a specific telephone created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-telephones/:id"`*

# Manager-Company-Address

When logged in, the manager can access information about Company's address, it allows him to create, update, show and list them.

## Create

> Create Address

```ruby
horus-cli create addresses '"street":"Jericho Tpke Suite 344", "number":"2417", "complement":"Apartment", "zipcode":"11040", "neighborhood":"Commack", "city":"Cidade", "state":"Estado", "country":"Pais"' clients "id_client"

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
  "id":"id_address"
}
```

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X POST -d  
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
          "id":"id_address"
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
    "id":"id_address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id_address"
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
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id_address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id_address/client"
        }
      }
    }
  }
}
```

The user manager create a address accessing the route described below.

Route: *`POST "/api/v1/manager/client-addresses"`*

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

> Update Address

```ruby
horus-cli update addresses "id_address" '"street":"Baker Street", "number":"221B", "complement":"Apartment", "zipcode":"5150117", "neighborhood":"unknown", "city":"Westminster", "state":"London", "country":"UK"'

# Return
{
  "id":"id_address", 
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

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X PATCH -d 
'{ 
  "data":
  {
    "id":"address_id",
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
http://localhost:3000/api/v1/manager/client-addresses/address_id

# Return
{
  "data":
  {
    "id":"address_id",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/address_id"
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
          "self":"http://localhost:3000/api/v1/manager/client-addresses/address_id/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/address_id/client"
        }
      }
    }
  }
} 
```

The manager can edit the information contained in address accessing the route described below.

Route: *`PATCH "/api/v1/manager/client-addresses/:id"`*

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

## List

> List Addresses

```ruby
horus-cli list addresses

# Return
[
  {, 
    "id":"id_address_01", 
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
    "id":"id_address_02", 
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

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
-H "Authorization: Bearer 'access_token'" -X GET -d 
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
      "id":"id_address_01",
      "type":"client-addresses",
      "links":
      {"
        self":"http://localhost:3000/api/v1/manager/client-addresses/id_address_01"
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
            "self":"http://localhost:3000/api/v1/manager/client-addresses/id_address_01/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/id_address_01/client"
          }
        }
      }
    }, 
    {
      "id":"id_address_02",
      "type":"client-addresses",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-addresses/id_address_02"
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
            "self":"http://localhost:3000/api/v1/manager/client-addresses/id_address_02/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/id_address_02/client"
          }
        }
      }
    }
  ]
} 
```

The manager can visualize all addresses created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-addresses"`*

## Show

> Show Address

```ruby
horus-cli show addresses "id_address"

# Return
{
  "id":"id_address", 
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

```shell
# The access_token is obtained in the login (id_access_token).

curl --header "Content-Type: application/vnd.api+json" 
  -H "Authorization: Bearer 'access_token'" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://localhost:3000/api/v1/manager/client-addresses/id_address

# Return
{
  "data":
   {
    "id":"id_address",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/id_address"
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
          "self":"http://localhost:3000/api/v1/manager/client-addresses/id_address/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/id_address/client"
        }
      }
    }
  }
```

The manager can visualize a specific address created for him accessing the route described below.

Route: *`GET "/api/v1/manager/client-addresses/:id"`*

# License

Copyright 2015 Zertico Tecnologias de Internet LTDA
