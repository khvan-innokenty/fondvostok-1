# API Privatization-FondVostok

## POST Создание нового участка

Клиент формирует POST-запрос по адресу http://domain/main/vostok/areas

Для авторизации требуется передать access_token пользователя. Возможно 2 варианта:
1. через HTTP заголовок
	Пример: Authorization: Bearer {your_access_token_here}
2. через параметр строки запроса
	Пример: http://domain/main/vostok/areas?access_token={your_access_token_here}

Данные по участку необходимо передать в json формате. 
На текущий момент обязательные поля:
1. **id** - идентификатор участка, уникальная строка
1. **coords** - массив координат в градусах с точностью 6 точек после запятой
1. **area** - площадь участка в гектарах с точностью 2 точки после запятой

```javascript
{
   "id": "1234567890ABCD",
   "coords": [
      {
         "lat": 43.406667,
         "lng": 134.895467
      },
      {
         "lat": 43.419250,
         "lng": 134.932517
      },
      {
         "lat": 43.413717,
         "lng": 134.937050
      },
      {
         "lat": 43.400583,
         "lng": 134.898900
      }
   ],
   "buffer_coords": [
      {
         "lat": 43.406667,
         "lng": 134.895467
      },
      {
         "lat": 43.419250,
         "lng": 134.932517
      },
      {
         "lat": 43.413717,
         "lng": 134.937050
      },
      {
         "lat": 43.400583,
         "lng": 134.898900
      }
   ],
   "area": 242.71,
   "act": "Приказ территориального управления Росрыболовства от 03.06.2017 №106",
   "municipality": "Приморский край",
   "waterbodies": [
      "Японское море",
      "Охотское море"
   ],
   "landmarks": "3 км на запад от о. Беличий",
   "start_price": 96954.84,
   "deposit": 38781.93,
   "bid_increment": 4664.77,
   "vol_pasturable": 251.7,
   "vol_industrial": 308.33,
   "period_pasturable": 6,
   "period_industrial": 4,
   "water_use": "Совместное",
}
```

Пример ответа сервера:
```javascript
{
   "code": 202,
   "message": "Запрос принят в обработку",
   "id": "1234567890ABCD",
   "timestamp": 1496411085
}
```

## POST Получение информации об участках

Клиент формирует POST-запрос по адресу http://domain/main/vostok/areas/search
На текущий момент авторизация не требуется.

Массив идентификаторов участков необходимо передать в json формате. 
```javascript
{
   "ids": [
   "1234567890ABCD",
   "1234567890ABCX"
   ]
}
```

Пример ответа сервера:
```javascript
[
   {
      "code": 601,
      "message": "Заявка отправлена",
      "id": "1234567890ABCD",
      "timestamp": 1496411085,
      "data":{
         "sent_date": "2017-06-02",
         "request_number": "127-028"
      }
   },
   {
      "code": 404,
      "message": "Участок не существует",
      "id": "1234567890ABCX",
      "timestamp": 1496411085,
      "data": null
   }
]
```

Дополнительная информация, содержащаяся в поле **data** будет обсуждаться позднее.

## GET Получение информации об участке

Клиент формирует GET-запрос по адресу http://domain/main/vostok/areas/{id}
На текущий момент авторизация не требуется.

Пример ответа сервера:
```javascript
{
	"code": 404,
	"message": "Участок не существует",
	"id": "1234567890ABCX",
	"timestamp": 1496411085,
	"data": null
}
```

Дополнительная информация, содержащаяся в поле **data** будет обсуждаться позднее.