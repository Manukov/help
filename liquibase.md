## Content

* [Commands](#commands)
* [Databasechangelock](#databasechangelock)
* [Databasechangelog](#databasechangelog)
* [Migration](#migration)
* [Комманды / Commands](#commands)
* [Миграция / Migration](#migration)

### Liquibase

### ChangeLog

### ChangeSet

Виды:
* [Raw SQL changeset](#raw-sql-changeset)
* [ChangeTypes](#changetypes)

### ChangeTypes
ChangeTypes - это изменения описанные на JSON, XML, YAML. Преимущество ChangeTypes в том, что они одинаково раскатываются на все базы данных

### Commands
* [diff](#diff-command)
* [diff-changelog](#diff-changelog-command)
* [generateChangeLog](#generatechangelog-command)
* [rollback](#rollback-command);
* [snapshot](#snapshot-command);
* [update](#update-command);

### Databasechangelock
Databasechangelock - это таблица 

### Databasechangelog

### diff-command
diff - команда выводит разницу между структурами двух баз данных. Команда делает [snapshot](#snapshot-command) одной базы данных, [snapshot](#snapshot-command) второй базы данных, получает 2 списка структур и сравнивает эти структуры между собой (что есть
в первой, но нет во второй, и что есть во второй, но нет в первой).
``` 
liquibse diff --outputFile=diff.txt             # Для H2. Базы беруться из liquibase.properties, где url - исходный инстанс базы данных, а referenceUrl - второй инстанс
                                                # результат сравнения выводится в файл "diff.txt"
                                                
liquibse diff --outputFile=diff.txt diffTypes=tables,columns    # сравнение производиться только для таблиц и полей
```


### diff-changelog-command
diff-changelog - то же самое что и [diff](#diff-command), но дополнительно создается файл changelog. И если этот файл с набором changeset применить на первой базе, то получим структуру идентичную второй
``` 
# комманда выполняется как через "diff-changelog" так и "diffСhangelog"  

liquibse diff-changelog --changeLogFile=diff-changelog.h2.sql                       #            
liquibse diffСhangelog --changeLogFile=diff-changelog.h2.sql --diffTypes=tables     # только для таблиц           
```


### generateChangeLog-command
generateChangeLog - 
``` 
liquibase generateChangeLog --changeLogFile=changelog.h2.sql            # получаем файл changelog.h2.sql который будет содержать текущее состояния базы данных
                                                                        # для каждой таблицы в базе данных liquibase создает отдельный changeSet
                                                                        # h2 - указание для какой СУБД генерируется SQL
                                                                        
liquibase generateChangeLog --changeLogFile=changelog.xml               # получаем файл changelog.xml который будет содержать текущее состояния базы данных
                                                                        # для каждой таблицы в базе данных liquibase создает отдельный changeSet
                                                                        # указание СУБД не требуется, так как используется ChangeTypes
                                                                        
liquibase generateChangeLog --changeLogFile=changelog.h2.sql --dyffTypes=tables     # получаем файл changelog.h2.sql который будет содержать текущее состояния базы данных
                                                                                    # но каждый changeSet будет содержать только скрипт создания пустой таблицы (без полей, ключей, индексов и т. п.)
                                                                                    
liquibase generateChangeLog --changeLogFile=changelog.h2.sql --dyffTypes=tables,indexes     # получаем файл changelog.h2.sql который будет содержать текущее состояния базы данных
                                                                                            # в файле будут changeSet-ы для создания таблиц и changeSet-ы для создания индексов
 
liquibase generateChangeLog --changeLogFile=changelog.h2.sql --dyffTypes=tables,indexes,columns        # получаем файл changelog.h2.sql который будет содержать текущее состояния базы данных
                                                                                                        # в файле будут changeSet-ы для создания таблиц c полями и changeSet-ы для создания индексов
```

### Master File
Master File - это changelog в который подключаются другие changelog 


### Migration
Migration (Миграция) - переезд с одной версии на другую. Мод миграцией подразумевается любое изменение структуры. К термину "миграция" относятся 3 термина:
* changeLogFile
* changeSet
* changetypes

### Raw SQL changeset

### rollback-command
rollback - это команда, которая используется для отката базы данных до какого-то состояния (состояние фиксируется в таблице [Databasechangelog](#databasechangelog)
* rollbackToDate <yyyy-MM-dd'HH:mm:aa> - откатывает базу до указанной даты
* rollbackCount <кол-во changeset> - отсчитывает указанное кол-во changeset с конца таблицы
* rollbackTag <tag> - 

[Raw SQL changeset](#raw-sql-changeset) должны содержать rollback в явном виде, чтобы изменения можно было откатить. При использовании [ChangeTypes](#changetypes) многие rollback поддерживаются из коробки, но лучше так же задавать их в явном виде
``` 
liquibase rollbackCount 1 --changeLogFile=changelog.xml             # из changelog.xml считывает все changeset-ы и отменяет 1 последний
```

### snapshot-command
snapshot - команда которая выводит информацию о ткущем состоянии базы данных. Liquibase выведет список всех структур которые он видит в базе данных, включая таблицы [Databasechangelog](#databasechangelog) и [Databasechangelock](#databasechangelock)
``` 
liquibase snapshot                                                  # получаем текущее состояние базы и выводим в коноль
liquibase snapshot --outputfile=file.txt                            # получаем текущее состояние базы и записываем полученный отчет в файл "file.txt"
liquibase snapshot --outputfile=file.json --snapshotFormat=JSON     # получаем текущее состояние базы и записываем полученный отчет в файл "file.json" и форматируем как JSON
liquibase snapshot --outputfile=file.yaml --snapshotFormat=YAML     # получаем текущее состояние базы и записываем полученный отчет в файл "file.yaml" и форматируем как YAML
```

### update-command
update - команда применяет changeset описанные в файле changelog. Liquibase применяет changeset в том порядке, в котором они описаны в файле changelog. Для
каждого changeset проверяется наличие уникального сочетания id, author, path и сверяет его с таблицей [Databasechangelog](#databasechangelog). Если такой комбинации в таблице
нет, то changeset применяется. Если такое сочетание id, author, path уже есть в таблице, тогда выполняется сравнение хэш-суммы. Если хэш суммы равны, то это значит что такой changeset
уже был применен, если хэш суммы не совладают, то возникает исключительная ситуация.
``` 
# обновить инстанс integration из файла changelog.xml. В результате все changeset из файла changelog.xml будут применены к инстансу integration
liquibase update url=jdbc:h2:tcp://localhost:9090/mem:integration --changeLogFile=changelog.xml 

```