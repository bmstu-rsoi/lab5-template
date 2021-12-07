# Лабораторная работа #5

![GitHub Classroom Workflow](../../workflows/GitHub%20Classroom%20Workflow/badge.svg?branch=master)

## OAuth2 Authorization

### Формулировка

На базе [Лабораторной работы #2](https://github.com/bmstu-rsoi/lab2-template) реализовать OAuth2 token-based
авторизацию.

* Для авторизации использовать OpenID Connect, в роли Identity Provider использовать сторонее решение.
* Реализовать [Authorization flow](https://auth0.com/docs/authorization/flows/authorization-code-flow) на Gateway.
* На Identity Provider настроить возможность
  использования [Resource Owner Password flow](https://auth0.com/docs/authorization/flows/resource-owner-password-flow)
  (для тестов).
* На Gateway Service реализовать метод `GET /api/v1/authorize` для инициации процесса OAuth2 Authorization Flow
  и `GET /api/v1/callback` для обработки callback от Identity Provider для обмена code на token.
* Все остальные методы `/api/**` (кроме `/api/v1/authorize` и `/api/v1/callback`) на Gateway закрыть token-based
  авторизацией.
* В качестве токена использовать [JWT](https://jwt.io/introduction), для валидации токена
  использовать [JWKs](https://auth0.com/docs/security/tokens/json-web-tokens/json-web-key-sets), запрос к Identity
  Provider делать не нужно.
* Убрать заголовок `X-User-Name` и получать пользователя из JWT-токена.
* Если авторизация некорректная (отсутстиве токена, ошибка валидации JWT токена, закончилось время жизни токена
  (поле `exp` в payload)), то отдавать 401 ошибку.
* В `scope` достаточно указывать `openid profile email`.
* Реализовать межсервисную авторизацию с помощью проброса JWT токена между сервисами. Валидацию токена так же
  реализовать через JWKs.

### Требования

1. Для автоматических прогонов тестов в файле [autograding.json](.github/classroom/autograding.json)
   и [classroom.yml](.github/workflows/classroom.yml) заменить `<variant>` на ваш вариант.
1. Код хранить на Github, для сборки использовать Github Actions.
1. Каждый сервис должен быть завернут в docker.
1. В classroom.yml дописать шаги на сборку, прогон unit-тестов.

### Пояснения

1. В роли Identity Provider можно использовать любое решение, вот несколько рабочих вариантов:
    1. [Okta](https://developer.okta.com/docs/guides/)
    2. [Auth0](https://auth0.com/developers)
    3. [Keycloak](https://www.keycloak.org/docs/latest/getting_started/index.html) – self hosted решение, можно
       попробовать его запихнуть во free dyno на Heroku, но там лимит 512Mb памяти и Keycloak может вести себя
       нестабильно.
2. Для получения метадаты для OpenID Connect можно
   использовать [Well-Known URI](https://auth0.com/docs/security/tokens/json-web-tokens/locate-json-web-key-sets):
   `https://[base-server-url]/.well-known/openid-configuration`.
3. Из Well-Known метадаты можно получить Issuer URI и JWKs URI.
4. Для локальной разработки можно поднять Keycloak в docker: `docker compose up keycloak` (для Docker должно быть выдано
   минимум 4Gb, 2CPU).<br>
   Админка доступна по адресу `http://localhost:8090/auth/`, credentials: `admin`/`admin`.<br>
   OpenID Connect well-known
   endpoint: `http://localhost:8090/auth/realms/services-realm/.well-known/openid-configuration`. <br>
   При старте контейнера экспортируется `services-realm`:
    1. clientId/clientSecret: `services`/`81ecb5e5-c132-4c33-ad84-dde95995d4ab`
    2. user: Ivanov Max `tester`/`test`.
6. Для реализации OAuth2 можно использовать сторонние библиотеки.

### Прием задания

1. При получении задания у вас клонируется этот репозиторий для вашего пользователя.
1. После того, как все тесты успешно завершатся, в Github Classroom на Dashboard будет отмечено успешное выполнение
   тестов.

### Варианты заданий

Распределение вариантов заданий аналогично [ЛР #2](https://github.com/bmstu-rsoi/lab2-template).

1. [Flight Booking System](v1/README.md)
1. [Hotels Booking System](v2/README.md)
1. [Car Rental System](v3/README.md)
1. [Library System](v4/README.md)
