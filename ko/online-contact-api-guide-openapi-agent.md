## Contact Center > Online Contact > API 가이드 > 상담원 관리
### 상담원 리스트 취득
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com /{serviceId}/openapi/v1/users.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/users.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|상담원 리스트 취득|HTTPS  |GET    |UTF-8|JSON    |상담원 리스트 취득|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에  설정한 {serviceId}|
|사용자 권한	|role	|String	|X	|ROLE_FRONT_ADMIN : 관리자, ROLE_FRONT_AGENT : 일반 상담원|
|사용자 명	|name	|String	|X	|사용자 명칭|
|페이지 수	|page	|Int	|X	|디폴트 값 = 1|
|페이지 노출 건수	|pageSize	|Int	|X	|디폴트 값 = 10|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|----|----|
|result.contents	|userId	|INT	|O	|사용자 ID|
|	                |usercode	|String	|O	|사용자 Code|
|	                |uuid	|String	|O	|IAM |사용자 ID|
|	                |username	|String	|O	|사용자 명|
|	                |role	|String	|O	|사용자 권한. ROLE_FRONT_ADMIN : 관리자, ROLE_FRONT_AGENT : 일반 상담원|

#### Response Body
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "contents": [
      {
        "userId": 10058,
        "usercode": "he.ronggang",
        "username": "赫荣刚",
        "uuid": "ef1bd956-6c13-4391-8256-1eb0d840355a",

        "role": "ROLE_FRONT_ADMIN",
      }
    ]
  }
}
```

### 상담원 정보 취득
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com /{serviceId}/openapi/v1/users/{id}.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/users/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|상담원 정보 취득|HTTPS  |GET    |UTF-8|JSON    |상담원 ID를 통해 상담원 정보 취득|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|사용자 ID	|id	|INT	|O	|URL PATH 내에 설정한 {id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result.contents	|userId	|INT	|O	|사용자ID|
|	                |usercode	|String	|O	|사용자 Code|
|	                |uuid	|String	|O	|IAM 사용자 ID|
|	                |username	|String	|O	|사용자 명|
|	                |role	|String	|O	|사용자 권한. ROLE_FRONT_ADMIN : 관리자, ROLE_FRONT_AGENT : 일반 상담원|

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
        "userId": 10058,
        "usercode": "he.ronggang",
        "username": "赫荣刚",
        ""uuid"": ""ef1bd956-6c13-4391-8256-1eb0d840355a"",
        "role": "ROLE_FRONT_ADMIN",
      }
    }
  }
}
```
