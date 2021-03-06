---
editable: false
---

# MMAX

_Оконные функции_

#### Синтаксис {#syntax}


```
MMAX( value, rows_1 [ , rows_2 ] [ TOTAL | WITHIN [ dim1, ... ] | AMONG [ dim1, ... ] ] )
```

#### Описание {#description}
Возвращает скользящий максимум значений по окну записей. Значение определяется порядком сортировки и аргументами:

| `rows_1`      | `rows_2`   | Окно                                                             |
|:--------------|:-----------|:-----------------------------------------------------------------|
| положительное | -          | Текущая запись и `rows_1` предшествующих.                        |
| отрицательное | -          | Текущая запись и -`rows_1` последующих.                          |
| любой знак    | любой знак | `rows_1` предшествующих записей, текущая и `rows_1` последующих. |



Аналогичное поведение у оконных функций [MCOUNT](MCOUNT.md), [MCOUNT](MCOUNT.md), [MMIN](MMIN.md), [MAVG](MAVG.md).

См. также [MAX](MAX.md), [RMAX](RMAX.md).

**Типы аргументов:**
- `value` — `Логический | Дата | Дата и время | Число | Строка | UUID`
- `rows_1` — `Целое число`
- `rows_2` — `Целое число`


**Возвращаемый тип**: Совпадает с типом аргументов (`value`)

{% note info %}

Значения аргументов (`rows_1`, `rows_2`) должны быть константами.

{% endnote %}

{% note warning %}

Функция зависит от порядка сортировки в чарте. Она будет правильно работать только если:
- в чарте явно задана сортировка;
- в сортировке участвуют __все__ поля, не содержащие оконных функций.

{% endnote %}


#### Примеры {#examples}

```
MMAX([Profit], -2)
```

```
MMAX([Profit], 3)
```

```
MMAX([Profit] 5, 5 TOTAL)
```

```
MMAX([Profit], -5 WITHIN [Date])
```

```
MMAX([Profit], -5 AMONG [Date])
```


#### Поддержка источников данных {#data-source-support}

`Материализованный датасет`, `ClickHouse 1.1`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `PostgreSQL 9.3`.
