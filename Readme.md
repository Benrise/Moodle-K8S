# LMS Moodle + CodeRunner + Docker/K8S/Helm

Реализация с помощью:
1. Docker Compose
2. Kubernetes
3. Helm Chart




## Необходимое ПО

* Docker
* Windows WSL
* Helm

## Запуск с помощью Docker Compose

### Запуск:

```
docker compose up -d --build
```

### Сброс:

```
docker compose down
```

## Запуск в среде Kubernetes

### Запуск:

```
kubectl apply -f deployment.yaml
kubectl apply -f pvc.yaml
kubectl apply -f service.yaml
```

### Сброс:

```
kubectl delete deployment --all
kubectl delete pvc --all
kubectl delete svc --all
```

## Запуск Helm Chart

### Запуск:

```
helm install app-dev ./
```

### Сброс:

```
helm delete app-dev
```

## Доступ к сайту

### Для Kubernetes и Helm Chart:

```
kubectl get svc
moodle-service -> PORT(S) -> 80:XXXXX

localhost:XXXXX
```

### Для Docker Compose:

```
localhost
```

## Авторизация LMS Moodle

login: user
password: bitnami

## Установка CodeRunner

1. Администрирование -> Плагины -> Установка плагинов -> Выберете файл... -> Загрузить файл -> Выбрать архив 'coderunner.zip'
2. Установите плагины, необходимые для удовлетворения зависимостей (1)
3. Завершите установку плагином кнопкой "Обновить Moodle"

## Настройка CodeRunner

1. Администрирование -> Плагины -> Обзор плагинов -> CodeRunner:
    - Сервер Jobe необходимо установить значение на jobe-service:4000 или jobe (в случае docker-compose).
    - Сохраните изменения.
2. Далее:
    - Администрирование -> Основные (спускаемся вниз) -> Безопасность -> Безопасность HTTP
        - В списке заблокированных хостов cURL стереть 10.0.0.0/8.
        - В списке разрешенных портов cURL внести порты 8080 и 4000.

## Создание курса и тестирование работы

1. Создайте курс:
    - Мои курсы -> Создать новый курс -> Войти в режим редактирования (правый верхний угол) -> Общее -> Добавить элемент или ресурс -> Тест -> Созданный тест -> Добавить вопрос (справа синяя ссылка "Добавить ⮛") -> (+ новый вопрос)
        - Вопросы -> CodeRunner -> "Добавить" -> Обновить страницу
        - Тип вопроса CodeRunner -> Тип вопроса -> python3
        - Общее -> Название вопроса {ввести} -> Текст вопроса {ввести}
        - Ответ -> print(123) {ввести}
        - Тестовые примеры -> Тестовый пример 1 -> {оставить пустым} -> Ожидаемый результат -> 123 {ввести}
2. Тестируйте работу:
    - Мои курсы -> Созданный курс -> Созданный тест -> "Предварительный просмотр теста" -> {попробовать ввести print(123) и др.}
