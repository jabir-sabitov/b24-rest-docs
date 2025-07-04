# Типы данных и структура объектов в REST API CRM

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- Сделать ссылки с catalog_product.id и catalog_measure.code на справочник, когда появится

{% endnote %}

{% endif %}

Базовые типы данных перечислены в отдельной [статье](../data-types.md).

В этой статье рассмотрим типы данных и структуру объектов, характерные именно для crm.

## Типы данных

#|
|| **Тип** | **Описания и значения** ||
|| `crm_status` | Строковый идентификатор элемента справочника CRM (например, `NEW`). Получить возможные значения конкретного справочника можно с помощью метода [crm.status.list](./status/crm-status-list.md) с фильтром по `ENTITY_ID`. ||
|| `crm_lead` | Целочисленный идентификатор лида CRM. Получить информацию о лиде можно с помощью метода [crm.lead.get](./leads/crm-lead-get.md). ||
|| `crm_deal` | Целочисленный идентификатор сделки CRM. Получить информацию о сделке можно с помощью метода [crm.deal.get](./deals/crm-deal-get.md). ||
|| `crm_contact` | Целочисленный идентификатор контакта CRM. Получить информацию о контакте можно с помощью метода [crm.contact.get](./contacts/crm-contact-get.md). ||
|| `crm_company` | Целочисленный идентификатор компании CRM. Получить информацию о компании можно с помощью метода [crm.company.get](./companies/crm-company-get.md). ||
|| `crm_quote` | Целочисленный идентификатор коммерческого предложения CRM. Получить информацию о коммерческом предложении можно с помощью метода [crm.quote.get](./quote/crm-quote-get.md). ||
|| `crm_category` | Целочисленный идентификатор воронки (направления) CRM. Получить информацию о воронке (направлении) можно с помощью метода [crm.category.get](./universal/category/crm-category-get.md) ||
|| `crm_entity`| Целочисленный идентификатор элемента некоторого объекта CRM. Поля с таким типом явно содержат в себе информацию к какому объекту CRM они принадлежат. Например, поля вида `parentId{entityTypeId}`, содержат внутри своего названия идентификатор типа сущности CRM. Получить информацию об элементе можно с помощью метода [`crm.item.get`](universal/crm-item-get.md) передав `entityTypeId` из названия поля и `id` из его значения ||
|| `lang_map`  | Объект формата:
```
{
    lang_1: value_1,
    lang_2: value_2,
    ..
    lang_n: value_n,
}
```

где
`lang_n` - [Идентификатор языка](#lang-ids)
`value_n` - Значение для языка `lang_n`
||
|| [`crm_item_product_row`](#crm_item_product_row) | Целочисленный идентификатор товарной позиции объекта CRM. Получить идентификаторы товарных позиций можно с помощью метода [crm.item.productrow.list](../crm/universal/product-rows/crm-item-productrow-list.md) ||
|| [`crm_multifield`](#crm_multifield) | Объект, описывающий «множественное поле». Множественные поля применяются для хранения телефонов, email-адресов и другой контактной информации. В лидах, контактах и компаниях полями этого типа являются `PHONE`, `EMAIL`, `WEB` и `IM`. ||
|| [`crm_currency`](#crm_currency) | Объект, описывающий валюту ||
|| [`crm_currency_localization`](#crm_currency_localization) | Объект, описывающий локализацию валюты ||
|| [`crm_orderentity`](#crm_orderentity) | Объект, описывающий связь CRM с заказами интернет-магазина ||
|| [`type`](#type) | Объект, описывающий пользовательский тип объекта CRM (смарт-процесс) ||
|| [`type.relations`](#typerelations) | Объект, содержащий в себе связи к другим сущностям CRM ||
|| [`relation`](#relation) | Объект, описывающий привязанный элемент CRM  ||
|| [`type.linkedUserFields`](#typelinkeduserfields) | Объект, описывающий набор полей, в которых должен отображаться смарт-процесс ||
|#


## Структура объектов

### crm_multifield

#|
|| **Значение**
`тип` | **Описание** ||
|| **ID**
[`integer`](../data-types.md) | Идентификатор значения множественного поля ||
|| **TYPE_ID**
[`string`](../data-types.md) | Тип множественного поля. Может принимать значения  `PHONE`, `EMAIL`, `WEB`, `IM`, `LINK` ||
|| **VALUE**
[`string`](../data-types.md) | Строковое значение множественного поля ||
|| **VALUE_TYPE**
[`string`](../data-types.md) | Тип значения множественного поля.
Может принимать значения  `WORK`, `MOBILE`, `FAX`, `HOME`, `PAGER`, `MAILING`, `OTHER` для телефона,
`WORK`, `HOME`, `MAILING`, `OTHER` для почты,
`WORK`, `HOME`, `FACEBOOK`, `VK`, `LIVEJOURNAL`, `TWITTER`, `OTHER` для сайта,
`FACEBOOK`, `TELEGRAM`, `VK`, `SKYPE`, `VIBER`, `INSTAGRAM`, `BITRIX24`, `OPENLINE`, `IMOL`, `ICQ`, `MSN`, `JABBER`, `OTHER` для мессенджера
||
|#

### crm_item_product_row

#|
|| **Значение**
`тип` | **Описание** ||
|| **id**
[`integer`](../data-types.md) | Идентификатор товарной позиции ||
|| **ownerId**
[`integer`](../data-types.md) | Идентификатор объекта CRM ||
|| **ownerType**
[`string`](../data-types.md) | Идентификатор [`типа объекта CRM`](#tip-obuekta-crm) ||
|| **productId**
`catalog_product.id` | Идентификатор товара из каталога ||
|| **productName**
[`string`](../data-types.md) | Название товара в товарной позиции ||
|| **price**
[`double`](../data-types.md) | Цена за единицу товарной позиции с учетом скидок и налогов ||
|| **priceAccount**
[`double`](../data-types.md) | Стоимость за единицу товарной позиции с учетом скидок и налогов, сконвертированная в валюту отчетов ||
|| **priceExclusive**
[`double`](../data-types.md) | Стоимость за единицу товарной позиции с учетом скидок, но без учета налогов ||
|| **priceNetto**
[`double`](../data-types.md) | Стоимость за единицу товарной позиции без учета скидок и без учета налогов ||
|| **priceBrutto**
[`double`](../data-types.md) | Стоимость за единицу товарной позиции с учетом налогов, но без учета скидок ||
|| **quantity**
[`double`](../data-types.md) | Количество товара ||
|| **discountTypeId**
[`integer`](../data-types.md) | Тип скидки
Возможные значения:
- `1` — абсолютное значение
- `2` — процентное значение ||
|| **discountRate**
[`double`](../data-types.md) | Значение скидки в процентах ||
|| **discountSum**
[`double`](../data-types.md) | Абсолютное значение скидки ||
|| **taxRate**
[`double`](../data-types.md) | Ставка налога в процентах ||
|| **taxIncluded**
[`string`](../data-types.md) | Индикатор того, включен ли налог в стоимость
Возможные значения:
- `Y` – налог включен
- `N` – налог не включен ||
|| **customized**
[`string`](../data-types.md) | Устаревшее ||
|| **measureCode**
`catalog_measure.code` | Код единицы измерения ||
|| **measureName**
[`string`](../data-types.md) | Текстовое представление единицы измерения (например - шт, кг, м, л и т.д.) ||
|| **sort**
[`integer`](../data-types.md) | Сортировка ||
|| **xmlId**
[`string`](../data-types.md) | Внешний идентификатор товарной позиции ||
|| **type**
[`integer`](../data-types.md) | Тип товара
Возможные значения:
- `1` - Простой товар
- `2` - Комплект
- `3` - Товар с торговыми предложениями
- `4` - Торговое предложение
- `5` - Торговое предложение, у которого нет товара (не указан или удален)
- `6` - Специфический тип, означает невалидный товар с торговыми предложениями
- `7` — Услуга ||
|| **storeId**
[`integer`](../data-types.md) | Идентификатор склада ||
|#

### crm_currency

#|
|| **Значение**
`тип` | **Описание** ||
|| **AMOUNT**
[`double`](../data-types.md) | Курс обмена по отношению к базовой валюте
Для базовой валюты всегда равен `1`. Точность — 4 знака после запятой
 ||
|| **AMOUNT_CNT**
[`integer`](../data-types.md) | Номинал.
Для базовой валюты всегда равен `1`
 ||
|| **BASE**
[`string`](../data-types.md) | Признак, является ли валюта базовой (`Y`/`N`) ||
|| **CURRENCY**
[`string`](../data-types.md) | Идентификатор валюты. Соответствует стандарту ISO 4217 ||
|| **DATE_UPDATE**
[`datetime`](../data-types.md) | Дата последнего изменения ||
|| **SORT**
[`integer`](../data-types.md) | Сортировка ||
|| **LID**
[`string`](../data-types.md) | Код языка, для которого возвращаются [параметры локализации](#crm_currency_localization) ||
|| **DECIMALS**
[`integer`](../data-types.md) | Число десятичных знаков дробной части (параметр локализации) ||
|| **DEC_POINT**
[`string`](../data-types.md) | Десятичная точка при выводе (параметр локализации) ||
|| **FORMAT_STRING**
[`string`](../data-types.md) | Шаблон формата (параметр локализации) ||
|| **FULL_NAME**
[`string`](../data-types.md) | Название валюты (параметр локализации) ||
|| **THOUSANDS_SEP**
[`string`](../data-types.md) | Разделитель триад (параметр локализации) ||
|| **LANG**
[`object`](../data-types.md) | Локализации валюты.
Объект со списком доступных локализаций в формате `{"lang_1": "value_1", ... "lang_N": "value_N"}`, где `lang_N` — идентификатор языка, а `value` — объект типа [crm_currency_localization](#crm_currency_localization).
Идентификатор языка — строка из двух латинских букв. Возможные значения смотрите в [таблице идентификаторов языков](#lang-ids)
 ||
|#

### crm_currency_localization

#|
|| **Значение**
`тип` | **Описание** ||
|| **DECIMALS**
[`integer`](../data-types.md) | Число десятичных знаков дробной части.

Значение по умолчанию — `2` ||
|| **DEC_POINT**
[`string`](../data-types.md) | Десятичная точка при выводе.

Значение по умолчанию — `.` (символ точки) ||
|| **FORMAT_STRING**
[`string`](../data-types.md) | Шаблон формата. Должен содержать символ # — вместо него будет подставлено значение цены.

Значение по умолчанию — `#`.

Примеры шаблонов для суммы 1000:
- `$ #` — $ 1000
- `# руб.` — 1000 руб.
- `€ #` — € 1000
  ||
|| **FULL_NAME**
[`string`](../data-types.md) | Название валюты.

Значение по умолчанию — [`crm_currency.CURRENCY`](#crm_currency)  ||
|| **HIDE_ZERO**
[`string`](../data-types.md) | Признак, скрывать незначащие нули или нет (`Y`/`N`).

Значение по умолчанию — `N` ||
|| **THOUSANDS_SEP**
[`string`](../data-types.md) | Разделитель триад.

Значение по умолчанию — ` ` (пробел) ||
|| **THOUSANDS_VARIANT**
[`string`](../data-types.md) | Код разделителя триад.

Значение по умолчанию — `S`.

При создании или изменении локализации, если указано значение для поля `THOUSANDS_VARIANT`, то значение в `THOUSANDS_SEP` будет проигнорировано и заменено согласно списку:
- `N` — пусто, разделитель триад отсутствует. Пример: 12345678
- `C` — запятая. Пример: 12,345,678
- `D` — точка. Пример: 12.345.678
- `S` — пробел. Пример: 12 345 678
- `B` — неразрывный пробел. Пример: 12 345 678
    От предыдущего варианта отличается тем, что при переносе строк результат не разбивается на части

Если разделитель триад не нужен, необходимо явно передавать поле `THOUSANDS_VARIANT` со значением `N`. Пустая строка в поле `THOUSANDS_SEP` не допускается.
 ||
|#

### crm_orderentity

#|
|| **Значение**
`тип` | **Описание** ||
|| **OWNER_ID**
[`integer`](../data-types.md) | Идентификатор объекта CRM ||
|| **OWNER_TYPE_ID**
[`integer`](../data-types.md) | Идентификатор [типа объекта CRM](#object_type)
||
|| **ORDER_ID**
[`sale_order.id`](../sale/data-types.md#sale_order) | Идентификатор заказа ||
|#

### type

#|
|| **Значение**
`тип` | **Описание** ||
|| **id**
[`integer`](../data-types.md)  | Идентификатор смарт-процесса ||
|| **title**
[`string`](../data-types.md) | Название смарт-процесса ||
|| **code** 
[`string`](../data-types.md) | Символьный код ||
|| **createdBy**
[`integer`](../data-types.md)  | Идентификатор пользователя, который создал данный смарт-процесс ||
|| **entityTypeId**
[`integer`](../data-types.md)  | Идентификатор типа сущности ||
|| **isCategoriesEnabled**
[`boolean`](../data-types.md)  | Включены ли свои воронки и туннели продаж ||
|| **isStagesEnabled**    
[`boolean`](../data-types.md)  | Включено ли использование своих стадий и канбана ||
|| **isBeginCloseDatesEnabled**
[`boolean`](../data-types.md)  | Включены ли поля **Дата начала** и **Дата завершения** ||
|| **isClientEnabled**    
[`boolean`](../data-types.md)  | Включено ли поле **Клиент** ||
|| **isUseInUserfieldEnabled** 
[`boolean`](../data-types.md)  | Включено ли использование смарт-процесса в пользовательском поле ||
|| **isLinkWithProductsEnabled**
[`boolean`](../data-types.md)  | Включена ли привязка товаров каталога ||
|| **isMycompanyEnabled** 
[`boolean`](../data-types.md)  | Включено ли поле **Реквизиты вашей компании** ||
|| **isDocumentsEnabled** 
[`boolean`](../data-types.md)  | Включена ли печать документов ||
|| **isSourceEnabled**    
[`boolean`](../data-types.md)  | Включены ли поля **Источник** и **Дополнительно об источнике** ||
|| **isObserversEnabled** 
[`boolean`](../data-types.md)  | Включено ли поле **Наблюдатели** ||
|| **isRecyclebinEnabled**
[`boolean`](../data-types.md)  | Включено ли использование корзины ||
|| **isAutomationEnabled**
[`boolean`](../data-types.md)  | Включены ли роботы и триггеры ||
|| **isBizProcEnabled**   
[`boolean`](../data-types.md)  | Включено ли использование дизайнера бизнес процессов ||
|| **isSetOpenPermissions**    
[`boolean`](../data-types.md)  | Делать ли новые воронки доступными для всех ||
|| **isPaymentsEnabled**  
[`boolean`](../data-types.md)  | Системное поле, которое показывает, включена ли возможность оплаты ||
|| **isCountersEnabled**  
[`boolean`](../data-types.md)  | Системное поле, которое показывает, включена ли счётчики ||
|| **createdTime** 
[`datetime`](../data-types.md) | Системное поле, указывающее время создания смарт-процесса ||
|| **updatedTime** 
[`datetime`](../data-types.md) | Системное поле, указывающее на время изменения данного смарт-процесса ||
|| **updatedBy**
[`integer`](../data-types.md)  | Идентификатор пользователя, изменившего данный смарт-процесс ||
|| **relations**
[`object`](../data-types.md)   | Объект, содержащий в себе связи к другим сущностям CRM ||
|| **linkedUserFields**   
[`object`](../data-types.md)   | Набор полей в которых должен отображаться данный смарт-процесс ||
|| **customSections**
[`array`](../data-types.md)    | Список всех цифровых рабочих мест

Параметр устарел. Для работы с цифровыми рабочими местами используйте методы [`crm.automatedsolution.*`](./automated-solution/index.md) ||
|| **customSectionId**
[`integer`](../data-types.md)  | Идентификатор цифрового рабочего места

Параметр устарел. Для работы с цифровыми рабочими местами используйте методы [`crm.automatedsolution.*`](./automated-solution/index.md) ||
|#

### type.relations

#|
|| **Значение**
`тип` | **Описание** ||
|| **parent** 
`relation[]`  | Элементы CRM, которые будут привязаны к данному смарт-процессу ||
|| **child**  
`relation[]`  | Элементы CRM, к котором будет привязан данный смарт-процесс    ||
|#

#### relation

#|
|| **Значение**
`тип` | **Описание** ||
|| **entityTypeId**     
[`integer`](../data-types.md)  | Идентификатор [системного](./universal/index.md) или [пользовательского типа](./universal/user-defined-object-types/index.md) сущности CRM ||
|| **isChildrenListEnabled**
[`boolean`](../data-types.md)  | Добавлять ли связанный элемент в карточку ||
|| **isPredefined**        
[`boolean`](../data-types.md)  | Является ли данная связь предустановленной (системной) ||
|#

### type.linkedUserFields

#|
|| **Значение**
`тип` | **Описание** ||
|| **CALENDAR_EVENT\|UF_CRM_CAL_EVENT**
[`boolean`](../data-types.md) | Событие в календаре ||
|| **TASKS_TASK\|UF_CRM_TASK**
[`boolean`](../data-types.md) | Задачи ||
|| **TASKS_TASK_TEMPLATE\|UF_CRM_TASK**
[`boolean`](../data-types.md) | Шаблоны задач ||
|#

## Идентификаторы языков для Битрикс24 {#lang-ids}

#|
|| **Идентификатор языка** | **Язык** ||
|| `ar` | Арабский ||
|| `br` | Португальский (Бразилия) ||
|| `de` | Немецкий ||
|| `en` | Английский ||
|| `fr` | Французский ||
|| `hi` | Хинди ||
|| `id` | Индонезийский ||
|| `it` | Итальянский ||
|| `ja` | Японский ||
|| `la` | Испанский ||
|| `ms` | Малайский ||
|| `pl` | Польский ||
|| `ru` | Русский ||
|| `sc` | Китайский ||
|| `tc` | Китайский (Тайвань) ||
|| `th` | Тайский ||
|| `tr` | Турецкий ||
|| `ua` | Украинский ||
|| `vn` | Вьетнамский ||
|#

## Объекты, используемые в ответах

### Описание отдельно взятого поля crm_rest_field_description {#crm_rest_field_description}

#|
|| **Название** 
`тип` | **Описание** ||
|| **type**
[`string`](../data-types.md)  | Тип поля ||
|| **isRequired**
[`boolean`](../data-types.md) | Является ли поле обязательным ||
|| **isReadOnly**
[`boolean`](../data-types.md) | Является ли поле неизменяемым ||
|| **isImmutable**
[`boolean`](../data-types.md) | Признак возможности однократного заполнения значения поля только при создании нового элемента ||
|| **isMultiple**
[`boolean`](../data-types.md) | Признак множественности поля. При true значения в поле передаются в виде массива ||
|| **isDynamic**
[`boolean`](../data-types.md) | Является ли поле пользовательским ||
|| **title**
[`string`](../data-types.md)  | Название поля ||
|| **upperName**
[`string`](../data-types.md)  | Название поля в верхнем регистре |
|#

### Описание пользовательского поля типа адресс {#crm_user_field_address}

Пользовательское поле типа «Адрес» хранит данные одной строкой. В таблице приведено описание составных частей этой строки.
Подробное описание составляющих частей адреса можно найти в статье [Об адресах](./requisites/addresses/index.md).

#|
|| **Название** 
`тип` | **Описание** | **Пример** ||
|| **ADDRESS_1**
[`string`](../data-types.md)  | Улица, номер дома | Малый Знаменский переулок 7/10 с2 ||
|| **ADDRESS_2**
[`string`](../data-types.md) | Квартира, офис, комната, этаж | 5 ||
|| **POSTAL_CODE**
[`string`](../data-types.md) | Почтовый индекс | 119019 ||
|| **CITY**
[`string`](../data-types.md) | Населенный пункт | Москва ||
|| **REGION**
[`string`](../data-types.md) | Район | район Арбат ||
|| **PROVINCE**
[`string`](../data-types.md) | Регион | Москва ||
|| **COUNTRY**
[`string`](../data-types.md) | Страна | Россия ||
|| **LATITUDE**
[`string`](../data-types.md)  | Координаты широты | 55.748289 ||
|| **LONGITUDE**
[`string`](../data-types.md)  | Координаты долготы | 37.60504 ||
|| **LOC_ADDR_ID**
[`string`](../data-types.md)  | Идентификатор адреса местоположения | 10 ||
|#

## Тип объекта CRM {#object_type}

#|
|| **Тип объекта** | **Числовой идентификатор типа**
`entityTypeId` | **Символьный код типа**
`entityTypeName` | **Краткий символьный код типа**
`entityTypeAbbr` | **Тип объекта пользовательского поля**
`userFieldEntityId` ||
|| Лид | 1 | LEAD | L | CRM_LEAD ||
|| Сделка | 2 | DEAL | D | CRM_DEAL ||
|| Контакт | 3 | CONTACT | C | CRM_CONTACT ||
|| Компания | 4 | COMPANY | CO| CRM_COMPANY ||
|| Счет (старый) | 5 | INVOICE | I | CRM_INVOICE ||
|| Счет (новый) | 31 | SMART_INVOICE | SI | CRM_SMART_INVOICE ||
|| Предложение | 7 | QUOTE | Q | CRM_QUOTE ||
|| Реквизит | 8 | REQUISITE | RQ | CRM_REQUISITE ||
|| Заказ | 14 | ORDER | O | ORDER ||
|| Смарт-процесс | 128 | DYNAMIC_128 | T80 | CRM_1 ||
|#

> В таблице приведено описание смарт-процесса с идентификатором типа 128 и идентификатором 1.
>
> Идентификаторы типа смарт-процессов находятся в промежутке от 128 до 191 (включительно), либо имеют значение больше чем 1030 (включительно) и являются четными.
>
> Идентификаторы типа смарт-процессов, удаленных в корзину, находятся в промежутке от 192 до 255 (включительно), либо имеют значение больше чем 1030 и являются нечетными.
>
> Чтобы определить префикс смарт-процесса, необходимо:
> - сконвертировать идентификатор из десятичной системы в шестнадцатеричную. В случае с идентификатором равным 128, получаем значение 80.
> - взять полученное значение в нижнем регистре и к полученному значению дописать латинскую букву T в начале. Таким образом, получаем префикс — T80.
