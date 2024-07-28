
* [Annotation Processor](#annotation-processor)
* [ElementType](#elementtype-class)
* [Marker Annotation](#marker-annotation)
* [Meta-Annotation](#meta-annotation)
* [Parameter Annotation](#parameter-annotation)
* [Parameterized Annotation](#parameterized-annotation)
* [Repeatable Annotation](#repeatable-annotation)
* [RetentionPolicy](#retentionpolicy-class)
* [value](#value)
* [Аннотация-маркер / Marker Annotation](#marker-annotation)
* [Аннотация без параметров / Marker Annotation](#marker-annotation)
* [Параметр аннотации/Parameter Annotation](#parameter-annotation)
* [Параметризованные аннотации / Parameterized Annotation](#parameterized-annotation)
* [повторяющиеся аннотации / Repeatable Annotation](#repeatable-annotation)
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
* для объявления аннотации используется ключевое слово "@interface". под капотом [JVM](/java.md#jvm) преобразует свойства аннотацию в методы интерфейса, а саму аннотацию в реализацию этого интерфейса; 
* аннотации могут иметь:
  * обязательные элементы - свойства не имеющие значений по умолчанию;
  * необязательные элементы - свойства имеющие значение по умолчанию. В качестве дефолтного значения может использоваться только константное НЕ null-значение;
  * константы - все константы, так же как в интерфейсах неявно public, static, final;
* свойства аннотаций неявно public и abstract, поэтому для свойств аннотации нельзя применить модификаторы private, final (конфликтует с неявным abstract)
* для свойства [value](#value) не обязательно указывать ключ, можно передавать только значение

Виды аннотаций:
* [мета-аннотации](#meta-annotation);
* [аннотации с параметрами](#parameterized-annotation) и аннотации без параметров или [маркетрные аннотации](#marker-annotation)
* [повторяющиеся аннотации](#repeatable-annotation) и неповторяющиеся

```java
import java.lang.annotation.*;

@Documented                                 //тип аннотированный @CustomAnnotation попадет в javadoc
@Inherited                                  //наследники типа аннотированного @CustomAnnotation унаследуют @CustomAnnotation
@Retention(RetentionPolicy.SOURCE)          //доступность @CustomAnnotation только в source-файлах
@Target({ElementType.TYPE})                 //целевой объект - класс или интерфейс. Если не указано то можно применить к любому элементу 
public @interface CustomAnnotation {
    int MIN = 1;                             //константа
    String name();                          //обязательный элемент
    boolean load() default false;           //необязательный элемент
    
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
Marker Annotation (маркерные аннотации) - это аннотация, которая содержит только объявление и не содержит атрибутов. При использовании маркерных аннотаций можно опускать круглые скобки после названия.
```java
@MarkerAnnoatation      //использование маркетной аннотации без скобок
class CustomClass {}

@MarkerAnnoatation()      //использование маркетной аннотации со скобками
class CustomClass {}
```

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

### Repeatable
RepeatableAnnotation (повторяющаяся аннотация) - это аннотация которая может быть применена к програмномиу элементу более одного раза. Для того чтобы аннотация была повторяющейся:
* при объявлении эта аннотация должна аннотироваться [@Repeatable](#repeatable-annotation)
* должен быть дополнительно объявлен контейнер для аннотаций

```java
import java.lang.annotation.Repeatable;

@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE})
@Repeatable(Container.class)     //указываем что оаннотация повторяющаяся и тип который служит контейнером
public @interface CustomAnnotation {
  String value();

  String name();
}

public @interface Container {
  CustomAnnotation[] value();   
}

```

### RetentionPolicy-class
RetentionPolicy (политика доступности) - это перечисление, которое содержит перечень элементов для аннотации [@Retention](#retentionpolicy-class):
* SOURCE - аннотация доступна только в исходном коде (в .java-файлах). В .class-файлы аннотация такого типа не попадает. Примеры SOURCE-аннотаций: @Override, @SuppresWarning; 
* CLASS - аннотация доступна в исходном коде и в байт-коде. На этапе выполнения через Reflection API такая аннотация будет недоступна. CLASS-аннотации используются как правило [анализаторами байткода](/java.md#bytecode-analyzer); 
* RUNTIME - аннотация доступна в исходном коде, в байт-коде, во время выполнения через Reflection API ;


### value
value - это специальное зарезервированное слово, которое позволяет для одного параметра не указывать имя параметра. Но если параметров более одного, то имя параметра "value" необходимо указывать.

### @Documented-annotation
@Documented - это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации. Эта аннотация используется только javadoc и указывает что тип который аннотирован @Documented попадет в javadoc.

### @Inherited-annotation
@Inherited - это [мета-аннотация](#meta-annotation) которая указывает, что аннотация будет наследоваться потомками.

### @Repeatable-annotation
@Repeatable - это [мета-аннотация](#meta-annotation) которая применяется к [повторяющейся аннотации](#repeatable)

### @Retention-annotation
@Retention (доступность или время жизни) - это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации, которая показывает на каком этапе будет видна/доступна аннотация. Этап указывается через перечисление [RetentionPolicy](#retentionpolicy-class)

### @Target-annotation
@Target- это [мета-аннотация](#meta-annotation) используемая при объявлении аннотации, которая показывает к чему будет применяться аннотация. Типы элементов заданы в перечислении [ElementType](#elementtype-class). Если для аннотации не указывать тип, то она может быть применена к любому програмному элементу. 