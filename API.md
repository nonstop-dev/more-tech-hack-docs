# API банковских точек

## GET api/points

### Модель запроса

| Имя       | Место | Формат          | Описание               |
| --------- | ----- | --------------- | ---------------------- |
| latitude  | query | number($double) | Географическая широта  |
| longitude | query | number($double) | Географическая долгота |
| radius    | query | number($double) | Радиус (масштаб карты) |

### Модель ответа

| Код  | Описание              |
| :--- | :-------------------- |
| 200  | [Point](#point)[]     |
| 400  | Bad Request           |
| 404  | Not Found             |
| 500  | Internal Server Error |

## GET api/points/{id:guid}

### Модель запроса

| Имя  | Место | Формат        | Описание     |
| ---- | ----- | ------------- | ------------ |
| id   | path  | string($uuid) | Id отделения |

### Модель ответа

TBD

## POST api/points/{id:guid}/book

### Модель запроса

| Имя         | Место | Формат             | Описание     |
| ----------- | ----- | ------------------ | ------------ |
| id          | query | string($uuid)      | Id отделения |
| time        | body  | string($date-time) | Время        |
| serviceType | body  | string             | Тип услуги   |

### Модель ответа

| Код  | Описание              |
| :--- | :-------------------- |
| 204  | NoContent             |
| 400  | Bad Request           |
| 404  | Not Found             |
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

| Имя   | Тип    | Описание |
| ----- | ------ | -------- |
| days  | string |          |
| hours | string |          |



