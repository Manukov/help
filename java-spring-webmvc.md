
* [Annotation](#annotation)
* [Controller](#controller)
* [DispatcherServlet](#dispatcherservlet)
* [Spring MVC](#spring-web-mvc)


### Spring Web MVC
Spring Web MVC - это модуль Spring Framework который позволяет разрабатывать web-приложения с использованием архитектуры Model-View-Controller. При работе с Spring MVC реализовываются только:
* Controller
* Model
* View

### Annotation

### Controller
Controller - это класс аннотированный [@Controller](java-spring.md#controller-annotation) который:
* обрабатывает запросы пользователя
* обменивается данными с моделью
* показывает пользователю правильное представление
* Переадресовывает пользователя на другие страницы

### DispatcherServlet
DispatcherServlet - это входная точка в Spring MVC приложение. Spring MVC предоставляет его реализацию (самостоятельно реализовывать не надо). Это компонент, ко торорый:
1. Принимает Http-запрос
2. Отправляет запрос на нужный Controller

### Model
Model - это класс аннотированный @Entity. Этот компонент/слой:
* хранит данные
* взаимодействует с БД для получения данных
* отдает данные контроллеру

### View
View (Представление) - это html-страница.