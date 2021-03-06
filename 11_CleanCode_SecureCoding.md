



#  Clean Code & Secure Coding

##  클린코드란?

###  SW Master들이 생각하는 클린코드 

> "깨끗한 코드는 한 가지를 제대로 한다." - Bjarne Stroustrup , C++ 창시자 
>
> "깨끗한 코드는 단순하고 직접적이다." - Grady Bouch, 객체지향 대가 
>
> "특정 목적을 달성하는 방법은 (여러가지가 아니라) 하나만 제공한다." - Dave Thomas, OTI창립자
> "깨끗한 코드는 언제나 누군가 주의 깊게 짰다는 느낌을 준다." - Michael Feathers
>
> "중복 줄이기, 표현력 높이기, 초반부터 간단한 추상화 고려하기, 내게는 이 세가지가 깨끗한 코드를 만드는 비결이다." - Ron Jeffries 
>
> "코드를 읽으면서 짐작했던 기능을 각 루틴이 그대로 수행한다면 깨끗한 코드라 불러도 되겠다." - Ward Cunningham , 위키 창시자, 피트 창시자 



###  클린코드란? 

- 코드를 작성하는 의도와 목적이 명확하다.

- 다른 사람이 쉽게 읽을 수 있어야 한다.  = 가독성이 좋다.

- 가독성이 좋다 = 타인이 이해하는데 들이는 시간을 최소화 하는 방식으로 작성 됨 

- 이해 = 코드를 자유롭게 수정하고, 버그를 찾고, 변경 내용이 기존코드와 어떻게 상호작용하는지 안다.

  

## 클린코드를 만드는 규칙

### 개발시간을 단축할 수 있는 방법

- **코드읽는 시간 : 코드짜는 시간 = 10 : 1**

- 새 코드를 짜면서 계속 기존 코드를 읽는다.



###  의미있는 이름 - Naming

- 변수, 클래스, 메서드에 의도가 분명한 이름을 사용한다.
- 측정하는 값과 단위를 나타내는 이름을 사용한다.
- 잘못된 정보를 전달할 수 있는 이름은 사용하지 않는다. 
  - 범용적으로 사용되는 단어를 다른 의미로 사용하지 않는다 (ex. hp, aix, sco )
  - 가독성이 떨어지는 문자를 사용하지 않는다. (ex. 1, i ,l, 0,o,ㅇ) 
  - 연속된 숫자 또는 불용어(noise word)를 덧붙이지 않는다. 
- 발음하기 쉬운 이름을 사용하라, 코드 공유시 커뮤니케이션을 쉽게 하기 위해. 
  -  나쁜예 `Date genymdhms;`  / 좋은예 `Date generationTimestamp;` 



###  명확하고 간결하게 주석달기 - Comment 

- 주석의 목적 : 열람자가 작성자만큼 이해할 수 있도록 돕는다
- 주석은 반드시 달아야 할 이유가 있는 경우에만 사용한다. 
  - 보안문제에 유의
  - 코드로 빠르게 유추할 수 있는 내용에는 주석을 달지 않는다. 
  - 설명을 위한 설명을 피한다
    - 나쁜예 : 주석 내용이 함수 선언과 동일한 내용
    - 좋은예 : 함수 내 중요한, 코드에 나타나지 않는 시스템 사항



###  보기좋게 배치하고 꾸미기 - Aesthetics 

- 보기좋은 코드가 읽기도 좋다. 
- 나쁜예 : 일관되지 않는 들여쓰기, 불규칙한 줄바꿈, 코드사이에 숨어있는 주석, 중복주석, 테스트코드
- 헬퍼 메소드를 이용해 가독성 향상, 열 정렬
- 코드를 그룹, 계층구조 방식으로 조작한다.
- 코드를 문단으로 나눠서 작성한다. 



###  읽기 쉽게 흐름제어 만들기 

- 좌측에 변수, 우측에 상수를 두고 비교하라 ` if(10 <= length) ` -> `if(length => 10)`

- 부정이 아닌 긍정을 다뤄라  ` if(a != b) ` -> `if(a == b)`

- if / else를 사용하고 삼항 연산자는 매우 간단한 경우에만 사용한다.

- do / while 루프를 피하라 

  - ` do { if () return } while (); return ` 

    -> ` while () { if () return; } return;`

- 중첩을 최소화 : 새로운 요구사항을 반영하여 수정할때 코드를 사로운 관점에서 재작성 
- 설명변수와 요약변수를 이용하여 커다란 표현을 작게 만들어라 
  - ` if 조건 == "root"`  -> `username = 조건; if username = "root"` 
  - `if A == B { } ; if A != B ` -> `C = (A == B);  if( C ){};  if( !C ){};`  

- 동일한 부분을 요약 변수로 추출해 함수의 시작 부분에 정의 = 정제하라



###  착한 함수 - Function 

- 함수는 가급적 작게, 한번에 하나의 작업만 수행하도록 작성되어야 한다. 



## 레거시 코드를 다루기 위한 실습

###  코드리뷰 - code inspection

- 작성한 코드를 분석하여 개발 표준에 위배되었거나 잘못 작성된 부분을 수정하는 작업

####  1. Code Inspection flow

- ![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/85/Fagan_Inspection_Simple_flow.svg/1018px-Fagan_Inspection_Simple_flow.svg.png)
  - planning : 계획수립
  - overview : 교육과 역할 정의 
  - preparation : 코드인스펙션을 위한 인터뷰, 산출물, 도구 준비 
  - meeting : 인스펙션 검토 회의로 각자 역할수행 
  - rework : 발견된 결함 수정, 재검토 필요 여부 결정
  - follow-up : 결함 및 이슈 수정 여부 확인 및 시정조치

#### 2. Code Inspection role

| 역할              | 설명                                                   |
| ----------------- | ------------------------------------------------------ |
| 조정자, moderator | 인스펙션 계획, 의장역할(주관자), 담당자 지정, 이슈관리 |
| 발표자, reader    | 산출물 저자, 도메인전문가, 예상되는 이슈 제공          |
| 검토자, reviewer  | 코드 검토, 의견 제시, 수정방안 토론                    |
| 기록자, recoder   | 수정사항 기록, 결과 공유, 이슈 추적                    |



####  3. Code Inspection Solution 

![](http://pseg.or.kr/pseg/files/attach/images/6498/663/008/9c71e87bfec20b6242a73bbd0fdc4fc7.png)

1. 개발자는 소스코드를 개발브랜치로 푸시
2. CI서버는 형상관리서버 Git저장소를 트리거하여 빌드 수행 
3. CI서버는 빌드검증결과와 단위테스트 결과를 형상관리서버에 알려줌 
4. 코드 감사결과를 인스펙션서버에 업데이트
5. 개발자는 개발브랜치에 코드를 마스터브랜치로 머지하기 위해 pull request 수행 
6. 인스펙션 서버는 코드감사결과를 pull request에 업데이트
7. 리뷰어는 코드감사결과를 확인하고 소스코드를 머지한다 = 코드클린, 안정성보완

- Bamboo 또는 젠킨스 CI도구를 사용한다. 



####  4. Code Inspection Effect 

![](https://smartbear.com/SmartBear/media/images/product/collaborator/code-review-best-practices-figure-02.gif)

![](https://smartbear.com/SmartBear/media/images/product/collaborator/code-review-best-practices-figure-01.gif)

####  5. Code Review Checklist 

- [ ] 코딩 스타일가이드를 준수하는가
- [ ] 하나의 함수가 하나의 기능만을 수행하는가
- [ ] 각 함수의 정보는 코드를 설명하기에 충분한가
- [ ] 주석은 적절하게 기술되어 있는가
- [ ] 코드는 잘 구조화되어 있는가 - 가독성, 기능적 측면
- [ ] 헤더, 함수 정보를 도구로 추출해서 자동으로 문서화할 수 있는 구조인가 
- [ ] 함수와 변수명은 일관되고 상세하게 기술되어 있는가
- [ ] 숫자를 직접서술하지 않고 상수를 사용하는가
- [ ] 주석처리 된 코드는 삭제되었는가
- [ ] 설명을 보거나 작성자에게 문의해야만 이해할수 있는 코드가 존재하는가
- [ ] 함수의 길이는 적절한가 - 20줄 이내, 라인당 150문자 이하 
- [ ] 코드 재사용이 가능한가
- [ ] 전역변수를 최소화했는가
- [ ] 변수범위는 적절하게 선언되었는가
- [ ] 클래스함수와 관련된 기능끼리 그룹으로 묶여있는가
- [ ] 중복된 함수, 클래스, 코드가 있는가
- [ ] 테이터에 맞게 타입이 구체적으로 선언되었는가 
- [ ] if/else 구문에 2단계 이상 중첩이 있는가
- [ ] 중첩되었아면 함수로 더 구분했는가
- [ ] switch/case문이 중첩되었는가, 더 구분할 수 없는가 
- [ ] 리소스에 lock이 있다면 unlock되었는가 
- [ ] 스택변수는 반환하고 있는가 

- 아래부터는 큰 위험을 초래할 수 있는 부분에 대한 체크리스트이므로 더욱 긴밀히 보아야 한다. 

- [ ] 입력 파라미터의 유효범위는 체크하고 있는가 

- [ ] 오류코드를 반환하는 함수보다 예외를 적극적으로 활용하고 있는가

- [ ] try/catch 에러 핸들링 사용방법은 적절하게 구현되었는가

- [ ] 메서드에서 null을 전달하거나 반환하고 있지는 않나

- [ ] switch문에 default가 존재하며, 예외처리하고있는가

- [ ] 배열 사용시 index범위를 체크하는가

- [ ] 포인트 사용기 유효범위를 체크하는가

- [ ] garbage collection은 제대로 수행되는가 

- [ ] 에러 조건이 체크되고 여러 메세지와 에러코드가 의미를 잘 전달하는가

  

###  리팩토링

: 점진적으로 반복 수행 과정을 통해 코드개선 

####   리펙토리 대상 카테고리 

| 역할                    | 설명                                                    |
| ----------------------- | ------------------------------------------------------- |
| 메서드 정리             | 그룹으로 묶을 수 있는 코드, 수식을 메서드로 변경        |
| 객체간 기능이동         | 메서드 기능에 따른 위치 변경, 클래스 기능의 명확한 구분 |
| 데이터구성              | 객체지향 캡슐화 기법을 적용해 데이터 접근 관리          |
| 조건문 단순화           | 조건 논리를 단순하고 명확하게 작성                      |
| 메서드 호출 단순화      | 메서드 이름, 목적이 맞지않는 경우 변경                  |
| 클래스 및 메서드 일반화 | 동일 기능 메서드가 여러 클래스에 있으면 슈퍼클래스 이동 |



####   리펙토링 방법

- 아키텍처 관점에서 시작 -> 디자인 패턴 적용 -> 단계적으로 하위 기능에 대한 변경으로 진행
- 의도하지 않은 기능 변경이나 버그의 발생에 대비해 회귀테스트도 진행
- 이클립스와 같은 IDE 도구 이용



##  시큐어코딩이란?

#### 안전한 소프트웨어는?

- 실수, 오류, 결함, 버그, 장애, 결점이 없는 SW
- 안전한 SW개발을 위해 존재할 수 있는 잠재적인 보안약점을 제거하고, 보안을 고려하여 기능을 설계, 구현하는 등 SW개발 과정에서 일련의 보안활동을 수행하는 SW개발보안을 적용

####  SW보안약점 vs SW보안취약점

![](https://t1.daumcdn.net/cfile/tistory/99ECEA465A3C54D205)

| 보안약점                                                     | 보안취약점                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Weakness                                                     | Vulnerabilities                                              |
| 소프트웨어에서 해킹등 실제 보안 사고에 악용될 수 있는 보안 취약점의 근본 원인 | 소프트웨어 실행시점에 여러개의 보안약점 중 실제 침해 사고의 원인이 되는 그 보안 약점 |



####  안전한 소프트웨어 개발의 필요성

- 해커로부터 침해사고가 발생하는 SW단 별 빈도율 
  - 방화멱 : 0.5 % 
  - IDS/IPS : 3 %
  - 웹방화벽 : 10 %
  - **개발서버 : 75 %**  



####  취약점의 일반론

- 사용자 , 특히 공격자가 조작할 수 있는 입력 또는 객체를 통해 공격이 수행된다. 
- 즉, 신뢰되지 않는 외부 입력을 그대로 사용하는 것이 중요한 침해사고의 원인이 된다.



####  시큐어코딩과 소프트웨어 개발보안 활동

![](https://t1.daumcdn.net/cfile/tistory/2142BF4559080B522A)



##  사고사례기반 시큐어코딩의 필요성

- SQL인젝션 취약점으로 개인정보 유출사고 - [기사보기](http://www.bloter.net/archives/278144)

![](http://www.bloter.net/wp-content/uploads/2017/04/Yogi_Hacking.jpg)

- URL 파라미터 조작 개인정보 노출 - [기사보기](https://news.sbs.co.kr/news/endPage.do?news_id=N1003506305)

- 무작위 대입공격 기프트카드 정보 유출 -  [기사보기](http://www.donga.com/news/article/all/20160219/76533042/1)

- 웹애플리케이션 취약점이용 

  : 접근제어기능이 취햑한 app을 대상으로 공격자는 서버로 전달되는 파라미터를 자동화된 툴을 이용하여 조작, 다른사용자 정보 유출 

  ![](http://www.jjan.kr/news/photo/201403/505305_153131_4612.jpg)

  1. 해커 : 취약한 페이지 로그인 
  2. 해커 : 요금명세서 조회 
  3. 해커 - Paros : 로그인한 사용자의 고객번호 123456789
  4. 해커 - Paros : Paros에서 위조된 고객번호 조회 요청 678912345
  5. DB - 서버 : DB DB조회 요청처리 
  6. 서버 -> Paros : 678912345 조회결과 전송 
  7. Paros -> 해커 : 678912345 조회결과 전송 



##  시큐어코딩의 예

###  SQL 인젝션 

- SQL 쿼리문의 일부로 사용되는 사용자의 입력데이터에 대한 적절한 검증 작업이 수행되지 않아서 발생 
- 외부에서 입력되는 값을 쿼리문에 사용하는 경우 입력값을 받는 변수를 $가 아니라 #를 사용함으로써 바인딩 처리 가능  : `.. WHERE NAME LIKE '${username}' ` -> ` .. WHERE NAME = #{username}` 

###  크로스사이트 스크립트 (XSS)

- 웹애플리케이션 입력값에 대한 검증이 미비한 경우 공격자로부터 입력된 악의적인 데이터는 웹애플리케이션을 매개로 다른 사용자의 브라우저에서 실행되도록 함 
- 크로스사이트 스크립트 취약점을 제거하기 위해서는 외부입력값을 안전하게 필터링해서 사용 

###  파라미터 변조로 접근제어 우회

- URL이나 파라미터, 헤더나 쿠키값을 조작하여 허가되지 않은 기능이나 리소스에 접근하여 허가되지 않은 정보가 유출된다. 



##  보안약점 제거기준

###  CWE

- Common Weakness Enumeration 
- http://cwe.mitre.org
- 미국 국토안보부에서 관리 
- SW 취약점을 사전식으로 분류
- 취약점에 대한 정의, 설명, 해당 취약점의 플랫폼(언어), 반향, 빈도 및 예제코드, 이를 완화하기 위한 방법론 

###  CVE

- Common Vulnerabilities and Exposures 
- http://cve.mitre.org 
- 시간에 따라 감지도나 보안취약점 또는 위험 노출을 정리해둔 목록
- MITRE를 주축으로 SW(주로 운영체제) 개발 회사와 CERT/CC 같은 기관에서 감지된 보안취약점을 보고하면, CVE조정위원회를 통해 목록으로 관리 
- CVE + 년도 + 일련번호 

### SANS Top 25 

- SANS TOP 25 Most Dangerous Software Errors 

- http://www.sans.org/top25-software-errors/

- SANS : SysAdmin, Audit, Network, Security - 산학협동연구소 

- SWSS (Common Weakness Scoring System) 사용

- 취약점에 대한 설명과 주요 완화 방법 함께 설명 

- 취약점을 3개 카테고리로 분류 (자세한 내용은 위 링크)

  - **구성요소간 안전하지 않은 상호작용 (6개)** 

    개별 구성요소, 모듈, 프로그램, 프로세스, 스레드, 시스템간에 안전하지 않은 방법으로 데이터가 송수신되는 방법과 관련이 있는 취약점 정의

  - **위험한 자산관리 (8개)**

    소프트웨어가 중요한 시스템 자원을 적절하게 생성, 사용, 전송, 폐기하지 않는 것과 관련이 있는 취약점 정의

  - **허점이 많은 방어 (11개)**

    오남용하거나 쉽게 무시되는 방어 기법과 관련이 있는 취약점을 정의

### OWASP Top 10

- OWASP : The Open Web Application Security project 
  - 오픈소스 웹 애플리케이션 보안 프로젝트 
  - 주로 웹에 관한 정보토출, 악성 파일 및 스크립트, 보안 취약점 등을 연구
- OWASP Top10 
  - 운영중인 웹 서버에서 가장 많이 발생하는 침해사고 유형을 정리한 리스트 
  - 이중 취약점 공격 가능성, 탐지 가능성, 영향 평가 등을 고려해 가장 많이 퍼져있으며, 위험도가 큰 상위 10개를 정해 해당 문제에 대해 대을할 수 있는 기본적인 기술을 제공하며, 이를 근거로 향후 방향 제시 
  - https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project 
- OWASP Top10 장점 
  - 웹서비스를 중심으로 취약점이 정리 
  - 리스트 길이가 짧아서 개발시 적용하거나 교육하기가 비교적 용이
  - 리스트 순서가 중요도(빈도와 심각성)를 반영