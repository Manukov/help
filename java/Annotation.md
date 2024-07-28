
* [Annotation Processor](#annotation-processor)
* [ElementType](#elementtype-class)
* [Marker Annotation](#marker-annotation)
* [Meta-Annotation](#meta-annotation)
* [Parameter Annotation](#parameter-annotation)
* [Parameterized Annotation](#parameterized-annotation)
* [RetentionPolicy](#retentionpolicy-class)
* [value](#value)
* [Аннотация-маркер / Marker Annotation](#marker-annotation)
* [Аннотация без параметров / Marker Annotation](#marker-annotation)
* [Параметр аннотации/Parameter Annotation](#parameter-annotation)
* [Параметризованные аннотации / Parameterized Annotation](#parameterized-annotation)
* [Процессор аннотауий / Annotation Processor](#annotation-processor)

### Annotation
Annotation (Аннотация) - это форма [метаданных](/index.md#metadata) которые представляют информацию об элементе программы. Характеристики аннотаций:
* хранятся внутри кода, но напрямую на код не влияют. Для того чтобы аннотации влияли на код нужен обработчик. в Spring Framework аннотации как правило обрабатывают аспекты;
* аннотации используются:
  * компилятором 
  * средой разработки - это аннотации которые не влияют на код, но подсказывает среде разработчики об намерениях, например: @Nullable, @NotNull, @Comtract. На основании этих аннотаций среда разработки может выдавать дополнительные warning и каждая среда разработки имеет свои настройки и свои аннотации;
  * [процессором аннотаций](#annotation-processor); 
  * [анализаторами байткода](/java.md#bytecode-analyzer) - программа, которая берет скомпилированный байт-код и что-то с ним делает;
  * runtime - в процессе выполнения обработчик аннотации преобразовывает данные
* для объявления аннотации используется ключевое слово "@interface"

Виды аннотаций:
* [мета-аннотации](#meta-annotation);
* [маркетрные аннотации](#marker-annotation)
* [аннотации с параметрами](#parameterized-annotation)



```java
import java.lang.annotation.*;

@Documented                                 //обрабатывается javadoc
@Retention(RetentionPolicy.SOURCE)          //доступность
@Target({ElementType.TYPE})                 //целевой объект. 
public @interface CustomAnnotation {
    
    String name();                          //свойство не имеет значения п оумолчанию
    boolean load() default false;           //свойство имеет значенмие по умолчанию
    
}
```


### Annotation Processor
Annotation Processor (Процессор аннотаций) 
- это отдельная программа, которая на основании аннотаций дописывает код. Например, так работет Lombok.

### ElementType-class
ElementType - это перечисление, которое содержит перечень элементов передаваемых параметрами аннотации [@Target](#target-annotation) и указывающими к чему может быть применена аннотация:
* TYPE - аннотация устанавливается над классо и интерфейсов;
* FIELD - поле класса
* METHOD - метод
* PARAMETER - параметру метода
* COMSTRUCTOR - конструктору
* LOCAL_VARIABLE - локальная переменная
* ANNOTATION_TYPE - аннотация
* PACKAGE - пакет
* TYPE_PARAMETER (java 8) - параметр типа. Используеться в generic
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


#### Parameter Annotation
Parameter Annotation (Параметр аннотации) - .... Параметрами аннотации могут быть:
* примитивные типы
* Srting
* Class, Class<? extends XYZ>
* Enum - например, [ElementType](#elementtype-class), [RetentionPolicy](#retentionpolicy-class)
* аннотация (без циклических зависимостией)
* Одномерный массив чего-то вышеперечисленного - например, [@Target](#target-annotation) принимает параметром массив [ElementType](#elementtype-class)

### Parameterized Annotation
Parameterized Annotation (параметризованные аннотации) - это аннотация, которая может принимать один или несколько [параметров](#parameter-annotation). Если у аннотации один параметр, то он указывается в скобках, а если у аннотации несколько параметров, то необходимо указывать имя параметра и его значение.

### RetentionPolicy-class
RetentionPolicy (политика доступности) - это перечисление, которое содержит перечень элементов для аннотации [@Retentio](#retentionpolicy-class):
* SOURCE - аннотация доступна только в исходном коде (в .java-файлах). В .class-файлы аннотация такого типа не попадает. Примеры SOURCE-аннотаций: @Override, @SuppresWarning; 
* CLASS - аннотация доступна в исходном коде и в байт-коде. На этапе выполнения через Reflection API такая аннотация будет недоступна. CLASS-аннотации используются как правило [анализаторами байткода](/java.md#bytecode-analyzer); 
* RUNTIME - аннотация доступна в исходном коде, в байт-коде, во время выполнения через Reflection API ;


### value
value - это специальное зарезервированное слово, которое позволяет для одного параметра не указывать имя параметра. Но если параметров более одного, то имя параметра "value" необходимо указывать.

### @Documented-annotation
@Documented - это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации. Эта аннотация используется только javadoc и указывает что тип который аннотирован @Documented попадет в javadoc.


### @Inherited-annotation
@Inherited - это [мета-аннотация](#meta-annotation) которая указывает, что аннотация наследуется потомками.

### @Retention-annotation
@Retention (доступность) - это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации, которая показывает на каком этапе будет видна/доступна аннотация. Этап указывается через перечисление [RetentionPolicy](#retentionpolicy-class)

### @Target-annotation
@Target- это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации, которая показывает к чему будет применяться аннотация. Типы элементов заданы в перечислении [ElementType](#elementtype-class) 