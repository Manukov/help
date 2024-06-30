## Content

* [Cross-Cutting Concern](/index.md#cross-cutting-concern)
* [org.aspect](#orgaspectj)
* [Сквозная функциональность / Cross-Cutting Concern](/index.md#cross-cutting-concern)


### AspectJ
AspectJ - это [аспектно-ориентированный](/index.md#aop) фреймворк для языка Java


### Advice
Advice — средство оформления кода, которое должно быть вызвано из точки соединения. Совет может быть выполнен до, после или вместо точки соединения.


### Aop Proxy


### Aspect
Aspect — модуль или класс, реализующий сквозную функциональность. Аспект изменяет поведение остального кода, 
применяя совет в точках соединения, определённых некоторым срезом.

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


### introduction
— изменение структуры класса и/или изменение иерархии наследования для добавления функциональности аспекта в инородный код. Обычно реализуется с помощью некоторого метаобъектного протокола (англ. metaobject protocol, MOP).

### Join Point
— точка в выполняемой программе, где следует применить совет. Многие реализации АОП позволяют использовать вызовы методов и обращения к полям объекта в качестве точек соединения.

### PointCut 
— набор точек соединения. Срез определяет, подходит ли данная точка соединения к данному совету. Самые удобные реализации АОП используют для определения срезов синтаксис основного языка (например, в AspectJ применяются Java-сигнатуры) и допускают их повторное использование с помощью переименования и комбинирования.

### org.aspectj
org.aspectj - это groupId зависимостей AspectJ. Библиотеки AspectJ
* [aspectjrt](#aspectjrt) 
* [aspectjweaver](#aspectjweaver)
