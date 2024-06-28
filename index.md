## Content

* [Absolute path](#absolute-path)
* [Current Directory](#current-directory)
* [File Descriptor](#file-descriptor)
* [ID](#identifier)
* [Identifier](#identifier)
* [HTML](html.md)
* [Regex](index/regex.md)
* [Relative Path](#relative-path)
* [URL-encoding](html.md#url-encoding)
* [Дескриптор файла / File Descriptor](#file-descriptor)
* [Регулярные выражения / Regex](index/regex.md)
* [Файловый дескриптор / File Descriptor](#file-descriptor)

### Absolute Path
Absolute Path (абсолютный путь) - это путь который указывается с начала файловой системы («/»  - определяет корневая директория диска если идет первым символом в пути). Абсолютный путь = относительный путь + текущая директория, где запущена JVM.

[content](#content) [Java-SE-IO](java/java-SE-IO.md#absolute-path)

### Buffer

### Current Directory
Current Directory (Текущая директория)

### File Descriptor
File Descriptor (файловый дескриптор, дескриптор файла) — натуральное число ([идентификатор](#identifier)), закреплённое за определённым потоком ввода-вывода. При создании нового потока ввода-вывода (который может быть связан как с файлами, так и с каталогами, сокетами и FIFO), ядро возвращает его файловый дескриптор создавшему его процессу. Файловый дескриптор может использоваться для получения доступа к потоку.

### Identifier
Identifier (Идентификатор) — уникальный признак объекта, позволяющий отличать его от других объектов.

### Relative Path