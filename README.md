# mediaiplus_daily
my daily report

******

<details>
<summary>week1</summary>

> <details>
> 
> <summary>20230302</summary>
> 
> ```
> 
> vscode
> DBeaver
> WinSCP
> MongoCompass
> 
> jh.park@mediaiplus.com 
> 123ssk12!
> 
> 메일확인 outlook
> 
> confluence
> 
> 임상시험공부 - 글로벌 임상시험 성공하기
> 
> 인턴십OT 내용정리
> 
> 컴공핵심과목 : 내가 잘하는거->대답잘할수있는거
> 자기소개 : 내가 얼마나 개발을 잘하는지, 얼마나빠르게 성장할수있는지 
> 면접관의 의도?? 편한마음으로 임하자..?
> 
> pw : 0130
> 
> task1 : EudraCT -> CTIS 
> task2 : CRIS result 수집하기
> 
> ```
> 
> </details>
> 
> <details>
> <summary>20230303</summary>
> 
> ```
> 
> 질문할거 -> 구글링 먼저하자
> 1. yml 
> 2. 파서에서 start_date yesterday 주석 이상한것같음
> 3. start_date, saving_start_date difference -> 왜 굳이 따로 두는가 ??
> 
> 
> 폴더 강제삭제 : rm -rf (folder)
> 
> 코드해석하기
> l19 : 파서
> l20 : common에서 logger가져오기 -> common_util로 가보면
> l80 : scraper 정의
> 
> 코드실행하기
> 
> 커맨드 : python scraper_manager.py
> 
> 디폴트값 nih 
> Scraper클래스로 nih 인스턴스 만듬
> _get_model 메소드 실행 -> _handling_date메소드 실행 -> NIHct 모델 리턴함 (클래스로 선언된 모델 임포트해서 갖고옴)
> 
> Namespace(start_date='lastupdatedate', end_date='today', save='no', insert='no', date_parameter=0, cris_start=0, cris_end=None, cris_lang='K', model='nih', email='no')
> 
> cris, mfds -> yaml에서 함
> 
> 핸들링데이터 메소드의 역할 
> 2023-03-01 today 를 아래처럼 변환해줌
> 03/01/2023 03/03/2023
> 
> dao가 뭘까?
> dao
> 
> run 메소드를 이해해보자
> 1. 비교
> 2. 크롤링해옴
> 3. 디비에 트리로 바꿔서 집어넣음
> 
> 
> parser?? : 커맨드라인 인수 파싱하기
> 
> 로컬 디비 만들기 : mysql부터 다시 깔자
> 
> get방식으로 api가져오기 -> 스키마 컴페어 부분부터 다시보기
> 
> ```
> 
> </details>
  
</details>

<!-- week2 -->

<details>
<summary>week2</summary>

<details>
<summary>20230306</summary>

```
import ipdb; ipdb.set_trace() 앞으로 디버깅은 이거로 하자
로컬에 DB설치하는법을 따로 배워야함...     
tqdm 이라는 신기한 라이브러리를 배웠음
  
api를 통해 정보를 받아올수있다.
Headers : fakeheaders -> 크롤링시 우회용

nih 접속하여 회사DB와 비교해보았음. 가장최신화된 자료가 NCT05754515 였는데,
회사DB에 contacts 정보가 정확히 입력되어있었음. 
exact_tree 코드  556~690 
  
https://www.clinicaltrials.gov/ct2/home
  
```
<img
     src="https://user-images.githubusercontent.com/126745832/223040633-c0b674cc-ac1f-47f8-ab99-f5087f376cc2.png"
     width=300
     height=100
/>
<img
     src="https://user-images.githubusercontent.com/126745832/223040690-9e20b7f5-e17a-4cf8-a415-63d850956a90.png"
     width=300
     height=100
/>
  
```
위와 같이 
/home/jh_park/test/_test/models/nihct/utils/info.py 코드에 적혀진대로 4개가 DB에도 저장된것.
```
<img
     src="https://user-images.githubusercontent.com/126745832/223041521-9cb969b8-3bbf-43ce-9add-3deb3032159f.png"
     width=300
     height=300
/>

```
각각은 위와 같이 정의됨.
DB에서 column의 이름임. > RDB cloumn scheme

compare scheme > crawl data > make tree > insert to DB
  
__repr__ : Node만들때(make tree) 사용했음.
```
  
</details>

<details>
<summary>20230307</summary>

```
__str__, __repr__ 차이점 보기
  
>>> import datetime
>>> a = datetime.datetime(2017, 9, 27)
>>> str(a)
'2017-09-27 00:00:00'
>>> repr(a)
'datetime.datetime(2017, 9, 27, 0, 0)'

  
  
크롤링과정 

NStudiesFound : 업데이트해줘야하는 데이터
trial/100 만큼 iteration -> full_study_list 채움
make tree를 이용하여 트리구조로 field_list를 만듬
23개의 element를 갖고있음 
field_list[0] 는 이중리스트형태로 각각의 요소가 그에 해당되는 모듈의 정보를 갖고있음.
예시 : [ ['NCT05756881', Node (Level 0) : [struct] IdentificationModule / None // num of child of this node : 5],
         ['NCT05756868', Node (Level 0) : [struct] IdentificationModule / None // num of child of this node : 5],
         ['NCT05756855', Node (Level 0) : [struct] IdentificationModule / None // num of child of this node : 6] ... ]
  
이를 바탕으로 rows를 만들면

[ ['NCT00001971', 'Evaluation of Patients With Liver Disease', 'Evaluation of Patients With Liver Disease', 'National Institutes of Health Clinical Center (CC)', '910214', 'NIH', None, None, None, None, '2023-03-07 10:18:13', '2023-03-07 10:18:13'], 
  ['NCT00001481', 'The Role of Hormones in Postpartum Mood Disorders', 'An Endocrine Model for Postpartum Mood Disorders', 'National Institutes of Health Clinical Center (CC)', '950097', 'NIH', None, None, None, None, '2023-03-07 10:18:13', '2023-03-07 10:18:13'], 
  ['NCT00001160', 'Studies on Tumors of the Thyroid', 'Studies on Thyroid Nodules and Thyroid Cancer', 'National Institutes of Health Clinical Center (CC)', '770096', 'NIH', None, None, None, None, '2023-03-07 10:18:13', '2023-03-07 10:18:13'] ... ]  

  
cris 데이터 가져오기 
  
그전에 질문

1. DB에 중복 데이터가 존재함 
  https://cris.nih.go.kr/cris/search/detailSearch.do/?seq=14743&search_page=L&search_lang=K
  https://cris.nih.go.kr/cris/search/detailSearch.do/?seq=15988&search_page=L&search_lang=K
  -> cris가 버전관리를 안해서 생기는 문제였음. 나중에 최신의 버전 (높은 key)을 유지하자
2. PRE20190408-003 ??
  pre로 key로만 들어갈수있음
3. selenium.common.exceptions.WebDriverException: Message: 'chromedriver' executable may have wrong permissions. Please see https://chromedriver.chromium.org/home
  해결 : 크롬드라이버 깔아서 .env.yml 변
4. 링크접속불가 
  https://cris.nih.go.kr/cris/resultsearch/resultSearch.do/
5. 디비에 널값이 있는이유? 


크롤링하는법  
 
먼저 갱신일을 기준으로 검색을 함.
  
parsing_kor_doc 부터 다시 확인하기. 
  
  
```
  
</details>

<details>
<summary>20230308</summary>

```

vscode 단축키

ctrl + end : 커서 맨끝으로
shift + end : 선택하면서 행의 맨끝으로
ctrl + shift + end : 선택하면서 페이지 맨끝으로 

ctrl + arrow : 커서 단어 단위로 옮기기 
ctrl + shift + arrow : 단어단위 선택하면서 맨끝으로

crtl + alt : 다중택

DB -> mediaiplus -> DB name 'RAW'

cris : 최신업데이트 부터 오늘날짜로 받아오기 

질문
1. cris 커맨드 입력받을때 인덱스를 왜입력받는가?

2. dev_fe_ctx_cris_ct 테이블의 용도?
```
```
git clone 하고 해야하는거 !!!

1. .env 
2. 크롬드라이버 받기 
```
```
CRIS 가장 큰 문제점 : api도없고, 계속해서 사이트가 변경됨 -> 지금만들어도 나중에 cris가 데이터를 게시하는 방법이 달라지면 다시 업로드 해야할 필요가 있음. -> 일단은 현재 버전으로 만들어봐야함.

현상황 : cris_ct_result 데이터들 12/16을 마지막으로 업데이트가 안됨.
현재(230308 16:06) 기준 연구결과가 등록된 데이터들은 총 551건이 검색되는데, 막상 결과가 등록이 안된경우가 많음

결과등록이 안된경우 
```

<img
     src="https://user-images.githubusercontent.com/126745832/223645866-4067dd5f-441d-4647-95e4-8868149798c0.png"
     width=300
     height=300
/>
<img
     src="https://user-images.githubusercontent.com/126745832/223645982-f809fdaa-e813-4611-9af6-c2d701a3897c.png"
     width=300
     height=300
/>

  
```
결과등록이 잘된경우
```  
<img
     src="https://user-images.githubusercontent.com/126745832/223645598-a3332d69-3451-441b-9550-bf9e7cb93345.png"
     width=300
     height=300
/>

```
내일 확인해봐야하는거 : 3/7 기준 6개가 업데이트됨, 그러나 DB엔 5개만 업데이트됨 (16157 누락) -> 3/7에 정기적으로 스크랩할때, 스크랩하기 전에 5개가 업데이트 된것이고, 나머지 하나는 스크랩 이후 업데이트된 것이었음. 


```
</details>




</details>

<!-- week3 -->

