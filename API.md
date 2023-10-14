# API

## Points

### GET api/points

#### Модель запроса

| Имя       | Место | Формат          | Описание               |
| --------- | ----- | --------------- | ---------------------- |
| latitude  | query | number($double) | Географическая широта  |
| longitude | query | number($double) | Географическая долгота |
| radius    | query | number($double) | Радиус (масштаб карты) |

#### Модель ответа

| Код  | Описание              |
| :--- | :-------------------- |
| 200  | [Point](#point)[]     |
| 400  | Bad Request           |
| 500  | Internal Server Error |

### GET api/points/{id:guid}

#### Модель запроса

| Имя  | Место | Формат        | Описание     |
| ---- | ----- | ------------- | ------------ |
| id   | path  | string($uuid) | Id отделения |

#### Модель ответа

| Код  | Описание              |
| :--- | :-------------------- |
| 200  | [Point](#point)       |
| 400  | Bad Request           |
| 500  | Internal Server Error |

### POST api/points/{id:guid}/book

#### Модель запроса

| Имя         | Место | Формат             | Описание     |
| ----------- | ----- | ------------------ | ------------ |
| id          | query | string($uuid)      | Id отделения |
| time        | body  | string($date-time) | Время        |
| serviceType | body  | string             | Тип услуги   |

#### Модель ответа

| Код  | Описание              |
| :--- | :-------------------- |
| 204  | NoContent             |
| 400  | Bad Request           |
| 404  | Not Found             |
| 500  | Internal Server Error |

### POST api/points/{id:guid}/check

#### Модель запроса

| Имя        | Место | Формат             | Описание                                                  |
| ---------- | ----- | ------------------ | --------------------------------------------------------- |
| id         | query | string($uuid)      | Id отделения                                              |
| time       | body  | string($date-time) | Время в формате ISO-8601 (2023-10-15T13:30:00.000Z)       |
| clientType | body  | string             | Физическое или юридическое лицо. Значения: Private, Legal |

#### Модель ответа

| Код  | Описание                        |
| :--- | :------------------------------ |
| 200  | true - открыто, false - закрыто |
| 400  | Bad Request                     |
| 404  | Not Found                       |
| 500  | Internal Server Error           |

## Atms

### GET api/atms

#### Модель запроса

| Имя       | Место | Формат          | Описание               |
| --------- | ----- | --------------- | ---------------------- |
| latitude  | query | number($double) | Географическая широта  |
| longitude | query | number($double) | Географическая долгота |
| radius    | query | number($double) | Радиус (масштаб карты) |

#### Модель ответа

| Код  | Описание              |
| :--- | :-------------------- |
| 200  | [Atm](#atm)[]         |
| 400  | Bad Request           |
| 500  | Internal Server Error |

### GET api/points/{id:guid}

#### Модель запроса

| Имя  | Место | Формат        | Описание     |
| ---- | ----- | ------------- | ------------ |
| id   | path  | string($uuid) | Id банкомата |

#### Модель ответа

| Код  | Описание              |
| :--- | :-------------------- |
| 200  | [Atm](#atm)           |
| 400  | Bad Request           |
| 500  | Internal Server Error |

## Модели

### Point

| Имя                 | Тип                   | Описание                |
| ------------------- | --------------------- | ----------------------- |
| id                  | string($uuid)         | Id отделения            |
| salePointName       | string                | Наименование ТП         |
| address             | string                | Адрес ТП                |
| status              | string                | Статус ТП               |
| openHours           | [OpenHour](#openhour) | Режим обслуживания ЮЛ   |
| rko                 | boolean               | Наличие РКО             |
| openHoursIndividual | [OpenHour](#openhour) | Режим обслуживания ФЛ   |
| officeType          | string                | Тип офиса               |
| salePointFormat     | string                | Формат ТП               |
| suoAvailability     | string                | Наличие СУО             |
| hasRamp             | boolean               | Наличие пандуса         |
| latitude            | number($double)       | Географическая широта   |
| longitude           | number($double)       | Географическая долгота  |
| metroStation        | string                | Станция метро           |
| distance            | integer($int32)       | Расстояние              |
| kep                 | boolean               | Признак выдачи КЭП      |
| myBranch            | boolean               | Признак "Мое отделение" |

### OpenHour

| Имя   | Тип    | Описание    |
| ----- | ------ | ----------- |
| days  | string | День недели |
| hours | string | Часы работы |

### Atm

| Имя       | Тип                   | Описание               |
| --------- | --------------------- | ---------------------- |
| id        | string($uuid)         | Id банкомата           |
| address   | string                | Адрес                  |
| latitude  | number($double)       | Географическая широта  |
| longitude | number($double)       | Географическая долгота |
| allDay    | boolean               | Круглосуточно или нет  |
| services  | [Services](#services) | Доступность сервисов   |

### Services

| Имя               | Тип                               |
| ----------------- | --------------------------------- |
| Wheelchair        | [ServiceSupport](#servicesupport) |
| Blind             | [ServiceSupport](#servicesupport) |
| NfcForBankCards   | [ServiceSupport](#servicesupport) |
| QrRead            | [ServiceSupport](#servicesupport) |
| SupportsUsd       | [ServiceSupport](#servicesupport) |
| SupportsChargeRub | [ServiceSupport](#servicesupport) |
| SupportsEur       | [ServiceSupport](#servicesupport) |
| SupportsRub       | [ServiceSupport](#servicesupport) |

### ServiceSupport

| Имя               | Тип    |
| ----------------- | ------ |
| ServiceCapability | string |
| ServiceActivity   | string |
