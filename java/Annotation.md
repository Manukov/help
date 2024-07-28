
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

```java
import java.lang.annotation.*;

@Documented                                 //обрабатывается javadoc
@Retention(RetentionPolicy.SOURCE)          //доступность
@Target({ElementType.TYPE})                 //целевой объект. 
public @interface CustomAnnotation {
}
```


### Annotation Processor
Annotation Processor (Процессор аннотаций) 
- это отдельная программа, которая на основании аннотаций дописывает код. Например, так работет Lombok.

### ElementType-class
ElementType - это перечисление, которое содержит перечень элементов передаваемых параметрами аннотации [@Target](#target-annotation)
* TYPE - для классов и интерфейсов;
* FIELD
* METHOD
* PARAMETER
* COMSTRUCTOR
* LOCAL_VARIABLE
* ANNOTATION_TYPE
* PACKAGE
* TYPE_PARAMETER (java 8)
* TYPE_USE (java 8)
* MODULE (java 9)


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
RetentionPolicy (политика доступности) - это перечисление, которое содержит перечень элементов для аннотации [@Retentio](#retentionpolicy-class):
* SOURCE - аннотация доступна только в исходном коде (в .java-файлах). В .class-файлы аннотация такого типа не попадает. Примеры SOURCE-аннотаций: @Override, @SuppresWarning; 
* CLASS - аннотация доступна в исходном коде и в байт-коде. На этапе выполнения через Reflection API такая аннотация будет недоступна. CLASS-аннотации используются как правило [анализаторами байткода](/java.md#bytecode-analyzer); 
* RUNTIME - аннотация доступна в исходном коде, в байт-коде, во время выполнения через Reflection API ;

### @Documented-annotation
@Documented - это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации. Эта аннотация используется только javadoc и указывает создавать ли для типа документацию.

### @Retention-annotation
@Retention (доступность) - это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации, которая показывает на каком этапе будет видна/доступна аннотация. Этап указывается через перечисление [RetentionPolicy](#retentionpolicy-class)

### @Target-annotation
@Target- это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации, которая показывает к чему будет применяться аннотация. Типы элементов заданы в перечислении [ElementType](#elementtype-class) 