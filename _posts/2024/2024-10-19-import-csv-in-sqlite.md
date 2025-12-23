---
title: SQLite 기존 테이블에 csv 파일 INSERT(import) 하기
date: 2024-10-19
categories: interest
tags:
  - sqlite
image: /assets/images/logo_sqlite.png
toc: true
pin: false
math: true
mermaid: true
description: SQLite에서 새로 생성되는 데이터를 기존 테이블에 추가하는 방법을 알아본다.
---

## 기존 테이블에 csv 파일로 내용 추가 하기

매일 현장에서 생성되는 데이터를 수집, 정제한 후 그 결과를 csv 파일로 저장한다.  정형화된 csv 파일은 DBMS나 별도 프로그램을 통해  DB에 축적한다. RPA로 csv 파일까지 만들어지면 sqlite 함수를 통해 기존 테이블에 추가하는 방법을 알아본다.

![](/assets/images/Pasted%20image%2020241019004610.png)

아래와 같은 형식으로 csv 파일이 제공된다고 가정해 보자.

```
PersonID,LastName,FirstName,Address,City
105,John,Kim,New York,NY
```

SQLiteStudio에서는 `import` 메뉴를 통해 추가가 가능하다.

![](/assets/images/Pasted%20image%2020241019152738.png)

csv 파일에 해더(컬럼 이름)이 포함되어 있다면 `First line represents CSV column names` 옵션을 체크한다. 위 예제에서는 해더가 포함되어 있어 체크되어 있다. 또한 csv 파일 포멧이라 하더라도 구분자가 콤마가 아닌 세미콜론이나 기타 기호가 있을 수 있으니 확인 후 반영하도록 한다.

![](/assets/images/Pasted%20image%2020241019154156.png)

이렇게 수작업을 통해 진행할 수도 있지만, 스크립트를 작성해 주기적으로 반복하도록 스케쥴러에 등록하면 자동화가 가능해진다. 우선 sqlite CLI에서 어떻게 수행할 수 있는지 알아본다.

```
SQLite version 3.46.1 2024-08-13 09:16:08 (UTF-16 console I/O)
Enter ".help" for usage hints.
Connected to a transient in-memory database.
Use ".open FILENAME" to reopen on a persistent database.
sqlite> .open employee
sqlite> .mode csv
sqlite> .import --skip 1 employee_20241019.csv Persons
sqlite>
```

![](/assets/images/Pasted%20image%2020241019154116.png)

위 내용으로 아래와 같이 배치파일을 만들 수 있다.

```batch
sqlite3 employee ".mode csv" ".import --skip 1 employee_20241019.csv Persons"
```

