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

> <details>
> <summary>20230306</summary>
> 
> ```
> import ipdb; ipdb.set_trace() 앞으로 디버깅은 이거로 하자
> 로컬에 DB설치하는법을 따로 배워야함...     
> tqdm 이라는 신기한 라이브러리를 배웠음
>   
> api를 통해 정보를 받아올수있다.
> Headers : fakeheaders -> 크롤링시 우회용
> 
> nih 접속하여 회사DB와 비교해보았음. 가장최신화된 자료가 NCT05754515 였는데,
> 회사DB에 contacts 정보가 정확히 입력되어있었음. 
> exact_tree 코드  556~690 
>   
> https://www.clinicaltrials.gov/ct2/home
>   
> ```
> <img
>      src="https://user-images.githubusercontent.com/126745832/223040633-c0b674cc-ac1f-47f8-ab99-f5087f376cc2.png"
>      width=300
>      height=100
> />
> <img
>      src="https://user-images.githubusercontent.com/126745832/223040690-9e20b7f5-e17a-4cf8-a415-63d850956a90.png"
>      width=300
>      height=100
> />
>   
> ```
> 위와 같이 
> /home/jh_park/test/_test/models/nihct/utils/info.py 코드에 적혀진대로 4개가 DB에도 저장된것.
> ```
> <img
>      src="https://user-images.githubusercontent.com/126745832/223041521-9cb969b8-3bbf-43ce-9add-3deb3032159f.png"
>      width=300
>      height=300
> />
> 
> ```
> 각각은 위와 같이 정의됨.
> DB에서 column의 이름임. > RDB cloumn scheme
> 
> compare scheme > crawl data > make tree > insert to DB
>   
> __repr__ : Node만들때(make tree) 사용했음.
> ```
>   
> </details>
> 
> <details>
> <summary>20230307</summary>
> 
> ```
> __str__, __repr__ 차이점 보기
>   
> >>> import datetime
> >>> a = datetime.datetime(2017, 9, 27)
> >>> str(a)
> '2017-09-27 00:00:00'
> >>> repr(a)
> 'datetime.datetime(2017, 9, 27, 0, 0)'
> 
>   
>   
> 크롤링과정 
> 
> NStudiesFound : 업데이트해줘야하는 데이터
> trial/100 만큼 iteration -> full_study_list 채움
> make tree를 이용하여 트리구조로 field_list를 만듬
> 23개의 element를 갖고있음 
> field_list[0] 는 이중리스트형태로 각각의 요소가 그에 해당되는 모듈의 정보를 갖고있음.
> 예시 : [ ['NCT05756881', Node (Level 0) : [struct] IdentificationModule / None // num of child of this node : 5],
>          ['NCT05756868', Node (Level 0) : [struct] IdentificationModule / None // num of child of this node : 5],
>          ['NCT05756855', Node (Level 0) : [struct] IdentificationModule / None // num of child of this node : 6] ... ]
>   
> 이를 바탕으로 rows를 만들면
> 
> [ ['NCT00001971', 'Evaluation of Patients With Liver Disease', 'Evaluation of Patients With Liver Disease', 'National Institutes of Health Clinical Center (CC)', '910214', 'NIH', None, None, None, None, '2023-03-07 10:18:13', '2023-03-07 10:18:13'], 
>   ['NCT00001481', 'The Role of Hormones in Postpartum Mood Disorders', 'An Endocrine Model for Postpartum Mood Disorders', 'National Institutes of Health Clinical Center (CC)', '950097', 'NIH', None, None, None, None, '2023-03-07 10:18:13', '2023-03-07 10:18:13'], 
>   ['NCT00001160', 'Studies on Tumors of the Thyroid', 'Studies on Thyroid Nodules and Thyroid Cancer', 'National Institutes of Health Clinical Center (CC)', '770096', 'NIH', None, None, None, None, '2023-03-07 10:18:13', '2023-03-07 10:18:13'] ... ]  
> 
>   
> cris 데이터 가져오기 
>   
> 그전에 질문
> 
> 1. DB에 중복 데이터가 존재함 
>   https://cris.nih.go.kr/cris/search/detailSearch.do/?seq=14743&search_page=L&search_lang=K
>   https://cris.nih.go.kr/cris/search/detailSearch.do/?seq=15988&search_page=L&search_lang=K
>   -> cris가 버전관리를 안해서 생기는 문제였음. 나중에 최신의 버전 (높은 key)을 유지하자
> 2. PRE20190408-003 ??
>   pre로 key로만 들어갈수있음
> 3. selenium.common.exceptions.WebDriverException: Message: 'chromedriver' executable may have wrong permissions. Please see https://chromedriver.chromium.org/home
>   해결 : 크롬드라이버 깔아서 .env.yml 변
> 4. 링크접속불가 
>   https://cris.nih.go.kr/cris/resultsearch/resultSearch.do/
> 5. 디비에 널값이 있는이유? 
> 
> 
> 크롤링하는법  
>  
> 먼저 갱신일을 기준으로 검색을 함.
>   
> parsing_kor_doc 부터 다시 확인하기. 
>   
>   
> ```
>   
> </details>
> 
> <details>
> <summary>20230308</summary>
> 
> ```
> 
> vscode 단축키
> 
> ctrl + end : 커서 맨끝으로
> shift + end : 선택하면서 행의 맨끝으로
> ctrl + shift + end : 선택하면서 페이지 맨끝으로 
> 
> ctrl + arrow : 커서 단어 단위로 옮기기 
> ctrl + shift + arrow : 단어단위 선택하면서 맨끝으로
> 
> crtl + alt : 다중택
> 
> DB -> mediaiplus -> DB name 'RAW'
> 
> cris : 최신업데이트 부터 오늘날짜로 받아오기 
> 
> 질문
> 1. cris 커맨드 입력받을때 인덱스를 왜입력받는가?
> 
> 2. dev_fe_ctx_cris_ct 테이블의 용도?
> ```
> ```
> git clone 하고 해야하는거 !!!
> 
> 1. .env 
> 2. 크롬드라이버 받기 
> ```
> ```
> CRIS 가장 큰 문제점 : api도없고, 계속해서 사이트가 변경됨 -> 지금만들어도 나중에 cris가 데이터를 게시하는 방법이 달라지면 다시 업로드 해야할 필요가 있음. -> 일단은 현재 버전으로 만들어봐야함.
> 
> 현상황 : cris_ct_result 데이터들 12/16을 마지막으로 업데이트가 안됨.
> 현재(230308 16:06) 기준 연구결과가 등록된 데이터들은 총 551건이 검색되는데, 막상 결과가 등록이 안된경우가 많음
> 
> 결과등록이 안된경우 
> ```
> 
> <img
>      src="https://user-images.githubusercontent.com/126745832/223645866-4067dd5f-441d-4647-95e4-8868149798c0.png"
>      width=300
>      height=300
> />
> <img
>      src="https://user-images.githubusercontent.com/126745832/223645982-f809fdaa-e813-4611-9af6-c2d701a3897c.png"
>      width=300
>      height=300
> />
> 
>   
> ```
> 결과등록이 잘된경우
> ```  
> <img
>      src="https://user-images.githubusercontent.com/126745832/223645598-a3332d69-3451-441b-9550-bf9e7cb93345.png"
>      width=300
>      height=300
> />
> 
> ```
> 내일 확인해봐야하는거 : 3/7 기준 6개가 업데이트됨, 그러나 DB엔 5개만 업데이트됨 (16157 누락) -> 3/7에 정기적으로 스크랩할때, 스크랩하기 전에 5개가 업데이트 된것이고, 나머지 하나는 스크랩 이후 업데이트된 것이었음. 
> 
> 결과 탭에 접속이 가능하다가 안되는 경우는 어떻게 해야할까... -> 업데이트 되는지 알 수가 없음 
>   그럼 전수조사를 해야하는가? -> 경우에 따라 다름 만약 잘못된 데이터를 지우기 위해 결과를 없앤것이라면..?
>   없어진 이유를 알 수 없음.
>   
> ```
> </details>
>
> <details>
> <summary>20230309</summary>
> 
> ```
> 
> study results 존재 -> 연구결과 국문/Eng 보고 크롤링하면 될듯  
> 
> TODO
> 
> 연구결과 탭이 존재하지않음 -> 링크로 접속하면 페이지 존재 (cris_seq=8930) (상세검색 불가, cris_seq으로만 접속가능)
> https://cris.nih.go.kr/cris/resultsearch/resultSearch.do?seq=8930&search_page=L&search_lang=&
> 크롤링 할 때 결과있음으로하면 cris_seq=8930과 같은 데이터는 검색불가 -> 어떻게 크롤링할까
> 
> 상세검색할때 실제 갱신일과, 상세검색에서 검색할때의 저장된 갱신일이 다름. -> KCT0000001
> 
> 현재 크롤링은 상세검색 페이지에서 셀레니움으로 함 -> cris_seq range로 바꾸기?
> 
> 결론!! : 그냥 최종갱신일로 크롤링하자.
> 
> ```
> 
> ```
> study results 형식
> 크게 4가지임
> 1. Participant Flow
> 2. Baseline Characteristics
> 3. Outcome Measures
> 4. Adverse Events
> 
> 
> ct_list를 토대로 ct_result_list를 만들자.
> 
> ct_list 구조 파악하기.
> 
> ct_list는 길이가 업데이트해야하는 데이터의 갯수 만큼 가진 리스트임.
> 예를들어 -start_date=2023-03-01 의 옵션을 준경우, 3월1일부터 오늘날짜(today)까지의 새로 갱신해야할 데이터를 수집하여 저장함
> 이때 ct_list의 각각의 요소가 갱신된 데이터의 정보를 담고있음.
> ```
> ```
> 예를들면 len(ct_list)=3 인경우, 갱신해야할 데이터가 3개가 있는것임.
> 각 데이터의 정보를 dictionary 로 만들어줌 
> 
> ct_list.append({
>             'seq': i,
>             'status': date_list,
>             'content': table_dict,
>             'url': f'{self.base_url}?seq={i}&search_page=L&search_lang={self.language}',
>         })
> 그렇다면 각각의 키에 해당하는 밸류값들을 보자
> ct_list[0]['seq'] = '24303'
> ct_list[0]['status'] = ['등록', '2022/10/25', '2022/12/23', '2023/03/08']
> 
> ct_list[0]['content'] 는 defaultdict 자료형임.
> 
> ct_list[0]['content'].keys() = dict_keys(['1. 연구개요', '2. 임상연구윤리심의', '3. 연구자', '4. 연구현황', '5. 연구비지원기관', '6. 연구책임기관', '7. 연구요약', '8. 연구설계', '9. 대상자선정기준', '10. 결과변수', '11. 연구결과 및 발표', '12. 연구데이터 공유(익명화된 연구대상자 데이터)'])
> 또한 이 key들의 해당하는 value 또한 defaultdict 임
> 
> 예를들면 ct_list[0]['content']['1. 연구개요'] 는 아래와 같이 구성됨. 각각의 key들은 대체로 cris 자료 테이블의 row : contents임
> 
> defaultdict(None, {'CRIS등록번호': 'KCT0008025', '연구고유번호': 'NCC2022-0319', '요약제목': 'MET 또는 EGFR 단백질이 과발현된 전이성 위암의 3차이상 요법으로서의 CKD-702/이리노테칸 1b/2상 임상시험', '연구제목': 'MET 또는 EGFR 단백질이 과발현된 전이성 위암의 3차이상 요법으로서의 CKD-702/이리노테칸 1b/2상 임상시험', '연구약어명': 'CKD-702', '식약처규제연구': '예(Yes)', 'IND/IDE Protocol 여부': '아니오(No)', '타등록시스템 등록여부': '아니오(No)', '임상연구 요양급여적용 신청 여부': '신청 중(Submitted pending)'})
> 
> ct_list[0]['url'] = 'https://cris.nih.go.kr/cris/search/detailSearch.do/?seq=24303&search_page=L&search_lang=K'
> 
> 
> 만약 데이터의 개수가 가변적이라면, 리스트로 만들어줌 -> 하나의 cris_seq가 아니라 여러개의 cris_seq가 있는것, 
> PRIMARY KEY를 하나더잡아줌 즉 예를들어 cris_seq = 24303의 데이터중 연구참여기관이 두개인경우, SRSID라는 PRIMARY KEY를 잡아주는것.
> ```
> <img
> src="https://user-images.githubusercontent.com/126745832/223931817-b00a1bc7-93fc-4871-8ec7-e04dcf821f05.png"
> width=500
> height=50
> />
> 
> ```
> 스키마에대해 일단 모두 rows에 SCHEME[:-2]로 None을 넣어놈
> 
> 오늘의 질문점
> 
> [오후 4:28] 박 진호
> 저 추가적으로 질문드립니다..! cris_ct_result_participant_flow_desc 테이블에서 KCTId = 'KCT0006080' 필터로 검색해보면 cris_seq가 19160, 19735 두개로 나오는데,  https://cris.nih.go.kr/cris/search/listDetail.do여기서 상세검색에서 연구결과를 연구결과 등록으로 두고, CRIS등록번호에 6080을 검색하면 6080데이터가 나와야하는데 안나오더라구요 그래서 이유를 찾아보았습니다.  먼저 연구결과 필터를 미등록으로 바꾸고 6080을 검색하면, 19160페이지가 검색되었습니다. 제 생각엔 CRIS에서 19160의 연구결과를 지우고 갱신을 안해준것 같습니다.  또 추가로 같은 KCTId를 갖는 19735는 연구결과가 있으나 19160에는 없었습니다.  19735는 상태가 임시저장된 데이터라 상세검색 으로는 검색이 안되고, url로는 접속할 수 있더라구요, 19735에는 결과탭이 있지만, 접속은 안되었습니다.https://cris.nih.go.kr/cris/search/detailSearch.do?seq=19735 그래서 제가 생각한점은 데이터베이스에 이러한 결과가 등록되었다가 다시 없어진경우가 추가적으로 존재할수있고, 이러한 데이터들은 CRIS에서 갱신처리를 안해주다보니 저희가 업데이트를 할 수 없다고 판단되는데,  이런경우 현재 데이터베이스에 있는 결과데이터들은 옳은 정보라고 할 수 있는건가요? 만약 그렇지 않다면 현재 데이터들은 지우고 새로운 데이터들로 채워야한다고 생각이되는데.. 제가 생각한점이 맞을까요??아닌경우면 그냥 현재 데이터베이스에 duplicate하는 방식으로 코드를 짜면 되는것일까요?  감사합니다! 
> 
> [오후 4:47] 조용장
> 네, 말씀주신대로가 맞습니다!자세한 설명을 좀 더 미리 드렸으면 고민하실만한 상황이 나오지 않았을텐데 죄송스럽네요..  1.일단 첫번째로 cris_seq는 고유하지만 cris_seq에 상응하는 KCTId는 고유하지 않습니다.이런 문제는 실제로 하나의 임상이 "임시 등록", "반려" 등 "등록"이 되기 전의 형상으로 여러개의 버전이 존재하기 때문인데요. 각 버전은 새로운 cris_seq를 발급 받지만 KCTId는 모두 동일할 수 있습니다. 초기에는 "임시 등록"이나 "반려" 등의 데이터도 의미가 있을 것이라고 판단하여 cris_seq를 기준으로 전체 수집하였습니다. 하지만 그럴 필요가 없다고 판단이 되기도 하였고최종 갱신일을 기준으로 임상시험 문서를 가져와야할 필요성이 대두되면서 cris_seq를 기준으로 데이터를 수집하는 것이 아닌 KCTId를 기준으로 CRIS 데이터를 수집해야 하는 상황이 된거죠. 2.두번째로 말씀주신 6080번과 같이 CRIS에는 등록이되거나 웹 상에 공개되었다가 제거되는 문서들이 있었습니다. 이런 문서들은 추후에 다시 접근하려해도 데이터를 얻을 수 없는 문제점이 발생하구요.  "이런 데이터를 두고 저희는 DB상에서 제거하기 보다는 가지고 있는 편이 더 저희 서비스를 가치있게 만들어 줄거라고 판단하고 있기는 합니다."  그 문서의 등록 취소 요인이 무엇인지는 알 수 없으나 특정 기업에서 어떤 종류의 질병에 대해 어떤 시도를 하려했다..는 정보는 중요할 것 같아서요. 게다가 저희 DB 설계상 제거된 문서에 대한 검출은 전수조사를 하는 수 밖에 없기도 하구요..  따라서 결론은 같은 KCTId에 대해서는 값을 replace하면 될 것 같습니다. 그리고 과거에 존재하였다가 현재에 존재하지 않는 문서에 대해서는 제거하지 않구요. 다만 추후에 동일한 KCTId 임상시험에 대해서 언제 어떻게 업데이트 되었는지 히스토리를 버전별로 가지고 있을 계획은 있습니다. 깃헙에도 이슈 사항으로 올려 놓기는 했어요.
> 
> [오후 4:48] 조용장 
> 글이다 보니 아무래도 제가 조금 이해하기 어렵게 작성해 놓은 내용이 있을 수도 있을 것 같기는해요... 조금 헷갈리시면 다음주에 다시 이야기 나누시죠~
> 
> ```
> </details>
> <details>
> <summary>20230310</summary>  
> 
> ```
> 결과 데이터들의 스터럭쳐가 매우 상이함 => 일반화 할 방법을 생각해보자
> 
> get result cris id 수정 : 
> 
> 다음을 추가함 :
> from selenium.webdriver.support.ui import Select
> Select(self.driver.find_element(By.XPATH, '//*[@id="results_yn"]')).select_by_value("Y")
> 
> 위 코드의 의미는 연구결과가 등록된 문서만 검색하겠다 라는 필터를 설정해준다는 의미임.
> 
> result들의 url을 보려고했는데, 몇개이상의 페이지를 로드하다보니 이런에러가 나는듯 -> 다음주에 다시 확인하기
> stale element reference: element is not attached to the page document
> 
> ```
> 
> </details>
</details>

<!-- week3 -->

<details>

<summary>week3</summary>

> <details>
> 
> <summary>20230313</summary>
>   
> ```
> 연구결과 등록으로 검색 -> 1. 에러페이지가 나오는지 확인 -> 에러나면 그대로 리턴
> 2. 페이지에 접속을 해도, 실제 데이터가 없을수있음.
> 3. 국문/영문으로 할지, 각각 페이지에서 크롤링 할지 정하기 -> 물어봐야 할듯 근데 KCT0008257 를 보면 각각 따로 하는게 좋을듯함.
>  
> 
> 현재 발생한 문제점 : 
> 1. 로딩되는 시간을 줘야 에러가 안남
> 2. 검색되는 데이터의 개수가 다름 -> 
>     연구결과 등록된 데이터들을 볼때, start date를 비워둔 데이터의 개수와 2010-01-01, 즉 cris홈페이지에서 제공하는 초기값을 주면 데이터 개수값이 달라짐.
>     
> 
> html구조
> 연구정보, 연구결과 상이함
> main div -> print div 
> 내일 물어볼거 : date_list는 필요없는건가?
>   
>   
>   
> 결과구조분석
> 1. Participant Flow
> 모집상세설명
> 배정 전 상세설명
> -> 고정적인 두개의 행!!
> 그다음 기간이나옴 -> 주로 기간은 한개존재함.
> 
> 
> 크롤링 과정
> 만약 K인경우, E인경우 나눠서
> 각각 parsing_result_kor_doc(resp), parsing_result_eng_doc(resp) 을 호출함.
> 
> ```
> 
> </details>
>   
> <details>
> 
> <summary>20230314</summary>
>   
> ```
> 연구결과 등록으로 검색 -> 1. 에러페이지가 나오는지 확인 -> 에러나면 그대로 리턴
> 2. 페이지에 접속을 해도, 실제 데이터가 없을수있음.
> 3. 국문/영문으로 할지, 각각 페이지에서 크롤링 할지 정하기 -> 물어봐야 할듯 근데 KCT0008257 를 보면 각각 따로 하는게 좋을듯함.
> 
> study details/study results를 크롤링해와야함 -> 먼저 검색조건에 맞는 날짜에 갱신된 데이터에 한해서 크롤링 그 후 결과가 등록된 데이터를 크롤링
> get max update 는, study details를 크롤링할때 받아와지므로 자동으로 업데이트됨.
>   결과 등록된 데이터는 없는 경우가 많음
>   
>   표안에 표 : 하나의 tr내에 두개의 th
>   원래대로라면 [[th],[td]] 이지만 th가 두개라면 [[th,th],[td]]가 됨
>   td내에 pre가 되어있을수도있다... -> ().text 사용하면 똑같이나옴
>   
>   먼저 results를 크게 4개로 분리, 그 후 각각을 다시 테이블로 분리, 그러면 그 각각의 테이블들은 tr을 갖는다.
>   각 tr을 th_list, td_list로 분리한다. 그후 [th_list, td_list]로 만들어 캡션과함께 테이블딕셔너리에 해당하는 value에 append해준다.
>   
>   tr,td를 분리할때, colspan rowspan을 잘 보자 -> 
>   rowspan = 2 의 의미? 두개의 행을 차지함.
>   colspan = 2 의 의미? 두개의 열을 차지함 즉 세분화된 데이터가 있는경우, colspan, rowspan이 사용
>   
>   코드에 주석으로 남겨둠.
>   
>   
>   Participant Flow 구조 >>>
>   하나의 시퀀스에 여러개의 피리어드
>   각각 피리어드 내에는 여러개의 암그룹이 있을 수 있음 
>   
>   현재 Participant Flow 관련 메소드:
>   cris_ct_result_participant_flow_desc -> 수정필요 x
>   cris_ct_result_participant_flow_list_desc -> 하나의 시퀀스에 여러개의 피리어드를 PFSId로 구분해서 넣어놈. 스키마는 단위, 코멘트
>   cris_ct_result_participant_flow_arm_group -> 암그룹당 정보, 탈락관련정보누락됨
>   cris_ct_result_participant_flow_arm_group_research_step -> 마일스톤은 암그룹당 없을수도있거나 여러개임
>   
>   -> 탈락관련데이터가 아예 없다!
>   
>   
>   
>   
>   
> api로 받아오기????
> ```
> 
> </details>
> 
> <details>
> <summary>20230315</summary>
> 
> ```
> 
> scraper를 fork해봄
> git명령어에 익숙해져가고 있음. 처음으로 clone, fork, ... 등등을 해보았고, git을 사용한 협업이 필수적임을 깨닫게 되었음.
> 
> 추가로 parser를 업데이트하는 커밋을 해봄.
> 
> 현재 PF데이터에 탈락사유가 없어서, 추가적인 테이블을 만들어줌.
> 
> 
> ```
>     
> </details>
> 
> <details>
> <summary>20230316</summary>
> 
> ```
> ct_result_list : 딕셔너리, key로 'Participant Flow', 'Baseline Characteristics', 'Outcome Measure', 'Adverse Events' 를 가짐
>   
> PF구조 파악하기
> result_dict['Participant Flow'].keys() = dict_keys(['모집상세설명', '배정 전 상세설명', 'Participant Flow List'])
>   
> result_dict['Participant Flow']['Participant Flow List'] 의 길이는 Period의 갯수를 의미함 
> 하나의 피리어드 내부에는, 여러개의 암그룹이 있을수 있음. -> 암그룹 리스트가 필요함
> result_dict['Participant Flow']['Participant Flow List'][0].keys() = dict_keys(['기간명', 'Arm Group List', '단위'])
>   
>   첫번째 암그룹의 데이터를 보자.
>   result_dict['Participant Flow']['Participant Flow List'][0]['Arm Group List'][0].keys() = 
>   dict_keys(['중재 / 관찰군명', '중재 / 관찰군 상세내용', '연구시작', 'Important Study Step List', '연구완료', '탈락', 'Fail Reason List'])
> 
>   암그룹 내부에는, 여러개의 마일스톤 데이터와 탈락사유가 있을수 있음.
>   첫번쨰 피리어드 내부의 첫번째 암그룹의 첫번째 마일스톤을 보자.
>   result_dict['Participant Flow']['Participant Flow List'][0]['Arm Group List'][0]['Important Study Step List'][0]
> {'중요연구단계': '시험약 또는 위약 복용', '중요연구단계 결과': '9'}
>   마일스톤 리스트의 요소는 딕셔너리의 형태로 되어있음 -> 탈락사유 리스트또한 같은 구조의 딕셔너리임.
>   
>   BC구조 파악하기
>   
>   먼저 첫번째 테이블은 고정적임
>   다음 테이블은, 나이 테이블 -> 나이는 범주형, 연속형, 그외속성으로 나뉘고 3개가 다 있거나 하나만 있을 수 있음.
>   그러므로 나오는대로 다만듬
>   total_dict['Arm Group List'][i] 에는 딕셔너리가 들어감. 각 딕셔너리의 키가 td가없는 데이터의 th, 즉 타이틀이됨.
>   
>   나이 그 외 특성 아웃라이어 : 
>   https://cris.nih.go.kr/cris/resultsearch/resultSearch.do/?seq=24196&search_page=L&search_lang=K
>   지역
>   https://cris.nih.go.kr/cris/resultsearch/resultSearch.do/?seq=6904&search_page=L&search_lang=K
>   
>   result_dict['Baseline Characteristics']['Arm Group List'][0].keys() = 
> dict_keys(['중재 / 관찰군명', '중재 / 관찰군 상세내용', '전체분석 대상수', '나이, 연속형 Dict', '성별 : 여성, 남성 Dict', '등록지역 Dict', 'Study Specific Measure List'])
>   
>   result_dict['Baseline Characteristics'].keys()
> dict_keys(['Arm Group List', 'Total', '분석단위', '전체분석 대상설명', '나이, 연속형 Dict', '성별 : 여성, 남성 Dict', '등록지역 Dict', 'Study Specific Measure List'])
> ```
> 
> </details>
> 
> <details>
> <summary>20230317</summary>
> 
> ```
> 
> ctrl + u : 리눅스 커맨드 삭제
> 
> 디비에 넣는 메소드
>   주요 아이디어 : 암그룹마다 공통데이터인지, 차이가나는지에 따라 테이블 분리
>   
> cris_ct_result_baseline_chc_desc : 첫번째 테이블의 모든 암그룹의 공통 데이터만
>   
> cris_ct_result_baseline_chc_age_categorical : 나이 범주형이 존재할때, 암그룹의 공통 데이터
> cris_ct_result_baseline_chc_age_continuous : 나이 연속형이 존재할때, 암그룹의 공통 데이터
> cris_ct_result_baseline_chc_age_other : 나이 그 외 특성이 존재할때, 암그룹의 공통 데이터
> 
> cris_ct_result_baseline_chc_gender : 성별 여성남성이 존재할때, 암그룹의 공통 데이터
> cris_ct_result_baseline_chc_gender_other : 성별 그 외 특성 존재할때, 암그룹의 공통 데이터
>   
> cris_ct_result_baseline_chc_enrollment_region : 등록지역, 공통데이터 
>   
> cris_ct_result_baseline_chc_other_specific : 그 외 특성, 같은 시퀀스에 대해 여러개의 OSSId가 있을 수 있다.
> OSSId를 사용함 (Other specific study Id)
>   
> 이제부턴 AGTId (Arm Group Title Id)를 암그룹 수에 따라 가질수 있음
> cris_ct_result_baseline_chc_arm : 첫번째 테이블 각각 암그룹 데이터 AGTId를 사용함
>   
> cris_ct_result_baseline_chc_arm_age_categorical : 나이 범주형 데이터, 암그룹마다 저장
> 
> 나이 연속형 데이터
> cris_ct_result_baseline_chc_arm_age_continuous_measure_type
> cris_ct_result_baseline_chc_arm_age_continuous_dispersion
>   -> 현재 테이블에 측정치 종류 분산도 측정을 따로 저장중인데, 한번에 저장하는거로 바꾸고, 
>   그 후 나이 연속형말고도 측정치 종류, 분산도 측정이 나올수있으므 만들어줘야함.
> 
> cris_ct_result_baseline_chc_arm_age_other_category : 한 시퀀스내에 여러개의 AGTId, 각각 AGTId당 AOCId가 할당될수있음.
> AOCId(Age other category Id)가 범주명의 갯수가됨.
>   
> cris_ct_result_baseline_chc_arm_age_other_category_result : 각 AOCId 에 ACRId할당.
>   연습용으로 좋은 seq : 13913
>   
> cris_ct_result_baseline_chc_arm_other_sp_category : 암그룹 -> 그외특성리스트 -> 범주명 리스트
> ```
> 
> </details>
</details>
  
<!--   week4 -->
  
<details>
<summary>week4</summary>
  
> <details>
> 
> <summary>20230320</summary>
> 
> ```
> 
> 분산도&측정치 수정 :
> cris_ct_result_baseline_chc_arm_age_continuous_measurements
> cris_ct_result_baseline_chc_arm_age_other_category_measurements
> cris_ct_result_baseline_chc_arm_gender_other_category_measurements
> 
> RAW -> REFINE 으로 옮기기
> 중요한 부분 : DB테이블이 변경되면, REFINE에 들어갈 데이터들도 바뀌어야하므로, 따로 코드를 수정해야함.
> 
> OM 분석하기
> 
> 결과변수의 갯수에 따라, 테이블의 갯수가 다름.
> 테이블 형식은, 결과변수 - 암그룹 정보 - data table 로 되어있음.
> 
> ct_result_list[i]['content']['Outcome Measure']['Outcome Measure List'][0] -> 0번째 OM, keys() 는
> dict_keys(['결과변수종류', '평가항목', '평가항목 상세설명', '평가시기', '통계분석', 'Arm Group List', '전체분석단위', '전체분석 대상설명', '측정단위']) 가 존재하고, Arm Group List를 제외하고 모두 공통항목임.
> 
> 기존의 방식에서 수정한부분 : 구조적으로는 없으나, 코드상오류가 하나 있었음
> 
> 나중에 다뤄야할 이슈 : 페이지 10개 넘어가면안됨.
> 
> AE 분석하기
> 
> 첫번째 테이블 고정
> 두번째 테이블은, 암그룹의 갯수만큼 column을 가짐. -> 행은 고정
> All cause mortality - 발생대상수, 연구대상수 고정
> Serious Adverse events - 발생대상수, 연구대상수, 이상반응 보고 횟수 고정
> 
> 
> ```
> 
> </details>
> 
> <details>
> 
> <summary>20230321</summary>
> 
> ```
> 
> 현재문제점 
> Other (Not Including Serious) Adverse Events 에서 
> 발생빈도보고기준 탭이 있으면, 데이터가 한칸씩 밀려남
> 
> Serious Adverse Events 에서
> Term, Total 아래 데이터는 무의미한 데이터로 취급함 -> 일단 유지 하기
> 
> 
> 
> ```
> 
> </details>
> 
> <details>
> 
> <summary>20230322</summary>
> 
> ```
> 
> cris api로 받아오기 : 페이지 설정을 해줘야함(데이터가 20개를 넘어가면 1페이지만으로 안끝남)
> prepared=True **
> 
> 
> ```
> 
> </details>
> 
> <details>
> 
> <summary>20230323</summary>
> 
> ```
> 
> DB에  만들기 : 
> import pymysql 을 import mysql.connector as pymysql 로 바꿔
> cursor 선언시 cursor = conn.cursor()  
> 
> 해야하는거 : sql구문 수정해서, 테이블 만들기
> 탈락사유 테이블 insert위해 함수만들기
> 
> cris_ct_result_baseline_chc_arm_age_other_category_result 수정해야함
> -> 수정완료
> 
> '측정치 종류', '분산도 측정' 이 나올수있는 데이터 : 나이연속 나이그외 성별그외 그외특성
> -> 나이연속은 이미존재하므로 총 6개의 추가 테이블을 만들어야함 : sql 수정, info 수정, 함수선언 
> 
> crisids받아오는 함수 수정
> 
> 
> ```
> 
> </details>
> 
> 
> 
> <details>
> 
> <summary>20230324</summary>
> 
> ```
> 
> 디비에서 스키마 잘못된것들 수정
> failed reason 에서 ISS -> FRS
> other sp 테이블 PRI key에 OSSID추가
> 
> eng차트 수정하기 
> 수정완료 
> DDL 수정
> info 수정
> extract_tree 수정
> parser 수정
> 
> ```
> 
> </details>

  
> </details>

<!-- week5 -->

<details>

<summary>week5</summary>

<details>
  
<summary>20230327</summary>
  
  ```
  
  Error occurred in cris_ct_result_outcome_measure_desc : Error while executing statement: Data too long for column 'outcome_measure_time_frame' at row 1 : 에러 수정 -> sql문 수정, 데이터의 입력값 범위 늘려야함
  varchar -> text 로 수정
  서버데이터삭제돼서 다시 옮겨오기
  ssh 접속시, fingerprint -> SSH에서 fingerprint는 공개키의 고유한 식별자로서, 해당 공개키가 유효하고 정확하게 인증된 것임을 보장하기 위한 기술적인 수단이다.
  
  ```
  
</details>

<details>
  
<summary>20230327</summary>
  
  ```
  
 연구결과가 있는 553개 데이터에 대해 크롤링하기
Error occurred in cris_ct_result_participant_flow_arm_group_failed_reason_eng : Error while executing statement: Data too long for column 'failed_reason' at row 1
Error occurred in cris_ct_result_baseline_chc_arm_eng : Error while executing statement: Data too long for column 'arm_group_title' at row 1
Error occurred in cris_ct_result_baseline_chc_arm_age_other_category_eng : Error while executing statement: Data too long for column 'category_title' at row 1
Error occurred in cris_ct_result_baseline_chc_arm_gender_other_category_result_eng : Error while executing statement: Data too long for column 'category_result' at row 1
Error occurred in cris_ct_result_outcome_measure_arm_group_eng : Error while executing statement: Data too long for column 'arm_group_title' at row 1
Error occurred in cris_ct_result_adverse_events_arm_group_eng : Error while executing statement: Data too long for column 'arm_group_title' at row 1
-> sql에서 text로 바꿔주기
  
  '분석대상수' 탭이 두개의 th로 나뉘어진경우, 스키마네임에 ''이 들어감 -> 예외처리를해줘야함
  
 현재 발생한 문제점 :
 1. DB에 저장이 안되는 테이블이 존재 -> 그러나 eng은 잘 저장이 되어있음. -> eng,kor 비교해서 해결하자
 cris_ct_result_adverse_events_all_cause_mortaity
 cris_ct_result_adverse_events_other_adverse_events
cris_ct_result_adverse_events_other_adverse_reaction
cris_ct_result_adverse_events_serious_adverse_events
cris_ct_result_adverse_events_serious_adverse_reaction

cris_ct_result_outcome_measure_arm_group_category
cris_ct_result_outcome_measure_arm_group_category_result

2. cris_ct_result_outcome_measure_desc_eng 에 데이터가 저장이안됨 -> 코드수정해야함



  ```
  
</details>

</details>

</details>


