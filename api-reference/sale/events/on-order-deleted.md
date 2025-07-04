# При удалении заказа из базы OnOrderDeleted

> Scope: [`sale`](../../scopes/permissions.md) 
>
> Кто может подписаться: любой пользователь

Событие `OnOrderDeleted` вызывается при непосредственном удалении заказа из базы.

## Что получает обработчик

Данные передаются в виде POST-запроса

```
[	
    'event' => 'ONORDERDELETED',
    'event_handler_id' => 1,
    'data' => [
        'FIELDS' => [
            'ID' => 300,
        ],
    ],
    'ts' => 1714649632,
    'auth' => [
        'access_token' => 's6p6eclrvim6da22ft9ch94ekreb52lv',
        'expires_in' => 3600,
        'scope' => 'sale',
        'domain' => 'some-domain.bitrix24.com',
        'server_endpoint' => 'https://oauth.bitrix24.tech/rest/',
        'status' => 'F',
        'client_endpoint' => 'https://some-domain.bitrix24.com/rest/',
        'member_id' => 'a223c6b3710f85df22e9377d6c4f7553',
        'refresh_token' => '4s386p3q0tr8dy89xvmt96234v3dljg8',
        'application_token' => '51856fefc120afa4b628cc82d3935cce',
    ],
]
```

## Параметры

{% include [Сноска об обязательных параметрах](../../../_includes/required.md) %}

#|
|| **Название**
`тип` | **Описание** ||
|| **event***
[`string`](../../data-types.md) | Символьный код события ||
|| **event_handler_id***
[`integer`](../../data-types.md) | Идентификатор обработчика события ||
|| **data***
[`object`](../../data-types.md) | Объект с данными события ||
|| **ts***
[`integer`](../../data-types.md) | timestamp отправки события из очереди событий ||
|| **auth***
[`object`](../../data-types.md) | Объект с параметрами авторизации и данными о портале, на котором произошло событие ||
|#

### Параметр data

{% include [Сноска об обязательных параметрах](../../../_includes/required.md) %}

#|
|| **Название**
`тип` | **Описание** ||
|| **FIELDS***
[`object`](../../data-types.md) | Объект со свойством `ID`, содержащим идентификатор заказа ||
|#

#### Параметр FIELDS

{% include [Сноска об обязательных параметрах](../../../_includes/required.md) %}

#|
|| **Название**
`тип` | **Описание** ||
|| **ID***
[`sale_order.id`](../data-types.md) | Идентификатор заказа. Для получения всех полей заказа по идентификатору используется метод [sale.order.get](../order/sale-order-get.md) ||
|#

### Параметр auth

{% include notitle [Параметр auth](../../../_includes/auth-params-in-events.md) %}