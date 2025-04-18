# Локализация статусов заказа и доставки в Интернет-магазине: обзор методов

[Статусы заказа и доставки](../status/index.md) можно адаптировать под разные языки.

> Быстрый переход: [все методы](#all-methods)

## Языки локализации

Локализация статусов доступна для языков:
- `ar` — арабский,
- `br` — португальский,
- `de` — немецкий,
- `en` — английский,
- `fr` — французский,
- `hi` — хинди,
- `id` — индонезийский,
- `in` — английский для Индии,
- `it` — итальянский,
- `ja` — японский,
- `la` — испанский,
- `ms` — малайский,
- `pl` — польский,
- `ru` — русский,
- `sc` — китайский упрощенный,
- `tc` — китайский традиционный,
- `th` — тайский,
- `tr` — турецкий,
- `ua` — украинский,
- `vn` — вьетнамский.

Список актуальных языков можно получить методом [sale.statuslang.getlistlangs](./sale-status-lang-get-list-langs.md).

## Связь локализации статусов с другими объектами

**Статус.** Укажите идентификатор нужного статуса. Список идентификаторов можно получить методом [sale.status.list](../status/sale-status-list.md).

## Обзор методов {#all-methods}

> Scope: [`sale`](../../scopes/permissions.md)
>
> Кто может выполнять метод: администратор

#|
|| **Метод** | **Описание** ||
|| [sale.statusLang.getListLangs](./sale-status-lang-get-list-langs.md) | Возвращает список языков для локализации статуса заказа или доставки ||
|| [sale.statusLang.add](./sale-status-lang-add.md) | Добавляет локализацию статуса ||
|| [sale.statusLang.list](./sale-status-lang-list.md) | Возвращает список локализаций статуса ||
|| [sale.statusLang.deleteByFilter](./sale-status-lang-delete-by-filter.md) | Удаляет локализацию статуса ||
|| [sale.statusLang.getFields](./sale-status-lang-get-fields.md) | Возвращает поля локализации статуса ||
|#