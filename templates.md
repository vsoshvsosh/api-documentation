# Шаблоны

"Шаблон" — это содержимое электронных писем, которые отправляются целевым получателям. Они могут быть импортированы из существующего электронного письма или созданы с нуля.

Кроме того, шаблоны могут содержать отслеживающие изображения, чтобы Gophish знал, когда пользователь открывает электронное письмо.

Шаблоны имеют следующую структуру:

```text
{
  id            : int64
  name          : string
  subject       : string
  text          : string
  html          : string
  modified_date : string(datetime)
  attachments   : list(attachment)
}
```

Шаблоны поддерживают отправку вложений. Вложения имеют следующую структуру:

```text
  content: string
  type   : string
  name   : string
```

> Примечание: Ожидается, что поле `content` во вложении будет закодировано в base64.

{% api-method method="get" host="https://localhost:3333" path="/api/templates" %}
{% api-method-summary %}
Получить шаблоны
{% endapi-method-summary %}

{% api-method-description %}
Возвращает список шаблонов.
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
    "id" : 1,
    "name" : "Password Reset Template",
    "subject" : "{{.FirstName}}, please reset your password.",
    "text" : "Please reset your password here: {{.URL}}",
    "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
    "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
    "attachments" : [],
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/templates/:id" %}
{% api-method-summary %}
Получить шаблон
{% endapi-method-summary %}

{% api-method-description %}
Возвращает шаблон с указанным ID.  
  
Возвращает ошибку 404: Not Found, если указанный шаблон не существует.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID шаблона
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
    "name" : "Password Reset Template",
    "subject" : "{{.FirstName}}, please reset your password.",
    "text" : "Please reset your password here: {{.URL}}",
    "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
    "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
    "attachments" : [],
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Template not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://localhost:3333" path="/api/templates/" %}
{% api-method-summary %}
Создать шаблон
{% endapi-method-summary %}

{% api-method-description %}
Создает новый шаблон из предоставленного тела запроса JSON.
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
Тело запроса должно быть JSON-представлением шаблона. См. схему в верхней части этой страницы для формата шаблона.
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
    "name" : "Password Reset Template",
    "subject" : "{{.FirstName}}, please reset your password.",
    "text" : "Please reset your password here: {{.URL}}",
    "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
    "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
    "attachments" : [],
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Должно быть указано хотя бы одно текстовое или HTML-поле, иначе будет возвращена ошибка 400: Bad Request
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Need to specify at least plaintext or HTML content",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Этот метод ожидает, что шаблон будет предоставлен в формате JSON. Вы должны указать `name` шаблона и `text` и/или `html` для шаблона.

{% hint style="info" %}
**Импорт существующего электронного письма** 

Какой лучший способ создать идеальные электронные письма, чем импортировать существующее электронное письмо, которое уже есть в вашем почтовом ящике?

Используя конечную точку [Импорт электронного письма](templates.md#import-template), вы можете взять необработанное электронное письмо и разобрать его как действительный шаблон Gophish.
{% endhint %}

Чтобы добавить отслеживание, убедитесь, что вы указали `{{.Tracker}}` в поле `html`. Пользовательский интерфейс добавляет его автоматически, но его необходимо указать, если вы используете API.

Этот метод возвращает JSON-представление созданного шаблона.

{% api-method method="put" host="https://localhost:3333" path="/api/templates/:id" %}
{% api-method-summary %}
Изменить шаблон
{% endapi-method-summary %}

{% api-method-description %}
Изменяет существующий шаблон.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID шаблона для изменения
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
JSON-представление шаблона, который вы хотите изменить. Необходимо предоставить весь шаблон, а не только поля, которые вы хотите обновить.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Этот метод ожидает, что шаблон будет предоставлен в формате JSON. Вы должны предоставить полный шаблон, а не только поля, которые вы хотите обновить.

Этот метод возвращает JSON-представление измененного шаблона.

{% api-method method="delete" host="https://localhost:3333" path="/api/templates/:id" %}
{% api-method-summary %}
Удалить шаблон
{% endapi-method-summary %}

{% api-method-description %}
Удаляет шаблон по ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Template deleted successfully!",
  "success": true,
  "data": null
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Если не найден шаблон с указанным ID, возвращается ошибка 404: Not Found
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Template not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если указанный шаблон не найден.

Этот метод возвращает сообщение о состоянии, указывающее, что шаблон был успешно удален.

{% api-method method="post" host="https://localhost:3333" path="/api/import/email" %}
{% api-method-summary %}
Импортировать шаблон
{% endapi-method-summary %}

{% api-method-description %}
Импортирует электронное письмо как шаблон.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="convert\_links" type="boolean" required=true %}
Следует ли автоматически преобразовывать ссылки внутри электронного письма в {{.URL}}.
{% endapi-method-parameter %}

{% api-method-parameter name="content" type="string" required=true %}
Исходное содержимое электронного письма в формате RFC 2045, включая исходные заголовки.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "text": "Email text",
  "html": "Email HTML",
  "subject": "Email subject"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Gophish предоставляет возможность парсить существующее электронное письмо для использования в качестве шаблона. Это облегчает перепрофилирование легитимных электронных писем для ваших фишинговых оценок.

Эта конечная точка ожидает необработанное содержимое электронного письма в [формате RFC 2045](https://www.ietf.org/rfc/rfc2045.txt), включая исходные заголовки. Обычно это находится с помощью функции "Показать исходный текст" в почтовых клиентах.

Тело запроса для этой конечной точки представляет собой JSON-запрос в форме:

```javascript
{
    content:       string
    convert_links: boolean
}
```

При установке атрибута `convert_links` в значение `true`, Gophish автоматически изменит все ссылки в электронном письме на `{{.URL}}`.

{% hint style="info" %}
**Примечание:** Этот метод не импортирует полностью электронное письмо как шаблон. Вместо этого он анализирует электронное письмо, возвращая ответ, который может быть использован с конечной точкой "[Создать шаблон](templates.md#create-template)".
{% endhint %}

