# Проект YaMDb
## Описание
Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).

Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха.

Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор.

Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

## Технологии
Python 3.7, Django 2.2, DRF 3.12, JWT 2.1.0, gunicorn 20.0.4, nginx, PostgreSQL.

## Установка
Для запуска контейнеров необходимо склонировать к себе репозиторий.
Перейти в папку infra.
Заполнить своими данными подключение к БД, секретный ключ Django, параметры подключения к почтовому серверу в файле .env
`DB_ENGINE=your_db_engine`

`DB_NAME=your_db_name`

`POSTGRES_USER=your_db_user`

`POSTGRES_PASSWORD=your_db_user_password`

`DB_HOST=your_db_hostname_or_ip`

`DB_PORT=your_db_connection_ip`

`SECRET_KEY='some_secret_key_for_django'`

`EMAIL_USER=username@domain.com`

`EMAIL_PASS=somepassword`

`EMAIL_HOST=smtp.domain.com`

В папке nginx в файле конфигурации default.conf указать ip адрес вашего веб сервера.

`server_name = 127.0.0.1`

Далее запустите контейнеры с помощью 'docker-compose':

`docker-compose up -d`

Выполните миграции БД:

`docker-compose exec web python manage.py migrate`

Создайте суперпользователя Django:

`docker-compose exec web python manage.py createsuperuser`

Выполните при необходимости первичное наполение БД тестовыми данными:

`cat fixtures.json |docker-compose exec -T web python manage.py loaddata --format json -`

Собираем статику:

`docker-compose exec web python manage.py collectstatic --no-input `

Полное описание сервиса доступно по endpoint /redoc/.

Собранный образ доступен на DockerHub albertxyc/api_yamdb
