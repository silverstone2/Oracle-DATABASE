# Oracle(DATABASE)
Oracle(DATABASE)

## 설치 및 초기 설정
- www.oracle.com 에서 oracle 설치(설치 시 비밀번호는 기억하기 쉬운 걸로 설정! ex) oracle)
- 설치 완료 후 cmd(명령 프롬포트)창에서 sqlplus.exe를 입력해 Oracle 프로그램 실행<br>
(윈도우+R을 입력해 실행창에서 바로 sqlplus 입력해도 무관!)
- 초기 관리자 계정으로 로그인하여 테스트 혹은 작업할 계정을 생성해준다.<br>
이 때 관리자 계정은<br>
관리자 계정 : system <br>
관리자 계정 비밀번호 : 설치 시 설정한 비밀번호

* 계정 생성 방법
- 오라클 설치 후 명롱 프롬프트(cmd)창에서 oracle 실행(sqlplus.exe 실행)<br>
- 사용자명 / 비번 : system / oralce으로 생성
- CREATE USER acorn IDENTIFIED BY acorn1234(사용자 계정은 acorn / 비밀번호는 acorn1234로 생성)

------------------------


* cmd - sqlplus.exe
- 사용자명 / 비번 : systme / oracle

- (테스트)사용자 계정 & 비밀번호 만들기
- CREATE USER acorn IDENTIFIED BY acron1234;

- 테스트 계정 / 비밀번호 : acorn / acorn1234

- 계정 생성후 접속 권한과 자원을 줘야 함
- GRANT CONNECT, RESOURCE TO acorn;
            -> 위의 과정이 초기설정 완료임

- command창 닫고 acorn계정으로 재접속하기

 DB에 저장하는 정보 종류
 1. 숫자
 2. 문자
 3. 날짜
를 주로 저장을 함.

- key value의 쌍으로 저장하는 db도 있지만
- oracle의 경우는 표(table) 형식으로 정보를 저장한다.

- oracle에서는 테이블의 칼럼을 정해줘야하고 저장하는 정보의 type도 정해줘야 한다.
- oracle = 정보가 추가/삭제될때 row가 추가/삭제되는 형식

- 파일로 저장시 데이터 신뢰성 확보 x / 용량도 많음 / 찾기 힘듬

* oracle 명령어는 대/소문자를 구별하지 않는다!
명령어를 대문자로 표기하면 구분하기 쉽다!
; 이 나오기 전까지는 실행을 안함(그냥 enter누르면 개행이 됨)

CREATE 명령어 : 무언가를 새로 생성하는 명령어
DROP 명령어는 삭제하는 명령어

()안에서 num 칼럼명 NUMBER은 숫자타입, VARCHAR2는 문자타입이고 VARCHAR2 옆의 숫자는 최대 문자크기를 말한다.
* 영문자의 경우에는 1씩 차지하나 한글은 3씩 차지한다.

테이블의 구조를 보고 싶을 땐 'DESC 테이블명'을 치면 된다.
문자를 입력할 때는 싱글 따옴표를 사용한다.

* 정보 입력한거 조회하는 방법
SELECT 요소명 FROM 테이블명; 요소명 대신에 * 을 넣으면 전체를 조회함.
조건달아서 조회할 때는 SELECT 요소명 * FROM 테이블명 WHERE 타입 = 값;
명령어 : SELECT / UPDATE / INSERT / DELETE => commit하기 전까지는 임시반영의 개념

* 갱신하는 방법
UPDATE 테이블명 SET 수정할 사항 WHERE 수정할 테이블의 로우나 칼럼;

* 삭제하는 방법
DELETE FROM 테이블명 WHERE 삭제하려는 정보;

테이블이나 데이터를 수정후 commit을 해야 다른 세션에서 확인이 가능하다.

primary key라는 것을 통해 제약조건을 적용시킬수 있음.
primary key는 해당 칼럼에 대한 데이터는 무조건 입력을 해야함.
동일한 조건을 적게 되면 무결성 제약 조건에 위배된다는 에러메세지 출력됨.
* 선생님이 주신 pdf 파일 참조할 것

특정 하나만 삭제 수정을 하려면 row를 대표할 수 있는 primary key를 활용해야함.




<질문>
선생님 PDF 파일에는 VARCHAR2(50) => 가변 문자열 최대 영문자 50 (한글:25) 글자로 되어있는데 아까 한글은  3정도 먹는다고 하셨는데 둘중에 뭐가 맞는건가요?!


<답변>
한글을 처리하는 방식은 command 프롬프트 환경에서 한들을 처리하는 방식 때문에 3을 먹는거구요
나중에 실제로 java application 을 활용해서 한글을 저장하면 2 를 먹게 됩니다.


변수 크기를 크게 설정하고 값을 입력해주면
컬럼이 밀리는 현상 발생한다 이때 쓰는 방법

SET LINESIZE 200(숫자는 유동적)
COLUMN name FORMAT A10 -> 숫자는 글자 자릿수를 의미
COLUMN addr FORMAT A15
하지만 위의 과정은임시반영이기에 완전반영이 필요할 땐 commit을 실행시켜야함.

DELETE FROM member; 처럼 조건을 안주면 전체삭제가됨.
복구하고 싶으면 ROLLBACK; 명령어를 치면 됨.

날짜 데이터는 SYSDATE를 통해서 나타낼수 있음
- oracle에서도 javascript에서처럼 함수를 호출할때는 ()를 쓰지만
  아무것도 전달하지 않을 때는 소괄호를 사용하지 않는다.

  oracle에서는 우리가 table을 만들지 않아도 dual이라는 테이블이 존재함.

  SELECT test_seq.NEXTVAL FROM dual; 에서 NEXTVAL는 순차적인 값을 보여줌.


계정 쉽게 생성 + 테이블 정보까지 받아오는 방법
-> scott이라는 test계정을 만들고 tiger라는 비밀번호와 안의 테이블까지 가져오는 방법
@하고 파일을 끌어오면 됨. 그러면 파일안의 내용을 모두 실행을 함
(계정 생성부터 테이블 생성 및 샘플데이터 입력까지 모두 되어 있음)


정렬을 쓸때는 ORDER BY 명령어를 쓰고 ASC은 오름차순 DESC는 내림차순이다.

WHERE 절의 효과는 row를 추려내는 효과가 있다!

일시적으로 세션에서 컬럼 깔끔하게 보는 코드
SET LINESIZE 200
COLUMN ENAME FORMAT A10
COLUMN JOB FORMAT A10

명령어는 대소문자를 안가리지만 변수는 가림

칼럼에 별칭을 붙일 수 있다.
칼럼명 뒤에 AS라고 적으면 된다.(AS ALIAS의 약자)
AS는 따옴표로 안감싸도 되고 띄어쓰기 안해도 됨.

SQL연산자 주에서
%j% 에서 %~%는 해당 글자 포함되는 거 출력
_A%에서 _는 한글자를 의미함.
            
            
            
------------------------------------
* 20220714
            
host라고 치면 윈도우 환경으로 나감.
exit치면 다시 돌아옴

SPOOL my_spool.txt 라고 치면 지금부터 내가 기록한 것들은 텍스트파일로 저장한다는 뜻
저장을 여기까지만하겠다고 하면 SPOOL OFF 입력하면 됨.
cmd 안에서 확인할 때는 type spool.txt락 입력한다. 이때 확인은 host명령어를 사용해 윈도우 환경에서 확인해야한다.

dual은 dummy table

중간에 한글 넣고 싶으면 ""로 한글을 감싸줘야함.


DATE -> CHAR : TO_CHAR()
CHAR -> DATE : TO_DATE()
---------------------여기까지 단일행 함수=--------------------



복수행 함수
여러개의 로우 당 하나의 값을 반환하는 함수
group by 절을 쓸떄 select와 from사이에는 group을 대표할 수 있는 값만 써야함


GROUP BY 는 로우에 대한 조건 절이고

HAVING절은 특정 조건을 주고 싶을 때 쓴다.


ORACLE은 JOIN절을 사용하지 않는다면 FROM절에 있는 모든 경우의 수를 다 조합해서 표현한다.
조건이 여러개라면 AND를 통해서 여러개의 조건을 적용시킬 수 있다.
테이블명이 길면 제일 앞글자를 따서 별칭을 이용해 코드를 작성할 수 있다.
ANSI 조인을 사용하면 가독성이 더 좋아짐.

FROM EMP
INNER JOIN DEPT ON
-> EMP 안에 JOIN을 조인해주겠다는 뜻이고 ON 다음에 JOIN 조건을 적어주면 됨, 

USING 절을 활용해서 ANSI JOIN을 좀더 쉽게 할 수 있음
(단 조인을 쓸때 같은 칼럼일때만 USING을 사용해야 한다.)
ORACLE에서 NULL은 비교 불가이기 때문에 연산자를 써야함.

INNER JOIN은 DEFAULT라서 생략해도 가능하다

OUTER JOIN : (+)를 WHERE절 왼쪽 조건뒤에 붙여야 함 -> 보이지 않았던 정보도 OUTER JOIN을 통해 보여줌.
오른쪽의 칼럼이 왼쪽보다 하나 이상 많아서 범주를 벗어나 오른쪽이 삐져나오면 RIGHT OUTER JOIN이라고 함.

            
            ------------------------------------------------------------------------
            
            * 20220715
            rownum은 행번호를 붙이고 싶을 때 사용하는 명령어


서브쿼리는 메인쿼리보다 먼저 실행됨.
단일행 쿼리는 = 와 같은 동등연산자로 비교 가능
다중행 쿼리는 단일행과는 다르게 = 와 같은 동등연산자로 비교불가
그래서 in all any exist를 사용한다.
group by는 서브쿼리가 리턴하는 행의 개수가 여러개일때 사용

* 특정 로우의 위아래값을 같은 로우에 표시하고 싶다면?
lead와 lag는 값이 없을 때 0가 default값이 된다.

문자열로 할때는 문자열의 기본값음 'no'또는 '없음'이라고 하면 됨.




----------오후 시작-----------
localhost:8080/apex 오라클 gui

관계형데이터베이스


dml = commit하기 전까지는 임시반영
* 참고사항 :  primary key = not null + unique
시퀀스 생성

oracle에서 command창은 직접 commit이나 rollback을 해줘야 함,. 

참조하는 방법 -> db 참조방법 사진 참고 (regerence 사용해서 참조)


DESC USER_TABLES는 오라클에서 제공해주는 테이블관련 명령어임.
USER_ 뒤에 단어 붙이면 유저에 대한 정보가 나타남
DESC USER_CONSTRAINTS는 제약조건에 대한 경고를 조회할 수 있는 커리



TABLE_NAME                                                   CONSTRAINT_NAME
          CO
------------------------------------------------------------ ------------------------------------------------------------ --
EMP2                                                         SYS_C004008
          R  REFERENCE
MEMBER                                                       SYS_C004004
          C  NOT NULL
EMP                                                          FK_DEPTNO
          R 
DEPT                                                         PK_DEPT
          P  PRIMARY KEY
EMP                                                          PK_EMP
          P
MESSAGE                                                      SYS_C004003
          P
BIN$6bzPFNdCS4CrUAcWrG0VTA==$0                               BIN$RYNPWeFqQeC3xFOBke2w5w==$0
          P
BIN$ltKOZLEMTKGKfQk7YZLwtg==$0                               BIN$fzww+3yYRC2i17Ln9WYk9A==$0
          P
MEMBER                                                       SYS_C004005
          P
DEPT2                                                        SYS_C004006
          P
EMP2                                                         SYS_C004007
          P

11 개의 행이 선택되었습니다.
fk = 외래기 foreign key





제약조건의 이름을 이쁘게 지으면 관리하기 편해짐.
제약 조건의 이름을 부여하지 않으면 임의로 시스템이 부여함.


객체를 삭제할 땐 DROP 명령어 사용(테이블 삭제는 rollback이 안됨 / 걍 새로만들기)


column level 제약조건 : 칼럼을 정의할 때 바로 정의하는 것
table level 제약조건 : 칼럼 정의할 때 정의 안하는 거
-> 뒤에 언급해줄때 어디에 적용할건지 ()안에다가 명시를 해줘야함.
외래키의 제약조건의 경우는 foreign KEY(참조할 칼럼)이라고 명시해줘야한다.



-----------------
###20220718

-오전-
ORACLE에서 계정을 삭제할 때는 테이블이나 객체가 있을 경우 바로 삭제가 안된다.
REM은 주석
group by로 묶을 때는 그 값을 대표하는 값만을 묶어야 오류가 안생긴다.
USING 쓰면 약자 사용 금지 ex)e.ename 사용 금지


ANSI와 OUTER를 같이 쓸때 FROM에 있는게 왼쪽이고 JOIN다음에 오는게 오른쪽임


테이블에서 전체의 값이 아닌 특정 구간의 데이터만을 빼올려면 서브쿼리를 이용해야한다.
방법 : 정렬을 실시한 후 정렬한 것을 괋호로 묶는다(행번호를 부여해야함)
       이 때 묶은 테이블은 이미 정렬이 된 테이블이며 이후 행번호를 부여한다.
       select 옆 result1.*은 정렬된 select문에대한 값을 의미

rownum은 select한 시점에서 숫자를 반환하는 형식의 함수!
서브쿼리로 묶을 때 where절은 사용불가능함
where절을 써버리면 선택된 레코드가 없다고 뜸(where절의 조건은 false로 반환됨)


