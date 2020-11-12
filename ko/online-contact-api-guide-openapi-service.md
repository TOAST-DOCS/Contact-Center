## Contact Center > Online Contact > API 가이드 > 서비스 
### 서비스 추가
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/add.json
- URL(개발): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/add.json

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 추가  |HTTPS  |POST    |UTF-8|JSON    |신규 서비스 추가|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|서비스 정보	|request body	|String	|O	|서비스 정보 (JSON)|
|	          |serviceId	  |String	|O	|서비스 ID (유일한 값:예 ; 길이:min = 0, max = 45 ; 형식:영문)|
|	          |name	        |String	|O	|서비스 명 (유일한 값:예; 길이:min = 0, max = 100)|
|	          |language	    |String	|O	|서비스 언어 (값:zh\|ja\|ko\|en, ko:한국어, ja:일본어, en:영어, zh:중국어)|
|				    |timeZone	    |String	|X	|타임 존 (값:Asia/Seoul\|Asia/Tokyo|...)|

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
|	              |language	  |String	  |O	|서비스 언어（값:zh\|ja\|ko\|en, ko:한국어, ja:일본어, en:영어, zh:중국어)|
|	              |timeZone 	|String	  |X	|타임 존（값:Asia/Seoul\|Asia/Tokyo|...)|
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
|               |language	  |String	|O	|서비스 언어（값:zh\|ja\|ko\|en, ko:한국어, ja:일본어, en:영어, zh:중국어)|
|	              |timeZone	  |String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo|...)|
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

### 서비스 수정
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json 						
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 수정  |HTTPS  |PUT    |UTF-8|JSON    |서비스 아이디를 통해 서비스 정보 수정|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한{serviceId}|
|서비스 정보	|request body	|String	|O	|서비스 정보（JSON）|
|	          |name	|String	|O	|서비스 명（유일한 값:예; 길이:min = 0, max = 100)|
|	          |language	|String	|O	|서비스 언어(값:zh\|ja\|ko\|en）ko:한국어, ja:일본어, en:영어, zh:중국어)|
|	          |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo|...)|

변수 timeZone의 기본 값은 다음과 같습니다.
- language=ko: timeZone=Asia/Seoul
- language=ja: timeZone=Asia/Tokyo
- language=en: timeZone=America/New_York
- language=zh: timeZone=Asia/Shanghai

#### Request Body
```
{
    "name":"GameBaseServiceAPI",
    "language":"ko",
    "timeZone":"Asia/Seoul"
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|result.content	|serviceId	|String	|O	|서비스 ID|
|	              |name	|String	|O	|서비스 명|
|	              |active	|Boolean	|X	|서비스 상태. true:활성화, false:비활성화|
|	              |language	|String	|O	|서비스 언어（값:zh\|ja\|ko\|en）ko:한국어, ja:일본어, en:영어, zh:중국어)|
|	              |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo|...)|
|	              |createdDt	|Long	|X	|서비스 생성시간|
|	              |updatedDt	|Long	|X	|서비스 업데이트 시간|
|	              |securityKey	|String	|X	|Open API Key|

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
            "active":null,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "createdDt":null,
            "updatedDt":1586761475102,
            "securityKey":null
        }
    }
}
```

### 서비스 비활성화
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/disable.json							
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/disable.json			 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 비활성화  |HTTPS  |PUT    |UTF-8|JSON    |서비스 아이디를 통해 서비스 비활성화   |공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID（query）|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result.content	|serviceId	|String	|O	|서비스 ID|
|	              |name	|String	|O	|서비스 명|
|	              |active	|Boolean	|X	|서비스 상태. true:활성화, false:비활성화|
|	              |language	|String	|O	|서비스 언어（값:zh\|ja\|ko\|en）ko:한국어, ja:일본어, en:영어, zh:중국어)|
|	              |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo|...)|
|	              |createdDt	|Long	|X	|서비스 생성시간|
|	              |updatedDt	|Long	|X	|서비스 업데이트 시간|
|	              |securityKey	|String	|X	|Open API Key|

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
            "active":false,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "updatedDt":1586745222000,
            "updatedDt":1586761475000,
            "securityKey":null
        }
    }
}

```

### 서비스 활성화
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/enable.json					
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/enable.json					 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 활성화  |HTTPS  |PUT    |UTF-8|JSON    |서비스 아이디를 통해 서비스 활성화   |공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID（query）|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|----|----|
|result.content	|serviceId	|String	|O	|서비스 ID|
|               |name	|String	|O	|서비스 명|
|	              |active	|Boolean	|X	|서비스 상태. true:활성화, false:비활성화|
|	              |language	|String	|O	|서비스 언어（값:zh\|ja\|ko\|en）ko:한국어, ja:일본어, en:영어, zh:중국어)|
|	              |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo|...)|
|	              |createdDt	|Long	|X	|서비스 생성시간|
|	              |updatedDt	|Long	|X	|서비스 업데이트 시간|
|	              |securityKey	|String	|X	|Open API Key|

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
            "updatedDt":1586745222000,
            "updatedDt":1586761475000,
            "securityKey":null
        }
    }
}
```

### 서비스 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json					
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json							 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 삭제  |HTTPS  |DELETE    |UTF-8|JSON    |서비스 아이디를 통해 비활성화된 서비스 삭제 |공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한{serviceId}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|result.content		|String	|X	|"SUCCESS":삭제 성공, "ENABLE":활성화 상태로 삭제할 수 없음，비활성화 후 삭제 가능|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":"SUCCESS"
    }
}
```

### 서비스 API Key 재발급
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/apikey/refresh.json						
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/apikey/refresh.json								 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 API Key 재발급  |HTTPS  |PUT    |UTF-8|JSON    |서비스 아이디를 통해 해당 서비스에 생성된 API Key 다시 발급|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID（query）|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result.content		|String	|X	|신규 API Key|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":"bd7a45aa764f4936a43ef0c4500da7ba"
    }
}
```

### 서비스 리스트
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/list.json			 			
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/list.json								 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 리스트  |HTTPS  |GET    |UTF-8|JSON    |조직 내에 생성된 모든 서비스 조회|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|페이지	|page	|int	|	|기본 값:1|
|1페이지 노출 건수	|pageSize	|int	|	|기본 값:100|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|result.contents	|serviceId	|String	|O	|서비스 ID|
|	                |name	|String	|O	|서비스 명|
|	                |active	|Boolean	|X	|서비스 상태. true:활성화, false:비활성화|
|	                |language	|String	|O	|서비스 언어（값:zh\|ja\|ko\|en）ko:한국어, ja:일본어, en:영어, zh:중국어|
|	                |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo|...）|
|	                |createdDt	|Long	|X	|서비스 생성시간|
|	                |updatedDt	|Long	|X	|서비스 업데이트 시간|
|	                |securityKey	|String	|X	|Open API Key|
|result.total	|total	|Long	|X	|총 건수|
|result.pages	|pages	|int	|X	|총 페이지 수|
|result.pageNum	|pageNum	|int	|X	|현재 페이지|
|result.pageSize	|pageSize	|int	|X	|1페이지 노출 건수|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "contents":[
            {
                "serviceId":"gamebase",
                "name":"Gamebase",
                "active":true,
                "language":"ko",
                "timeZone":"Asia/Shanghai",
                "createdDt":1552901051000,
                "updatedDt":1566203644000,
                "securityKey":"1b7426d5821b42bc9e1503bfb2979aee"
            },
            {
                "serviceId":"GameBaseService",
                "name":"GameBaseServiceAPI",
                "active":true,
                "language":"ko",
                "timeZone":"Asia/Seoul",
                "createdDt":1586745222000,
                "updatedDt":1586765984000,
                "securityKey":"bd7a45aa764f4936a43ef0c4500da7ba"
            },
        ],
        "total":2,
        "pages":1,
        "pageNum":1,
        "pageSize":100
    }
}
```

