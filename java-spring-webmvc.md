
* [AbstractAnnotationConfigDispatcherServletInitializer](#abstractannotationconfigdispatcherservletinitializer-class)
* [Annotation](#annotation)
* [Controller](#controller)
* [DispatcherServlet](#dispatcherservlet)
* [Spring MVC](#spring-mvc)


### Spring MVC
Spring Web MVC - это модуль Spring Framework который позволяет разрабатывать web-приложения с использованием архитектуры Model-View-Controller. При работе с Spring MVC реализовываются только:
* Controller
* Model
* View

Поставка: модуль Spring MVC поставляется в библиотеках: [spring-web](#spring-web-dependency), [spring-webmvc](#spring-webmvc-dependency)


### AbstractAnnotationConfigDispatcherServletInitializer-class
AbstractAnnotationConfigDispatcherServletInitializer - абстрактный класс, который реализует интерфейс [WebApplicationInitializer](#webapplicationinitializer-class) и
позволяет более удобно использовать java-конфигурацию вместо [web.xml](java.md#web-xml).

### Annotation

### Controller
Controller - это класс аннотированный [@Controller](java-spring.md#controller-annotation) который:
* обрабатывает запросы пользователя
* обменивается данными с моделью
* показывает пользователю правильное представление
* Переадресовывает пользователя на другие страницы

### DispatcherServlet
DispatcherServlet - это входная точка в Spring MVC приложение. Spring MVC предоставляет его реализацию (самостоятельно реализовывать не надо). Это компонент, которыйна основании настроек:
1. Принимает Http-запрос
2. В зависимости от настроек, для настроенного url отправляет запрос на нужный Controller

DispatcherServlet конфигурируется одним из способов:
* в [web.xml](java.md#web-xml) 
* используя [AbstractAnnotationConfigDispatcherServletInitializer](#abstractannotationconfigdispatcherservletinitializer-class) или [WebApplicationInitializer](#webapplicationinitializer-class)


### DispatcherServlet-class
DispatcherServlet (org.springframework.web.servlet) - реализация [DispatcherServlet](#dispatcherservlet) предоставляемая библиотекой [spring-webmvc](#spring-webmvc-dependency).

### Model
Model - это класс аннотированный @Entity. Этот компонент/слой:
* хранит данные
* взаимодействует с БД для получения данных
* отдает данные контроллеру

### spring-web-dependency
Имеет транзитивные зависимости:
* [spring-beans](java-spring.md#spring-beans-dependency)
* [spring-core](java-spring.md#spring-core-dependency)

Пакеты:
* http
* remoting
* web
  * [@GetMapping](#getmapping-annotation)

Библиотека предоставляет:
* [@GetMapping](#getmapping-annotation)

### spring-webmvc-dependency
Имеет транзитивные зависимости:
* [spring-aop](java-spring.md#spring-aop-dependency)
* [spring-beans](java-spring.md#spring-beans-dependency)
* [spring-expression](java-spring.md#spring-expression-dependency)
* [spring-context](java-spring.md#spring-context-dependency)
* [spring-core](java-spring.md#spring-core-dependency)
* [spring-web](#spring-web-dependency)

Пакеты org.springframework.web.servlet:
* config
* functions
* handler
* i18h
* mvc
* resuorce
* tags
* theme
* view
* [Dispatcherservlet](#dispatcherservlet-class)

### View
View (Представление) - это html-страница.

### WebApplicationInitializer-class
WebApplicationInitializer - интерфейс, который позволяет конфигурировать web-приложение без файла [web.xml](java.md#web-xml). Класс который implemented WebApplicationInitializer переопределяет его метод onStertup и в этом 
методе инициализируется [DispatcherServlet](#dispatcherservlet) и настраивается шаблонизатор. Такой класс автоматически считывается Spring Framework.
```java
public class WebInitializer implements WebApplicationInitializer {
    
    @Override
    public void onStartup(ServletConext conext) {
        //код который до этого помещался в web.xml
    }
}
```


#### @GetMapping-annotation
@GetMapping 