- **==database==** : soft engenieer들이 데이터를 어떻게, 무엇으로 관리하는가? 
```mermaid
  graph LR
	user[user] --> app[APP] 
	app[APP] --> |앱을 사용| db[DATABASE]
	db --> |데이터베이스의 요청에서 데이터를 가지고 옴| app
	app --> |가지고온 데이터를 앱이 
	가공해서 사용자에게 제공| user
  ```
  ---
  - **==Relational DATABASE==** (관계형 데이터베이스)
  ```mermaid
flowchart TB
    subgraph RDB["Relational DATABASE"]
        direction TB
        MySQL
        Oracle
        SQLServer["SQL Server"]
        PostgreSQL
        등..
    end
  ```
---
## **==PostgreSQL==** 
- ==server-client  구조==를 지님
  - **==SERVER(PostgreSQL)== : 데이터를 보관하고 관리하는 프로그램**
	1) 대부분의 일을 하는 앱
	2) 사용자들은 server의 데이터를 직접 다룰 수 없음
	3) 대신, CLIENT를 사용해서 Server가 관리하는 데이터에 접근할 수 있음
  - **==GUI CLIENT(pgAdmin 4)==**
  - **==CLI CLIENT(psql)==**
  ``` mermaid
  flowchart LR
    %% CLIENT 영역
    subgraph CLIENT
        direction TB
        GUI["GUI Client<br/>pgAdmin 4"]
        CLI["CLI Client<br/>psql"]
    end

    %% SERVER 영역
    subgraph SERVER
        Postgre["PostgreSQL<br/>Server"]
    end

    %% 연결(양방향)
    GUI <--> Postgre
    CLI <--> Postgre
  ```
  -> 이와 같은 surver client 구조 덕분에 surver가 다른 컴퓨터에 있더라도 client를 이용해서 원격으로 인터넷을 이용해 다룰 수 있게 된다. 

## ==SERVER의 구조==
- **table(표)** : 하나의 app을 만들기 위해서는 여러 개의 table 필요
- **schema** : 여러 개의 연관된 table을 grouping하여 이름을 붙인 것
- **databse** : schema의 양이 많아져 이를 관리하기 위한 group 
-> *하나의 컴퓨터에는 여러 개의 database가 존재할 수 있음*
- **cluster(database server)** : 여러 개의 database를 grouping하여 묶은 것
 -> *client들은 이 cluster와 접속을 시도하는 것*
  ```mermaid
  flowchart LR
    SQLClient["💻 SQL Client"]

    Cluster["Cluster (DB Server)"]
    Database["Database"]
    Schema["Schema"]
    Table["Table"]

    %% 계층 구조
    SQLClient --> Cluster
    Cluster --> Database
    Database --> Schema
    Schema --> Table
    
    Table --> SQLClient
  ```
---

## ==pgAdmin 4 실습==
- ### ==**SERVER 등록**==
  -> **Name : MyPG**
  -> **Connection - Host name : localhost** (client와 server가 같은 컴퓨터에 있기 때문)
  *server 등록 후 Databases와 Roles가 생성되는데, Roles가 user임*
- ### ==**DATABASES 생성**==
  -> **Database : opentutorials**
  ![[Pasted image 20260115105307.png|450]] 
  : 이 코드가 서버로 전달되어서 opentutorials라는 database가 생성되는 것
- ### ==**Tables 생성**==
  -> **Name : topic**
  -> **Columns(열) 생성**
  ![[Pasted image 20260115104701.png|450]]
  1) Name : id - Data type : serial(자동으로 1씩 증가되는 값) - Not NULL(id값은 무조건 하나씩 있어야 함) - Primary key(id값은 고유의 값으로 중복을 방지, 빠르게 조회할 수 있음)
  2) Name : title - Data type : character varying(가변적인 텍스트의 길이) - Length/Percision:50(최대 기록할 글자 수) - Not NULL(제목은 무조건 하나씩 있어야 함)
  3) Name : body - Data type : text(긴 텍스트를 허용) - Not NULL x (본문은 없을 수도 있기 때문)  
  4) Name : created - Data type : timestamp with time zone (시간과 날짜를 선택할 때) -Not NULL (시간과 날짜는 반드시 있어야 하기 때문) + Default : now() (행을 추가 할 때 자동으로 시간이 기록되도록)
     ![[Pasted image 20260115110746.png|450]]
     : table을 만들 때 사용될 SQL문
     <br>
- ### ==**SQL을 이용해 행을 조작하는 방법**==
  - ==**S**==tructured : 구조화된
  - ==**Q**==uery : 질의
  - ==**L**==anguage : 언어
    -> Client가 Server에게 여러가지 요청을 전달할 때 사용하는 언어
  - ==**SQL로 CRUD하는 방법**==
    - ==**C**==reate -> ==Insert==
    - ==**R**==ead -> ==Select==
    - ==**U**==pdate -> Update
    - ==**D**==elete -> Delete
    1) ==**Insert**==
       - 방법 1) GUI도구를 사용하여 행 추가
       ![[Pasted image 20260115112018.png|450]]
       - 방법 2) SQL문을 입력하여 행 추가
       ![[Pasted image 20260115112618.png|450]]
    2) ==**Select**==
       - **현재 가지고 있는 data** : ![[Pasted image 20260115113134.png|300]]
       - **data를 읽는 방법 1) **
         -> * : 가지고 있는 모든 data를 읽을 때 사용
         ![[Pasted image 20260115113421.png|300]] 
       - **data를 읽는 방법 2)**
         -> 가장 먼저 해야 할 것 : data 줄이기
         ![[Pasted image 20260115113937.png|300]]
         -> **WHERE 문** : 행을 제한 
         (ex. id = 1 -> id가 1인 값만 / id <> 1 -> id가 1인 값 제외한 값 / id > 1 -> id가 1보다 큰 값)
         + WHERE id > 1 ORDER BY id **DESC** : id가 1보다 큰 값들 중에 큰 순서대로 나열
         + WHERE id > 1 ORDER BY id **ASC** : id가 1보다 큰 값들 중에 작은 순서대로 나열
         + **LIMIT** : 양을 직접 제한
    3) ==**Update**==
       - ==필수 : **WHERE문으로 id를 지정**==
         (안 할 시에는, 모든 행이 수정됨)
       ![[Pasted image 20260115114922.png|450]]
    4) ==**Delete**==
      - ==필수 : **WHERE문으로 id를 지정**==
	     (안 할 시에는, 모든 행이 삭제됨)
	     ![[Pasted image 20260115115247.png|450]]


---
- ==**JOIN**== : 관계형 데이터베이스의 정체성
  -> ex> 사용자 + 글 등 분리된 table을 하나의 table로 합쳐서 가지고 올 수 있는 기능
  <br>
- ==**Relational Data Modeling**== : 복잡한 application을 위한 table을 구성하려고 하면, table을 분류하는 방법
  <br>
- ==**INDEX**== : 데이터 조회의 시간을 단축하기 위한 방법
  -> 성능 향상의 핵심
  <br>
- ==**BACKUP**== : 데이터를 안전하게 보관하고 복원하는 능력
