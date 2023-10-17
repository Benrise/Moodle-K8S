--- ПО --

Docker
Windows WSL
Helm


--- Docker Compose --



--- Kubernetes ---

Запуск:
kubectl apply -f deployment.yaml
kubectl apply -f pvc.yaml
kubectl apply -f service.yaml

Сброс:
kubectl delete deployment --all
kubectl delete pvc --all
kubectl delete svc --all

--- Helm Chart  ---

Запуск:
helm install app-dev ./

Сброс:
helm delete app-dev


--- Доступ к сайту ---

Для Kubernetes и Helm Chart:
kubectl get svc 
moodle-service -> PORT(S) -> 80:ХХХХХ

localhost:XXXXX

Для Docker Compose:

localhost

--- Авторизация ---

login: user
password: bitnami

--- Установка CodeRunner ---

Администрирование -> Плагины -> Установка плагинов -> Выберете файл... -> Загрузить файл -> Выбрать архив 'coderunner.zip'

Важно: нужно установить плагины, необходимые для удовлетворения зависимостей (1)

Закончить установку плагином кнопкой "Обновить Moodle"

--- Настройка CodeRunner ---


Администрирование -> Плагины -> Обзор плагинов -> CodeRunner:
1. Сервер Jobe необходимо установить значение на jobe-service:4000 или jobe (в случае docker-compose).
2. Сохранить изменения.

Далее:
Администрирование -> Основные (спускаемся вниз) -> Безопасность -> Безопасность HTTP

1. В списке заблокированных хостов cURL стереть 10.0.0.0/8.
2. В списке разрешенных портов сURL внести порты 8080 и 4000.

--- Создание курса и тестирование работы ---

Создаем курс:

Мои курсы 
    -> Создать новый курс 
        -> Войти в режим редактирования (правый верхний угол) 
            -> Общее 
                -> Добавить элемент или ресурс 
                    -> Тест 
                        -> Созданный тест 
                            -> Добавить вопрос (справа синяя ссылка "Добавить ⮛") -> (+ новый вопрос)
                                -> Вопросы -> CodeRunner -> "Добавить" -> Обновить страницу
                                    -> Тип вопроса CodeRunner -> Тип вопроса -> python3
                                    -> Общее 
                                        -> Название вопроса {ввести}
                                        -> Текст вопроса {ввести}
                                    -> Ответ
                                        -> print(123) {ввести}
                                    -> Тестовые примеры
                                        -> Тестовый пример 1 
                                            -> {оставить пустым}
                                        -> Ожидаемый результат
                                            -> 123 {ввести}

Тестируем работу:
Мои курсы 
    -> Созданный курс 
        -> Созданный тест 
            -> "Предварительный просмотр теста" -> {попробовать вести print(123) и др.}



                                    



