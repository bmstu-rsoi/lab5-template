## Flight Booking System

Система предоставляет пользователю возможность поиска и покупки билетов. При покупке билетов пользователю начисляются
баллы, которые он может использовать для оплаты.

Описание в формате [OpenAPI](%5Binst%5D%5Bv1%5D%20Flight%20Booking%20System.yml).

### Данные для тестов

Создать данные для тестов:

```yaml
airport:
  – id: 1
    name: Шереметьево
    city: Москва
    country: Россия
  - id: 2
    name: Пулково
    city: Санкт-Петербург
    coutry: Россия

flight:
  - id: 1
    flight_number: "AFL031"
    datetime: "2021-10-08 20:00"
    from_airport_id: 1
    to_airport_id: 2
    price: 1500
```
