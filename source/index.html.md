---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='http://kaspr.fr'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Kaspr API! You can use our API to access Kaspr API endpoints, which can get information on various , kittens, and breeds in our database.



# Authentication



Kaspr uses Bearer API keys to allow access to the API. You can register a new API key at our [developer portal](http://kaspr.fr).

Kaspr expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer YOUR-API-KEY-HERE`

<aside class="notice">
You must replace <code>YOUR-API-KEY-HERE</code> with your personal API key.
</aside>

# Rate limiting


Kaspr allows a certain number requests per hour sent from a single key. The API Key will be blocked after passing the limit.

If blocked, the access will be reset with the API Key after a certain amount of time.

Information about the the rate limiting will be provided in the response header of every request:

`X-RateLimit-Limit: max number of request per hour `<br><br>
`X-RateLimit-Remaining: number of remaining requests before reset` <br><br>
`X-RateLimit-Reset: time in ms until reset`

# Credits


Kaspr public API shares the same credits system as in the web application.

The user will will charged a certain amount of credits after requests.

Information about the the rate limiting will be provided in the response header of every request except the  :

`Decreased-Credits: amount ofcredits used for the request`<br><br>
`Remaining-Credits: amount of credits left`

# Keys

## verifyKey

```python
import requests

headers = {
    'Authorization': 'YOUR-API-KEY-HERE',
}

response = requests.get('http://developer.kaspr.fr/keys/verifyKey', headers=headers)
```

```shell
curl "http://developer.kaspr.fr/keys/verifyKey"
  -H "Authorization: YOUR-API-KEY-HERE"
```

```ruby
require 'net/http'
require 'uri'

uri = URI.parse("http://developer.kaspr.fr/keys/verifyKey")
request = Net::HTTP::Get.new(uri)
request["Authorization"] = "YOUR-API-KEY-HERE"

req_options = {
  use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
  http.request(request)
end

# response.code
# response.body
```

```javascript
var request = require('request');

var headers = {
    'Authorization': 'YOUR-API-KEY-HERE'
};

var options = {
    url: 'http://developer.kaspr.fr/keys/verifyKey',
    headers: headers
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);
```

> > The above command returns authenticated user's email:


```json
{
  "user": "email@adress"
}
```

This endpoint verifies if our API Key is valid.

### HTTP Request

`GET http://developer.kaspr.io/keys/verifyKey`



<aside class="success">
Remember — You have to be authenticated!
</aside>


# Leads

## Get Lead
```shell
curl -X POST
  -H "Authorization: YOUR-API-KEY-HERE"
  -H "Content-Type: application/json" 
  --data '{"id":"linkedinId","name":"Linkedin Name"}'  
  "http://developer.kaspr.fr/profile/profile"
```

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://developer.kaspr.fr/profile/profile")
request = Net::HTTP::Post.new(uri)
request.content_type = "application/json"
request["Authorization"] = "YOUR-API-KEY-HERE"
request.body = JSON.dump({
  "id" => "linkedinId",
  "name" => "Linkedin Name"
})

req_options = {
  use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
  http.request(request)
end

# response.code
# response.body
```

```python
import requests

headers = {
    'Authorization': 'YOUR-API-KEY-HERE',
    'Content-Type': 'application/json',
}

data = '{"id":"linkedinId","name":"Linkedin Name"}'

response = requests.post('http://developer.kaspr.fr/profile/profile', headers=headers, data=data)
```



```javascript
var request = require('request');

var headers = {
    'Authorization': 'YOUR-API-KEY-HERE',
    'Content-Type': 'application/json'
};

var dataString = '{"id":"linkedinId","name":"Linkedin Name"}';

var options = {
    url: 'http://developer.kaspr.fr/profile/profile',
    method: 'POST',
    headers: headers,
    body: dataString
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);

```

> > The above command returns JSON with an object "profile" as an object conaining the information of the prospect


```json
{
    "profile": {
        "id": "Casper-Linkedin",
        "name": "Casper The Ghost",
        "firstName": "Casper",
        "lastName": "The Ghost",
        "emails": [
            {
                "email": "Casper@example.com",
                "valid": true
            },
            {
                "email": "Casper@gmail.com",
                "valid": null
            }
        ],
        "currentProEmails": [
            "Casper@example.com"
        ],
        "currentPersonalEmails": [
            "Casper@gmail.com"
        ],
        "phones": [],
        "location": "Home",
        "title": "Ghost",
        "companyName": "Home",
        "fetchedAt": 1588682813481,
        "currentProEmail": "Casper@example.com",
        "processingTime": 3.885,
        "currentEmail": "Casper@example.com"
    }
}
```

This endpoint retrieves emails or phone of a certain prospect or lead.

### HTTP Request

`POST http://developer.kaspr.io/profile/profile`

### body Parameters

Parameter | Required | Type | Description | Default
--------- | -------- | ---- | ----------- | -------
id | true | string | represents the Linkedin ID of the lead "https://www.linkedin.com/in/id-here/" | Na
name | true | string | represents the likedin name of the lead | Na
isPhoneRequired | false | boolean | If set to true, the data will be sure to include phone numbers. Else, no data will be returned. | false

<aside class="success">
Remember — You have to be authenticated!
</aside>



# Company

## Get Pattern

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://developer.kaspr.fr/company/domainPattern")
request = Net::HTTP::Post.new(uri)
request.content_type = "application/json"
request["Authorization"] = "YOUR-API-KEY-HERE"
request.body = JSON.dump({
  "domain" => "company@domain"
})

req_options = {
  use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
  http.request(request)
end

# response.code
# response.body
```

```python
import requests

headers = {
    'Authorization': 'YOUR-API-KEY-HERE',
    'Content-Type': 'application/json',
}

data = '{"domain":"company@domain"}'

response = requests.post('http://developer.kaspr.fr/company/domainPattern', headers=headers, data=data)

```

```shell
curl -X POST 
  -H "Authorization: YOUR-API-KEY-HERE"
  -H "Content-Type: application/json" 
  --data '{"domain":"company@domain"}'  
  "http://developer.kaspr.fr/company/domainPattern"
```

```javascript
var request = require('request');

var headers = {
    'Authorization': 'YOUR-API-KEY-HERE',
    'Content-Type': 'application/json'
};

var dataString = '{"domain":"company@domain"}';

var options = {
    url: 'http://developer.kaspr.fr/company/domainPattern',
    method: 'POST',
    headers: headers,
    body: dataString
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);

```

> The above command returns JSON with an array "pattern" as a list of pattern with the score of validity of each one:

```json
{
    "patterns": [
        {
            "pattern": "{f}{last}@example.com",
            "score": 0.64560313367866
        },
        {
            "pattern": "{first}{last}@example.com",
            "score": 0.583964853062278
        },
        {
            "pattern": "{first}.{last}@example.com",
            "score": 0.574788995391232
        },
        {
            "pattern": "{first}-{last}@example.com",
            "score": 0.477391044114061
        }
    ]
}
```

This endpoint retrieves the patterns of emails of a certain company.

### HTTP Request

`POST http://developer.kaspr.io/company/domainPattern`

### body Parameters

Parameter | Required | Type | Description | Default
--------- | -------- | ---- | ----------- | -------
domain | true | string | domain of a company | Na

<aside class="success">
Remember — You have to be authenticated!
</aside>

## Get Employees

```ruby
require 'net/http'
require 'uri'
require 'json'

uri = URI.parse("http://developer.kaspr.fr/company/domainEmployees")
request = Net::HTTP::Post.new(uri)
request.content_type = "application/json"
request["Authorization"] = "YOUR-API-KEY-HERE"
request.body = JSON.dump({
  "domain" => "company@domain",
  "contactsNumberLimit" => 10,
  "isPhoneRequired" => true
})

req_options = {
  use_ssl: uri.scheme == "https",
}

response = Net::HTTP.start(uri.hostname, uri.port, req_options) do |http|
  http.request(request)
end

# response.code
# response.body
```

```python
import requests

headers = {
    'Authorization': 'YOUR-API-KEY-HERE',
    'Content-Type': 'application/json',
}

data = '{"domain":"company@domain","contactsNumberLimit":10,"isPhoneRequired":true}'

response = requests.post('http://developer.kaspr.fr/company/domainEmployees', headers=headers, data=data)

```

```shell
curl -X POST 
  -H "Authorization: YOUR-API-KEY-HERE"
  -H "Content-Type: application/json" 
  --data '{"domain":"company@domain","contactsNumberLimit":10,"isPhoneRequired":true}'  
  "http://developer.kaspr.fr/company/domainEmployees"
```

```javascript
var request = require('request');

var headers = {
    'Authorization': 'YOUR-API-KEY-HERE',
    'Content-Type': 'application/json'
};

var dataString = '{"domain":"company@domain","contactsNumberLimit":10,"isPhoneRequired":true}';

var options = {
    url: 'http://developer.kaspr.fr/company/domainEmployees',
    method: 'POST',
    headers: headers,
    body: dataString
};

function callback(error, response, body) {
    if (!error && response.statusCode == 200) {
        console.log(body);
    }
}

request(options, callback);

```

> > The above command returns JSON with an array "employees" as a list where each object contains the information of an employee:


```json
{
    "employees": [
        {
            "firstName": "Casper",
            "lastName": "The Ghost",
            "name": "Casper The Gost",
            "company": "Home",
            "job": "Ghost",
            "email": "Casper@example.com",
            "emails": [
                {
                    "email": "Casper@example.com",
                    "valid": null
                }
            ],
            "phones": [ "+33 0 00 00 00 00"],
            "phone": "+33 0 00 00 00 00",
            "location": "Home"
        },
        {
            "firstName": "Kathleen",
            "lastName": "Harvey",
            "name": "Kathleen Harvey",
            "company": "Home",
            "job": "Kid",
            "email": "Kathleen-Harvey@example.com",
            "emails": [
                {
                    "email": "Kathleen-Harvey@example.com",
                    "valid": null
                }
            ],
            "phones": [
                "+33 0 00 00 00 00"
            ],
            "phone": "+33 0 00 00 00 00",
            "location": "Home"
        }
    ]
}
```

This endpoint retrieves the list of employees of a certain company.


### HTTP Request

`POST http://developer.kaspr.io/company/domainEmployees`

### URL Parameters

Parameter | Required |Type | Description | Default
--------- | -------- |---- | ----------- | -------
domain |  true |string | domain of a company | Na
contactsNumberLimit | false | integer | maximum number of employees to retrieve | 5
isPhoneRequired | false | boolean | If set to true, the data will be sure to include phone numbers. Else, no data will be returned. | false


<aside class="success">
Remember — You have to be authenticated!
</aside>

