## Contact Center > Online Contact > API 가이드 > Open API

### API 인증방법 설명
#### Security Key
##### 조직 레벨
TOAST CONSOLE에서 생성하신 조직 별로 유일한 Security Key를 보유하고 있습니다. Security Key를 통해 API로 전송되는 데이터를 암호화 처리할 수 있으며, 조직 관리와 관련된 Open API를 호출할 수 있습니다. (서비스 등록, 수정, 삭제 등) 사용하고 계시는 조직의 Online Contact에 접속하신 후 전체 관리 → SSO 로그인 → API Key에서 조직 레벨의 Security key를 확인하실 수 있습니다.
![](http://static.toastoven.net/prod_contact_center/dev1.png)

##### 서비스 레벨
하나의 조직에서 여러 개의 서비스를 생성하실 수 있으며, 생성하신 각 서비스 별로 유일한 Security Key를 보유하고 있습니다. Security Key를 통해 API로 전송되는 데이터를 암호화 처리할 수 있으며, 서비스 관리와 관련된 Open API를 호출할 수 있습니다. (티켓 관리, FAQ 등) 서비스 추가 API(/openapi/v1/admin/service/add.json)를 통해 서비스 추가가 가능하며, 서비스 추가 후 리턴 결과 값에서 서비스 레벨의 Security Key를 취득할 수 있습니다. 또한 사용하고 계시는 조직의 Online Contact에 접속하신 후 security key를 확인하고자 하는 서비스를 선택, 서비스 관리 → 인증 → OPEN API → API Key에서도 서비스 레벨의 Security Key 취득이 가능합니다.
![](http://static.toastoven.net/prod_contact_center/dev2.png)

###### Response Body
```JSON
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":{
            "serviceId":"GameBaseService",
            "name":"GameBaseServiceAPI",
            "active":true,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "createdDt":1586745222442,
            "updatedDt":1586745222442,
            "securityKey":"cfdc25cc7ef54759ad29e6345213f2ed"
        }
    }
}
```

#### 인증 Header
각 Request Header에 아래의 값들을 반드시 설정해야 합니다.
- Authorization：Security Key를 통해 생성된 인증 문자열
- X-TC-Timestamp：현재 UTC 시간 값{new Date().getTime()}
- OUCODE：유저 code（필수 아님，설정하지 않을 경우 기본 값은 Owner）

#### Authorization 문자열 생성 방법
HmacSHA256로 암호화하거나, (조직ID + request URI + 파라미터 값 + 현재 UTC시간 값）문자열에 대해 암호화하여 Authorization 문자열을 생성하실 수 있습니다.

##### Java 예시
```Java
String URL = "http://nhn-cs.alpha-oc.toast.com/openapi/v1/admin/service/add.json";
String organizationId = "WopqM8euoYw89B7i"; // 조직ID
String securityKey = "0983e74b682b416684d2da59347aec82"; //조직 API Key
String uri = /openapi/v1/admin/service/add.json"; // request uri
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
sb.append("GameBaseService").append("&").append("GameBaseServiceAPI").append("&").append("ko").append("&").append("Asia/Seoul");// 파라미터 값은 이름 오름차 순, 파라미터 사이는 &로 분리
Date date = new Date();
sb.append(date.getTime());
SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));
```

- request body가 있을 경우 파라미터 뒤에 body 문자열 추가
- 파일 첨부 시, 파일의 MD5는 파라미터 값으로 인증 문자열에 추가
- Security Key
	- /openapi/v1/admin/* 형태의 API 호출 시 조직 레벨 Security Key 사용
	- {serviceId}/openapi/v1/* 형태의 API 호출 시 ，서비스 레벨 Security Key 사용

### 공통 리턴 결과
|명칭	|변수|	데이터 타입	|필수|	설명|
|-----|---|--------------|----|------|
|Header	|resultCode	|VARCHAR(2)	|O	|리턴 결과 Code , 정상은 200|
|	|resultMessage|	VARCHAR(50)|	O|	리턴 오류 메시지|
|	|isSuccessful|	Boolean|	O|	실행 결과(성공：true ，실패：false)|
|Result|	contents|	JSON|	X|	목록 결과 내용|
|	|content|	JSON|	X|	상세 결과 내용

#### 리턴 Code 정보	
- 200 :SUCCESS	
- 400 :Bad Request	
- 403 : Forbidden	
- 404 : Not Data Found	
- 500 : Server Error	
- 9007 : 관련된 데이터가 이미 존재	
- 9005 : 관련된 데이터가 없음	

