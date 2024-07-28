
* [AbstractAnnotationConfigDispatcherServletInitializer](#abstractannotationconfigdispatcherservletinitializer-class)
* [Annotation](#annotation)
* [Controller](#controller)
* [DispatcherServlet](#dispatcherservlet)
* [spring-web](#spring-web-dependency)
* [spring-webmvc](#spring-webmvc-dependency)
* [Spring MVC](#spring-mvc)
* [WebApplicationInitializer](#webapplicationinitializer-class)


### Spring MVC
Spring Web MVC - это модуль Spring Framework который позволяет разрабатывать web-приложения с использованием архитектуры Model-View-Controller. При работе с Spring MVC реализовываются только:
* Controller
* Model
* View

Поставка: модуль Spring MVC поставляется в библиотеках: [spring-web](#spring-web-dependency), [spring-webmvc](#spring-webmvc-dependency)


### AbstractAnnotationConfigDispatcherServletInitializer-class
AbstractAnnotationConfigDispatcherServletInitializer - абстрактный класс, который реализует интерфейс [WebApplicationInitializer](#webapplicationinitializer-class) и позволяет более удобно использовать java-конфигурацию вместо [web.xml](java.md#web-xml). 
Этот класс дополнительно требует подключения зависимости "javax.servlet-api".

### Annotation
* [@EnableWebMvc](#enablewebmvc-annotation)
* [@Getmapping](#getmapping-annotation)

### Controller
Controller - это класс аннотированный [@Controller](java-spring.md#controller-annotation) который:
* обрабатывает запросы пользователя
* обменивается данными с моделью
* показывает пользователю правильное представление
* Переадресовывает пользователя на другие страницы

Описание:
* методы контроллера могут иметь любое название
* обычно (но не всегда) каждый метод соотвествет одному url


### DispatcherServlet
DispatcherServlet - это входная точка в Spring MVC приложение. Spring MVC предоставляет его реализацию (самостоятельно реализовывать не надо). Это компонент, которыйна основании настроек:
1. Принимает Http-запрос
2. В зависимости от настроек, для настроенного url отправляет запрос на нужный Controller

<details><summary>Example: конфигурация Dispatcher Servlet при xml-конфигурации</summary>

При xml конфигурации используется [web.xml](java.md#web-xml) и файл в котором настраивается шаблонизатор.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" version="4.0">
  <display-name>Archetype Created Web Application</display-name>
  <absolute-ordering/>
  <servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <!-- ссылка на файл с настройками шаблонизатора. -->
      <param-value>/WEB-INF/engineConfig.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <!-- все запросы на один диспетчер сервлетов -->
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>
```
</details>

<details><summary>Example: конфигурация Dispatcher Servlet при java-based конфигурации</summary>

При java-based конфигурации используется один из 2-х вариантов:
* наследование от [AbstractAnnotationConfigDispatcherServletInitializer](#abstractannotationconfigdispatcherservletinitializer-class);
* реализация интерфеса [WebApplicationInitializer](#webapplicationinitializer-class).
```java
public class DispatcherServletConfig extends AbstractAnnotationConfigDispatcherServletInitializer {

  @Override
  protected Class<?>[] getRootConfigClasses() {
    return null;        //этот метод не используется
  }
  
  /** Аналог секции <servlet> в web.xml */
  @Override
  protected Class<?>[] getServletConfigClasses() {
    return new Class[] {TemplateEngineConfig.class};    //<param-value>/WEB-INF/applicationContext.xml</param-value>
  }

  /** Аналог секции <servlet-mapping> в web.xml */
  @Override
  protected String[] getServletMappings() {
    return new String[] {"/"};          //<url-pattern>/</url-pattern>
  }
}
```
</details>

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

#### @DeleteMapping-annotation

### @EnableWebMvc-annotation
@EnableWebMvc (org.springframework.web.servlet.config.annotation) - аннотация подключает обработчики аннотаций из библиотеки [spring-webmvc](#spring-webmvc-dependency). 
Использование аннотации аналогично тэгу ```mvc:annotation-driven``` из схемы http://www.springframework.org/schema/mvc.
>
#### @GetMapping-annotation
@GetMapping - связывает метод контроллера с GET-методом. 

#### @PatchMapping-annotation
@PatchMapping - связывает метод контроллера с GET-методом

#### @PostMapping-annotation

#### @PutMapping-annotation

#### @RequestMapping-annotation
@RequestMapping - аннотация, которая связывает метод [контроллера](#controller) с url

Атрибуты:
* method - устанавливает HTTP-метод