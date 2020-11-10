## Contact Center > Online Contact > API 가이드 > 서비스 
### 서비스 추가
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/add.json
- URL(개발): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/add.json

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 추가  |HTTPS  |POST    |UTF-8|JSON    |신규 서비스 추가|공통 인증   |

|담당자 이름	|담당자 이메일	|담당자 부서	|
|-----------|--------------|-----------|
|徐凯|xu_kai@nhn-st.com|CS Development Part|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|서비스 정보	|request body	|String	|O	|서비스 정보（JSON|
|	          |serviceId	  |String	|O	|서비스 ID（유일한 값:예 ; 길이:min = 0, max = 45 ; 형식:영문)|
|	          |name	        |String	|O	|서비스 명（유일한 값:예; 길이:min = 0, max = 100|
|	          |language	    |String	|O	|서비스 언어（값:zh|ja|ko|en, ko:한국어, ja:일본어, en:영어, zh:중국어）|
|				    |timeZone	    |String	|X	|타임 존（값:Asia/Seoul|Asia/Tokyo|...）|

변수 timeZone의 기본 값은 다음과 같습니다.
- language=ko: timeZone=Asia/Seoul
- language=ja: timeZone=Asia/Tokyo
- language=en: timeZone=America/New_York
- language=zh: timeZone=Asia/Shanghai

#### Request Body
```
{
    "serviceId":"GameBaseService",
    "name":"GameBaseServiceAPI",
    "language":"ko",
    "timeZone":"Asia/Seoul"
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|----------|-----|----|
|result.content	|serviceId	|String	|O	|서비스 ID|
|	              |name	      |String	|O	|서비스 명|
|	              |active	    |Boolean	|X	|서비스 상태(true:활성화, false:비활성화)|
|	              |language	  |String	  |O	|서비스 언어（값:zh|ja|ko|en, ko:한국어, ja:일본어, en:영어, zh:중국어|
|	              |timeZone 	|String	  |X	|타임 존（값:Asia/Seoul|Asia/Tokyo|...）|
|               |createdDt	|Long	    |X	|서비스 생성 시간|
|	              |updatedDt	|Long	    |X	|서비스 업데이트 시간|
|               |securityKey	|String	|X	|Open API Key|

#### Response Body
```Cabal Config
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

### 서비스 상세
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 상세  |HTTPS  |GET    |UTF-8|JSON    |서비스 아이디를 통해 서비스 정보 조회|공통 인증   |

|담당자 이름|담당자 이메일|CS Development Part|
|----------|------------|------------------
|徐凯|xu_kai@nhn-st.com|담당자 부서	|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한{serviceId}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result.content	|serviceId	|String	|O	|서비스 ID|
|	              |name	      |String	|O	|서비스 명|
|	              |active	    |Boolean|		|서비스 상태(true:활성화, false:비활성화)|
|               |language	  |String	|O	|서비스 언어（값:zh|ja|ko|en, ko:한국어, ja:일본어, en:영어, zh:중국어|
|	              |timeZone	  |String	|X	|타임 존（값:Asia/Seoul|Asia/Tokyo|...）|
|              	|createdDt	|Long	  |X	|서비스 생성 시간|
|	              |updatedDt	|Long	  |X	|서비스 업데이트 시간|
|             	|securityKey|String	|X	|Open API Key|

#### Response Body
```
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
