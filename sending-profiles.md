# Профили Отправки

"Профиль отправки" - это конфигурация SMTP, которая указывает Gophish, как отправлять электронные письма.

Профили отправки поддерживают аутентификацию и игнорирование недействительных SSL-сертификатов.

Профили отправки имеют следующую структуру:

```text
{
  id                 : int64
  name               : string
  username           : string (необязательно)
  password           : string (необязательно)
  host               : string
  interface_type     : string
  from_address       : string
  ignore_cert_errors : boolean (по умолчанию:false)
  modified_date      : string(datetime)
  headers            : array({key: string, value: string}) (необязательно)
}
```

{% api-method method="get" host="https://localhost" path="/api/smtp/" %}
{% api-method-summary %}
Получить Профили Отправки
{% endapi-method-summary %}

{% api-method-description %}
Получает список профилей отправки, созданных аутентифицированным пользователем.
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
Список профилей отправки, созданных аутентифицированным пользователем.
{% endapi-method-response-example-description %}

```javascript
[
  {
    "id" : 1,
    "name":"Example Profile",
    "interface_type":"SMTP",
    "from_address":"John Doe <john@example.com>",
    "host":"smtp.example.com:25",
    "username":"",
    "password":"",
    "ignore_cert_errors":true,
    "modified_date": "2016-11-20T14:47:51.4131367-06:00",
    "headers": [
      {
        "key": "X-Header",
        "value": "Foo Bar"
      }
    ]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/smtp/:id" %}
{% api-method-summary %}
Получить Профиль Отправки
{% endapi-method-summary %}

{% api-method-description %}
Возвращает профиль отправки по указанному ID, возвращая ошибку 404, если профиль отправки с указанным ID не найден.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID профиля отправки для возврата
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
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true,
  "modified_date": "2016-11-20T14:47:51.4131367-06:00",
  "headers": [
    {
      "key": "X-Header",
      "value": "Foo Bar"
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
  "message": "SMTP not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://localhost:3333" path="/api/smtp" %}
{% api-method-summary %}
Создать Профиль Отправки
{% endapi-method-summary %}

{% api-method-description %}
Создает профиль отправки.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
Тело запроса — это JSON-представление профиля отправки. Обратитесь к введению для ознакомления с действительным форматом профиля отправки.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true,
  "modified_date": "2016-11-20T14:47:51.4131367-06:00",
  "headers": [
    {
      "key": "X-Header",
      "value": "Foo Bar"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Если обязательные поля не предоставлены, или если профиль отправки с указанным именем уже существует, будет возвращена ошибка 400: Bad Request.
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Error message indicating the issue",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Этот метод ожидает, что профиль отправки будет предоставлен в формате JSON. Вы должны указать `name` профиля отправки, `from_address`, с которого отправляются электронные письма, и SMTP-relay `host`.

Профили отправки поддерживают аутентификацию путем установки `username` и `password`.

Кроме того, многие развертывания SMTP-серверов используют самоподписанные сертификаты. Чтобы указать Gophish игнорировать эти недействительные сертификаты, установите поле `ignore_cert_errors` в значение `true`.

Этот метод возвращает JSON-представление созданного профиля отправки.

{% api-method method="put" host="https://localhost:3333" path="/api/smtp/:id" %}
{% api-method-summary %}
Изменить Профиль Отправки
{% endapi-method-summary %}

{% api-method-description %}
Изменяет существующий профиль отправки.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID профиля отправки для изменения
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
Тело запроса — это JSON-представление профиля отправки. Обратитесь к введению для ознакомления с действительным форматом профиля отправки.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true,
  "modified_date": "2016-11-20T14:47:51.4131367-06:00",
  "headers": [
    {
      "key": "X-Header",
      "value": "Foo Bar"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Если профиль отправки с указанным ID не существует, возвращается ошибка 404: Not Found.
{% endapi-method-response-example-description %}

```javascript
{
  "message": "SMTP not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Этот метод ожидает, что профиль отправки будет предоставлен в формате JSON. Вы должны предоставить полный профиль отправки, а не только поля, которые вы хотите обновить.

Этот метод возвращает JSON-представление измененного профиля отправки.

{% api-method method="delete" host="https://localhost:3333" path="/api/smtp/:id" %}
{% api-method-summary %}
Удалить Профиль Отправки
{% endapi-method-summary %}

{% api-method-description %}
Удаляет профиль отправки по ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID профиля отправки для удаления
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
  "message": "SMTP deleted successfully!",
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
  "message": "SMTP not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если указанный профиль отправки не найден.

Этот метод возвращает сообщение о состоянии, указывающее, что профиль отправки был успешно удален.

