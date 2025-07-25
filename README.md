# Провести аналитику рейсов в аэропортах
Есть **csv** файл, расположенный по ссылке. Скачать можно по ссылке: https://disk.yandex.ru/d/xPxSLEfEt6tkvQ. <br>
Там внутри 3 файла, их нужно скачать и положить в папку в проекте **sample_data**. <br>
В этой же папке **sample_data**, после работы **DAG** <br>
будут лежать графики (сейчас их можно там увидеть), расчитанные по на основе данных из файлов.

## Файл с данными о полетах:

`DATE`: Дата полета. <br>
`DAY_OF_WEEK`: День недели. <br>
`AIRLINE`: Авиалиния. <br>
`FLIGHT_NUMBER`: Номер рейса. <br>
`TAIL_NUMBER`: Номер самолета. <br>
`ORIGIN_AIRPORT`: Аэропорт отправления (IATA код). <br>
`DESTINATION_AIRPORT`: Аэропорт назначения (IATA код). <br>
`DEPARTURE_DELAY`: Задержка при вылете (в минутах). <br>
`DISTANCE`: Расстояние (в милях). <br>
`ARRIVAL_DELAY`: Задержка при прибытии (в минутах). <br>
`DIVERTED`: Был ли рейс перенаправлен. <br>
`CANCELLED`: Был ли рейс отменен. <br>
`CANCELLATION_REASON`: Причина отмены (A - авиалиния, B - погода, C - NAS, D - безопасность). <br>
`AIR_SYSTEM_DELAY`: Задержка по вине системы авиадиспетчерского управления. <br>
`SECURITY_DELAY`: Задержка по причинам безопасности. <br>
`AIRLINE_DELAY`: Задержка по вине авиалинии. <br>
`LATE_AIRCRAFT_DELAY`: Задержка по вине позднего прибытия предыдущего рейса. <br>
`WEATHER_DELAY`: Задержка из-за погоды. <br>
`DEPARTURE_HOUR`: Час вылета. <br>
`ARRIVAL_HOUR`: Час прибытия. <br>

## Файл с данными о аэропортах:

`IATA CODE`: Код IATA. <br>
`Airport`: Название аэропорта. <br>
`City`: Город. <br>
`Latitude`: Широта. <br>
`Longitude`: Долгота. <br>

## Файл с данными о авиалиниях: 

`IATA CODE`: Код IATA. <br>
`AIRLINE`: Название авиалинии. <br>

## Задания:

1. Загрузим файл данных в **DataFrame** **PySpark**. Обязательно выведем количество строк.

2. Убедимся, что данные корректно прочитаны (правильный формат, отсутствие пустых строк). Проверим соответствует ли содержимое полей названиям в файлах.

3. Преобразуем текстовые и числовые поля в соответствующие типы данных (например, дата, число).

4. Найдем топ-5 авиалиний с наибольшей средней задержкой.

5. Вычислим процент отмененных рейсов для каждого аэропорта.

6. Определим, какое время суток (утро, день, вечер, ночь) чаще всего связано с задержками рейсов.

7. Добавим в данные о полетах новые столбцы, рассчитанные на основе существующих данных:

**IS_LONG_HAUL**: Флаг, указывающий, является ли рейс дальнемагистральным (если расстояние больше 1000 миль). <br>
**DAY_PART**: Определим, в какое время суток происходит вылет (утро, день, вечер, ночь). <br>

8. Создадим схему таблицы в **PostgreSQL**, которая будет соответствовать структуре ваших данных в даге.

9. Настроим соединение с **PostgreSQL** из кода из **PySpark**. (обязательно сделать это нужно в **Airflow**)

10. Загрузим только 10.000 строк из **DataFrame** в таблицу в **PostgreSQL**. (обязательно сделать это нужно в **Airflow**)

11. Выполним **SQL** скрипт в **Python-PySpark** скрипте, который выведет компанию - общее время полетов ее самолетов.

### Просмотр данных через DBeaver:
В **DBeaver**, после успешной работы пайплайна, можно посмотреть полученную таблицу `airlines_data` в **PostgreSQL**.


#### Для подключение к **PostgreSQL** используются следующие параметры:
```
    Хост: localhost
    Порт: 5432
    База данных: test
    Пользователь: user
    Пароль: password
```

#### Команды для запуска проекта:
```bash
    git clone https://github.com/MikhalevaAnna/pipeline_analyze_airports.git
    cd pipeline_analyze_airports
    docker build -t airflow-with-java-airlines .
    docker-compose up --build
```
    
- Далее идем по адресу - **http://localhost:8080**
- Логин и пароль - **airflow**.

