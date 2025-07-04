# Изменить сообщение Ленты новостей log.blogpost.update

{% note warning "Мы еще обновляем эту страницу" %}

Тут может не хватать некоторых данных — дополним в ближайшее время

{% endnote %}

{% if build == 'dev' %}

{% note alert "TO-DO _не выгружается на prod_" %}

- не указаны типы параметров
- не указана обязательность параметров
- отсутствуют примеры
- отсутствует ответ в случае успеха
- отсутствует ответ в случае ошибки
  
{% endnote %}

{% endif %}

> Scope: [`log`](../scopes/permissions.md)
>
> Кто может выполнять метод: любой пользователь

Изменяет сообщение Ленты новостей.

## Параметры функции

#|
|| **Параметр** | **Описание** ||
|| **POST_ID** | Идентификатор сообщения Ленты новостей. ||
|| **USER_ID** | Идентификатор автора сообщения. Указать в качестве значения не текущего пользователя может только пользователь с административными правами и только в случае коробочной версии Битрикс24. В облачной версии в качестве значения данного параметра можно указывать только идентификатор [текущего пользователя](../how-to-call-rest-api/authorization.md#понятие-текущего-пользователя). ||
|| **POST_MESSAGE** | Текст сообщения. ||
|| **POST_TITLE** | Заголовок сообщения. ||
|| **DEST** | Список адресатов, которые получат право на просмотр сообщения.  Возможные значения элементов массива:

{% include notitle [адресаты сообщения](./_includes/log-recepients.md) %}

Значение по умолчанию - `['UA']`
||
|| **SPERM** | Список адресатов, которые получат право на просмотр сообщения. (устаревшее). Аналогично `DEST` ||
|| **FILES** | Прикреполенные к сообщению файлы в виде массива значений. Особенности работы с файлами описаны в статье [Как обновить и удалить файлы](../files/how-to-update-files.md). ||
|#

{% include [Сноска о параметрах](../../_includes/required.md) %}
