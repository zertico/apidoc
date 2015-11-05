---
title: API Reference

language_tabs:
  - ruby: cli
  - shell

includes:
  - errors

search: true
---

# Horus API

Welcome to the Horus API! Horus is an API that enables a Company to distribute and manage Cloud Services more simply, this API is mainly focused on SoftLayer.

The Horus API does a division of authentication according to the type of user, We can do this division initially in three layers.

## Distributor (Manager)

Distributor is the responsible for distribute products and services Softlayer (initially) to Companies.

Authentication as Distributor allows the user to list and update information about yourself account.

Authentication as Distributor allows the user to list, create and update informations about Companies.

## Reseller (Admin)

Reseller is the responsible for sell products and services Softlayer (initially) to Clients.

Authentication as Reseller allows the user to list and update information about yourself account.

Authentication as Reseller allows the user to list, create and update informations about Users.

## End Customer (User)

End Customer is last layer in this API, it is the responsible only for consume the products and services  Softlayer (initially).

Authentication as User allows the user to list and update information about yourself account

# Version

You will be able to discover the version of the Horus API that is used by the command line below.

> Version

```ruby
horus-cli version
```

```shell
Not implemented
```

Currently the API is in version V1.

# Installation

# Usage

## Login

First of all, you should do the login using an email and a password already registered, along with the login you must specify which is your level of authenticating. The System Horus API currently has three types of authenticating how already explained above.

Route: `POST "/oauth/token"`

> Authentication

```ruby
# Manager

horus-cli login --manager
 
Login: manager@example.com
 
Password: pass1234

# Admin

horus-cli login --admin --domain smart.lvh.me:3000
 
Login: admin@smart.com
 
Password: pass1234

# User

horus-cli login --user --domain smart.lvh.me:3000
 
Login: user@smart.com
 
Password: pass1234

# Return

You are logged!
```

```shell
# Manager

curl -X POST -H "Content-Type: application/json" -d
'{
  "username":"manager@example.com", 
  "password":"pass1234", 
  "grant_type":"password"
}'
http://localhost:3000/oauth/token

# Admin

curl -X POST -H "Content-Type: application/json" -d 
'{
  "username":"admin@smart.com", 
  "password":"pass1234", 
  "grant_type": "password"
}' 
http://smart.lvh.me:3000/oauth/token

# User

curl -X POST -H "Content-Type: application/json" -d 
'{
  "username":"user@smart.com", 
  "password":"pass1234", 
  "grant_type": "password"
}' 
http://smart.lvh.me:3000/oauth/token

# Return

{
  "access_token":"4444141e89f4793327f6614ad8619f4242c49077f7c62a6b742dee5967cb0ae8", 
  "token_type":"bearer", 
  "expires_in":6166, 
  "refresh_token":"444488ecd358b48773d1c1bab1d79f9fae22251e01f0a63b5722c0f26d04f314", 
  "created_at":1446428109
}
```

## Profile

Once authenticated, you will have the option of show and update you profile through the following command lines.

### Show

You can show your profile using a command line or accessing a route, both cases are described below. In this example we use the manager.

Route: `GET "/api/v1/manager/profile"`

> Show Profile

```ruby
horus-cli profile show

# Return

{
  "id":"1c9dcbb4-758d-55c0-874a-da7a8285a814", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"Godlike", 
  "last-name":"Manager"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X GET -d 
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
    "id":"1c9dcbb4-758d-55c0-874a-da7a8285a814",
    "type":"profiles", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/profiles/1c9dcbb4-758d-55c0-874a-da7a8285a814"
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

### Update

You also can updatet your profile using a command line or accessing a route, both cases are described below. In this example we use the manager.

Route: `GET "/api/v1/manager/profile"`

> Update Profile

```ruby
horus-cli profile update '"first-name":"Company","last-name":"LTDA"'

# Return

{
  "id":"1c9dcbb4-758d-55c0-874a-da7a8285a814", 
  "type":"profile", 
  "email":"manager@example.com", 
  "first-name":"Company", 
  "last-name":"LTDA"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X PATCH -d 
'{
  "data":
  {
    "type":"profiles", 
    "id":"profile_id", 
    "attributes":
    {
      "first-name":"New_Company", 
      "last-name":"CIA"
    }
  }
}' 
http://192.168.2.15:3000/api/v1/manager/profile

# Return

{
  "data":
  {
    "id":"1c9dcbb4-758d-55c0-874a-da7a8285a814", 
    "type":"profiles", 
    "links":
    {
      "self":"http://192.168.2.15:3000/api/v1/manager/profiles/1c9dcbb4-758d-55c0-874a-da7a8285a814"
    },
    "attributes":
    {
      "email":"manager@example.com",
      "first-name":"New_Company",
      "last-name":"CIA"
    }
  }
} 
```

## Resource

Once authenticated, except a user, you can create new resources, edit, list and show it through the following command lines.

### Create

You can create a resource using a command line or accessing a route, both cases are described below. In this example we use the manager.

Route: `POST "/api/v1/manager/clients"`

> Create Resource

```ruby
horus-cli create clients '"corporate-name":"Corporate_name", "trade-name":"Trade_name", "key-name":"key", "email":"client@example.com"'

# Return

{
  "corporate-name":"Corporate_name", 
  "trade-name":"Trade_name", 
  "key-name":"key", 
  "email":"client@example.com", 
  "type":"clients", 
  "id":"497cec48-f018-4382-a5ea-f9e0afbec09a"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X POST -d  
'{
  "data":
  {
    "type":"clients", 
    "attributes":
    {
      "corporate-name":"Corporate_name", 
      "trade-name":"Trade_name", 
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
    "id":"fec0f2a6-ac7c-4e51-94e3-9ba222b0e467", 
    "type":"clients", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/fec0f2a6-ac7c-4e51-94e3-9ba222b0e467"
    }, 
    "attributes":
    {
      "corporate-name":"Corporate_name", 
      "trade-name":"Trade_name", 
      "key-name":"key", 
      "email":"client@example.com"
    }, 
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/fec0f2a6-ac7c-4e51-94e3-9ba222b0e467/relationships/client-address", 
          "related":"http://localhost:3000/api/v1/manager/clients/fec0f2a6-ac7c-4e51-94e3-9ba222b0e467/client-address"
        }, 
        "data":null
      }, 
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/fec0f2a6-ac7c-4e51-94e3-9ba222b0e467/relationships/client-telephones", 
          "related":"http://localhost:3000/api/v1/manager/clients/fec0f2a6-ac7c-4e51-94e3-9ba222b0e467/client-telephones"
        }
      }
    }
  }
}
```

### Update

You also can update a resource using a command line, with the id of the resource, or accessing a route, both cases are described below. In this example we use the manager.

Route: `PATCH "/api/v1/manager/clients/:id"`

> Update Resource

```ruby
horus-cli update clients "id_client" '"corporate-name":"Corporate_01", "trade-name":"Trade_01", "key-name":"key", "email":"client_01@example.com"'

# Return

{
  "id":"690c7235-59b3-5a4e-9c04-e1aa98cc6e38", 
  "type":"clients", 
  "corporate-name":"Corporate_01", 
  "trade-name":"Trade_01", 
  "key-name":"key", 
  "email":"client_01@example.com"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X PATCH -d 
'{
  "data":
  {
    "id":"client_id", 
    "type":"clients", 
    "attributes":
    { 
      "corporate-name":"Corporate_03", 
      "trade-name":"Trade_03", 
      "email":"client_03@example.com"
    }
  }
}' 
http://192.168.2.15:3000/api/v1/manager/clients/client_id

# Return

{
  "data":
  {
    "id":"918ba9c6-bde4-543a-a280-afbc1bf698ad", 
    "type":"clients", 
    "links":
    {
      "self":"http://192.168.2.15:3000/api/v1/manager/clients/918ba9c6-bde4-543a-a280-afbc1bf698ad"
    },
    "attributes":
    {
      "corporate-name":"Corporate_03",
      "trade-name":"Trade_03",
      "key-name":"smart",
      "email":"client_03@example.com"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://192.168.2.15:3000/api/v1/manager/clients/918ba9c6-bde4-543a-a280-afbc1bf698ad/relationships/client-address", 
          "related":"http://192.168.2.15:3000/api/v1/manager/clients/918ba9c6-bde4-543a-a280-afbc1bf698ad/client-address"
        },
        "data":
        {
          "type":"client-addresses","id":"918ba9c6-bde4-543a-a280-afbc1bf698ad"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://192.168.2.15:3000/api/v1/manager/clients/918ba9c6-bde4-543a-a280-afbc1bf698ad/relationships/client-telephones", 
          "related":"http://192.168.2.15:3000/api/v1/manager/clients/918ba9c6-bde4-543a-a280-afbc1bf698ad/client-telephones"
        }
      }
    }
  }
}
```

### List

You also can list your resources using a command line or accessing a route, both cases are described below. In this example we use the manager.

Route: `GET "/api/v1/manager/clients"`

> List Resources

```ruby
horus-cli list clients

# Return

[
  {
    "id":"1fb9488a-e632-4536-a321-0107f0ea15f8", 
    "type":"clients", 
    "corporate-name":"Corporate_name", 
    "trade-name":"Trade_name", 
    "key-name":"key", 
    "email":"client@example.com"
  },
  {
    "id":"690c7235-59b3-5a4e-9c04-e1aa98cc6e38", 
    "type":"clients", 
    "corporate-name":"Acme Inc.", 
    "trade-name":"Acme", 
    "key-name":"acme", 
    "email":"contact@acme.com"
  }
]
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X GET -d 
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
      "id":"1fb9488a-e632-4536-a321-0107f0ea15f8", 
      "type":"clients", 
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/clients/1fb9488a-e632-4536-a321-0107f0ea15f8"
      }, 
      "attributes": 
      {
        "corporate-name":"Corporate_name", 
        "trade-name":"Trade_name", 
        "key-name":"key", 
        "email":"client@example.com"
        }, 
        "relationships": 
        {
          "client-address":
          {
            "links":
            {
              "self":"http://localhost:3000/api/v1/manager/clients/1fb9488a-e632-4536-a321-0107f0ea15f8/relationships/client-address", 
              "related":"http://localhost:3000/api/v1/manager/clients/1fb9488a-e632-4536-a321-0107f0ea15f8/client-address"
            },
            "data":null
          },
          "client-telephones":
          {
            "links":
            {
              "self":"http://localhost:3000/api/v1/manager/clients/1fb9488a-e632-4536-a321-0107f0ea15f8/relationships/client-telephones", 
              "related":"http://localhost:3000/api/v1/manager/clients/1fb9488a-e632-4536-a321-0107f0ea15f8/client-telephones"
            }
          }
        }
      },
      {
        "id":"507129fd-38d2-4ec4-9caf-d12fd779ce08",
        "type":"clients", 
        "links": 
        {
          "self":"http://localhost:3000/api/v1/manager/clients/507129fd-38d2-4ec4-9caf-d12fd779ce08"
        }, 
        "attributes":
        {
          "corporate-name":"Corporate_name", 
          "trade-name":"Trade_name", 
          "key-name":"key", 
          "email":"client@example.com"
        }, 
        "relationships":
        {
          "client-address":
          {
            "links":
            {
              "self":"http://localhost:3000/api/v1/manager/clients/507129fd-38d2-4ec4-9caf-d12fd779ce08/relationships/client-address", 
              "related":"http://localhost:3000/api/v1/manager/clients/507129fd-38d2-4ec4-9caf-d12fd779ce08/client-address"
            },
            "data":
            {
              "type":"client-addresses", 
              "id":"749df322-3d8e-4b75-bd99-0922986b0876"
            }
          }, 
          "client-telephones":
          {
            "links": 
            {
              "self":"http://localhost:3000/api/v1/manager/clients/507129fd-38d2-4ec4-9caf-d12fd779ce08/relationships/client-telephones", 
              "related":"http://localhost:3000/api/v1/manager/clients/507129fd-38d2-4ec4-9caf-d12fd779ce08/client-telephones"
            }
          }
        }
      }
    }
  ]
}
```
### Show

You also can show a resource using a command line, with the id of the resource, or accessing a route, both cases are described below. In this example we use the manager.

Route: `GET "/api/v1/manager/clients/:id"`

> Show Resource

```ruby
horus-cli show clients "id_client"

# Return

{
  "id":"1fb9488a-e632-4536-a321-0107f0ea15f8", 
  "type":"clients", 
  "corporate-name":"Corporate_name", 
  "trade-name":"Trade_name", 
  "key-name":"key", 
  "email":"client@example.com"
}
```

```shell
# The access_token is obtained in the login.

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
    "id":"05c96f99-1fc1-4f1a-83eb-1b02366e4f2b",
    "type":"clients",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/clients/05c96f99-1fc1-4f1a-83eb-1b02366e4f2b"
    },
    "attributes":
    {
      "corporate-name":"Corporate_name",
      "trade-name":"Trade_name",
      "key-name":"key",
      "email":"client@example.com"
    },
    "relationships":
    {
      "client-address":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/05c96f99-1fc1-4f1a-83eb-1b02366e4f2b/relationships/client-address",
          "related":"http://localhost:3000/api/v1/manager/clients/05c96f99-1fc1-4f1a-83eb-1b02366e4f2b/client-address"
        },
        "data":
        {
          "type":"client-addresses",
          "id":"3c13bf0d-bd60-4f6d-8a45-32b733243ef4"
        }
      },
      "client-telephones":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/clients/05c96f99-1fc1-4f1a-83eb-1b02366e4f2b/relationships/client-telephones",
          "related":http://localhost:3000/api/v1/manager/clients/05c96f99-1fc1-4f1a-83eb-1b02366e4f2b/client-telephones"
        }
      }
    }
  }
}
```

## Telephone

Once authenticated, except a user, you can create new telephone for a specific resource, edit, list and show it through the following command lines.

### Create

You can create a telephone using a command line, with the id of the resource to which it belongs, or accessing a route, both cases are described below.

> Create Telephone

```ruby
horus-cli create telephones '"country-code" => "55", "number" =>  "7578889890"' clients "id_client"

# Return

{
  "country-code":"55", 
  "number":"7578889890", 
  "type":"client-telephones", 
  "id":"c9e166cd-d523-447a-84e3-5d5802487698"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X POST -d  
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
          "id":"507129fd-38d2-4ec4-9caf-d12fd779ce08"
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
    "id":"0a347ff7-026f-4e43-8bf1-6d1cbc351dd8", 
    "type":"client-telephones", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8/relationships/client", 
          "related":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8/client"
        }
      }
    }
  }
} 
```

### Update

You also can update a telephone using a command line, with the id of the telephone, or accessing a route, both cases are described below.

Route: `PATCH "/api/v1/manager/client-telephones/:id"`

> Update Telephone

```ruby
horus-cli update telephones "id_telephone" '"country-code":"12", "number":"789890888"'

# Return

{
  "id":"918ba9c6-bde4-543a-a280-afbc1bf698ad", 
  "type":"client-telephones", 
  "country-code":"12", 
  "number":"789890888"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X PATCH -d 
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
http://192.168.2.15:3000/api/v1/manager/client-telephones/telephone_id

# Return

{
  "data":
  {
    "id":"690c7235-59b3-5a4e-9c04-e1aa98cc6e38",
    "type":"client-telephones",
    "links":
    {
      "self":"http://192.168.2.15:3000/api/v1/manager/client-telephones/690c7235-59b3-5a4e-9c04-e1aa98cc6e38"
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
          "self":"http://192.168.2.15:3000/api/v1/manager/client-telephones/690c7235-59b3-5a4e-9c04-e1aa98cc6e38/relationships/client",
          "related":"http://192.168.2.15:3000/api/v1/manager/client-telephones/690c7235-59b3-5a4e-9c04-e1aa98cc6e38/client"
        }
      }
    }
  }
}
```

### List

You also can list your telephones using a command line or accessing a route, both cases are described below.

Route: `GET "/api/v1/manager/client-telephones"`

> List Telephones

```ruby
horus-cli list telephones

# Return

[
  {
    "id":"0de8d725-16a0-49ae-9389-010df0ca0996", 
    "type":"client-telephones", 
    "country-code":"55", 
    "number":"7578889890"
  }, 
  {
    "id":"ca4dffcc-a23c-4d2a-918b-615196e2c615", 
    "type":"client-telephones", 
    "country-code":"34", 
    "number":"7777777777"
  }
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X GET -d 
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
      "id":"0a347ff7-026f-4e43-8bf1-6d1cbc351dd8", 
      "type":"client-telephones", 
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8"
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
            "self":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8/relationships/client", 
            "related":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8/client"
          }
        }
      }
    }, 
    {
      "id":"0de8d725-16a0-49ae-9389-010df0ca0996", 
      "type":"client-telephones", 
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-telephones/0de8d725-16a0-49ae-9389-010df0ca0996"
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
            "self":"http://localhost:3000/api/v1/manager/client-telephones/0de8d725-16a0-49ae-9389-010df0ca0996/relationships/client", 
            "related":"http://localhost:3000/api/v1/manager/client-telephones/0de8d725-16a0-49ae-9389-010df0ca0996/client"
          }
        }
      }
    }
  ]
}
```

### Show

You also can show a telephone using a command line, with the id of the telephone, or accessing a route, both cases are described below.

Route: `GET "/api/v1/manager/client-telephones/:id"`

> Show Telephone

```ruby
horus-cli show telephones "id_telefone"

# Return

{
  "id":"c9e166cd-d523-447a-84e3-5d5802487698", 
  "type":"client-telephones", 
  "country-code":"55", 
  "number":"7578889890"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X GET -d 
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
    "id":"0a347ff7-026f-4e43-8bf1-6d1cbc351dd8", 
    "type":"client-telephones", 
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8"
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
          "self":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8/relationships/client", 
          "related":"http://localhost:3000/api/v1/manager/client-telephones/0a347ff7-026f-4e43-8bf1-6d1cbc351dd8/client"
        }
      }
    }
  }
} 
```

## Address

Once authenticated, except a user, you can create new address for a specific resource, edit, list and show it through the following command lines. A resource can only have an address.

### Create

You can create an address using a command line, with the id of the resource to which it belongs, or accessing a route, both cases are described below.

Route: `POST "/api/v1/manager/client-addresses"`

> Create Address

```ruby
horus-cli create addresses '"street" => "Rua", "number" =>  "55", "complement" => "Casa", "zipcode" => "37500344", "neighborhood" => "Bairro", "city" => "Cidade", "state" => "Estado", "country" => "Pais"' clients "id_client"

# Return

{
  "street":"Rua", 
  "number":"55", 
  "complement":"Casa", 
  "zipcode":"37500344", 
  "neighborhood":"Bairro", 
  "city":"Cidade", 
  "state":"Estado", 
  "country":"Pais", 
  "type":"client-addresses", 
  "id":"3c13bf0d-bd60-4f6d-8a45-32b733243ef4"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X POST -d  
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
          "id":"507129fd-38d2-4ec4-9caf-d12fd779ce08"
        }
      }
    }, 
    "attributes":
    {
      "street":"Rua", 
      "number":"55", 
      "complement":"Casa", 
      "zipcode":"37500344", 
      "neighborhood":"Bairro", 
      "city":"Cidade", 
      "state":"Estado", 
      "country":"Pais"
    }
  }
}'  
http://localhost:3000/api/v1/manager/client-addresses

# Return

{
  "data":
  {
    "id":"41f848fd-a072-4f2a-aed9-fd1b3419c128",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/41f848fd-a072-4f2a-aed9-fd1b3419c128"}, 
      "attributes":
      {
        "street":"Rua",
        "number":"55",
        "complement":"Casa",
        "zipcode":"37500344",
        "neighborhood":"Bairro",
        "city":"Cidade",
        "state":"Estado",
        "country":"Pais"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/client-addresses/41f848fd-a072-4f2a-aed9-fd1b3419c128/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/41f848fd-a072-4f2a-aed9-fd1b3419c128/client"
          }
        }
      }
    }
  }
}
```

### Update

You also can update an address using a command line, with the id of the address, or accessing a route, both cases are described below.

Route: `PATCH "/api/v1/manager/client-addresses/:id"`

> Update Address

```ruby
horus-cli update addresses "id_address" '"street" => "Av.", "number" =>  "7", "complement" => "Predio", "zipcode" => "3750000", "neighborhood" => "Vila", "city" => "City", "state" => "State", "country" => "Country"'

# Return

{
  "id":"a688f3e8-bfea-5ee1-853a-9c5ee614de18", 
  "type":"client-addresses", 
  "street":"Av.", 
  "number":"7", 
  "complement":"Predio", 
  "zipcode":"3750000, 
  "neighborhood":"Vila", 
  "city":"City", 
  "state":"State", 
  "country":"Country"
}
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X PATCH -d 
'{ 
  "data":
  {
    "id":"address_id",
    "type":"client-addresses",
    "attributes":
    {
      "street":"Baker Street", 
      "number":"221B", 
      "complement":"nil", 
      "zipcode":"5150117", 
      "neighborhood":"nil", 
      "city":"Westminster", 
      "state":"London", 
      "country":"UK"
    }
  }
}' 
http://192.168.2.15:3000/api/v1/manager/client-addresses/address_id

# Return

{
  "data":
  {
    "id":"918ba9c6-bde4-543a-a280-afbc1bf698ad",
    "type":"client-addresses",
    "links":
    {
      "self":"http://192.168.2.15:3000/api/v1/manager/client-addresses/918ba9c6-bde4-543a-a280-afbc1bf698ad"
    },
    "attributes":
    {
      "street":"Baker Street",
      "number":"221B",
      "complement":"nil",
      "zipcode":"5150117",
      "neighborhood":"nil",
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
          "self":"http://192.168.2.15:3000/api/v1/manager/client-addresses/918ba9c6-bde4-543a-a280-afbc1bf698ad/relationships/client",
          "related":"http://192.168.2.15:3000/api/v1/manager/client-addresses/918ba9c6-bde4-543a-a280-afbc1bf698ad/client"
        }
      }
    }
  }
} 
```

### List

You also can list your addresses using a command line or accessing a route, both cases are described below.

Route: `GET "/api/v1/manager/client-addresses"`

> List Addresses

```ruby
horus-cli list addresses

# Return

[
  {
    "id":"a688f3e8-bfea-5ee1-853a-9c5ee614de18", 
    "type":"client-addresses", 
    "street":"R. Almiro Gomes de Lima", 
    "number":"70", 
    "complement":nil, 
    "zipcode":"37502530", 
    "neighborhood":"Nossa Senhora de Fatima", 
    "city":"Itajubá", 
    "state":"MG", 
    "country":"BR"
  },
  {
    "id":"f0f8fbe4-4003-472f-a3f2-177d898206ab", 
    "type":"client-addresses", 
    "street":"Rua", 
    "number":"55", 
    "complement":"Casa", 
    "zipcode":"37500344", 
    "neighborhood":"Bairro", 
    "city":"Cidade", 
    "state":"Estado", 
    "country":"Pais"
  }
]
```

```shell
# The access_token is obtained in the login.

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X GET -d 
'{
  "data":
  {
    "type":"client-addresses"
  }
}' 
http://localhost:3000/api/v1/manager/client-addr

# Return

{
  "data":
  [
    {
      "id":"3c13bf0d-bd60-4f6d-8a45-32b733243ef4",
      "type":"client-addresses",
      "links":
      {"
        self":"http://localhost:3000/api/v1/manager/client-addresses/3c13bf0d-bd60-4f6d-8a45-32b733243ef4"
      },
      "attributes":
      {
        "street":"Rua",
        "number":"55",
        "complement":"Casa",
        "zipcode":"37500344",
        "neighborhood":"Bairro",
        "city":"Cidade",
        "state":"Estado",
        "country":"Pais"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/client-addresses/3c13bf0d-bd60-4f6d-8a45-32b733243ef4/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/3c13bf0d-bd60-4f6d-8a45-32b733243ef4/client"
          }
        }
      }
    }, 
    {
      "id":"f0f8fbe4-4003-472f-a3f2-177d898206ab",
      "type":"client-addresses",
      "links":
      {
        "self":"http://localhost:3000/api/v1/manager/client-addresses/f0f8fbe4-4003-472f-a3f2-177d898206ab"
      },
      "attributes":
      {
        "street":"Rua",
        "number":"55",
        "complement":"Casa",
        "zipcode":"37500344",
        "neighborhood":"Bairro",
        "city":"Cidade",
        "state":"Estado",
        "country":"Pais"
      },
      "relationships":
      {
        "client":
        {
          "links":
          {
            "self":"http://localhost:3000/api/v1/manager/client-addresses/f0f8fbe4-4003-472f-a3f2-177d898206ab/relationships/client",
            "related":"http://localhost:3000/api/v1/manager/client-addresses/f0f8fbe4-4003-472f-a3f2-177d898206ab/client"
          }
        }
      }
    }
  ]
} 
```

### Show

You also can show an address using a command line, with the id of the address, or accessing a route, both cases are described below.

Route: `GET "/api/v1/manager/client-addresses/:id"`

> Show Address

```ruby
horus-cli show addresses "id_address"

# Return

{
  "id":"3c13bf0d-bd60-4f6d-8a45-32b733243ef4", 
  "type":"client-addresses", 
  "street":"Rua", 
  "number":"55", 
  "complement":"Casa", 
  "zipcode":"37500344", 
  "neighborhood":"Bairro", 
  "city":"Cidade", 
  "state":"Estado", 
  "country":"Pais"
}
```

```shell
  

curl --header "Content-Type: application/vnd.api+json" -H "Authorization: Bearer 'access_token'" -X GET -d 
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
    "id":"41f848fd-a072-4f2a-aed9-fd1b3419c128",
    "type":"client-addresses",
    "links":
    {
      "self":"http://localhost:3000/api/v1/manager/client-addresses/41f848fd-a072-4f2a-aed9-fd1b3419c128"
    },
    "attributes":
    {
      "street":"Rua",
      "number":"55",
      "complement":"Casa",
      "zipcode":"37500344",
      "neighborhood":"Bairro",
      "city":"Cidade",
      "state":"Estado",
      "country":"Pais"
    },
    "relationships":
    {
      "client":
      {
        "links":
        {
          "self":"http://localhost:3000/api/v1/manager/client-addresses/41f848fd-a072-4f2a-aed9-fd1b3419c128/relationships/client",
          "related":"http://localhost:3000/api/v1/manager/client-addresses/41f848fd-a072-4f2a-aed9-fd1b3419c128client"
        }
      }
    }
  }
```

# License

Copyright 2015 Zertico Tecnologias de Internet LTDA