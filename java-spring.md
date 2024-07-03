## Content


* [CDL](#contextualized-dependency-lookup)
* [Contextualized Dependency Lookup](#contextualized-dependency-lookup)
* [Dependency Injection](#dependency-injection)
* [Dependency Lookup](#dependency-lookup)
* [Dependency Pull](#dependency-pull)
* [spring-context](#spring-context-dependency)

* [@EnableAspectJAutoProxy](#enableaspectjautoproxy-annotation)


### Spring


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

### spring-beans-dependency

### spring-context-dependency
spring-context - ..... Включает транзитивные зависимости:
* [spring-core](#spring-core-dependency)
* [spring-beans](#spring-beans-dependency)
* [spring-aop](java-spring/java-spring-AOP.md#spring-aop-dependency)

### spring-core-dependency

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