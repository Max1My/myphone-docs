---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - graphql
  - json

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the MyPhone API! You can use our API to access MyPhone API endpoints, which can get information.

# Authentication

### HTTP Request

`POST http://api.myphone.group/partner/login`

> To authorize, use this code:

```json
{
  "username": "username",
  "password": "password"
}
```
> The above command returns JSON structured like this:

```json
{
    "data": {
        "access": {
            "token": "token",
            "expires": "2023-07-16T11:58:20.333Z"
        },
        "refresh": {
            "token": "token",
            "expires": "2023-07-23T11:58:20.333Z"
        }
    }
}
```

> Make sure to replace `token` with your API key.

MyPhone uses API keys to allow access to the API. You can register a new MyPhone API key at our portal.

MyPhone expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer token`

<aside class="notice">
You must replace <code>token</code> with your personal API key.
</aside>

# Filters

Filtering can be applied to those queries that support them

### Variables

Parameter | Default | Description
--------- |---------| -----------
field | None    | Select one of the fields by which you want to filter from query
value | None    | The value can be of different types, such as integers, filters, strings and lists.
operator | None    | Choose one of the operators "OR" or "AND"
comparator | None    | Choose one of the comparotors.

```graphql
"filter": [{
                "field": "some_field",
                "value": some_value,
                "operator": "OR", "AND",
                "comparator": "EQ", "NEQ", "LT", "LTE", "GT", "GTE", "IN", "NIN", "CONTAINS", "STARTS_WITH", "ENDS_WITH", "NULL"
            }]

```
# Sorting

Sorting can be applied to those queries that support them

### Variables

Parameter | Default | Description
--------- |---------| -----------
field | None    | Select one of the fields by which you want to sort from query
order | None    | Choose how you want to sort "ASC" or "DESC".

```graphql
"sort": [{
                "field": "some_field",
                "order": "OR", "AND",
            }]

```

# Simcards

## Get All simcards

```graphql
query($offset: Int, $limit: Int, $filter: [FilterInput], $sort: [SortInput]) {
            simcards(pagination: {offset: $offset, limit: $limit},
                     filter: $filter,
                     sort: $sort) {
                items {
                    id
                    iccidPlastic
                    simId
                    isBlocked
                    allowFreeCallerIdChange
                    allowFreeVoiceSubstitution
                    resource{
                        balance
                        dataBalance
                    }
                    fmcs {
                        msisdn
                    }
                    callerIds {
                        msisdn
                    }
                    externalMsisdns {
                        msisdn
                    }
                    currentTariff {
                        name
                        packageTotalCallsMaxDuration
                        tariffType
                    }
                    profile
                    description
                    latestActivity
                    tariffExpiresAt
                    imei {
                      imei
                      imeiIsCorrect
                    }
                    isArchived
                }
                count
            }
        }
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all simcards.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Fields

Field | Type    | Description
------ |---------| --------------
id | ID      | Internal ID Simcard                                                                                      
iccidPlastic | String  | It's a unique 18-22 digit code that includes a SIM card's country, home network, and identification number. 
simId | String  | Your external sim card ID           
isBlocked | Boolean | Sim card status                     
allowFreeCallerIdChange | Boolean | desc                                
allowFreeVoiceSubstitution | Boolean | desc                                
resource | Array of objects | desc                                
balance | Float   | desc                                
dataBalance | Float   | desc                                
fmcs | Object  | desc                                
msisdn | String  | desc                                
callerIds | List    | desc                                
msisdn | String  | desc                                
externalMsisdns | List    | desc                                
msisdn | String  | desc                                
currentTariff | Object  | Current Tarrif                      
name | String  | Tarrif Name                         
packageTotalCallsMaxDuration | Integer | desc                                
tariffType | String  | Tariff Type                         
profile | String  | Sim Card Profile(S1, S2, etc.).     
description | String  | desc                                
latestActivity | Date    | Latest Activity                     
tariffExpiresAt | Date    | Tariff Expires At           
imei | String  | imei                                
imeiIsCorrect | Boolean | Status Imei                         
isArchived | Boolean | Status Archived sim card            
count | Integer | Maximum number of displayed objects 

### Variables

Parameter | Type             | Description
--------- |------------------| -----------
offset | Integer          | The offset query parameter is used to exclude from a response the first N items of a resource collection.
limit | Integer          | You can combine the limit and the offset options to request a particular set of items. Note that the offset option is applied before the limit option, regardless of its position in the request. That is, top results are selected from a collection where a set of items is already excluded.
filter | Array of objects | Read about [Filters](http://localhost:4567/?graphql#filters)
sort | Array of objects | Read about [Sorting](http://localhost:4567/?graphql#sortings)


<aside class="success">
Remember — only authorized users can use this request!
</aside>

## Get a Specific Simcard


```graphql
            query($id: ID!) {
                simcard(id: $id) {
                items {
                    id
                    iccidPlastic
                    simId
                    isBlocked
                    allowFreeCallerIdChange
                    allowFreeVoiceSubstitution
                    resource{
                        balance
                        dataBalance
                    }
                    fmcs {
                        msisdn
                    }
                    callerIds {
                        msisdn
                    }
                    externalMsisdns {
                        msisdn
                    }
                    currentTariff {
                        name
                        packageTotalCallsMaxDuration
                        tariffType
                    }
                    profile
                    description
                    latestActivity
                    tariffExpiresAt
                    imei {
                      imei
                      imeiIsCorrect
                    }
                    isArchived
                }
                count
            }
        }
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Fields

Field | Type    | Description
------ |---------| --------------
id | ID      | Internal ID Simcard                                                                                      
iccidPlastic | String  | It's a unique 18-22 digit code that includes a SIM card's country, home network, and identification number. 
simId | String  | Your external sim card ID           
isBlocked | Boolean | Sim card status                     
allowFreeCallerIdChange | Boolean | desc                                
allowFreeVoiceSubstitution | Boolean | desc                                
resource | Array of objects | desc                                
balance | Float   | desc                                
dataBalance | Float   | desc                                
fmcs | Object  | desc                                
msisdn | String  | desc                                
callerIds | List    | desc                                
msisdn | String  | desc                                
externalMsisdns | List    | desc                                
msisdn | String  | desc                                
currentTariff | Object  | Current Tarrif                      
name | String  | Tarrif Name                         
packageTotalCallsMaxDuration | Integer | desc                                
tariffType | String  | Tariff Type                         
profile | String  | Sim Card Profile(S1, S2, etc.).     
description | String  | desc                                
latestActivity | Date    | Latest Activity                     
tariffExpiresAt | Date    | Tariff Expires At           
imei | String  | imei                                
imeiIsCorrect | Boolean | Status Imei                         
isArchived | Boolean | Status Archived sim card            
count | Integer | Maximum number of displayed objects 

### Filters

Parameter | Type | Description
--------- |------| -----------
ID | ID   | Enter the id of the sim card you want to search


## Block a Specific Simcard

```graphql
mutation($simcardId: ID!) {
                    simcard {
                        block(simcardId: $simcardId)
                    }
                }
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint blocking a specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`


### Variables

Variable | Type | Description
---------|------|-------------
simcardId | ID | Enter the id of the sim card you want to block

## Unblock a Specific Simcard

```graphql
mutation($simcardId: ID!) {
                    simcard {
                        unblock(simcardId: $simcardId)
                    }
                }
```

This endpoint unblocking a specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
simcardId | ID | Enter the id of the sim card you want to unblock

## Attach Caller ID

```graphql
mutation($sim_card_id: ID!, $caller_id: String!){
                simcard {
                    attachCallerId(id: $sim_card_id, msisdn: $caller_id)
                }   
            }
```

This endpoint attaching a specific simcard by caller id.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
sim_card_id | ID | Enter the id of the sim card you want to unblock
caller_id | ID | Enter the id of the sim card you want to unblock
