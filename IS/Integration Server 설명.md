
[[Integration Server Administrator's Guide]](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/index.html#page/b2b-integration-compendium%2F_b2b_integration_compendium.1.2334.html%23)


# Integration Server
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-07 오전 8_49_06](https://github.com/minya8703/webMethods/assets/97384342/fa6264d5-08b8-4ec0-aaa9-cebbdaeae80c)
IS 환경에서 관리자는 webMethods Integration Server의 설치, 구성 및 유지 관리를 담당
## 1. Server
![image](https://github.com/minya8703/webMethods/assets/97384342/e087023e-e460-4cc6-a0e7-e1956a270a22)

### 1-1.Scheduler
- 서버의 스케줄링 기능을 사용하여 지정한 시간에 서비스가 실행되도록 한다.

![image](https://github.com/minya8703/webMethods/assets/97384342/38d4ce1f-5919-481c-a42f-ce6676370201)
#### ■ Pause Scheduler (currently Running)
  - 현재 실행중인 스케줄러 일시 정지 버튼
  - 링크를 누르면 아래와 같이 표시

![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-07 오전 8_58_08](https://github.com/minya8703/webMethods/assets/97384342/4a485328-6a16-4025-ac36-17810c7e5082)
#### ■ View System Tasks
그림 추가 필요
  - 예약된 각 작업의 이름, 서버가 작업을 실행할 다음 날짜 및 시간, 서버가 적업을 실행하는 빈도등이 표시
  - Session, Listener log 등 같은 시스템 스케줄러

#### ■ Create a Scheduled Task
![192 168 110 205_5097_ (1)](https://github.com/minya8703/webMethods/assets/97384342/5e353c04-2ff9-4648-8edf-bc5e973ad2ed)

|or this parameter|Specify|
|---|---|
|Description|스케줄러 상태 설명|
|folder.subfolder:service|통합 서버가 실행할 서비스의 전체 경로와 서비스 이름|
|Run As User|스케줄러를 실행할 때 서버에서 실행시키는 사용자 이름 <br> ex).Administrator|
|Target Node|동일한 데이터베이스에 연결된 다른 통합 서버 에서 작업을 실행할지 여부 <br> Any server - 작업이 데이터베이스에 연결된 하나의 서버에서만 실행 되어야 하고 어떤 서버인지는 중요하지 않은 경우 <br> All servers - 클러스터된 모든 통합서버에서 실행 <br> 선택된 서버 - 스케줄러가 특정 서버에서만 실행되어야 하는 경우|

- If the Task Is Overdue

|This parameter|Specify|
|---|---|
|Run immediately|즉시 실행|
|Skip and run at next scheduled time|이 작업 실행을 건너뛰고 예약된 다음 실행 시간에 다시 실행|
|Suspend|관리자가 작업을 재개하거나 취소할 때까지 작업을 일시 중단 상태|

 ```
Note: "if more than xxx minutes late"  이 필드가 허용할수 있는 최대 시간(분)은 35000분
이 필드에 지정한 분 수만큼 예약된 시작 시간을 놓친 경우 "지연 작업"을 수행
```

- Run Once, Repeating, or Complex Repeating

|Select|To|
|---|---|
|Run Once|한 번만 실행되도록 작업을 예약  <br> **Date** - 통합서버에서 실행할 날짜 YYYY/MM/DD 형식<br> **Time** - 통합 서버에서 실행할 시간 HH:MM:SS 형식|
|Repeating|예를 들어 하루에 한 번 특정 시간에 단순 반복 작업을 예약 <br> **Start Date** - 첫 번째 실행 날짜 및 시간<br> **End Date** - 마지막으로 실행 날짜 및 시간 종료 날짜를 생략하면 무기한으로 실행<br> **Interval** - 실행 주기 서비스 실행 사이에 대기할 시간(초)을 입력<br> **Repeat after completion** - 다음 서비스를 시작하기 전에 서비스의 이전 실행이 완료될 때까지 대기여부 Repeat after completion의 체크 박스를 선택하면 서비스를 실행전에 전에 실행된 서비스가 완료될 때까지 기다리며 서비스가 지연 된다.|
|Complex Repeating|격일 또는 한 달에 두 번과 같이 보다 복잡한 간격으로 반복되는 작업을 예약 <br> **Start Date** - 첫 번째 실행 날짜 및 시간<br> **End Date** - 마지막으로 실행 날짜 및 시간 종료 날짜를 생략하면 무기한으로 실행<br> **Repeat after completion** - 다음 서비스를 시작하기 전에 서비스의 이전 실행이 완료될 때까지 대기여부 Repeat after completion의 체크 박스를 선택하면 서비스를 실행전에 전에 실행된 서비스가 완료될 때까지 기다리며 서비스가 지연 된다. <br> **Run Mask.** - 서비스를 실행하려는 특정 월, 날짜, 요일, 시간, 분, 초 각 범주에서 하나 이상항목을 선택할수 있으며 여러항목을 선택하려면 CTRL키를 누르면서 선택|


#### ■ Filter Services
![192 168 110 205_5097_ (2)](https://github.com/minya8703/webMethods/assets/97384342/e2c6eaca-2618-48fc-9969-d6b8d3eaf5bb)
- 필터를 사용하여 표시할 작업 목록을 관리하기 쉽게 만들수 있다.

|Option|Description|
|---|---|
|Service Name| 검색하고자 하는 서비스 이름 "*"(별표) 및 "?" (물음표)만 지원, 서비스 이름은 대소문자를 구분|
|Status Is Active|활성화 되어 있는 서비스만 표시를 선택 또는 선택하지않으면 모든 서비스를 조회|
|Hide Remote Tasks|현재 서버에서 실행되는 작업만 표시할지를 선택|


### 1-2. Service Usage
- 본 화면에서는 각 캐시 제어 서비스에 대한 캐시 제어 설정의 현재 결과가 표시됨

### 1-3. Statistics
![image](https://github.com/minya8703/webMethods/assets/97384342/deecbf6f-f457-4158-99f2-ac632d62598f)

## 2. Logs
- 각 영역별 발생한 로그를 표시
### 2-1. Error
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-07 오전 9_04_17](https://github.com/minya8703/webMethods/assets/97384342/d8b565e0-fd51-434a-8c31-0d8c9eaf0b4a)
- 통합 서버 관리자에서어 오류 로그를 표시

|Column|Details|
|---|---|
|Timestamp| 로그에 기록된 날짜 및 시간|
|Service Name| 예외가 발생한 서비스의 이름|
|Service Stack| 예외가 발생한 서비스에 대한 상위 서비스|
|Error Message| 발생한 예외를 설명하는 메시지|
|Stack Trace| 예외로 이어지는 호출 시퀀스를 표시하는 추적입니다. 스택 추적 데이터의 표시를 확장하려면 로그 표시 제어 영역에서 스택 추적 데이터 확장 확인란을 선택 하고 새로 고침을 클릭합니다 .|
|Root Context <br> Parent Context <br> Current Context| 컨텍스트 정보 webMethods Monitor는 다른 로그의 관련 항목을 연결하는 데 사용|

### 2-2. Guaranteed Delivery
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-07 오전 9_11_02](https://github.com/minya8703/webMethods/assets/97384342/0e16f940-de24-4ad5-8b0a-9d24b60eb127)
- 통합 서버 의 보장된 전달 기능을 사용하여 보장된 일회성 서비스 실행을 보장
- 통합 서버 보장 전달 기능은 일시적인 오류에도 불구하고 다음이 발생하도록 보장
  - 클라이언트의 서비스 실행 요청이 서버로 전달
  - 서비스는 한 번만 실행되며 한 번만 실행
  - 서비스 실행에 대한 응답을 클라이언트로 전달
### 2-3. Security
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-07 오전 9_11_02](https://github.com/minya8703/webMethods/assets/97384342/66cd3109-4c93-49f7-bda2-3b33d68759db)
### 2-4. Server
![Editing webMethods_IS_Integration Server 설명 md at main · minya8703_webMethods - Chrome 2023-08-07 오전 9_16_59](https://github.com/minya8703/webMethods/assets/97384342/6f2ac7a8-6da8-418b-b489-a4a64754c0bc)
### 2-5. Service
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-07 오전 9_19_39](https://github.com/minya8703/webMethods/assets/97384342/5cbec4ec-f5cf-4105-bf15-94c679887a56)
### 2-6. Session
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-07 오전 9_26_49](https://github.com/minya8703/webMethods/assets/97384342/1f7575b5-a2dc-4b3d-a7c3-8f40e5334d9b)


## 3. Packages
- 패키지를 사용하여 서비스 및 관련 파일을 그룹화
![192 168 230 89_5097 - webMethods Integration Server - Chrome 2023-08-09 오전 9_11_40](https://github.com/minya8703/webMethods/assets/97384342/fa6054cf-8f03-4309-8c14-a7d5266ab99b)

### 3-1. Management
- Integration Server에서 구성된 패키지들을 관리
### 3-2. Publishing
- 서버별 사용유저 추가 삭제 관리
### 3-3. Subscribing
- 유저에게 사용 package 추가 삭제 관리
- 사용할 유저가 구독 요청을 만들기 위해 게시자에 연결하는 데 사용하는 방법
- 관리자가 사용유저에게 패키지를 보낼 때 연결하는 데 사용하는 방법
## 4. Solutions
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-09 오전 10_43_48](https://github.com/minya8703/webMethods/assets/97384342/15c3e953-ead2-4d72-87cf-5107691103ff)
### 4-1. VCS...
- 버전 제어 관리를 위한 시스템
![webMethods Deployer - Chrome 2023-08-09 오전 10_50_14](https://github.com/minya8703/webMethods/assets/97384342/87ac4e5a-ad38-4d7b-91b0-f19c5b6fd3ed)

### 4-2. Deployer...
- 다른 서버에 개발한 자산을 배포
![webMethods Deployer - Chrome 2023-08-09 오전 10_49_04](https://github.com/minya8703/webMethods/assets/97384342/49c555c4-a998-43e9-be53-a851462acf36)

## 5. Adapters
![Editing webMethods_SAP_회계용어 md at main · minya8703_webMethods - Chrome 2023-08-09 오전 10_47_48](https://github.com/minya8703/webMethods/assets/97384342/987e134a-790f-4b93-9b47-73ee139ff2b4)

### 5-1. PKI...
- PKI (공개키기반구조) 관리
![PKI - WEAI-DA02 - webMethods Integration Server - Chrome 2023-08-09 오전 11_04_48](https://github.com/minya8703/webMethods/assets/97384342/5c37d82d-7c83-47de-a9e3-5d1818900d06)

### 5-2. WmDB...
- WmDB 패키지를 사용하여 데이터베이스에 액세스
- 데이터베이스에 연결하는 서비스를 구축하는 데 사용할 수 있는 서비스 및 DSP(Dynamic Server Pages)가 포함되어 있다.
![WmDB - WEAI-DA02 - webMethods Integration Server - Chrome 2023-08-09 오전 11_05_45](https://github.com/minya8703/webMethods/assets/97384342/24631690-3fcd-4938-92d1-25d1763ef8a5)

### 5-3. JDBC Adapter...
[9-0_Adapter_for_JDBC_Install_and_Users_Guide.pdf] (https://documentation.softwareag.com/webmethods/adapters_estandards/Adapters/JDBC/JDBC_9-0/9-0_Adapter_for_JDBC_Install_and_Users_Guide.pdf, "JDBC Adapter Guide 참조")

![9-0_Adapter_for_JDBC_Install_and_Users_Guide pdf - Chrome 2023-08-09 오후 12_36_42](https://github.com/minya8703/webMethods/assets/97384342/b9a3fc67-d2f8-4c0e-a55a-971a08406d6c)

- JDBC 연결을 위한 어댑터를 구성할 때 다음과 같은 정보를 지정 Intergration Server는 JDBC 시스템에 연결하는 데 사용
- 어댑터를 구성할 수 있으며, Intergration Server 관리자 화면을 사용하여 수동으로 JDBC 연결 또는프로그래밍 방식으로 pub.jdbcAdapter:createConnectionNodes 서비스를 사용 및 관리

연결 방법은 따로 추가 예정.

### 5-4. SAP Adapter...
[webMethods SAP Adapter User’s Guide Version 6.5 SP1] : (https://documentation.softwareag.com/webmethods/adapters_estandards/Adapters/SAP/SAP_6-5/webMethods%20SAP%20Adapter%20Users%20Guide%206.5%20Service%20Pack%201.pdf)
- SAP 시스템에 대한 연결을 설정 및 관리
![Editing webMethods_IS_Integration Server 설명 md at main · minya8703_webMethods - Chrome 2023-08-09 오후 12_51_42](https://github.com/minya8703/webMethods/assets/97384342/9a3908c5-0765-4caf-997d-899c4608868f)

연결 방법은 따로 추가 예정.

## 6. webMethods Cloud
### 6-1. Settings
### 6-2. Accounts
### 6-3. Applications


## 7. Security
### 6-1. ACLs
- Integration Server에 있는 패키지, 폴더, 파일, 서비스 및 기타 요소에 대한 액세스를 제어
- ex) https://tech.forums.softwareag.com/t/invoking-integration-server-service-using-basic-authentication-http/238345
### 7-2. Certificates

### 7-3. CSRF Guard
- CSRF(Cross-Site Request Forgery)는 웹 사이트 및 웹 애플리케이션에 대한 가장 일반적인 공격 중 하나입니다. CSRF 공격은 사용자가 악의적인 요청이 포함된 웹 페이지를 실수로 로드할 때 발생합니다. 이 웹 페이지는 구성 변경 또는 서비스 호출과 같은 원하지 않는 작업을 수행하기 위해 사용자의 ID 및 권한을 사용하여 웹 사이트 또는 웹 응용 프로그램에 악의적인 요청을 보냅니다.
애플리케이션이 인증된 사용자의 입력을 기반으로 작업을 수행하지만 사용자가 특정 작업을 승인하도록 요구하지 않는 경우 웹 애플리케이션은 CSRF 공격에 취약합니다. 즉, 웹 브라우저에 저장된 쿠키로 웹 응용 프로그램에 대해 인증을 받은 경우 자신도 모르게 응용 프로그램에 악의적인 HTTP 또는 HTTPS 요청을 보낼 수 있습니다.
- 통합 서버는 CSRF 보호 기능을 사용하여 CSRF 공격을 방지합니다. 통합 서버는 통합 서버 관리자 또는 기타 클라이언트 응용 프로그램 에서 인증 요청을 받을 때 세션당 하나의 CSRF 보안 토큰을 생성하여 CSRF 공격을 방지합니다 . 통합 서버는 세션이 만료될 때까지 이 CSRF 보안 토큰을 후속 요청에 추가합니다. CSRF 토큰은 세션이 종료되면 만료됩니다.
요청을 보낼 때 통합 서버는 요청에 있는 토큰의 존재와 유효성을 확인하고 이를 세션의 토큰과 비교합니다. 요청에 토큰이 없거나 요청의 토큰이 세션의 토큰과 일치하지 않는 경우 통합 서버는 요청을 종료합니다. 통합 서버는 또한 이벤트를 서버 로그 및 보안 감사 로그에 잠재적인 CSRF 공격으로 기록합니다.
통합 서버 관리자를 사용하여 통합 서버 에서 CSRF 보호를 활성화하거나 비활성화합니다 .

### 7-4. Enterprise Gateway Rules
Enterprise Gateway Rules은 Enterprise Gateway 서버를 통해 내부 서버로 전달할 수 있는 요청을 결정하는 하나 이상의 필터로 구성
### 7-5. Keystore
- 통합 서버는 개인 키와 SSL 인증서를 키 저장소 파일에 저장하고 인증서의 신뢰할 수 있는 루트를 신뢰 저장소 파일에 저장합니다. 키 저장소 및 신뢰 저장소는 업계 표준 파일 형식의 보안 파일입니다.
### 7-6. OAuth
- 통합 서버는 OAuth 클라이언트, 권한 부여 서버 또는 자원 서버일 수 있습니다. 통합 서버 관리자는 개발자가 이러한 역할을 만들고 관리하는 데 사용할 수 있는 OAuth 구성 기능을 제공합니다. OAuth 기능을 활성화하려면 통합 서버 에 Software AG의 라이선스가 있어야 합니다. 
### 7-7. Outbound Passwords
- 정상적인 작업의 일부로 통합 서버는 원격 통합 서버 , 프록시 서버 및 데이터베이스 와 같은 응용 프로그램 및 하위 시스템에 연결할 수 있습니다 . 클라이언트 역할을 하는 통합 서버는 이들 시스템에 연결하기 전에 각 시스템에 아웃바운드 비밀번호 라고 하는 비밀번호를 제공해야 합니다 . 통합 서버는 아웃바운드 비밀번호를 사용하여 자신을 식별하거나 다른 시스템 에 인증합니다 .
데이터베이스와 같은 애플리케이션 또는 서브시스템에 연결하도록 통합 서버를 구성할 때 통합 서버가 데이터베이스 서버에 연결하기 위해 보내야 하는 비밀번호를 지정합니다 . 나중에 통합 서버 사용자가 데이터베이스가 필요한 요청을 하면 통합 서버는 구성된 비밀번호를 데이터베이스 서버로 보내고 연결합니다.
### 7-8. Ports
- 통합 서버는 지정한 포트에서 요청을 수신합니다. 각 포트는 HTTP, HTTPS, FTP, FTPS, WebSockets, 이메일 또는 파일 폴링과 같은 특정 유형의 프로토콜과 연결
### 7-9. SAML
- 인증을 위해 WS-SecurityPolicy를 기반으로 하는 정책을 사용하고 해당 정책에 SAML 토큰이 필요한 경우 SAML 토큰을 처리할 수 있도록 통합 서버를 설정해야 합니다 . 통합 서버는 인바운드 요청에 대해 공급자 웹 서비스 설명자에 연결된 정책에서만 SAML 토큰을 지원
- 클라이언트 인증을 위해 SAML 토큰을 포함하는 WS-SecurityPolicy 기반 정책을 사용하려면 SAML 토큰을 처리할 수 있도록 통합 서버를 설정해야 합니다. 요구 사항 중 하나는 통합 서버가 신뢰하도록 할 STS를 식별하는 것입니다. 
### 7-10. User Management
## 8. Settings
![192 168 230 90_5097 - webMethods Integration Server - Chrome 2023-08-09 오후 3_08_37](https://github.com/minya8703/webMethods/assets/97384342/694732e3-27e3-49d9-af46-8f60177303a3)
### 8-1. Caching
https://documentation.softwareag.com/webmethods/microservices_container/msc10-5/10-5_MSC_PIE_webhelp/index.html#page/pie-webhelp%2Fto-configuring_ehcache_on_integration_server.html%23
- 캐시를 생성, 편집, 지우기, 비활성화, 활성화 및 삭제
- Integration Server 및 Integration Server 에서 실행되는 Software AG 구성 요소는 Ehcache를 사용하여 많은 자체 내부 작업과 관련된 데이터를 캐시합니다. 또한 Integration Server는 일련의 공용 서비스를 제공합니다( pub.cacheWmPublic 패키지의 폴더) 개발자가 빌드하는 솔루션에 캐싱 기능을 추가하는 데 사용할 수 있다.
- 캐싱은 자주 사용하는 데이터를 메모리에 유지하여 서비스의 성능을 향상시킬 수 있는 최적화 기능입니다. 캐싱은 트래픽이 많은 웹 서버 및 데이터베이스에서 정보를 검색하는 서비스의 응답 시간을 크게 향상시킬 수 있습니다.
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-09 오후 3_49_19](https://github.com/minya8703/webMethods/assets/97384342/eb161974-246a-4889-8034-08d5a25c7719)

### 8-2. Clustering
- 서버 클러스터링을 사용하도록 설정한 경우 의 모든 서버 목록을 표시할 수 있으며, 클러스터. 서버는 정보를 검색하여 클러스터에 있는 다른 서버를 학습 할 수 있다.
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-09 오후 4_27_24](https://github.com/minya8703/webMethods/assets/97384342/019331c0-a026-4db7-bc9e-e6c96b18dee8)

### 8-3. Enhanced XML Parsing
- 메모리 사용 제한과 사용 제한이 충족될 때 파티션이 로컬 디스크 저장소 또는 BigMemory 로 오버플로되는지 여부를 나타냅니다.
![192 168 230 90_5097 - webMethods Integration Server - Chrome 2023-08-09 오후 3_06_43](https://github.com/minya8703/webMethods/assets/97384342/c68444fc-7a2f-4048-a4d0-6c032b3c47da)

### 8-4. Global Variables
- Intergration Server를 사용하여 전역 변수를 정의할 수 있다.
- 작성 중인 전역 변수가 비밀번호인 경우 Integration Server는 OPE(아웃바운드 비밀번호 암호화)를 사용하여 이를 암호화하고 저장
- 전역 변수 값의 최대 길이는 255자
- 전역 변수를 편집할 때 값 필드만 수정할 수 있다.
- 전역 변수는 클러스터의 모든 Integration Server에서 동일해야 한다.
- webMethods Deployer를 사용하여 전역 변수를 배포할 수 있다.
- 서비스를 디버깅할 때 전역 변수 대체를 사용할 수 있다.
|Parameter|Specify|
|---|---|
|Is Password?|정의하는 전역 변수가 암호인지 여부|
|Key|전역 변수의 이름입니다. Integration Server는 전역 변수 대체를 수행하는 동안 이 키를 사용하여 전역 변수를 참조|
|Value|전역 변수의 값|

![192 168 230 90_5097 - webMethods Integration Server - Chrome 2023-08-09 오후 3_00_20](https://github.com/minya8703/webMethods/assets/97384342/64e0b2bb-ea3b-4e8d-be11-ab0d96290557)

### 8-5. JDBC Pools
- Integration Server를 외부 RDBMS의 데이터베이스 구성 요소에 연결합니다 .
- *JDBC 데이터베이스 연결 풀을 정의합니다 . 연결 풀은 Integration Server를 데이터베이스 구성 요소를 호스트하는 데이터베이스 서버에 연결하기 위한 매개변수를 지정합니다 . 런타임 시 Integration Server는 각 데이터베이스 구성 요소에 대해 별도의 연결 풀 인스턴스를 생성합니다.
*데이터베이스 구성 요소에 대한 연결 풀에서 각 기능을 지정하여 데이터베이스 구성 요소에 쓰도록 기능을 지시합니다 . 예를 들어, ISCoreAudit 데이터베이스 구성 요소의 연결 풀에서 ISCoreAudit Log 함수를 가리키고, CrossReference 데이터베이스 구성 요소의 연결 풀에서 Xref 함수를 가리키는 식입니다. Integration Server는 데이터베이스 구성요소에 쓸 수 있는 각 데이터 유형에 대해 사전 정의된 기능을 제공합니다.
Integration Server 설치 중에 외부 데이터베이스를 사용하도록 선택하면 설치 프로그램에서 데이터베이스 연결 매개변수를 제공하도록 요청합니다. Integration Server를 처음 시작하면 Integration Server는 제공된 매개변수에서 하나의 JDBC 연결 풀을 생성하고 해당 풀을 사용하여 데이터베이스 구성 요소에 쓰도록 미리 정의된 함수를 구성합니다 .

![192 168 230 90_5097 - webMethods Integration Server - Chrome 2023-08-09 오후 4_37_14](https://github.com/minya8703/webMethods/assets/97384342/b7f30b59-6784-4981-a2a2-601b1dda0043)


### 8-6. Licensing
- 라이센스 정보를 보거나 Integration Server의 라이센스 키를 변경 가능
### 8-7. Logging
- 플랫폼에 대한 로깅은 플랫폼 활동을 모니터링하고 문제를 수정하는 데 필요한 중요한 데이터를 제공
- Universal Messaging 클라이언트 로그 파일은 umClient.log라고 합니다. 범용 메시징 클라이언트 로그 파일 의 세부 정보 양을 제어하도록 UM 클라이언트 로거를 구성할 수 있습니다 .
### 8-8. Messaging
- 메시징은 webMethods 플랫폼 에서 문서(메시지라고도 함)를 보내고 받는 포괄적인 용어로 Integration Server 컨텍스트 내에서 webMethods 메시징 에는 하나 의 Integration Server 또는 Integration Server 에서 실행되는 애플리케이션에서 webMethods 메시징 공급자 로의 기본 IData 형식으로 문서 게시가 포함됩니다 . Software AG Universal Messaging 또는 webMethods Broker 중 하나인 webMethods 메시징 공급자는 다른 Integration Server 의 구독자에게 문서를 라우팅합니다.문서를 검색하고 처리하는 s. webMethods 메시지는 네이티브 메시징이라고도 합니다.
https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/index.html#page/b2b-integration-compendium%2Fconfigure_wm_msg_connection_alias_4.html

### 8-9. Metadata
- CentraSite 에 있는 공유 라이브러리 또는 레지스트리에 정보 또는 메타데이터를 게시 및 철회 할 수 있으며, 이 메타데이터를 게시하면 이러한 자산을 다른 CentraSite 사용자 가 사용할 수 있습니다 . 
- pub.metadata.assets:publishPackages 서비스 를 사용하여 메타데이터를 게시하려면 먼저 CentraSite 의 공유 라이브러리에 연결하도록 Integration Server를 구성하면서 CentraSite설정시 사용
### 8-10. Proxy Servers
- Integration Server는 원격 서버에 대해 요청을 실행할 때 지정된 대상 서버에 HTTP, HTTPS, FTP 또는 SOCKS 요청을 발행합니다. 예를 들어 Integration Server는 원격 Integration Server 에서 서비스를 호출하거나 웹 서비스를 호출하는 웹 서비스 커넥터를 실행할 수 있습니다. Integration Server가 방화벽 뒤에 있고 타사 프록시 서버를 통해 이러한 HTTP, HTTPS, FTP 또는 SOCKS 요청을 라우팅해야 하는 경우 Integration Server 관리자를 사용하여 Integration Server가 이러한 요청을 라우팅할 하나 이상의 프록시 서버를 식별 할 수 있습니다. .
Integration Server가 프록시 서버를 사용 하려면 프록시 서버 별명을 정의해야 합니다 . 프록시 서버 별칭은 프록시 서버와 요청을 라우팅하려는 서버의 포트를 식별합니다.
각 아웃바운드 요청 유형(HTTP, HTTPS, FTP 및 SOCKS)에 대해 요청을 하나 이상의 프록시 서버 별명으로 라우팅하도록 Integration Server를 구성할 수 있습니다 .
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-10 오전 9_57_15](https://github.com/minya8703/webMethods/assets/97384342/aa139f9d-8f77-4b28-a4bf-b00d564dbf4d)

### 8-11. Quiesce
- 유지 관리를 위해 서버 중지
- Ports : 통합 서버는 정지 모드를 시작하고 종료하는 데 사용되는 진단 포트와 포트를 제외한 모든 포트를 비활성화
- JMS messaging : 통합 서버는 모든 JMS 연결 별칭을 비활성화하고 SOAP-JMS 트리거 및 웹 서비스 엔드포인트 트리거를 포함한 모든 JMS 트리거를 일시 중단합니다. 이것은 새 메시지의 검색 및 처리를 방지
- webMethods messaging : 통합 서버는 Universal Messaging을 메시징 공급자로 지정하는 모든 webMethods 메시징 연결 별칭을 비활성화합니다. 또한 통합 서버는 통합 서버 에서 로컬로 게시된 문서 또는 Universal Messaging , Broker 에서 문서를 수신하는 webMethods 메시징 트리거를 포함하는 webMethods 메시징 트리거 에 대한 문서 검색 및 문서 처리를 일시 중단합니다 . 실행 중인 모든 트리거 서비스는 완료될 때까지 실행을 시도합니다. 통합 서버 방법에 대한 자세한 내용은webMethods 메시징 트리거 에 대한 문서 검색을 일시 중단
- Packages : 통합 서버는 WmRoot 및 WmPublic을 제외한 모든 패키지를 비활성화합니다. 서버는 패키지와 해당 리소스를 언로드하고 패키지의 종료 서비스를 완료하며 메모리에서 패키지를 비활성화
- Scheduled user tasks : 통합 서버는 스케줄러를 일시 중지하고 이미 실행 중인 예약된 사용자 작업의 완료를 허용하며 아직 시작되지 않은 예약된 사용자 작업을 일시 중단합니다. 종속 서비스가 비활성화되기 전에 실행 중인 사용자 작업이 완료되지 않으면 해결되지 않은 종속성으로 인해 작업이 오류로 종료
- Guaranteed delivery : 통합 서버는 인바운드 및 아웃바운드 보장 전달 작업 관리자를 종료하고 문서의 인바운드 및 아웃바운드 보장 전달을 모두 중지합니다. 아웃바운드 전달의 경우 서버는 watt 속성 watt.tx.disabled를 True로 설정하여 아웃바운드 요청에 대한 보장된 전달 사용을 비활성화
- Clustering : Integration Server는 Integration Server_directory \instances\ instance_name \config\Caching 디렉토리 에 있는 모든 캐시 관리자를 종료 하고 클러스터를 종료
- Active tasks : Integration Server는 Integration Server가 정지 모드에 들어가기 전에 시작된 사용자 작업을 완료합니다 . 통합 서버는 정지 모드에 있는 동안 예약된 시스템 작업을 계속 처리
- Audit logging : 서버는 정지 모드에 있는 동안 데이터베이스에 감사 로깅 레코드를 계속 씁니다.
- Enterprise Gateway : 내부 서버 역할을 하는 통합 서버가 중지 되면 서버는 엔터프라이즈 게이트웨이 서버 에 대한 기존 연결을 끊고 서버가 중지 모드로 전환되기 전에 시작된 사용자 작업을 완료합니다. 엔터프라이즈 게이트웨이 서버 역할을 하는 통합 서버가 중지 되면 서버의 외부 및 등록 포트가 비활성화되고 내부 서버에 대한 기존 연결의 연결이 끊어지며 내부 서버에서 엔터프라이즈 게이트웨이 서버 에 대한 모든 요청이 시간 초과됩니다.
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-10 오전 9_58_14](https://github.com/minya8703/webMethods/assets/97384342/e0962300-32ff-4765-8034-fdaee38756d2)

### 8-12. Remote Servers
- 원격 서버에 대한 alias를 설정할 수 있습니다. alias를 통한 통신이 최적화되어 원격 서버와의 트랜잭션이 더 빨라집니다.
### 8-13. Resources

- XA 트랜잭션 복구를 활성화하거나 비활성화할 수 있습니다 . XA 트랜잭션 복구를 비활성화하면 통합 서버는 불완전한 트랜잭션을 자동으로 복구하려고 시도하지 않습니다. 또한 통합 서버 관리자를 사용하여 불완전한 트랜잭션을 수동으로 복구할 수 없습니다.
향상된 처리 성능에 대한 대가로 XA 트랜잭션 의 안정성과 복구를 기꺼이 교환하려는 경우 XA 트랜잭션 복구를 비활성화할 수 있습니다 . 기본적으로 통합 서버는 XA 트랜잭션 복구를 사용합니다 .
- 합 서버 에서 사용자에 대한 참조를 제거하는 과정에서 전자 메일 주소에 대한 참조도 제거해야 할 수 있습니다 . 다음을 검토하고 필요에 따라 이메일 주소를 제거하거나 바꾸십시오.
*중요한 정보, 새 패키지 릴리스, 규칙 위반 등에 대한 알림을 위한 이메일 주소. 다음 중 하나 이상의 이메일 주소를 업데이트해야 할 수 있습니다 .
- 통합 서버 에서 사용자에 대한 참조를 제거하는 과정에서 전자 메일 주소에 대한 참조도 제거해야 할 수 있습니다 . 다음을 검토하고 필요에 따라 이메일 주소를 제거하거나 바꾸십시오.
*중요한 정보, 새 패키지 릴리스, 규칙 위반 등에 대한 알림을 위한 이메일 주소. 다음 중 하나 이상의 이메일 주소를 업데이트해야 할 수 있습니다 .
### 8-14. SFTP
- SFTP(SSH 파일 전송 프로토콜)는 SSH(Secure Shell 프로토콜)를 기반으로 하는 네트워크 프로토콜입니다. SFTP는 안정적인 데이터 스트림을 통해 안전한 파일 액세스, 파일 전송 및 파일 관리를 용이하게 합니다.
### 8-15. URL Aliases
- URL alias를 생성할 때 통합 서버 의 리소스와 alias 간의 연결을 생성
- HTTP URL alias는 URL의 일부를 통합 서버 의 리소스로 바꾸기 위해 만드는 alias입니다 . URL alias은 일반적으로 리소스의 이름과 위치를 식별하는 URL의 경로 부분을 대체합니다. 예를 들어, 서비스에 대한 URL alias을 생성하면 alias가 호출 지시문과 통합 서버 의 서비스 이름 및 위치를 대체합니다 . 서비스에 대한 클라이언트 요청에는 invoke 지시문 및 서비스 정보 대신 alias가 포함됩니다. 통합 서버가 요청을 받으면 통합 서버는 alias와 연결된 서비스를 호출합니다.
### 8-16. Web Services
- 웹 서비스 Endpoint Aliases는 네트워크 주소 및 선택적으로 웹 서비스와 함께 사용할 보안 자격 증명을 나타냅니다. 네트워크 주소 속성을 사용하여 웹 서비스에 대한 동적 주소 지정을 활성화할 수 있습니다. 보안 자격 증명을 사용하여 웹 서비스에 대한 전송 수준 및 메시지 수준 보안을 모두 제어할 수 있습니다.
웹 서비스 설명자에서 Endpoint Aliases는 바인더와 연결됩니다. 통합 서버는 바인더를 사용하여 하나의 컨테이너 에 있는 특정 포트 유형에 대한 주소, 통신 프로토콜 및 데이터 형식에 대한 정의를 수집합니다. 하나의 컨테이너에서 특정 포트 유형에 대한 주소, 통신 프로토콜 및 데이터 형식에 대한 정의를 수집합니다. Endpoint Aliases를 바인더와 연결하는 방법에 대한 자세한 내용은 webMethods Service Development Help 를 참조하십시오 .

- Dynamic endpoint addressing : Endpoint의 실제 값은 런타임에 조회되기 때문에 Endpoint Aliases를 사용하면 웹 서비스를 사용할 때마다 서버 정보를 지정하거나 변경하지 않아도 됩니다.
- Security : 웹 서비스 공급자 및 소비자에 대해 WS-Security를 ​​구성하려면 Endpoint Aliases가 필요합니다. WS-Security 구현에 대한 정보는 Web Services Developer's Guide 에서 WS-Security에 대한 정보를 참조하십시오 .
- WS-Addressing 메시지 주소 지정 속성을 사용하여 요청이 아닌 다른 주소로 응답을 보내는 데 필요한 인증 자격 증명을 지정할 수 있습니다. 메시지 주소 지정 속성은 SOAP 메시지에 첨부할 수 있는 WS-Addressing 정보를 정의합니다. WS-Addressing에 대한 자세한 내용은 Web Services Developer's Guide 를 참조하십시오 .
- WS-ReliableMessaging 신뢰할 수 있는 메시징 속성은 두 Endpoint Aliases(웹 서비스와 클라이언트 또는 신뢰할 수 있는 메시징 원본과 대상) 간에 메시지를 안정적으로 전달하도록 합니다. 통합 서버 에 정의된 모든 웹 서비스 Endpoint에 대해 웹 서비스 Endpoint 또는 글로벌 수준에서 특정한 신뢰할 수 있는 메시징 속성을 구성할 수 있습니다 .
![192 168 110 205_5097 - webMethods Integration Server - Chrome 2023-08-10 오후 3_02_57](https://github.com/minya8703/webMethods/assets/97384342/c6f11f09-78ea-4553-8815-663335d63e95)


