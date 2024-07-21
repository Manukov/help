## Content

* [Annotation-based Configuration](#annotation-based-configuration)
* [Application Context](#application-context)
* [Autowiring](#autowiring)
* [Bean](#bean)
* [Bean Ambiguity](#bean-ambiguity)
* [BeanLifecycle](#beanlifecycle)
* [BeanFactory](#beanfactory-class)
* [CDL](#contextualized-dependency-lookup)
* [ClassPathXmlApplicationContext](#classpathxmlapplicationcontext-class)
* [Component Scan](#component-scan)
* [Configuration](#configuration)
* [Contextualized Dependency Lookup](#contextualized-dependency-lookup)
* [Dependency Injection](#dependency-injection)
* [Dependency Lookup](#dependency-lookup)
* [Dependency Pull](#dependency-pull)
* [destroy-method](#destroy-method)
* [factory-method](#factory-method)
* [init-method](#init-method)
* [IoC-контейнер](#application-context)
* [Java-based Configuration](#java-based-configuration)
* [Scope](#scope)
* [spring-context](#spring-context-dependency)
* [spring-jcl](#spring-jcl-dependency)
* [XML-based Configuration](#xml-based-configuration)
* [Контекст приложения / Application Context](#application-context)
* [Неоднозначность бинов / Bean Ambiguity](#bean-ambiguity)
* [Сканирование компонентов / Component Scan](#component-scan)

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
Annotation-based Configuration - описание бинов и их зависимостей производиться при помощи аннотаций [@Component](#component-annotation), [@Bean](#bean-annotation) и незначительная часть настраивается в xml-файле. 
Spring сканирует конфигурационные классы - классы аннотированные [@Configuration](#configuration-annotation) и в этих классах: 
1. Считывает все методы аннотированные [@Bean](#bean-annotation) и создает бины для всех таких методов
2. Считывает путь указанный в [@ComponentScan](#componentscan-annotation) и в этом пакете создает бины для классов аннотированных [@Component](#component-annotation)

Преимущества:
* Короче и удобнее чем [xml-конфигурация](#xml-based-configuration)
* Код становится более читабельным

### Application Context
Application Context (Контекст приложения) - ... Для работы с контейнером Spring достаточно зависимости [spring-context](#spring-context-dependency), которая транзитивно подтянет все остальные.

### ApplicationContext
ApplicationContext (org.springframework.context) - это [интерфейс](java/Interface.md), который описывает  

### Autowiring
Autowiring - автоматизация внедрения зависимостей. Spring сам предугадывает тип и сам внедряет зависимость.

### Bean
Bean - объект создаваемый и управляемым [контейнером Spring](#application-context).
* id - уникальный идентификатор бина. Если не указывается явно, то используется имя класса с маленькой буквы
* class - путь к классу (полное имя класса), объект которого создается;
* [scope](#scope) - область видимости бинов;
* [factory-method](#factory-method) - указываем статический фабричный метод создания объекта, если создание объектов не производиться через конструктор
* [init-method](#init-method) - это метод который вызывается для инициализации бина, в нем производится инициализация ресурсов, обращение к внешним файлам, запуск БД и пр.
* [destroy-method](#destroy-method) - это метод который вызывается при завершении работы приложения. в нем производится закрытие потоков ввода-вывода, закрытие доступа к БД


### Bean Ambiguity
Bean Ambiguity (Неоднозначность бинов) - это ситуацию когда существет несколько бинов одного и того же типа и Spring Framework не может однозначно определить, какой бин использовать при внедрении зависимостей. В такой ситуации Spring Framewor бросает исключение NoUniqueBeanDefinitionException. Для решения проблемы неоднозначности бинов существует несколько сценариев:
* Использование @Qualifier:
* Использование @Primary:
* Использование [XML-конфигурации](#xml-based-configuration):


### BeanFactory-class
BeanFactory (org.springframework.beans.factory) - это интерфейс 

### BeanLifecycle
BeanLifecycle (жизненный цикл бина) - ...
* Старт приложения
* Запускается [application context](#application-context)
* Spring Framework читает конфигурационный файл и создаются бины объявленные в конфигурационном xml-файле либо объявленные в конфигурационном классе 
* В бин внедряются зависимости - происходит [dependency injection](index.md#dependency-injection)
* Вызывается init-method (создается в классе бина) - в этом методе запускается инициализация бина.
* Бин готов к использованию
* вызывается destriy-method(создается в классе бина) - метод вызывается при завершении работы приложения
* Остановка приложения

### ClassPathXmlApplicationContext-class
ClassPathXmlApplicationContext (org.springframework.context.support) - это имплементация application context для [работы с xml-файлом конфигурации](#xml-based-configuration).
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


### Component Scan
Component Scan (сканирование компонентов) - поиск классов для которых будут созданы бины. 

```xml
<beas>
    <!-- сканирует все классы в пакете by.manukov. Для всех классов в этом пакете аннотированных @Component будут созданы бины -->
    <context:component-scan base-package="by.manukov"/>
</beas>
```



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

Используя DI можно внедрять:
* простые значения, как константы, так и значения из внешнего файла
* ссылки на другие бины

<details> <summary>Dependency injection через конструктор (xml-кронфигурация)</summary>

```java
public class BeanB {  }     

public class BeanA {
    private final BeanB b;                  //поле может быть final
    public BeanA(BeanB b) { this.b=b; }     //класс ждет зависимость через конструктор
}
```
```xml
<beas>
    <bean id="beanB" class="by.sandbox.BeanB"/>  <!-- бин самой зависимости -->
    
    <bean id="beanA" class="by.sandbox.beanA">
        <constructor-arg ref="beanB"/>           <!-- Указываем id бина. ref - это ссылка на другой объект-->
    </bean>
</beas>
```
</details>
<details> <summary>Dependency injection через setter (xml-конфигурация)</summary>

Spring Framework при внедрении зависимостей через setter в объект класса А:
* создает бин зависимости;
* создает объект типа А в который будет внедряться зависимость - у объекта А обязательно должен быть конструктор без параметров;
* находит у объекта A соответствующий setter. Для поиска берется имя свойства, первая буква переводиться в upperCase и к полученному результату добавляется префикс set. Т. е. для если ``` <property name="bean" ref="testBean"/> ```, то setter должен быть ```setBean```;
* у объекта А вызываем метод set.. и передает туда аргументом объект уже созданной зависимости

```java
public class A {  }     

public class A {
    private BeanB b;                            //поле не может быть final
    public void setB(BeanB b) { this.b=b; }     //класс ждет зависимость через setter
}
```
```xml
<beas>
    <bean id="beanB" class="by.sandbox.BeanB"/>     <!-- бин самой зависимости -->
    
    <bean id="a" class="by.sandbox.A">
        <property name="bean" red="beanB"/>            <!-- в setter setBean передаем объект с id = beanB -->
    </bean>
</beas>
```

</details>

[content](#content) [index](index.md#dependency-injection)






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
### destroy-method
Destroy-method - это метод, который объявляется в классе бина и вызывается при завершении работы приложения для бинов со scope singleton. Destroy-method:
* может иметь любой модификатор - public, private, protected; 
* может иметь любой тип возвращаемого значения, но чаще всего используется void, поскольку нет возможности получить возвращаемое значение, так как этот метод вызывается Spring 
* не должен иметь параметров


### factory-method
factory-method - это имплементация паттерна "Фабричный метод". Метод создает объекты не напрямую, используя конструктор, а через вызов специального статического фабричного метода, который и использует new.

### init-method
Init-method - это метод, который объявляется в классе бина и вызывается в жизненном цикле бина после того как в бин заинжектились зависимости. Init-method:
* может иметь любой модификатор - public, private, protected;
* может иметь любой тип возвращаемого значения, но чаще всего используется void, поскольку нет возможности получить возвращаемое значение, так как этот метод вызывается Spring
* не должен иметь параметров

### IoC
IoC (Инверсия управления) - ....  Понятие IoC может быть разложена на 2 подтипа:
* [Dependency Injection](#dependency-injection)
* [Dependency Lookup](#dependency-lookup)

### Java-based Configuration
- вся настройка бинов производиться в java-коде

### Scope
Scope (область видимости) - определяет, как Spring Framework будет создавать бины.
* Singleton (по умолчанию) - при всех вызовах getBean() возвращается [ссылка](java.md#reference) на один и тот же [объект](java.md#object). При этом scope возможна ситуация, когда 2 и более бинов имеют зависимостью один и тот же объект в памяти и ситуация, когда 2 переменные ссылаются на один и тот же объект. Этот scope используется в том случае, когда бин является [stateless](index.md#stateless). Если у singleton-бина изменять состояние, то столкнемся с проблемой.
* prototype - при каждом вызове getBean() контейнер создает новый объект. Этот scope используется в том случае, когда бин является [statefull](index.md#stateful). Для бинов этого scope Spring не вызывает [destroy-method](#destroy-method) поскольку Spring не управляет такими бинами, а только создает бин и отдает его клиенту
* request
* session
* global-session

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

### UnsatisfiedDependencyException-class
UnsatisfiedDependencyException - исключение которое выбрасывает Spring Framework при невозможности внедрить зависимость в бин. Это исключение бросается в 2-х случаях:
* NoSuchBeanDefinitionException - когда подходящего бина нет
* NoUniqueBeanDefinitionException- когда есть несколько бинов и возникает проблема [неоднозначности бинов](#bean-ambiguity)

### XML-based Configuration
XML-based Configuration (XML-конфигурация) - описание бинов и их зависимостей храниться в xml-файле. 
При работе с XML-конфигурацией используется [ClassPathXmlApplicationContext](#classpathxmlapplicationcontext-class)

Преимущества:
* позволяет настраивать бины без перекомпиляции приложения;

### @Autowired-annotation
@Autowired - делигирует фреймворку Spring поиск бина для зависимости и автоматическое внедрение этой зависимости. Аннотация подбирает подходящие бины по типу (класс или интерфейс)
1. Spring сканирует все классы с аннотацией @Component и создает баны для этих классов
2. Spring сканирует все созданные бины и проверяет, подходит ли хотя бы один бин в качестве зависимости там, где установлена аннотация @Autowired
3. Если находиться хотя бы один бин, то он вредряется в качестве зависимости
4. Если не находиться ни одного бина - ошибка
5. Если находиться более одного бина - неоднозначность

@Autowired можно испоьзовать на:
* полях - внедояет зависимост ьдаже в private-поле если нет конструктора или сетеера. Это реализуется при помощи Reflection API
* сеттерах 
* конструкторах

### @Bean-annotation

#### @Component-annotation
@Component (org.springframework.stereotype) - это аннотация, которая указывает Spring для каких классов создавать бины. В качестве атрибута value аннотация принимает строковое представление id бина, если атрибут value не используется, то в качестве id бина будет использоваться название класса с маленькой буквы. Аннотация применяется только к классу, а не к интефрейсу

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

### @Qualifier-annotation
@Qualifier (Уточнитель) - аннотация используется совместно с аннотацией [@Autowired](#autowired-annotation) для решения проблемы [неоднозначности бинов](#bean-ambiguity). Аттрибуты:
* String value - id бина который нужно внедрить

```java
/** При использовании аннотации @Qualifier с конструктором, необходимо указывать аннотацию перед аргументами конструктора */
@Autowired
publuc MusicPlayer(@Qualifier("rockMusic") Music music1, @Qualifier("classicalMusic") Music music2) {
    this.music1=music1;
    this.music2=music2;
}

@Autowired
@Qualifier("rockMusic")
public void setMusic(Music music) {
    this.music=music;
}

```