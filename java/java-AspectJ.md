## Content

* [aspectjweaver](#aspectjweaver)
* [Cross-Cutting Concern](/index.md#cross-cutting-concern)
* [org.aspect](#orgaspectj)
* [Сквозная функциональность / Cross-Cutting Concern](/index.md#cross-cutting-concern)

* [@EnableAspectJAutoProxy](/java-spring.md#enableaspectjautoproxy-annotation)

### AspectJ
AspectJ - это [аспектно-ориентированный](/index/AOP.md#aop) расширение для языка Java (фреймворк). 

Преимущества:
* В отличие от [Spring AOP](../java-spring/java-spring-AOP.md) предоставляет всю функциональность.

Недостатки:
* Более сложен в использовании чем [Spring AOP](../java-spring/java-spring-AOP.md)

Этот фреймворк стал де-факто стандартов АОП в Java и предоставляет
всю функциональность АОП, в отличие от Spring AOP который предоставляет только самую распространенную и необходимую функциональность.


### Advice
Advice - это метод в аспект-классе и который определяет что должно произойти. В зависимости от типа [advice](/index/AOP.md#advice) этот метод может быть аннотирован:
* [@Before](#before-annotation)

 [content](#content) [advice](/index/AOP.md#advice)

### Aop Proxy

### aspectjrt
aspectjrt (AspectJ Runtime) - 

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjrt</artifactId>
    <version>${aspect.version}</version>
</dependency>
```

### aspectjweaver
```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>${aspect.version}</version>
</dependency>
```

### introduction
— изменение структуры класса и/или изменение иерархии наследования для добавления функциональности аспекта в инородный код. Обычно реализуется с помощью некоторого метаобъектного протокола (англ. metaobject protocol, MOP).

### Join Point
— точка в выполняемой программе, где следует применить совет. Многие реализации АОП позволяют использовать вызовы методов и обращения к полям объекта в качестве точек соединения.

### PointCut 
— набор точек соединения. Срез определяет, подходит ли данная точка соединения к данному совету. Самые удобные реализации АОП используют для определения срезов синтаксис основного языка (например, в AspectJ применяются Java-сигнатуры) и допускают их повторное использование с помощью переименования и комбинирования.

### org.aspectj
org.aspectj - это groupId зависимостей AspectJ. Библиотеки AspectJ
* [aspectjrt](#aspectjrt) 
* [aspectjweaver](#aspectjweaver):
  * [@Aspect](#aspect-annotation)
  * [@Before](#before-annotation)


### @Aspect-annotation
@Aspect (org.aspectj.lang.annotation) - аннотация применяется к классу который является [Аспектом](/index/AOP.md#aspect).
```java
/**Т.к. класс аннотирован @Aspect, то для него будет создан AOP-прокси*/
@Component
@Aspect     //Указываем что этот класс является аспектом 
public class Aspect {
    //advice A ...
    //advice B ...
}
```
Зависимость: [aspectjweaver](#aspectjweaver)

### @Before-annotation
@Before (org.aspectj.lang.annotation) - это аннотация которой аннотируется advice-метод типа Before (должен отработать до вызова метода с бизнес-логикой)
```java
/** advice-метод beforeAdvice() - типа Before должен вызываться перед вызовом метод указанного в pointcut
 * "execution(public void execCode())" - это pointcut 
 * Поскольку в pointcut не указан класс, то этот шаблон подойдет для метода в любом классе, который совпадет по сигнатуре*/
@Component
@Aspect                
public class Aspect {
    //перед вызовом метода public void execCode() выполнить метод beforeAdvice()
    @Before("execution(public void execCode())")   //Advice типа Before                  
    public void beforeAdvice() {  
        //код сквозной функциональности
    }
}
```
Зависимость: [aspectjweaver](#aspectjweaver)