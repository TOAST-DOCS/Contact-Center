## Contact Center > Online Contact > API 가이드 > 접수유형 관리
### 접수유형 추가
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/add.json			
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/add.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|접수유형 추가  |HTTPS  |POST    |UTF-8|JSON    |신규 접수유형 추가|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|접수유형 정보	|request body	|String	|O	|접수유형 정보（JSON)|
|	             |name	|String	|O	|접수유형명（유일한 값:예; 길이:min = 0, max = 50; 형식:^(\_\|-\|[^\\pP])+$）|
|	             |orderNo	|Int	|X	|접수유형 노출 순서（기본 값:0）|

#### Request Body
```
{
    "name":"bug",
    "orderNo":1
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|----|---|
|result.content	|categoryId	|Int	|O	|접수유형 ID|
|             	|serviceId	|String	|O	|서비스 ID|
|	              |parent	|Int	|X	|상위 접수유형 ID（고정 값:0）|
|	              |name	|String	|O	|접수유형 명|
|	              |level	|Int	|X	|뎁스（고정 값:1）|
|	              |path	|String	|X	|뎁스 경로（고정 값:"\\\\"）|
|	              |orderNo	|Int	|X	|접수유형 노출 순서（기본 값:0）|
|	              |createdDt	|Long	|X	|접수유형 생성시간|
|	              |updatedDt	|Long	|X	|접수유형 업데이트 시간|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"bug",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1586830915532,
            "updatedDt":1586830915532
        }
    }
}
```

### 접수유형 상세
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|접수유형 상세  |HTTPS  |GET    |UTF-8|JSON    |접수유형 아이디를 통해 접수유형 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|접수유형 ID	|categoryid	|Int	|O	|접수유형 ID，URL PATH 내에 설정한 {categoryid}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result.content	|categoryId	|Int	|O	|접수유형 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |parent	|Int	|X	|상위 접수유형 ID（고정 값:0）|
|	              |name	|String	|O	|접수유형 명|
|           	  |level	|Int	|X	|뎁스（고정 값:1）|
|	              |path	|String	|X	|뎁스 경로（고정 값:"\\\\"）|
|	              |orderNo	|Int	|X	|접수유형 노출 순서（기본 값:0）|
|	              |createdDt	|Long	|X	|접수유형 생성시간|
|	              |updatedDt	|Long	|X	|접수유형 업데이트 시간|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"bug",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1586830915532,
            "updatedDt":1586830915532
        }
    }
}

```

### 접수유형 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|접수유형 수정  |HTTPS  |PUT    |UTF-8|JSON    |접수유형 아이디를 통해 접수유형 수정|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|접수유형 ID	|categoryid	|Int	|O	|접수유형 ID，URL PATH 내에 설정한 {categoryid}|
|접수유형 정보	|request body	|String	|O	|접수유형 정보（JSON）|
|	             |name	|String	|O	|접수유형 명（유일한 값:예; 길이:min = 0, max = 50; 형식:^(\_\|-\|[^\\pP])+$|
|              |orderNo	|Int	|X	|접수유형 노출 순서（기본 값:0）|

#### Request Body
```
{
    "name":"bug",
    "orderNo":1
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result.content	|categoryId	|Int	|O	|접수유형 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |name	|String	|O	|접수유형 명|
|	              |orderNo	|Int	|X	|접수유형 노출 순서（기본 값:0）|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "name":"bug",
            "orderNo":1
        }
    }
}
```

### 접수유형 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|접수유형 삭제  |HTTPS  |DELETE    |UTF-8|JSON    |접수유형 아이디를 통해 접수유형 삭제|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|접수유형 ID	|categoryid	|Int	|O	|접수유형 ID，URL PATH 내에 설정한 {categoryid}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result|		|	|X	|null:삭제 성공|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":null
}
```

### 접수유형 목록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/list.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/list.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|접수유형 목록 |HTTPS  |GET    |UTF-8|JSON    |서비스 내 접수유형 목록 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result.contents	|categoryId	|Int	|O	|접수유형 ID|
|                 |serviceId	|String	|O	|서비스 ID|
|	                |parent	|Int	|X	|상위 접수유형 ID（고정 값:0）|
|	                |name	|String	|O	|접수유형 명|
|	                |level	|Int	|X	|뎁스（고정 값:1）|
|	                |path	|String	|X	|뎁스 경로（고정 값:"\\\\"）|
|	                |orderNo	|Int	|X	|접수유형 노출 순서（기본 값:0）|
|	                |createdDt	|Long	|X	|접수유형 생성시간|
|	                |updatedDt	|Long	|X	|접수유형 업데이트 시간|

- 리스트 순서는 order by orderNo, name asc

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
                "categoryId":1571,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"help",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1586835618000,
                "updatedDt":1586835618000
            },
            {
                "categoryId":1570,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"chat",
                "level":1,
                "path":"\\",
                "orderNo":1,
                "createdDt":1586835599000,
                "updatedDt":1586835599000
            },
            {
                "categoryId":1567,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"bug",
                "level":1,
                "path":"\\",
                "orderNo":3,
                "createdDt":1586830916000,
                "updatedDt":1586841262000
            }
        ]
    }
}
```
