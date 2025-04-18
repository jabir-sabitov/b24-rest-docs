# Офисные сети: обзор методов

Офисная сеть — это группа IP-адресов, используемых в локальной сети организации. Работа с диапазонами IP-адресов офисной сети выполняется методами группы timeman.networkrange.*.

> Быстрый переход: [все методы и события](#all-methods)

## Получить диапазон

Узнать текущие настройки диапазонов IP-адресов можно методом [timeman.networkrange.get](./timeman-networkrange-get.md). Метод возвращает список всех установленных диапазонов.

## Настроить диапазон

Метод [timeman.networkrange.set](./timeman-networkrange-set.md) создает или обновляет диапазоны. В качестве диапазона можно указать:
-  одиночный IP-адрес. Например, `10.10.0.1`
-  блок адресов в формате `начальный_адрес-конечный_адрес`. Например, `10.0.0.0-10.255.255.255`

## Проверить IP-адрес

Метод [timeman.networkrange.check](./timeman-networkrange-check.md) проверяет, относится ли указанный IP-адрес к диапазонам офисной сети. Если адрес не указан, система проверит текущий IP.

[Отчет о выявленных отсутствиях](../timecontrol/timeman-timecontrol-reports-get.md) содержит IP-адреса начала и окончания дня сотрудника. С помощью метода [timeman.networkrange.check](./timeman-networkrange-check.md) можно проверить, находился ли человек в эти моменты в офисной сети.

## Обзор методов {#all-methods}

> Scope: [`timeman`](../../scopes/permissions.md)
>
> Кто может выполнять метод: администратор

#|
|| **Метод** | **Описание** ||
|| [timeman.networkrange.get](./timeman-networkrange-get.md) | Получает диапазоны сетевых адресов, входящие в офисную сеть ||
|| [timeman.networkrange.set](./timeman-networkrange-set.md) | Устанавливает диапазоны сетевых адресов, входящие в офисную сеть ||
|| [timeman.networkrange.check](./timeman-networkrange-check.md) | Проверяет входит ли IP-адрес в диапазоны сетевых адресов офисной сети ||
|#
