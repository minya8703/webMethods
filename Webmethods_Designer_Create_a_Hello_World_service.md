
 What Is a Flow Service?
=============

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

  Flow Service에는 Flow Step이 포함됩니다.  Flow Step은 webMethods Integration Server가 실행하는 기본 작업 단위( webMethods flow language로 표현됨) 입니다.
- 필드 값을 기반으로 지정된 시퀸스를 조건부로 실행
- 성공할 때까지 지정된 시퀸스를 재시도
- 배열 필드의 각 요소에 대해 지정된 시퀸스(Loop)를 반복합니다.
- Flow Service, Flow Step 또는 반복을 종료합니다
- 설정된 Step을 시도하여 해당 단계에서 발생하는 오류를 찾아 처리하고 일련의 정리 단계를 실행
아래의 Flow Service에서는 서비스의 하위 집합을 통해 반복을 만들고 마지막 단계에서 두 서비스 중 하나로 분기하도록 제어 단계가 삽입되었습니다.

---
### Invocation Steps()
---
INVOKE - 지정된 서비스를 실행

---

### Data-Handling Steps
---
MAP - pipeline에서 지정된 편집 작업(예 : pipeline의 변수 매핑. pipeline에 변수 추가, pipeline에서 변수 삭제)을 수행 MAP 단계는 서비스 호출인 변환기를 포함할 수도 있다.

---
###  Control Steps
---
BRANCH - pipeline에 지정된 변수 값에 따라 지정된 Flow step를 실행

---
LOOP - 배열 형태의 데이터를 데이터의 갯수만큼 지정된  Flow step 반복하여 실행

---
REPEAT - successful 또는 non-successful 여부에 따라서 지정된 횟수까지 지정된 Flow step  set 을 반복하여 실행

---
SEQUENCE - Flow step을 그룹화 합니다. SEQUENCE 단계는 기본적으로 

---
BRANCH 단계의 하위를 제외한 Flow service의 모든 단계는 암시적 

---
-SEQUENCE 단계의 구성원인 것처럼 실행

---
EXIT - Flow step의 실행을 제어(예:  깊이 중첩된 일련의 단계 내에서 전제 흐름서비스 중단. Java 서비스 작성 없이 예외 발생 또는 예외 발생없이 LOOP 또는 REPEAT종료)

---
T RY - CATCH 또는 FINALLY 단계에서 실패 처리 나 또는 CATCH 또는 FINALLY 를 제공하려는 일련의 흐름 단계를 실행

---
CATCH - TRY step에서 실패한 처리를  Stepdㄹ 실행

---
FINALLY - Try 단계 또는 CATCH 단계가 실행된 후 일부 휴형절리를 수행하는 흐름 단계를 실행


---

###  파이프라인이란?
파이프 라인 흐름 서비스에 대해 입력 및 출력 값이 유지되는 데이터구조를 타나내는 데 사용되는 용어로 Flow service에서 데이터를 공유 할 수 있다.

Pipeline은 흐름 서비스에 대한 입력으로 시작하여 Flow의 다음 서비스에서 입력 및 출력을 수집합니다. Flow Service가 실행되면 해당 지점에서 파이프라인의 모든 데이터에 액세스 할 수 있습니다.

## Flow Service 만들기
	
**Flow Service를 생성하려면**
	
1. File > New > Flow Service를 선택
2. New Flow Service를 저장할 폴더를 선택
3. Choose template에서 사용할 template이 있을 경우 목록에서 선택후 다음을 클릭
4. Source Type 에서 Empty Flow 선택 후 Finish
5. 파일명에 Interface ID 입력하고 

webMethods Flow Steps <https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/index.html#page/b2b-integration-compendium%2Fesb.flowSteps.html%23>

### The INVOKE Step
* 사용
    * 다른 Flow Service 및 웹 서비스 커넥터를 포함하여 모든 유형의 서비스를 호출
	*  로컬 및 다른 webMethods Integration Server의 서비스를 호출
	* Flow Service를 재귀적으로 호출. Flow Service를 재귀적으로 사용하는 경우 재귀를 종료할 수단이 필요
	*  서비스를 호출하여 해당 입력 및 출력의 유효성을 검사합니다.
* 서비스 속성 지정 - property의 (...) 버튼으로 서비스 를 변경 하거나 정규화된 이름으로 서비스를 지정(예 : purchase.orders:getOrders)
* 내장 서비스 호출 - webMethods에서 제공하는 기본 서비스 및 라이브러리 연산 수행
* 다른 통합 서버에서 서비스 호출 - 기본 제공 서비스인 pub.remote:invoke를 사용하여 원격 통합 서버에서 서비스를 호출하고 결과를 반환할 수 있습니다.
-----
### INVOKE Step Properties 설정
  ```
 * Service *
 - 호출될 서비스의 이름을 설정

 *  Timeout  * 
 - 선택항목
 - 이 Step을 실행해야하는 최대시간(초)를 지정
 - Step이 완료되기 전에 이 시간이 경과 할 경우 FlowTimeoutException을 발행하고 서비스의 다음 단계에서 실행을 계속 진행
 - 이 속성에 대하여 pipeline 변수 값을 사용하려면 % 기호사이에 변수이름을 지정(%expiration%)
 - 제한 시간이 필요 없을 경우 비워 둡니다.
 - 시간초과 처리는 watt.server.threadKill.timeout.enabled 구성 매개변수에 대한 설명을 참조

 *  Validate input *
 - 서버가 서비스 입력 서명에 대해 서비스에 대한 입력의 유효성을 검사할지의 여부 
 - 입력 확인일 경우 TRUE 입력을 확인 하지 않으려면 FALSE

 *  Validate output *
 - 서버가 서비스 출력 서명에 대해 서비스 출력의 유효성을 검사할지 여부
 - 입력 확인일 경우 TRUE 입력을 확인 하지 않으려면 FALSE
  ```
-----

### The BRANCH Step
* 사용
    *  실행시 변수 값을 기반으로 단계를 조건부로 실행할 수 있습니다.
    *  예) BRANCH 단계를 사용하여 PaymentType 값이 "CREDIT CARD" 인 경우 한 가지 방식으로, "CORP ACCT"인 경우 다른 방식으로 구매 주문을 처리 가능
-----
* 스위치 값에서 분기 - 변수를 사용하여 실행할 하위 단계를 결정. 실행시 BRANCH단계는 스위치 변수의 값을 각 대상의 Label속성과 일치시켜 레이블이 스위치 값과 일치하는 하위 단계를 실행

 ```
  스위치 값에서 분기 방법
  1. 조건부 단계(대상 단계)목록을 생성하고 BRANCH 단계의 하위 항목으로 만듭니다.
  2. BRANCH 단계의 특성 보기에서 값이 스위치 역활을 할 파이프라인 변수의 이름을 스위치 특성에 지정(예 : BuyerInfo/AccountNum)
  3. 각 대상 단계의 레이블 속성에서 해당 단게를 실행할 값을 지정합니다. 
 ```
 -----
* 식에서 분기 - 식을 사용하여 하위 단계를 결정. 런타임시 BRANCH 단계는 각 하위 단계의 Label 특성에 있는 표현식을 평가하여 표현식이"TRUE"로 평가되는 첫 번째 하위 단계를 실행
 ```
  식에서 분기 방법
  1. 조건부 단계(대상 단계) 목록을 생성하고 BRANCH 단계의 하위 항목으로 만듭니다.
  2. BRANCH 단계의 특성 보기에서 레이블 평가를 TRUE로 설정
  3. 각 대상의 레이블 속성에서 TRUE인 경우 대상 단계가 실행되게 하는 식을 지정. 생성하는 표현식은 여러 변수를 포함할 수 있으며 변수 값의 범위를 지정할 수 있습니다. 
 ※ BRANCH 단계의 하위 하나만 실행된다는 점에 유의. 레이블에 TRUE로 평가되는 표현식이 포함된 첫 번째 대상 단계며 어떤 식도 TRUE로 평가되지 않으면 하위 단계가 호출되지 않고 서비스의 다음 단계로 넘어 가게 된다. **Label 속성의 $default** 값을 사용하여 true로 평가되는 식이 없는 경우에 대한 기본 단계를 지정할 수 있스니다.
```

[조건식을 참조](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/index.html#page/b2b-integration-compendium%2Fto-conditional_expressions.html%23wwID0ENCA1B, "조건식")

-----
*  Null 및 빈 값에서 분기 - BRANCH 단계 는 변수가 파이프라인에 없거나 명시적으로 null로 설정된 경우 스위치 값을 null 로 간주합니다. BRANCH 단계 는 변수가 파이프라인에 존재하지만 해당 값이 길이가 0인 문자열인 경우 스위치 값을 빈 문자열로 간주합니다 . null 또는 빈 값에서 분기하려면 대상 단계의 레이블 속성을 다음과 같이 설정합니다.
 ```
  Null 및 빈 값에서 분기 방법
 * A null value * 
 - property의 Label 속성을 $null로 설정 실행시 BRANCH 단계는 스위치 변수가 명시적으로 null로 설정되거나 파이프라인에 존재하지 않은 경우 $null Label이 있는 대상 단계를 실행
 * An empty string * 
 -  property의 Label 속성을 비워 두고 실행시 BRANCH 단계는 스위치 변수가 있지만 문자가 없는 경우 Label 없이 대상 단계를 실행
  ```
-----
*  기본 단계 지정 - 실행시 일치하지 않는 값이 발생할 때 서비스가 BRANCH단계를 거치지 않도록 하려면, 일치하지 않는 사례를 처리하기 위한 기본 대상 단계를 포함시킵니다. BRANCH property의 Label을 $default로 설정
-----
*  SEQUENCE를 BRANCH의 대상으로 사용 - 단일 단계가 아닌 일련의 여러  단계를 조건부로 실행하기 위해 BRANCH Step을 원하는 경우 SEQUENCE Step을 대상 단계로 사용하여 그룹화 할수 있습니다.
-----
* BRANCH Step 구축
 ```
  BRANCH Step 빌드 방법
  1. BRANCH 단계를 기존 흐름 서비스에 추가하는 경우 해당 서비스를 편집기에 표시하고 BRANCH Step을 추가할 바로 위의 단계를 강조 표시
  2. 다음의 하나를 수행
     - 
  3. 아래의 BRANCH Step의 Properties를 설정
  4. 다음 단계를 사용하여 BRANCH(해당 하위)에 속하는 조건부 단계
    4-1. Flow Step Palette에서추가하려는 
    4-2.
    4-3.
  5. file > save 를 클릭
```

### BRANCH Step Properties 설정
 ```
 Comments 
 - 이 Step에 대한 설명
 Scope
 - 이 Step을 제한하려는 파이프라인의 문서(IData 객체)이름
 - 전체 파이프라인에 액세스하려면 이 속성을 공백으로 설정
 Timeout
 - 이 Step를 실행해야하는 최대 시간(초) 이Step가 완료되기 전에 경과하면 통합 서버는 FlowTimeoutException을 발행하고 서비스의 다음 Step에서 실행을 계속합니다.
 - 이 속성에 대하여 pipeline 변수 값을 사용하려면 % 기호사이에 변수이름을 지정(%expiration%)
 - 제한 시간이 필요 없을 경우 비워 둡니다.
 - 시간초과 처리는 watt.server.threadKill.timeout.enabled 구성 매개변수에 대한 설명을 참조
 Label
 - 이 Step에 대한 선택적 이름 또는 null 
 - 이 Step을 다른 BRANCH 또는 EXIT Step의 대상으로 사용하는 경우 Label 특성에 값을 지정
 Switch
 - 이 Step을 제한하려는 파이프라인의 문서(IData 객체)이름
 Evaluate label
 - 하위 Step의 Label을 조건식으로 평가할지에 대한 여부
 - 식에서 분기를 하려면 True, 스위치 값에서 분기하려면 False(기본값)을 선택
 ```
-----

### The REPEAT Step
### The SEQUENCE Step
### The LOOP Step
### The EXIT Step
### The MAP Step
### The TRY, CATCH, and FINALLY Steps



https://techdocs.broadcom.com/kr/ko/ca-enterprise-software/it-operations-management/application-performance-management/10-5/345392263/345392665/345392690.html
