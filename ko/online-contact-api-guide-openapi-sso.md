## Contact Center > Online Contact > API 가이드 > SSO 로그인
### 개요
SSO 로그인은 사용자 시스템과 상담 시스템을 연동하는 기능이며, 원격인증은 API Key를 통해 진행됩니다.
API Key는 임의로 생성되는 유일한 문자열이며 원격로그인을 통해 상담시스템에 접속할 수 있도록 하는 안전한 인증방식입니다.

### 프로세스
1. 고객이 문의 접수, 채팅 상담 등을 위해 상담 시스템에 접속
2. 고객이 상담 시스템에서 로그인 시도 시 상담 조직에서 설정해 둔 SSO 로그인 화면으로 이동
3. Online Contact의 로그인 화면이 아닌, 제공 중인 시스템의 로그인 화면에서 로그인
4. 로그인 성공후, 유저 정보와 API Key를 통해 토큰 생성
5. 유저 정보와 토큰을 상담 시스템으로 전달
6. 상담 시스템에서 토큰에 대해 인증, 성공후 고객 로그인 진행
7. 로그인 전 화면으로 이동（returnUrl）

### SSO 로그인 설정
#### SSO 로그인 등록
![](http://static.toastoven.net/prod_contact_center/dev3.png)
Online Contact 접속 후, 전체 관리 → SSO 로그인 메뉴에서 SSO 로그인을 먼저 등록합니다. SSO 로그인 URL, 로그인 상태 URL을 입력해주세요.
SSO 로그인을 등록하신 후에 API Key를 복사해주세요. 원격로그인 API 호출 시 인증 토큰으로 사용됩니다.

#### SSO 로그인 활성화 및 지정
![](http://static.toastoven.net/prod_contact_center/dev4.png) 
서비스 관리 → 인증 → SSO 로그인 탭에서 SSO 로그인의 활성화 및 비활성화가 가능하며, 활성화하셨을 경우 선택하신 서비스에 지정하실 SSO 로그인을 선택하실 수 있습니다.

### 인증토큰 생성
Token 생성 샘플은 아래와 같습니다. 파라미터 순서는 반드시 아래와 일치해야 하며, SSO 로그인 API Key를 확인해주세요.
```
private String getSHA256Token(String serviceId, String usercode, String username, String email, String phone,
        String returnUrl, Long time, String apiKey) throws Exception {
    StringBuilder sb = new StringBuilder();
    // Order by follow number:
    sb.append(serviceId); // 1
    sb.append("&");
    sb.append(usercode); // 2
    sb.append("&");
    if (StringUtils.isNotBlank(username)) {
        sb.append(username); // 3
        sb.append("&");
    }
    if (StringUtils.isNotBlank(email)) {
        sb.append(email); // 4
        sb.append("&");
    }
    if (StringUtils.isNotBlank(phone)) {
        sb.append(phone); // 5
        sb.append("&");
    }
    if (StringUtils.isNotBlank(returnUrl)) {
        sb.append(returnUrl); // 6
        sb.append("&");
    }
    sb.append(time); // 7

    SecretKeySpec signingKey = new SecretKeySpec(apiKey.getBytes("UTF-8"), "HmacSHA256");
    Mac mac = Mac.getInstance(signingKey.getAlgorithm());
    mac.init(signingKey);
    byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
    return new String(Base64.encodeBase64(rawHmac));
}
```

### SSO API
#### SSO 원격로그인 API (Client Side)
##### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/v2/enduser/remote.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/v2/enduser/remote.json		

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|SSO 원격로그인 API (Client Side)|HTTPS  |POST    |UTF-8|Redirect    |사용자 시스템에서 동적으로 form를 생성하여 브라우저에 반환하며, form은 자동으로 API에 form정보를 전달. API에서 전달된 form정보로 인증 후 성공시 로그인 Cookie 값 설정.|

##### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스ID	|service	|Varchar(50)	|O	|서비스 ID|
|유저ID	   |usercode	|Varchar(50)	|O	|유저ID，유일한 유저임을 표시|
|유저 명	  |username	|Varchar(50)	|X	|유저 명|
|유저 이메일 주소	|email	|Varchar(100)	|X	|유저 이메일|
|전화번호	        |phone	|Varchar(20)	|X	|전화번호|
|현재 시간의 timestamp	|time	|Long	|O	|호출 시간이 3분 초과시, 타임아웃 얼럿 출력.|
|인증 Token	           |token	|Varchar	|O	|아래 파라미터 값과 SSO API Key로 산출된 SHA256 (필수가 아닌 파라미터 값이 null 혹은 빈값일 경우 , 암호화 문자열에 추가 할 필요 없음.주의：문자열 중 각 값의 순서는 아래 예시에 지정된 순서와 일치해야 함.) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|
|리턴 화면 URL	|returnUrl	|Varchar	|X	|설정 및 로그인 성공시 해당 주소로 이동|

##### 결과 데이터
returnUrl 파라미터 존재시 지정된 returnUrl로 이동 , returnUrl 없을 경우 문자열 : SUCCESS 반환

##### 인증 Token 산출
 API 가이드 → SSO 로그인 → [인증토큰 생성](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-api-guide-openapi-sso/#_3) 항목을 참조해주세요.

#### SSO 원격로그인 API (Server Side)
##### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/api/v2/enduser/remote.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/api/v2/enduser/remote.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|SSO 원격로그인 API (Server Side)|HTTPS  |POST    |UTF-8|String   |사용자가 서버에서 직접 API 호출. API 로그인 성공 후 로그인 Cookie 값 설정.|
  
##### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|서비스ID	|service	|Varchar(50)	|O	|서비스 ID|
|유저ID	|usercode	|Varchar(50)	|O	|유저ID，유일한 유저임을 표시|
|유저 명	|username	|Varchar(50)	|X	|유저 명|
|유저 이메일 주소	|email	|Varchar(100)	|X	|유저 이메일|
|전화번호	|phone	|Varchar(20)	|X	|전화번호|
|현재 시간의 timestamp	|time	|Long	|O	|호출 시간이 3분 초과시, 타임아웃 얼럿 출력.|
|인증 Token	|token	|Varchar	|O	|아래 파라미터 값과 SSO API Key로 산출된 SHA256 (필수가 아닌 파라미터 값이 null 혹은 빈값일 경우 , 암호화 문자열에 추가 할 필요 없음.주의：문자열 중 각 값의 순서는 아래 예시에 지정된 순서와 일치해야 함.) SHA256Digest(service + usercode + username + email + phone + time)|

##### 결과 데이터
SUCCESS

##### 인증 Token 산출
 API 가이드 → SSO 로그인 → [인증토큰 생성](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-api-guide-openapi-sso/#_3) 항목을 참조해주세요.
 
#### SSO 로그인 URL (사용자)
##### 인터페이스 설명
|인터페이스 명|프로토콜|호출방향|인코딩|URL|URL(개발)|결과 형식|
|------------|--------|--------|------|--|----------|--------|
|SSO 로그인 URL|HTTPS|GET|UTF-8|사용자 제공|사용자 제공|Redirect|

##### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|---------|----|
|리턴 URL	|returnUrl	|Varchar	|O	|로그인 성공후 이동되는 URL|

##### SSO 로그인 기능 설명
###### 유저 미 로그인 상태
- ① 로그인 화면으로 이동
- ② 유저 로그인
- ③ 서비스 측의 서버에서 유저 로그인 처리 및 로그인 유저 관련 쿠키 생성
- ④ SSO 원격 로그인 API 호출

###### 유저 로그인 상태
- ① SSO 원격 로그인 API 호출

##### SSO 원격 로그인 API 호출 방법 설명
###### SSO 원격 로그인 (Client Side)
- ① 유저 정보와 API Key 기준으로 로그인 token 생성
- ② 유저 정보와 token을 브라우저로 리다이렉트
- ③ 화면에서 Form 작성, 상세한 파라미터는 [SSO 원격 로그인 API-1]() 참조
- ④ Form 제출
- ⑤ SSO 원격 로그인 API를 통해 유저 정보와 token 전송
- ⑥ 로그인 성공 후 {returnUrl}로 이동

###### SSO 원격 로그인 (Server Side)
- ① 유저 정보와 API Key 기준으로 로그인 token 생성
- ② 서버에서 "SSO 원격 로그인 API (Server Side)" 호출
- ③ API 호출 파라미터 (usercode와 time)을 returnUrl 뒤에 추가 
  - 예시) https://nhn-cs.alpha-oc.toast.com/multilanguage/hc/ticket/list/?usercode=xxxxxx@163.com&time=1566531359635
- ④ {returnUrl}로 이동

##### 인증 Token 산출
 API 가이드 → SSO 로그인 → [인증토큰 생성](https://alpha-docs.toast.com/ko/Contact%20Center/ko/online-contact-api-guide-openapi-sso/#_3) 항목을 참조해주세요.
 
#### SSO 로그인 상태 API (사용자)
##### 인터페이스 설명
|인터페이스 명|프로토콜|호출방향|인코딩|URL|URL(개발)|인터페이스 설명|결과 형식|
|------------|--------|--------|------|--|----------|--------|
|SSO 로그인 상태 API|HTTPS|GET|UTF-8|사용자 제공|사용자 제공|사용자가 쿠키 정보를 기준으로 로그인 여부를 확인 후 JSON 형식의 데이터를 리턴|JSON|

##### 요청 파라미터 정의 
- 없음

##### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|---------|----|
|javascript function	|login	|Boolean	|O	|로그인 상태. 로그인 ：true, 미로그인 ：false|
|유저 코드	|usercode	|Varchar(50)	|X	|유저 ID(유니크 값). 로그인 상태가 true 인 경우 유저코드는 필수|

##### Response Body
```
{
"login": "true",
"usercode":"usercodeXXX"
}

{
"login": "false",
"usercode": null
}
```
 
