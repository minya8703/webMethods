
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
LOOP 단계는 지정한 배열의 각 요소에 대해 하위 Step Sequence를 한번씩 반복합니다.  예로 파이프라인에 구매 주문 라인 항목의 배열이 포함된 경우 LOOP 단계를 사용하여 배열의 각 라인 항목을 처리할 수 있습니다.  LOOp본문을 구성하는 일련의 단계(즉, LOOP가 반복할 단계 세트 )를 지정하려면 다음 예제와 같이 LOOP 아래에 해당 단계를 하위단계로 들여 사용

* 입력 배열의 지정
 Loop Step에서는 Loop의 하나 이상의 Step에대한 입력으로 사용될 개별 요소가 포함된 입력 배열을 지정해야 하며 런타임에  Loop 단계는 지정된 배열의 각 멤버에 대해 루프의 한 처리를 실행. 예를 들어 구매 주문서에 저장된 각 라인 항목에 대해 Loop 를 실행하려는 경우 주문 라인 항목이 Loop의 입력 배열로 저장된 문서 목록을 사용.
 * LOOP Step의 속성 보기에서 입력 배열의 이름을 지정합니다. 지정하는 배열은 다음 데이터 유형 중 하나입니다,
   * String list
   * String table
   * Document list
   * Object list

#### LOOP properties
Flow를 설계할 때 루프 내의 서비스는 지정된 입력 배열의 개별 요소에 대해 작동하기 때문에 전체 배열이 아닌 배열의 요소를 입력으로 사용하도록 설계되어야 한다.
예) Loop가 Item, Qty 및 UnitPrice라는 하위 항목을 포함하는 LineItems라는 문서 목록에 대해 실행되는 경우 LineItems를 LOOP단계의 입력 배열로 지정 하지만 루프 내의 서비스는 LineItems(예를 들어 Item, Qty, UnitPrice)을 입력으로 사용
※ LOOP단계는 입력 배열이 다른 변수의 하위(예 : 문서의 하위인 문자열 목록)인 경우 스레드로 부터 안전하지 않습니다. LOOP Step은 단계 실행 중에 입력 및 출력 배열의 차원을 변경하기 때문에 상위 변수에 액세스하는 서비스를 호출하는 모든 스레드는 입력 배열 변수를 배열 또는 스칼라로 경험할 수 잇습니다. 이로 인해 상위 변수에 액세스하는 스레드에 대해 예측할 수 없는 동작이 발생합니다.

입력 배열이 파이프라인의 최상위 변수인 경우 Loop단계를 포함아는 서비스에 대한 파이프라인 개체(IData)에 액세스하는 스레드도 예측할 수 없는 동작을 경험할 수 있습니다. 따라서 입력 배열의 포함하는 문서, 문서 목록 또는 파이프라인과 같이 객체에 동시에 액세스 할 수 있는 다른 서비스를 코딩하지 마십시오.LOOP Step의 입력 차원 변경 사항에 대한 자세한 내용은 
[LOOP 단계의 파이프라인 정보를](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.flow.loop.aboutPipelineForLoop.html#wwID0EWBAQB "LOOP 단계의 파이프라인 정보")  참조

* LOOP Step에서 출력 수집
  * Loop Step에서 출력 변수를 생성하는 경우 서버는 해당 출력을 파이프라인의 배열로 수집할 수 있습니다.
  * 이렿게 하려면 출력 배열 매개 변수를 사용하여 서버가 루프의 각 반복에 대한 출력을 수집할 배열 변수의 이름을 지정
  * 예) Loop가 구매 주문서에 있는 각 라인 항목의 재고 상태를 확인하고 실행될 때마다 InventoryStatus 라는 문자열을 생성 하는 경우 InventoryStatus를 출력 배열 의 값으로 지정 합니다. 런타임에 서버는 InventoryStatus를 각 루프 반복의 출력을 포함하는 배열 변수로 자동 변환합니다.
  ※ Loop Step을 종료하도록 구성된 EXIT Step 또는 Loop Step의 반복은 출력 배열의 내용에 영향을 미칩니다. [반복, 단계 또는 서비스 종료를](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.flow.exit.exitFrom.html#wwID0EVFBQB "반복, 단계 또는 서비스 종료") 참조
* LOOP 단계의 파이프라인 정보
  * LOOP Step의 분문에서 입력 배열로 사용되는 필드가 차원적으로 축소됩니다. 예로 입력 배열이 문자열 목록인 경우 입력은 LOOP본문 내에서 문자열로 표시됩니다. 입력 배열이 문자열 테이블인 경우 입력은 LOOP본문 내의 문자열 목록입니다. 이는 LOOP 단계가 입력 배열의 각 요소에서 작동하기 때문입니다.
  *  출력 배열로 사용되는 필드도 LOOP단계의 본문 내에서 차원이 줄어듭니다. Loop Step이 배열을 생성하는 동안 LOOP Step의 각 반복은 배열에 하나의 요소를 생성합니다. 출력 배열이 문자열 목록인 경우 LOOP 본문 내에서 문자열입니다. 출력 배열이 문자열 테이블인 경우 LOOP 본문 내에서 출력은 문자열 목록입니다.
다음 예에서 Loop Step은 myInputLIst 라는 입력 배열의 각 항목에 대해  pub.math:addInts 서비스를 실행합니다. LOOP 단계는 출력을 myOutputList라는 배열로 수집합니다. 즉, pub. math:addInts 서비스는 문자열을 입력으로 사용하고 문자열을 출력하고 생성합니다. 결과적으로 pub.math:addInts 서비스 파이프라인에서 입력은 myInputList 라는 문자열 이고 출력은 myOutputList라는 문자열입니다. LOOP Step이 완료된 후 파이프라인을 보면 myInputLIst 및 myOutputLIst 가 문자열 목록으로 나타납니다.
![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/loop_dimensions.png)
* LOOP Step 만들기
  1. LOOP Step을 기존 Flow Service에 추가하하는 경우 편집기에 해당 서비스를 표시하고 Loop Step을 추가할 바로 위의 단계를 선택
  2. 아래의 하나를 수행
    2-1. Flow Service 편집기 도구 모음에서 ?? 옆에 있는 버튼을 클릭
    2-2. Flow Service 편집기 옆을 클릭하여 팔레트 보기를 엽니다. 클릭 ?? 하여 Flow Service 편집기로 드래그
  3. Properties 설명을 참고하여 필드를 완성
  4. 다음 Step을 사용하여 루프 본문을 작성
    4-1. Flow Service 편집기 도구 모음의 버튼을 사용하여 Flow Step을 추가
    4-2. Flow Service 편집기 두구 모음에서 ?? 을 사용하여 Flow Step의 하위 단계로 만듭니다.
    4-3. 필요에 따라 하위 단계의 속성을 설정
  5.  파이프라인 보기를 사용하여 입력 배열의 요소를 LOOP단계의 각 하위에 필요한 입력 변수에 연결하십시오. 파이프라인 보기 사용자에 대한 자세한 내용은 [Flow Services의 데이터 매핑을](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.map.html#wwID0EGSFQB "Flow Services의 데이터 매핑") 참조
#####  Properties 설명
 |For this property…|Specify…|
|------|---|
|Comments|해당 Step의 설명|
|Scope|해당 Step을 제한하려는 파이프라인의 문서(IData 객체)이름입니다.|
|Timeout|다른 Step의 Timeoutr과 동일|
|Label|해당 Step의 설명|
|Input array| LOOP가 작동할 배열 변수의 이름. 이 변수는 문자열 목록, 문자열 테이블, 문서 목록 또는 객체 목록 유형 중 하나여야 합니다.|
|Output array| LOOP가 실행될 때마다 서버에서 수집할 요소의 이름, LOOP가 출력 값을 생성하지 않거나 입력 배열의 요소를 수집하는 경우 이 속성을 지정할 필요가 없습니다.|

 ```
 ※LOOP Step을 빌드할 때 LOOP 본문의 MAP 또는 INVOKE 단계 내에서 출력 배열 변수에 대한 링크를 생성하기 전에 LOOP 출력 배열 속성에 출력 배열 변수를 지정했는지 확인하십시오. 링크를 만든 후 출력 배열 변수를 지정하면 런타임 시 링크가 실패합니다. Designer에서 단계를 디버그하여 링크가  성공하였는지 확인할 수 있습니다. 링크가 실패하면 출력 배열 변수에 대한 링크를 삭제한 다음 다시 생성하십시오.
```

### The EXIT Step
* EXIT Flow  Step은 전체 Flow Service, 특정 상위 흐름 단계 또는 LOOP 또는 REPEAT 단계 내의 반복을 종료하고 종료의 일부로 성공 또는 실패 신호를 보냅니다. 전체 Flow Service를 종료할 때 EXIT 단계는 실행 제어를  Flow Service 또는 Java 서비스일 수 있는 상위 서비스로 이전합니다. 종료로 인해 Flow Service의 최상위 수준이 종료되면 Flow Service 실행이 성공적으로 종료 되거나 예외와 함께 종료됩니다. Flow Service 내에서 Step을 종료할 때 EXIT Step은 실행 제어를 다른 Flow Step으로 이전합니다.

* 서비스 실행이 계속되는지 여부와 제어가 이전되는 위치는 EXIT 단계가 성공 또는 실패 신호를 보내는 지 여부와 EXIT Step이 종료되는 단계에 따라 다릅니다.
* EXIT Step을 사용하는 경우
  * 몇 단계로 중첩된 단계 내에서 천체 흐름 서비스를 종료
  * ServiceException을 발생시키는 Java 서비스를 작성하지 않은 Flow 또는 Flow Step을 종료할 때 예외 발생
  * Flow Step을 갑자기 완료
  * 예외를 발생시키지 않고 LOOP 뜨는 REPEAT 흐름 단계를 종료
  * 전체 LOOP 또는 REPEAT 단계를 종료하지 않고 LOOP 또는 REPEAT 흐름 단계의 반복을 종료

* 다음 Flow Service에는 실행될 경우 가장 가까운 상위 LOOP 단계를 종료하는 두 개의 EXIT Step이 포함되어 있습니다. CreditCardType의 값이 null이거나 빈 문자열인 경우 일치하는 EXIT Step이 실행되고 '/POs/PurchaseOrdersList' 단계에서 LOOP를 종료합니다.
![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/FlSvc_EXITstep.png)

* 성공 또는 실패 시 종료 - EXIT Step에서 종료가 성공 조건 또는 실패 조건을 반환해야하는 지 여부를 나타냅니다.
  * 성공은 포함하는 Flow Service 또는 Flow Step이 성공적으로 실행됨을 나타냅니다. 단계가 종료되는 반복, 흐름 단계 또는 Flow Service를 나타내는 종료 속성 값에 따라 서비스 실행이 계속됩니다.
    Flow Step 또는 Service의 갑자기 발생시킬 완료를 수행하기 위해 종료하고 성공 신호를 보낼 수 있습니다. 갑자기 발생한 완료는 정상적인 완료 전에 Flow Step에서 전환되는 것으로, 단계 또는 포함 단계의 끝까지 실행됩니다. 갑자기 발생한 완료는 시패가 아니며, 실행은 흐름 서비스의 다음 반복, 흐름 단계 또는 서비스에서 계속됩니다. Exit from 속성은 서비스가 종료되는 위치와 결과적으로 서비스 실행이 계속되는 방식을 결정합니다.
 $iteration, $lopp, $flow 또는 $parent를 종료하고 성공 신호를 보내도록 구성된 EXIT 단계를 사용하여 갑자기 발생하는 완료를 수행 할 수 있습니다.
* 실패는 EXIT Stepo가 종료되는 Flow Service 또는 Flow Step이 실패로 종료 됨을 나타 냅니다. 신호 실패 잡히거나 Flow 가 완료될 때까지 보류 중인 예외를 생성합니다. 실패와 함께 Step이 종료되면 실패가 상위 Step으로 이동하여 오류가 흐름의 최상의 수준으로 이동하며 발견되지 않으면 통합 서버에서 FlowExceprion이 발생합니다. 통합 서버가 발생시키는 예외와 리턴되는 오류 메시지의 텍스트를 지정할 수 있습니다.
 ``` 
 ※TRY, CATCH, FINALLY 사용 패턴의 일부로 CATCH Step을 사용하여 EXIT 단계에서 발생한 예외를 포함하여 예외를 발견하고 응답하도록 서비스를 구성할 수 있습니다.
```

* 정상완료, 갑작스러운 완료 및 실패에 대한 정보와 이것이 TRY, CATCH 및 FINALLY Step에 미치는 영향에 대한 자세한 내용은  [CATCH 및 FINALLY 단계의 정상 및 갑작스러운 완료 및 실패를](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.tcf.completion.html#wwID0EJLVQB "TRY, CATCH 및 FINALLY 단계의 정상 및 갑자기 발생하는 완료 및 실패")를 참조

* 반복, 단계 또는 서비스 종료

  * EXIT Step을 빌드할 때 LOOP또는 REPEAT Step의 반복,  상위 Flow Step, 특정 Flow Step 또는 전체 Flow Service와 같이 EXIT Step을 종료하려는 항복 에서 지정합니다. Flow Service 내에서 Step을 종료하면 EXIT Step이 종료된  다음 Step에서 실행이 계속 됩니다.
  * EXIT Step 실행으로 인해 통합 서버가 Flow Service의 끝에 도달하면 ( 즉, 동일한 Flow Service에 다음 단계가 없음) Flow Service가 종료 됩니다. EXIT Step의 결과에 따라 Flow 서비스가 성공 또는 실패로 완료하였는지 여부가 결정됩니다.  서비스가 실패로 끝나면 통합 서버는 보류 중인 예외를 처리합니다. EXIT Step이 실패로 완료로 처리 메시지를 보냈지만 특정 예외를 지정하지 않은 경우 통합 서버는 FlowException을 처리합니다.


 |Exit from value | Description|
|------|---|
|$parent| Flow Step에 관계없이 상위 Flow Step에서 즉시 종료|
|$loop| 가장 가까운 상위 LOOP 또는 REPEAT Flow Step에서 종료 <br>
EXIT Step이 TRY, CATCH 또는 FINALLY Step의 인접한 하위 Step인 경우 TRY, CATCH 또는 FINALLY Step 내에서 실패한 $loop를 종료하는 것은 허용되지 않습니다. 이것은 흐름 정의 오류로 간주됩니다. 이로 인해 FlowException이 발생하고 Flow Service가 바로 종료된다. <br>
그러나 TRY, CATCH 또는 FINALLY 내부의 더 깊이 중첩된 단계 내에서 오류가  있는 $loop를 종료하는 것은 가능합니다. 컨트롤이 TRY, CATCH 또는 FINALLY Step으로 돌아 갑니다. <br>
LOOP Step을 종료할 때 통합 서버는 출력 변수의 현재 값을 출력 배열로 복사하지 않습니다. 이는 LOOP Step에 출력 배열 변수의 값을 매핑하거나 설정하는 MAP 단계 또는 INVOKE Step이 포함된 경우에도 마찬가지 입니다. Loop에서 나가면 LOOP 단계의 본문이 정상적으로 완료되지 않으므로 결과적으로 출력 배열 변수의 값이 파이프라인에 복사되지 않는다. |
|$flow| 통합 서버는 Flow Service의 맨 위에 도달할 때까지 EXIT Step의 상위 흐름 Step에서 종료됩니다. $flow 값에서 종료는 통합 서버가 전체흐름 서비스를 종료함을 나타냅니다.  $flow whith failure는 바로 종료 되며 통합 서버는 개입하는 CATCH 또는 FINALLY 단계를 실행 하지 않습니다.  Exit from $flow whith successful은 EXIT와 Flow의 상단 사이에 개입하는 FINALLY 단계를 실행합니다.|
|$iteration| 가장 가까운 상위 LOOP또는 REPEAT 단계의 현재 반복에서 종료합니다. 통합 서버는 EXIT 단계에 가장 가까운 상위 LOOP 또는 REPEAT Step의 현재 반복을 종료합니다. 그런 다음 통합 서버는 LOOP 또는 REPEAT Step의 다음 반복을 실행<br> ※ 반복을 종료할 때 EXIT는 성공 신호를 보내야 합니다. 반복 종료 및 신호 실패는 허용되지 않으며 실행시 FlowException이 발생하고 FlowException이 발생하고 Flow Service가 즉시 종료됩니다. EXIT Step은 $loop를 종료할 때 실패 신호를 보낼 수 있습니다.<br>※ 반복을 종료할 때 통합 서버는 EXIT Step 실행 전에 발생한 조치를 롤백하지 않습니다. 예를 들어 EXIT Step이 실행되기 전에 반복의 출력이 출력 배열 변수에 설정된 경우 반복 출력은 여전히 출력 배연 변수에 나타납니다. <br>Loop Step 내에서 포함하는 TRY, CATCH 또는 FINALLY Step에서 실행되는 exit $iteration은 해당 단계와 Loop Step 까지의 중간 단계를 갑자기 완료합니다. 발견되지 않은 실패로 FINALLY Step이 갑자기 완료되면서 실패가 삭제 됩니다. <br> REPEAT Step 포함된 TRY, CATCH 또는 FINALLY Step에서 실행된 exit $iteration은 해당 단계와 REPEAT Step까지의 중간 단계를 갑자기 완료합니다. 발견되지 않은 실패로 FINALLY가 갑자기 완료되면 실패가 삭제됩니다. 이로 인해 반복 실패가 성공이 되고 REPEAT Step 실행이 완료될 수 있습니다.|
|label| 통합 서버는 지정된 레이블이 있는 흐림 단계에 도달할 때까지 상위 Flow Step을 종료합니다. 지정된 레이블은 EXIT Step에 대한 상위 Flow Step이어야 합니다. 그렇지 않은 경우 Flow Service는 FlowException으로 종료됩니다. <br> EXIT Step이 TRY, CATCH 또는 FINALLY Step의 직속 자식인 경우 TRY, CATCH또는 FINALLY 단계 내에서 실패한 레이블에서 종료하는 것은 허용 되지 않습니다. 이는 흐름 정의 오류로 간주되며 FlowException이 발생하고 Flow Service가 즉시 종료 <br> 그러나 TRY, CATCH 또는 FINALLY 내부의 더 깊이 중첩된 단계 내에서 오류가 있는 레이블에서 종료하는 것은 가능합니다. 컨트롤이 에리블이 지정된 단계로 가게 됩니다.|

* EXIT Step 만들기
  * Flow Service에서 EXIT Step을 빌드할 때 컨테이너 역활을 하는 Flow Step만 하위에서 종료 단계를 가질 수 있습니다. 여기에는 SEQUENCE, BRANCH, REPEAT, LOOP, TRY, CATCH 및 FINALLY가 포함됩니다. Flow Service의 최상위 Step은 암시적 SEQUENCE의 구성원 입니다.
  *  자세한 내용은 지침을 포함하여  TRY, CATCH 및 FINAL과 함께 종료 단계를 사용하는 방법[Limitations for the TRY, CATCH, and FINALLY Steps](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/to-try_catch_finally_2.html#wwID0EUIWQB "Limitations for the TRY, CATCH, and FINALLY Steps")을 참조
  *  다음중 하나를 수행
    * Flow Service 편집기 도구 모음에서  ?? 옆에 있는 버튼을 클릭하고 ?? 을 클릭합니다
    * Flow Service 편집기 옆을 클릭하여 파레트 보기를 열어 ??을 클릭하여 Flow Service 편집기로 드래그 합니다.
  #####  Properties 설명
 |For this property…|Specify…|
|------|---|
|Comments|해당 Step의 설명|
|Label| 이 특정 Step에 대한 선택적 이름 또는 null, 일치하지 않거나 빈 문자열 ($null, $default, 공백)<br> ※이 Step을 BRANCH Step의 대상으로 사용하는 경우 레이블 특성에 값을 지정 해야 합니다. BRANCH Step에 대한 자세한 내용은 BRANCH Step을 참조|
|Exit from| 종료하려는 Flow Step입니다. 아래의 하나를 지정 <br>$parent - Step 유형에 관계없이 상위 Flow입니다. 이것이 기본값<br>$loop- 가장 가까운 상위 Loop 또는 REPEAT Flow<br>$flow- 전체 Flow <br>$iteration- 가장 가까운 상위 Loop 또는 REPEAT Flow Step의 반복입니다.<br>label - 이 값과 일치하는 레이블이 있는 가장 가까운 상위 Flow Step입니다. ※ 지정한 레이블이 상위 Flow Step의 레이블과 일치하지 않으면 서비스가 FlowExceprion과 함께 종료<br><blank> - 가장 가까운 상위 Loop 또는 REPEAT Flow Step 이는 $loop값을 지정하는 것과 같습니다.|
|Signal|종료를 성공 실패로 간주할지 여부. 다음 중 하나를 지정<br> SUCCESS - 성공 조건으로 Flow Service 또는 Flow Step을 종료<br> FAILURE - 실패 조건으로 Flow Service 또는 Flow Step을 종료. 종료 후 예외가 발생. 실패 메시지 속성으로 오류 메시지를 지정 예를 들어:

java.lang.예외

com.wm.app.b2b.server.ServiceException

com.wm.lang.flow.FlowException

com.costomerCo.CustomException

유효한 클래스 이름은 현재 클래스 로더에서 사용할 수 있어야 하며 java.lang.Exception을 확장해야 합니다.

클래스 이름이 유효하지 않은 경우 통합 서버는 실패 메시지 값 에 다음 메시지가 추가된 기본 예외를 처리합니다 .

-- 지정된 실패에 대한 클래스를 찾을 수 없거나 유효하지 않음

실패 이름 속성 의 기본값은 종료 위치 값 에 따라 다릅니다 .

* Exit from이 $flow 로 설정된 경우 기본값은 com.wm.lang.flow.FlowException입니다.
* 다른 모든 Exit from 값의 경우 기본값은 com.wm.lang.FlowFailure입니다.

이 속성에 대해 파이프라인 변수 값을 사용하려면 % 기호 사이에 변수 이름을 입력합니다(예: %failure% ). 지정하는 변수는 문자열이어야 합니다.

EXIT 단계에서 예외를 발생시키려면 실패 이름 또는 실패 인스턴스 특성에 대한 값을 지정하십시오. 둘 다 지정하는 경우 통합 서버는 실패 인스턴스 값을 사용합니다 .

이 속성은 Signal이 FAILURE 로 설정된 경우에만 사용됩니다 .|
|Failure name| 이 실패에 대해 생성될 보류중인 예외의 정규화된 Java 클래스 이름 |
|Failure instance|EXIT 단계에서 실패로 식별하려는 기존 예외 인스턴스가 포함된 파이프라인 변수의 이름입니다. 이 인스턴스는 pub.flow:getLastFailureCaught 서비스의 실패 출력 매개변수 일 가능성이 큽니다 .

지정된 파이프라인 변수는 객체 유형이어야 합니다.

파이프라인의 개체 변수는 java.lang.Exception을 확장해야 합니다. 그렇지 않은 경우 통합 서버에서 FlowException이 발생합니다.

존재하지만 런타임 시 예외를 포함하지 않는 파이프라인 변수를 지정하거나 존재하지 않는 변수를 지정하는 경우 통합 서버는 FlowException을 발생시키고 흐름 서비스를 종료합니다.

이 속성은 Signal이 FAILURE 로 설정된 경우에만 사용됩니다 .|
|Failure message|표시하려는 예외 메시지의 텍스트입니다. 이 속성에 대해 파이프라인 변수 값을 사용하려면 % 기호 사이에 변수 이름을 입력합니다(예: %mymessage% ). 지정하는 변수는 문자열이어야 합니다.

이 속성은 Signal이 FAILURE 로 설정된 경우에만 사용됩니다 .|

### The MAP Step
MAP Step을 사용하면 Flow 서비스이 모든 지점에서 파이프라인의 내용을 조정할 수 있습니다. MAP 단계를 빌드하면 다음을 수행 할 수 있습니다.
* 파이프라인에서 변수를 연결, 추가 및 삭제하여 Flow 서비스의 다음 단계에서 사용할 파이프라인을 준비
* 이전 단계에서 추가 했지만 다음 단계에서 필요하지 않은 필드를 제거하여 이전 단계 후에 파이프라인을 정리
* 변수를 이동하거나 파이프라인의 변수에 값을 할당 합니다.
* 흐름 서비스의 입력 값을 초기화합니다.
* 단일 단계에서 여러 서비스(transformers)를 호출합니다.
* 한 형식에서 다른 형식으로 문서를 매핑. 예) XML형식문서를 ebXML형식이나 소유 형식으로 매핑가능
※ MAP Step은 Flow Service에서 초기 입력 값 집합을 하드 코딩하는 데 특히 유용합니다. 이 방법으로 사용하려면 흐름의 시작 부분에 MAP Step을 추가한 다음 값 설정 수정자를 사용하여 Pipeline Out의 적절한 변수에 값을 할당합니다.

### The TRY, CATCH, and FINALLY Steps
TRY, CATCH 및 FINALLY Step은 Flow Service의 서비스의 실패를 처리하기 위한 webMethods Flow 언어 기능
* TRY Step에는 통합 서버 에서 시도하고 실패 처리를 제공하려는 일련의 흐름 단계가 포함
* CATCH Step 이전 TRY Stepd이 실패할 경우 실행하려는 일련의 단계가 포함되어 있습니다. 종종 CATCH Step에는 복구 놀리가 포함됩니다.
* FINALL Step에는 TRY Step의 성공 여부에 관계 없이 통합 서버가 실행하는 논리가 포함됩니다. 종종 FINALY Step단계의 결과에 관계없이 실행해야 하는 정리 논리가 포함되어 있습니다.

## Layout Tab 에서 작업

### Layout Tab이란
 * Layout Tab은 Tree Tap과 같이 디자이너가 Flow Service 편집기에 표시하하는 Flow Service의 보기이며 두 Tab중 하나를 사용하여 흐름 서비스를 구축하거나 편집할 수 있습니다. 그러나 Layout Tab은 Flow Service를 생성할 수 있는 더 많은 그래픽 보기를 제공합니다.
 * Layout Tab에서 Flow Service는 순서도와 유사하게 표시하며, 디자이너는 Flow Step과 Flow Service의 시작 및 종료에 대한 구체화된 모양을 표시합니다. 선은 Flow Step을 연결하고 Flow Step이 실행되는 순서를 보여줍니다.
 * 언제 Layout Tab을 사용하나?
   * 두 Tab 중 사용하기 쉬운 페이지에서 작업하며, Flow Service를 구축할 때 Tab 간에 쉽게 전환할 수 있다. 예로 Layout Tab에서 Flow Step을 추가하고 Flow Service의 기본 구조를 정희하는 것이 더 쉬울 수 있지만 Tree Tab을 사용하여 데이터 매핑을 할 수 있다.
   * 아래의 경우 Layout Tab이 편리하다
     * Flow Service를 순서대로 작성하는 것보다 플로우 차트로 작성하는 것이 더 쉽다거나 Flow Service를 일련의 라인별 단계가 아닌 다이어그램으로 보면 Flow Service가 수행하는 프로세스를 더 쉽게 상상할 수 있습니다.
     * 프로그래밍에 익숙하지 않거나 webMethods Intergration Server 에 익숙하지 않은 사람과 비지니스 프로세스를 설계할경우 순서도가 편할 수 있다.
     * Flow Service가 관리에 작동하는 방식에 대한 다이어그램을 표시해야 합니다.(Flow Service는 인쇄 불가)
   * 
### Layout Tab에서 Flow Service는 어떻게 표시되나
 Layout Tab은 Flow Service의 시작과 끝,  상위 단계, 하위 단계, Flow Step이 실행되는 순서와 같은 프름 서비스 요소에 대한 구체화된 모양과 구조를 사용. 디자이너는 Flow Step을 왼쪽에서 오른쪽으로 순차적으로표시하고 해당 순서 대로 단계를 실행
 Designer는 Flow Service를 생성할 때 시작 및 종료 기호를 자동으로 추가하며, Flow Service에 Step을 추가하면 Designer는 Flow Step을 서비스의 나머지 단계에 연결하는 선을 자동으로 이어 줍니다.
 
### Flow Service 편집기에서 눈금선 표시 또는 숨기기
View > Grid 를 선택
### Layout Tab에서 Flow Service 구축
Layout Tab에서 Flow Service를 구축하는 것은 Tree Tab에서 Flow Service를 구축하는 것과 동일한 단계인 Flow Service 생성, Flow Step 추가, 속성설정, 서비스 입력 및 출력 매개변수 선언, 파이프라인 데이터 매핑, 실행 설정으로 구성. -시간매개변수 Flow Step을 추가하고 이동하는 방법을 제외하고 각 단계를 완료하는 절차는 Tree Tab에서 Layout Tab에서 동일

# Flow Services의 데이터 매핑
시스템은 다른 시스템에 필요한 정확한 형식으로 데이터를 생성하는 경우가 거의 없기 때문에 일반적으로 데이터 변환을 수행하는 흐름 서비스를 빌드 해야 합니다. Designer 에서 데이터를 매핑하여 데이터 변환을 수행 할 수있다.

* 이름 변환 이러한 유형의 변환은 데이터 명명 방식의 차이를 해결 이름 변환을 수행하면 문서 구조에서 변수의 값과 위치는 동일하게 유지되면서 변수의 이름은 변경됩니다.(예. 한 서비스는 전화번호 정보에 대한 변수 이름을 telephone을 사용하고 다른 서비스에서는 phoneNumber를 사용하는 경우)
* 구조적 변형 이 유형의 변환은 값이 표현되는 방식의 차이를 해결(예. 한 서비스의 문서 형식은 telephone 이라는 문자열에 전화 번호를 넣을 수 있으며 다른 서비스에서는 문서형식은 customerInfo라는 이름 문서에 중첩된 것을 찾을 수 있습니다만 구조 변환을 수행할 때 변수 값은 동일하게 유지되지만 문서 구조에서 변수의 데이터 유형 또는 위치는 변경됩니다.)
* 가치 변환 이 유형의 변환은 값이 표현되는 방식의 차이를 해결합니다. 값 변환을 수행할 때 변수의 이름과 위치는 동일하게 유지되지만 변수에 포함된 데이터는 변경됩니다.(예. 시스템 표준코드, 통화단위, 날짜 또는 무게와 측정값과 같은 값에 대해 다른 표기법을 사용하는 경우)
## 파이프라인 보기에는 무엇이 포함되어 있나?
파이프라인 보기는 데이터를 매핑하고 파이프라인의 내용을 검사할 수 있는 모든 데이터의 그래픽 표현을 제공합니다. 이 보기의 도구를 사용하여 서비스간에 또는 문서 형식 간에 변수(데이터)를 라우팅 합니다.
파이프라인 보기는 호출된 서비스(INVOKE 단계) 또는 Flow Service의 MAP Step에 대한 파이프라인을 표시 파이프라인 보기의 내용은 INVOKE Step과 MAP Step이 다릅니다.

### INVOKE 단계에 대한 파이프라인 보기
 Invoke Step의 경우 파이프라인 보기는 편집기에서 선택한 서비스와 관련된 파이프라인 두 단계를 나타냅니다.
 ![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/Mapping_PipelineViewINVOKEstep.png)
|This stage...|Represents...|
|------|---|
|1 | 선택한 서비스가 실행되기 직전에 예상되는 파이프라인 상태입니다. <br> Pipeline In은 서비스가 실행되기 전에 파이프라인에 있을 것으로 예상되는 변수 집합을 나타냅니다(이전 서비스의 선언된 입력 및 출력 매개 변수 기반) Service In은 선택한 서비스가 입력으로 예상하는 변수 세트를 나타냅니다(입력 매개변수에 의해 정의 됨)<br> 파이프라인 보기에서 이 단계에 "파이프라인 수정자"를 추가하여 서비스 요구 사항에 맞게 파이프라인의 콘텐츠를 조정할 수 있습니다.<br> 예).변수를 연결하고, 변수에 값을 할당하고, 파이프라인에서 변수를 삭제하거나 파이프라인에 변수를 추가할 수 있습니다. 이 단계에서 지정하는 수정 사항은 서비스가 런타임에 실행 되기 직전에 수행 |
|2 | 서비스 실행 직후 예상되는 파이프라인 상태 <br> Service Out은 서비스가 출력으로 생성하는 변수 집합을 나타냅니다(해당 출력 매개 변수에 의해 정의)<br> Pipeline Out은 서비스 실행후 파이프라인에 있을 것으로 예상되는 변수 집합을 나타냅니다. 흐름의 다음 서비스에서 사용할 수 있는 변수 집합을 나타냅니다. 선택한 서비스(INVOKE Step)가 흐름 서비스의 마지막 단계인 경우 Pipeline Out은 흐름 서비스에 대한 출력 변수를 표시합니다(입력/ 출력 탭에서 선언됨)<br> 파이프라인 보기에서 이 단계에 "파이프라인 수정자"를 추가하여 파이프라인의 내용을 조정할 수 있습니다. 예를 들어 변수를 연결하고, 변수에 값을 할당하고, 파이프라인에서 변수를 삭제하거나 파이프라인에 변수를 추가할 수 있습니다. 이 단계에서 지정하는 수정 사항은 서비스가 런타임에 실행된 직후에 수행 |

### MAP 단계에 대한 파이프라인 보기
MAP Step의 경우 파이프라인 보기는 파이프라인의 단일 단계를 표시합니다. 파이프라인 보기에는 두개의 변수 세트인 Pipeline In 및 Pipeline Out이 포함되어 있다. 이러한 변수 세트 사이에 파이프라인 보기에는 Transformers 라는 열이 포함되어있다.
![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/mappingdatainflowservice_scr_02.gif)
* Pipeline In 열은 MAP Step에 대한 입력을 나타내며. 여기에는 프름의 이 지점에서 파이프라인의 모든 변수 이름이 포함된다.
* Transformers 열에는 값 변환을 완료하기 위해 MAP Step에 삽입된 모든 서비스가 표시됩니다. MAP Step에서 서비스 호출에 대한 자세한 정보는 [Transformers  작업을](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.map.transformer.html#wwID0E1EOQB "트랜스포머 작업") 참조
* Pipeline Out 열은 MAP Step의 출력을 나타냅니다. 여기에는 MAP 단계가 완료될 때 파이프라인에서 사용할 수 있는 변수의 이름이 포함됨
* MAP Step을 Flow에 처음  삽입할 때 Pipline In과 Pipline Out은 동일하나 MAP Stepd이 Flow Service의 유일한 단계이거나 Flow Service의 마지막 단계인 경우 Pipeline Out은 Flow Service에서 출력으로 선언된 변수도 표시합니다.

## 기본 맵핑 작업방법
기본 매핑 작업은 파이프라인 콘텐츠와 파이프라인의 변수 값을 관리하기 위해 수행하는 작업이빈다. 파이프라인 보기이에서 다음과 같은 기본 매핑을 수행할 수 있습니다.
* **변수를 서로 연결합니다.** 한 서비스 또는 문서형식의 변수 값을 다른 서비스 또는 문서 형식의 변수에 복사할 수 있습니다.
* **변수에 값을 할당합니다.** 변수 값을 하드 코딩하거나 변수에 기본값을 할당할 수 있습니다.
* **파이프라인에서 변수를 삭제합니다.** 흐름의 후속 서비스에서 사용하지 않은 파이프라인 변수를 제거할 수 있습니다
* **파이프라인에 변수를 추가합니다.** 흐름 서비스의 입력 또는 출력 매개변수로 선언되지 않은 변수를 추가할 수 있습니다. 흐름 서비스가 호출하는 서비스(내부 호출 서비스)에 대한 입력 및 출력 변수를 추가할 수도 있다.

### 변수 연결 정보
 서비스 또는 문서형식의 변수 값을 다른 변수에 복사하여는 경우 변수를 연결합니다. Designer는 파이프라인 보기의 서비스 및 파이프라인 변수를 링크 라는 선으로 연결 변수 아이에 링크를 생성하려면 런타임에 한 변수에서 다른 변수로 값이 복사됩니다.
 Flow 내에서 Designer는 이름이 동일하고 데이터 유형이 호환되는 변수를 암시적으로 연결합니다. 예) 다음 흐름의 서비스는 AcctNumber라는 변수를 사용합니다. 이름의 변수가 Pipeline In에 이미 있으므로 Service In의 Acctnumber변수에 자동으로 연결 됩니다. Designer는 암시적으로 연결된 변수를 회색 링크로 연결
![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/Mapping_ImplicitLinks.png)
Flow Service가 정보 조각에 동일한 이름을 사용하지 않는 경우 파이프라인 보기를 사용하여 변수를 서로 명시적으로 연결합니다. 명시적 연결은 흐름에 필요한 이름 및 구조 변환을 수행 하는 방법입니다. 디자이너는 명시적으로 연결된 변수를 검은 색 실선으로 연결합니다.
파이프라인 보기의 입력 측에서 ?? 파이프라인의 변수를 서비스에 연결하는데 사용합니다.  예).  서비스는 파이프라인 변수 BuyersTotal과 동인한 OrderTotal이라는 값을 예상합니다(즉, 동일한 데이터에 대해 단순히 다른 이름) BuyersTotal 값을 OrderTotal값으로 사용하려면 ?를 사용하여 파이프라인 변수를 서비스에 "연결"합니다.

런타임 서버는 서비스를 실행하기 전에 원본 변수(BuyersTotal)의 값을 대상 변수(OrderTotal)로 복사합니다.
![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/Mapping_LinkingPipelineSvcInput.png)

서비스가 생성하는 모든 출력 변수는 자동으로 파이프라인에 배치됩니다. Pipeline In 단계의 변수를 입력 변수에 연결할 수가 있는 것처럼 서비스의 출력을 Pipeline Out의 다른 변수에 연결할 수 있습니다.

예). TransNumber라는 변수는 TransactionRecord라는 문서의 Num 필드에 연결 됩니다. 런타임 서버는 TransNumber의 값을 Num에 복사하고 TransNumber과 Num은 Flow의 다음 Service에서 사용가능

![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/Mapping_LinkSrvOutputPipeline.png)

* 변수 사이의 링크 생성
  * 연결하려는 변수는 source 입니다 . 예를 들어 파이프라인 입력 의 변수를 서비스 입력 의 변수에 연결하면 파이프 라인 입력 변수가 소스입니다. Service Out 의 변수를 Pipeline Out 의 변수에 연결하면 Service Out 변수가 소스입니다.
  * 연결하려는 변수는 target 입니다 . 예를 들어 파이프라인 입력 의 변수를 서비스 입력 의 변수에 연결하면 서비스 입력 변수가 대상이 됩니다. Service Out 의 변수를 Pipeline Out 의 변수에 연결하면 Pipeline Out 변수가 대상이 됩니다.
  * Service In 변수는 배열 인덱싱을 사용하거나 변수에 대한 링크에 조건을 배치하는 경우에만 둘 이상의 링크의 대상이 될 수 있습니다.
  * 변수를 서로 연결하여 소스 변수 에서 대상 변수로 데이터를 복사합니다. (단, 문서는 참조로 복사됩니다. 자세한 내용은 [What Happens When Integration Server Executes a Link? 를](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.map.link.executes.html#wwID0E25HQB "통합 서버가 링크를 실행하면 어떻게 됩니까?") 참조하십시오 .)
  * 대상 변수는 하나의 소스 변수에만 연결할 수 있습니다. 대상 변수에 대한 링크를 그린 후에는 대상 변수에 대한 다른 링크를 그릴 수 없습니다. (이 규칙에 대한 두 가지 예외는 배열 변수 및 조건부 링크와 관련이 있습니다. 배열 변수 연결에 대한 자세한 내용은 [파이프라인에서 배열 변수 연결을](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.map.link.arrays.html#wwID0EBCJQB "파이프라인에서 배열 변수와 연결") 참조하십시오 . 변수 간 연결에 조건을 배치하는 방법에 대한 자세한 내용은 [조건부로 변수 연결을](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.map.link.conditional.html#wwID0E5ZKQB "변수를 조건부로 연결하기") 참조하십시오 .
  * 이미 변수에 값을 할당한 경우 변수에 대한 링크를 생성할 수 없습니다.
  * 링크가 실행된 후 소스 및 대상 변수가 모두 파이프라인에 존재합니다. 대상 변수는 소스 변수를 대체하지 않습니다.
  * 변수에 고정 null 또는 기본값이 할당된 경우 변수에 대한 링크를 생성할 수 없습니다. Designer는![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/fixed.gif) 변수 아이콘 옆에 있는 기호를 사용하여 변수에 다른 변수에 연결하여 재정의할 수 없는 고정 값이 있음을 나타냅니다.
* 통합 서버가 링크를 실행하면 어떻게 됩니까?
  * 런타임에 변수 사이의 링크를 실행할 때 통합 서버는 다음 중 하나를 수행
  * 소스 변수의 값으 ㄹ대상 변수에 복사합니다. 예). 소스 문자열 변수를 대상 문자열 변수에 링크하면 통합 서버는 소스문자열의 값을 대상 문자열에 복사합니다. 이를"값으로 복사"라고 함
  * 소스 변수에 대한 참조를 생성하고 참조를 대상 변수의 값으로 사용 예). 소스 문서와 대상 문서 사이의 링크를 실행할 때 통합 서버는 소스 문서 값에 대한 참조를 작성하고 참조를 대상문서의 값으로 사용합니다. 이를 "참조에 의한 복사"라고 함
  * 통합 서버는 소스 또는 대상 변수가 문자열인 경우 값으로 복사합니다(이 동작에 대한 예외는 문자열에서 개체로의 링크를 실행 할 때 통합 서버가 참조로 복사하게 되는 것)
  * 다른 모든 유형의 변수 간에 링크를 실행할 때 통합 서버는 참조로 복사합니다.  (이 동작에 대한예외는 문자열에서 개체로의 링크를 실행할 때 통합 서버는 소스 분서 값에 대한 참조를 작성하고 참조를 대상 문서의 값으로 사용합니다. 이를 "참조에 의한 복사")
  * 다른 모든 유형의 변수간에 링크를 실행할 때 통합 서버는 참조로 복사하면 런타임에 링크를 실행하는 데 필요한 메모리와 시간이 크게 줄어듭니다.
  * 참조로 값을 복사하면 후속 Flow Stepp에서 소스 변수 값의 사본이 포함되어 있지 않습니다. 
  * [참조에 의한 복사의 예](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.map.link.executes.copyRef.html#wwconnect_header)
  * [파이프라인 값 덮어쓰기 방지](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.map.link.executes.overwrite.html#wwconnect_header)
* 문서 및 문서 목록 변수에 연결
  * 파이프라인에서 문서 변수로 작업할 때 소스 변수를 문서 변수 또는 변수의 하위에 연결할 수 있다.
  * 문서(또는 문서목록) 와 해당 하위 항목은 모두 대상이 될 수 없습니다. 문서 또는 문서 목록이 링크의 대상이 된 후에는 해당 하위 항목이 링크의 대상이 될 수 없습니다.
  * 문서 또는 문서 목록의 하위 번수가 링크의 대상이 된 후에 상위 문서 또는 문서 목록이 링크의 대상이 된 후에는 해당 하위 항목이 링크의 대상이 될 수 없습니다.
  * 문서 변수에서 다른 문서 변수로 연결하면 소스 문서 변수의 구조가 대상 문서 변수의 구조를 덮어씁니다.
  * 문서 목록의 크기가 다른 경우 중첩된 문서 목록을 대상 문서 목록에 연결할 수 없습니다. 중첩된 문서 목록은 상위 문서 목록 내에 포함된 문서 목록입니다. 문서 목록은 목록 내의 항목 수가 다른 경우 크기가 다른 것으로 간주됩니다. 소스 문서 목록에서 대상으로 값을 이동해야 하는 경우 LOOP 흐름 단계를 사용하여 소스에서 대상으로 값을 하나씩 할당하는 사용자 코드를 생성합니다.
  * 문서 참조 또는 문서 참조 목록이 데이터 유형이 동일하고 이름이 동일한 변수를 포함하는 IS 문서 유형을 참조하고 동일한 이름의 변수에 값이 지정되거나 다른 변수에 링크되는 경우 통합 서버는 문서 참조의 순서를 유지하지 않을 수 있습니다 . 서비스가 실행될 때 파이프라인의 문서 내용. 예를 들어 통합 서버는 문서 끝에서 모든 동일한 변수를 그룹화할 수 있습니다. 문서 내용의 순서 변경을 방지하려면 동일한 이름의 변수에 기본값을 설정하십시오. 이렇게 하려면 변수에 값을 연결하거나 할당하려는 단계 앞에 서비스에 MAP 단계를 삽입합니다. MAP 단계의 Pipeline Out에서 Document Reference 변수를 선택하고![](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/images/map_default.gif)파이프라인 보기 도구 모음에서 Enter Input for 대화 상자에서 동일한 이름의 변수에 기본값을 할당합니다.
* 다른 데이터 유형의 변수 연결
  * 파이프라인 보기에서 서로 다르지만 호환되는 데이터 유형을 서로 연결할 수 있습니다. 예를 들어 AccountNumber 라는 문자열 값을 Accounts 라는 문자열 목록에 연결할 수 있습니다 . 런타임에 서버는 AccountNumber 의 데이터를 Accounts 에 연결하는 데 필요한 구조 변환을 자동으로 수행합니다 . (이 경우 변환 결과 단일 요소 문자열 목록이 생성됩니다.) 서로 다른 데이터 유형을 서로 연결하여 구조 변환을 수행할 수 있습니다.
  *  모든 데이터 유형을 서로 연결할 수 있는 것은 아닙니다. 예를 들어 문서(IData 개체)를 문자열에 연결할 수 없습니다. 두 데이터 유형이 호환되지 않는 경우 Designer는 이들을 서로 연결하는 것을 허용하지 않습니다.
  * 동일한 기본 유형 의 다른 변수에만 변수를 연결할 수 있습니다 . 기본 유형은 모든 차원이 제거된 변수의 데이터 유형을 나타냅니다. 예를 들어 문자열 목록 또는 문자열 테이블의 기본 유형은 문자열입니다. 이 규칙에 대한 두 가지 예외는 다음과 같습니다.
    * 모든 변수는 개체 또는 개체 목록 변수에 연결할 수 있습니다.
    * 개체는 모든 데이터 형식에 연결할 수 있습니다.
  *  할당된 Java 클래스로 제한되는 개체 및 개체 목록 변수는 동일한 Java 클래스의 다른 개체 및 개체 목록 변수 또는 알 수 없는 유형의 개체 및 개체 목록 변수에만 연결되어야 합니다. Designer가 서로 다른 Java 클래스가 있는 제한된 개체 간의 링크를 허용 하더라도 런타임 결과는 정의되지 않습니다. 객체에 대한 Java 클래스 지정에 대한 자세한 내용은 [객체에 대한 Java 클래스를](https://documentation.softwareag.com/webmethods/compendiums/v10-3/C_B2B_Integration/b2b-integration-compendium/esb.dataTypes.javaClasses.html#wwID0EEZVZB "개체에 대한 Java 클래스") 참조하십시오 .
  * 스칼라 변수와 배열 변수를 연결할 때 연결할 배열 변수의 요소를 지정할 수 있습니다. 스칼라 변수는 String, Document 및 Object와 같은 단일 값을 보유하는 변수입니다. 배열 변수는 문자열 목록, 문자열 테이블, 문서 목록 및 개체 목록과 같이 여러 값을 보유하는 변수입니다. 예를 들어 문자열을 문자열 목록의 두 번째 요소에 연결할 수 있습니다. 또는 문자열 목록의 두 번째 요소를 문자열에 연결할 수 있습니다.
  * 스칼라 변수와 배열 변수를 연결하고 연결하려는 배열 변수의 요소를 지정하지 않은 경우 Designer는 기본 동작을 사용하여 대상 변수의 값을 결정합니다.
* 파이프라인에서 배열 변수와 연결
* 변수 사이의 링크 삭제
* 변수를 조건부로 연결하기
	
https://techdocs.broadcom.com/kr/ko/ca-enterprise-software/it-operations-management/application-performance-management/10-5/345392263/345392665/345392690.html
