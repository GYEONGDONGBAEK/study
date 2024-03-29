# Section 8-1. HTTP 헤더2 - 캐시와 조건부 요청-(1)

---

## 캐시

클라이언트가 서버에 요청하는 자원(resource)은 단순한 텍스트부터, 이미지, 영상, 파일까지 다양하다. 그 중에서는 용량이커서 큰 네트워크 비용을 부담해야하는 자원들이 있고, 변경 가능성이 잦지 않은 자원들이 있다.

이런 자원들을 매 번 요청시마다 새로 다운받는건 큰 네트워크 비용 부담이다.

그래서 나온 것이 캐시라는 개념으로 이런 자원들에 대해 브라우저 캐시에 우선 저장해두고, 해당 자원이 변경되지 않았다면, 서버에서 다운받지않고 브라우저 캐시에 저장해놓은 자원을 다시 사용한다는 개념이다.

### 캐시가 없을때

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/fc5a6a05-4d31-4d32-8712-30fac400d20c">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/d94a9ade-e34e-4a52-adf7-8992a09973c4">

- **데이터가 변경되지 않아도** 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다.
- 인터넷 네트워크는 매우 느리고 비쌈 (pc의 메모리나 하드디스크에 비해 상대적으로)
- 브라우저의 로딩 속도가 느리다.
- **이로 인해 느린 사용자 경험이 발생한다.**

### 캐시 적용 후

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/75a0bfc2-9524-4dc4-9f40-f859f47a2ff7">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/f64ffa7c-01e2-452f-8854-3f98c5939ab3">

이렇게 캐시를 적용하게 되면, 일정 시간 동안 같은 요청을 보낼 때, 네트워크를 통해서 결과를 받아오지 않고, 브라우저 캐시에 접속해서 결과를 받아오기 때문에 이 과정에서 시간이 크게 단축된다.

- 캐시 덕분에 캐시 가능 시간동안 **네트워크를 사용하지 않아도** 된다.
- 비싼 **네트워크 사용량을 줄일 수** 있다.
- 브라우저 로딩 속도가 매우 빠르다.
- **빠른 사용자 경험**을 만들어준다.

웹 브라우저 이용시 한 번 들어갔던 사이트를 재방문할 때 매우 빠른 이유는 캐시를 사용한 덕분이다

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/f480822a-6cea-4574-8cc2-7ed4f9a73633">

이러한 경우 다시 서버에 요청을 통해 받아와 기존의 유효 시간이 지난 캐시를 새로운 데이터로 덮어씌워서 초기화시킨다.

### **캐시 시간 초과**

- 캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다.
- 이때 다시 네트워크 다운로드가 발생한다.

---

### **검증 헤더와 조건부 요청 1**

캐시의 시간이 초과되어 더 이상 유효하지 않은 경우 새롭게 서버에 접속해 데이터를 받아와 캐싱해야 하는데, 이를 조건에 따라서 갱신하기 위해 사용하는 방법이다.

### **캐시 시간 초과**

캐시 유효 시간이 초과해서 서버에 다시 요청하면, 다음 두 가지 상황이 나타난다.

1. 서버에서 기존 데이터를 변경했다.
2. 서버에서 기존 데이터를 변경하지 않았다.

 

**캐시 만료후에도 서버에서 데이터를 변경하지 않는 경우**

- 생각해보면 데이터를 전송하는 대신 저장해 두었던 캐시를 재사용할 수 있다.
- 단, 클라이언트의 데이터와 서버의 데이터가 같다는 사실을 확인할 수 있는 별도의 방법이 필요하다. ⇒ **검증 헤더** 추가

### 검증 헤더

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/2aa3abab-6a0d-4ec6-9364-ce353cd15ce2">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/480f1728-5385-4874-aa05-a11869e13bbb">

캐시에 **유효한 시간 + 데이터 최종 수정일** 정보를 함께 보관

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/59f9dc46-701f-48d8-a3ad-8730245b922c">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/afa4e3d1-17c2-4b2b-abf2-6e19b2b846b5">

서버에서 **if-modified-since header**에 작성된 최종 수정일 정보를 이용해 데이터가 수정되었는지 여부를 판단하고

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/cdcfb035-9de0-4b7d-b52c-fee1bac65b9f">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/c81a047b-9aba-41c6-b42a-fa55ca0e8cbb">

**304 Not Modified**를 이용하면, HTTP Body를 생략하고 response message를 전송하는 구조로 동작해서, 기존의 **1.1M**의 네트워크 사용량을 차지하던 방식을 **0.1M**만 점유하도록 대체할 수 있게 된다.

304 Not Modified response를 받은 client는 cache에 있던 데이터의 유효 시간을 갱신(60초로)해서 다시 사용할 수 있게 된다.

### **조건부 요청1 - 정리**

이 상황에서는 검증 헤더(Last-Modified)와 조건부 요청(if-modified-since)를 같이 사용하여 문제를 해결한 상황이다.

- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않았으면
- 304 Not Modified + 헤더 메타 정보만 응답 (body X)
- 클라이언트는 서버가 보낸 응답 헤더의 정보로 캐시의 메타 정보(최종 수정일, 유효 기간 등..)를 갱신한다.
- 클라이언트는 캐시에 저장되어 있는 **데이터를 재활용**할 수 있게 된다.
- 결과적으로 네트워크 다운로드가 발생하기는 하지만, 용량이 적은 **헤더 정보만 다운로드**하면 되도록 변화
- **매우 실용적인 해결책!**