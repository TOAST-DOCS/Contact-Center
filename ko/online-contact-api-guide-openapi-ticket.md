## Contact Center > Online Contact > API 가이드 > 티켓 관리

### 티켓 생성
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|티켓 생성  |HTTPS  |POST    |UTF-8|JSON    |신규 티켓 생성|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	     |String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|티켓 정보 |request body	|String	|O	|티켓 정보（JSON)|
|    	     |categoryId	|Int	|X	|접수유형 ID，없을 경우 지정하지 않아도 됨|
|   	     |subject	    |String	|O	|티켓 제목（max=255）|
|          |content	        |String	|O	|티켓 내용|
| 	       |endUser.usercode	|String	|O	|유저 코드（유일한 값). 비회원 문의로 해당 값이 없을 경우 이메일+이름+전화번호 등 형태로 유일한 값을 생성|
|	         |endUser.email	    |String	|X	|유저 이메일（티켓 처리 시 해당 이메일로 답변이 발송 됨. 없을 경우 메일이 발송되지 않음). Online Contact에서 티켓 처리 시 필수 항목|
|	         |endUser.username	|String	|X	|유저 명|
|          |endUser.phone	    |String	|X	|유저 전화번호|
|	         |addition	        |String	|X	|기본 필드 외에 추가 된 필드 정보|
|            |status	        |String	|X	|값 : open(처리중), new(미할당). 기본 값 : open(처리중)|
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
    "status":"new" ,
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
|result.content	|ticketId	    |String	|O	|티켓 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |subject	    |String	|O	|티켓 제목|
|	              |categoryId	|Int	|X	|접수유형 ID|
|               |categoryName	|String	|X	|접수유형 명|
|	              |status	    |String	|O	|티켓 상태 (new : 미힐당, open : 처리중, closed:처리 완료)|
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

### 전화티켓 생성
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/call.json		
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/call.json		

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|전화티켓 생성|HTTPS  |PUT     |UTF-8|JSON    |Mobile Contact APP을 통한 전화 티켓 생성|공통인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|서비스ID	|serviceId	|String	|O	|서비스ID，URL PATH중 {serviceId}에 설정|
|전화티켓 정보	|request body	|String	|O	|전화티켓 정보（JSON）|
|	             |subject	     |String(255)	|O	|Online Contact 티켓 제목|
|	             |content	     |String	        |O	|Online Contact 티켓 내용|
|	             |requesterId	|Integer	|O	|CTI 상담원 ID (CTI 측 agentid)|
|	             |endUser.phone	|String	        |O	|고객 전화번호|
|	             |endUser.username	|String		|X      |고객 이름（이메일 입력 시 해당 항목 반드시 입력 필요）|
|	             |endUser.email	|String		|X      |고객 이메일|
|	             |ticketCall.inoutFlg	|String	|O	|전화 유형 (in:인입, out:발신)|
|	             |ticketCall.ivrPathNo	|String	|O	|전화 ivr 경로|
|	             |ticketCall.disconnectCd	|String	|O	|전화 종료구분 (agent: 상담원 끊기，block: 강성 종료，customer: 고객 끊기)|
|	             |ticketCall.callRingKey	|String	|O	|전화 UCID|
|	             |ticketCall.callRingDt	|String(14)	|O	|전화 울림시간 (UTC timestamp시간)|
|	             |ticketCall.callStartDt	|String(14)	|O	|상담 시작일시 (UTC timestamp시간)|
|	             |ticketCall.callEndDt	|String(14)	|O	|상담 종료일시 (UTC timestamp시간)|

#### Request Body
```
{	
    "subject":"test1",	
    "content":"12312312313",	
    "requesterId":2020112233,	
    "endUser":{	
         "phone":"01012345678",	
         "username":"test",	
         "email":"test@test.com"	
    },	
    "ticketCall":{	
         "inoutFlg":"in",	
         "ivrPathNo":"70556",	
         "disconnectCd":"agent",	
         "callRingKey":"BC9E3D2B-B42E-4555-81EF-62E9680C4A37",	
         "callRingDt":"20210101120000",	
         "callStartDt":"20210101120000",	
         "callEndDt":"20210101120000"	
    },	
}	
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|--------|----|
|result.content	|ticketId	|String	 |	|생성된 티켓 ID|
|	        |code	        |String	 |	|호출 결과 (success: 성공, error: 실패)|
|	        |message	|String	 |	|실패 메시지, 성공 시 null|

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
            "code":"success",	
            "message":null	
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

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|티켓 ID	|id	|String	|O	|티켓 ID|
|티켓 처리 유형	|type	|String	|X	|티켓 처리유형 (new : 미할당, open : 처리중, reply : 보류, solved : 해결, closed : 완료). 티켓 해결 후 완료처리 가능|
|답변 내용	|comment	|String	|X	|Request Body로 제출한 {"comment":"답변내용"}|
|티켓 처리자 명	|assigneeName	|String	|X	|티켓 처리자 , 기본 값 : null|
|첨부파일	|attachments	|String	|X	|첨부파일 ID（형식（파일 ID는 ,로 분리）：파일ID1,파일ID2,…,파일IDn）|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result.content	|id	|String	|O	|티켓 ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |subject	|String	|O	|티켓 제목|
|	              |categoryId	|Int	|X	|접수유형 ID|
|	              |categoryName	|String	|X	|접수유형 명|
|	              |status	|String	|O	|티켓 상태（new : 미할당, open : 처리중, reply : 보류, solved : 해결, closed : 완료）|
|	              |endUser.usercode	|String	|O	|유저 코드（유일한 값）|
|	              |endUser.email	|String	|X	|유저 이메일（티켓 처리 시 해당 이메일로 답변이 발송 됨. 없을 경우 메일이 발송되지 않음)|
|	              |endUser.username	|String	|X	|유저 명|
|	              |endUser.phone	|String	|X	|유저 전화번호|
|	              |content	|String	|O	|티켓 문의 내용|
|               |createdDt	|Long	|O	|티켓 생성시간|
|	              |updatedDt	|Long	|O	|티켓 업데이트 시간|
|	              |contents.content	|String	|X	|티켓 처리 내용|
|                 |contents.type	|String	|X	|티켓 유형 (reply : 상담원 답변, enduser : 고객 재문의)|
|                 |contents.userName	|String	|X	|티켓 처리자/재문의 고객 명，기본 값 : null|
|	              |contents.createdDt	|Long	|X	|티켓 처리 시간|
|	              |contents.attachments	|String	|X	|티켓 처리 첨부파일 ID|
|	              |attachments[].attachmentId	|String	|X	|첨부파일 ID|
|               |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|
|               |assigneeName	|String	|X	|티켓 처리자, 기본 값 : null|

#### Request URL
```
?id=티켓ID&type=티켓 유형&assigneeName=티켓 처리자 명	
```

#### Request Body
- 형식: application/json;charset=UTF-8
```
{
   "comment":"티켓 답변 내용"
}
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
	                "type":"reply",
             	    "userName":"티켓 처리자/재문의 고객 명",
                    "createdDt":1586927311120,
                    "attachments":null
                }
            ],
            "attachments":null,
            "addition":null
            "assigneeName":"티켓 처리자 명" 
        }
    }
}
```

### 고객 재문의
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/comment.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/comment.json

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|고객 재문의  |HTTPS  |POST    |UTF-8|JSON    |티켓 아이디 기준으로 고객 재문의|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|티켓 ID	 |id	     |String	|O	|티켓 ID|
|재문의 내용	|comment	|String	  |O	|Request Body를 통해 제출. 제출 형태 : {"comment" : "재문의 내용"}|
|첨부파일	 |attachments	|String	|X	|첨부파일 ID. 형식(파일 ID는 ,로 분리) : 파일ID1, 파일ID2, … ,파일IDn|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.content	|contentId	|Long  |		|내용 ID|
|	            |ticketId	|String	|	    |티켓 ID|
|	            |type	    |String	 |	    |티켓 유형 (enduser:고객 재문의)|
|	            |content	|String	 |	    |재문의 내용|
|	            |createdDt	|Long	 |	    |재문의 시간|
| 	            |attachments	|String |		|첨부파일 ID|

#### Request URL
```
?id=티켓ID
```

#### Request Body
```
{
   "comment":"재문의 내용"
}
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
            "contentId":22891,
            "ticketId":"T1586918360295gJrtI",
            "eventId":45205,
            "type":"enduser",
            "subject":null,
            "content":"재문의 내용",
            "active":true,
            "userId":10111,
            "userName":null,
            "groupId":null,
            "groupName":null,
            "createdDt":1586927311120,
            "attachments":[]
        }
    }
}
```

### 티켓 상세
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/{id}.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|티켓 상세  |HTTPS  |GET    |UTF-8|JSON    |티켓 아이디를 통해 티켓 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|티켓 ID	|id	|String	|O	|티켓 ID，URL PATH 내에 설정한 {id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.content	|ticketId	|String	|O	|티켓 ID|
|	            |serviceId	|String	|O	|서비스 ID|
|	            |subject	|String	|O	|티켓 제목|
|	            |categoryId	|Int	|X	|접수유형 ID|
|	            |categoryName	|String	|X	|접수유형 명|
|	            |status	        |String	|O	|티켓 상태（new : 미할당, open : 처리중, reply : 보류, solved : 해결, closed : 완료）|
|	            |endUser.usercode	|String	|O	|유저 코드（유일한 값）|
|	            |endUser.email	    |String	|X	|유저 이메일（티켓 처리 시 해당 이메일로 답변이 발송 됨. 없을 경우 메일이 발송되지 않음)|
|	            |endUser.username	|String	|X	|유저 명|
|	            |endUser.phone	    |String	|X	|유저 전화번호|
|	            |content	        |String	|O	|티켓 문의 내용|
|	            |createdDt	        |Long	|O	|티켓 생성시간|
|	            |updatedDt	        |Long	|O	|티켓 업데이트 시간|
|	            |contents.content	|String	|X	|티켓 처리내용|
|               |contents.type	    |String	|X	|티켓 유형. reply : 상담원 답변, enduser : 고객 재문의|
|               |contents.userName	|String	|X	|티켓 처리자/재문의 고객 명，기본 값 : null|
|	            |contents.createdDt	|Long	|X	|티켓 처리시간|
|	            |contents.attachments.attachmentId	|String	|X	|티켓 처리 첨부파일 ID|
|	            |contents.attachments.fileName	|String	|X	|티켓 처리 첨부파일 명|
|	            |contents.attachments.contentType	|String	|X	|티켓 처리 첨부파일 유형|
|	            |contents.attachments.disposition	|String	|X	|티켓 처리 첨부파일 처리방식（attachment:첨부파일）|
|	            |contents.attachments.size	|Long	|X	|티켓 처리 첨부파일 크기|
|	            |contents.attachments.createdDt	|Long	|X	|티켓 처리 첨부파일 업로드 시간|
|	            |attachments.attachmentId	|String	|X	|티켓 문의 첨부파일 ID|
|	            |attachments.fileName	|String	|X	|티켓 문의 첨부파일 명|
|	            |attachments.contentType	|String	|X	|티켓 문의 첨부파일 유형|
|	            |attachments.disposition	|String	|X	|티켓 문의 첨부파일 처리방식（attachment:첨부파일）|
|	            |attachments.size	|Long	|X	|티켓 문의 첨부파일 크기|
|	            |attachments.createdDt	|Long	|X	|티켓 문의 첨부파일 업로드 시간|
|	            |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|
|               |assigneeName	|String	|X	|티켓 처리자 명 , 기본 값 : null|


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
            "endUser":{
                "usercode":"gamebaseuser1",
                "username":"TestUser",
                "email":"gamebaseuser1@toast.com",
                "phone":"13333333333"
            },
            "content":"I have a question for you",
            "createdDt":1586918360000,
            "updatedDt":1586927309000,
            "contents":[
                {
                    "content":"I solve it",
	                "type":"reply",
                    "userName":"티켓 처리자/재문의 고객 명",
                    "createdDt":1586927311000,
                    "attachments":[
                        {
                            "attachmentId":"bb7109b2ebd14780ae5403f17de88246",
                            "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3 (1).zip",
                            "contentType":"application/x-zip-compressed",
                            "disposition":"attachment",
                            "size":223573,
                            "createdDt":1586918795000
                        },
                        {
                            "attachmentId":"914cd0fb61934c0698655118158d84d5",
                            "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3.zip",
                            "contentType":"application/x-zip-compressed",
                            "disposition":"attachment",
                            "size":223573,
                            "createdDt":1586918801000
                        }
                    ]
                }
            ],
            "attachments":[
                {
                    "attachmentId":"5a13cbfd3c574f7dae644536d3e4159c",
                    "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3 (1).zip",
                    "contentType":"application/x-zip-compressed",
                    "disposition":"attachment",
                    "size":223573,
                    "createdDt":1586918296000
                },
                {
                    "attachmentId":"43f035ea67554ceab7f11535ee7ac5ac",
                    "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3.zip",
                    "contentType":"application/x-zip-compressed",
                    "disposition":"attachment",
                    "size":223573,
                    "createdDt":1586918300000
                }
            ],
            "addition":"{'sex':'male','age':20}"
            "assigneeName":"티켓 처리자 명"
        }
    }
}
```

### 티켓 목록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/list.json						
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/list.json				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|티켓 목록  |HTTPS  |GET    |UTF-8|JSON    |검색 조건을 통해 조건에 맞는 티켓 목록 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|시작시간	|startDt	|String	|X	|검색 범위 시작시간(티켓 생성시간)(형식:yyyyMMddHHmmss）|
|종료시간	|endDt	|String	|X	|검색 범위 종료시간(티켓 생성시간)(형식:yyyyMMddHHmmss）|
|티켓 ID	|ticketId	|String	|X	|티켓 ID|
|제목	|subject	|String	|X	|제목|
|티켓 상태	|status	|String	|X	|티켓 상태（new : 미할당, open : 처리중, reply : 보류, solved : 해결, closed : 완료）|
|접수유형	|categoryId	|Int	|X	|접수유형 ID（ID가 여러개 일 경우 , 로 분리）|
|유저 코드	|usercode	|String	|X	|유저 코드（유일한 값）|
|유저 명	|username	|String	|X	|유저 명|
|유저 이메일	|email	  |String	|X	|유저 이메일|
|정렬 순서	|sort	   |String	|X	|정렬 순서(기본값:updatedDt:desc; 형식 변수:정렬（오름차순:asc, 내림차순:desc))|
|페이지	|page	    |Int	|X	|기본 값:1|
|1페이지 노출 건수	|pageSize	|Int	|X	|기본 값:10;max=200|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.contents	|ticketId	|String	|O	|티켓 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |subject	|String	|O	|티켓 제목|
|	                |categoryId	|Int	|X	|접수유형 ID|
|	                |categoryName	|String	|X	|접수유형 명|
|	                |status	|String	|O	|티켓 상태（new : 미할당, open : 처리중, reply : 보류, solved : 해결, closed : 완료）|
|	                |createdDt	|Long	|O	|티켓 생성시간|
|	                |updatedDt	|Long	|O	|티켓 업데이트 시간|
|	                |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|
|result.total	|total	        |Long	|O	|총 건수|
|result.pages	|pages	        |Int	|O	|총 페이지수|
|result.pageNum	|pageNum	    |Int	|O	|현재 페이지|
|result.pageSize	|pageSize	|Int	|O	|1페이지 노출 건수|

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
                "ticketId":"T1586918360295gJrtI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586918360000,
                "updatedDt":1586927309000,
                "addition":null
            },
            {
                "ticketId":"T1586915418254WQQM9",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586915418000,
                "updatedDt":1586915505000,
                "addition":null
            },
            {
                "ticketId":"T1586914789452LJEcI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586914789000,
                "updatedDt":1586915162000,
                "addition":null
            },
            {
                "ticketId":"T1586846795949Ij1xA",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846796000,
                "updatedDt":1586852906000,
                "addition":null
            },
            {
                "ticketId":"T1586846821052WKmoK",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846821000,
                "updatedDt":1586852382000,
                "addition":null
            },
            {
                "ticketId":"T1586849274901SZ94B",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586849275000,
                "updatedDt":1586851357000,
                "addition":null
            }
        ],
        "total":6,
        "pages":1,
        "pageNum":1,
        "pageSize":10
    }
}
```

### 유저 티켓 목록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/{usercode}/list.json							
- URL (개발):	https://{domain}.alpha-oc.toast.co/{serviceId}/openapi/v1/ticket/{usercode}/list.json						

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|유저 티켓 목록 |HTTPS  |GET    |UTF-8|JSON    |검색 조건을 통해 조건에 맞는 사용자의 티켓 목록 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	 |String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|유저 코드	|usercode	|String	|O	|유저 코드(유일한 값)，URL PATH 내에 설정한{usercode}|
|시작시간	|startDt	|String	|X	|검색 범위 시작시간(티켓 생성시간)(형식:yyyyMMddHHmmss）|
|종료시간	|endDt	    |String	|X	|검색 범위 종료시간(티켓 생성시간)(형식:yyyyMMddHHmmss）|
|티켓 ID	|ticketId	  |String	|X	|티켓 ID|
|제목	|subject	      |String	|X	|제목|
|티켓 상태	|status	    |String	|X	|티켓 상태（new : 미할당, open : 처리중, reply : 보류, solved : 해결, closed : 완료）|
|접수유형	|categoryId	|Int	|X	|접수유형 ID（ID가 여러개 일 경우 , 로 분리）|
|정렬방식	|sort	    |String	|X	|정렬 순서(기본값:updatedDt:desc; 형식 변수:정렬（오름차순:asc, 내림차순:desc))|
|페이지	|page	     |Int	|X	|기본 값:1|
|1페이지 노출 건수	|pageSize	|Int	|X	|기본 값:10;max=200|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.contents	|ticketId	|String	|O	|티켓 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |subject	|String	|O	|티켓 제목|
|	                |categoryId	|Int	|X	|접수유형 ID|
|	                |categoryName	|String	|X	|접수유형 명|
|	                |status	|String	|O	|티켓 상태（new : 미할당, open : 처리중, reply : 보류, solved : 해결, closed : 완료）|
|                   |createdDt	|Long	|O	|티켓 생성시간|
|	                |updatedDt	|Long	|O	|티켓 업데이트 시간|
|	                |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|
|result.total	    |total	|Long	|O	|총 건수|
|result.pages	    |pages	|Int	|O	|총 페이지수|
|result.pageNum	    |pageNum	|Int	|O	|현재 페이지|
|result.pageSize	|pageSize	|Int	|O	|1페이지 노출 건수|

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
                "ticketId":"T1586918360295gJrtI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586918360000,
                "updatedDt":1586927309000,
                "addition":null
            },
            {
                "ticketId":"T1586915418254WQQM9",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586915418000,
                "updatedDt":1586915505000,
                "addition":null
            },
            {
                "ticketId":"T1586914789452LJEcI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586914789000,
                "updatedDt":1586915162000,
                "addition":null
            },
            {
                "ticketId":"T1586846795949Ij1xA",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846796000,
                "updatedDt":1586852906000,
                "addition":null
            },
            {
                "ticketId":"T1586846821052WKmoK",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846821000,
                "updatedDt":1586852382000,
                "addition":null
            },
            {
                "ticketId":"T1586849274901SZ94B",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586849275000,
                "updatedDt":1586851357000,
                "addition":null
            }
        ],
        "total":6,
        "pages":1,
        "pageNum":1,
        "pageSize":10
    }
}
```

### 티켓 첨부파일 첨부
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json			 							
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json									

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|첨부파일 첨부  |HTTPS  |GET    |UTF-8|JSON    |서버에 파일 업로드			|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|첨부한 파일	|file	|File	|O	|첨부한 파일은 form 형태로 제출|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|첨부한 파일 ID|
|	            |fileName	    |String	|O	|파일 명|
|	            |contentType	|String	|O	|파일 유형|
|	            |disposition	|String	|O	|파일 처리방식（attachment:첨부파일）|
|	            |size	|Long	|O	|파일 크기|
|               |createdDt	|Long	|O	|파일 첨부 시간|

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
            "attachmentId":"e5f0eab5cf694d4fb356c21a9bdaee48",
            "fileName":"1.jpeg",
            "contentType":"image/jpeg",
            "disposition":"attachment",
            "size":40375,
            "createdDt":null
        }
    }
}
```

### 티켓 첨부파일 열기/다운로드
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}					 							
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}												

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|첨부파일 열기/다운로드  |HTTPS  |GET    |UTF-8|JSON    |서버에 업로드된 파일 열기/다운로드|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|첨부한 파일 ID	|id	|String	|O	|첨부한 파일 id| 
|처리방식	|type	|String	|X	|기본 값은 브라우저로 열기（download:다운, open:브라우저로 열기）|

#### 결과 데이터
- 없음

#### Response Body
- File

### 티켓 첨부파일 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json						 							
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json														

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|첨부파일 삭제  |HTTPS  |DELETE    |UTF-8|JSON    |서버에 업로드된 파일 삭제|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|첨부한 파일 ID	 |id	|String	|O	|첨부한 파일 id|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|첨부한 파일 id| 
|	            |fileName	|String	|O	|파일 명|
|	            |contentType	|String	|O	|파일 유형|
|	            |size	|Long	|O	|파일 크기|

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
            "attachmentId":"e5f0eab5cf694d4fb356c21a9bdaee48",
            "fileName":"1.jpeg",
            "contentType":"image/jpeg",
            "disposition":"attachment",
            "size":40375,
            "createdDt":1586849962000a
        }
    }
}
```
