## Contact Center > Online Contact > API 가이드 > Hidden 값 접수 API 가이드

### API 인증방법 설명
#### Security Key
조직 내 서비스는 유일한 Security Key를 가지고 있으며, Security Key를 통해 API로 전달하는 데이터가 암호화됩니다.
사용하시는 서비스의 Security Key는 Online Contact → 서비스 관리 → 인증 → OPEN API 탭에서 확인하실 수 있습니다. 
![](http://static.toastoven.net/prod_contact_center/1.1-(1).png)

#### 인증 Header
모든 Request Header에 반드시 아래 값을 설정해야 합니다.
- Authorization: Security Key로 생성된 인증 스트링
- X-TC Timestamp: 현재 UTC 시간 값 {new date().getTime()}
- OUCODE: 유저 code (필수 아님, 설정하지 않을 경우 디폴트 값이 owner)

#### 인증 스트링 생성 방법
HmacSHA1를 사용한 암호화, (조직ID + request URI + 파라미터 값 + 현재UTC시간 값）스트링에 대해 암호화를 하는 방법이 있습니다.

##### Java 예시
```Java
String URL = "https://triple.oc.toast.com/triple/hc/openapi/v1/addition.json";
String paramContent = "XXXXXXX";
Integer paramVisible = 1;
String organizationId = "WopqM8euoYw89B7i"; // 조직ID는 TOAST → CONSOLE → 조직 설정 탭에서 확인
String securityKey = "3df6370bf3a64936b5e611dfc6f74550"; // 서비스 관리 → 인증 → OPEN API 탭에서 확인
String uri = "/triple/hc/openapi/v1/addition.json"; // request uri
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
sb.append(paramContent).append("&").append(paramVisible); // 파라미터 값은 파라미터명으로 오름차순，파라미터 값 사이 & 분리
Date date = new Date();
sb.append(date.getTime());
SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA1");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));
```

### 헬프센터 지정 데이터 추가
#### 인터페이스 설명

|인터페이스 명                       |헬프센터에 지정 데이터 추가         |담당자 이름                 |赫荣刚                  |
----------------------------------- | -------------------------------- | --------------------------|-------------------------|
|프로토콜                            |HTTPS                             |담당자 이메일               |he.ronggang@nhn-st.com |
|호출방향                            |POST                              |담당자 부서                 |OC TF                  |
|인코딩                              |UTF-8                             |결과 형식                   |JSON                   |
|URL                                 |https://{domain}.oc.toast.com /{serviceId}/hc/openapi/v1/addition.json|  |             |
|URL (개발)                           |https://{domain}.alpha-oc.toast.com /{serviceId}/hc/openapi/v1/addition.json||        |
|인터페이스 설명                       |추가 필요한 고객정보를 DB에 저장|           |                                            |

#### 요청 파라미터

|명칭                   |변수                  |데이터 타입              |필수             | 설명                         |
|-----------------------|---------------------|------------------------|-----------------|------------------------------|
|서비스 ID               |serviceID            |String                 |O               |URL PATH 내에 설정한 {serviceId}|
|                       |content              |String                  |O               |추가 고객정보                   |
|노출 여부|visible|int|X|문의 내용 입력박스에 노출 여부 (1: 노출, 0: 숨김, 기본 값: 0)|

#### 결과 데이터
|명칭|변수|데이터 타입|필수|설명|
|---|----|---------|---|------|
|result.content|additionID|string|O|생성된 ID|

#### Response Body

````
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": ef1bd956
  }
}
````
