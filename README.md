# DAY_05
데이터베이스
DDL/DML

--------------------
DB조회
--------------------
show databases;

--------------------
DB위치 지정
--------------------
use mysql;

--------------------
테이블 확인
--------------------
show tables;
select * from user;


--------------------
DB 생성
--------------------
db생성(TUI)
create database testdb;
show databases;


--------------------
Table 생성
--------------------
table 생성(GUI) - 생략

table 생성(TUI)
use testdb;
show tables;
mysql> create table tbl_user(
    -> user_id varchar(10) primary key,
    -> user_password varchar(100) not null,
    -> user_name varchar(45) not null );
Query OK, 0 rows affected (0.02 sec)

mysql> show tables;
+------------------+
| Tables_in_testdb |
+------------------+
| tbl_user         |
+------------------+
1 row in set (0.00 sec)

mysql> desc tbl_user;
+---------------+--------------+------+-----+---------+-------+
| Field         | Type         | Null | Key | Default | Extra |
+---------------+--------------+------+-----+---------+-------+
| user_id       | varchar(10)  | NO   | PRI | NULL    |       |
| user_password | varchar(100) | NO   |     | NULL    |       |
| user_name     | varchar(45)  | NO   |     | NULL    |       |
+---------------+--------------+------+-----+---------+-------+
3 rows in set (0.00 sec)


--------------------
Table 생성(문제)
--------------------
테이블 생성합니다(TUI)
테이블명 : tbl_product
컬럼종류
prod_id		int 		primary,
prod_name 	varchar(100) 	not null,
prod_category 	varchar(10)	null,
prod_details	varchar(1024)	null,
reg_date	datetime	not null,
prod_price	int		not null

[참고 - create]
user testdb;
create table 테이블명(
	컬럼명 자료형 제약조건,
	컬럼명 자료형 제약조건,
	컬럼명 자료형 제약조건,
...
);
--------------------
Table 생성(정답)
--------------------
mysql> create table testdb.tbl_product(
    -> prod_id int primary key,
    -> prod_name varchar(100) not null,
    -> prod_category varchar(10) null,
    -> prod_details varchar(1024) null,
    -> reg_date datetime not null,
    -> prod_price int not null);
Query OK, 0 rows affected (0.02 sec)



--------------------
컬럼 추가 alter
--------------------
mysql> alter table tbl_user add column user_tel varchar(30) null after user_name;
mysql> desc tbl_user;
+---------------+--------------+------+-----+---------+-------+
| Field         | Type         | Null | Key | Default | Extra |
+---------------+--------------+------+-----+---------+-------+
| user_id       | varchar(10)  | NO   | PRI | NULL    |       |
| user_password | varchar(100) | NO   |     | NULL    |       |
| user_name     | varchar(45)  | NO   |     | NULL    |       |
| user_tel      | varchar(30)  | YES  |     | NULL    |       |
+---------------+--------------+------+-----+---------+-------+


--------------------
컬럼 삭제 alter
--------------------
mysql> alter table tbl_user drop user_password;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
mysql> desc tbl_user;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| user_id   | varchar(10) | NO   | PRI | NULL    |       |
| user_name | varchar(45) | NO   |     | NULL    |       |
| user_tel  | varchar(30) | YES  |     | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)



--------------------
컬럼 수정 alter
--------------------
mysql> alter table tbl_user change column user_tel user_phone varchar(100) not null;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tbl_user;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| user_id    | varchar(10)  | NO   | PRI | NULL    |       |
| user_name  | varchar(45)  | NO   |     | NULL    |       |
| user_phone | varchar(100) | NO   |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
3 rows in set (0.00 sec)


--------------------
alter명령어
--------------------
tbl_product 의 구조를 다음과 같이 수정하세요
Column 추가 : amount int not null 
Column 수정 : product_price -> product_price varchar(100) null
Column 삭제 : product_details

column 추가 : alter table 테이블명 add column 컬럼명 자료형 제약조건
column 수정 : alter table 테이블명 change column 기존컬럼명 변경컬럼명 변경자료형 제약조건
column 삭제 : alter table 테이블명 drop 컬럼명


--------------------
alter명령어(정답)
--------------------
mysql> alter table tbl_product add column amount int not null;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table tbl_product change column prod_price prod_price varchar(100) null;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table tbl_product drop column prod_details;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0



--------------------
값삽입(DML-SELECT,INSERT)
--------------------
mysql> select * from tbl_user;
Empty set (0.00 sec)

mysql> desc tbl_user;
+------------+--------------+------+-----+---------+-------+
| Field      | Type         | Null | Key | Default | Extra |
+------------+--------------+------+-----+---------+-------+
| user_id    | varchar(10)  | NO   | PRI | NULL    |       |
| user_name  | varchar(45)  | NO   |     | NULL    |       |
| user_phone | varchar(100) | NO   |     | NULL    |       |
+------------+--------------+------+-----+---------+-------+
3 rows in set (0.00 sec)


mysql> insert into testdb.tbl_user(user_id,user_name,user_phone) values('user10','홍길동','010-222-3333');
Query OK, 1 row affected (0.00 sec)

mysql> insert into testdb.tbl_user values('user20','남길동','010-555-6666');
Query OK, 1 row affected (0.00 sec)

mysql> select * from tbl_user;
+---------+-----------+--------------+
| user_id | user_name | user_phone   |
+---------+-----------+--------------+
| user10  | 홍길동    | 010-222-3333 |
| user20  | 남길동    | 010-555-6666 |
+---------+-----------+--------------+
2 rows in set (0.00 sec)

mysql> select user_id,user_name from tbl_user;
+---------+-----------+
| user_id | user_name |
+---------+-----------+
| user10  | 홍길동    |
| user20  | 남길동    |
+---------+-----------+
2 rows in set (0.00 sec)

--------------------
값수정(DML-UPDATE)
--------------------
mysql> select * from tbl_user;
+---------+-----------+--------------+
| user_id | user_name | user_phone   |
+---------+-----------+--------------+
| user10  | 홍길동    | 010-222-3333 |
| user20  | 남길동    | 010-555-6666 |
+---------+-----------+--------------+
2 rows in set (0.00 sec)

mysql> update tbl_user set user_name='철수' where user_id='user20';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from tbl_user;
+---------+-----------+--------------+
| user_id | user_name | user_phone   |
+---------+-----------+--------------+
| user10  | 홍길동    | 010-222-3333 |
| user20  | 철수      | 010-555-6666 |
+---------+-----------+--------------+
2 rows in set (0.00 sec)


--------------------
값삭제 (DML-DELETE)
--------------------
mysql> delete from tbl_user where user_id='user10';
Query OK, 1 row affected (0.00 sec)

mysql> select * from tbl_user;
+---------+-----------+--------------+
| user_id | user_name | user_phone   |
+---------+-----------+--------------+
| user20  | 철수      | 010-555-6666 |
+---------+-----------+--------------+
1 row in set (0.00 sec)

--------------------
DML 문제
--------------------
tbl_product안에 다음과 같은 작업을 수행하세요
[값 추가]
prod_id		prod_name	prod_category	reg_date	prod_price	amount
1111		LG_GRAM_2023	가전		2024/01/22	830,000		100	
1112		SAMSUNG_FLEX2	가전		2024/01/22	3,000,000	50
2000		대우_통돌이_01	가전		2024/01/22	590,000		25
3001		이것이리눅스다	도서		2023/01/22	30,000		1000


[값 수정]
prod_category가 '가전'인 모든행의 reg_date를 2023/01/01 로 변경하세요


[값 삭제]
prod_id가 1111인 행을 삭제하세요
문제
DB확인  : show databases;
Tbl확인 : show tables;
Source가져오기 : source sql파일명
Tbl구조 : desc 테이블명
삽입	: insert into 테이블명(열1,열2...) values(값1,값2...);
수정	: update 테이블명 set 열이름=값,열이름=값 where 열이름=값;
삭제	: delete from 테이블명 where 열이름=값;
조회	: select * from 테이블명;

DB 생성 : create database 테이터베이스명;
Tbl생성 : create table 테이블명(열1 자료형 [제약조건],열2 자료형 [제약조건]..);
Tbl구조 변경 : [열추가] alter table 테이블명 add column 열이름 자료형 [제약조건] [after 열이름]
Tbl구조 변경 : [열변경] alter table 테이블명 change column 기존열이름 바꿀열이름 자료형 [제약조건]
Tbl구조 변경 : [열삭제] alter table 테이블명 drop column 열이름

Tbl삭제 : 

DB 삭제 : drop DB명;
Tbl삭제 : drop 테이블명

접속하기 : 
mysql -u 유저명 -p -h ServerIP
