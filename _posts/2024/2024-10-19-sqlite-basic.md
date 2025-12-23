---
title: SQLite
date: 2024-10-19
categories: interest
tags:
  - sqlite
image: /assets/images/logo_sqlite.png
toc: true
pin: false
math: true
mermaid: true
description: 응용 프로그램에 넣어 사용하거나 중소 규모 작업을 위한 가벼운 SQLite에 대해 알아본다.
---
## SQLite

**SQLite**는 가볍고, 빠르고,  독립적이고, 안정성 높은 완전한 기능을 갖춘 SQL DB엔진을 구현한 C언어 라이브러리이다.[^1]

[^1]: [https://sqlite.org/](https://sqlite.org/)

SQLite는 [여기](https://sqlite.org/download.html)에서 OS 및 배포 형태에 따라 다운로드 가능하다.  Windows 버전을 다운로드 하면 `sqlite3.exe` 파일이 압축되어 있다. 이 파일을 실행시키면 된다.

![](/assets/images/Pasted%20image%2020241018234515.png)
![](/assets/images/Pasted%20image%2020241018234555.png)

사용편의를 위해 SQLiteStudi을 [다운로드](https://github.com/pawelsalawa/sqlitestudio/releases/download/3.4.4/SQLiteStudio-3.4.4-windows-x64-installer.exe) 받아 사용한다.
![](/assets/images/Pasted%20image%2020241018234807.png)

자세한 사용법은 [User_Manual](https://github.com/pawelsalawa/sqlitestudio/wiki/User_Manual)을 참고한다.

## SQL 문법

예제 테이블을 다음과 같이 생성한다.[^2]

```sql
CREATE TABLE Persons (  
	PersonID int,  
	LastName varchar(255),  
	FirstName varchar(255),  
	Address varchar(255),  
	City varchar(255)  
);
```

[^2]: [https://www.w3schools.com/sql/default.asp](https://www.w3schools.com/sql/default.asp)

![](/assets/images/Pasted%20image%2020241019004610.png)


SQLite **CRUD**(Create, Read, Update, Delete)는 일반 SQL 구문과 유사하다.

- Create - INSERT
- Read - SELECT
- Update - UPDATE
- Delete - DELETE

각각에 대해 간략히 알아본다.
### INSERT

INSERT 구문은 다음과 같은 구조를 갖는다. 테이블에 행을 생성한다.

```sql
INSERT INTO table_name (column1, column2, column3, ...)  
VALUES (value1, value2, value3, ...);
```

```sql
INSERT INTO Persons (PersonID, LastName, FirstName, Address, City)
VALUES (104, 'John', 'Kim', 'Kangnam', 'Seoul');
```

![](/assets/images/Pasted%20image%2020241019004945.png)
### SELECT

SELECT 구문은 다음과 같은 구조를 갖는다.

```sql
SELECT * FROM table_name;
SELECT column1, column2, ... FROM table_name;
SELECT column1, column2, ... FROM table_name WHERE condition;
```

```sql
SELECT LastName, FirstName, Address
FROM Persons
WHERE PersonID = 101;
```

![](/assets/images/Pasted%20image%2020241019005244.png)
### UPDATE

```sql
UPDATE table_name  
SET column1 = value1, column2 = value2, ...  
WHERE condition;
```

```sql
UPDATE Persons
SET FirstName = 'Wick'
WHERE PersonID = 104
```

![](/assets/images/Pasted%20image%2020241019005659.png)

### DELETE
```sql
DELETE FROM table_name WHERE condition;
```

```sql
DELETE FROM Persons WHERE PersonID = 104;
```

![](/assets/images/Pasted%20image%2020241019005926.png)
## Reference