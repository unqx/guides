# Правила написания кода на Python в Bestdoctor

## Мотивация

Мы разрабатываем здоровенный продукт с кучей функциональности.
Более того, нам потом этот код ещё поддерживать и развивать.

Для этого код должен быть гибким, слабо связанным, соблюдать принципы
DRY, KISS и ещё много чего должен. Иначе в долгосрочной перспективе
 вся лажа вылезет наружу и будет больно разработчикам, бизнесу и поддержке.
 Такой лажи надо избегать.

Чтобы получать код, подходящий нашим требованиям, надо постоянно думать.
Постоянно думать сложно: выходит медленно и постоянно ошибаешься.
Поэтому некоторые кусочки думанья, которые касаются кода, мы выносим в
стайлгайд. Теперь в некоторых случаях можно не думать, а просто пользоваться правилом.

К гайду нужно относиться не как к строгому своду правил, а как к опытному советнику.
Соблюдаем правила не ради правил, а чтобы получать классный код, отвечающий нашим требованиям.

Нам также важно, чтобы код нравился команде разработки. Поэтому наш гайд
заточен под участников нашей команды и их вкусы. Вам это может быть не по вкусу.
Это нормально. Расслабьтесь. Выдохните. Закажите виски сауэр.


## Можно нарушать

Любое правило из этого гайда можно нарушить. Более того, в некоторых
ситуациях не нарушать гайд – это ошибка. Такие ситуации случаются редко,
и в каждой из них нужно иметь железную аргументацию для нарушения.

Ни одно из правил не соблюдаем ради соблюдения правила.
Бывают ситуации, когда можно сделать `import *`, `except Exception`,
отступы табами и длиннющие строки. Смело это делаем, если уверены, что это улучшит код.
Устраивать пляски с бубном ради Карго-культа не для нас.


## Последний Python

В бою 3.7, на стейджинге 3.7, на всех инстансах 3.7,
думаем тоже на 3.7.


## PEP8

Любим и соблюдаем PEP8, за исключением длины строки. У нас жёсткая граница - 120 символов.

## Комментарии

### Нет необходимых комментариев

Есть правила, которые требуют написание комментариев в некоторых местах.
Например, у публичных модулей, классов, методов.

У нас таких правил нет. Комментарии необходимо писать там, где они к месту:
когда функция делает что-то неочевидное, обрабатывается хитрый случай.

Если из названия сущности непонятно, что она делает, сначала стоит
попробовать её переименовать, чтобы было понятно.


### Однострочные докстринги

Короткий способ написать докстринг, который помещается на одной строке.
Переносить не надо, заканчивать точкой обязательно.

Плохо:
~~~
"""
Подсчёт статистки по юрлицам клиентов.
"""
~~~

Плохо:
~~~
"""Подсчёт статистки по юрлицам клиентов"""
~~~


Хорошо:
~~~
"""Подсчёт статистки по юрлицам клиентов."""
~~~


### Многострочные докстринги

Нужны, когда есть что сказать и одной строки мало.
Структура такая: первая строка описывает что это такое и заканчивается точкой.
Отбивается от тела комментария пустой строкой.
У комментария нет дополнительных отступов от кавычек.

Плохо:
~~~
"""
Активный период обслуживания.
Работает как надо, если у человека не более одного активного слота
"""
~~~

Плохо (точка потерялась):
~~~
"""
Активный период обслуживания

Работает как надо, если у человека не более одного активного слота
"""
~~~

Хорошо:
~~~
"""
Активный период обслуживания.

Работает как надо, если у человека не более одного активного слота
"""
~~~

### Инлайновые комментарии

Можно и нужно писать, чтобы описать неявный случай, сослаться на
тикет или вики.

Не пишем, если хотим пошутить, дать коду характеристику или разбить
код на логические блоки. Для первых двух пунктов есть кухня,
для третьего – рефакторинг кода на более мелкие куски.

Плохо:
~~~
# это какое-то говно
~~~

Плохо:
~~~
# получаем данные пользователя
...
# формируем контекст для отчёта
...
# генерируем отчёт
...
~~~


Хорошо:
~~~
# подробнее о формулах можно почитать в BES-482
~~~


### Комменты TODO и FIXME

Пишем комменты TODO и FIXME, когда вспоминаем что-то важное
в процессе работы над фичей и не хотим отвелекаться,
но перед коммитом всё вычищаем: фиксим или создаём тикеты.

Это нужно по двум причинам: во-первых, эти комментарии часто висят
годами и с ними ничего не происходит, а во-вторых, они создают
впечатление поломанности проекта.

Задачам по доработке и рефакторингу место в трекере задач, а не в коде.


## Строковые литералы и форматирование

Используем одинарные кавычки для строковых литералов, но избегаем
обратных слешей в строках.

Для форматирования используем `.format` или эфстринги с нумерованными или
именованными аргументами. Не складываем строки с помощью `+`.

Эфстринги используем по желанию и не напихиваем внутри много логики.

Плохо:
~~~
'%s %s' % (first_name, last_name)
~~~

Плохо:
~~~
'{} {}'.format(first_name, last_name)
~~~

Хорошо:
~~~
'{0} {1}'.format(first_name, last_name)
~~~


## Импорты

Сущности извне стандартной библиотеки импортируем точечно:
перечисляем нужные функции и классы.
Не импортируем весь модуль и точно не делаем `import *`.
Если происходит коллизия имён, используем `as`.

Модули из стандартной библиотеки импортируем целиком.

Импорты делим на три блока, по PEP8.
Сортировка внутри блока не регламентирована.

Плохо:
~~~
from collections import Counter
~~~

Плохо:
~~~
from core import models
~~~

Хорошо:
~~~
import collections
from core.models import Patient
~~~



## Код в `__init__.py`

В инитах можно писать только импорты. Больше ничего нельзя.


## Форматирование вызовов

Если вызов вместе со всеми аргументами умещается на одну строку,
никаких переносов не ставим.

Если вызов не умещается на одну строку, но при переносе
после открывающей скобки всё умещается на две, делаем так.

Если аргументов много, есть вложенные вызовы или вызов не помещается
на две строки, используем расширенное форматирование.
При таком форматировании можно ставить несколько аргументов на одну
строку, если они схожи по смыслу. Например, `date_from` и `date_to`
или `to` и `on_delete`.

Плохо:
~~~
recieved_date = models.DateField(
    'Дата получения', auto_now_add=True,
)  # если аргументы помещаются на одной строке, то скобку стоит оставлять там же

legal = models.ForeignKey(
    'bestdoctor.ClinicLegalEntity',
    models.CASCADE,
    'registries', 'registry',
    verbose_name='юридическое лицо клиники',
    )  # скобка с лишним отступом
~~~

Хорошо:
~~~
recieved_date = models.DateField(
    'Дата получения', auto_now_add=True)

legal = models.ForeignKey(
    'bestdoctor.ClinicLegalEntity',
    models.CASCADE,
    'registries', 'registry',
    verbose_name='юридическое лицо клиники',
)
~~~

Хорошо:
~~~
legal = models.ForeignKey(
    'bestdoctor.ClinicLegalEntity',
    models.CASCADE,
    'registries',
    'registry',
    verbose_name='юридическое лицо клиники',
)
~~~


## Запятые
У всех многострочных перечислений ставим запятую после последнего элемента.
Это касается не только списков, но и вызовов, туплов и всего
остального многострочного с запятыми.

Если перечисление однострочное, то запятой после последнего элемента не ставим.
Исключение – `set` с одним элементом.

Плохо (потерялась последняя запятая):
~~~
list_filter = (
    'legal', 'is_finished', 'is_paid', 'client_registry__record__report_date'
)
~~~

Плохо:
~~~
Act.objects.create(
    date=today(),
    act_type='tech',
    report_date=report_date,
    is_finished=False
)
~~~

Хорошо:
~~~
list_filter = (
    'legal', 'is_finished', 'is_paid', 'client_registry__record__report_date',
)

Act.objects.create(
    date=today(),
    act_type='tech',
    report_date=report_date,
    is_finished=False,
)

~~~


## Неиспользуемый код

Мы хотим, чтобы в нашем коде было как можно меньше багов.
Классный способ избавиться от багов – избавиться от кода.
Нет кода – нет проблем.

Поэтому мы удаляем из кодовой базы весь код, который можем.
Закомментированный код, неактуальные фичи,
какие-то разовые скрипты – всё под нож.

Потом их можно несложно вытащить т.к. все коммиты привязаны к тикету в таск-менеджере,
поэтому если понадобится найти удалённый код, всегда можно отыскать тикет,
потом его коммиты, а потом накатить их.

Всё, что не нужно прямо сейчас и не понадобится в течение месяца – под нож.

## Данные в настройках

Мы стараемся класть данные туда, где им место, и в последнюю очередь храним их в настройках. Вот пример, в котором мы переносим данные в БД с помощью `BooleanField`:

Было:

```python
# settings.py
NOTIFY_IN_SLACK_COMPANY_IDS = [123, 456, 789]

# code
send_slack_notification(NOTIFY_IN_SLACK_COMPANY_IDS)
```

Стало:

```python
# Теперь это просто компании с галочкой notify_in_slack
notify_in_slack_company_ids = Company.objects.filter(notify_in_slack=True).value_list('id', flat=True)
send_slack_notification(notify_in_slack_company_ids)
```

## Правила для полей Django-моделей

1. Порядок указания полей регламентирован в [flake8-class-attributes-order](https://github.com/best-doctor/flake8-class-attributes-order).
2. Названия полей типа `DateTimeField` заканчиваем на `_at`.
3. Названия полей типа `DateField` заканчиваем на `_date`.
4. Если у поля есть `choices`, то оформляем его через `Enum`.
5. У каждой модели сразу делаем `__str__` и проверяем, что оно не генерирует много запросов к БД.
6. Всем полям типа `ForeignKey` обязательно указываем `related_name`.

## Правила для Django urls

 1. В `urls.py` приложения не используем декораторы. Для Class-based views используем `method_decorator` для cоответствующих типов HTTP запросов, подробнее можно почитать о данном декораторе в [официальной документации Django](https://docs.djangoproject.com/en/2.2/topics/class-based-views/intro/#decorating-the-class).
 
 
