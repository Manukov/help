## Content

* [Annotation-based Configuration](#annotation-based-configuration)
* [Application Context](#application-context)
* [Bean](#bean)
* [BeanFactory](#beanfactory-class)
* [CDL](#contextualized-dependency-lookup)
* [ClassPathXmlApplicationContext](#classpathxmlapplicationcontext-class)
* [Configuration](#configuration)
* [Contextualized Dependency Lookup](#contextualized-dependency-lookup)
* [Dependency Injection](#dependency-injection)
* [Dependency Lookup](#dependency-lookup)
* [Dependency Pull](#dependency-pull)
* [IoC-контейнер](#application-context)
* [Java-based Configuration](#java-based-configuration)
* [spring-context](#spring-context-dependency)
* [spring-jcl](#spring-jcl-dependency)
* [XML-based Configuration](#xml-based-configuration)
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


### Annotation-based Configuration

### Application Context
Application Context (Контекст приложения) - ... Для работы с контейнером Spring достаточно зависимости [spring-context](#spring-context-dependency), которая транзитивно подтянет все остальные.

### ApplicationContext
ApplicationContext (org.springframework.context) - это [интерфейс](java/Interface.md), который описывает  

### Bean
Bean - объект создаваемый и управляемым [контейнером Spring](#application-context).
* id - уникальный идентификатор бина;
* class - путь к классу (полное имя класса), объект которого создается;


### BeanFactory-class
BeanFactory (org.springframework.beans.factory) - это интерфейс 

### ClassPathXmlApplicationContext-class
ClassPathXmlApplicationContext (org.springframework.context.support)
<details> <summary>Конструкторы</summary>

``` java
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");  //applicationContext.xml" - xml-консигурация бинов
//... вызов бинов из контекста
context.close();               //закрываем контекст
```
</details>

<details> <summary>Методы</summary>

* void close(); - закрываем контекст. Контекст приложения должен быть закрыт всегда
</details>

### Configuration
* [XML-based Configuration](#xml-based-configuration)
* [Java-based Configuration](#java-based-configuration)
* [Annotation-based Configuration](#annotation-based-configuration)

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

### Java-based Configuration

### spring-aop-dependency

### spring-beans-dependency
- это зависимость, которая включает функциональность создания новых объектов или [бинов](#bean). Эта зависимость включает транзитивные зависимости: [spring-core](#spring-core-dependency), [spring-jcl](#spring-jcl-dependency). 

### spring-context-dependency
- это зависимость, в которой находятся различные имплементации [контейнеров Spring](#application-context). Эта зависимость включает транзитивные зависимости:
* [spring-aop](#spring-aop-dependency)
* [spring-beans](#spring-beans-dependency)
* [spring-core](#spring-core-dependency)
* [spring-expression](#spring-expression-dependency)
* [spring-jcl](#spring-jcl-dependency)

### spring-core-dependency
spring-core - ... включает транзитивную зависимость [spring-jcl](#spring-jcl-dependency)


### spring-expression-dependency

### spring-jcl-dependency


### XML-based Configuration

### @ComponentScan-annotation
@ComponentScan (org.springframework.context.annotation) - это аннотация, которая указывает Spring-контейнеру на то, какие пакеты нужно сканировать для поиска компонентов/бинов
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