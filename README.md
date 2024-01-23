# Flask-Calendar-API

## Запуск приложения

```
flask --app ./calendar/server.py run
```


## cURL тестирование

### Добавление нового события
```
curl http://127.0.0.1:5000/api/v1/calendar/ -X POST -d "ГГГГ-ММ-ДД|Заголовок|Текст"
```

### Получение всего списка событий
```
curl http://127.0.0.1:5000/api/v1/calendar/
```

### Получение события по идентификатору / ID == 1
```
curl http://127.0.0.1:5000/api/v1/calendar/1/
```

### Обновление текста события по идентификатору / ID == 1 /  новый текст == "Новый текст"
```
curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "ГГГГ-ММ-ДД|Заголовок|Новый текст"
```

### Удаление события по идентификатору / ID == 1
```
curl http://127.0.0.1:5000/api/v1/calendar/1/ -X DELETE
```


## Пример исполнения команд с выводом

```
$ curl http://127.0.0.1:5000/api/v1/calendar/ -X POST -d "2024-01-23|Заголовок|Текст"
new id: 1

$ curl http://127.0.0.1:5000/api/v1/calendar/ -X POST -d "2024-01-23|Заголовок 2|Текст 2"
failed to CREATE with: MAX events allowed per day: 1

$ curl http://127.0.0.1:5000/api/v1/calendar/ -X POST -d "2024-01-24|Заголовок 2|Текст 2" 
new id: 2

$ curl http://127.0.0.1:5000/api/v1/calendar/
1|2024-01-23|Заголовок|Текст
2|2024-01-24|Заголовок 2|Текст 2

$ curl http://127.0.0.1:5000/api/v1/calendar/1/
1|2024-01-23|Заголовок|Текст

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "2024-01-23|Заголовок|Новый текст"
updated

$ curl http://127.0.0.1:5000/api/v1/calendar/1/
1|2024-01-23|Заголовок|Новый текст

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "2024-01-23|Заголовок|Очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень очень  очень длинный текст"
failed to UPDATE with: text lenght > MAX: 200

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X PUT -d "2024-01-23|Длиииииииииииииииииииииииииииииииииииииииииииииииииииинный заголовок|Текст"
failed to UPDATE with: title lenght > MAX: 30

$ curl http://127.0.0.1:5000/api/v1/calendar/1/ -X DELETE
deleted

$ curl http://127.0.0.1:5000/api/v1/calendar/2/ -X DELETE
deleted

$ curl http://127.0.0.1:5000/api/v1/calendar/
-- пусто --
```