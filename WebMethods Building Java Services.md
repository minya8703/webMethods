# webMethods Building Java Services

## Java 서비스 구축 개요
* 통합 서버에는 Designer 로컬 작업공간에서 사용되는 Java컴파일어와 동일한 버전의 Java컴파일러가 있어야한다,
* 디자이너는 Java서비스가 상주할 통합 서버에 연결되어야 합니다.

## Java Service 편집기
* Source Tap
  *  Java서비스에 대한 코드가 포함되어있습니다.
  * 표준 Eclipse Java 편집기를 확장하는 소스 탭에서 Java서비스에 대한 코드를 지정. Eclipse Java편집기는 소스 파일이 로컬 작업 공간에 있어야하므로 Designer도 소스 파일이 로컬 작업 공간에 있어야 합니다. 이를 달성하기 위해 Designer는 Java 서비스를 지원하기 위한 확장이 포함된 프로젝트인 서비스 개발 프로젝트에 Java클래스를 추가합니다. 
  * Eclipse Java편집기의 전체 기능(예:소스 서식 지정, 코드 완성 등)을 사용할 수 있습니다. 그러나 Eclipse Java편집기와 달리 Designer Java서비스 편집기는 구조적 손상을 방지하기 위해 필요한 코드가 포함된 Java서비스 섹션을 보호합니다. 서비스에 다음 새로 생성된 서비스에 대해 소스 탭의 내용입니다.

|내용|소스|
|---|---|
|자바 패키지 정의|패키지 주문.주문 상태|
|여기에 추가 가져오기 추가|import com.wm.data.*; <br> import com.wm.util.Values; <br> import com.wm.app.b2b.server.Service<br>import com.wm.app.b2b.server.ServiceException;|
|클래스 정의|public final class orderStatus_checkStatus_SVC|
|여기에 확장 및 구현 추가|  |
|기본 메서드 정의|{  <br>/**  <br>&nbsp;* Java 서비스의 기본 메소드 <br>*  <br>* @param pipeline  <br>* IData 파이프라인  <br>* @throws ServiceException  <br>*/  <br>public static final void  <br>orderStatus_checkStatus(IData pipeline)  <br>throws ServiceException { |
|여기에 기본 Java 서비스 메서드의 소스 코드 추가|  |
| | }<br><br> // --- <<IS-BEGIN-SHARED-SOURCE-AREA>> ---|
|여기에 공유 코드 추가| <br>// --- <<IS-END-SHARED-SOURCE-AREA>> ---<br> }|
|최종 "}"| } |
* Input/Output Tap
  *  Java서비스의 입력 및 출력 서명이 포함되어 있습니다. 
* Logged Fields Tap
  *  통합 서버가 데이터를 기록하는 입력 및 출력 매개변수를 나타냅니다. 
* Comments Tap
  *  Java 서비스에 대한 주석 또는 참고 사항이 포함되어 있습니다.
## Java Service 입력 및 출력에 IData 개체 사용
* IData 개체는 Java서비스가 서비스 입력 및 출력에 사용하는 범용 컨테이너입니다. Java서비스 메서드 서명은 IData 유형의 인수를 정확히 하나만 취하며 동일한 IData 개체에 서비스의 출력이 포함됩니다. IData 개체이는 서비스가 작동하는 키/값 쌍의 정렬된 컬렉션이 포함되어 있습니다. 키/값 쌍의경우
  * 키는 문자열이어야 합니다.
  * 값은 모든 Java 객체(IData 객체 포함) 일 수 있습니다.
* 입력 값 가져오기 및 설정을 위한 샘플 코드
  * Java 서비스는 공개적이고 정적인 메소드입니다. com.wm.data.IData의 단일 인스턴스를 입력으로 사용하고 동일한 IData 개체에 출력을 배치해야 합니다. 다음 코드는 샘플을 보여줍니다.
```java
public final static void myservice (IData pipeline)  
	throws ServiceException  
		{  
	return;  
}
```
  * Java 서비스가 호출되면 통합 서버는 IData오브젝트를 여기에 전달합니다. 서비스는 IData개체 내의 키/값 쌍에서 필요한 입력 값을 가져와야 합니다. 다음 샘플 코드는 IDataCursor클래스의 메서드를 사용하여 배치하고 getValue 메서드를 사용하여 IData 개체에서 myVariable 입력 변수의 입력 값을 가져 온다.
```java
public final static void myservice (IData pipeline)  
	throws ServiceException  
{  
	IDataCursor myCursor = pipeline.getCursor();  
	if (myCursor.first( "inputValue1" )) {  
		String myVariable = (String) myCursor.getValue();  
		.  
		.  
}  
	myCursor.destroy();  
	.  
	.  
	return;  
}
```
서비스는 입력 값에 사용된 것과 동일한 IData개체에 추가하여 출력을 반환. 모든 서비스의 출력은 IData 개체에 기록 되어야 한다. 
예:
```java
public final static void myservice (IData pipeline)  
	throws ServiceException  
	{  
		IDataCursor myCursor = pipeline.getCursor();  
		if (myCursor.first( "inputValue1" )) {  
			String myVariable = (String) myCursor.getValue();  
			.  
			.  
		}  
		myCursor.last();  
		myCursor.insertAfter( "outputValue1", myOutputVariable );  
		myCursor.destroy();  
		return;  
}
```

  * IData 개체 만들기
  IDataFactory 클래스를 사용하여 IData개체를 만듭니다.
  예:
  ```java
public final static void myservice (IData pipeline)  
	throws ServiceException  
	{  
		myIDataObject = IDataFactory.create();  
		IDataCursor myCursor = myObject.getCursor();  
		myCursor.insertAfter("VA", new Double("0.045"));  
		myCursor.insertAfter("MD", new Double("0.05"));  
		myCursor.insertAfter("DE", new Double("0.0"));  
	return;  
}
  ```
* IData 개체에서 요소 가져오기 및 설정
  * IDataCursor 클래스를 사용하여 IData요소(즉, 키/ 값 쌍)에서 값을 가져오고 값을 설정합니다. IData 요소에서 값을 가져오거나 설정하려면 두 단계가 필요합니다.
  * 먼저 가져오거나 설정하려는 IData요소에 커서를 놓습니다. IDataCursor 클래스에서 커서를 IData 개체의 첫 번째, 마지막 또는 다음 요소에 배치하는 것과 같은 기본 커서 작업을 수행하기 위한 메서드가 포함되어 있습니다.
  * 커서 위치를 지정한 후 getValue 또는 setValue 메소드를 사용하여 각각 요소의 값을 읽거나 씁니다. 이 클래스는 새 요소를 삽입하고, 키 이름을 가져오고, 요소를 삭제하기 위한 메서드도 제공
