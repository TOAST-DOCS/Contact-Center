## Contact Center > Online Contact > API 가이드 > 회원 연동 (POST)

## 회원 연동
### 개요
회원 연동 기능은 고객사에서 제공하는 서비스의 회원 인증을 온라인컨택의 헬프센터에서도 적용하여 회원 문의를 접수하고 접수한 문의 내역을 다시 확인 할 수 있도록 하기 위한 기능입니다.
회원 연동은 GET 방식과 POST 방식의 두 가지 타입으로 제공하고 있으며 연동을 위해서는 저희가 제공하는 개발 명세서에 따라 API를 개발하여 온라인컨택 회원연동 관리 화면에 등록해 주셔야 합니다.

#### POST 방식
- 연동하려는 서비스가 PC, MOBILE 플랫폼에서 모두 WEB 기반으로 제공 될 경우에 적합합니다.
- 서비스의 로그인 화면이 WEB URL 형태로 제공 되어야 사용 가능합니다.
- 개발 명세에서 CLIENT-SIDE, SERVICER-SIDE 세부적으로 2가지 타입을 제공합니다.

#### GET 방식
- WEB 기반의 로그인 화면이 없는 서비스의 경우 적합합니다.
- WEB 기반이 아닌 Native APP 서비스의 경우 적합한 연동 방식입니다.

### 프로세스 (POST 방식)
1. USER가 헬프센터 문의하기 또는 문의 내역 페이지 접속
2. 헬프센터 페이지에서 로그인 상태 URL 호출하여 로그인 상태 확인 (여기서 ‘로그인 상태 URL’은 고객사에서 아래 제공된 명세서에 따라 개발 후 OC 회원연동 화면에 등록해야 합니다.)
3. 로그인 상태 확인 후 결과에 따라
   - 3-1. ‘미로그인’ 상태일 경우 고객사 서비스의 ‘로그인 URL’ 호출하여 로그인 유도 (여기서 ‘로그인 URL’은 고객사에서 제공하고 있는 로그인 화면 URL이며 OC 회원연동 화면에 등록해야 합니다.)
   - 3-2. ‘로그인’ 상태일 경우 ‘원격 로그인 API’ 호출 하여 고객 정보를 OC헬프센터에 전달
4. 회원 문의 또는 문의 내역 페이지 접속합니다.

### 회원 연동 방법
![](http://static.toastoven.net/prod_contact_center/dev_post_(1).png)
1. 서비스 관리 > 헬프센터 > 회원 연동 접속
2. 회원 연동 활성화 항목에서 ‘활성화’ 버튼 클릭
3. 서비스 성격에 맞는 ‘로그인 타입’ 선택
4. 각 타입에 따라 필요한 API 개발 및 URL 설정 및 저장

## 개발 명세서
### 인증토큰 생성
Token 생성 샘플은 아래와 같습니다. 파라미터 순서는 반드시 아래와 일치해야 하며, 전체 관리 → SSO 로그인 메뉴에서 API Key를 확인해주세요.

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
### SSO 원격로그인 API (Client Side)
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/v2/enduser/remote.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/v2/enduser/remote.json		

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|SSO 원격로그인 API (Client Side)|HTTPS  |POST    |UTF-8|Redirect    |사용자 시스템에서 동적으로 form를 생성하여 브라우저에 반환하며, form은 자동으로 API에 form정보를 전달. API에서 전달된 form정보로 인증 후 성공시 로그인 Cookie 값 설정.|

**사용자 시스템에서의 호출 방법**은 하단 Sample project의 다음과 같은 class를 참조해 주세요.
- FormLoginController.java
- Method: submitLogin  

#### 요청 파라미터 정의
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

#### 결과 데이터
returnUrl 파라미터 존재시 지정된 returnUrl로 이동 , returnUrl 없을 경우 문자열 : SUCCESS 반환

### SSO 원격로그인 API (Server Side)
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/api/v2/enduser/remote.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/api/v2/enduser/remote.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|SSO 원격로그인 API (Server Side)|HTTPS  |POST    |UTF-8|String   |사용자가 서버에서 직접 API 호출. API 로그인 성공 후 로그인 Cookie 값 설정.|
  
**사용자 시스템에서의 호출 방법**은 하단 Sample project의 다음과 같은 class를 참조해 주세요.
- ApiLoginController.java
- Method: submitLogin     
  
#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|서비스ID	|service	|Varchar(50)	|O	|서비스 ID|
|유저ID	|usercode	|Varchar(50)	|O	|유저ID，유일한 유저임을 표시|
|유저 명	|username	|Varchar(50)	|X	|유저 명|
|유저 이메일 주소	|email	|Varchar(100)	|X	|유저 이메일|
|전화번호	|phone	|Varchar(20)	|X	|전화번호|
|현재 시간의 timestamp	|time	|Long	|O	|호출 시간이 3분 초과시, 타임아웃 얼럿 출력.|
|인증 Token	|token	|Varchar	|O	|아래 파라미터 값과 SSO API Key로 산출된 SHA256 (필수가 아닌 파라미터 값이 null 혹은 빈값일 경우 , 암호화 문자열에 추가 할 필요 없음.주의：문자열 중 각 값의 순서는 아래 예시에 지정된 순서와 일치해야 함.) SHA256Digest(service + usercode + username + email + phone + time)|

#### 결과 데이터
SUCCESS
 
### SSO 로그인 URL (사용자)
#### 인터페이스 설명
- URL: 사용자 제공			
- URL (개발): 사용자 제공	

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|
|------------|--------|--------|------|------|
|SSO 로그인 URL|HTTPS|GET|UTF-8||Redirect|

서비스 측 로그인 URL은 아래 기능을 제공해야 합니다.

1) 사용자 미로그인
- 로그인 화면 출력
- 계정/비밀번호로 로그인 진행
- 로그인 성공 후 cookie 생성 및 로그인 상태 기록，로그인 상태 체크시 사용 됨
- 로그인 성공 후 Client 혹은 Server단에서 고객 정보를 OC로 전달 (SSO 원격로그인 API Client Side, Server Side 참조)

2) 사용자 로그인 상태
- 로그인 성공 후 Client 혹은 Server단에서 고객 정보를 OC로 전달 (SSO 원격로그인 API Client Side, Server Side 참조)

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|---------|----|
|리턴 URL	|returnUrl	|Varchar	|O	|로그인 성공후 이동되는 URL|

#### SSO 로그인 기능 설명
1) 유저 미 로그인 상태
- ① 로그인 화면으로 이동
- ② 유저 로그인
- ③ 서비스 측의 서버에서 유저 로그인 처리 및 로그인 유저 관련 쿠키 생성
- ④ SSO 원격 로그인 API 호출

2) 유저 로그인 상태
- ① SSO 원격 로그인 API 호출

#### SSO 원격 로그인 API 호출 방법 설명
1) SSO 원격 로그인 (Client Side)
- ① 유저 정보와 API Key 기준으로 로그인 token 생성
- ② 유저 정보와 token을 브라우저로 리다이렉트
- ③ 화면에서 Form 작성, 상세한 파라미터는 [SSO 원격로그인 API (Client Side)](https://docs.toast.com/ko/Contact%20Center/ko/online-contact-api-guide-openapi-sso/#sso-api-client-side) 참조
- ④ Form 제출
- ⑤ SSO 원격 로그인 API를 통해 유저 정보와 token 전송
- ⑥ 로그인 성공 후 {returnUrl}로 이동

2) SSO 원격 로그인 (Server Side)
- ① 유저 정보와 API Key 기준으로 로그인 token 생성
- ② 서버에서 "SSO 원격 로그인 API (Server Side)" 호출
- ③ API 호출 파라미터 (usercode와 time)을 returnUrl 뒤에 추가 
  - 예시) https://nhn-cs.alpha-oc.toast.com/multilanguage/hc/ticket/list/?usercode=xxxxxx@163.com&time=1566531359635
- ④ {returnUrl}로 이동
 
### SSO 로그인 상태 URL (사용자)
#### 인터페이스 설명
- URL: 사용자 제공			
- URL (개발): 사용자 제공	

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|--------|--------|------|--|----------|
|SSO 로그인 상태 API|HTTPS|GET|UTF-8|JSON|사용자가 쿠키 정보를 기준으로 로그인 여부를 확인 후 JSON 형식의 데이터를 리턴|

**사용자 시스템에서의 호출 방법**은 하단 Sample project의 다음과 같은 class를 참조해 주세요.
- FormLoginController.java
- Method: loginStatus

#### 요청 파라미터 정의 
- 없음

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|---------|----|
|javascript function	|login	|Boolean	|O	|로그인 상태. 로그인 ：true, 미로그인 ：false|
|유저 코드	|usercode	|Varchar(50)	|X	|유저 ID(유니크 값). 로그인 상태가 true 인 경우 유저코드는 필수|

#### Response Body
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

## 적용 예시
### Sample Code
✔ [Sample Code 다운로드](http://static.toastoven.net/prod_contact_center/oc_sso_sample.zip)

### iframe을 이용한 헬프센터 예시
#### 1. iframe을 이용하여 Online Contact 헬프센터를 사용자 페이지에 삽입
Sample Code 파일 중 'oc_sso_sample/src/main/resources/templates/help_frame.ftl'을 참조해주세요.
iframe의 이름은 반드시 id = "ocPage"로 지정하셔야 합니다.
```
<iframe src="https://${domain}/hangame/hc/?iframe=true" id="ocPage" frameborder="0" scrolling="no" style="padding-top: 60px; box-sizing: unset; height: 100px; width: 100%">
</iframe>
```  
 
페이지에 viewport를 설정할 시 mobile/web 브라우저 모두에서 헬프센터를 사용하실 수 있습니다.
```
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=0">
```

#### 2. Online Contact 헬프센터 페이지의 높이를 확인하여 iframe의 height 조정
help_frame.ftl 파일 중 javascript 코드를 참조해주세요.
```
// Listener for OC content height change
window.addEventListener('message',function(event){
    // Set iframe height
    if(event.data > 0) {
    updateHeight(event.data);
    }
});

var updateHeight = function(wrapHeight) {
var iframe = window.document.getElementById('ocPage');
if(iframe != null) {
iframe.style.height = '0px'; 
var setHeight = (document.body.clientHeight > document.body.scrollHeight) ? document.body.clientHeight : document.body.scrollHeight;
var margin = 70;
setHeight = setHeight > wrapHeight ? setHeight : wrapHeight;
iframe.style.height = setHeight + margin + "px";
}
};
```

#### 3. 로그인 처리 후 설정해야 할 쿠키는 사용자 페이지에서 취득 가능
help_frame.ftl 파일 중 javascript 코드를 참조해주세요.
```
// get cookie
function getCookie(name) {
    var arr,reg=new RegExp("(^| )"+name+"=([^;]*)(;|$)");
    if(arr=document.cookie.match(reg))
        return unescape(arr[2]);
    else
        return null;
}
$.when( $.ready ).then(function() {
    var ssotoken = getCookie("sso_test_login");
    var usercode = getCookie("usercode");
    if(ssotoken != null && usercode != null) {
        var signout = $("#signout");
        $("#signout").html("Welcome " + usercode + "! <a href='/logout.nhn'>Sign out</a>");
        $("#signout").show();
        $("#signin").hide();
    }
});
```
