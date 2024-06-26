## Content

* [Absolute Path](#absolute-path)
* [Buffer](#buffer)
* [Buffered Stream](#buffered-stream)
* [Byte Stream](#byte-stream)
* [Character Stream](#character-stream)
* [destination]
* [File](#file)
* [Input](#input)
* [InputStream](#inputstream-class)
* [Output](#output)
* [OutputStream](#outputstream-class)
* [Source / Источник данных](#source)
* [Stream](#stream)
* [Абсолютный путь / Absolute Path](#absolute-path)
* [Буферизованный поток / Buffered Stream](#buffered-stream)
* [Входной поток / Input](#input)
* [Выходной поток / Output](#output)
* [Источник данных / Source](#source)
* [Символьный поток / Character Stream](#character-stream)
* [Файл/File](#file)


## I/O


### Absolute Path
Absolute Path (Абсолютный путь) - 

[content](#content) [index](/index.md)

### Buffer

### Buffered Stream
Buffered Stream (Буферизованный поток) - это потоки, которые к стандартным операциям ввода-вывода, добавляют [буфер в памяти](#buffer) с помощью которого, повышается производительность при чтении и записи. К буферизованным потокам относятся:
* [BufferedInputStream](#bufferedinputstream-class) - буферизованный входной поток байтов
* [BufferedReader](#bufferedreader-class) - буферизованный входной поток символов
* [BufferedOutputStream](#bufferedoutputstream-class) - буферизованный выходной поток байтов
* [BufferedWriter](#bufferedwriter-class) - буферизованный выходной поток символов

### BufferedInputStream-class
BufferedInputStream (java.io) - это [буферизованный поток](#buffered-stream) ввода, который накапливает вводимые данные в специальном буфере без постоянного обращения к устройству ввода. Кроме буфера класс не добавляет дополнительной функциональности.
<details> <summary>Конструкторы</summary>

``` java
BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream("c:\\file.txt"));         // (1) поток ввода, с которого данные будут считываться в буфер       
BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream("c:\\file.txt"), 1024);   // (1) поток ввода, с которого данные будут считываться в буфер, (2) размер буфера в байтах 
```
</details>

### BufferedReader-class
BufferedReader (java.io) - это [буферизованный поток](#buffered-stream) ввода

### BufferedOutputStream-class
BufferedOutputStream (java.io) - это [буферизованный поток](#buffered-stream) вывода, который накапливает выводимые данные в специальном буфере без постоянного обращения к устройству вывода, и когда буфер будет заполнен тогда производиться запись. Кроме буфера класс не добавляет дополнительной функциональности.
<details> <summary>Конструкторы</summary>

``` java
BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(new FileOutputStream("c:\\file.txt"));         // (1) поток вывода, в который будут записываться данные из буфера       
BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(new FileOutputStream("c:\\file.txt"), 1024);   // (1) поток вывода, в который будут записываться данные из буфера , (2) размер буфера в байтах 
```
</details>

### BufferedWriter-class
BufferedWriter (java.io)- это [буферизованный поток](#buffered-stream) вывода...

### ByteArrayInputStream-class
ByteArrayInputStream - это имплементация [InputStream](#inputstream-class) для работы с массивом байтов в памяти, для чтения данных из массива байтов.

### ByteArrayOutputStream-class
ByteArrayOutputStream - это имплементация [OutputStream](#outputstream-class) для работы с массивом байтов в памяти, для записи данных в массив байтов.

### Byte Stream
Byte Stream (поток байтов) - 

### Character Stream
Character Stream (символьный поток, поток символов) - это обертка над [потоком байтов](#byte-stream)

### Destination
Destination (пункт назначения)

### File
File (Файл) - .... Файл описывается типом [java.io.File](#file-class). Для работы с файлами используются:
* FileInputStream - для считывания данных из файла
* FileOutputStream - для записи данных в файл

### File-class
File - это объектно-ориентированное представление [файла](#file) или папки на жестком диске.

### FileInputStream-class
FileInputStream - это имплементация [InputStream](#inputstream-class) для работы с файлами, для чтения данных из файла.

### FileOutputStream-class
FileOutputStream - это имплементация [OutputStream](#outputstream-class) для работы с файлами, для записи данных в файл.

### FilterInputStream-class
FilterInputStream (java.io) - обертка над [InputStream](#inputstream-class) которая принимает аргументов конструктора объект [InputStream](#inputstream-class) и сохраняет его в volatile-переменной "in". Собственной функциональности класс не добавляет и существует только как промежуточный клас для того чтобы от него наследовались другие классы, такие как:
* BufferedInputStream

### Input
Input (входной поток) - ввод данных из внешнего источника в приложение. Если приложению нужно получить данные из [истончика](#source) то используются:
* [InputStream](#inputstream-class)
* [Reader](#reader-class)

### InputStream-class
InputStream (поток ввода) - это абстрактный класс, который описывает [входной поток](#input) или поток байтов из внешнего источника в приложение. Основной метод read(). Имеет реализации:
* BufferedInputStream
* ByteArrayInputStream - входной поток читающий из массив байтов в памяти;
* DataInputStream
* FileInputStream - входной поток читающий из файла;
* FilterInputStream
* ObjectInputStream
* PipedInputStream
* PushbackInputStream
* SequenceInputStream

### Output
Output (выходной поток) - вывод данных из приложения во внешний источник. Если приложению нужно отправить данные в [пункт назначения](#destination) то используются:
* [InputStream](#outputstream-class)
* [Writer](#writer-class)

### OutputStream-class
OutputStream (поток вывода) - это абстрактный класс, который описывает [выходной поток](#output) или поток байтов из приложения во внешний источник. Основной метод write(). Имеет реализации:
* BufferedOutputStream
* ByteArrayOutputStream - выходной поток записывающий в массив байтов в памяти;
* DataOutputStream
* FileOutputStream - выходной поток записывающий в файл;
* FilterOutputStream
* ObjectOutputStream
* PipedOutputStream
* PrintStream

### Reader-class
Reader - это поток символов из внешнего источника в приложение.

### Source
Source (источник данных) 

### Stream
Stream (Поток) - абстракция... 

### Writer-class
Writer - это поток символов из приложения во внешний источник.