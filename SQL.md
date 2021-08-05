# SQL문

## 1.기본

- 데이터 베이스 : 기업이나 조직에서 필요한 데이터를 저장하는 것(데이터의 집합)

- DBMS(Data Base Management System)

  - 데이터를 관리하는 시스템

  - 데이터의 유지보수 및 보안을 유지

  - 소프트웨어

  - `DBMS`를 이용하여 데이터를 입력 수정 삭제 조회 할 수 있다.

  - 종류로는 계층적데이터베이스, 네트워크데이터베이스, 관계형데이터베이스

  - 장점 : 데이터의 일관성 유지

    ​          무결한 데이터를 유지

    ​          데이터를 공유

​                        중복을 최소화(관계형데이터베이스)     

- DBA(Data Base Administrator)
  - 데이터를 관리하는자
  - 데이터설계, 인덱싱등 튜닝작업
  - 데이터백업등을 처리



- Oracle (관계형데이터베이스)

  - 2차원 테이블로 데이터를 저장

  - 관계형데이터베이스에서 테이블은 성격별로 각각 정의해서 관리

  - 데이터의 무결성을 보장

  - 데이터처리를 위해서 SQL문을 사용

  - 테이블 설계시 정의할 수 있는 컬럼

    - 기본키(primary key) : 테이블에서 레코드를 구한부기 위해서 사용하는 키 

      ​                                      중복과 공백을 허용하지 않음

    - 외래키(foreign key) : 기본키를 참조하는키

      ​                                     테이블과 테이블의 관계를 나타내기 위해서 사용

      ​                                     기본키에 정의되지 않은 값을 사용할 수 없다

  - 참조 무결성이 강화

  - 테이블을 분리해서 설계(테이블 정규화)

  - 테이블 정규화 : 하나의 테이블로 표현하기에 중복이 많이 발생하는 경우 두 개 이상의 

    ​                           테이블로 정의하여 관리한다.



## 2. SQL(structured query languge)

- 데이터를 조회 입력, 수정, 삭제 저장하는데 사용되는 언어
- DML(데이터조작어) : insert, update, delete
- DDL(데이터정의어) : create table, alter table, drop table 
- DCL(데이터제어어) : grant, revoke
- TCL(트랜잭션처리어) : commit, rollback
- Query : 데이터의 조회 : 기본조회, 함수적용조회, 그룹화(집계), 조인, 서브쿼리
- 테이블(Relation)구성요소
  - 컬럼(열,column)`<Attribute>` 
  - 레코드(행,row) `<Tuple>`



## 2.0 초기 실행

- 사용자계정 만들기

  - 관리자계정 접속

    - ```sql
      conn 계정명/계정패스워드
      ```

  - 계정 생성하기

    - ```sql
      create user 계정명 identified by 패스워드xxxxxxxxxx
      ```

  - 권한 부여

    - ``` 
      grant connect, resource to 계정명
      ```

  - 샘플데이터 추가

  - 테이블확인

    - ```sql
      select * from tab
      ```

- 실습계정

  - ```sql
    conn hr/hr 
    conn system/manager
    alter user hr account unlock;
    conn hr/hr
    ```

- 계정비밀번호 변경

  - ```sql
    conn system/manager
    alter user 계정이름 identified by 변경할 비밀번호
    ```

- 환경구축

  - 오라클 설치시 레지스트리에 기록 되므로 오라클 제거 or 수정시 반드시 setup.exe로 할것
  - 관리자계정 접속
  - 사용자계정 생성
  - 사용자계정 권한 설정 – 관리자계정에서 작업
  - 사용자계정으로 접속해서 데이터 저장

- 호스트 확인

  - ```
    oraclexe>app>app>product>11.2.0>server>network>admin>>lister.ora & tnsnames.ora
    ```

- 오류발생시 확인

  - ``` 
    window 서비스 > oracleserviceXE & oracleXETNSlistener (항상 실행상태 일 것)
    ```

    



### 2.1 기초 코딩

- select기본

  ```
  [구문] 
  
  select 컬럼명, 컬럼명....
  
  from 테이블명1, 테이블2....
  ```

  - `sql`문은 대소문자를 구분하지 않는다
  - `sql`문은 명령문의 끝에 ;을 추가한다
  - `select`절 뒤에 컬럼명 대신` *`을 추가하면 모든 컬럼을 조회하겠다는 의미
  - 컬럼과 컬럼을 구분하기 위해` ,`를 이용하여 구분
  - 컬럼명에 `alias`(별칭)을 사용할 수 있다. 별칭을 사용하면 컬러명 대신 별칭이 컬럼명처럼 표기된다.
  - 컬럼명` alias`     -  컬럼명 `as alias`
  - `select deptno` 부서코드,  `empno as `사번
  - `alias`에 특수문자나 공백을 포함하고 싶은 경우` “”`로 표시
  - 함수나 산술연산을 컬럼에 적용할 수 있다
  - 사용할 수 없는 값이 저장되어 있지 않은 것을 `null`이라고 한다.
  - `null`은 0과 다르며 연산을 해도 결과가 표시되지 않는다(연산 결과도` null`)
  - 연결연산자`(||)`를 사용해서 컬럼 여러개를 하나의 컬럼으로 표기 가능(문자열도 연결가능)
  - `distinct`를 이용하면 중복을 제거 할 수 있다. (값이 동일한 레코드 제거)
  - 오라클에서 문자열은 `‘’`로 표기

- select문 정의 :  select > from > where > group by > having >order by

- select문 실행 순서 : from > where > group by > having >select >order by 

​	

- select문에 조건을 적용

  ``` 
  [구문] 
  select 컬럼명, 컬럼명....
  from 테이블명1, 테이블2. ...
  where 조건(컬럼명 연산자 비교할값)
  ```

  - 숫자데이터를 이용해서 비교연산자(대소문자구분)를 사용 가능(`>`,`>=`,`<`,`<=`,`=`,`<>`)

  - 결과가` true`나` false`를 리턴하도록 식을 구성

  - 오라클에서 날짜, 문자열은 `‘’`로 표시

  - 조건이 여러개인 경우 `and`와 `or`연산자를 이용해서 처리

    ​                                      `and` :모든 조건이 만족하는 경우` true`

    ​                                      `or` : 모든 조건 중 하나만 일치 하는 경우` true`

    ​                                     where 컬럼명1 연산자 조건1 and&or 컬럼명2 연산자 조건2....

  - 하나의 컬럼에 대해 조건으로 명시된 값이 어떤 범위안에 포함되는 값이 경우(사잇값)
    - 컬럼명 between A and B
  - 동일한 컬럼에 일치하는 값에 대해  or연산을 적용하는 경우 in연산자 
    - 컬럼명 in (값1, 값2, 값3.....)
  - not 부정문
    - `null`인 데이터 조회 : is null
    - `null`이 아닌 데이터 조회 : is not null
  - like연산자와 와일드카드 이용하여 비교가능( 정확히 일치하지 않아도 비교가능)
    - `% `: 모든문자열        ` _ `: 한 글자 .
  - 오라클에서 비교되는 값을 이터럴이라 한다.
  - 문자열,날짜 `: `로 표시     `- `숫자는 숫자만 표시



- select문과 정렬

  ```
  [구문]
  select컬럼명
  from 테이블명1
  where 저간
  order by 정렬할 컬럼명 정렬기준
  ```

  - 데이터를 정렬할 때 사용

  - 정렬기준  

    - 오름차순 : asc (A>Z, 1>9 ,ㄱ>ㅎ)

      내림차순 : desc (Z>A , 9>1, ㅎ>ㄱ)

  - 정렬기준 생략시 오름차순 정렬



## 2.2 함수

- 실행구분 
  - 단일행함수
  - 그룹함수
- 카테고리별 구분
  - 문자열 관련 함수
  - 숫자함수
  - 변환함수
  - 날짜함수
- 개요
  - `where`절에 그룹함수를 사용할 수 없다
  - `select`절에 일반 컬럼과 그훕함수를 같이 사용 할수 없다



### 2.2.1 문자열 함수

- lower(문자열 or 컬럼)  : 문자열을 소문자로 변환

- lower(문자열 or 컬럼) : 문자열을 소문자로 변환

- initcap(문자열 or 컬럼) :  문자열의 첫글자를 대문자로 변환

- length(문자열 or 컬럼) : 문자열의 길이를 리턴

- concat(문자열1 or 문자열2) : `||`연산자와 동일하게 실행, 문자열과 문자열을 연결

- substr(문자열, 숫자1, 숫자2) :  전체문자열에서 원하는 문자열만 추출                      

  ​                                                     숫자1 : 시작위치 (음수로 표현시 오른쪽부터 시작위치)

  ​                                                     숫자2: 추출한 문자열의 길이

- instr(문자열1, 문자, 숫자1, 숫자2) : 특정문자의 위치를 추출

  ​                                                            문자열1 : 문자를 찾을 문자열이나 칼럼

  ​                                                            문자 : 찾고자 하는 것

  ​                                                            숫자1 : 찾기 시작할 위치

  ​                                                            숫자2 :` n`번째 만나는 문자 

- lpad(문자열1,숫자,문자) : 문자열1을 지정된 숫자의 길이만큼 표시, 남는 자리는 문자로 채움  (왼쪽에서 채울 문자를 표기)

  ​                                              문자열1 : 원본문자

  ​                                             숫자 : 표기할 문자열의 길이

  ​                                             문자 : 채울문자

- rpad(문자열1,숫자,문자) 문자열1을 지정된 숫자의 길이만큼 표시, 남는 자리는 문자로 채움  (오른쪽에 채울 문자를 표기)

- ltrim(문자열 or 칼럼, 삭제할 문자) 지정된 칼럼이나 문자열에서 연속으로 나오는 삭제할 문자를 지운다 (왼쪽에서 지운다)
- rtrim(문자열 or 칼럼, 삭제할 문자) 지정된 칼럼이나 문자열에서 연속으로 나오는 삭제할 문자를 지운다 (오른쪽에서 지운다)



### 2.2.2 숫자함수

- round(반올림할 숫자,칼럼,숫자) : 반올림 숫자(양수, 0, 음수)

  - ```sql
    elect round (1128.4567,2) from dual;

- trunc(버림할 숫자,칼럼,숫자) :버림 숫자(양수, 0, 음수)

  - ```sql
    elect months_between ('2021/08/01','2021/01/02'),
    trunc(months_between('2021/08/01','2021/01/02'),0) from dual;
    ```

- mod(숫자1, 숫자2) : 숫자1을 숫자2로 나눈 나머지

  - ```sql
    select mod(10,3) from dual;
    ```

- abs(숫자,컬럼) : 주어진 값보다 큰 가장 최소값을 구하는 함수

  - ```sql
    select abs(-2), abs(2) from dual;
    ```

- ceil(숫자,컬럼) : 절대값	

  - ```sql
    select ceil(1128.9567) from dual;
    ```



### 2.2.3 날짜함수

> 오라클에 날짜는 연산 가능, 1970/01,01기준



- months_between(날짜1,날짜2) : 날짜1(최근날짜) 과 날짜2 사이의 경과한 개월의 수

  - [실습] emp테이블에서 10번부서의 근무하는 사원들의 현재까지 근무한 개월수를 조회하기 소주점이하 버리기 

    - ```sql
      select ename, hiredate, sysdate, months_between(sysdate, hiredate),
         trunc(months_between(sysdate, hiredate),0) 개월수 from emp
         where deptno = 10;
      ```

- add_month(날짜1,숫자) ; 날짜에 숫자개월을 더함

  - ```sql
    select sysdate, add_months(sysdate,6) from dual;
    ```

  - [실습]20부서의 사원들의 입사일로부터 5개월 후의 날짜를 출력하기

    - ```sql
      elect ename, hiredate, add_months(hiredate,5)" 5개월후" 
        from emp where deptno = 20;
      ```

- last_day(날짜) : 날짜테이터의 마지막날

- next_day(날짜,요일번호) : 정의된 날짜 이후의 데이터에서 지정한 요일에 해당되는 날짜

  - ```sql
    select sysdate, next_day(sysdate,5), last_day(sysdate) from dual;
    ```



### 2.2.4 변환함수

> 데이터타입을 변환할 때 사용하는 함수



- 숫자 > 문자 > 날짜
- 숫자 > 문자 : to_char (숫자 format을 나타낼 때 사용,특수문자 사용하여 표시)

​     (날짜 > 문자)                  ` 9,0`:숫자 ` ,`:콤마  `.`:소수점  ` $,L`:통화기호  

​                                              `YYYY,YY`:년도, `MM`:월,` DD`:일, `DY`:요일,` HH`:시간,` MI`:분,` SS`:초

- ``` sql
  select to_char(sysdate,'YYYY'), to_char(sysdate,'MM'), to_char(sysdate,'DD') 
     from dual;
  ```

- 문자 > 숫자 : to_number 
- 문자 > 날짜 : to_date 



### 2.2.5 null함수

- nvl(nul이 있는 칼럼,변경할 값) : null인 경우 치환할 값은 반드시 컬럼의 타입과 일치 null값을 특정 값으로 변환

  - [실습] select ename, sal, comm, sal*12+comm 연봉 from emp; 위의 sql문을 수정하여 comm이 null이면 0이 더해져서 출력되도록 수정

    - ```sql
      select ename, sal, comm, sal*12+nvl(comm, 0) 연봉 from emp;
      ```

- nvl2(칼럼,값1,값2) null을 평가해서 null이면 값2를 아니면 값1을 리턴

  - ```sql
    select ename, sal, nvl2(to_char(comm),'영업사원', '신입사원')  from emp;
    ```





### 2.2.6 그룹함수

- ```
  [구문]
  selelct 그룹함수
  from 테이블명
  where 조건
  group by 컬럼(그룹화 하고싶은 기준)
  having 그룹화된 데이터에 명시할 조건
  order by 컬럼
  ```

- 여러 레코드의 데이터를 묶어서 처리하는 방식

- 통계작업을 위해 사용

- 그룹함수(그룹당 하나의 결과를 리턴하는 함수)를 이용해서 처리

  - ```sql
    select deptno, count(empno) from emp group by deptno order by deptno;
    ```

- select 문에는 일반 데이터조회처럼 아무 컬럼이나 저의 할 수 없다

- group by에 명시한 컬럼만 정의할 수 있다

- where절을 group by보다 먼저 실행하여 레코드를 그룹으로 나누기 전에  제외한다.

- group by전에 조건을 적용해야 한다면 where절에 명시

- group by한 후에 만들어지는 결과에 조건을 적용해야 하면  where절에 명시하지 않는다

- hvaing절에 추가

- [실습1] 직업별 인원수와 편균 sal를 출력하세요

  - ```sql
    select job , count(empno), avg(sal) from emp group by job;
    ```

- [실습2] 입사월별로 인원수를 출력하세요. 단, sal이 5000이상인 사원은 제외

  - ```sql
    select to_char(hiredate,'MM'), count(empno) from emp 
       where sal < 5000 
       group by to_char(hiredate,'MM') 
       having count(empno)>1 
       order by to_char(hiredate,'MM');
    ```

- [실습3] 부서별로 최대급여, 최소급여를 출력하세요 단, job이 PRESIDENT 인 데이터는 제외하고  최대급여가 3000이상인 부서만 

  출력하세요, 부서별로 오름차순 정리

  - ```sql
    select deptno, max(sal)최대급여, min(sal)최소급여 from emp 
       where job <> 'PRESIDENT' 
       group by deptno having max(sal) >= 3000
       order by deptno;
    ```





## 2.3 조인

- 여러테이블의 데이터를 조회하는 것을 조인

- 일반적인 경우 pk나 fk를 이용해서 조인한다

- 관계형 데이터 베이스에서 가장 기본적이고 중요

  - ```sql
    elect emp.empno, emp.ename, emp.deptno, dept.dname from emp, dept 
       where emp.deptno = dept.deptno;
    ```

  - ```sql
    select e.ename, e.empno, e.deptno, d.dname from emp e, dept d 
       where e.deptno = d.deptno;
    ```

- 조인방법

  - `from`절에 조회하고 싶은 테이블을 모두정의
  - 컬럼명을 정의할 때 컬럼며의 모호성을 피하기 위해서 테이블명을 표시
  - 보통은 테이블명을` alias`로 정의
  - 조인을 하는 경우 반드시 어떤 컬럼끼리 관계가 있는지 명시해야한다.
  - 즉. 어떤 컬럼의 값을 기준으로 원하는 값을 찾아와야 하는지 알아야 적절한 테이터를 가져올 수 있다
  - 비교해야 하는 컬럼을 명시하는 것을 조인조건이라 한다
  - 조인조건은` where`절에 정의한다.
  - 일반적으로 조인조건은` pk`테이블의 `pk`와`fk`와` fk`테이블의 `fk`키가 `=` 연산자로 처리
  - 조인조건은 테이블이 `N`개이면 `N-1`개의 조건이 필요하다
  - 조인조건을 정의하지 않거나 잘못 정의하는 경우 어떻게 비교해야 할지 애매하므로 `from`절에 명시된 모든 테이블릐 레코드를 조회해서 출력한다 이를 카티션프로덕트`(CARTESIAN PRODUCT)`라 한다.
  - 조건이` 1`개 조인조건과 무조건 `and`조건으로 연결됨
  - `select절`에 두 개 이상의 테이블의 컬럼을 표시하지 않는다고 하더라도 조건에 사용되면     조인조건을 명시해야 한다

- [실습2] DALLAS에 근무하는 사원의 사원번호, 사원명, sal 출력하시오

  - ```sql
    select e.empno, e.ename, e.sal from emp e, dept d, locations l 
         where l.city = 'DALLAS' 
         and e.deptno = d.deptno 
         and d.loc_code = l.loc_code;
    ```

- [실습3] 부서별 인원수를 출력하세요. 단, 부서명과 인원수를 출력합니다.

  - ```sql
    select d.dname, count(e.empno) 
      from emp e, dept d 
      where e.deptno = d.deptno 
      group by d.dname; 
    ```

- [실습]도시별로 근무하는 직원의 인원수를 출력하세요 )city 인원수

  - ```sql
     select l.city, count(e.empno) 
        from emp e, dept d, locations l 
        where e.deptno = d.deptno 
        and d.loc_code = l.loc_code  
        group by l.city;
    ```

  

