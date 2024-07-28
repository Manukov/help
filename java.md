## Content

* [Access modifier](#access-modifier)
* [Annotation](#annotation)
* [Annotation Processor](java/Annotation.md#annotation)
* [artifact](#artifact)
* [Bytecode Analyzer](#bytecode-analyzer)
* [Class](java/Class.md)
* [Class](#class-class)
* [Classpath](#classpath)
* [Deployment descriptor](#deployment-descriptor)
* [ear](#ear)
* [Interface](java/Interface.md)
* [jar](#jar)
* [javaagent](#javaagent)
* [Keywords](#keywords)
* [MANIFEST.FM](#manifest-fm)
* [Meta-Annotation](java/Annotation.md#meta-annotation)
* [META-INF](#meta-inf)
* [Object](#object)
* [Object](#object-class)
* [Non-Primitive Data Types](#reference-data-type)
* [Primitive Data Types](#primitive-data-types)
* [Reference](#reference)
* [Reference Data Type](#reference-data-type)
* [Resources Root](#resources-root)
* [Service Provider Interface](#spi)
* [Setter](#setter)
* [SPI](#spi)
* [String](java/String.md)
* [war](#war)
* [WEB-INF](#web-inf)
* [web.xml](#web-xml)
* [webapp](#webapp)
* [Анализатор байткода/Bytecode Analyzer](#bytecode-analyzer)
* [Дескриптор развертывания / Deployment descriptor](#deployment-descriptor)
* [Модификатор доступа / Access modifier](#access-modifier)
* [Ссылка / Reference](#reference)


### Access modifier
Access modifier (Модификатор доступа) 

### Annotation
Annotation (аннотации) - это специальный тип комментариев в коде с помощью которых:
* можно передавать инструкции компилятору
* можно передавать инструкции анализатору исходного кода
* передавать метаданые, которые могут быть использованы Java-приложением с помощью рефлексии

### artifact
Artifact (артефакт) - это файл [jar-архив](#jar) или [war-архив](#war) в который упаковано приложение.

### Base Class
Base Class (Базовый класс) -

### Bytecode Analyzer

### Class-class
Class<T> (java.lang) - объект этого класса содержит информацию о типе (класс, интерфейс) и используется там, где нужно передать информацию о типе. Способы получения объекта типа Class<>:
* .class - вызов метода .class на типе, используется в случае когда объект этого класса еще не создан. Вызов эквивалентен вызову getClass() на объекте;
* getClass() - вызов метода getClass() на объекте, используется в случае когда объект этого класса уже создан. Вызов эквивалентен вызову .class на типе;

```java
public static void main (String[] args) {
    Class<?> clazz = String.class;                  //сведения о типе для типа (объект не создан)
    Class<?> clazz = new String().getClass();       //сведения о типе для объекта (объект создан)
}
```

### Classpath
Classpath – это [переменная окружения](index.md#environment-variable), которая сообщает JVM, где искать пользовательские и системные классы. Это может быть путь к директории, где хранятся скомпилированные классы, или путь к jar-файлам.

### Data Type
* [Primitive Data Types](#primitive-data-types)
* [Reference Data Type](#reference-data-type)


### deployment descriptor
Deployment descriptor (дескриптор развертывания) - это конфигурационный файл, который указывает "инструментам развертывания" развернуть приложение или модуль с определенными параметрами контейнера, настройками безопасности и описывает требования к конфигурации. Виды дескрпторов развертывания:
* [web.xml](#web-xml) - это дескриптор развертывания для веб-приложения который должен находиться в каталоге [WEB-INF](#web-inf) в корне веб-приложения;
* application.xml - это дескриптор развертывания для Java EE приложения и который должен находиться в каталоге [META-INF](#meta-inf) на верхнем уровне файла [.ear](#ear) приложения


### ear

### jar

### javaagent

### JVM

### Keywords
* [abstract](#abstract-keyword)
* [assert](#assert-keyword)
* [break](#break-keyword)
* [byte](#byte-keyword)
* [case](#case-keyword)
* [catch](#catch-keyword)
* [class](#class-keyword)
* [const](#const-keyword)
* [continue](#continue-keyword)
* [default](#default-keyword)
* [do](#do-keyword)
* [double](#double-keyword)
* [else](#else-keyword)
* [enum](#enum-keyword)
* [extends](#extends-keyword)
* [final](#final-keyword)
* [finally](#finally-keyword)
* [for](#for-keyword)
* [goto](#goto-keyword)
* [if](#if-keyword)
* [implements](#implements-keyword)
* [import](#import-keyword)
* [int](#int-keyword)
* [instanceof](#instanceof-keyword)
* [interface](#interface-keyword)
* [long](#long-keyword)
* [native](#native-keyword)
* [new](#new-keyword)
* [package](#package-keyword)
* [private](#private-keyword)
* [protected](#protected-keyword)
* [public](#public-keyword)
* [return](#return-keyword)
* [static](#static-keyword)
* [strictfp](#strictfp-keyword)
* [super](#super-keyword)
* [switch](#switch-keyword)
* [synchronized](#synchronized-keyword)
* [this](#this-keyword)
* [throw](#throw-keyword)
* [throws](#throws-keyword)
* [transient](#transient-keyword)
* [try](#try-keyword)
* [void](#void-keyword)
* [volatile](#volatile-keyword)
* [while](#while-keyword)


### MANIFEST-FM

### META-INF

### Object

### Object-class

### Primitive Data Types
- примитивные типы данных

### Reference

### Reference Data Type
Reference Data Type (ссылочные типы данных) - ....
* Arrays
* Class
* Interface
* Enumeration
* Annotation

### Resources Root
Resources Root - директория с ресурсами приложения, по умолчанию называемая "resources". Все файлы, помещенные в эту директорию буду доступны в java-классах

### Setter
Setter - это специальный метод который используется для присвоения значений полям класса, не нарушая инкапсуляцию

### Sources Root
Resources Root - директория с исходными кодами приложения


### SPI
SPI (Service Provider Interface) - ???

### war
War (Web Archive) - это формат в который упаковывается проект. Виды:
* war
* war exploded - это формат архива, который позволяет производить горячую замену статических элементов в web-приложении

### WEB-INF
WEB-INF - это директория в корне архива java-приложения. Эта директория используется только в [веб-архивах](#war). Эта директория не заменяет, а дополняет [META-INF](#meta-inf). В ней хранятся:
* [web.xml](#web-xml);
* Дескрипторы тегов .TLD;
* Поддиректория classes/ с классами web-приложения;
* Поддиректория lib/ с .jar-библиотеками зависимостей;
* Поддиректория tag/ с файлами тегов.

### web-xml
Web.xml - это [дескриптор развертывания](#deployment-descriptor) веб-приложения который храниться в директории [WEB-INF](#web-inf).

Для Spring Framework конфигурация из web.xml может быть настроена в java-коде, при использовании абстрактного класса [AbstractAnnotationConfigDispatcherServletInitializer](java-spring-webmvc.md#abstractannotationconfigdispatcherservletinitializer-class) или интерфейса [WebApplicationInitializer](java-spring-webmvc.md#webapplicationinitializer-class)

### webapp




### abstract-keyword

### assert-keyword

### boolean-keyword

### break-keyword

### byte-keyword

### case-keyword

### catch-keyword

### char-keyword

### class-keyword
- ключевое слово для объявления [интерфейса](java/Interface.md)

### const-keyword
Const - это зарезервированное ключевое слово.

### continue-keyword

### default-keyword

### do-keyword

### double-keyword

### else-keyword

### enum-keyword

### extends-keyword

### final-keyword

### finally-keyword

### float-keyword

### for-keyword

### goto-keyword
Goto- это зарезервированное ключевое слово.

## if-keyword

### implements-keyword

### import-keyword

### instanceof-keyword

### int-keyword

### interface-keyword
- ключевое слово для объявления [класса](java/Class.md)

### long-keyword

### native-keyword

### new-keyword

### package-keyword

### private-keyword

### protected-keyword

### public-keyword

### return-keyword

### short-keyword

### static-keyword

### strictfp-keyword

### super-keyword

### switch-keyword

### synchronized-keyword

### this-keyword

### throw-keyword

### throws-keyword

### transient-keyword

### try-keyword

### void-keyword

### volatile-keyword

### while-keyword