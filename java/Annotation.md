
* [Annotation Processor](#annotation-processor)
* [ElementType](#elementtype-class)
* [Marker Annotation](#marker-annotation)
* [Meta-Annotation](#meta-annotation)
* [Parameterized Annotation](#parameterized-annotation)
* [RetentionPolicy](#retentionpolicy-class)
* [Аннотация-маркер / Marker Annotation](#marker-annotation)
* [Аннотация без параметров / Marker Annotation](#marker-annotation)
* [Параметризованные аннотации / Parameterized Annotation](#parameterized-annotation)
* [Процессор аннотауий / Annotation Processor](#annotation-processor)

### Annotation
Annotation (Аннотация) - это форма [метаданных](/index.md#metadata) которые представляют информацию об элементе программы. Аннотации используются:
* компилятором 
* средой разработки - это аннотации которые не влияют на код, но подсказывает среде разработчики об намерениях, например: @Nullable, @NotNull, @Comtract. На основании этих аннотаций среда разработки может выдавать дополнительные warning и каждая среда разработки имеет свои настройки и свои аннотации;
* [процессором аннотаций](#annotation-processor) 
* анализаторами байткода - программа которая берет скомпилированный байт-код и что-то с ним делает
* runtime

Виды аннотаций:
* [meta-Annotation](#meta-annotation);
* аннотации для типов;
* аннотации для кода
* нативные аннотации


Для объявления аннотации переиспользовали ключ. слово interface 


<details><summary>Объявление аннотации</summary>

1. Аннотация объявляется с помощью ключевого слова "@interface"
2. Атрибуты аннотации задаются так же как и методы интерфейса

```java
public @interface CustomAnnotation {
    String name() default "";
    int value();
}
```
</details>

### Annotation Processor
Annotation Processor (Процессор аннотаций) 
- это отдельная программа, которая на основании аннотаций дописывает код. Например, так работет Lombok.

### ElementType-class
ElementType - это перечисление, которое содержит перечень элементов для аннотации [@Target](#target-annotation)

### Marker Annotation
Marker Annotation (маркерные аннотации) - это аннотация, которая содержит только объявление и не содержит атрибутов.

### Meta-Annotation
Meta-Annotation (мата-аннотация) - это аннотация, которая может быть применена к другой аннотации.

Основные мета-аннотации (находяться в пакете java.lang.annotation):
* [@Target](#target-annotation): указывает контекст, для которого применима аннотация
* [@Retention](#retention-annotation): указывает, до какого шага во время компиляции аннотация будет доступна
* @Documented: указывает, что аннотация должна быть задокументирована с помощью javadoc
* @Inherited: позволяет реализовать наследование аннотаций родительского класса классом-наследником
* @Repeatable: указывает, что аннотация может быть использована повторно в том же месте

### Parameterized Annotation
Parameterized Annotation (параметризованные аннотации) - это аннотация, которая может принимать один или несколько параметров. Если у аннотации один параметр, то он указывается в скобках, а если у аннотации несколько параметров, то необходимо указывать имя параметра и его значение.

### RetentionPolicy-class
RetentionPolicy - это перечисление, которое содержит перечень элементов для аннотации [@Retentio](#retentionpolicy-class)

### @Documented-annotation
@Documented - это [мета-аннотация](#meta-annotation),

### @Retention-annotation
@Retention - это [мета-аннотация](#meta-annotation), которая показывает на каком этапе будет видна/доступна аннотация. Этап указывается через перечисление [RetentionPolicy](#retentionpolicy-class)

### @Target-annotation
@Target- это [мета-аннотация](#meta-annotation), которая показывает к чему будет применяться аннотация. Типы элементов заданы в перечислении [ElementType](#elementtype-class) 