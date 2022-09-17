# API социальной сети "Yatube"

### **Описание проекта**
В проекте реализован интерфейс API, благодаря которому социальная сеть "Yatube" сможет взаимодействовать с другой программой.

### **Использованные технологии**

| программа                     | версия |
|-------------------------------|--------|
| Django                        | 2.2.16 |
| pytest                        | 6.2.4  |
| pytest-pythonpath             | 0.7.3  |
| pytest-django                 | 4.4.0  |
| djangorestframework           | 3.12.4 |
| djangorestframework-simplejwt | 4.7.2  |
| Pillow                        | 8.3.1  |
| PyJWT                         | 2.1.0  |
| requests                      | 2.26.0 |

### **Запускаем проект в dev режиме на OC Linux**
Клонировать репозиторий с GitHub
```
git clone git@github.com:boginskiy/api-Yatube.git
```

Установить виртуальное окружение venv
```
python3 -m venv venv
```

Aктивировать виртуальное окружение venv
```
source venv/bin/activate
```

Установить зависимости из файла requirements.txt
```
pip install -r requirements.txt
```

Выполнить миграции
```
python3 manage.py migrate
```

Запустить проект
```
python3 manage.py runserver
```

### **Примеры запросов API**
#### **Запросы для публикаций (posts)**

Получить спискок публикаций (GET): `http://127.0.0.1:8000/api/v1/posts/`

* _При настройки постраничного вывода контента необходимо указать параметры:
limit - количество публикаций на страницу;
offset - номер страницы после которой начинать выдачу_
* _Допустимы анонимные запросы от пользователей_
---

###### Запрос к posts
Создание публикации (POST): `http://127.0.0.1:8000/api/v1/posts/`

```
    # Тело запроса

    {
        "text": "string",
        "group": 1
    }
```

* _Добавить публикацию может только авторизованный пользователь_
---

###### Запрос к posts
Получить публикацию (GET): `http://127.0.0.1:8000/api/v1/posts/{post_id}/`

* _{post_id} - id публикации_
* _Допустимы анонимные запросы от пользователей_
---

###### Запрос к posts
Обновление публикации (PUT): `http://127.0.0.1:8000/api/v1/posts/{post_id}/`

```
    # Тело запроса

    {
        "text": "string",
        "image": "string",
        "group": 0
    }
```

* _{post_id} - id публикации_
* _Обновить публикацию может только автор публикации_
---

###### Запрос к posts
Частичное обновление публикации (PATCH): `http://127.0.0.1:8000/api/v1/posts/{post_id}/`

```
    # Тело запроса

    {
        "text": "string",
        "image": "string",
        "group": 0
    }
```

* _{post_id} - id публикации_
* _Частично обновить публикацию может только автор публикации_
---

###### Запрос к posts
Удаление публикации (DELETE): `http://127.0.0.1:8000/api/v1/posts/{post_id}/`

* _{post_id} - id публикации_
* _Удалить публикацию может только автор публикации_
---

#### **Запросы для комментариев к публикациям (comments):**

Получение всех комментариев к публикации (GET): `http://127.0.0.1:8000/api/v1/posts/{post_id}/comments/`

* _{post_id} - id публикации с комментариями_
* _Допустимы анонимные запросы от пользователей_
---

###### Запрос к comments
Добавление нового комментария к публикации (POST): `http://127.0.0.1:8000/api/v1/posts/{post_id}/comments/`

```
    # Тело запроса

    {
        "text": "string"
    }
```

* _{post_id} - id публикации с комментариями_
* _Добавить комментарий к публикации может только авторизованный пользователь_
---

###### Запрос к comments
Получение комментария к публикации по id (GET): `http://127.0.0.1:8000/api/v1/posts/{post_id}/comments/{id}`

* _{post_id} - id публикации с комментариями_
* _{id} - id комментария_
* _Допустимы анонимные запросы от пользователей_
---

###### Запрос к comments
Обновление комментария к публикации по id (PUT): `http://127.0.0.1:8000/api/v1/posts/{post_id}/comments/{id}`

```
    # Тело запроса

    {
        "text": "string"
    }
```

* _{post_id} - id публикации с комментариями_
* _{id} - id комментария_
* _Обновить комментарий может только автор комментария_
---

###### Запрос к comments
Частичное обновление комментария к публикации по id (PUTCH): `http://127.0.0.1:8000/api/v1/posts/{post_id}/comments/{id}`

```
    # Тело запроса

    {
        "text": "string"
    }
```

* _{post_id} - id публикации с комментариями_
* _{id} - id комментария_
* _Частично обновить комментарий может только автор комментария_
---

###### Запрос к comments
Удаление комментария к публикации по id (DELETE): `http://127.0.0.1:8000/api/v1/posts/{post_id}/comments/{id}`

* _{post_id} - id публикации с комментариями_
* _{id} - id комментария_
* _Удалить комментарий может только автор комментария_
---

#### **Запросы к сообществам (groups):**

Получение списка доступных сообществ. (GET): `http://127.0.0.1:8000/api/v1/groups/`

* _Посмотреть сообщества может только авторизованный пользователь_
---

###### Запрос к groups
Получение информации о сообществе по id. (GET): `http://127.0.0.1:8000/api/v1/{id}/`

* _{id} - id группы_
* _Посмотреть информацию о сообществе может только авторизованный пользователь_
---

#### **Запросы к подпискам (follow):**

Получение всеx подписок пользователя. (GET): `http://127.0.0.1:8000/api/v1/follow/`

* _Возвращает все подписки пользователя, сделавшего запрос_
* _Анонимные запросы запрещены_
---

###### Запрос к follow
Подписка пользователя. (POST): `http://127.0.0.1:8000/api/v1/follow/`

```
    # Тело запроса

    {
        "following": "string"
    }
```

* _Подписка пользователя от имени которого сделан запрос на пользователя переданного в теле запроса_
* _Анонимные запросы запрещены_
---

#### **Запросы к JWT-токен (jwt):**

Получение JWT-токена. (POST): `http://127.0.0.1:8000/api/v1/jwt/create/`

```
    # Тело запроса

    {
        "username": "string",
        "password": "string"
    }
```
---

###### Запрос к JWT-токен
Обновление JWT-токена. (POST): `http://127.0.0.1:8000/api/v1/jwt/refresh/`

```
    # Тело запроса

    {
        "refresh": "string"
    }
```
---

###### Запрос к JWT-токен
Проверка JWT-токена. (POST): `http://127.0.0.1:8000/api/v1/jwt/verify/`

```
    # Тело запроса

    {
        "token": "string"
    }
```

### **Автор**
[Богинский Дмитрий](https://github.com/boginskiy) - python разработчик
