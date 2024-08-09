## Content

* [Batch](#batch)
* [Clause](#clause)
* [Command](#statement)
* [Common Table Expression](#common-table-expression)
* [CTE](#common-table-expression)
* [Data Definition Language](#data-definition-language)
* [DDL](#data-definition-language)
* [Optimization Engines](#optimization-engines)
* [Predicate](#predicate)
* [Query](#query)
* [Query Dispatcher](#query-dispatcher)
* [Script](#script)
* [Statement](#statement)
* [Subquery](#subquery)
* [View](#view)
* [Диспетчер запросов / Query Dispatcher](#query-dispatcher)
* [Запрос / Statement](#statement)
* [Общее табличное выражение /Common Table Expression](#common-table-expression)
* [Оператор / Statement](#statement)
* [Подзапрос / Subquery](#subquery)
* [Предикат / Predicate](#predicate)
* [Представление / View](#view)


### Batch
Batch (Пакет инструкций) — это единица, в которой работа отправляется на сервер. Пакет состоит из одного или нескольких [операторов](#statement)

В SQL Server каждый пакет (обычно) разделяется GO. Разделение скрипта на пакеты — это работа, выполняемая клиентскими инструментами.

### Clause
Clause (Предложение) - это раздел или часть [statement](#statement). Предложение само по себе не может быть выполнено, но в сочетании с другими предложениями ее выполнение возможно. Например:
```
-- Statement (оператор) который состоит из 3-х предложений (clause)
-- каждое из которых не может быть выполнено самостоятельно
-- но комбинация которых создает statement (оператор).
Select col1, col2, col3         -- claause 1
From table_name                 -- claause 2
Where (some condition)          -- claause 3
```
Предложения обычно вводятся ключевым словом в честь которого они и называются, например:
* WHEN clause - [WHEN](#when-keyword)
* WHERE clause -[WHERE](#where-keyword)

### Common Table Expression
Common Table Expression (общее табличное выражение) - это временный результат выполнения SQL-выражения, который можно использовать в другом SQL-выражении. CTE позволяет упрощать сложные SQL-запросы, разбивая их на составные части.

* считается "временным" потому что что результат не сохраняется где-либо на постоянной основе в схеме базы данных, а действует как временное представление, которое существует только на время выполнения запроса, то есть оно доступно только во время выполнения операторов SELECT, INSERT, UPDATE, DELETE или MERGE 
* действительно только в том запросе, которому он принадлежит

```
-- создаем CTE
WITH Aeroflot_trips AS
    (SELECT TRIP.* FROM Company
        INNER JOIN Trip ON Trip.company = Company.id WHERE name = "Aeroflot")
        
- используем CTE       
SELECT plane, COUNT(plane) AS amount FROM Aeroflot_trips GROUP BY plane;
```



### Data Definition Language
Data Definition Language (DDL, язык определения данных)

### Expression
Expression (Выражение) — это то, что производит значение. В обычных языках "выражение" - это то что производит скалярное значение, но в SQL это немного изменено, потому что при работе с набором строк, выражение будет производить одно скалярное значение на строку или группу строк.

### Index

### Keywords
* [CREATE](#create-keyword)
* [INDEX](#index-keyword)
* [UNIQUE](#unique-keyword)
* [WITH](#with-keyword)


### Optimization Engines
Optimization Engines (Движок оптимизации)

### Predicate
Predicate (предикат) - это логическое [выражение](#expression)


### Query

### Query Dispatcher


### Script
Script (Скрипт) - это файл содержащий код SQL. Скрипт может содержать один или несколько [пакетов](#batch).

### Statement
Statement (Command, Query) — это законченный фрагмент кода, который движок базы данных может выполнить. Для СУБД statement является наименьшей единицей индивидуальной работы, с которой может работать сервер и как результат
этой работы возвращать набор данных или изменять данные на сервере. Обычно сервер компилирует каждый оператор по отдельности (но может выполнять каждую компиляцию для каждого оператора в пакете до того, как любой из них будет выполнен).

Statement - это структурированный запрос, который состоит из одного или нескольких [clause](#clause)

### Subquery
Subquery (Подзапрос) — это SELECT-запрос, вложенный в другой запрос или подзапрос. 
Подзапрос является внутренним запрсоов, а внешним запросом является оператор который содержит подзапрос. 
Подзапросами пользуются, когда нужно использовать результат выполнения одного запроса в следующем запросе.

Синтаксически подзапрос — это SELECT-запрос, обернутый в круглые скобки ( ). Подзапрос может быть вложен 
в любой другой оператор. Можно вкладывать подзапросы в подзапросы.

Виды подзапросов:
* Простой - это подзапрос, который не зависит от внешнего запроса. СУБД выполнит такой подзапрос один раз перед выполнением внешнего запроса — и позже будет использовать значение столько раз, сколько понадобится;
* Сложный - это подзапрос, который обращаются к полям внешнего запроса. СУБД будет вынуждена выполнить подзапрос для каждой строки, подставляя значение строки внешнего значения как параметр подзапроса


<details> <summary>Пример: простой подзапрос</summary>

```
-- Простой подзапрос SELECT DISTINCT student_id FROM Marks выполниться только один раз
SELECT * FROM Students WHERE id NOT IN (SELECT DISTINCT student_id FROM Marks);
```
</details>
<details> <summary>Пример: сложный подзапрос</summary>

```
-- Сложный подзапрос использует Students.id из внешнего запроса
SELECT * FROM Students 
WHERE (SELECT AVG(mark) FROM Marks WHERE Students.id = Marks.student_id) 
```
</details>

### View





### CREATE-keyword

### INDEX-keyword

### INNER-keyword

### UNIQUE-keyword

### WHEN-keyword

### WHERE-keyword

### WITH-keyword