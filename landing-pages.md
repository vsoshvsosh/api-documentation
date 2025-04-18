# Целевые Страницы

"Целевая страница" — это HTML-содержимое, возвращаемое, когда цели кликают по ссылкам в электронных письмах Ruphish.

Целевые страницы имеют следующую структуру:

```text
{
  id                  : int64
  name                : string
  html                : string
  capture_credentials : bool
  capture_passwords   : bool
  modified_date       : string(datetime)
  redirect_url        : string
}
```

{% api-method method="get" host="https://localhost:3333" path="/api/pages/" %}
{% api-method-summary %}
Получить Целевые Страницы
{% endapi-method-summary %}

{% api-method-description %}
Возвращает список целевых страниц.
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
    "name": "Example Page",
    "html": "<html><head></head><body>This is a test page</body></html>",
    "capture_credentials": true,
    "capture_passwords": true,
    "redirect_url": "http://example.com",
    "modified_date": "2016-11-26T14:04:40.4130048-06:00"
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/pages/:id" %}
{% api-method-summary %}
Получить Целевую Страницу
{% endapi-method-summary %}

{% api-method-description %}
Возвращает целевую страницу по указанному ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID целевой страницы
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
   "name": "Example Page",
   "html": "<html><head></head><body>This is a test page</body></html>",
   "capture_credentials": true,
   "capture_passwords": true,
   "redirect_url": "http://example.com",
   "modified_date": "2016-11-26T14:04:40.4130048-06:00"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Page not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если указанная целевая страница не найдена.

{% api-method method="post" host="https://localhost:3333" path="/api/pages/" %}
{% api-method-summary %}
Создать Целевую Страницу
{% endapi-method-summary %}

{% api-method-description %}
Создает целевую страницу.
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
JSON-представление создаваемой целевой страницы
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
   "name": "Example Page",
   "html": "<html><head></head><body>This is a test page</body></html>",
   "capture_credentials": true,
   "capture_passwords": true,
   "redirect_url": "http://example.com",
   "modified_date": "2016-11-26T14:04:40.4130048-06:00"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Этот метод ожидает, что целевая страница будет предоставлена в формате JSON. Вы должны указать `name` целевой страницы и `html` для целевой страницы.

{% hint style="info" %}
**Импорт Сайта**

Позвольте Ruphish сделать за вас сложную работу, импортировав сайт. Используя конечную точку [Импорт Сайта](landing-pages.md#import-site), вы можете просто дать Ruphish URL, и сайт будет получен для вас и возвращен в формате, который можно использовать с этим методом.
{% endhint %}

#### Захват Учетных Данных

Захват учетных данных — это мощная функция Ruphish. Устанавливая определенные флаги, вы можете захватывать весь пользовательский ввод или только ввод, не являющийся паролем.

Для захвата учетных данных установите атрибут `capture_credentials`. Если вы также хотите захватывать пароли, установите атрибут `capture_passwords`.

По умолчанию Ruphish не будет захватывать пароли, так как они хранятся в виде открытого текста.

Ruphish также предоставляет возможность перенаправлять пользователей на URL после отправки учетных данных. Это контролируется путем установки атрибута `redirect_url`.

{% api-method method="put" host="https://localhost:3333" path="/api/pages/:id" %}
{% api-method-summary %}
Изменить Целевую Страницу
{% endapi-method-summary %}

{% api-method-description %}
Изменяет существующую целевую страницу.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID целевой страницы для изменения
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
JSON-представление изменяемой целевой страницы
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
   "id": 1,
   "name": "Example Page",
   "html": "<html><head></head><body>This is a test page</body></html>",
   "capture_credentials": true,
   "capture_passwords": true,
   "redirect_url": "http://example.com",
   "modified_date": "2016-11-26T14:04:40.4130048-06:00"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Page not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если указанная целевая страница не найдена.

Этот метод ожидает, что целевая страница будет предоставлена в формате JSON. Вы должны предоставить полную целевую страницу, а не только поля, которые вы хотите обновить.

Этот метод возвращает JSON-представление измененной целевой страницы.

{% api-method method="delete" host="https://localhost:3333" path="/api/pages/:id" %}
{% api-method-summary %}
Удалить Целевую Страницу
{% endapi-method-summary %}

{% api-method-description %}
Удаляет целевую страницу.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID целевой страницы для удаления
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
  "message": "Page Deleted Successfully",
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
  "message": "Page not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если указанная целевая страница не найдена.

Этот метод возвращает сообщение о состоянии, указывающее, что целевая страница была успешно удалена.

{% api-method method="post" host="https://localhost:3333" path="/api/import/site" %}
{% api-method-summary %}
Импортировать Сайт
{% endapi-method-summary %}

{% api-method-description %}
Получает URL для последующего импорта в качестве целевой страницы
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="include\_resources" type="boolean" required=false %}
Создавать ли тег `<base>` в результирующем HTML для разрешения статических ссылок (рекомендуется: `false`)
{% endapi-method-parameter %}

{% api-method-parameter name="url" type="string" required=true %}
URL для получения
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "html": "<html><head>..."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Эта конечная точка просто получает и возвращает HTML с предоставленного URL. Если `include_resources` имеет значение `false` (рекомендуется), добавляется тег `<base>`, чтобы относительные ссылки в HTML разрешались из исходного URL.

Кроме того, если HTML содержит элементы формы, эта конечная точка добавляет еще один вход, `__original_url`, который указывает на исходный URL. Это делает возможным воспроизведение захваченных учетных данных позже.

{% hint style="info" %}
**Примечание:** Эта конечная точка API фактически не создает новую целевую страницу. Вместо этого вы можете использовать HTML, возвращенный из этой конечной точки, в качестве входных данных для метода [Создать Целевую Страницу](landing-pages.md#create-landing-page).
{% endhint %}



