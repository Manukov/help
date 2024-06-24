## Content

* [Absolute Path](#absolute-path)
* [Buffer](#buffer)
* [Buffered Stream](#buffered-stream)
* [Byte Stream](#byte-stream)
* [Character Stream](#character-stream)
* [File](#file)
* [Input](#input)
* [InputStream](#inputstream-class)
* [Output](#output)
* [OutputStream](#outputstream-class)
* [Stream](#stream)
* [Абсолютный путь / Absolute Path](#absolute-path)
* [Буферизованный поток / Buffered Stream](#buffered-stream)
* [Входной поток / Input](#input)
* [Выходной поток / Output](#output)
* [Символьный поток / Character Stream](#character-stream)
* [Файл/File](#file)


### Absolute Path
Absolute Path (Абсолютный путь) - 

[content](#content) [index](/index.md)

### Buffer

### Buffered Stream
Buffered Stream (Буферизованный поток) - это потоки, которые к стандартным операциям ввода-вывода, добавляют [буфер в памяти](#buffer) с помощью которого, повышается производительность при чтении и записи

### ByteArrayInputStream-class
ByteArrayInputStream - это имплементация [InputStream](#inputstream-class) для работы с массивом байтов в памяти, для чтения данных из массива байтов.

### ByteArrayOutputStream-class
ByteArrayOutputStream - это имплементация [OutputStream](#outputstream-class) для работы с массивом байтов в памяти, для записи данных в массив байтов.

### Byte Stream
Byte Stream (поток байтов) - 

### Character Stream
Character Stream (символьный поток, поток символов) - это обертка над [потоком байтов](#byte-stream)

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

### Input
Input (входной поток) - ввод данных из внешнего источника в приложение. 

### InputStream-class
InputStream (поток ввода) - это абстрактный класс, который описывает [входной поток](#input) или поток байтов из внешнего источника в приложение. Основной метод read(). Имеет реализации:
* ByteArrayInputStream - входной поток читающий из массив байтов в памяти;
* FileInputStream - входной поток читающий из файла;

### Output
Output (выходной поток) - вывод данных из приложения во внешний источник.

### OutputStream-class
OutputStream (поток вывода) - это абстрактный класс, который описывает [выходной поток](#output) или поток байтов из приложения во внешний источник. Основной метод write(). Имеет реализации:
* ByteArrayOutputStream - выходной поток записывающий в массив байтов в памяти;
* FileOutputStream - выходной поток записывающий в файл;

### Reader
Reader - это поток символов из внешнего источника в приложение.

### Stream
Stream (Поток) - абстракция... 

### Writer
Writer - это поток символов из приложения во внешний источник.