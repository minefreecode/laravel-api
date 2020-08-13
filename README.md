# Описание 
`API` на `laravel 7`: 
- У клиента есть имя, фамилия, один или более номеров телефона, один или более почтовых ящиков. 
- Имеются пять методов: добавления, просмотра, изменения, удаления, поиска клиента. 
- Поиск осуществляется в четырех вариантах: по имени и фамилии, телефону, почте или по всем предыдущим опциям одновременно. 
- Тип поиска передается в параметре запроса. 
- Доступ к API осуществляется по токену. 
- Имеется лог всех операций через API с сохранением авторства.

# Разворачивание
1. Склонируйте проект с репозитория
2. Выполните `composer install && composer update`
3. Созджайте `.env` как в примере `.env.example`
4. Создайте базу данных `laravel`
5. Выполните `php artisan passport:install`
    Выпишите результаты выполнения команды
    ````
    Personal access client created successfully.
    Client ID: 1
    Client secret: 9u2RfPphmxCoVgG3NbGzKgUtdBmWwAHAU70AINbT
    Password grant client created successfully.
    Client ID: 2
    Client secret: N05c9s7Xy2WZtBZ7jxqjmHeeTlJ2OuEFJ8wZPQNx
    ````
    в соответствующие строки в файле
    ````
    PERSONAL_CLIENT_ID=1
    PERSONAL_CLIENT_SECRET=9u2RfPphmxCoVgG3NbGzKgUtdBmWwAHAU70AINbT
    PASSWORD_CLIENT_ID=2
    PASSWORD_CLIENT_SECRET=N05c9s7Xy2WZtBZ7jxqjmHeeTlJ2OuEFJ8wZPQNx
    ````
    Это нужно для OAuth-авторизации с помощью токенов.
    Passport-авторизация использована поскольку с появлением AirLock она не устарела и все еще 
    является основной авторизацией проверенная временем.
6. Выполните `php artisan config:cache`
7. Выполните `php artisan migrate`
8. Выполните `php artisan db:seed`
9. Тестирование проекта `php artisan test`. Эта команда  - новинка в `Laravel 7`. перед тестированием
обязательно убедитесь что выполнили `php artisan db:seed`
10. Для запуска сервера `php artisan serve` 

# Особенности кода приложения
1. Используется OAuth-авторизация для API
2. Для тестирования используются транзакции
3. Для тестов имеется базовый класс `TestCase`, в котором получается токен для выполнения тестов. Получение токена 
реализовано через сервис IoC с интерфейсом `IAuthToken` 
4. Для каждого из объектов имеются `Seeder`, `Factory`
5. Реализован постраничный просмотр
6. Все `API` покрыто тестами. С
