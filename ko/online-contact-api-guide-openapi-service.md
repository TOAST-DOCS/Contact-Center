## Contact Center > Online Contact > API 가이드 > 서비스 

### 계약 항목 코드
- ticket: 티켓 (기본 활성화, 변경 불가능)
- chat: 채팅
- telticket: 티켓 (전화 포함 - CTI 사용 포함)
- endusermanagement: 고객정보관리
- callback: 콜백
- helpdoc: FAQ
- knowledge: 지식관리
- issuetransferstatistics: 이슈이관 통계 (향후 추가 예정)
- reinquiryrate: 재문의율 (향후 추가 예정)
- smssend: SMS (향후 추가 예정)
- smssendingstatus: SMS 발송 현황 (향후 추가 예정)
- electronicboard: 전광판 (향후 추가 예정)
- ticketevaluation: 티켓 평가 (향후 추가 예정)
- happycall: 해피콜 (향후 추가 예정)
- security: 보안 서비스 (향후 추가 예정)


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
|				    |timeZone	    |String	|X	|타임 존 (값:Asia/Seoul\|Asia/Tokyo\|...)|

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
|	              |timeZone 	|String	  |X	|타임 존（값:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|서비스 생성 시간|
|	              |updatedDt	|Long	    |X	|서비스 업데이트 시간|
|               |securityKey	|String	|X	|Open API Key|

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
|	              |active	    |Boolean|X		|서비스 상태(true:활성화, false:비활성화)|
|               |language	  |String	|O	|서비스 언어（값:zh\|ja\|ko\|en, ko:한국어, ja:일본어, en:영어, zh:중국어)|
|	              |timeZone	  |String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo\|...)|
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
|	          |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo\|...)|

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
|	              |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo\|...)|
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
|	              |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo\|...)|
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
|	              |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo\|...)|
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
|-----|----|------------|----|----|
|result.content	|	|String	|X	|"SUCCESS":삭제 성공, "ENABLE":활성화 상태로 삭제할 수 없음，비활성화 후 삭제 가능|

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

### 서비스 목록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/list.json			 			
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/list.json								 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 목록 |HTTPS  |GET    |UTF-8|JSON    |조직 내에 생성된 모든 서비스 조회|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|페이지	|page	|Int	|X	|기본 값:1|
|1페이지 노출 건수	|pageSize	|Int	|X	|기본 값:100|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|result.contents	|serviceId	|String	|O	|서비스 ID|
|	                |name	|String	|O	|서비스 명|
|	                |active	|Boolean	|X	|서비스 상태. true:활성화, false:비활성화|
|	                |language	|String	|O	|서비스 언어（값:zh\|ja\|ko\|en）ko:한국어, ja:일본어, en:영어, zh:중국어|
|	                |timeZone	|String	|X	|타임 존（값:Asia/Seoul\|Asia/Tokyo\|...）|
|	                |createdDt	|Long	|X	|서비스 생성시간|
|	                |updatedDt	|Long	|X	|서비스 업데이트 시간|
|	                |securityKey	|String	|X	|Open API Key|
|result.total	|total	|Long	|X	|총 건수|
|result.pages	|pages	|Int	|X	|총 페이지 수|
|result.pageNum	|pageNum	|Int	|X	|현재 페이지|
|result.pageSize	|pageSize	|Int	|X	|1페이지 노출 건수|

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

### 서비스 계약 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/reg.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/reg.json						 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 계약 등록 |HTTPS  |POST    |UTF-8|JSON    |서비스 신규 계약 등록|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 계약 정보	|request body	|String	|O	|서비스 정보(JSON)|
|	                |serviceId	   |String	|O	|서비스 ID(유니크 값:예; 길이:min = 0, max = 45;형태:영문)|
|	                |billingSettings	|List	|X	  |계약 항목 설정 리스트|
|	                |    billingSettingCode	|String	|O	|항목 코드(계약 항목 코드 참조)|
|	                |    active	            |Boolean	|X	|활성화:true  비활성화:false|

#### Request Body
```
{
        "serviceId": "example",
        "billingSettings": [{
                "billingItemCode": "callback",
                "active": false
        }, {
                "billingItemCode": "chat",
                "active": true
        }, {
                "billingItemCode": "endusermanagement",
                "active": false
        }, {
                "billingItemCode": "helpdoc",
                "active": false
        }, {
                "billingItemCode": "knowledge",
                "active": true
        }, {
                "billingItemCode": "telticket",
                "active": false
        }]
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|----|-----|
|result.content	|id	|Long	|O	|계약 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |organizationId	|String	|O	|조직 ID|
|	              |type	          |Int	  |O	|서비스 타입(1:상담관리, 2:이슈관리), 기본 값:1|
|	              |status	        |String	|O	|계약 상태(작성중:create, 이용중:inuse, 이용중지:pause, 삭제:stop)|
|	              |startDt	      |String	|O	|서비스 이용 시작일(한국시간)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|할인률(%)|
|	              |freeExtension	|Int	  |O	|무료체험 기간 연장 날짜|
|	              |active	        |Boolean	|O	|서비스 계약(활성화:true, 비활성화:false)|
|	              |freeTrial	    |Boolean	|O	|무료체험 기간(예:true, 아니오:false)|
|	              |billingSettings	|List	  |O	|계약항목 설정 리스트|
|	              |    id	              |Long	  |O	|계약항목 설정 ID|
|	              |    billingId	      |Long	  |O	|계약 ID|
|	              |    billingSettingCode	|String	|O	|항목 코드(계약항목 코드 참조)|
|	              |    active	            |Boolean	|O	|활성화:true, 비활성화:false|

#### Response Body
```
{
        "header": {
                "resultCode": 200,
                "resultMessage": "",
                "isSuccessful": true
        },
        "result": {
                "content": {
                        "id": 214,
                        "organizationId": "WopqM8euoYw89B7i",
                        "organizationName": "NHN-CS",
                        "serviceId": "example",
                        "serviceName": "example",
                        "type": 1,
                        "language": "zh",
                        "status": "inuse",
                        "startDt": "20201204090910",
                        "discountRate": 0,
                        "freeExtension": 0,
                        "email": "xxxxxxxxxxxx@nhn.com",
                        "active": true,
                        "createdDt": 1607044142000,
                        "updatedDt": 1607044150934,
                        "freeTrial": false,
                        "billingSettings": [{
                                "id": 656,
                                "billingId": 214,
                                "billingItemCode": "callback",
                                "active": false
                        }, {
                                "id": 657,
                                "billingId": 214,
                                "billingItemCode": "chat",
                                "active": true
                        }, {
                                "id": 658,
                                "billingId": 214,
                                "billingItemCode": "endusermanagement",
                                "active": false
                        }, {
                                "id": 659,
                                "billingId": 214,
                                "billingItemCode": "helpdoc",
                                "active": false
                        }, {
                                "id": 660,
                                "billingId": 214,
                                "billingItemCode": "knowledge",
                                "active": true
                        }, {
                                "id": 661,
                                "billingId": 214,
                                "billingItemCode": "telticket",
                                "active": false
                        }, {
                                "id": 662,
                                "billingId": 214,
                                "billingItemCode": "ticket",
                                "active": true
                        }]
                }
        }
}
```

### 서비스 계약 변경
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/update/{billingId}.json						
- URL (개발): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/update/{billingId}.json						 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스 계약 변경 (하루 1회만 가능) |HTTPS  |PUT    |UTF-8|JSON    |계약 변경|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 계약 정보	|request body	|String	|O	|서비스 정보(JSON)|
|	                |id	          |Long	  |O	|계약 ID|
|	                |serviceId	  |String	|O	|서비스 ID(유니크 값:예; 길이:min = 0, max = 45;형태:영문)|
|	                |billingSettings	|List	|O	|계약 항목 설정 리스트|
|	                |id	              |Long	|O	|계약 항목 설정 ID|
|	                |billingId	      |Long	|X	|계약 ID|
|	                |    billingSettingCode	|String	|O	|항목 Code(계약항목 코드 참조)|
|	                |    active	            |Boolean	|X	|활성화:true  비활성화:false|

#### Request Body
```
{
        "id": 205,
        "serviceId": "qwqwqw",
        "billingSettings": [{
                "id": 620,
                "billingId": 205,
                "billingItemCode": "callback",
                "active": false
        }, {
                "id": 621,
                "billingId": 205,
                "billingItemCode": "chat",
                "active": false
        }, {
                "id": 622,
                "billingId": 205,
                "billingItemCode": "endusermanagement",
                "active": false
        }, {
                "id": 623,
                "billingId": 205,
                "billingItemCode": "helpdoc",
                "active": false
        }, {
                "id": 624,
                "billingId": 205,
                "billingItemCode": "knowledge",
                "active": false
        }, {
                "id": 625,
                "billingId": 205,
                "billingItemCode": "telticket",
                "active": false
        }]
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|계약 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |organizationId	|String	|O	|조직 ID|
|	              |type	          |Int	  |O	|서비스 타입(1:상담관리, 2:이슈관리), 기본 값:1|
|	              |status	        |String	|O	|계약 상태(작성중:create, 이용중:inuse, 이용중지:pause, 삭제:stop)|
|	              |startDt	      |String	|O	|서비스 이용 시작일(한국시간)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|할인률(%)|
| 	            |freeExtension	|Int	  |O	|무료체험 기간 연장 날짜|
|               |active	        |Boolean	|O	|서비스 계약(활성화:true, 비활성화:false)|
|	              |freeTrial	    |Boolean	|O	|무료체험 기간(예:true, 아니오:false)|
|	              |billingSettings	|List	  |O	|계약항목 설정 리스트|
|	              |    id	          |Long	  |O	|계약항목 설정 ID|
|	              |    billingId	  |Long	  |O	|계약 ID|
|	              |    billingSettingCode	|String	|O	|항목 코드(계약항목 코드 참조)|
|	              |    active	            |Boolean	|O	|활성화:true, 비활성화:false|

#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "content": {
            "id": 205,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "qwqwqw",
            "serviceName": "qwqwqw",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201202115045",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606877440000,
            "updatedDt": 1607046392063,
            "freeTrial": false,
            "billingSettings": [{
                "id": 620,
                "billingId": 205,
                "billingItemCode": "callback",
                "active": false
            }, {
                "id": 621,
                "billingId": 205,
                "billingItemCode": "chat",
                "active": false
            }, {
                "id": 622,
                "billingId": 205,
                "billingItemCode": "endusermanagement",
                "active": false
            }, {
                "id": 623,
                "billingId": 205,
                "billingItemCode": "helpdoc",
                "active": false
            }, {
                "id": 624,
                "billingId": 205,
                "billingItemCode": "knowledge",
                "active": false
            }, {
                "id": 625,
                "billingId": 205,
                "billingItemCode": "telticket",
                "active": false
            }]
        }
    }
}

하루 1번이상 변경 시，Response：
{
    "header": {
        "resultCode": 9015,
        "resultMessage": "billing.setting.today.already.changed",
        "isSuccessful": false
    },
    "result": {
        "content": {
            "exception": "OcException",
            "message": "billing.setting.today.already.changed"
        }
    }
}
```

### 서비스 계약 목록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/list.json									
- URL (개발): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/list.json									 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|조직 내 서비스 계약 목록|HTTPS  |GET    |UTF-8|JSON    |조직 내 서비스 계약 목록 취득|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|조직 내 서비스 계약 리스트 취득	|page	|Int	|X	|페이지, 기본 값:1|
|	                              |pageSize	|Int	|X	|1페이지 노출건수，기본 값:10|
|	                              |billingSettingCode	|		|   |   |
|	                              |active			        |   |   |   |

#### Request URL
```
/openapi/v1/admin/billing/list.json?page=1&pageSize=10	
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|----|
|result.contents	|id	|Long	|O	|계약 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |organizationId	|String	|O	|조직 ID|
|	                |type	          |Int	  |O	|서비스 타입(1:상담관리, 2:이슈관리), 기본 값:1|
|	                |status	        |String	|O	|계약 상태(작성중:create, 이용중:inuse, 이용중지:pause, 삭제:stop)|
|	                |startDt	      |String	|O	|서비스 이용 시작일(한국시간)：yyyyMMddHHmmss|
|	                |discountRate	  |Int	  |O	|할인률(%)|
|	                |freeExtension	|Int	  |O	|무료체험 기간 연장 날짜|
|	                |active	        |Boolean	|O	|서비스 계약(활성화:true, 비활성화:false)|
|	                |freeTrial	    |Boolean	|O	|활성화:true, 비활성화:false|

#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "contents": [{
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000
        }, {
            "id": 212,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201203154729",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606981630000,
            "updatedDt": 1606981649000
        }, {
            "id": 205,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "qwqwqw",
            "serviceName": "qwqwqw",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201202115045",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606877440000,
            "updatedDt": 1607046392000
        }, {
            "id": 196,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example2",
            "serviceName": "example2",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201201105044",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606787441000,
            "updatedDt": 1606875428000
        }, {
            "id": 192,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example3",
            "serviceName": "example3",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201127082852",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606436928000,
            "updatedDt": 1606436933000
        }, {
            "id": 191,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example4",
            "serviceName": "example4",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201127072001",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606432792000,
            "updatedDt": 1606432802000
        }, {
            "id": 154,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example5",
            "serviceName": "example5",
            "type": 1,
            "language": "ja",
            "status": "inuse",
            "startDt": "20201124103657",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606181811000,
            "updatedDt": 1606783784000
        }, {
            "id": 153,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "testfour",
            "serviceName": "testfour",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201124090639",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606179981000,
            "updatedDt": 1606181786000
        }, {
            "id": 152,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "testthird",
            "serviceName": "testthird",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201124093856",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606178332000,
            "updatedDt": 1606180298000
        }, {
            "id": 146,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "aaammm",
            "serviceName": "aaammm",
            "type": 1,
            "language": "zh",
            "status": "pause",
            "startDt": "20201119142206",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": false,
            "createdDt": 1605762562000,
            "updatedDt": 1606093890000
        }],
        "total": 70,
        "pages": 7,
        "pageNum": 1,
        "pageSize": 10
    }
}
```

### 서비스 계약 상세 - 서비스ID
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/service/{serviceId}.json									
- URL (개발): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/service/{serviceId}.json								 				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|서비스ID로 계약 상세 정보 취득|HTTPS  |GET    |UTF-8|JSON    |서비스 ID로 계약 상세 정보 취득|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 계약 상세 정보	|serviceId	|String	|O	|서비스 ID|

#### Request URL
```
/openapi/v1/admin/billing/service/example.json	
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|계약 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |organizationId	|String	|O	|조직 ID|
|	              |type	          |Int	  |O	|서비스 타입(1:상담관리, 2:이슈관리), 기본 값:1|
|	              |status	        |String	|O	|계약 상태(작성중:create, 이용중:inuse, 이용중지:pause, 삭제:stop|
|	              |startDt	      |String	|O	|서비스 이용 시작일(한국시간)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|할인률(%)|
|	              |freeExtension	|Int	  |O	|무료체험 기간 연장 날짜|
|	              |active	        |Boolean	|O	|서비스 계약(활성화:true, 비활성화:false)|
|	              |freeTrial	    |Boolean	|O	|무료체험 기간(예:true, 아니오:false)|
|	              |billingSettings	|List	  |O	|계약항목 설정 리스트|
|	              |    id	              |Long		|O  |계약항목 설정 ID|
|	              |    billingId	      |Long	  |O	|계약 ID|
|	              |    billingSettingCode	|String	|O	|항목Code|
|	              |    active	            |Boolean	|O	|활성화:true, 비활성화:false|
|	              |    billingItem	      |Object	  |X	|유료 서비스 항목 상세|
|	              |        code	              |String	  |O	|항목Code|
|	              |        open	              |Boolean	|O	|활성화:true, 비활성화:false|

#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "content": {
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000,
            "freeTrial": false,
            "billingSettings": [{
                "id": 656,
                "billingId": 214,
                "billingItemCode": "callback",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "callback",
                    "parentCode": "additional",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "",
                    "sumCounterName": "onlinecontact.callback_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "14"
                }
            }, {
                "id": 657,
                "billingId": 214,
                "billingItemCode": "chat",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "chat",
                    "parentCode": "chat",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.chat_lisence",
                    "sumCounterName": "onlinecontact.chat_count",
                    "resourceIdSuffix1": "06",
                    "resourceIdSuffix2": "07"
                }
            }, {
                "id": 658,
                "billingId": 214,
                "billingItemCode": "endusermanagement",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "endusermanagement",
                    "parentCode": "endusermanagement",
                    "baseAmount": 250000,
                    "dayAmount": 8333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.customer_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "19"
                }
            }, {
                "id": 659,
                "billingId": 214,
                "billingItemCode": "helpdoc",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "helpdoc",
                    "parentCode": "helpcenter",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.faq_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "10"
                }
            }, {
                "id": 660,
                "billingId": 214,
                "billingItemCode": "knowledge",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "knowledge",
                    "parentCode": "guide",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.knowledge_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "09"
                }
            }, {
                "id": 661,
                "billingId": 214,
                "billingItemCode": "telticket",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "telticket",
                    "parentCode": "ticket",
                    "baseAmount": 70000,
                    "dayAmount": 2333,
                    "useUserCount": true,
                    "countFree": 6000,
                    "countLevel1": 40000,
                    "countLevel1Unit": 3.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 1.5,
                    "open": true,
                    "licenceCounterName": "onlinecontact.call_licence",
                    "sumCounterName": "onlinecontact.call_seconds",
                    "resourceIdSuffix1": "02",
                    "resourceIdSuffix2": "03"
                }
            }, {
                "id": 662,
                "billingId": 214,
                "billingItemCode": "ticket",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "ticket",
                    "parentCode": "ticket",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.ticket_licence",
                    "sumCounterName": "onlinecontact.ticket_count",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "01"
                }
            }, {
                "billingItemCode": "ticketevaluation",
                "active": false,
                "billingItem": {
                    "code": "ticketevaluation",
                    "parentCode": "additional",
                    "baseAmount": 100000,
                    "dayAmount": 3333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": false,
                    "sumCounterName": "onlinecontact.ticket.evaluation_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "17"
                }
            }]
        }
    }
}
```

### 서비스 계약 상세 - 계약ID
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/{billingId}.json											
- URL (개발): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/{billingId}.json					

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|계약 ID로 계약 상세 정보 취득|HTTPS  |GET    |UTF-8|JSON    |계약 ID로 계약 상세 정보 취득|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 계약 상세 정보	|billingId	|Long	|O	|계약ID|

#### Request URL
```
/openapi/v1/admin/billing/214.json
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|계약 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |organizationId	|String	|O	|조직 ID|
|	              |type	          |Int	  |O	|서비스 타입(1:상담관리, 2:이슈관리), 기본 값:1|
|	              |status	        |String	|O	|계약 상태(작성중:create, 이용중:inuse, 이용중지:pause, 삭제:stop|
|	              |startDt	      |String	|O	|서비스 이용 시작일(한국시간)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|할인률(%)|
|	              |freeExtension	|Int	  |O	|무료체험 기간 연장 날짜|
|	              |active	        |Boolean	|O	|서비스 계약(활성화:true, 비활성화:false)|
|	              |freeTrial	    |Boolean	|O	|무료체험 기간(예:true, 아니오:false)|
|	              |billingSettings	|List	  |O	|계약항목 설정 리스트|
|	              |    id	              |Long		|O  |계약항목 설정 ID|
|	              |    billingId	      |Long	  |O	|계약 ID|
|	              |    billingSettingCode	|String	|O	|항목Code|
|	              |    active	            |Boolean	|O	|활성화:true, 비활성화:false|
|	              |    billingItem	      |Object	  |X	|유료 서비스 항목 상세|
|	              |        code	              |String	  |O	|항목Code|
|	              |        open	              |Boolean	|O	|활성화:true, 비활성화:false|

#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "content": {
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000,
            "freeTrial": false,
            "billingSettings": [{
                "id": 656,
                "billingId": 214,
                "billingItemCode": "callback",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "callback",
                    "parentCode": "additional",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "",
                    "sumCounterName": "onlinecontact.callback_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "14"
                }
            }, {
                "id": 657,
                "billingId": 214,
                "billingItemCode": "chat",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "chat",
                    "parentCode": "chat",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.chat_lisence",
                    "sumCounterName": "onlinecontact.chat_count",
                    "resourceIdSuffix1": "06",
                    "resourceIdSuffix2": "07"
                }
            }, {
                "id": 658,
                "billingId": 214,
                "billingItemCode": "endusermanagement",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "endusermanagement",
                    "parentCode": "endusermanagement",
                    "baseAmount": 250000,
                    "dayAmount": 8333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.customer_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "19"
                }
            }, {
                "id": 659,
                "billingId": 214,
                "billingItemCode": "helpdoc",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "helpdoc",
                    "parentCode": "helpcenter",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.faq_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "10"
                }
            }, {
                "id": 660,
                "billingId": 214,
                "billingItemCode": "knowledge",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "knowledge",
                    "parentCode": "guide",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.knowledge_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "09"
                }
            }, {
                "id": 661,
                "billingId": 214,
                "billingItemCode": "telticket",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "telticket",
                    "parentCode": "ticket",
                    "baseAmount": 70000,
                    "dayAmount": 2333,
                    "useUserCount": true,
                    "countFree": 6000,
                    "countLevel1": 40000,
                    "countLevel1Unit": 3.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 1.5,
                    "open": true,
                    "licenceCounterName": "onlinecontact.call_licence",
                    "sumCounterName": "onlinecontact.call_seconds",
                    "resourceIdSuffix1": "02",
                    "resourceIdSuffix2": "03"
                }
            }, {
                "id": 662,
                "billingId": 214,
                "billingItemCode": "ticket",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "ticket",
                    "parentCode": "ticket",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.ticket_licence",
                    "sumCounterName": "onlinecontact.ticket_count",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "01"
                }
            }, {
                "billingItemCode": "ticketevaluation",
                "active": false,
                "billingItem": {
                    "code": "ticketevaluation",
                    "parentCode": "additional",
                    "baseAmount": 100000,
                    "dayAmount": 3333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": false,
                    "sumCounterName": "onlinecontact.ticket.evaluation_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "17"
                }
            }]
        }
    }
}
```
