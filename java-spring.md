## Content

* [Application Context](#application-context)
* [Bean](#bean)
* [CDL](#contextualized-dependency-lookup)
* [Contextualized Dependency Lookup](#contextualized-dependency-lookup)
* [Dependency Injection](#dependency-injection)
* [Dependency Lookup](#dependency-lookup)
* [Dependency Pull](#dependency-pull)
* [IoC-контейнер](#application-context)
* [spring-context](#spring-context-dependency)
* [spring-jcl](#spring-jcl-dependency)
* [Контекст приложения / Application Context](#application-context)

* [@EnableAspectJAutoProxy](#enableaspectjautoproxy-annotation)


### Spring

Преимущества Spring Framework:
* при запуске приложения создает все необходимые объекты, устанавливает для них зависимости (на основании описания этой связи), помещает все объекты в [application context](#application-context) и управляет этими объектами. Это позволяет не создавать объекты используя оператор new и не устанавливать зависимости для создаваемых объектов вручную;

Недостатки Spring Framework:
* 

Версии Spring Framework:

| release | year | J2EE |   |
|---------|------|------|---|
| 0.9     | 2003 |      |   |
| 1.0     | 2004 |      |   |
| 2.0     | 2006 |      |   |
| 2.5     | 2007 |      |   |
| 3.0     | 2009 |      |   |
| 3.1     | 2011 |      |   |
| 4.0     | 2013 |      |   |
| 4.2.0   | 2015 |      |   |
| 4.3     | 2016 |      |   |
| 5.0     | 2017 |      |   |
| 6.0     |      |      |   |

Компоненты Spring:
* Spring Boot
* Spring Security

Зависимости:
* spring-core


### Application Context
Application Context (Контекст приложения) - 

### Bean
Bean - объект создаваемый и управляемый [контейнером Spring](#application-context).
* id - уникальный идентификатор бина;
* class - путь к классу (полное имя класса), объект которого создается;



### Contextualized Dependency Lookup
Contextualized Dependency Lookup (Контекстный поиск зависимостей) - 

### Dependency Injection
Dependency Injection (Внедрение зависимостей) - форма [IoC](#ioc) ... может иметь в свою очередь 2 формы:
* Через конструктор
* Через сеттер

### Dependency Lookup
Dependency Lookup (Поиск зависимостей) - форма [IoC](#ioc) ... может иметь в свою очередь 2 формы:
* [Dependency Pull](#dependency-pull)
* [Contextualized Dependency Lookup](#contextualized-dependency-lookup)

### Dependency Pull
Dependency Pull (извлечение зависимостей) - форма, при которой зависимости вытягиваются из реестра по мере необходимости. Пример реализации такого подхода - это поиск через JNDI
```java
public static void main (String[] args) {
    ApplicationContext ctx = new ClassPathApplicationContext("spring/app-context.xml");     //передаем путь к файлу конфигурации
    MessageRender mr = ctx.getBean("render", MessageRender.class);                          //извлекаем бин по имени и типу
    mr.render();
}
```

### IoC
IoC (Инверсия управления) - ....  Понятие IoC может быть разложена на 2 подтипа:
* [Dependency Injection](#dependency-injection)
* [Dependency Lookup](#dependency-lookup)

### spring-aop-dependency

### spring-beans-dependency
spring-beans - это зависимость которая включает фнукциональность создания новых объектов или [бинов](#bean). Эта зависимость включает транзитивные зависимости: [spring-core](#spring-core-dependency), [spring-jcl](#spring-jcl-dependency). 

### spring-context-dependency
spring-context - ..... Включает транзитивные зависимости:
* [spring-aop](#spring-aop-dependency)
* [spring-beans](#spring-beans-dependency)
* [spring-core](#spring-core-dependency)
* [spring-expression](#spring-expression-dependency)
* [spring-jcl](#spring-jcl-dependency)

### spring-core-dependency
spring-core - ... включает транзитивную зависимость [spring-jcl](#spring-jcl-dependency)


### spring-expression-dependency

### spring-jcl-dependency

### @ComponentScan-annotation
@ComponentScan (org.springframework.context.annotation) - аннотация которая указывает Spring-контейнеру на то, какие пакеты нужно сканировать для поиска компонентов/бинов
``` java
class 
```
Зависимость: [spring-context](#spring-context-dependency)

### @Configuration-annotation
@Configuration (org.springframework.context.annotation)
Зависимость: [spring-context](#spring-context-dependency)

### @EnableAspectJAutoProxy-annotation
@EnableAspectJAutoProxy (org.springframework.context.annotation) - позволяет использовать Spring AOP Proxy. Обработчик аннотации создает прокси для класса аннотированного данной аннотацией.
Зависимость: [spring-context](#spring-context-dependency)