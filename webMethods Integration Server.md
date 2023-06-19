# webMethods Intergration Server의 관리
https://techdocs.broadcom.com/jp/ja/ca-enterprise-software/it-operations-management/application-performance-management/10-5/345384579/345384976/345385001.html
## webMethods Integration Server에 관해서
* webMethods Integration Server 는 기업의 새로운 비지니스와 기존의 비지니스 서비스를 관리 및 통합을 할 수 있습니다.
이 제품은 새로운 서비스의 설계, 테스트 및 배포를 진행하고 작은 결합 서비스와 레거시 시스템을 자동화하고, 자동화, 조정 및 조합하여 비즈니스 프로세스를 개선하기 위한 도구가 포함되어 있습니다.

* webMethods Integration Server는 서비스의 실행 및 배포하기 위해 하나로 통합한 플랫폼을 제공합니다.  클라이언트의 요구를 받아 들여 해석하여 요구한 서비스를 식별하여 불러와 데이터을 예정된 형식으로 실행 되고 있는 서비스에 전달하여 서비스에 따라 생성된 출력을 받아, 그 출력을 클라이언트에게 전달한다.

통합 플랫폼으로서 WebMethods는 주로 어플리케이션 서버, 데이터 베이스 및 커스텀 어플리케이션간의 오퍼레이션을 조설 하기 위해 사용되고 있다.WebMethods에 따라 기업 또는 거래 상대와 전자 문서를 교환할 수 있게 된다.
webMethods Integration Server의 오퍼레이션을 감시 하는 것에 대한 것은 이하의 최상위 구성 요소의 메트릭을 사용합니다.

### Adapter
* Adapter를 사용하면 서비스 인터페이스의 공통 어댑터 프레임워크에 따라 외부 애플리케이션과 webMethods를 통합할 수 있습니다.어댑터는 다음 요소로 구성됩니다.
  * Integration Server가 실행시 외부리소스 또는 시스템에 접속 될수 있게하는 Adapter 접속
  * Integration Server 에서 실행되어 외부 리소스에 대한 운영을 시작하는 어댑터 서비스 외부 리소스를 감시하고, 이벤트가 Integration Server에 따라 개시되지 않은 것을 Integration Server에 통지하는 어댑터 통지 서비스가 발생합니다.
  * SOA extension for webMethods 는, [Adapter Conection Pool], {Adapter Services],  및 [Adapter Notifications] 노드의 매트릭스를 사용하여 webMethods Integration Server를 위해 전개한 모든 어댑터의 성능과 가동 상황을 감시 할 수 있다.
###  비지니스 프로세스는 특정 목적을 달성하기 위해서
  * 비즈니스 프로세스는, 특정의 비지니스 방식을 사용하여, 특정의 순서 대로 실행 됩니다. 일련의 상호 관련 비즈니스 태스크입니다. 대부분의 비즈니스 프로세스에서 역활과 다른 여러 시스템 또는 여러 유저 간의 상호 작용이 필요합니다. 예를 들어 신입사원의  입사 준비, 발주서 처리, 청구서 송부등에 대응 하는 비즈니스 프로 세스가 있다고 하면 이 경우 각 비즈니스프로세스에서 신입사원에 대하여 회사의 작업 공간 지정, 인사(HR) 시스템의 사원 추가, 사무기기와 비품을 발주 비즈니스 태스크등이 포함됩니다.
  * SOA extension for webMethods에서 [WebMethods] - [Business Processes]노드의 매트릭스를 사용하여 정의하는 비즈니스 프로세스의 성능과 전반적인 가동 상황을 모니터링을 할 수 있다.
### Flow Service
* Flow Service 는 webMethods의 Flow언어로 되어 있으며 webMethods Integration Server 상에 전개되는 서비스 입니다. Flow Service는 다른 Flow Service, 유저 정의 서비스, 조합된 서비스, 다른 프로바이더(webMethods 어댑터와 .NET플러그인등) 서비스를 포함하여, webMethods 서버에서 실행되고 있는 어떤 서비스도 호출할 수도 있다.
* SOA extension for webMethods는 모든 Flow Service의 작업과 전반적인 가동상황을 감시하며, 감시대상이 되지 않는 Flow Service를 홀드하여 제외하는 것도 가능합니다. Flow Service에 포함되는 개개의 Flow 순서에 관한 메트릭은, [WebMethods]- [Flow Services]노드의 아래에 표시됩니다.
### Java Service
* Java Service는 Java로 기술되며(또는, 다른 언어로 기재되어 서비스가 Java클래스를 사용), webMethods Integration Server 상의 서비스로 공개된 매커니즘의 서비스 및 사용자 정의 서비스 입니다.
* SOA extension for webMethods는 모든 Java Service의 성능과 전반적인 가동 상황을 감시하거나 감시 대상으로 하지않는 Java서비스를 필터하여 제외할 수 있습니다. 각 Java클래스에 포함되는 Java메서드에 관한 메트릭은, ［WebMethods］-［Java services］노드의 아래에 표시됩니다.
### JDBC Connection Pools
* webMethods Integration Server는, 네트워크의 경우 통지와 정보전송을 위해 Java 데이터베이스 접속을 사용합니다.
* SOA extension for webMethods은, ［WebMethods］-［JDBC Connection Pools］노드의 메트릭을 사용하여 JDBC접속의 가용성을 감시
###  Thread Pool
* webMethods Intergration Server은, 서비스의 실행, webMethods Broker로 부터의 취득, 및 트리거의 실행 스레드를 사용
* SOA extension for webMethods 는 ［WebMethods］-［Thread Pools］노드의 메트릭을 사용하여 스레드의 가용성을 감시할수 있습니다.
### Trading Networks
* 각조직은 Trading Networks를 사용하여 도큐멘트의 교환함으로써 기업간의 관계를 확립하고 충실하게 할 수 있습니다.
* SOA extension for webMethods은, ［WebMethods］-［Trading Networks］노드의 메트릭스를 사용하여 도큐멘트의 인식을 감시할수 있습니다.
### Triggers
* Triggers는 발생가능한 도큐멘트 유형에 대한 subscription을 확립하고 그러한 문서 인스턴스의 처리 방법을 지정합니다.
* Broker(로컬)트리거는 Integration Server 상의 로컬에서 발생한 도큐먼트, 또는 Broker에 전송된 도큐멘트를 구독하여 처리하는 트리거입니다. Broker트리거는 종종 비동기 어댑터 알림과 관련이 있습니다.
* JMS 트리거는 JMS프로바이더상의 수신처(큐 또는 토픽)로 부터 메시지를 받아 그것을 메시지 처리하는 트리거 입니다.
* SOA extension for webMethods은, ［WebMethods］-［Triggers］노드의 메트릭스를 사용하여 트리거를 감시 할 수 있습니다.

### WebServices
* WebServices메트릭스는,  클라이언트 서버의 비지니스 서비스의 엔드 포인트, 또는 각 서비스내의 관련하는 오퍼레이션 을 표시합니다.
* SOA extension for webMethods은, ［WebMethods］-［WebServices］노드를 사용하며 클라이언트와 유저의 Web서비스 엔드포인트의 성능과 전반적인 가동 상황을 감시 할 수있습니다.
### XSLTServices
* webMethods의 내부에서는 XSLT스타일 시트를 사용하여 XML데이터를 다른 평식으로 변경하고, 그 변경 결과를 다른 서비스에 포함 할 수 있습니다.
* SOA extension for webMethods은, ［WebMethods］-［XSLT Services］노드를 사용하여 XSLT교환의 퍼포먼스와 전반적인 가동 상황을 감시할 수 있습니다.
