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
    content: Documentation for the MyPhone API
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

## Detach Caller

```graphql
mutation($sim_card_id: ID!){
                simcard{
                    detachCallerId(id: $sim_card_id)
                }
            }
```

This endpoint detaching a specific simcard by caller id.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
sim_card_id | ID | Enter the id of the sim card you want to detach

## Charge Balance

```graphql
mutation($simcardId: ID!, $amount: Decimal!, $comment: String!) {
                simcard {
                    chargeBalance(simcardId: $simcardId,
                           amount: $amount,
                           comment: $comment)
                }
            }
```

This endpoint charging balance for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
simcardId | ID | Enter the id of the sim card you want to charge
amount | Float | Enter the replenishment amount
comment | String | Destination

## Charge Data Balance

```graphql
mutation($simcardId: ID!, $amount: Decimal!, $comment: String!) {
                simcard {
                    chargeDataBalance(simcardId: $simcardId,
                           amount: $amount,
                           comment: $comment)
                }
            }
```

This endpoint charging data balance for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
simcardId | ID | Enter the id of the sim card you want to charge
amount | Float | Enter the replenishment amount
comment | String | Destination

## Recharge Balance

```graphql
mutation($simcardId: ID!, $amount: Decimal!, $comment: String!) {
                simcard {
                    rechargeBalance(simcardId: $simcardId,
                           amount: $amount,
                           comment: $comment)
                }
            }
```

This endpoint recharging balance for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
simcardId | ID | Enter the id of the sim card you want to charge
amount | Float | Enter the replenishment amount
comment | String | Destination

## Recharge Data Balance

```graphql
mutation($simcardId: ID!, $amount: Decimal!, $comment: String!) {
                simcard {
                    rechargeDataBalance(simcardId: $simcardId,
                           amount: $amount,
                           comment: $comment)
                }
            }
```

This endpoint recharging data balance for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
simcardId | ID | Enter the id of the sim card you want to charge
amount | Float | Enter the replenishment amount
comment | String | Destination


## Change Tariff

```graphql
mutation($simcardId: ID!, $tariffId: ID!) {
                simcard {
                    changeTariff(simcardId: $simcardId, tariffId: $tariffId, free: false)
                }
            }
```

This endpoint change tariff for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type   | Description
---------|--------|-------------
simcardId | ID     | Enter the id of the sim card you want to charge
tariffId | ID     | Get Available tariffs you can [This]()


### Update Description

```graphql
mutation($sim_card_id: ID!, $description: String!){
                simcard {
                    updateDescription(id: $sim_card_id, description: $description)
                }   
            }
```

This endpoint update description for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type   | Description
---------|--------|-------------
simcardId | ID     | Enter the id of the sim card you want to charge
description | String | Enter the description for simcard


## Change Remaining Tariff Days

```graphql
mutation($sim_card_id: ID!, $remaining_days: Int!){
                simcard {
                    changeRemainingTariffDays(simcardId: $sim_card_id, day: $remaining_days)
                }   
            }
```

This endpoint change remaining tariff days for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type    | Description
---------|---------|-------------
sim_card_id | ID      | Enter the id of the sim card you want to charge
remaining_days | Integer | Enter count days


## Archive Simcard

```graphql
mutation($simcardId: ID!) {
                    simcard {
                        archive(simcardId: $simcardId)
                    }
                }
```

This endpoint archive specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type    | Description
---------|---------|-------------
simcardId | ID      | Enter the id of the sim card you want to archive

## Unzip Simcard

```graphql
mutation($simcardId: ID!) {
                    simcard {
                        unarchive(simcardId: $simcardId)
                    }
                }
```

This endpoint unzip specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type    | Description
---------|---------|-------------
sim_card_id | ID      | Enter the id of the sim card you want to unzip


# Tariff

## Get All Tariffs

```graphql
query($offset: Int, $limit: Int, $filter: [FilterInput]!) {
            tariffs(pagination: {offset: $offset, limit: $limit},
                    filter: $filter,
                    sort: {order: DESC, field: "id"}) {
                items {
                    id
                    name
                    tariffType
                    isArchived
                    cost {
                        amount {
                            readable
                        }
                    }
                    callOutgoingRate {
                        amount {
                            readable
                        }
                    }
                    callIncomingRate {
                        amount {
                            readable
                        }
                    }
                    dataRate {
                        amount {
                            readable
                        }
                    }
                    callOutgoingRateAmount
                    callIncomingRateAmount
                    dataRateAmount
                    duration
                }
                count
            }
        }
```

This endpoint retrieves all tariffs.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Fields

Field | Type             | Description
------ |------------------| ---------------------
id | ID               | Internal ID Tariff                                                                                      
name | String           | Tariff Name
tariffType | String           | One of ["PREPAID_UNLIMITED", "PREPAID_PACKAGE", "POSTPAID_MINUTE", "MARGIN_CALCULATE", "RENEWAL_PREPAID_PACKAGE"]          
isArchived | Boolean          | Tariff status                     
cost | Array of objects | desc                                
amount | Integer          | desc                                
readable | Float            | desc                                
callOutgoingRate | Array of objects | desc                                
amount | Integer          | desc                                
readable | Object           | desc                                
callIncomingRate | Array of objects | desc                                
amount | Integer          | desc                                
readable | Float            | desc                                
dataRate | Array of objects | desc                                
amount | Integer          | desc                                
readable | Float            | desc                   
callOutgoingRateAmount | Integer          |                         
callIncomingRateAmount | Integer          | desc                                
dataRateAmount | Integer          | desc                       
duration | Integer          | desc     
count | Integer          | Maximum number of displayed objects 

### Variables

Parameter | Type             | Description
--------- |------------------| -----------
offset | Integer          | The offset query parameter is used to exclude from a response the first N items of a resource collection.
limit | Integer          | You can combine the limit and the offset options to request a particular set of items. Note that the offset option is applied before the limit option, regardless of its position in the request. That is, top results are selected from a collection where a set of items is already excluded.
filter | Array of objects | Read about [Filters](http://localhost:4567/?graphql#filters)
sort | Array of objects | Read about [Sorting](http://localhost:4567/?graphql#sortings)


## Get Specific Tariff

```graphql
query ($id: ID!) {
            tariff(id: $id) {
                id
                tariffType
                name
                duration
                callOutgoingRateAmount
                callIncomingRateAmount
                dataRateAmount
                cost {
                    amount {
                        readable
                    }
                }
                callOutgoingRate {
                    amount{
                        readable
                    }
                }
                callIncomingRate {
                    amount {
                        readable
                    }
                }
                dataRate {
                    amount {
                        readable
                    }
                }
                packages {
                    id
                    resource {
                        quota
                        unit
                    }
                }
            }
        }
```

This endpoint retrieves all tariffs.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Fields

Field | Type             | Description
------ |------------------| ---------------------
id | ID               | Internal ID Tariff                                                                                      
name | String           | Tariff Name
tariffType | String           | One of ["PREPAID_UNLIMITED", "PREPAID_PACKAGE", "POSTPAID_MINUTE", "MARGIN_CALCULATE", "RENEWAL_PREPAID_PACKAGE"]           
cost | Array of objects | desc                                
amount | Integer          | desc                                
readable | Float            | desc                                
callOutgoingRate | Array of objects | desc                                
amount | Integer          | desc                                
readable | Object           | desc                                
callIncomingRate | Array of objects | desc                                
amount | Integer          | desc                                
readable | Float            | desc                                
dataRate | Array of objects | desc                                
amount | Integer          | desc                                
readable | Float            | desc                   
callOutgoingRateAmount | Integer          |                         
callIncomingRateAmount | Integer          | desc                                
dataRateAmount | Integer          | desc                       
duration | Integer          | desc     
packages | Array of objects | 
id | ID               | ID Package
resource | Array of objects | 
quota | String           | desc
unit | Integer          | desc
count | Integer          | Maximum number of displayed objects 

### Variables

Parameter | Type             | Description
--------- |------------------| -----------
offset | Integer          | The offset query parameter is used to exclude from a response the first N items of a resource collection.
limit | Integer          | You can combine the limit and the offset options to request a particular set of items. Note that the offset option is applied before the limit option, regardless of its position in the request. That is, top results are selected from a collection where a set of items is already excluded.
filter | Array of objects | Read about [Filters](http://localhost:4567/?graphql#filters)
sort | Array of objects | Read about [Sorting](http://localhost:4567/?graphql#sortings)


## Activate Tariff

```graphql
mutation($simcardId: ID!, $tariffId: ID!) {
                simcard {
                    changeTariff(simcardId: $simcardId, tariffId: $tariffId, free: false)
                }
            }
```

This endpoint change specific tariff for specific simcard.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type    | Description
---------|---------|-------------
simcardId | ID      | Enter the id of the sim card you want to change tariff
tariffId | ID | Enter the id of the tariff you want to change

## Archive Tariff

```graphql
mutation($tariff_id: ID!) {
                tariff {
                    archive(id: $tariff_id)
                }
            }
```

This endpoint archive specific tariff.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type    | Description
---------|---------|-------------
tariff_id | ID | Enter the id of the tariff you want to archive


## Create Package

```graphql
mutation($tariffId: ID!,
                     $resourceQuota: ID!,
                     $resourceUnit: QuotaUnit!) {
                tariff {
                    createPackage(tariffId: $tariffId,
                                  resourceQuota: $resourceQuota,
                                  resourceUnit: $resourceUnit)
                }
            }
```

This endpoint create package for tariff.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
tariffId | ID   | Enter the id of the tariff you want to create package
resourceQuota | ID   |
resourceUnit | QuotaUnit | 


## Create Package

```graphql
mutation($tariffId: ID!,
                     $resourceQuota: ID!,
                     $resourceUnit: QuotaUnit!) {
                tariff {
                    createPackage(tariffId: $tariffId,
                                  resourceQuota: $resourceQuota,
                                  resourceUnit: $resourceUnit)
                }
            }
```

This endpoint create package for tariff.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type | Description
---------|------|-------------
tariffId | ID   | Enter the id of the tariff you want to create package
resourceQuota | ID   |
resourceUnit | QuotaUnit | 


## Update Tariff

```graphql
            mutation($id: ID!,
                     $name: String!,
                     $type: TariffType!,
                     $duration: Int!, 
                     $dataCost: Float!, 
                     $incomingCost: Float!,
                     $outgoingCost: Float!) {
                tariff {
                    updateTariff(id: $id,
                           name: $name,
                           type: $type,
                           duration: $duration, 
                           dataRateValue: $dataCost,
                           voiceIncomingRateValue: $incomingCost,
                           voiceOutgoingRateValue: $outgoingCost)
                }
            }
```

This endpoint update tariff.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type      | Description
---------|-----------|-------------
id | ID        | Enter the id of the tariff you want to update
name | String    | Enter the name of tariff
type | TariffType | One of ["RENEWAL_PREPAID_PACKAGE", "MARGIN_CALCULATE", "POSTPAID_MINUTE", "PREPAID_PACKAGE"]
duration | Integer | Enter duration
dataCost | Float | Enter data cost
incomingCost | Float | Enter incoming cost
outgoingCost | Float | Enter outgoing cost

## Delete Package

```graphql
            mutation($id: ID!) {
                tariff {
                    deletePackage(id: $id)
                }
            }
```

This endpoint delete package.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Variables

Variable | Type      | Description
---------|-----------|-------------
id | ID        | Enter the id of the tariff you want to delete


# Virtual Number

## Get all virtual numbers

```graphql
        query($offset: Int, $limit: Int, $filter: [FilterInput], $sort: [SortInput]) {
            didService {
                dids(pagination: {offset: $offset, limit: $limit},
                     filter: $filter,
                     sort: $sort) {
                     items {
                        id
                        simcard {
                            simId
                        }
                        msisdn
                        state
                        rentedAt
                        attachedAt
                        isSmsEnabled
                        cost {
                            amount {
                                readable
                            }
                        }
                    }
                    count
                }
            }
        }
```

This endpoint retrieve all virtual numbers.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`


### Fields

Field | Type             | Description
------ |------------------| ---------------------
id | ID               | Internal ID Virtual Number                                                                                      
simcard | Array of objects | Simcard
simId | String           | External Simcard ID
msisdn | String           | desc                                
state | String           | One of ["AVAILABLE_FOR_RENT", "RENTED", "ATTACHED" ]                                
rentedAt | Date             | desc                                
attachedAt | Date             | desc                                
isSmsEnabled | Boolean          | Supported sms                              
cost | Object           | desc                                
amount | Integer          | desc                                
readable | Float            | desc
count | Integer          | Maximum number of displayed objects 

### Variables

Parameter | Type             | Description
--------- |------------------| -----------
offset | Integer          | The offset query parameter is used to exclude from a response the first N items of a resource collection.
limit | Integer          | You can combine the limit and the offset options to request a particular set of items. Note that the offset option is applied before the limit option, regardless of its position in the request. That is, top results are selected from a collection where a set of items is already excluded.
filter | Array of objects | Read about [Filters](http://localhost:4567/?graphql#filters)
sort | Array of objects | Read about [Sorting](http://localhost:4567/?graphql#sortings)


## Get Rent list

```graphql
        query($prefix: String!,
              $limit: Int,
              $offset: Int) {
            didService {
                didForRent {
                    multitel(prefix: $prefix, limit: $limit, offset: $offset) {
                        id
                        number
                        monthlyPrice
                        isSmsEnabled
                    }
                }
            }
        }
```

This endpoint retrieve rent list.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Fields

Field | Type             | Description
------ |------------------| ---------------------
id | ID               | Internal ID Virtual Number                                                                                      
number | Array of objects | Virtual Number
monthlyPrice | Decimal          | Price
isSmsEnabled | Boolean          | Supported SMS             

### Variables

Parameter | Type             | Description                                                                                                                                                                                                                                                                                           
--------- |------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
prefix | String           | Prefix. Example 1785,1681, 1470                                                                                                                                                                                                                                                                       
limit | Integer          | You can combine the limit and the offset options to request a particular set of items. Note that the offset option is applied before the limit option, regardless of its position in the request. That is, top results are selected from a collection where a set of items is already excluded.filter | Array of objects | Read about [Filters](http://localhost:4567/?graphql#filters)
offset | Integer | The offset query parameter is used to exclude from a response the first N items of a resource collection.  


## Rent

```graphql
        mutation($didId: ID!) {
            didService {
                rent {
                    multitel(didId: $didId)
                }
            }
        }
```

This endpoint rent specific number.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`


### Variables

Parameter | Type | Description                                                                                                                                                                                                                                                                                           
--------- |------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
didId | ID   | Available id's you can get [this](http://localhost:4567/?graphql#get_rent_list)


## Detach

```graphql
        mutation($didId: ID!) {
            didService {
                detach(didId: $didId)
            }
        }
```

This endpoint detach number.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`


### Variables

Parameter | Type | Description                                                                                                                                                                                                                                                                                           
--------- |------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
didId | ID   | Available id's you can get [this](http://localhost:4567/?graphql#get_rent_list)


## Reject

```graphql
        mutation($didId: ID!) {
            didService {
                reject(didId: $didId)
            }
        }
```

This endpoint reject number.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`


### Variables

Parameter | Type | Description                                                                                                                                                                                                                                                                                           
--------- |------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
didId | ID   | Available id's you can get [this](http://localhost:4567/?graphql#get_rent_list)

## Rent Deductions

```graphql
        query($offset: Int, $limit: Int, $filter: [FilterInput]){
          didRentDeductions(pagination: {offset: $offset, limit: $limit},
                             filter: $filter,
                             sort: {order: DESC, field: "performedAt"}
          ) {
            items {
              id
              simCard{
                simId
              }
              type
              value
              performedAt
              comment
              oldValue
              newValue
            }
            count
          }
        }
```

This endpoint reject number.

### HTTP Request

`POST http://api.myphone.group/partner/graphql`

### Fields

Field | Type    | Description
------ |---------| ---------------------
id | ID      | Internal ID Virtual Number                                                                                      
simCard | Object  | Simcard
simId | String  | External ID Simcard
type | Boolean | Billing Type
value | Decimal | desc
performedAt | Date | desc
comment | String | desc
oldValue | Decimal | desc
newValue | Decimal | desc
count | Integer | Maximum number of displayed objects 

### Variables

Parameter | Type             | Description
--------- |------------------| -----------
offset | Integer          | The offset query parameter is used to exclude from a response the first N items of a resource collection.
limit | Integer          | You can combine the limit and the offset options to request a particular set of items. Note that the offset option is applied before the limit option, regardless of its position in the request. That is, top results are selected from a collection where a set of items is already excluded.
filter | Array of objects | Read about [Filters](http://localhost:4567/?graphql#filters)
sort | Array of objects | Read about [Sorting](http://localhost:4567/?graphql#sortings)
