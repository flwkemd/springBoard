## Spring 4 + MyBatis 3 + MariaDB 기반 게시판 ##

각 내용은 다음과 같이 구성되었다.

### 1. board Step 1 (board1) ###
- List: 모든 게시물 출력
- Form: 사용자 입력 내용 저장
- Update: 사용자 입력 내용 수정
- Read:   사용자 입력 내용 보기
- Delete: 지정된 게시물 삭제

URL: http://localhost:8081/board/board1List

### 2. board Step 2 (board2) ###
- List: 페이징, 새로운 번호 부여
- Form: 입력/수정을 하나로
- Read: 조회수 
- Delete: 삭제에서 숨기기로

URL: http://localhost:8081/board/board2List


### 3. board Step 3 (board3) ###
- List: 검색, 제목을 한 줄로 표시 ==> 페이징을 공통으로 
- Form: 필수입력, 수정/저장 서비스 하나로
- Read: 스크립트 실행 방지

### 4. board Step 4 (board4) ###
- 자료실

- Step 4.1 (board41)
: CheckStyle, PMD, FindBugs 적용 후 수정

### 5. board Step 5 (board5) ###
- 댓글

### 6. board Step 6 (board6) ###
- 무한 댓글 (계층형)

### 7. board Step 7 (board7) ###
- JQuery 활용


### 8. board Step 8 (board8) ###
- 멀티 게시판

### 9. board Step 9 (board9) ###
- 멀티 게시판 관리자

### 개발 환경 ### 
    Programming Language - Java 1.7
    IDE - Eclipse
    DB - MariaDB 
    Framework - MyBatis, Spring 4
    Build Tool - Maven

### 설치 ###

먼저 다음과 같은 테이블을 생성해야 한다.
 
    CREATE TABLE TBL_BOARD (
      BGNO INT(11),								-- 게시판 그룹번호
      BRDNO int(11) NOT NULL AUTO_INCREMENT,	-- 글 번호
      BRDTITLE varchar(255),						-- 글 제목
      BRDWRITER varchar(20),						-- 작성자
      BRDMEMO   varchar(4000),					-- 글 내용
      BRDDATE	datetime,							-- 작성일자
      BRDHIT INT,									-- 조회수
      BRDDELETEFLAG CHAR(1),						-- 삭제 여부
      PRIMARY KEY (BRDNO)
    ) ;

	CREATE TABLE TBL_BOARDFILE (
	    FILENO INT(11)  NOT NULL AUTO_INCREMENT, -- 파일 번호
	    BRDNO INT(11),                           -- 글번호
	    FILENAME VARCHAR(100),                   -- 파일명
	    REALNAME VARCHAR(30),                    -- 실제파일명
	    FILESIZE INT,                            -- 파일 크기
	    PRIMARY KEY (FILENO)
	);
    
	CREATE TABLE TBL_BOARDREPLY (
	    BRDNO INT(11) NOT NULL,					-- 게시물 번호
	    RENO INT(11) NOT NULL,                 -- 댓글 번호
	    REWRITER VARCHAR(10) NOT NULL,         -- 작성자
	    REMEMO VARCHAR(500) DEFAULT NULL,      -- 댓글내용
	    REDATE DATETIME DEFAULT NULL,          -- 작성일자
	    REDELETEFLAG VARCHAR(1) NOT NULL,      -- 삭제여부
	    REPARENT INT(11),							-- 부모 댓글	
	    REDEPTH INT,								-- 깊이	
	    REORDER INT,								-- 순서
	    PRIMARY KEY (RENO)
	);

	CREATE TABLE TBL_BOARDGROUP (
	  BGNO INT(11) NOT NULL AUTO_INCREMENT,		-- 게시판 그룹번호
	  BGNAME VARCHAR(50),							-- 게시판 그룹명
	  BGPARENT INT(11),							-- 게시판 그룹 부모
	  BGDELETEFLAG CHAR(1),						-- 삭제 여부
	  BGUSED CHAR(1),								-- 사용 여부
	  BGREPLY CHAR(1),							-- 댓글 사용여부
	  BGREADONLY CHAR(1),							-- 글쓰기 가능 여부
	  BGDATE DATETIME,							-- 생성일자
	  PRIMARY KEY (BGNO)
	);




\board\src\main\webapp\WEB-INF 폴더에 있는 applicationContext.xml에서 적절한 DB 접속 정보를 입력하고 실행하면 된다.


# springBoard
