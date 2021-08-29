# Онлайн-проекта <a href="https://github.com/JavaWebinar/topjava">TopJava</a>

## [Патчи](https://drive.google.com/drive/u/1/folders/1ZsPX879m6x4Va0Wy3D1EQIBsnZUOOvao)

### ![correction](https://cloud.githubusercontent.com/assets/13649199/13672935/ef09ec1e-e6e7-11e5-9f79-d1641c05cbe6.png) Правки в проекте

#### Apply 12_fix

- Добавил `NamedTo`. Если проект использовать как начальный код для чего-то большего, он пригодится.
- Перенес `MealTestData` и `UserTestData` в соответствующие пакеты. Потянуло за собой много изменений в импортах.

## Spring Boot + Миграция

### 1. Пройдите основы Spring Boot: [BootJava](https://javaops.ru/view/bootjava)

### 2. Миграция REST части проекта `Calories Management` на Spring Boot

Вычекайте в отдельную папку (как отдельный проект) ветку `spring-boot`:

```
git clone --branch spring_boot --single-branch https://github.com/JavaWebinar/topjava.git topjava_boot
```  

Если будете его менять, [настройте `git remote`](https://javaops.ru/view/bootjava/lesson01#project)

- Проект сделал с минимальным количеством кода (как тестовое задание или ТЗ на выпускной проект): убрал слой сервисов, профили, группы, локализацию, весь UI.
- **В отличие от курса BootJava не использую Spring Data REST. Мне кажется, что борьба с кастомизацией контроллеров и тестами займут больше времени, чем выигрыш от автогенерации контроллеров**
- База создается автогенерацией по модели (для тестового задания и базы в памяти - хороший вариант).
- В нашем приложении остались только REST контроллеры, не надо добавлять `Rest` в имя. Каждый контроллер занимается своими CRUD, переименовал `Admin[Rest]Controller` в `AdminUserController`
- Заменил префикс `/rest` в URLs на `/api`
- Исключил `AppConfig.h2Server` из тестов, он там не нужен
- Удалил проверки `ValidationUtil.checkNotFound`. Для `get` использую `ResponseEntity.of(repository.findById(id))`, для модификаций `Repository.checkBelong`
- Сделал `BaseRepository` - сюда можно размещать [общие методы репозиториев](https://stackoverflow.com/questions/42781264/multiple-base-repositories-in-spring-data-jpa)
- Вместо своих конверторов использую `@DateTimeFormat`
- Мигрировал все тесты контроллеров. В тестовом проекте столько тестов **НЕ ТРЕБУЕТСЯ**, достаточно нескольких на основные юзкейсов.
- [REST API documentation](http://localhost:8080/swagger-ui.html) сделал на основе [OpenAPI 3.0](https://javaops.ru/view/bootjava/lesson06#openapi). **Добавьте в выпускной проект - это будет большим
  плюсом и избавит от необходимости писать документацию**. Не забудьте ссылку на нее в `readme.md`!
- Кэширование желательно в выпускном. 7 раз подумайте, что будете кэшировать! **Максимально просто, самые частые запросы, которые редко изменяются**.

### 3. Начальный код [проекта TopJava-2](https://github.com/JavaOPs/topjava2) обновил.

Добавил `NoHtml` и в `pom.xml` взял свежие версии. Его отличие от нашей ветки `spring_boot` - нет еды.    
Для основы выпускного можно использовать любой из них - просто перенесите сюда свою модель, контроллеры и сервисы. 
