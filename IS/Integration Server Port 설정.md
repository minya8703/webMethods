
[영문판 Document](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/index.html#page/b2b-integration-compendium%2Fto-configure_ports_6.html%23wwconnect_header) <br>
[일어판 Document](https://documentation.softwareag.com/webmethods/wmsuites/wmsuite10-4_j/Integration_Server/10-4_Integration_Server_Administrators_Guide_J.pdf)
<br> 9. Port의 설정 참고
# Port에 대해
- Integration Server는 지정 Port에서 요청을 수신 대기 하며 각 Port는 HTTP, HTTPS, FTP,FTPS,WebSocket,전자메일,파일폴링 등 특정 프로토콜 타입과 관련이 있습니다.
## 사용가능한 Port타입
|Port타입|목적|
|---|---|
|HTTP|보안되지 않은 요청을 서버에 제출합니다.|
|HTTPS|SSL 암호화를 사용하여 서버에 요청을 제출합니다.|
|FTP|서버 간에 파일을 이동|
|FTPS|SSL 암호화를 사용하여 서버 간에 파일을 이동|
|이메일|POP3 또는 IMAP과 같은 전자 메일 서버를 통해 요청을 받습니다.|
|FilePolling|새 파일이 도착하는지 파일 시스템을 모니터링하고 도착 시 특수 처리를 수행합니다.|
|진단Port|서버가 응답하지 않는 경우 통합 서버 관리자 에 액세스합니다 .|
|정지Port|서버 유지 관리를 위해 정지 모드를 시작하고 종료합니다.|
|Enterprise Gateway Server|webMethods Enterprise Gateway 구성 에서 외부 클라이언트의 요청을 수신하고 내부 서버에 대한 연결을 유지합니다|
|내부 서버|webMethods Enterprise Gateway 구성 에서 내부 서버를 엔터프라이즈 게이트웨이 서버 에 연결합니다 .|
|webMethods/WebSocket|WebSocket 프로토콜을 사용하여 서비스 요청을 제출합니다.|

## 기본 제공 Port
|Alias|Protocol|Port Type|Port Number|
|---|---|---|---|
|DefaultPrimary |HTTP|Primary|5555|
|DefaultDiagnostic|HTTP|Diagnostic|9999|

- 통합 서버 의 기본 Port에 할당된 별칭은 변경할 수 없으며, 기본 Port에서 사용되는 Port, 프로토콜, Port 유형에 대해 다른 별칭을 사용하려면 해당 Port를 삭제하고 새 별칭으로 다시 만들어야 한다.
- DefaultPrimary Port에 다른 별칭을 사용하려면 DefaultPrimary Port를 삭제하고 새 별칭으로 다시 생성하기 전에 다른 Port를 기본 Port로 지정해야 합니다.

## Port의 추가에 관한 고려사항
- 하나 이상의 추가 Port를 구성할 수 있습니다. HTTP, HTTPS, FTP, FTPS, 이메일 또는 파일 폴링 프로토콜을 추가 Port와 연결할 수 있습니다.
```
중요사항:
동일한 호스트 시스템에서 여러 통합 서버 인스턴스를 실행하는 경우 각 서버의 Port에는 고유한 Port 번호가 있어야 합니다.
```
### Port를 추가하는 이유
- 특정 Port 번호가 필요한 애플리케이션이 있는 경우.
- 여러 유형의 수신 프로토콜을 지원하려는 경우.
- 동일한 프로토콜에 대해 여러 Port를 열려고 하는 경우.
- webMethods Enterprise Gateway가 DMZ에 위치하여 요청을 내부 방화벽 뒤에 있는 서버로 전달하기 전에 가로채는 webMethods Enterprise Gateway 구성 으로 서버를 배포하려는 경우 . webMethods Enterprise Gateway Port 추가에 대한 지침은[webMethods Enterprise Gateway 구성을](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/index.html#page/b2b-integration-compendium/to-enterprise_gateway.html#wwID0EYFAIB) 참조하십시오 .

## HTTP Port의 추가
 1. Integration Server Administrator를 접속
  2.  메뉴에서 [Security] 를 열어、[Ports] 를 클릭
  3.  [Add Port] 를 클릭한다.
  4.  [Add Port]메뉴에서 [webMethods/HTTP]선택
  5.  [Submit]을 선택하면 Port정보를 입력하는 페이지에서 이하의 정보를 입력
 
![webMethods Integration Server - Chrome 2023-08-25 오후 1_24_53](https://github.com/minya8703/webMethods/assets/97384342/7bda7805-2c81-4441-be11-4024b95fe18d)

|For this parameter...|Specify...|
|---|---|
|Enable|HTTP 리스너를 활성화할지 안할지를 지정|
|Port|사용할 Port번호를 지정 사용하지 않는 번호로 선택한다.|
|Alias|Integration Server에 대해 고유한 Port의 명칭을 지정|
|Description|Port에 대한설명|
|Package Name|이 Port와 연결된 패키지로서 패키지를 유효로 하면, Port도 유효가 되며 패키지를 무효로 하면 이 Port는 무효가 된다.<br> 이 패키지를 복제하면 Integration Server가 같은 번호, 같은 설정의 포트가 타켓서버에 작성됩니다. 같은 번호의 포트가 존재할 경우 포트의 설정은 해당 설정은 그대로 유지<br> 이 기능은 특정 포트에서 입력필요한 어플리케이션을 작성하는 경우 편리합니다. 애플리케이션은 다른 서버에 복제된 후에도 계속 작동|
|Bind Address (optional)|이 포트의 바인딩할 IP주소입니다. Bind Address는 사용할 컴퓨터에 복수의 IP주소가 설정되어있고, 포트에서 지정한 주소로 사용할 경우 사용합니다. Bind Address를 지정하지 않을 경우 자동으로 지정됩니다.|
|Backlog|Integration Server에서 요청거부가 되기전에 유효한 포트의 큐(대기열)에 남아 있은 요청의 수 입니다. 기본값은 200입니다. 최대값은 65535입니다.|
|Keep Alive Timeout|서버가 이 제한 기간 값(밀리초)내에 클라이언트로부터 요청을 받지 못한 경우 연결을 닫을 시기입니다.|
|Threadpool|리스터가 요청 발송에만 이 풀을 사용할지 여부입니다. 기존 통합 서버 스레드 풀은 전역 스레드 풀입니다. 이 리소스에 로드가 매우 높은 경우 전역 스레드 풀이 요청을 처리할 때까지 기다려야 할 수 있으나 개인 스레드 풀 옵션이 활성화 되면 이 포트로 들어오는 요청은 스레드에 대해 다른 서버 기능과 경쟁할 필요가 없게 됩니다. 이 포트로 들어오는 요청에 대해 개인 스레드 풀을 설정하려면 활성화를 클릭합니다. <br> ・Threadpool 최소값 : 개인용 스레드 풀에 대한 최소 스레드 수를 나타냅니다. 기본 값은 1입니다. <br> ・Threadpool 최대값 : 이 개인 스레드 풀의 최대 스레드 수를 나탭니다. 기본값은 5입니다.<br>・Threadpool 우선순위 : Java 스레드 우선순위를 나타냅니다. 기본값은 5입니다.<br> ``` 중요: 이 설정은 서버 성능과 처리량에 영향을 미치므로 각별히 주의하여 사용하십시오. 스레드풀 기능을 사용할 필요가 없으면 비활성화 를 클릭합니다. 포트의 세부 정보를 볼 때 서버는 현재 포트에 사용 중인 개인 스레드 풀 스레드의 총 수를 보고합니다. ``` Threadpool 기능을 사용하지 않는 경우, [enable]을 클릭|


  6.  [Security Configuration] 이하의 정보를 입력

|For this parameter...|Specify...|
|---|---|
|Client Authentication|통합 서버가 이 HTTP 포트에 도착하는 요청에 대해 수행할 클라이언트 인증 유형 아래의 다음중 하나를 선택|

  |Option|Description|
  |---|---|
  |Username/Password|서버는 클라이언트에게 사용자 ID와 비밀번호를 묻는 메시지를 표시|
  |Digest|서버는 비밀번호 다이제스트를 사용하여 모든 요청을 인증|
  |Request Kerberos Ticket|HTTP 리스너를 활성화할지 안할지를 지정|
  |Require Kerberos Ticket|HTTP 리스너를 활성화할지 안할지를 지정|
  
|For this parameter...|Specify...|
|---|---|
|Kerberos Properties (Optional)|통합 서버가 이 HTTP 포트에 도착하는 요청에 대해 수행할 클라이언트 인증 유형|

  |Option|Description|
  |---|---|
  |Kerberos Properties (Optional)|HTTP 리스너를 활성화할지 안할지를 지정|
  |Digest|HTTP 리스너를 활성화할지 안할지를 지정|
  |Request Kerberos Ticket|HTTP 리스너를 활성화할지 안할지를 지정|
  |Require Kerberos Ticket|HTTP 리스너를 활성화할지 안할지를 지정|
# 표안의내용 수정필요

  7.  [Save Changes] 클릭
  8.  필요한 경우 포트 화면 에서 편집을 클릭하여 액세스 모드를 변경합니다. 액세스 모드를 기본적으로 허용으로 설정하거나 기본 액세스 설정으로 재설정 할 수 있습니다 .
  9.  포트 화면 에서 포트 목록을 확인하여 활성화 열의 상태가 예 인지 확인하세요 . 그렇지 않은 경우 아니요를 클릭하여 포트 를 활성화합니다.



# HTTPS Port의 추가
- HTTPS 포트를 사용하면 통합 서버가 클아이언트와 서버를 안전하게 인증하고 교환된 데이터를 암호화할 수 있습니다. 기본적으로 HTTPS 리스너는 기본 통합 서버 SSL 키 에 대한 인증서를 사용합니다 .
- 통합 서버 키 저장소(파일 또는 SmartCard/HSM 기반) 에 있는 자체 개인 키를 사용하도록 리스너를 구성할 수 있습니다 .
- 서버에서 수행할 클라이언트 인증 유형을 구성할 수 있습니다. 클라이언트 인증을 사용하면 클라이언트의 신원을 확인할 수 있습니다

# 파일 폴링 포트 정보
- 파일 폴링 포트는 파일 도착을 위해 모니터링 디렉터리를 주기적으로 폴링합니다. 그런 다음 통합 서버는 파일에 대해 특수 파일 처리 서비스를 실행합니다. 파일 폴링 포트 및 처리는 다음과 같은 방식으로 작동합니다.

  1. 통합 서버 의 파일 폴링 포트는 파일 도착을 위해 모니터링 디렉터리를 주기적으로 폴링합니다. 각 파일 폴링 포트는 하나의 모니터링 디렉터리만 폴링합니다.
  2. 새 파일을 발견하면 Integration Server는 해당 파일을 작업 디렉터리에 복사합니다.
  3. 통합 서버는 포트에 지정된 파일 처리 서비스를 실행합니다. 서비스는 파일을 구문 분석, 변환 및 검증한 다음 파일 시스템에 쓸 수 있습니다. 사용자가 작성하는 이 서비스는 이 포트를 통해 호출할 수 있는 유일한 서비스입니다.
  4. 서비스가 파일을 성공적으로 처리하는지 여부에 따라 다음 중 하나가 발생합니다.
     - 파일 처리가 성공적으로 완료되면 통합 서버는 파일을 완료 디렉터리로 이동합니다.
     - 파일 처리가 오류로 종료되면 통합 서버는 파일을 오류 디렉터리로 이동합니다.
  5. 통합 서버는 정기적으로 완료 및 오류 디렉터리를 정리합니다. 완료 또는 오류 디렉터리에서 파일을 제거하기 전에 파일이 얼마나 오래되어야 하는지와 통합 서버가 완료 및 오류 디렉터리를 정리하는 빈도를 구성할 수 있습니다.
 
- Integration Server 클러스터 또는 클러스터되지 않은 Integration Server 그룹에서 파일 폴링은 개별 Integration Server 에서와 거의 동일한 방식으로 작동합니다 . 유일한 차이점은 둘 이상의 통합 서버가 모니터링 디렉터리를 폴링한다는 것입니다. 그룹의 통합 서버가 모니터링 디렉터리에서 파일을 검색하면 해당 파일은 그룹의 다른 통합 서버 에서 사용할 수 없습니다.
파일 폴링을 구성하려면 다음을 수행해야 합니다.
    - 통합 서버 에 모니터링 디렉터리를 설정합니다 . 파일 폴링에 사용되는 다른 디렉토리는 Integration Server 에 의해 자동으로 생성됩니다
    - 파일 처리 서비스를 작성하고 통합 서버 에서 사용할 수 있도록 합니다 . 이러한 서비스의 예는 webMethods 서비스 개발 도움말 및 플랫 파일 스키마 개발자 가이드를 참조하세요.
    - 통합 서버 에 파일 폴링 포트를 설정합니다 .

 ## 파일 폴링 포트 추가
 1. Integration Server Administrator를 접속
  2.  메뉴에서 [Security] 를 열어、[Ports] 를 클릭
  3.  [Add Port] 를 클릭한다.
  4.  [Add Port]메뉴에서 [webMethods /FilePolling.]선택
  5.  [Submit]을 선택하면 Port정보를 입력하는 페이지에서 이하의 정보를 입력

|For this parameter...|Specify...|
|---|---|
|Package Name|지정하는 포트와 연결된 패키지|
|Alias|Integration Server에 대해 고유한 Port의 명칭을 지정|
|Description|Port에 대한설명|
|Package Name|이 Port와 연결된 패키지로서 패키지를 유효로 하면, Port도 유효가 되며 패키지를 무효로 하면 이 Port는 무효가 된다.<br> 이 패키지를 복제하면 Integration Server가 같은 번호, 같은 설정의 포트가 타켓서버에 작성됩니다. 같은 번호의 포트가 존재할 경우 포트의 설정은 해당 설정은 그대로 유지<br> 이 기능은 특정 포트에서 입력필요한 어플리케이션을 작성하는 경우 편리합니다. 애플리케이션은 다른 서버에 복제된 후에도 계속 작동|
|Bind Address (optional)|이 포트의 바인딩할 IP주소입니다. Bind Address는 사용할 컴퓨터에 복수의 IP주소가 설정되어있고, 포트에서 지정한 주소로 사용할 경우 사용합니다. Bind Address를 지정하지 않을 경우 자동으로 지정됩니다.|
|Backlog|Integration Server에서 요청거부가 되기전에 유효한 포트의 큐(대기열)에 남아 있은 요청의 수 입니다. 기본값은 200입니다. 최대값은 65535입니다.|
|Keep Alive Timeout|서버가 이 제한 기간 값(밀리초)내에 클라이언트로부터 요청을 받지 못한 경우 연결을 닫을 시기입니다.|
|Threadpool|리스터가 요청 발송에만 이 풀을 사용할지 여부입니다. 기존 통합 서버 스레드 풀은 전역 스레드 풀입니다. 이 리소스에 로드가 매우 높은 경우 전역 스레드 풀이 요청을 처리할 때까지 기다려야 할 수 있으나 개인 스레드 풀 옵션이 활성화 되면 이 포트로 들어오는 요청은 스레드에 대해 다른 서버 기능과 경쟁할 필요가 없게 됩니다. 이 포트로 들어오는 요청에 대해 개인 스레드 풀을 설정하려면 활성화를 클릭합니다. <br> ・Threadpool 최소값 : 개인용 스레드 풀에 대한 최소 스레드 수를 나타냅니다. 기본 값은 1입니다. <br> ・Threadpool 최대값 : 이 개인 스레드 풀의 최대 스레드 수를 나탭니다. 기본값은 5입니다.<br>・Threadpool 우선순위 : Java 스레드 우선순위를 나타냅니다. 기본값은 5입니다.<br> ``` 중요: 이 설정은 서버 성능과 처리량에 영향을 미치므로 각별히 주의하여 사용하십시오. 스레드풀 기능을 사용할 필요가 없으면 비활성화 를 클릭합니다. 포트의 세부 정보를 볼 때 서버는 현재 포트에 사용 중인 개인 스레드 풀 스레드의 총 수를 보고합니다. ``` Threadpool 기능을 사용하지 않는 경우, [enable]을 클릭|
 
webmethods git연동
https://tech.forums.softwareag.com/t/webmethods-9-8-designer-local-service-development-with-git/191393/9
