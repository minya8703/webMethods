# Integration Server
![image](https://github.com/minya8703/webMethods/assets/97384342/42a78218-76db-4ec7-b4df-40221723e124)
IS 환경에서 관리자는 webMethods Integration Server의 설치, 구성 및 유지 관리를 담당
## 1. Server
![image](https://github.com/minya8703/webMethods/assets/97384342/e087023e-e460-4cc6-a0e7-e1956a270a22)
### 1-1.Scheduler
- 서버의 스케줄링 기능을 사용하여 지정한 시간에 서비스가 실행되도록 한다.

![image](https://github.com/minya8703/webMethods/assets/97384342/38d4ce1f-5919-481c-a42f-ce6676370201)
#### ■ Pause Scheduler (currently Running)
  - 현재 실행중인 스케줄러 일시 정지 버튼
  - 링크를 누르면 아래와 같이 표시

![image](https://github.com/minya8703/webMethods/assets/97384342/1d0c0e3d-9eef-4659-b698-a7b9fd59bb0c)

#### ■ View System Tasks
그림 추가 필요
  - 예약된 각 작업의 이름, 서버가 작업을 실행할 다음 날짜 및 시간, 서버가 적업을 실행하는 빈도등이 표시
  - Session, Listener log 등 같은 시스템 스케줄러

#### ■ Create a Scheduled Task
![192 168 110 205_5097_](https://github.com/minya8703/webMethods/assets/97384342/897e66c3-9733-4273-abfb-171c1af10dba)

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
![image](https://github.com/minya8703/webMethods/assets/97384342/29b5db3f-0642-4d5b-bdb5-2c85f37b773b)
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
## 3. Packages
## 4. Solutions
## 5. Adapters
## 6. webMethods Cloud
## 7. Security
## 8. Settings
## 9. Commons
