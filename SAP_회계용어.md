
![SAP Easy Access 2023-08-03 오후 1_10_37](https://github.com/minya8703/webMethods/assets/97384342/21ecd8ae-259a-4f44-b8fa-2e8ecf80e971)


- GL : General Ledger (총계정원장 : 기업 회계상의 모든 계정과목들을, 한군데에 빠짐없이 수록한 장부 또는 간단히 원장이라고도 하며 대차대조표와 손익계산서는 총계정원장을 근거로 하여 만들어짐)
- AR : Account Receivable(매출채권 : 기업이 상품을 매출하는 과정에서 발생한 채권으로, 외상매출금과 받을어음을 말하는 것)
- AP : Account Payable(매입채무 : 미지급금은 회사의 대차대조표에 부채로 표시되는 공급자에게 기업이 갚아야 할 돈입니다. 이는 공식적인 법률 문서에 의해 생성된 부채인 지급 어음 부채와 구별됩니다.)
 -AA : Asset Accounting(자산회계 : 재무 회계 모듈(FI)에서 자산회계는 총계정 원장에 대한 보조원장의 역할을 하며,  자산의 취득, 이동, 재평가, 매각, 폐기, 가계정, 세무관리 등의 기능을 수행한다.)


  ## Organization Structure
![image](https://github.com/minya8703/webMethods/assets/97384342/4b9946e6-fbcd-472c-8e01-e78a8bb01a50)


회계마스터
General Ledger Account (총계정원장)
Customer Account(채권)
Vendor Account(채무)
Asset Account(고정자산)
Bank Key(은행)

## Reconciliation Account (조정계정)
- 회계가 GAAP (General Accepted Accounting Principle) 에 어긋나지 않도록 이루어 지는가를 결정하는 절차. G/L 계정 잔액이 전기 된 거래의 총합과 비교된다. 고객계정의 잔액과 구매처 계정잔액이 각각 채권잔액,채무잔액 및 전기된 거래와 비교된다.
