## Content

* [spring-aop](#spring-aop-dependency)

* [@EnableAspectJAutoProxy](/java-spring.md#enableaspectjautoproxy-annotation)

### Spring AOP
Spring AOP - фреймворк реализующий парадигму [АОП](/index/AOP.md). Этот фреймворк встроен во [spring-context](../java-spring.md#spring-context-dependency) поэтому идет в Spring из коробки.

Преимущества:
* Более прост в использовании чем [AspectJ](../java/java-AspectJ.md)

Недостатки:
* В отличие от [AspectJ](../java/java-AspectJ.md) предоставляет только самую распространенную и необходимую функциональность.

Для работы Spring AOP нужна зависимости [AspectJ](../java/java-AspectJ.md)

### spring-aop-dependency
spring-aop - зависимость, которая является транзитивной для [spring-context](../java-spring.md#spring-context-dependency)



