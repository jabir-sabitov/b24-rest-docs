# Перезагрузить страницу BX24.reloadWindow

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- отсутствуют примеры
- отсутствует ответ в случае успеха
- отсутствует ответ в случае ошибки

{% endnote %}

{% endif %}

```js
void BX24.reloadWindow()
```

Метод `BX24.reloadWindow` перезагружает страницу с приложением, работает только при открытии приложения в отдельном окне. При открытии приложения в слайдере и во встройках метод не работает. 