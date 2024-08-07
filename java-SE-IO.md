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
* [System.in](#systemin)
* [System.out](#systemout)
* [Source / Источник данных](#source)
* [Stream](#stream)
* [Абсолютный путь / Absolute Path](#absolute-path)
* [Буфер / Buffer](#buffer)
* [Буферизованный поток / Buffered Stream](#buffered-stream)
* [Входной поток / Input](#input)
* [Выходной поток / Output](#output)
* [Источник данных / Source](#source)
* [Поток ввода / InputStrem](#inputstream-class)
* [поток вывода / OutputStrem](#outputstream-class)
* [Символьный поток / Character Stream](#character-stream)
* [Файл/File](#file)


### Java I/O API


### Absolute Path
Absolute Path (Абсолютный путь) - 

[content](#content) [index](/index.md)

### Buffer
Buffer (Буфер) - это блок памяти, из которого мы можем читать или записывать данные

### Buffered Stream
Buffered Stream (Буферизованный поток) - это поток, который к стандартным операциям ввода-вывода добавляют [буфер в памяти](#buffer) с помощью которого, повышается производительность при чтении и записи. К буферизованным потокам относятся:
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
* [RandomAccessFile](#randomaccessfile-class) - запись, чтение и произвольное перемещение по файлу

### File-class
File - это объектно-ориентированное представление [файла](#file) или папки на жестком диске.

### FileInputStream-class
FileInputStream - это имплементация [InputStream](#inputstream-class) представляющая "считываемый файл" в виде потока, из которого возможно считывать данные только последовательно, от начала до конца. Для произвольного чтения из файла используется [RandomAccessFile](#randomaccessfile-class). 

### FileOutputStream-class
FileOutputStream - это имплементация [OutputStream](#outputstream-class) представляющая "записываемый файл" в виде потока, в который возможно записывать данные только последовательно, от начала точки записи до конца файла. Для произвольной записи в любую часть файла используется [RandomAccessFile](#randomaccessfile-class).

### FilterInputStream-class
FilterInputStream (java.io) - обертка над [InputStream](#inputstream-class) которая принимает аргументов конструктора объект [InputStream](#inputstream-class) и сохраняет его в volatile-переменной "in". Собственной функциональности класс не добавляет и существует только как промежуточный клас для того чтобы от него наследовались другие классы, такие как:
* BufferedInputStream

### Input
Input (входной поток) - ввод данных из внешнего источника в приложение. Если приложению нужно получить данные из [истончика](#source), то используются:
* [InputStream](#inputstream-class)
* [Reader](#reader-class)

### InputStream-class
InputStream (поток ввода) - это абстрактный класс, который описывает [входной поток](#input) или поток байтов из внешнего источника в приложение. Основной метод read(). Имеет реализации:
* BufferedInputStream
* ByteArrayInputStream - входной поток читающий из массива байтов в памяти;
* DataInputStream
* FileInputStream - входной поток читающий из файла;
* FilterInputStream
* ObjectInputStream
* PipedInputStream
* PushbackInputStream
* SequenceInputStream

### Offset
Offset (смещение) - определяется от начала файла 

индекс байта в котором в текущий момент находиться указатель

### Output
Output (выходной поток) - вывод данных из приложения во внешний источник. Если приложению нужно отправить данные в [пункт назначения](#destination), то используются:
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


### PrintStream-class
PrintStream (java.io) - это класс, который позволяет выводить информацию в [поток вывода](#outputstream-class). 

### PrintWriter-class

### RandomAccessFile-class
RandomAccessFile (java.io) - это класс, который позволяет перемещаться по файлу в произвольном порядке, читать из него или записывать в него по своему усмотрению, либо заменить существующие части файла. Такие операции невозможны при работе с [FileInputStream](#fileinputstream-class) или [FileOutputStream](#fileoutputstream-class).
Навигация по фалу осуществляется через offset/смещение - указатель на индекс байта в файле
<details> <summary>Конструкторы</summary>

При создании объекта устанавливается режим работы с файлом:
* r - режим чтения. Вызов методов записи приведет к возникновению исключения IOException
* rw - режим чтения и запи си
* rwd - ...
* rws - ...
``` java
RandomAccessFile file = new RandomAccessFile("c:\\data\\file.txt", "rw");       
```
</details>
<details> <summary>Методы</summary>

* long getFilePointer() - возвращает "текущую позицию" на которой находиться указатель;
* int read() - считывает 1 байт с позиции, на которую в настоящий момент указывает указатель. После считывания байта, указатель перемещается на следующую позицию, поэтому можно повторно использовать вызов read() без необходимости вручную перемещать указатель файла. Метод возвращает считанный байт;
* int read(dest, offset, lenght) - считывает в dest (массив байтов) все байты начиная от offset и не более чем указано в lenght. Метод вернет кол-во считанных байтов
* seek(long) - помещает указатель файла на позицию с которой нужно начинать считывать либо записывать. Аргументом метода передается индекс на который нужно переместить указатель файла;
* write(int) - записывает один байт в позицию, на которую оказывает указатель. Предыдущий байт на этой позиции будет перезаписан. Вызов метода увеличивает указатель файла на 1;
``` java
RandomAccessFile file = new RandomAccessFile("c:\\data\\file.txt", "rw"); 

//считывание массива байтов из середины файла
byte[] arr = new byte[1024];                    //массив байтов в который считываем байты из файла
int offset = 1;
int lenght = 1024;
int bytesRead = file.read(arr, offset, length);  //считываем в массив arr 1024 байта начиная с позиции под индексом 1  

file.close();               //закрываем файл
```
</details>


### Reader-class
Reader - это поток символов из внешнего источника в приложение.

### System.in
System.in – это статическая переменная по имени in типа InputStream в классе System

### System.out
System.out – это статическая переменная по имени out типа PrintStream (наследник OutputStream) в классе System.

### Source
Source (источник данных) 

### Stream
Stream (Поток) - абстракция... Все потоки ввода/вывода разделяются по:
1. Направлению: поток ввода, поток вывода
2. Типу данных: байтовый поток, символьный поток

|        | Поток ввода | Поток вывода |
|--------|-------------|--------------|
| Байт   | InputStream | OutputStream |
| Символ | Reader      | Writer       |

### Writer-class
Writer - это поток символов из приложения во внешний источник.