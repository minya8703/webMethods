
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
     - Flow Service 편집기 도구 모음에서 ?? 옆에 있는 버튼을 클릭하고 ??을 클릭합니다.
     - Flow Service 편집기 옆을 클릭하여 ?? 팔레트 보기를 엽니다. 큭릭 ?? 하여 흐림 서비스 편집기로 드래그 합니다.
  3. 아래의 BRANCH Step의 Properties를 설정
  4. 다음 단계를 사용하여 BRANCH(해당 하위)에 속하는 조건부 단계를 추가 합니다.
    4-1. Flow Step Palette에서추가하려는 flow step을 선택하여 추가
    4-2. Flow Service 에디터에서 하위 BRANCH step을 만듭니다.
    4-3.Label Proerties에서 이 step의 런타임 스위치의 값을 지정합니다.
    4-4. 필요에 따라 다른 속성을 설정
  5. file > save 를 클릭
```

Properties의 Switch 값 지정 방법
|To match|Specify...|
|------|---|
|That exact string|A string|
|The String representation of the object’s value|A constrained object value|
|Any string fitting the criteria specified by the regular expression Example  /^REL/|A regular expressio|
|An empty string|A blank field|
|A null value|$null|
|Any unmatched value (that is, execute the step if the value does not match any other label)|$default|



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
이 단계를 사용하면 해당 당계의 성공 또는 실패에 따라 일련의 하위 단계를 조건부로 반복이 가능 

- 세트 내의 단계가 실패하며 단계 세트를 다시 실행 (재시도 합니다.) 이 옵션은 외부 시시템(예: 데이터 데이스, ERP 시스템, 서버 또는 웹 서비스) 또는 장치에 액세스 할 때 발생할 수 있는 일시적인 오류를 수용하는 데 유용합니다.
- 세트 내의 단계중 하나가 실패할 때까지 일련의 단계를 다시 실항하십시오. 이 옾션은 특정 상황이 집합이 존재하는 한 프로세스를 반복하는데 유용합니다(예 :  데이터 항복이 데이터 집합에 존재)
####  REPEAT 조건 지정
* REPEAT 단계를 빌드할 때 하위 항목이 런타임에 다시 실행되도록 하는 조건(성공 또는 실패)을 지정하기 위해 반복 속성을 설정합니다.

|If you set “Repeat on” to…|The REPEAT step…|
|------|---|
|FAILURE|세트의 단계가 실패하면 하위 단계 세트를 다시 실행합니다.|
|SUCCESS|세트의 모든 단계가 성공적으로 완료되면 하위 단계 세트를 다시 실행합니다.|
####  REPEAT Count 설정
* REPEAT 단계의 Count 특성은 서버가 REPEAT 단계에서 하위 단계를 재실행하는 최대 횟수를 지정합니다.

|If you set “Count” to…|The REPEAT step…|
|------|---|
|0|하위 단계는 실행하지 않습니다.|
|Any value > 0| value의 횟수 만큼 하위 단계를 실행합니다.|
|-1 or blank|지정된 Repeat on 조건이 TRUE인 동안 하위 단계를 실행합니다.|
※　REPERT의 항목은 항상 최소 1번은 실행 Count 속성은 자식이 다시 실행될 수 있는 최대 횟수를 지정하며 반복이 끝나면 서버는 반복에 대한 조건(즉, 실패 또는 성공)이 만족되었는지 확인합니다. 조건이 true이고 Count가 충족되지 않으면 자식이 다시 실행되며 이 프로세스는 반복 조건이 거짓이거나 카운트가 충족 될때 까지 계속 실행(즉, Count가 -> -1 일 때 REPEAT의 자식이 실행할 최대 횟수는 Count + 1 입니다.)

####  REPEAT 는 언제 실패가 되나
아래의 조건으로 REPEAT step이 실패 합니다.
|If “Repeat on” is set to…|The REPEAT step fails if…|
|------|---|
|SUCCESS| REPEAT의 하위 단위가 실패 |
|FAILURE| 하위 단위가 성공적으로 실행되기 전에 개수 제한에 도달 하는 경우|

####  REPEAT 를 사용하여 실패한 단계 재시도
외부 시스템에 액세스하는 서비스를 호출하는 경우 REPEAT 단계를 사용하여 런타임에 사용중인 서비스 또는 연결 오류와 같은 네트워크 오류를 수용할 수 있습니다. 이 목적으로 REPEAT 단계를 사용하는 경웅 다음 사항에 유의
* 다음 유형의 실패는 FAILURE 조건을 충죽
  * 하위 단계의 제한 시간 만료
  * Java 서비스에서 발생한 예외
  * 허용되니 않는 null 값을 반환하는 문서 쿼리
* REPEAT Step에서 여러 하위를 지정하는 경우 하위 Step의 하나가 실패하면 천체 하위 세트가 다시 실행
* REPEAT Step는 현재 반복의 실패 지점에서 하위 세트를 즉시 종료합니다. 즉 , 3개의 세트의 두 번째 하위가 실패하면 REPEAT Step의 해당 반복에서 세 번째 하위 Step는 실행되지 않습니다.
* Repeat on이 FAILURE로 설정된 경우 REPEAT 단계 내 하위 항복의 실패로  Count 제한에도 도달하지 않는 한 REPEAT Step 자체가 실패 하지 않습니다.
* Repeat on이 FAILURE로 설정 되고 반복이 실패하면 파이프라인은 반복이 시작되기 전의 원래 상태로 복원 됩니다. 롤백 작업은 파이프라인의 첫 번째 수준에서만 수행 됩니다. 즉, 첫 번째 수준 변수는 반복이 실패하기 전에 원래 값으로 복원되지만 서버는 첫 번째 수분 변수가 참조하는 문서에 대한 사항을 롤백하지 않습니다.
* REPEAT Step의 Timeout 속성은 가능한 모든 반복을 포함하여 전체 REPEAT 단계가 완료되어야 하는 시간을 지정합니다.  REPEAT를 사용하여 실패 시 재시도할 때 제한 시간 값을 0(제한 없음)으로 두거나 매운 높은 값으로 설정할 수 있습니다. % 기호 사이에 변수 이름을 입력하여 속성을 파이프라인 변수 값으로 설정할 수도 있습니다. 저정하는 변수는 문자열 이어야 한다.
* 개발자는 REPEAT단계에 포함하는 프로세스에 대해 철저히 숙지해야 합니다. 실패가 발생한 경우 지정한 하위 단계를 안전하게 반복할 수 있는지 확인 하십시오. 주문 수락 또는 계정 잔액 입금과 같은 단일 작업이 두 번 적용될 가능 성이 있는 경우 REPEAT를 사용하지 않습니다.

* 실패한 단계를 재실행하는 REPEAT 단계를 빌드하려면
  1. REPEAT Step을 기존 Flow Service에 추가하는 경우 편집기에 해당 서비스를 표시하고 REPEAT Step을 추가 할 바로 위의 단계를 강조 표시
  2. 다음 중 하나를 수행
    2-1. Flow Service 편집기 도구 모음에서 ?? 옆에 있는 버튼을 클릭하고 ???을 클릭
    2-2. Flow Service 편집기 옆을 클릭하여 팔레트 보기를 열어 ??클릭하여 Flow 서비스 편집기로 드래그하여 가져옵니다.
    2-3. REPEAT Step 아래에서 다음 단계를 사용하여 반복하려는 각 단계를 추가
      2-3-1. Flow Service 편집기 도구 모음의 버튼을 사용하여 Flow Step을 추가
      2-3-2. Flow Service 편집기 도구 모음을 사용하여 해당 흐름 단계를 들여씁니다.(REPEAT 단계의 자식으로 만듭니다.)
      2-3-3. 필요에 따라 하위 단계의 속성을 설정합니다.
    2-4. File >  SAVE를 클릭 
 
#####  Properties 설명
 |For this property...|Specify...|
|------|---|
|Comments|해당 Step의 설명|
|Scope|해당 Step에서 제한하려는 파이프라인 문서(IData 객체)이름 입니다. 이단계에서 전체 파이프 라인에 액세스 하려면 이 속성은 공백으로|
|Timeout|실행 해야하는 최대시간(초) 단계가 완료되기 전에 이 시간이 경과 하면 통합 서버는 FlowTimeoutException을 발행하고 서비스의 다음 단계세서 실행을 계속 진행|
|Label|해당 REPEAT Step의 선택적 이름 또는 null, 일치하지 않거나 빈문자열($null, $default, 공백) <br>※ 이 Step을 BRANCH 또는 EXIT 단계의 대상으로 사용하는 경우 Label특성에 값을 지정해야합니다. |
|Count| 하위 Step을 다시 실행하려는 최대 횟수. 이 속성에 대하 파이프라인 변수 값을 사용하려면 % 기호 사이에 변수 이름을 입력(예:%servicecount%). 지정하는 변수는 문자열이어야 한다. 하위 항복이 모두 성공할 때까지(즉, 최대 제한 없음) 다시 실행하려면 이 값을 -1로 설정|
|Repeat interval| 서버가 하위 Step을 반복할 사이의 대기 시간(초)|
|Repeat on|실패|


####  REPEAT 를 사용하여 실패한 단계 재시도
REPEAT를 사용하여 실패한 단계를 재시도 하는 것 외에도 실패가 발생할 때까지 일련의 단계를 반복하는 장치로 사용 할 수도 있습니다.
* REPEAT Step을 사용하여 성공적인 하위 단게를 다시 실행하는 경우 다음사항에 유의 하십시오.
  * REPEAT 단계의 모든 지식이 단일 예외를 반환하지 않고 실행되면 성공 조건이 충족됨
  * 집합의 하위 Step중 하나가 실패하면 실패 지점에서 REPEAT 단계가 종료되고 나머지 자식 단계는 실행되지 안습니다.
 * 이하 내용은 위의  { REPEAT 를 사용하여 실패한 단계 재시도 의  2. 다음 중 하나를 수행}과 같다.


### The SEQUENCE Step
SEQUENCE 단계를 사용하여 그룹으로 처리할 일련의 단계를 빌드합니다. 그룹의 단계는 차레로 실행됩니다. 기본적으로 BRANCH 단계의 하위를 제외한 Flow 서비스의 모든 단계는 암시적 SEQUENCE단계의 구성원 이것 처럼 실행됩니다. 즉, Flow Step이 차례대로 실행된다. 그러나 일련의 Flow Step를 명시적으로 그룹화하는 것이 유용한 경우가 있으므로 가장 일반적인 이유는 다음과 같습니다.
* BRANCE 단계 아래의 단일 대안으로 일련의 단계를 그룹화 합니다. SEQUENCE단계 사용에 대한 자세한 내용은 SEQUENCE를 BRANCH의 대상으로 사용
* 통합 서버가 전체 세트를 실행하지 않고 일련의 단계를 종료하는 조건을 지정

#### SEQUENCE를 사용하여 종료 조건 지정
암시적 순서에서 단계가 실패하면 통합ㄴ 서버는 자동으로 순서를 종료합니다. (이는 Exit on 속성이 FAILURE로 설정된 명시적 시퀸스와 동일한 동작입니다.) 단계를 명시적 시퀸스로 그룹화 하여 이 기본 동작을 재정의 하고 SEQUENCE가 종료되는 조건을 지정할 수 있습니다. 이렇게 하려면 종료 매개 변수를 다음과 같이 설정합니다

 |Set “Exit on” to…|If you want Integration Server to…|
|------|---|
|FAILURE|SEQUENCE의 단계가 실패하면 SEQUENCE를 종료합니다 Flow Service의 다음 Flow 단계에서 실행이 계속되며 SEQUENCE의 기본 동작입니다 서로를 기반으로 하는 일련의 단계가 있는 경우 실패 시 종료하는 것이 유용합니다. 예를 들어 인증 코드를 받은 다음 PO를 제출하는 일련의 단계가 있는 경우 인증 단계가 실패하면 PO제출을 건너뛸 수 있습니다. 이 조건에서 SEQUENCE가 종료되면 SEQUENCE 단계가 실패합니다. ※MAP Step에서 변환기에 의한 실패로 인해 포함된 SEQUENCE는 종료가 FAILURE로 설정된 경우 종료됩니다.|
|SUCCESS|SEQUENCE의 단계가 성공하면 SEQUENCE를 종료합니다. Flow Service 의 다음 단계에서 실행이 계속됩니다.  성공시 종료는 런타임에 각각 시도 되는 일련의 대체 단계를 구축하는 데 유용합니다. 집합의 구성원중 하나가 성공적으로 실행되면 SEQUENCE의 나머지 단계를 건너 뜁니다. 성공시 종료하도록 구성된 SEQUENCE의 하위 단계가 실패하면 파이프라인에 대한 하위 단계의 모든 변경 사항이 롤백(실행취소)되고 SEQUENCE의 다음 하위 단계에서 처리가 계속 됩니다.　※MAP 단계에서 변환기에 의한 성공적인 실행은 Exit on이 SUCCESS로 설정된 경우 포함하는 SEQUENCE가 종료되지 않도록 합니다.  성공 시 종료하도록 구성된 SEQUENCE에서 모든 하위 단계가 실패하면 통합 서버는 SEQUENCE 단계가 성공한 것으로 간주합니다. ※모든 하위 Step가 실패한 경우 성공 시 종료하도록 구성된 SEQUENCE가 성공하지 않도록 하려면 SEQUENCE의 마지막 단계로 EXIT단계를 추가하여 흐름을 종료하고 실패 신호를 보내도록 EXIT 단계를 구성합니다. 특히 Exit form 속성을 $flow로 설정하고 Signal 속성을 FAILURE로 설정합니다. 런타임 시 SEQUENCE의 다른 모든 하위 단계가 실패하고 하위 EXIT 단계가 성공하면 통합 서버는 실패 조선으로 SEQUENNCE를 종료 합니다 통합 서버는 SEQUENCE 종료 후 예외를 처리합니다. |
|DONE|SEQUENCE의 모든 단계를 실행  통합 서버는 지정된 시간 초과 한계 내에서 모든 하위를 실행하는 한 완료 시 종료하도록 구성된 SEQUENCE 단계를 성공으로 간주하고, SEQUENCE 내 하위 단계의 성공 또는 실패는 고려되지 않습니다. 하위 단계가 실패하면 파이프라인에 대한 모든 변경 사항이 롤백(실행 취소) 되고 SEQUENCE의 다음 하위 단계에서 처리가 계속 된다.  통합 서버는 모든 하위 단계가 지정된 제한 시간 내에 실행되지 않는 경우 완료 시 종료하도록 구성된 SEQUENCE 단계를 실패로 간주합니다.|

 ```
참고 : 롤백작업은 파이프라인의 첫 번째 수준에서만 수행됩니다. 즉, 첫번째 수준 변수는 단계가 실패하기 전에 원래 값으로 복원되지만 서버는 첫 번째 수준 변수가 참조하는 문서에 대한 변경 사항을 롤백하지 않습니다.
```

SEQUENCE 단계에 SEQUENCE에서 종료하도록 구성된 EXIT 단계가 포함된 경우 EXIT단계를 실행하면 SEQUENC 단계가 성공, 완료 또는 실패 시 종료하도록 구성되었는지 여부에 관계없이 항상 SEQUENCE Step에서 종료 되며, 이는 SEQUENCE 내 EXIT 단계의 위치와 EXIT단계가 성공 또는 실패를 알리도록 구성되었는지 여부에 관계없이 발생

### The LOOP Step
### The EXIT Step
### The MAP Step
### The TRY, CATCH, and FINALLY Steps



https://techdocs.broadcom.com/kr/ko/ca-enterprise-software/it-operations-management/application-performance-management/10-5/345392263/345392665/345392690.html
