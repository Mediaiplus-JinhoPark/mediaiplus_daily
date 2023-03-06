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
tqdm 이라는 신기한 라이브러리를 배웠음
  
api를 통해 정보를 받아올수있다.<br>
Headers : fakeheaders -> 크롤링시 우회용

nih 접속하여 회사DB와 비교해보았음. 가장최신화된 자료가 NCT05754515 였는데,
회사DB에 contacts 정보가 정확히 입력되어있었음. 
exact_tree 코드  556~690 
  
https://www.clinicaltrials.gov/ct2/home
  
```
  
![스크린샷 2023-03-06 160019](https://user-images.githubusercontent.com/126745832/223040633-c0b674cc-ac1f-47f8-ab99-f5087f376cc2.png)
![스크린샷 2023-03-06 160028](https://user-images.githubusercontent.com/126745832/223040690-9e20b7f5-e17a-4cf8-a415-63d850956a90.png)
  
```
위와 같이 
/home/jh_park/test/_test/models/nihct/utils/info.py 코드에 적혀진대로 4개가 DB에도 저장된것.
```

![스크린샷 2023-03-06 160605](https://user-images.githubusercontent.com/126745832/223041521-9cb969b8-3bbf-43ce-9add-3deb3032159f.png)
```
각각은 위와 같이 정의됨.
DB에서 column의 이름임.
```
  
</details>




