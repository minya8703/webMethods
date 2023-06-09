# webMethods Service Designer를 사용하여 Adapter 서비스 생성 방법

https://tech.forums.softwareag.com/t/creating-adapter-services-using-webmethods-service-designer/237293 

## 단계
### 신뢰할수 있는 데이터 베이스 드라이버 얻기

### webMethods Integration Server에서 JDBC 연결
- (https://kylenoh-developer-note.tistory.com/entry/webMethods-Adapter)
	- 데이터 베이스 드라이버를 " Install_location \IntegrationServer\packages\WmJDBCAdapter\code\jars"에 추가
	- webMethods 서비스 디자이너를 실행(EAI 서버에서 설정)
		1. 관리자 권한으로 실행
		2. Adapter  > JDBC용 webMethods Adapter 를 클릭
		3. 새연결 구성을 클릭
		4. JDBC연결용 webMethods 어댑터 연결 유형을 선택
		5. 연결 유형 구성 페이지 에서 연결 세부 정보 구성
		6. 연결 저장을 클릭
		7. webMethods Adapter for JDBC 연결 페이지의 사용 가능 열에서 예를 선택하여 연결을 사용

### JDBC 연결을 사용하여 Adapter 를 생성하여 데이터의 정보를 얻어 옵니다.
	1. 새 패키지를 생성
		1. File > New > Package를 클릭
		2. 패키지 이름을 지정
	2. 패키지에 새 폴더를 만듭니다.
		1. File > New > Folder를 클릭
		2. 폴더 이름을 지정
	3. 폴더에 새 Adapter 서비스를 만듭니다.
		1. File > New > > Adapter  Service를 클릭
		2. 파일명에 Interface ID 를 입력하고 다음을 클릭
		3. Adapter Type 을 선택하고 다음
		4. 연결할 Adapter Connection Name을 선택하고 다음
		5.  작성할 Template 을 선택하여 Finish
	4. 작성한 Adapter 서비스에서  선택합니다.
		1.  Tables 탭에서 테이블 이름 열에서 ???을 클릭
		2. Adapter Tree Chooser 화면에서 사용할 테이블을 선택하여 OK
	5. 작성한 Adapter 서비스에서 SELECT 탭을 선택합니다.
		1. 테이블 행을 채우려면 아래의 아이콘 클릭
		   
		2. 테이블의 레코드가 표시됩니다.
	6. 필터 조건을 추가 하기 위해서는 WHERE 탭을 선택합니다.
		1. 필터 조건을 추가하려면 아래의 아이콘을 클릭
		   
	7. Adapter 서비스를 실행
		1. File > Save All 을 클릭
		2. Adapter 서비스를 마우스 오른쪽 버튼으로 클릭하여 Run As > Run Service 를 선택
		3. 어댑터 서비스 입력 마법사에서 필터조건을 입력하고 확인을 클릭
		   
		   

필터 조건에 따른 결과가 표시됩니다.




https://github.com/SoftwareAG


###   Package 명 <br>
   ├If 폴더명 : interface ID로 생성 <br>
   │├ adpt : Adapter Service 생성 용 폴더 <br>
   ││├ adpt_noti :  <br>
   ││├ adpt_serv: <br>
   │├ doc : Document 생성용 폴더 <br>
   │├ serv :  Flow Service 생성 용 폴더 <br>
   │├socket :  <br>
   │├tring : <br>
   │├ ws :  <br>
