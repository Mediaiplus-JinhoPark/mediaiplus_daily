# mediaiplus_daily
my daily report

******

<details>

<summary>20230302</summary>

```

vscode
DBeaver
WinSCP
MongoCompass

jh.park@mediaiplus.com 
123ssk12!

메일확인 outlook

confluence

임상시험공부 - 글로벌 임상시험 성공하기

인턴십OT 내용정리

컴공핵심과목 : 내가 잘하는거->대답잘할수있는거
자기소개 : 내가 얼마나 개발을 잘하는지, 얼마나빠르게 성장할수있는지 
면접관의 의도?? 편한마음으로 임하자..?

pw : 0130

task1 : EudraCT -> CTIS 
task2 : CRIS result 수집하기

```

</details>

<details>
<summary>20230303</summary>

```

질문할거 -> 구글링 먼저하자
1. yml 
2. 파서에서 start_date yesterday 주석 이상한것같음
3. start_date, saving_start_date difference -> 왜 굳이 따로 두는가 ??


폴더 강제삭제 : rm -rf (folder)

코드해석하기
l19 : 파서
l20 : common에서 logger가져오기 -> common_util로 가보면
l80 : scraper 정의

코드실행하기

커맨드 : python scraper_manager.py

디폴트값 nih 
Scraper클래스로 nih 인스턴스 만듬
_get_model 메소드 실행 -> _handling_date메소드 실행 -> NIHct 모델 리턴함 (클래스로 선언된 모델 임포트해서 갖고옴)

Namespace(start_date='lastupdatedate', end_date='today', save='no', insert='no', date_parameter=0, cris_start=0, cris_end=None, cris_lang='K', model='nih', email='no')

cris, mfds -> yaml에서 함

핸들링데이터 메소드의 역할 
2023-03-01 today 를 아래처럼 변환해줌
03/01/2023 03/03/2023

dao가 뭘까?
dao

run 메소드를 이해해보자
1. 비교
2. 크롤링해옴
3. 디비에 트리로 바꿔서 집어넣음


parser?? : 커맨드라인 인수 파싱하기

로컬 디비 만들기 : mysql부터 다시 깔자

get방식으로 api가져오기 -> 스키마 컴페어 부분부터 다시보기

```

</details>

<details>
<summary>20230306</summary>

```
import ipdb; ipdb.set_trace() 앞으로 디버깅은 이거로 하자
로컬에 DB설치하는법을 따로 배워야함...                                 
                                 

```

</details>
