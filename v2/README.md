## Hotels Booking System

Система предоставляет пользователю сервис поиска и бронирования отелей на интересующие даты. В зависимости от количества
заказов система лояльности дает скидку пользователю на новые бронирования.

Описание в формате [OpenAPI](%5Binst%5D%5Bv2%5D%20Hotels%20Booking%20System.yml).

### Данные для тестов

Создать данные для тестов:

```yaml
hotels:
  – id: 1
    hotelUid: "049161bb-badd-4fa8-9d90-87c9a82b0668"
    name: "Ararat Park Hyatt Moscow"
    country: "Россия"
    city: "Москва"
    address: "Неглинная ул., 4"
    stars: 5,
    price: 10000

loyalty:
  - id: 1
    username: "Test Max"
    reservation_count: 25
    status: "GOLD"
    discount: 10
```
