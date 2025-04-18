# Пользователи и Группы

Gophish управляет получателями для кампаний в группах. Каждая группа может содержать одного или нескольких получателей. Группы имеют следующий формат:

```text
{
    id              : int64
    name            : string
    targets         : array(Target)
    modified_date   : string(datetime)
}
```

Каждый получатель в поле `targets` имеет следующий формат:

```text
{
    email           : string
    first_name      : string
    last_name       : string
    position        : string
}
```

{% api-method method="get" host="https://localhost:3333" path="/api/groups/" %}
{% api-method-summary %}
Получить Группы
{% endapi-method-summary %}

{% api-method-description %}
Возвращает список групп.
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
    "name": "Example Group",
    "modified_date": "2018-10-08T15:56:13.790016Z",
    "targets": [
      {
        "email": "user@example.com",
        "first_name": "Example",
        "last_name": "User",
        "position": ""
      },
      {
        "email": "foo@bar.com",
        "first_name": "Foo",
        "last_name": "Bar",
        "position": ""
      }
    ]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/groups/:id" %}
{% api-method-summary %}
Получить Группу
{% endapi-method-summary %}

{% api-method-description %}
Возвращает группу с указанным ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID группы
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
  "name": "Example Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "targets": [
    {
      "email": "user@example.com",
      "first_name": "Example",
      "last_name": "User",
      "position": ""
    },
    {
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
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
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если группа с указанным ID не найдена.

{% api-method method="get" host="https://localhost:3333" path="/api/groups/summary" %}
{% api-method-summary %}
Получить Сводку Групп
{% endapi-method-summary %}

{% api-method-description %}
Возвращает сводку по каждой группе.
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
    "name": "Example Group",
    "modified_date": "2018-10-08T15:56:13.790016Z",
    "num_targets": 2
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/groups/:id/summary" %}
{% api-method-summary %}
Получить Сводку Группы
{% endapi-method-summary %}

{% api-method-description %}
Возвращает сводку для группы.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID группы
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
  "name": "Example Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "num_targets": 2
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возможно, вам нужно только количество участников в группе, а не обязательно полная информация об участниках. Эта конечная точка API возвращает сводку для группы.

Возвращает ошибку 404, если группа с указанным ID не найдена.

{% api-method method="post" host="https://localhost:3333" path="/api/groups/" %}
{% api-method-summary %}
Создать Группу
{% endapi-method-summary %}

{% api-method-description %}
Создает новую группу.
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
Группа для создания в формате JSON.
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
  "name": "Example Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "targets": [
    {
      "email": "user@example.com",
      "first_name": "Example",
      "last_name": "User",
      "position": ""
    },
    {
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Если предоставлен недопустимый запрос, будет возвращено сообщение об ошибке
{% endapi-method-response-example-description %}

```
{
  "message": "Group name not specified",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

При создании новой группы вы должны указать уникальное `name`, а также список `targets`. Вот пример тела запроса:

```javascript
{
    "name": "Example Group",
    "targets": [
    {
        "email": "user@example.com",
        "first_name": "Example",
        "last_name": "User",
        "position": ""
    },
    {
        "email": "foo@bar.com",
        "first_name": "Foo",
        "last_name": "Bar",
        "position": ""
    }
    ]
}
```

{% api-method method="put" host="https://localhost:3333" path="/api/groups/:id" %}
{% api-method-summary %}
Изменить Группу
{% endapi-method-summary %}

{% api-method-description %}
Изменяет группу.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
ID группы
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
Обновленное содержимое группы. Полная группа должна быть предоставлена в формате JSON.
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
  "name": "Example Modified Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "targets": [
    {
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
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
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Эта конечная точка API позволяет изменять существующую группу. Запрос должен включать полный JSON группы, а не только поля, которые вы хотите обновить. Это означает, что вам необходимо включить соответствующее поле `id`. Вот пример запроса:

```javascript
{
    "id": 1,
    "name": "Example Modified Go",
    "targets": [
    {
        "email": "foo@bar.com",
        "first_name": "Foo",
        "last_name": "Bar",
        "position": ""
    }
    ]
}
```

Возвращает ошибку 404, если группа с указанным ID не найдена.

{% api-method method="delete" host="https://localhost:3333" path="/api/groups/:id" %}
{% api-method-summary %}
Удалить Группу
{% endapi-method-summary %}

{% api-method-description %}
Удаляет группу
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="number" required=true %}
ID группы
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
  "message": "Group deleted successfully!",
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
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Возвращает ошибку 404, если группа с указанным ID не найдена.

{% api-method method="post" host="https://localhost:3333" path="/api/import/group" %}
{% api-method-summary %}
Импортировать Группу
{% endapi-method-summary %}

{% api-method-description %}
Читает и анализирует CSV, возвращая данные, которые можно использовать для создания группы.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Действительный ключ API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="file" type="object" required=true %}
Загрузка файла, содержащего содержимое CSV для анализа.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "email": "foobar@example.com",
    "first_name": "Example",
    "last_name": "User",
    "position": "Systems Administrator"
  },
  {
    "email": "johndoe@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "position": "CEO"
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Эта конечная точка API позволяет загрузить CSV, возвращая список целей группы. Например, вы можете использовать следующую команду `curl` для загрузки CSV:

```text
curl -k https://localhost:3333/api/import/group -XPOST \
    -F "file=@group_template.csv" \
    -H "Authorization: Bearer 0123456789abcdef"
```

Результаты этой конечной точки API могут быть использованы в качестве параметра `targets` при вызове конечной точки [Создать Группу](users-and-groups.md#create-group).

