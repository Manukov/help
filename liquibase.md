## Content

* [Commands](#commands)
* [Contexts](#contexts)
* [Databasechangelock](#databasechangelock)
* [Databasechangelog](#databasechangelog)
* [Label Expression](#label-expression)
* [Labels](#labels)
* [Master File](#root-changelog)
* [Migration](#migration)
* [Nested Changelog](#nested-changelog)
* [Root Changelog](#root-changelog)
* [Tag](#tag)
* [Команды / Commands](#commands)
* [Локальный мастер-файл / Nested Changelog](#nested-changelog)
* [Миграция / Migration](#migration)

### Liquibase

### ChangeLog
ChangeLog - это файл со списком миграций базы данных
* [Nested Changelog](#nested-changelog)
* [Root Changelog](#root-changelog)

### ChangeSet
Виды:
* [Raw SQL changeset](#raw-sql-changeset)
* [ChangeTypes](#changetypes)

Атрибуты: 
* [Labels](#labels)
* [Contexts](#contexts)

### ChangeTypes
ChangeTypes - это изменения описанные на JSON, XML, YAML. Преимущество ChangeTypes в том, что они одинаково раскатываются на все базы данных

### Commands
* [diff](#diff-command)
* [diff-changelog](#diff-changelog-command)
* [generateChangeLog](#generatechangelog-command)
* [rollback](#rollback-command);
* [snapshot](#snapshot-command);
* [update](#update-command);


### Contexts
Contexts - это атрибут [changeset](#changeset), который представлет собой строку или список строк и которыми мы можем помечать changeset-ы. 
Контексты добавляются к include и includeAll и на этапе внедрения changelog-файлов в [master file](#root-changelog) позволяют фильтровать добавление changeset-ов. Если сhangeset не имеет атрибута contexts то include без контекста будут выполняться для всех контекстов.

Синтаксис (используется в тэге Include и includeAll):
* AND - оператор логического И;
* OR или "," - оператор логического ИЛИ;
* ! - оператор отрицания;
* () - оператор, который используется для группировки;

```xml
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog
        xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-latest.xsd">

    <include file="/release-1.0.0/release-1.0.0-root.xml" context="(DEV OR IFT) AND !PROD"/>
    <include file="/release-2.0.0/release-2.0.0-root.xml" context="DEV"/>
</databaseChangeLog>
```

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
diff-changelog - 
- это команда, которая создает changelog-файл с изменениями для создания текущего состояния базы данных. 
- то же самое что и [diff](#diff-command), но дополнительно создается файл changelog. И если этот файл с набором changeset применить на первой базе, то получим структуру идентичную второй
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

### Label Expression
Label Expression - это логические выражения, которые передаются параметром в [liquibase-команды](#commands) для того, чтобы отфильтровать changeset-ы по labels. В момент выполнения Liquibase проверяет,
подходят ли label объявленные в changeset под Label Expressions. Changesets в которых вообще нет label будут выполняться для любого Label Expression

Синтаксис:
* AND - оператор логического И;
* OR или "," - оператор логического ИЛИ;
* ! - оператор отрицания;
* () - оператор, который используется для группировки;

```
# Если changeset помечен меткой JIRA-1234 и JIRA-4321 или release1.0.0 и метка не содержит JIRA-235
--liquibase update --labels="((JIRA-1234 AND JIRA-4321) OR release1.0.0) and !JIRA-235"
```

### Labels
Label (метка) - это атрибут [changeset](#changeset), который представлет собой строку или список строк, которыми мы можем помечать changeset-ы. С их помощью мы можем группировать changesets и контролировать, какие из них будут выполняться. Когда мы запускаем команду Liquibase мы передаем в атрибутах выражение (Label Expression). Это выражение будет использоваться как фильтр, чтобы определить, какие changesets нужно выполнить. Все labels регистронезависимы.
```
--liquibase firmatted sql
-- changeset manukov:001 labels:JIRA-1234, release1.1
CREATE TABLE CARDS (
    ...
)
```

### Migration
Migration (Миграция) - переезд с одной версии на другую. Мод миграцией подразумевается любое изменение структуры. К термину "миграция" относятся 3 термина:
* changeLogFile
* changeSet
* changetypes

### Nested Changelog
Nested Changelog (Вложенный changelog) - .... подключается к [Root Changelog](#root-changelog) двумя способами:
* ```include``` - после которой указывается вложенный changelog и путь к нему. Когда liquibase обрабатывает master file то вложенные changelog  он обрабатывает в порядке добавления
* ```includeAll``` - после которой указывается директория в которой находяться вложенные changelog

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

### Root Changelog
Root Changelog или Master File - это changelog в который подключаются другие changelog [вложенные changelog](#nested-changelog). Master File может быть написан на XML, JSON или YAML, но не может быть написан на SQL.

### snapshot-command
snapshot - команда которая выводит информацию о ткущем состоянии базы данных. Liquibase выведет список всех структур которые он видит в базе данных, включая таблицы [Databasechangelog](#databasechangelog) и [Databasechangelock](#databasechangelock)
``` 
liquibase snapshot                                                  # получаем текущее состояние базы и выводим в коноль
liquibase snapshot --outputfile=file.txt                            # получаем текущее состояние базы и записываем полученный отчет в файл "file.txt"
liquibase snapshot --outputfile=file.json --snapshotFormat=JSON     # получаем текущее состояние базы и записываем полученный отчет в файл "file.json" и форматируем как JSON
liquibase snapshot --outputfile=file.yaml --snapshotFormat=YAML     # получаем текущее состояние базы и записываем полученный отчет в файл "file.yaml" и форматируем как YAML
```

### Tag
Tag (тэг) - 

```xml
<?xml version="1.0" encoding="UTF-8"?>	
<databaseChangeLog
    xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-latest.xsd">

    <include file="/release-1.0.0/release-1.0.0-root.xml"/>
    <!-- После инструкции include отдельным changeSet устанавливает тэг "tag-release-1.0.0-end" для всех changeset-ов подключаемых файлом release-1.0.0-root.xml
    Это дает возможность откатить командой rolback все changeSet с таким тэгом-->
    <changeSet id="tag-release-1.0.0-end" author="_author">
        <tagDatabase taf="tag-release-1.0.0-end"/>
    </changeSet>
</databaseChangeLog>

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