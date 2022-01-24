

mysql 실행 : cd /usr/local/mysql/bin => ./mysql -u root -p => 비밀번호 입력

DB 생성 : create database  `DB이름` characte rset utf8 collate utf8_general_ci;

DB 삭제 : drop ``DB이름`

DB 사용 : use `DB이름` => 이후 내린 명령들은 DB이름 대상으로 SQL이 작동함.

스키마 : 테이블에 적재될 데이터의 구조와 형식을 정의(설계도)

테이블 생성 : create table 테이블 이름 (

​					컬럼 이름 db_type,

​					);

테이블 보기 : show tables;

테이블 구조 보기 : desc(description) 테이블 이름;

데이터 타입 특징:

- CHAR() : 고정문자이기 때문에 검색에서 효율적(도시명 같이 정형화된 데이터에 유리)
- VARCHAR() : 가변문자이기 때문에 용량 측면에서 효율적(주소같이 가변문자열에 유리)
- TINYINT < SMALLINT < MEDIUMINT < INT < BIGINT
- DATE : YYYY-MM-DD
- DATETIME : YYYY-MM-DD HH:MM:SS
- TIMESTAMP : YYYYMMDDHHMMSS
- ENUM() : 정해진 타입을 강제

---

INSERT

- insert into 테이블이름 (column1, colum2, ...) values (value1, value2, ..)  => 컬럼 정의 순서대로 value 삽입

- insert into 테이블이름 values (value1, value2, ..) => 컬럼 정의 순서대로 value를 넣아야 함

UPDATE

- update 테이블명 set 컬럼1 = 컬림1 값, 컬럼2 = 컬럼2 값... where 대상이 될 컬럼 명 = 컬럼 값

SELECT(조건에 따라 DB 성능에 영향을 미침)

- select 컬럼명1 ,컬럼명2(보고싶은 컬럼만 조회 가능) // => 생략가능 [from 테이블명] // where 대상 지정 <and | or  대상 2 ...>

  ​																								  [group by 그루핑 기준 컬럼명] => 그루핑 

  ​																			 					  [order by 컬럼명 [asc | desc] => 정렬(두개가 오면 제일 앞이 기준)

  ​																								   [limit offset, 조히할 행의 수] => 0, 2(0번째 row 부터 2개), 페이징 가능

- Index: 색인, 조회 시 원하는 행을 빠르게 찾을 수 있는 데이터
  - primary : 테이블마다 딱 하나의 PK만 가능, where 사용 가능
  - normal : 여러개로 키 지정 가능, 중복 허용
  - unique : PK와 유사하지만 여러개 지정 가능 => unique key 키 이름  (컬럼명)
  - foreign
  - full text : 스토리지 엔진 중 myisam에서만 사용 가능, InnoDB는 불가, 영어 디폴트 => lucene, spginx 전문검색 엔진으로 대체 가능

- join : 테이블간의 관계성에 따라서 복수의 테이블을 결합 => 하나의 테이블인것 처럼 결과 출력
  - outer join : 매칭되는 행이 없으면 null
    - left : select 가져올 컬럼 from 가져올 테이블 as 별명(from 앞에서 사용 가능) left join 테이블(왼쪽의 테이블일 기준으로 오른쪽을 가져옴) 		on(결합 조건) 왼쪽 id = 오른쪽 id
    - right
  - inner join : 매칭되는 행이 있어야 결과를 가져옴