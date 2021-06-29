# API_Yatube

REST API для мини социальной сети Yatube, созданной в рамках учебного курса Яндекс.Практикум
Аутентификация по JWT-токену
Работает со всеми модулями социальной сети Yatube: постами, комментариями, группами, подписчиками.
Предоставляет данные в формате JSON

----

Стек технологий

* Python +Django REST Framework
* библиотека Simple JWT - работа с JWT-токеном
* система управления версиями - git

Как запустить проект:
    Клонируйте репозитроий с проектом:

```python
git clone https://github.com/Marblelsp/api_final_yatube
```

В созданной директории установите виртуальное окружение, активируйте его и установите необходимые зависимости:

```python
pip install -r requirements.txt
```

Создайте в директории файл .env и поместите туда SECRET_KEY, необходимый для запуска проекта: сгенерировать ключ можно на сайте Djecrety

Выполните миграции:

```python
python manage.py makemigrations
python manage.py migrate
```

Создайте суперпользователя:

```python
python manage.py createsuperuser
```

Запустите сервер:

```python
python manage.py runserver
```

Ваш проект запустился на http://127.0.0.1:8000/

Полная документация (redoc.yaml) доступна по адресу http://localhost:8000/redoc/

С помощью команды pytest вы можете запустить тесты и проверить работу модулей
Аутентификация

Выполните POST-запрос http://localhost:8000/api/v1/token/ передав поля username и password.

API вернет JWT-токен в формате:

```json
{
    "refresh": "ХХХХХХХХХХХ",
    "access": "ХХХХХХХХХХХХ"
}
```

Токен вернётся в поле access, а данные из поля refresh нужны для обновления токена

При отправке запроcов передавайте токен в заголовке Authorization: Bearer <токен>
Как работает API_Yatube
Пример http-запроса (POST) для создания поста:

url = 'http://127.0.0.1/api/v1/posts/'

```pyton
data = {'text': 'Your post'}
headers = {'Authorization': 'Bearer your_token'}
request = requests.post(url, data=data, headers=headers)
```

Ответ API_Yatube:

Статус- код 200
```json
{
  "id": 0,
  "text": "string",
  "author": "string",
  "pub_date": "2020-08-20T14:15:22Z"
}
```
Пример http-запроса (GET) для получения списка постов:


url = 'http://127.0.0.1:8000/api/v1/posts/'

headers = {'Authorization': 'Bearer your_token'}
request = requests.get(api, headers=headers)

Ответ API_Yatube:
Статус- код 200

```json
[
    {
        "id": 1,
        "author": "admin",
        "text": "Очень важный пост",
        "pub_date": "2021-06-29T09:54:18.773484Z",
        "group": null
    }
]
```
