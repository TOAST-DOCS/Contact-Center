## Contact Center > Online Contact > API 가이드 > 회원 연동 (GET)

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

### 프로세스 (GET 방식)
① USER가 APP 내에서 헬프센터에 접속합니다.
② 고객사의 APP은 헬프센터 호출 시 아래 URL 형식으로 호출합니다.
- https://**{org}**.oc.toast.com/**{service}**/hc/?usercode=**{유저_아이디}**&username=**{유저_이름}**&email=**{유저_이메일}**&phone=**{유저_전화번호}**&token=**{인증토큰_값}**
③ 헬프센터에서 ‘토큰 검증 URL’을 호출합니다. (여기서 ‘토큰 검증 URL 은 고객사에서 아래 제공된 명세서에 따라 개발 후 OC 회원연동 화면에 등록해야 합니다.)
④ 토큰 검증 후 정상일 경우 ‘문의하기’ 또는 ‘문의내역’ 페이지에 접속합니다. 이 때 검증에 실패 할 경우 ‘문의하기’는 비회원으로 접수됩니다.

### 회원 연동 방법
![](http://static.toastoven.net/prod_contact_center/dev_post_(2).png)
① 서비스 관리 > 헬프센터 > 회원 연동 접속
② 회원 연동 활성화 항목에서 ‘활성화’ 버튼 클릭
③ 서비스 성격에 맞는 ‘로그인 타입’ 선택
④ 각 타입에 따라 필요한 API 개발 및 URL 설정 및 저장

## 개발 명세서
### 인증토큰 생성
Token 생성 샘플은 아래와 같습니다. 파라미터 순서는 반드시 아래와 일치해야 하며, 전체 관리 → 계약 서비스 현황 → 조직 정보 메뉴에서  Key를 확인해주세요.

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

### GET 회원인증 방법
#### 인터페이스 설명

URL

- https://{org}.oc.toast.com/{service}/hc/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{org}.oc.toast.com/{service}/hc/ticket/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{org}.oc.toast.com/{service}/hc/ticket/list/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d

URL (개발)

- https://{domain}.alpha-oc.toast.com/{service}/hc/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{domain}.alpha-oc.toast.com/{service}/hc/ticket/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{domain}.alpha-oc.toast.com/{service}/hc/ticket/list/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
  
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|GET 회원인증 |HTTPS |GET |UTF-8 | |서비스 측에서 헬프센터 접속 시, 고객정보 및 암호화 후 생성된 token 값을 파라미터 형태로 전송 |

#### 파라미터
|명칭|변수|데이터 타입|필수|설명|
|----|-------|----------|----|---|
|서비스 ID	|service	|VARCHAR(50)	|O	|서비스 ID|
|유저 ID	 |usercode	|VARCHAR(50)	|O	|유저ID(유니크 값)|
|유저 명	  |username	 |VARCHAR(50)	 |X	 |유저 명|
|유저 이메일	|email	  |VARCHAR(100)	|O	|유저 이메일|
|전화번호	   |phone	   |VARCHAR(20)	 |X	 |전화번호|
|회원번호	|memberno	|VARCHAR(50)	|X	|회원번호|
|timestamp	|time	    |LONG	        |O	|시간단위 : 밀리초|
|인증Token	|token	  |VARCHAR	     |O	|다음 파라미터 값과 조직 Key로 계산(SHA256). (선택사항 값이 null 혹은 없을 경우, token 생성에서 제외. 주의사항 : 문자열에서 각 값의 순서는 다음과 동일해야 함) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|

##### 인증 Token 생성 시 주의사항
1. Token 생성 시, 한글이 있을 경우 한글로 직접 생성. 인코딩 필요 없음
2. 생성된 Token을 URL 파라미터로 사용 시, encodeURIComponent()로 인코딩 필요

#### 결과 데이터
- Token 인증 성공: 회원으로 접속하는 주소로 이동		
- Token 인증 실패: 비회원으로 접속하는 주소로 이동		
- Token 인증 실패 상태에서 문의내역으로 접속 시, 문의하기 화면으로 이동		

### Token 인증 API (서비스 측)
#### 인터페이스 설명
- URL: 서비스 측에서 지원 		
- URL (개발): 서비스 측에서 지원

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|Token 인증 확인 API |HTTPS |GET |UTF-8 |JSON |서비스 측에서 token과 usercode로 로그인 상태 확인 후 JSON 형태 결과 값을 전송 |

#### 요청 파라미터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-------|----------|----|---|
|유저 ID	|usercode	|VARCHAR(50)	|O	|유저 ID(유니크 값)|
|서비스 측에서 생성한 Token	|token	|VARCHAR	|O	|다음 파라미터 값과 조직 Key로 계산(SHA256). (선택사항 값이 null 혹은 없을 경우, token 생성에서 제외. 주의사항 : 문자열에서 각 값의 순서는 다음과 동일해야 함) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|

#### Response Body
```
로그인：
{
"login": "true",
"usercode":"usercodeXXX"
}


미로그인：
{
"login": "false",
"usercode": null
}
```
