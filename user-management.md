# Управление Пользователями

Gophish поддерживает наличие нескольких учетных записей пользователей. Каждая из этих учетных записей отдельная, со своими собственными кампаниями, целевыми страницами, шаблонами и т.д.

Каждой учетной записи пользователя в Gophish назначается **роль**. Это глобальные роли, которые описывают разрешения пользователя в Gophish.

На момент написания существуют две роли:

| Роль | Идентификатор | **Описание** |
| :--- | :--- | :--- |
| Пользователь | `user` | Роль неадминистративного пользователя. Пользователи с этой ролью могут создавать объекты и запускать кампании. |
| Администратор | `admin` | Роль административного пользователя. Пользователи с этой ролью могут управлять общесистемными настройками, а также другими учетными записями пользователей в Gophish. |

Пользователи имеют следующий формат:

```text
{
    id              : int64
    username        : string
    role            : Role
    modified_date   : string(datetime)
}
```

Каждая Роль имеет следующий формат:

```text
{
    name            : string
    slug            : string
    description     : string
}
```

{% api-method method="get" host="https://localhost:3333" path="/api/users/" %}
{% api-method-summary %}
Получить Пользователей
{% endapi-method-summary %}

{% api-method-description %}
Возвращает список всех учетных записей пользователей в Gophish.
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
    "username": "admin",
    "role": {
      "slug": "admin",
      "name": "Admin",
      "description": "System administrator with full permissions"
    }
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/users/:id" %}
{% api-method-summary %}
Получить Пользователя
{% endapi-method-summary %}

{% api-method-description %}
Возвращает пользователя с указанным ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID пользователя
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
[
  {
    "id": 1,
    "username": "admin",
    "role": {
      "slug": "admin",
      "name": "Admin",
      "description": "System administrator with full permissions"
    }
  }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "User not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://localhost:3333" path="/api/users/" %}
{% api-method-summary %}
Создать Пользователя
{% endapi-method-summary %}

{% api-method-description %}
Создает нового пользователя.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="role" type="string" required=true %}
Идентификатор роли для использования в учетной записи
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
Пароль для установки в учетной записи
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=true %}
Имя пользователя для учетной записи
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 2,
  "username": "exampleuser",
  "role": {
    "slug": "user",
    "name": "User",
    "description": "User role with edit access to objects and campaigns"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Если предоставлен недопустимый запрос, будет возвращена ошибка в следующем формате
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Username already taken",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://localhost:3333" path="/api/users/:id" %}
{% api-method-summary %}
Изменить Пользователя
{% endapi-method-summary %}

{% api-method-description %}
Изменяет учетную запись пользователя. Это можно использовать для изменения роли, сброса пароля или изменения имени пользователя.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID пользователя
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="role" type="string" required=false %}
Идентификатор роли для использования в учетной записи
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=false %}
Пароль для установки в учетной записи
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=true %}
Имя пользователя для учетной записи
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 2,
  "username": "exampleuser",
  "role": {
    "slug": "user",
    "name": "User",
    "description": "User role with edit access to objects and campaigns"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Если предоставлен недопустимый запрос, ошибка будет возвращена в следующем формате:
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Username already taken",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "User not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://localhost:3333" path="/api/users/:id" %}
{% api-method-summary %}
Удалить Пользователя
{% endapi-method-summary %}

{% api-method-description %}
Удаляет пользователя, а также каждый объект (целевую страницу, шаблон и т.д.) и кампанию, которые он создал.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID пользователя
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
  "message": "User deleted Successfully!",
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
  "message": "User not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если пользователь с указанным ID не найден.

