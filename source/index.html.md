---
title: Swagger Petstore v1.0.0
language_tabs:
  - shell: Curl
  - ruby: Ruby
  - python: Python
  - go: Go
  - php: PHP
toc_footers:
  - >-
    <a href="https://github.com/Mermade/shins">Powered by Shin</a>
includes: []
search: true
highlight_theme: monokai-sublime
headingLevel: 2

---


# Introduction


Welcome to the unofficial API documentation for the Microfocus ArcSight Logger. This document describes all API endpoints available to users of the ArcSight Logger product.

The API itself supports only actions related to generating searches and retrieving it's results, and will only cover the endpoints available to the RESTful API.

# Mandatory legal part
All mentions of Microfocus, ArcSight and Logger is trademarked to Microfocus, this documentation is a collected source of educational material, any usage of products mentioned in this documentation requires a commercial license with MicroFocus or any of it's partners.

The documentation or associated open source software is not in any way part of the official documentation provided by Micro Focus and therefore not included in any support contract. It does not represent or try to imitate any products or services offered by Microfocus.

The documentation is provided "as-is" and can be changed or updated at any time, keeping it up to date for all versions is done by "best-effort".

While i do my best to keep this as updated as possible, there might be cases in which i am unable to do so, but anyone is allowed to fork, change or contribute to this project in any way they see fit.

Any other legal parts is covered in the LICENSE file and it's associated links.

# Authentication

To communicate with the API you need to include a so called API Token, this token is given to you after posting your username and password to the [login](#login) API endpoint. All further references to authToken during this documentation is related to that.

Please remember that all searches are related to your API token, this means that if your session times out due to inactivity, your search is lost, as logging in again will give you a new token.

After finalizing your actions, please remember to always [logout](#logout)

<aside class="notice">
Make sure to replace <code>authToken</code> with the authToken returned in the login response for all other API calls.
</aside>

# LoginService

## login
> Example Request

```shell
curl -X POST \
  https://HOSTNAME:9000/core-service/rest/LoginService/login \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'login=USERNAME&password=PASSWORD'
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/core-service/rest/LoginService/login")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/x-www-form-urlencoded'
request.body = "login=USERNAME&password=PASSWORD"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/core-service/rest/LoginService/login"

payload = "login=USERNAME&password=PASSWORD"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/x-www-form-urlencoded",
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/core-service/rest/LoginService/login"

  payload := strings.NewReader("login=USERNAME&password=PASSWORD")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/x-www-form-urlencoded")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/core-service/rest/LoginService/login');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/x-www-form-urlencoded',
  'Accept' => 'application/json'
));

$request->setContentType('application/x-www-form-urlencoded');
$request->setPostFields(array(
  'login' => 'USERNAME',
  'password' => 'PASSWORD'
));

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns HTTP 200 OK and a JSON response structured like this:

```json
[
  {
      "log.loginResponse": {
          "log.return": "7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo."
      }
  }
]
```

Returns a token used in all other API endpoints. This API call also supports GET with query parameters, but this is not recommended, as any sensitive data would be stored on the webservers and proxies utilizing this.

### HTTP Request

`POST https://HOSTNAME:9000/core-service/rest/LoginService/login`

### Query Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
login | String | null | Username with enough permissions to access the API | Yes
password | String | null | Password to related user account | Yes

## logout
```shell
curl -X POST \
  https://HOSTNAME:9000/core-service/rest/LoginService/logout \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d authToken=7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo.
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/core-service/rest/LoginService/logout")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/x-www-form-urlencoded'
request.body = "authToken=7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo."

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/core-service/rest/LoginService/logout"

payload = "authToken=7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo."
headers = {
    'Accept': "application/json",
    'Content-Type': "application/x-www-form-urlencoded",
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/core-service/rest/LoginService/logout"

  payload := strings.NewReader("authToken=7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo.")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/x-www-form-urlencoded")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/core-service/rest/LoginService/logout');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/x-www-form-urlencoded',
  'Accept' => 'application/json'
));

$request->setContentType('application/x-www-form-urlencoded');
$request->setPostFields(array(
  'authToken' => '7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo.'
));

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns HTTP Response 204 No Content on success:

Closes the session related to the authToken, with a 204 No Content responser upon success

### HTTP Request

`POST https://HOSTNAME:9000/core-service/rest/LoginService/logout`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
authToken | String | null | Auth Token that you want to logout | Yes

<aside class="warning">Please remember that any ongoing or finished search is tied with the session, when closed it will delete all searches related to the session</aside>

# SearchServices

## chart_data
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/chart_data \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id": "7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo.",
    "length": 100,
    "offset": 0
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI.parse('https://HOSTNAME:9000/server/search/chart_data')

json_headers = {'Content-Type' => 'application/json',
                'Accept' => 'application/json'}

data = {'search_session_id' => 100003,
        'user_session_id' => '7Kg2eRWvQGI3TBofLrFHMyHRv5FqIIqexHEMzzzcslo.',
        'length' => 100, 'offset' => 0}

http = Net::HTTP.new(url.host, url.port)

response = http.post(url.path, data.to_json, json_headers)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/chart_data"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"length\": 100,\r\n    \"offset\": 0\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/chart_data"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"length\": 100,\r\n    \"offset\": 0\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
use GuzzleHttp\Client;

$client = new Client([
    'base_uri' => 'https://HOSTNAME:9000/server/search/chart_data'
    'headers'   => [
        'Accept' => 'application/json',
        'Content-Type' => 'application/json'
    ],
    'json' => [
        'search_session_id'  => 10003,
        'user_session_id' => 'qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.',
        'length' => 100,
        'offset' => 0
    ]
]);

$response = $client->request('POST');
 
return json_decode($response->getBody()->getContents(), true);
```

> The above request returns HTTP Response 204 No Content on success:

Returns results from your search formatted to be used in charts or statistics, can also return values of search using aggregations like sort or head in their query.

### HTTP Request

`POST https://HOSTNAME:9000/server/search/chart_data`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes
length | Number | 25 | The amount of results you want to retrieve, maximum value is 100 | No
offset | Number | 0 | Auth Token that you want to logout | No

<aside class="warning">If no aggregation is used in the query during the intial search, the response will tell you that the search is not in a format that is supported for this API Endpoint</aside>

## close
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/close \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI.parse('https://HOSTNAME:9000/server/search/close')

json_headers = {'Content-Type' => 'application/json',
                'Accept' => 'application/json'}

data = {'search_session_id' => 100003, 'user_session_id' => 'qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.'}

http = Net::HTTP.new(url.host, url.port)

response = http.post(url.path, data.to_json, json_headers)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/close"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/close"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search/close');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns an empty HTTP 200 OK response upon success

This API call closes a search that has finalized. Search results from an API call is stored locally until the timeout you specified in your [search](#search), if you set a higher timeout to ensure data is not removed until you have finished your actions, you might want to remove your search manually before the timeout period, this is done with this API call.

### HTTP Request

`POST https://HOSTNAME:9000/server/search/close`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes

## drilldown
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/drilldown \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "end_time":"",
    "start_time":""
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI.parse('https://HOSTNAME:9000/server/search/close')

json_headers = {'Content-Type' => 'application/json',
                'Accept' => 'application/json'}

data = {'search_session_id' => 100003, 
        'user_session_id' => 'qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.',
        'start_time' => 'qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.'
        'end_time' => 'qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.'

          }

http = Net::HTTP.new(url.host, url.port)

response = http.post(url.path, data.to_json, json_headers)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/drilldown"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"end_time\":\"\",\r\n    \"start_time\":\"\"\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/drilldown"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"end_time\":\"\",\r\n    \"start_time\":\"\"\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search/drilldown');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "end_time":"",
    "start_time":""
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns an empty HTTP 200 OK response upon success

In certain cases you might want to only retrieve data from a specific time range even though your search was performed in a much larger timeframe.
This API call is used to change the timeframe of a currently completed search. First a [search](#search) is initiated, when the [status](#status) API call shows a successfully completed search you are able to utilize this [drilldown](#drilldown) API call to change the timeframe. If this returns an empty HTTP 200 OK response you can utilize any of the retrieval API calls to retrieve the same search, to only receive data within your newly defined `start_time` and `end_time`

### HTTP Request

`POST https://HOSTNAME:9000/server/search/drilldown`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes
end_time | timestamp | ANY | The new end time to be used for your finished search | Yes
start_time | timestamp | ANY | The new start time to be used for your finished search | Yes

## events
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/events \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id": "qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "dir": "forward",
    "fields": ["Event Time", "Device", "Logger", "Raw Message", "deviceVendor", "deviceProduct", "deviceVersion", "deviceEventClassId", "name"],
    "length": 1000,
    "offset": 0
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/server/search/events")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/json'
request.body = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"dir\": \"forward\",\r\n    \"fields\": [\"Event Time\", \"Device\", \"Logger\", \"Raw Message\", \"deviceVendor\", \"deviceProduct\", \"deviceVersion\", \"deviceEventClassId\", \"name\"],\r\n    \"length\": 1000,\r\n    \"offset\": 0\r\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/events"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"dir\": \"forward\",\r\n    \"fields\": [\"Event Time\", \"Device\", \"Logger\", \"Raw Message\", \"deviceVendor\", \"deviceProduct\", \"deviceVersion\", \"deviceEventClassId\", \"name\"],\r\n    \"length\": 1000,\r\n    \"offset\": 0\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/events"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"dir\": \"forward\",\r\n    \"fields\": [\"Event Time\", \"Device\", \"Logger\", \"Raw Message\", \"deviceVendor\", \"deviceProduct\", \"deviceVersion\", \"deviceEventClassId\", \"name\"],\r\n    \"length\": 1000,\r\n    \"offset\": 0\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search/events');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id": "qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "dir": "forward",
    "fields": ["Event Time", "Device", "Logger", "Raw Message", "deviceVendor", "deviceProduct", "deviceVersion", "deviceEventClassId", "name"],
    "length": 1000,
    "offset": 0
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns HTTP 200 OK and a JSON response structured like this:

```json
[
  {
      "fields": [
          {
              "name": "_rowId",
              "type": "string",
              "alias": "_rowId"
          },
          {
              "name": "Event Time",
              "type": "date",
              "alias": "Event Time"
          },
          {
              "name": "Logger",
              "type": "string",
              "alias": "Logger"
          },
          {
              "name": "Device",
              "type": "string",
              "alias": "Device"
          },
          {
              "name": "Receipt Time",
              "type": "date",
              "alias": "Receipt Time"
          },
          {
              "name": "deviceReceiptTime",
              "type": "date",
              "alias": "deviceReceiptTime"
          },
          {
              "name": "deviceCustomString2",
              "type": "string",
              "alias": "deviceCustomString2"
          },
          {
              "name": "destinationAddress",
              "type": "string",
              "alias": "destinationAddress"
          },
          {
              "name": "deviceCustomNumber3Label",
              "type": "string",
              "alias": "deviceCustomNumber3Label"
          },
          {
              "name": "deviceVersion",
              "type": "string",
              "alias": "deviceVersion"
          },
          {
              "name": "name",
              "type": "string",
              "alias": "name"
          },
          {
              "name": "deviceAddress",
              "type": "string",
              "alias": "deviceAddress"
          },
          {
              "name": "deviceVendor",
              "type": "string",
              "alias": "deviceVendor"
          },
          {
              "name": "Version",
              "type": "string",
              "alias": "Version"
          },
          {
              "name": "deviceCustomNumber1Label",
              "type": "string",
              "alias": "deviceCustomNumber1Label"
          },
          {
              "name": "deviceEventCategory",
              "type": "string",
              "alias": "deviceEventCategory"
          },
          {
              "name": "endTime",
              "type": "date",
              "alias": "endTime"
          },
          {
              "name": "fileName",
              "type": "string",
              "alias": "fileName"
          },
          {
              "name": "deviceCustomNumber2",
              "type": "number",
              "alias": "deviceCustomNumber2"
          },
          {
              "name": "deviceCustomNumber1",
              "type": "number",
              "alias": "deviceCustomNumber1"
          },
          {
              "name": "baseEventCount",
              "type": "number",
              "alias": "baseEventCount"
          },
          {
              "name": "startTime",
              "type": "date",
              "alias": "startTime"
          },
          {
              "name": "deviceCustomNumber3",
              "type": "number",
              "alias": "deviceCustomNumber3"
          },
          {
              "name": "agentSeverity",
              "type": "string",
              "alias": "agentSeverity"
          },
          {
              "name": "fsize",
              "type": "string",
              "alias": "fsize"
          },
          {
              "name": "deviceProduct",
              "type": "string",
              "alias": "deviceProduct"
          },
          {
              "name": "deviceEventClassId",
              "type": "string",
              "alias": "deviceEventClassId"
          },
          {
              "name": "deviceCustomNumber2Label",
              "type": "string",
              "alias": "deviceCustomNumber2Label"
          },
          {
              "name": "deviceCustomString2Label",
              "type": "string",
              "alias": "deviceCustomString2Label"
          },
          {
              "name": "fileType",
              "type": "string",
              "alias": "fileType"
          },
          {
              "name": "deviceCustomString6",
              "type": "string",
              "alias": "deviceCustomString6"
          },
          {
              "name": "deviceCustomString6Label",
              "type": "string",
              "alias": "deviceCustomString6Label"
          },
          {
              "name": "deviceCustomString1",
              "type": "string",
              "alias": "deviceCustomString1"
          },
          {
              "name": "deviceCustomString3",
              "type": "string",
              "alias": "deviceCustomString3"
          },
          {
              "name": "deviceCustomString1Label",
              "type": "string",
              "alias": "deviceCustomString1Label"
          },
          {
              "name": "deviceCustomString3Label",
              "type": "string",
              "alias": "deviceCustomString3Label"
          },
          {
              "name": "destinationUserId",
              "type": "string",
              "alias": "destinationUserId"
          },
          {
              "name": "destinationUserName",
              "type": "string",
              "alias": "destinationUserName"
          },
          {
              "name": "sourceAddress",
              "type": "string",
              "alias": "sourceAddress"
          },
          {
              "name": "message",
              "type": "string",
              "alias": "message"
          },
          {
              "name": "deviceCustomString4",
              "type": "string",
              "alias": "deviceCustomString4"
          },
          {
              "name": "deviceCustomString4Label",
              "type": "string",
              "alias": "deviceCustomString4Label"
          },
          {
              "name": "fileId",
              "type": "string",
              "alias": "fileId"
          }
      ],
      "results": [
          [
              "CC-0@Local",
              1541447890136,
              "Local",
              "Logger",
              1541448490709,
              1541447890135,
              "CurrentValue",
              "127.0.0.1",
              "used (MB)",
              "6.6.0.8204.0",
              "Storage Group Space Used",
              "127.0.0.1",
              "ArcSight",
              "0",
              "Percent Used",
              "/Monitor/StorageGroup/Space/Used",
              1541447890135,
              "Default Storage Group",
              180,
              2,
              1,
              1541447890135,
              1024,
              "1",
              "45",
              "Logger",
              "storagegroup:100",
              "retention period (days)",
              "timeframe",
              "storageGroup",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              ""
          ],
          [
              "CC-1@Local",
              1541447890136,
              "Local",
              "Logger",
              1541448490709,
              1541447890136,
              "CurrentValue",
              "127.0.0.1",
              "used (MB)",
              "6.6.0.8204.0",
              "Storage Group Space Used",
              "127.0.0.1",
              "ArcSight",
              "0",
              "Percent Used",
              "/Monitor/StorageGroup/Space/Used",
              1541447890136,
              "Internal Event Storage Group",
              365,
              33,
              1,
              1541447890136,
              1024,
              "1",
              "3",
              "Logger",
              "storagegroup:100",
              "retention period (days)",
              "timeframe",
              "storageGroup",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              "",
              ""
          ],
      ]
  }
]
```

After a successfull [search](#search) has been finalized you can now retrieve the data. There is several ways to retrieve it described in this document, all depending on how you want the returned data format to be.

The event API call returns all events associated with the specified search id. If the hit count of the completed search is larger than 1000 then only the first 1000 events will be shown.
This can be circumvented by setting the `length` parameter to a higher number, though the maximum is 10000 events on newer versions of the Logger (6.x i believe), and 1000 on older versions.

### HTTP Request

`POST https://HOSTNAME:9000/server/search/events`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes
dir | String | forward | In which order you want to sort the returned results, can be forward or backwards. | No
fields | String | Null | Defines which fields are to be returned for each event, defaults to all fields. | No
length | Number | 1000 | The maximum amount of events returned. | No
offset | Number | Null | Which event count to start at, for example if more than maximum length is needed | No

<aside class="warning">If you want to retrieve all events from a search that has a higher hit count than the maximum 10000, you will need to run several concurrent event API calls, each setting the value in the `offset` parameter higher, as this describes from which returned eventcount to start from.</aside>

## histogram
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/histogram \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/server/search/histogram")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/json'
request.body = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/histogram"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json"
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/histogram"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search/histogram');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns HTTP 200 OK and a JSON response structured like this:

```json
[
  {
      "bucket_count": 74,
      "bucket_width": 60000,
      "start_bucket_time": 1541447890000,
      "hits": [
          4,
          17,
          17,
          20,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          20,
          17,
          17,
          17,
          17,
          17,
          17,
          23,
          17,
          18,
          20,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          18,
          20,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          20,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          20,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          17,
          20,
          17,
          17,
          17,
          17,
          17,
          17,
          0,
          1,
          0,
          3
      ]
  }
]
```

Returns your events in an histogram format which is useful in cases you only want to retrieve data to be used in charts for example.
The `bucket_count` is the amount of buckets collected, `bucket_width` is the time in milliseconds per bucket, `start_bucket_time` is the UNIXTIME or Epoch time value from when the starting timeframe and last `hits` are the amount of hits per `bucket_width` timeframe.

### HTTP Request

`POST https://HOSTNAME:9000/server/search/histogram`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes

## raw_events
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/raw_events \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "row_ids": ["CC-0@Local", "CC-1@Local"]
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/server/search/raw_events")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/json'
request.body = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"row_ids\": [\"CC-0@Local\", \"CC-1@Local\"]\r\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/raw_events"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"row_ids\": [\"CC-0@Local\", \"CC-1@Local\"]\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/raw_events"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"row_ids\": [\"CC-0@Local\", \"CC-1@Local\"]\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search/raw_events');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "row_ids": ["CC-0@Local", "CC-1@Local"]
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns HTTP 200 OK and all raw events in an array:

```json
[
    "CEF:0|ArcSight|Logger|6.6.0.8204.0|storagegroup:100|Storage Group Space Used|1| cat=/Monitor/StorageGroup/Space/Used cn1=2 cn1Label=Percent Used cn2=180 cn2Label=retention period (days) cn3=1024 cn3Label=used (MB) cs2=CurrentValue cs2Label=timeframe dst=127.0.0.1 dvc=127.0.0.1 end=1541447890135 fileType=storageGroup fname=Default Storage Group fsize=45 rt=1541447890135",
    "CEF:0|ArcSight|Logger|6.6.0.8204.0|storagegroup:100|Storage Group Space Used|1| cat=/Monitor/StorageGroup/Space/Used cn1=33 cn1Label=Percent Used cn2=365 cn2Label=retention period (days) cn3=1024 cn3Label=used (MB) cs2=CurrentValue cs2Label=timeframe dst=127.0.0.1 dvc=127.0.0.1 end=1541447890136 fileType=storageGroup fname=Internal Event Storage Group fsize=3 rt=1541447890136"
]
```

The raw_events API endpoint is utilized to retrieve raw logging from specific rows of your search results. Retrieving the [events](#events) from a successful [search](#search) normally specifies the appropriate row id's on the first column, as can be seen from the example.

### HTTP Request

`POST https://HOSTNAME:9000/server/search/raw_events`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes
row_ids | Array of Strings | null | The specific row_ids wanted from a finalized search | Yes

## status
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/status \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/server/search/status")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/json'
request.body = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/status"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json"
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/status"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search/status');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns HTTP 200 OK and a JSON response structured like this:

```json
[
  {
      "status": "complete",
      "result_type": "histogram",
      "hit": 1726,
      "scanned": 1726,
      "elapsed": "00:00:00.276",
      "message": []
  }
]
```

The status API endpoint is used to monitor the current status of any existing [search](#search). 

### HTTP Request

`POST https://HOSTNAME:9000/server/search/status`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes

<aside class="warning">In certain cases, for example when a search creates an error, the HTTP response is still 200 OK, though the status is then changed to "error". Keep in mind if you only utilize HTTP status codes for error checking.</aside>

## search
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id": "qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "discover_fields": false,
    "end_time": "2018-10-26T11:00:00.000Z",
    "summary_fields": ["Event Time", "Device", "Logger", "Raw Message", "deviceVendor", "deviceProduct", "deviceVersion", "deviceEventClassId", "name"],
    "field_summary": false, 
    "local_search": true,
    "query":"",
    "search_type":"interactive",
    "start_time":"2018-10-26T09:00:00.000Z",
    "timeout": 120000
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/server/search")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/json'
request.body = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"discover_fields\": false,\r\n    \"end_time\": \"2018-10-26T11:00:00.000Z\",\r\n    \"summary_fields\": [\"Event Time\", \"Device\", \"Logger\", \"Raw Message\", \"deviceVendor\", \"deviceProduct\", \"deviceVersion\", \"deviceEventClassId\", \"name\"],\r\n    \"field_summary\": false, \r\n    \"local_search\": true,\r\n    \"query\":\"\",\r\n    \"search_type\":\"interactive\",\r\n    \"start_time\":\"2018-10-26T09:00:00.000Z\",\r\n    \"timeout\": 120000\r\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"discover_fields\": false,\r\n    \"end_time\": \"2018-10-26T11:00:00.000Z\",\r\n    \"summary_fields\": [\"Event Time\", \"Device\", \"Logger\", \"Raw Message\", \"deviceVendor\", \"deviceProduct\", \"deviceVersion\", \"deviceEventClassId\", \"name\"],\r\n    \"field_summary\": false, \r\n    \"local_search\": true,\r\n    \"query\":\"\",\r\n    \"search_type\":\"interactive\",\r\n    \"start_time\":\"2018-10-26T09:00:00.000Z\",\r\n    \"timeout\": 120000\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\": \"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\",\r\n    \"discover_fields\": false,\r\n    \"end_time\": \"2018-10-26T11:00:00.000Z\",\r\n    \"summary_fields\": [\"Event Time\", \"Device\", \"Logger\", \"Raw Message\", \"deviceVendor\", \"deviceProduct\", \"deviceVersion\", \"deviceEventClassId\", \"name\"],\r\n    \"field_summary\": false, \r\n    \"local_search\": true,\r\n    \"query\":\"\",\r\n    \"search_type\":\"interactive\",\r\n    \"start_time\":\"2018-10-26T09:00:00.000Z\",\r\n    \"timeout\": 120000\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id": "qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.",
    "discover_fields": false,
    "end_time": "2018-10-26T11:00:00.000Z",
    "summary_fields": ["Event Time", "Device", "Logger", "Raw Message", "deviceVendor", "deviceProduct", "deviceVersion", "deviceEventClassId", "name"],
    "field_summary": false, 
    "local_search": true,
    "query":"",
    "search_type":"interactive",
    "start_time":"2018-10-26T09:00:00.000Z",
    "timeout": 120000
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns HTTP 200 OK and a JSON response structured like this:

```json
[
  {
      "sessionId": "18"
  }
]
```

The search API endpoint is utilized when you want to retrieve any sort of data or information. When a search is executed a [status](#status) API call can be used to check if it is ongoing, have completed or failed.

When creating a search the minimum amount of information you need to provide is an `user_session_id` and a `search_session_id`.

If no other information is provided it will run the search with it's default values.

It is important to know that the `search_session_id` is a integer value set by the user and not the application. While there exists certain situations where two searches can be run with the same ID it is not recommended, for example you can run a new search with the same ID if the first one has finalized.

It is recommended to set the `search_session_id` to an ever increasing numerical value, like UNIXTIME/Epoch time to ensure there is never any situations which can cause an duplicated entry.

If you are experiencing that a search is missing once complete then it is important to note that the default timeout value is quite low. This is the timeout for when the search, when finished, removes itself and the results and not for how long it can run.

The returned `SessionID` in the response when successfully initiating a search is the reference ID internally on the Logger, this is not reused anywhere in your API calls.
It only allows you to login to the Logger web interface, click on Configuration in the top menu and choose Running Searches to display the currently active searches, with a SessionID to differentiate them.

<aside class="warning">A search is linked to your current authToken, meaning that if the user session ever times out, the search and it's results is lost.</aside>
<aside class="warning">Examples currently do not escape special characters in the query parameter, added on todo</aside>

### HTTP Request

`POST https://HOSTNAME:9000/server/search`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes
discover_fields | Boolean | false | If new fields should be discovered for the returned events | If field_summary is true
end_time | Timestamp | null | End time for when providing a specific timeframe | If start_time is specified
start_time | Timestamp | Timestamp 2 hours back from current | Start time for when providing a specific timeframe | If end_time is specified
summary_fields | Array of Strings | Values in example | List of displaynames of fields if creating a summary | If field_summary is true
field_summary | Boolean | false | Indicates if you want to retrieve a field summary | No
local_search | Boolean | true | If utilizing Logger Pools and you want to search over all loggers | No
query | String | null(*) | A single string representing your whole query, as being run on the Logger Web interface | No
search_type | String | interactive | Only supports interactive, so don't know why this is a parameter | No
timeout | Number | 120000 | How many milliseconds the search and it's results is stored after completed | No


## stop
```shell
curl -X POST \
  https://HOSTNAME:9000/server/search/stop \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}'
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://HOSTNAME:9000/server/search/stop")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Accept"] = 'application/json'
request["Content-Type"] = 'application/json'
request.body = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}"

response = http.request(request)
puts response.read_body
```

```python
import requests

url = "https://HOSTNAME:9000/server/search/stop"

payload = "{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}"
headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://HOSTNAME:9000/server/search/stop"

  payload := strings.NewReader("{\r\n    \"search_session_id\": 100003,\r\n    \"user_session_id\":\"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg.\"\r\n}")

  req, _ := http.NewRequest("POST", url, payload)

  req.Header.Add("Accept", "application/json")
  req.Header.Add("Content-Type", "application/json")

  res, _ := http.DefaultClient.Do(req)

  defer res.Body.Close()
  body, _ := ioutil.ReadAll(res.Body)

  fmt.Println(res)
  fmt.Println(string(body))

}
```

```php
$request = new HttpRequest();
$request->setUrl('https://HOSTNAME:9000/server/search/stop');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
));

$request->setBody('{
    "search_session_id": 100003,
    "user_session_id":"qFkEjr11ClMzLL0hitX1tbi1Oc-hl9emRVPULOYP5hg."
}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

> The above request returns an empty HTTP 200 OK response upon success

The stop API call ends a currently active search. The difference between stop and [close](#close) is that the results that are already found is still available to be retrieved until the timeout specified when running your [search](#search)

### HTTP Request

`POST https://HOSTNAME:9000/server/search/stop`

### URL Parameters

Parameter | Type | Default | Description | Required |
--------- | ---- | ------- | ----------- | -------- |
search_session_id | Number | null | The choosen search session used when creating the search | Yes
user_session_id | String | null | Auth Token returned by the login API endpoint | Yes