## Content


* [CDL](#contextualized-dependency-lookup)
* [Contextualized Dependency Lookup](#contextualized-dependency-lookup)
* [Dependency Injection](#dependency-injection)
* [Dependency Lookup](#dependency-lookup)
* [Dependency Pull](#dependency-pull)


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
``` java
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