

### ColumnPositionMappingStrategy-class

### CSVParser-class

### CSVParserBuilder-class
CSVParserBuilder - класс который позволяет настроить [CSVParser](#csvparser-class):


### CSVReader-class
CSVReader - только считывает в память данные из csv-файла. Объект CSVReader хранит:
* ссылку на [CSVParser](#csvparser-class)

```java
//Пример: считывание всего содержимого csv-файла
public List<String[]> readAllLines(Path filePath) throws Exception {
    try (Reader reader = Files.newBufferedReader(filePath)) {   //получаем объект Reader
        try (CSVReader csvReader = new CSVReader(reader)) {     //Reader оборачиваем в CSVReader
            return csvReader.readAll();                         //считываем все строки
        }
    }
}
```

### CSVReaderBuilder-class
CSVReaderBuilder

### CsvToBean-class
CsvToBean - класс считывает csv-файл в бины.


### CSVToBeanBuilder-class

### CSVWriter

### HeaderColumnNameMappingStrategy-class

### HeaderColumnNameTranslateMappingStrategy-class

### MappingStrategy
* [ColumnPositionMappingStrategy](#columnpositionmappingstrategy-class)
* [HeaderColumnNameMappingStrategy](#headercolumnnamemappingstrategy-class)

### opencsv

### Parser
Parser - ... В opencsv предусмотрены 2 парсера:
* CSVParser 
* RFC4180Parser



### @CsvBindAndJoinByPosition

### @CSVBindByName-annotation

### @CSVBindByPosition-annotation
@CSVBindByPosition - позволяет несколько колонок объединить в одну коллекцию