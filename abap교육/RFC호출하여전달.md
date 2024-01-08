
# RFC호출하여전달

<br> https://abapbbane.tistory.com/15
<br> https://m.blog.naver.com/yurimyang/222466782105
### RFC Connections 작성.
```

Include 문 생성

REPORT  ZF***** MESSAGE-ID ICC-KR.

INCLUDE ZF*****TOP.  -- 글로벌 데이터를 생성
INCLUDE ZF*****TOP_ALV. -- 
INCLUDE ZF*****F01. -- SUBROUTINE 사용시(PERFORM문)
INCLUDE ZF*****O01.
INCLUDE ZF*****I01.
INCLUDE ZF*****ALV.
INCLUDE ZF*****CLS.
INCLUDE ZF***RCOMM001.

```
