## Content

* [Commands](#commands)
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
в первой но нет во второй, и что есть во второй но нет в первой).

### diff-changelog-command
diff-changelog - то же самое что и [diff](#diff-command), но дополнительно создается файл changelog. И если этот файл с набором changeset применить на первой базе, то получим структуру идентичную второй

### generateChangeLog-command
generateChangeLog - 

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

### snapshot-command
snapshot - команда которая выводит информацию о ткущем состоянии базы данных. Liquibase выведет список всех структур которые он видит в базе данных

### update-command
update - команда применяет changeset описанные в файле changelog. Liquibase применяет changeset в том порядке, в котором они описаны в файле changelog. Для
каждого changeset проверяется наличие уникального сочетания id, author, path и сверяет его с таблицей [Databasechangelog](#databasechangelog). Если такой комбинации в таблице
нет, то changeset применяется. Если такое сочетание id, author, path уже есть в таблице, тогда выполняется сравнение хэш-суммы. Если хэш суммы равны, то это значит что такой changeset
уже был применен, если хэш суммы не совмадают, то возникает исключитьльная ситуация.
``` 
liquibase - - changeLogFile=changelog.xml update
```