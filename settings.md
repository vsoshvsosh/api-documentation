---
description: Эти конечные точки позволяют изменять различные настройки Ruphish.
---

# Настройки

{% api-method method="post" host="https://localhost:3333" path="/api/reset" %}
{% api-method-summary %}
Сброс ключа API
{% endapi-method-summary %}

{% api-method-description %}
Эта конечная точка позволяет сбросить ваш ключ API на новый, случайно сгенерированный ключ.  
  
Этот метод требует аутентификации с использованием вашего существующего ключа API.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Существующий ключ API.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Ключ API успешно сброшен. Новый ключ API предоставляется в параметре ответа `data`.
{% endapi-method-response-example-description %}

```javascript
{
    "success": true,
    "message": "API Key successfully reset!",
    "data": "0123456789abcdef"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



