# What Is a Flow Service?

## 참고자료
<https://tech.forums.softwareag.com/t/get-started-with-webmethods-service-designer-text-instructions-for-the-video/237274>

<https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/index.html#page/b2b-integration-compendium%2Fesb.flow.whatIs.html%23>


## Flow Service 란?

webMethods 의 flow language로 작성된 서비스로 이 서비스 를 사용하여 단일 서비스 내에서 일련 서비스를 캡슐화하고 이들 간의 데이터의 흐름을 관리 하는 서비스입니다.
예를 들어 구매자로 부터 구매 주문을 받아 내부 주문 시스템에 제출하기 전에 다음과 같은 flow 서비스를 생성이 가능합니다.
1. 구매자가 제출한 구매 주문서를 가져옵니다.
2. 감사 추적 파일에 주문을 기록합니다.
3. 신용조회를 합니다.
4. 주문 시스템에 주문 게시 

위의 그림과 같이 흐름 내에서 모든 서비스를 호출할 수 있습니다.


## Flow Step?

  Flow Service에는 Flow Step이 포함됩니다.  Flow Step은 webMethods Integration Server가 런타임에 해석하고 실행하는 기본 작업 단위( webMethods flow language로 표현됨) 입니다.
- 필드 값을 기반으로 지정된 시퀸스를 조건부로 실행
- 성공할 때까지 지정된 시퀸스를 재시도
- 배열 필드의 각 요소에 대해 지정된 시퀸스(Loop)를 반복합니다.
- Flow Service, Flow Step 또는 반복을 종료합니다
- 설정된 Step을 시도하여 해당 단계에서 발생하는 오류를 찾아 처리하고 일련의 정리 단계를 실행
아래의 Flow Service에서는 서비스의 하위 집합을 통해 반복을 만들고 마지막 단계에서 두 서비스 중 하나로 분기하도록 제어 단계가 삽입되었습니다.


## following types of flow steps
**Invocation Steps()**
---
- INVOKE - 지정된 서비스를 실행
----
Data-Handling Steps
---
MAP - pipeline에서 지정된 편집 작업(예 : pipeline의 변수 매핑. pipeline에 변수 추가, pipeline에서 변수 삭제)을 수행 MAP 단계는 서비스 호출인 변환기를 포함할 수도 있다.
Control Steps
---
BRANCH - pipeline에 지정된 변수 값에 따라 지정된 Flow step를 실행

LOOP - 배열 형태의 데이터를 데이터의 갯수만큼 지정된  Flow step 반복하여 실행

REPEAT - 지정된 Flow step에서 successful 또는 non-successful 여부에 따라서

SEQUENCE - 

EXIT - 

T RY - 

CATCH - 

FINALLY - 




- Hello World  Flow Service 만들기
	1. File > New > Flow Service를 선택
	2. 파일명에 Interface ID 입력하고 





https://techdocs.broadcom.com/kr/ko/ca-enterprise-software/it-operations-management/application-performance-management/10-5/345392263/345392665/345392690.html
