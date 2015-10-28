---
title: API Reference

language_tabs:
  - ruby

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

 Authentication as Reseler allows the user to list, create and update informations about Users.

## End Customer (User)

 End Customer is last layer in this API, it is the responsible only for consume the products and services  Softlayer (initially).

 Authentication as User allows the user to list and update information about yourself account.

# Version

 You will be able to discover the version of the Horus API that is used by the command line below.

 `ruby bin/horus-cli version`

 Currently the API is in version 0.1.0. 

# Installation

# Usage

## Login

 First of all, you should do the login using an email and a password already registered, along with the login you must specify which is your level of authenticating. The System Horus API currently has three types of authenticating how already explained above.

 Rota: `POST "/oauth/token"`

* Manager

 `ruby bin/horus-cli login --manager`
 
 `Login: `manager@example.com`
 
 `Password: pass1234`

* Admin

 `ruby bin/horus-cli login --admin --domain smart.lvh.me:3000`
 
 `Login: `admin@smart.com`
 
 `Password: pass1234`

* User

 `ruby bin/horus-cli login --user --domain smart.lvh.me:3000`
 
 `Login: `user@smart.com`
 
 `Password: pass1234`
 
## Profile

 Once authenticated, you will have the option of show and update you profile through the following command lines.

* Show

 You can show your profile using a command line or accessing a route, both cases are described below. In this example we use the manager.

 Route: `GET "/api/v1/manager/profile"`

 Command Line: `ruby bin/horus-cli profile show`

* Update

 You also can updatet your profile using a command line or accessing a route, both cases are described below. In this exeample we use the manager.

 Route: `GET "/api/v1/manager/profile"`

 Command Line: `ruby bin/horus-cli profile update '"first-name"=>"Company","last-name" => "LTDA"`

## Resource

 Once authenticated, except a user, you can create new resources, edit, list and show it through the following command lines.

* Create

 You can create a resource using a command line or accessing a route, both cases are described below. In this example we use the manager.

 Route: `POST "/api/v1/manager/clients"`

 Command Line: `ruby bin/horus-cli create clients '"corporate-name":"Corporate_name", "trade-name":"Trade_name", "key-name":"key", "email":"client@example.com"'`

* Update

 You also can update a resource using a command line, with the id of the resource, or accessing a route, both cases are described below. In this exeample we use the manager.

 Route: `PATCH "/api/v1/manager/clients/:id"`

 Command Line: `ruby bin/horus-cli update clients "id" '"corporate-name":"Corporate", "trade-name":"Trade", "key-name":"key", "email":"client_01@example.com"'``

* List

 You also can list your resources using a command line or accessing a route, both cases are described below. In this exeample we use the manager.

 Route: `GET "/api/v1/manager/clients"`

 Command Line: `ruby bin/horus-cli list clients`

* Show

 You also can show a resource using a command line, with the id of the resource, or accessing a route, both cases are described below. In this exeample we use the manager.

 Route: `GET "/api/v1/manager/clients/:id"`

 Command Line: `ruby bin/horus-cli show clients "id"`

## Telephone

 Once authenticated, except a user, you can create new telephone for a specific resource, edit, list and show it through the following command lines.

* Create

 You can create a telephone using a command line, with the id of the resource to which it belongs, or accessing a route, both cases are described below.

 Route: `POST "/api/v1/manager/client-telephones"`

 Command Line: `ruby bin/horus-cli create telephones '"country-code" => "55", "number" =>  "7578889890"' clients "id"`
    
* Update

 You also can update a telephone using a command line, with the id of the telephone, or accessing a route, both cases are described below.

 Route: `PATCH "/api/v1/manager/client-telephones/:id"`

 Command Line: `ruby bin/horus-cli update telephones "id" '"country-code":"1", "number":"789890888"'`

* List

 You also can list your telephones using a command line or accessing a route, both cases are described below.

 Route: `GET "/api/v1/manager/client-telephones"`

 Command Line: `ruby bin/horus-cli list telephones`

* Show

 You also can show a telephone using a command line, with the id of the telephone, or accessing a route, both cases are described below.

 Route: `GET "/api/v1/manager/client-telephones/:id"`

 Command Line: `ruby bin/horus-cli show telephones "id"`

## Address

 Once authenticated, except a user, you can create new address for a specific resource, edit, list and show it through the following command lines. A resource can only have an address.

* Create

 You can create an address using a command line, with the id of the resource to which it belongs, or accessing a route, both cases are described below.

 Route: `POST "/api/v1/manager/client-addresses"`

 Command Line: `ruby bin/horus-cli create addresses '"street" => "Rua", "number" =>  "55", "complement" => "Casa", "zipcode" => "37500344", "neighborhood" => "Bairro", "city" => "Cidade", "state" => "Estado", "country" => "Pais"' clients "id"`

* Update

 You also can update an address using a command line, with the id of the assress, or accessing a route, both cases are described below.

 Route: `PATCH "/api/v1/manager/client-addresses/:id"`

 Command Line: `ruby bin/horus-cli update addresses "id" '"street" => "Av.", "number" =>  "7", "complement" => "Predio", "zipcode" => "37500oo", "neighborhood" => "Vila", "city" => "City", "state" => "State", "country" => "Country"'`

* List

 You also can list your addresses using a command line or accessing a route, both cases are described below.

 Route: `GET "/api/v1/manager/client-addresses"`

 Command Line: `ruby bin/horus-cli list addresses`

* Show

 You also can show an address using a command line, with the id of the address, or accessing a route, both cases are described below.

 Route: `GET "/api/v1/manager/client-addresses/:id"`

 Command Line: `ruby bin/horus-cli show addresses "id"`

# License

 Copyright 2015 Zertico Tecnologias de Internet LTDA