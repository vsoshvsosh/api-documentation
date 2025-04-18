# Кампании

Кампании имеют следующую структуру:

```text
{
  id                  : int64
  name                : string
  created_date        : string(datetime)
  launch_date         : string(datetime)
  send_by_date        : string(datetime)
  completed_date      : string(datetime)
  template            : Template
  page                : Page
  status              : string
  results             : []Result
  groups              : []Group
  timeline            : []Event
  smtp                : SMTP
  url                 : string
}
```

Объекты `template`, `page`, `groups` и `smtp` являются объектами Ruphish. Их формат можно найти в соответствующих конечных точках API.

### События кампании

Ruphish отслеживает каждое событие кампании в её `timeline`. Каждое событие имеет следующий формат:

```text
{
  email                : string
  time                 : string(datetime)
  message              : string
  details              : string(JSON)
}
```

Поле `details` — это строка, содержащая JSON с необработанными данными о событии (такими как предоставленные учетные данные, информация о пользовательском агенте и т.д.). Поле `details` имеет следующий формат:

```text
{
  payload              : object
  browser              : object
}
```

### Результаты кампании

Кроме того, результаты кампании хранятся в атрибуте `results`. Он имеет формат, аналогичный членам `Group`, то есть они имеют следующую структуру:

```text
{
  id                   : int64
  first_name           : string
  last_name            : string
  position             : string
  status               : string
  ip                   : string
  latitude             : float
  longitude            : float
  send_date            : string(datetime)
  reported             : boolean
}
```

{% api-method method="get" host="https://localhost:3333" path="/api/campaigns/" %}
{% api-method-summary %}
Получить Кампании
{% endapi-method-summary %}

{% api-method-description %}
Возвращает список кампаний.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "id": 1,
    "name": "Example Campaign",
    "created_date": "2018-10-08T15:56:29.48815Z",
    "launch_date": "2018-10-08T15:56:00Z",
    "send_by_date": "0001-01-01T00:00:00Z",
    "completed_date": "0001-01-01T00:00:00Z",
    "template": {
      "id": 1,
      "name": "Example Template",
      "subject": "Click here!",
      "text": "",
      "html": "\u003chtml\u003e\n\u003chead\u003e\n\t\u003ctitle\u003e\u003c/title\u003e\n\u003c/head\u003e\n\u003cbody\u003e\n\u003cp\u003eClick \u003ca href=\"{{.URL}}\"\u003ehere\u003c/a\u003e!\u003c/p\u003e\n{{.Tracker}}\u003c/body\u003e\n\u003c/html\u003e\n",
      "modified_date": "2018-10-08T15:54:56.258392Z",
      "attachments": []
    },
    "page": {
      "id": 1,
      "name": "Example Landing Page",
      "html": "\u003chtml\u003e\u003chead\u003e\n\t\u003ctitle\u003e\u003c/title\u003e\n\u003c/head\u003e\n\u003cbody\u003e\n\u003cp\u003eLanding page HTML\u003c/p\u003e\n\n\n\u003c/body\u003e\u003c/html\u003e",
      "capture_credentials": false,
      "capture_passwords": false,
      "redirect_url": "",
      "modified_date": "2018-10-08T15:55:16.416396Z"
    },
    "status": "In progress",
    "results": [
      {
        "id": "hoqKYFn",
        "status": "Email Sent",
        "ip": "",
        "latitude": 0,
        "longitude": 0,
        "send_date": "2018-10-08T15:56:29.535158Z",
        "reported": false,
        "modified_date": "2018-10-08T15:56:29.535158Z",
        "email": "user@example.com",
        "first_name": "Example",
        "last_name": "User",
        "position": ""
      },
      {
        "id": "VYrDwtG",
        "status": "Clicked Link",
        "ip": "::1",
        "latitude": 0,
        "longitude": 0,
        "send_date": "2018-10-08T15:56:29.548722Z",
        "reported": false,
        "modified_date": "2018-10-08T15:56:46.955281Z",
        "email": "foo@bar.com",
        "first_name": "Foo",
        "last_name": "Bar",
        "position": ""
      }
    ],
    "timeline": [
      {
        "email": "",
        "time": "2018-10-08T15:56:29.49172Z",
        "message": "Campaign Created",
        "details": ""
      },
      {
        "email": "user@example.com",
        "time": "2018-10-08T15:56:29.535158Z",
        "message": "Email Sent",
        "details": ""
      },
      {
        "email": "foo@bar.com",
        "time": "2018-10-08T15:56:29.548722Z",
        "message": "Email Sent",
        "details": ""
      },
      {
        "email": "foo@bar.com",
        "time": "2018-10-08T15:56:44.679743Z",
        "message": "Email Opened",
        "details": "{\"payload\":{\"rid\":[\"VYrDwtG\"]},\"browser\":{\"address\":\"::1\",\"user-agent\":\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36\"}}"
      },
      {
        "email": "foo@bar.com",
        "time": "2018-10-08T15:56:46.955281Z",
        "message": "Clicked Link",
        "details": "{\"payload\":{\"rid\":[\"VYrDwtG\"]},\"browser\":{\"address\":\"::1\",\"user-agent\":\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36\"}}"
      }
    ],
    "smtp": {
      "id": 1,
      "interface_type": "SMTP",
      "name": "Example Sending Profile",
      "host": "localhost:1025",
      "from_address": "Test User \u003ctest@test.com\u003e",
      "ignore_cert_errors": true,
      "headers": [],
      "modified_date": "2018-09-04T01:24:21.691924069Z"
    },
    "url": "http://localhost"
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/campaigns/:id" %}
{% api-method-summary %}
Получить Кампанию
{% endapi-method-summary %}

{% api-method-description %}
Возвращает кампанию по указанному ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID кампании
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 1,
  "name": "Example Campaign",
  "created_date": "2018-10-08T15:56:29.48815Z",
  "launch_date": "2018-10-08T15:56:00Z",
  "send_by_date": "0001-01-01T00:00:00Z",
  "completed_date": "0001-01-01T00:00:00Z",
  "template": {
    "id": 1,
    "name": "Example Template",
    "subject": "Click here!",
    "text": "",
    "html": "\u003chtml\u003e\n\u003chead\u003e\n\t\u003ctitle\u003e\u003c/title\u003e\n\u003c/head\u003e\n\u003cbody\u003e\n\u003cp\u003eClick \u003ca href=\"{{.URL}}\"\u003ehere\u003c/a\u003e!\u003c/p\u003e\n{{.Tracker}}\u003c/body\u003e\n\u003c/html\u003e\n",
    "modified_date": "2018-10-08T15:54:56.258392Z",
    "attachments": []
  },
  "page": {
    "id": 1,
    "name": "Example Landing Page",
    "html": "\u003chtml\u003e\u003chead\u003e\n\t\u003ctitle\u003e\u003c/title\u003e\n\u003c/head\u003e\n\u003cbody\u003e\n\u003cp\u003eLanding page HTML\u003c/p\u003e\n\n\n\u003c/body\u003e\u003c/html\u003e",
    "capture_credentials": false,
    "capture_passwords": false,
    "redirect_url": "",
    "modified_date": "2018-10-08T15:55:16.416396Z"
  },
  "status": "In progress",
  "results": [
    {
      "id": "hoqKYFn",
      "status": "Email Sent",
      "ip": "",
      "latitude": 0,
      "longitude": 0,
      "send_date": "2018-10-08T15:56:29.535158Z",
      "reported": false,
      "modified_date": "2018-10-08T15:56:29.535158Z",
      "email": "user@example.com",
      "first_name": "Example",
      "last_name": "User",
      "position": ""
    },
    {
      "id": "VYrDwtG",
      "status": "Clicked Link",
      "ip": "::1",
      "latitude": 0,
      "longitude": 0,
      "send_date": "2018-10-08T15:56:29.548722Z",
      "reported": false,
      "modified_date": "2018-10-08T15:56:46.955281Z",
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
    }
  ],
  "timeline": [
    {
      "email": "",
      "time": "2018-10-08T15:56:29.49172Z",
      "message": "Campaign Created",
      "details": ""
    },
    {
      "email": "user@example.com",
      "time": "2018-10-08T15:56:29.535158Z",
      "message": "Email Sent",
      "details": ""
    },
    {
      "email": "foo@bar.com",
      "time": "2018-10-08T15:56:29.548722Z",
      "message": "Email Sent",
      "details": ""
    },
    {
      "email": "foo@bar.com",
      "time": "2018-10-08T15:56:44.679743Z",
      "message": "Email Opened",
      "details": "{\"payload\":{\"rid\":[\"VYrDwtG\"]},\"browser\":{\"address\":\"::1\",\"user-agent\":\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36\"}}"
    },
    {
      "email": "foo@bar.com",
      "time": "2018-10-08T15:56:46.955281Z",
      "message": "Clicked Link",
      "details": "{\"payload\":{\"rid\":[\"VYrDwtG\"]},\"browser\":{\"address\":\"::1\",\"user-agent\":\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36\"}}"
    }
  ],
  "smtp": {
    "id": 1,
    "interface_type": "SMTP",
    "name": "Example Sending Profile",
    "host": "localhost:1025",
    "from_address": "Test User \u003ctest@test.com\u003e",
    "ignore_cert_errors": true,
    "headers": [],
    "modified_date": "2018-09-04T01:24:21.691924069Z"
  },
  "url": "http://localhost"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Campaign not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если указанная кампания не найдена.

{% api-method method="post" host="https://localhost:3333" path="/api/campaigns/" %}
{% api-method-summary %}
Create Campaign
{% endapi-method-summary %}

{% api-method-description %}
Creates and launches a new campaign.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
The campaign details. See the introduction above for the format of a campaign.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 1,
  "name": "Example Campaign",
  "created_date": "2018-10-08T15:56:29.48815Z",
  "launch_date": "2018-10-08T15:56:00Z",
  "send_by_date": "0001-01-01T00:00:00Z",
  "completed_date": "0001-01-01T00:00:00Z",
  "template": {
    "id": 1,
    "name": "Example Template",
    "subject": "Click here!",
    "text": "",
    "html": "\u003chtml\u003e\n\u003chead\u003e\n\t\u003ctitle\u003e\u003c/title\u003e\n\u003c/head\u003e\n\u003cbody\u003e\n\u003cp\u003eClick \u003ca href=\"{{.URL}}\"\u003ehere\u003c/a\u003e!\u003c/p\u003e\n{{.Tracker}}\u003c/body\u003e\n\u003c/html\u003e\n",
    "modified_date": "2018-10-08T15:54:56.258392Z",
    "attachments": []
  },
  "page": {
    "id": 1,
    "name": "Example Landing Page",
    "html": "\u003chtml\u003e\u003chead\u003e\n\t\u003ctitle\u003e\u003c/title\u003e\n\u003c/head\u003e\n\u003cbody\u003e\n\u003cp\u003eLanding page HTML\u003c/p\u003e\n\n\n\u003c/body\u003e\u003c/html\u003e",
    "capture_credentials": false,
    "capture_passwords": false,
    "redirect_url": "",
    "modified_date": "2018-10-08T15:55:16.416396Z"
  },
  "status": "In progress",
  "results": [
    {
      "id": "hoqKYFn",
      "status": "Email Sent",
      "ip": "",
      "latitude": 0,
      "longitude": 0,
      "send_date": "2018-10-08T15:56:29.535158Z",
      "reported": false,
      "modified_date": "2018-10-08T15:56:29.535158Z",
      "email": "user@example.com",
      "first_name": "Example",
      "last_name": "User",
      "position": ""
    },
    {
      "id": "VYrDwtG",
      "status": "Clicked Link",
      "ip": "::1",
      "latitude": 0,
      "longitude": 0,
      "send_date": "2018-10-08T15:56:29.548722Z",
      "reported": false,
      "modified_date": "2018-10-08T15:56:46.955281Z",
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
    }
  ],
  "timeline": null,
  "smtp": {
    "id": 1,
    "interface_type": "SMTP",
    "name": "Example Sending Profile",
    "host": "localhost:1025",
    "from_address": "Test User \u003ctest@test.com\u003e",
    "ignore_cert_errors": true,
    "headers": [],
    "modified_date": "2018-09-04T01:24:21.691924069Z"
  },
  "url": "http://localhost"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This method expects the campaign to be provided in JSON format. For the various objects in a campaign, such as the template, landing page, or sending profile, you need to provide the `name` attribute. Here's an example of a JSON payload to create a new campaign:

```javascript
{
    "name":"CC Example Campaign",
    "template":{"name":"Example Template"},
    "url":"http://localhost",
    "page":{"name":"Example Landing Page"},
    "smtp":{"name":"Example Sending Profile"},
    "launch_date":"2018-10-08T16:20:00+00:00",
    "send_by_date":null,
    "groups":[{"name":"Example Group"}]
}
```

### Scheduling a Campaign

You can schedule a campaign to launch at a later time. To do this, simply put the desired time you want the campaign to launch in the `launch_date` attribute. Ruphish expects the date to be provided in ISO8601 format.

Without setting a launch date, Ruphish launches the campaign immediately.

### Spreading out Emails

By default, Ruphish sends all the emails in a campaign as quickly as possible. Instead, you may wish to spread emails out over a period of minutes, hours, days, or weeks. This is possible by setting the `send_by_date` to an ISO8601 formatted datetime. It's important to note that this must be after the `launch_date`.

{% api-method method="get" host="https://localhost:3333" path="/api/campaigns/:id/results" %}
{% api-method-summary %}
Get Campaign Results
{% endapi-method-summary %}

{% api-method-description %}
Gets the results for a campaign.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The campaign ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 1,
  "name": "Example Campaign",
  "status": "In progress",
  "results": [
    {
      "id": "hoqKYFn",
      "status": "Email Sent",
      "ip": "",
      "latitude": 0,
      "longitude": 0,
      "send_date": "2018-10-08T15:56:29.535158Z",
      "reported": false,
      "modified_date": "2018-10-08T15:56:29.535158Z",
      "email": "user@example.com",
      "first_name": "Example",
      "last_name": "User",
      "position": ""
    },
    {
      "id": "VYrDwtG",
      "status": "Clicked Link",
      "ip": "::1",
      "latitude": 0,
      "longitude": 0,
      "send_date": "2018-10-08T15:56:29.548722Z",
      "reported": false,
      "modified_date": "2018-10-08T15:56:46.955281Z",
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
    }
  ],
  "timeline": [
    {
      "email": "",
      "time": "2018-10-08T15:56:29.49172Z",
      "message": "Campaign Created",
      "details": ""
    },
    {
      "email": "user@example.com",
      "time": "2018-10-08T15:56:29.535158Z",
      "message": "Email Sent",
      "details": ""
    },
    {
      "email": "foo@bar.com",
      "time": "2018-10-08T15:56:29.548722Z",
      "message": "Email Sent",
      "details": ""
    },
    {
      "email": "foo@bar.com",
      "time": "2018-10-08T15:56:44.679743Z",
      "message": "Email Opened",
      "details": "{\"payload\":{\"rid\":[\"VYrDwtG\"]},\"browser\":{\"address\":\"::1\",\"user-agent\":\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36\"}}"
    },
    {
      "email": "foo@bar.com",
      "time": "2018-10-08T15:56:46.955281Z",
      "message": "Clicked Link",
      "details": "{\"payload\":{\"rid\":[\"VYrDwtG\"]},\"browser\":{\"address\":\"::1\",\"user-agent\":\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36\"}}"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Campaign not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

You may not always want the full campaign details, including the template, landing page, etc. Instead, you may just want to poll the campaign results for updates. This API endpoint only returns information that's relevant to the campaign results.

Returns a 404 error if the specified campaign isn't found.

{% api-method method="get" host="https://localhost:3333" path="/api/campaigns/:id/summary" %}
{% api-method-summary %}
Get Campaign Summary
{% endapi-method-summary %}

{% api-method-description %}
Returns summary information about a campaign.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The campaign ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 1,
  "name": "Example Campaign",
  "status": "In progress",
  "stats": {
    "total": 2,
    "sent": 2,
    "opened": 1,
    "clicked": 1,
    "submitted_data": 0,
    "email_reported": 0,
    "error": 0
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Campaign not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if the specified campaign isn't found.

There may be cases where you aren't interested in the specific results, but rather want high-level statistics, or a "summary", about a campaign.

The response includes a `stats` object which has the following format:

```text
{
  total            : int
  sent             : int
  opened           : int
  clicked          : int
  submitted_data   : int
  email_reported   : int
}
```

{% api-method method="delete" host="https://localhost:3333" path="/api/campaigns/:id" %}
{% api-method-summary %}
Delete Campaign
{% endapi-method-summary %}

{% api-method-description %}
Deletes a campaign by ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The campaign ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Campaign deleted successfully!",
  "success": true,
  "data": null
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Campaign not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if the specified campaign isn't found.

{% api-method method="get" host="https://localhost:3333" path="/api/campaigns/:id/complete" %}
{% api-method-summary %}
Complete Campaign
{% endapi-method-summary %}

{% api-method-description %}
Marks a campaign as complete.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The campaign ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Campaign completed successfully!",
  "success": true,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Get Campaign Summary

> Получить сводку о кампании

```
GET /api/campaigns/{id}/summary/
```

### Описание

Возвращает статистику высокого уровня о кампании.

### Параметры

| Параметр | Расположение | Тип | Описание |
| --------- | ------ | ---- | ----------- |
| api_key | header | string | Ваш действующий API ключ |
| id | url | integer | ID кампании |

### Пример запроса

```
GET /api/campaigns/1/summary/?api_key=12345678901234567890123456789012
```

### Пример успешного ответа

```json
{
  "id": 1,
  "name": "Example Campaign",
  "status": "Завершена",
  "stats": {
    "total": 120,
    "sent": 120,
    "opened": 38,
    "clicked": 16,
    "submitted_data": 10,
    "reported": 0,
    "error": 2
  },
  "timeline": [
    {
      "email": "",
      "time": "2017-03-13T05:59:02.168577Z",
      "message": "Кампания создана",
      "details": ""
    },
    {
      "email": "",
      "time": "2017-03-13T05:59:02.168652Z",
      "message": "Кампания запущена",
      "details": ""
    },
    {
      "email": "",
      "time": "2017-03-13T06:04:02.168652Z",
      "message": "Кампания завершена",
      "details": ""
    }
  ]
}
```

### Пример ответа с ошибкой (Кампания не найдена)

```json
{
  "message": "Кампания не найдена",
  "success": false,
  "data": null
}
```

## Delete Campaign

> Удалить кампанию

```
DELETE /api/campaigns/{id}/
```

### Описание

Удаляет кампанию.

### Параметры

| Параметр | Расположение | Тип | Описание |
| --------- | ------ | ---- | ----------- |
| api_key | header | string | Ваш действующий API ключ |
| id | url | integer | ID удаляемой кампании |

### Пример запроса

```
DELETE /api/campaigns/1/?api_key=12345678901234567890123456789012
```

### Пример успешного ответа

```json
{
  "message": "Кампания успешно удалена",
  "success": true
}
```

### Пример ответа с ошибкой (Кампания не найдена)

```json
{
  "message": "Кампания не найдена",
  "success": false,
  "data": null
}
```

