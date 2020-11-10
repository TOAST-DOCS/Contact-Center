## Contact Center > Online Contact > API 가이드 > 티켓 관리
### 티켓 생성
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|티켓 생성  |HTTPS  |POST    |UTF-8|JSON    |신규 티켓 생성|공통 인증   |

|담당자 이름	|담당자 이메일	|담당자 부서	|
|-----------|--------------|-----------|
|徐凯|xu_kai@nhn-st.com|CS Development Part|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|티켓 정보 |request body	|String	|O	|티켓 정보（JSON)|
|    	     |categoryId	|int	|X	|접수유형 ID，없을 경우 지정하지 않아도 됨|
|   	     |subject	|String	|O	|티켓 제목（max=255）|
|          |content	|String	|O	|티켓 내용|
| 	       |endUser.usercode	|String	|O	|유저 코드（유일한 값）|
|	         |endUser.email	|String	|X	|유저 이메일（티켓 처리 시 해당 이메일로 답변이 발송 됨. 없을 경우 메일이 발송되지 않음)|
|	         |endUser.username	|String	|X	|유저 명|
|          |endUser.phone	|String	|X	|유저 전화번호|
|	         |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|
|	         |attachments[].attachmentId	|String	|X	|첨부파일 ID

#### Request Body
```
{
    "categoryId":1567,
    "subject":"This is a new ticket",
    "content":"I have a question for you",
    "endUser":{
        "usercode":"gamebaseuser1",
        "username":"TestUser",
        "email":"gamebaseuser1@toast.com",
        "phone":"13333333333"
    },
    "addition":"{'sex':'male','age':20}" ,
    "attachments":[
       {
            "attachmentId":"5a13cbfd3c574f7dae644536d3e4159c"
        },
       {
            "attachmentId":"43f035ea67554ceab7f11535ee7ac5ac"
        }
    ]
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result.content	|ticketId	|String	|O	|티켓 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |subject	|String	|O	|티켓 제목|
|	              |categoryId	|int	|X	|접수유형 ID|
|               |categoryName	|String	|X	|접수유형 명|
|	              |status	|String	|O	|티켓 상태（open:신규 티켓; closed:처리 완료）|
|	              |endUser.usercode	|String	|O	|유저 코드（유일한 값）|
|	              |endUser.email	|String	|X	|유저 이메일（티켓 처리 시 해당 이메일로 답변이 발송 됨. 없을 경우 메일이 발송되지 않음)|
|	              |endUser.username	|String	|X	|유저 명|
|	              |endUser.phone	|String	|X	|유저 전화번호|
| 	            |content	|String	|O	|티켓 문의 내용|
|	              |createdDt	|Long	|O	|티켓 생성시간|
|	              |updatedDt	|Long	|O	|티켓 업데이트 시간|
|               |contents	|String	|X	|티켓 처리 정보|
|	              |attachments[].attachmentId	|String	|X	|첨부파일 ID|
|	              |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|

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
            "ticketId":"T1586918360295gJrtI",
            "serviceId":"GameBaseService",
            "subject":"This is a new ticket",
            "categoryId":1567,
            "categoryName":null,
            "status":"open",
            "endUser":{
                "usercode":"gamebaseuser1",
                "username":"TestUser",
                "email":"gamebaseuser1@toast.com",
                "phone":"13333333333"
            },
            "content":"I have a question for you",
            "createdDt":1586918360291,
            "updatedDt":1586918360291,
            "contents":null,
            "attachments":[
                {
                    "attachmentId":"5a13cbfd3c574f7dae644536d3e4159c",
                    "fileName":null,
                    "contentType":null,
                    "disposition":null,
                    "size":null,
                    "createdDt":null
                },
                {
                    "attachmentId":"43f035ea67554ceab7f11535ee7ac5ac",
                    "fileName":null,
                    "contentType":null,
                    "disposition":null,
                    "size":null,
                    "createdDt":null
                }
            ],
            "addition":"{'sex':'male','age':20}"
        }
    }
}
```

### 티켓 처리
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/solve.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/solve.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|티켓 처리  |HTTPS  |POST    |UTF-8|JSON    |티켓 아이디를 통해 티켓 처리|공통 인증   |

|담당자 이름	|담당자 이메일	|담당자 부서	|
|-----------|--------------|-----------|
|徐凯|xu_kai@nhn-st.com|CS Development Part|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|티켓 ID	|id	|String	|O	|티켓 ID|
|첨부파일	|attachments	|String	|X	|첨부파일 ID（형식（파일 ID는 ,로 분리）：파일ID1,파일ID2,…,파일IDn）|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result.content	|id	|String	|O	|티켓 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |subject	|String	|O	|티켓 제목|
|	              |categoryId	|int	|X	|접수유형 ID|
|	              |categoryName	|String	|X	|접수유형 명|
|	              |status	|String	|O	|티켓 상태（open:신규티켓; closed:처리완료）|
|	              |endUser.usercode	|String	|O	|유저 코드（유일한 값）|
|	              |endUser.email	|String	|X	|유저 이메일（티켓 처리 시 해당 이메일로 답변이 발송 됨. 없을 경우 메일이 발송되지 않음)|
|	              |endUser.username	|String	|X	|유저 명|
|	              |endUser.phone	|String	|X	|유저 전화번호|
|	              |content	|String	|O	|티켓 문의 내용|
|               |createdDt	|Long	|O	|티켓 생성시간|
|	              |updatedDt	|Long	|O	|티켓 업데이트 시간|
|	              |contents.content	|String	|X	|티켓 처리 내용|
|	              |contents.createdDt	|Long	|X	|티켓 처리 시간|
|	              |contents.attachments	|String	|X	|티켓 처리 첨부파일 ID|
|	              |attachments[].attachmentId	|String	|X	|첨부파일 ID|
|               |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|

#### Request Body
- 형식: application/json;charset=UTF-8
```
{"comment":"comment content.XXXXXXXXX"}
```

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
            "ticketId":"T1586918360295gJrtI",
            "serviceId":"GameBaseService",
            "subject":"This is a new ticket",
            "categoryId":1567,
            "categoryName":"bug",
            "status":"closed",
            "endUser":null,
            "content":null,
            "createdDt":1586918360000,
            "updatedDt":1586927308531,
            "contents":[
                {
                    "content":"I solve it",
                    "createdDt":1586927311120,
                    "attachments":null
                }
            ],
            "attachments":null,
            "addition":null
        }
    }
}
```
