## Contact Center > Online Contact > API Guide for Developers > Email Set-up

### Create representative account
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/create.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/create.json				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Create representative account|HTTPS  |POST    |UTF-8|JSON    |Create service representative account. (Cannot be modified after creation) Format: \*\*@oc.toast.com|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Email information	|mail	|String	|O	|Email information(Example:'mail' part of mail@oc.toast.com)|

#### Query String
- mail=mail

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|result.content	|displayMail	|String	|	  |Sender address|
|	              |external	    |String	|	  |List of external accounts|
|	              |mail	        |String	|O	|Address of representative account : mail@oc.toast.com|
|	              |name	        |String	|	  |Sender name|
|	              |template	    |String	|	  |Email format|
|	              |updatedDt	  |Long	  |	  |Updated time|

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
            "displayMail":"noreply@toast.com",
            "external":{},
            "mail":"mail@oc.toast.com",
            "name":"noreply",
            "template":"<p>#{content}</p>",
            "updatedDt":1597369998000
        }
    }
}
```

### Query email information
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Query email information|HTTPS  |GET    |UTF-8|JSON    |View all email information in the service|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|-----------|-----|----|
|result.content	|displayMail	|String	|	  |Sender address|
|	              |external	    |String	|	  |List of external accounts|
|	              |mail	        |String	|O	|Address of representative account : mail@oc.toast.com|
|	              |name	        |String	|	  |Sender name|
|	              |template	    |String	|	  |Email format|
|	              |updatedDt	  |Long	  |	  |Updated time|

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
            "displayMail":"noreply@toast.com",
            "external":{},
            "mail":"mail@oc.toast.com",
            "name":"noreply",
            "template":"<p>#{content}</p>",
            "updatedDt":1597371255000
        }
    }
}
```

### Check Validation of External Account
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/verify.json					
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/verify.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Check validation of external account|HTTPS  |POST    |UTF-8|JSON    |Check validation of external account|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|External Account Information	|request body	|String	  |O	|External account information(JSON)|
|	             |id	         |Integer	 |   |External account ID (Not required when creating new account, only for modification)|
|	             |name	       |String	 |O	 |External account name for differentiation(Length:min=1, max=20)|
|	             |active	     |Boolean	 |O	 |External account status(true:Enable ,false:Disable), Only required for modification|
|	             |host	       |String	 |O	 |Mail server|
|	             |port	       |Integer  |O	 |Port(Example:993)|
|	             |ssl	         |Boolean	 |O	 |SSL usage(true:use, false:do not use)|
|	             |mail	       |String	 |O	 |External account address(Precise email address)|
|	             |password	   |String	 |O	 |External account password(The email address and password you entered during your subscription will be retained.)|
|	             |mailDel   	 |Boolean	 |O	 |Use Leave Source feature(true:Delete(Email will be automatically deleted when converted to ticket）,false:Hold)|

#### Request Body
```
{
    "id":21,
    "name":"octest1",
    "active":true
    "host":"imap.163.com",
    "port":993,
    "ssl":true
    "mail":"octest1@163.com",
    "password":"yourpassword",
    "mailDel":false
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-------|--------|-------------|-----|---|
|result	|content	|String    	 |O	   |SUCCESS(success)|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
         "content":"SUCCESS",
    }
}
```

### Register External Account
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Register External Account|HTTPS|POST|UTF-8|JSON|Register External Account(Can register after validation checked)|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|External Account Information	|request body	|String	  |O	|External account information(JSON)|
|	             |name	       |String	 |O	 |External account name for differentiation(Length:min=1, max=20)|
|	             |host	       |String	 |O	 |Mail server|
|	             |port	       |Integer  |O	 |Port(Example:993)|
|	             |ssl	         |Boolean	 |O	 |SSL usage(true:use, false:do not use)|
|	             |mail	       |String	 |O	 |External account address(Precise email address)|
|	             |password	   |String	 |O	 |External account password(The email address and password you entered during your subscription will be retained.)|
|	             |mailDel   	 |Boolean	 |O	 |Use Leave Source feature(true:Delete(Email will be automatically deleted when converted to ticket）,false:Hold)|

#### Request Body
```
{
    "name":"octest1",
    "host":"imap.163.com",
    "port":993,
    "ssl":true
    "mail":"octest1@163.com",
    "password":"yourpassword",
    "mailDel":false
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|result.content	|id	      |Integer	|	  |외부계정 ID|
|               |name	    |String	  |O	|외부계정 구분 명칭|
|	              |active	  |Boolean	|O	|외부계정 상태(고정 값:true)|
|	              |host	    |String	  |O	|메일 서버|
|	              |port	    |Integer	|O	|포트(예:993)|
|               |ssl	    |Boolean	|O	|ssl 사용여부(true:사용,false:미사용)|
|	              |mail	    |String	  |O	|외부계정 주소|
|	              |password	|String	  |O	|외부계정 비밀번호|
|	              |mailDel	|Boolean	|O	|원본 남기기 기능 사용 여부(true:삭제,false:보류)|
|	              |createdDt	|Long	  |	  |생성시간|
|	              |updatedDt	|Long   |		|수정시간|

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
            "id":16,
            "name":"octest1",
            "active":true
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "password":"********",
            "mailDel":false,
            "createdDt":1597382469685,
            "updatedDt":1597382469685
        }
    }
}
```

### 외부계정 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json					
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|외부계정 수정|HTTPS|PUT|UTF-8|JSON|외부계정 수정(유효성 체크 후 수정 가능)|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|---|
|서비스 ID	     |serviceId	    |String	  |O	  |서비스 ID，URL PATH 내에 설정한{serviceId}|
|외부계정 ID	   |id	         |Integer   |O	 |외부계정 ID,URL PATH내에 설정된 {id}|
|외부계정 정보	 |request body	|String	  |O	  |외부계정 정보(JSON)|
|	              |name	         |String	 |O	   |외부계정 구분 명칭(길이:min=1, max=20)|
|	              |active	       |Boolean	 |	   |외부계정 상태(true:활성화,false:비활성화)|
|	              |host	         |String	 |O	   |메일 서버|
|	              |port	         |Integer	 |O	   |포트(예:993)|
|	              |ssl	         |Boolean	 |O	   |ssl 사용여부(true:사용,false:미사용)|
|	              |mail	         |String	 |O	   |외부계정 주소(정확한 이메일 주소)|
|	              |password	     |String	 |O	   |외부계정 비밀번호(서비스를 이용하는 기간 동안 입력한 이메일 주소와 비밀번호가 보관됩니다.)|
|	              |mailDel	     |Boolean	 |O	   |원본 남기기 기능 사용 여부(true:삭제(이메일이 티켓으로 전환되면 해당 이메일이 자동으로 삭제 됨）,false:보류)|

#### Request Body
```
{
    "name":"octest1",
    "host":"imap.163.com",
    "port":993,
    "ssl":true
    "mail":"octest1@163.com",
    "password":"yourpassword",
    "mailDel":false
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|----|----|
|result.content	|id	    |Integer	|	  |외부계정 ID|
|               |name	  |String	  |O	|외부계정 구분 명칭|
|	              |active	|Boolean	|O	|외부계정 상태(true:활성화,false:비활성화)|
|	              |host	  |String	  |O	|메일 서버|
|               |port	  |Integer	|O	|포트(예:993)|
|               |ssl	  |Boolean	|O	|ssl 사용여부(true:사용,false:미사용)|
|	              |mail	  |String	  |O	|외부계정 주소|
|	              |password	|String	|O	|외부계정 비밀번호|
|	              |mailDel	|Boolean	|O	|원본 남기기 기능 사용 여부(true:삭제,false:보류)|
|	              |createdDt	|Long		|   |생성시간|
|               |updatedDt	|Long		|   |수정시간|

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
            "id":null,
            "name":"octest1",
            "active":null
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "password":"********",
            "mailDel":false,
            "createdDt":null,
            "updatedDt":1597382469685
        }
    }
}
```

### 외부계정 활성화
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/enable.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/enable.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|외부계정 활성화|HTTPS|PUT|UTF-8|JSON|비활성화 상태 외부계정을 활성화|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|---|
|서비스 ID	   |serviceId	|String	 |O	 |서비스 ID，URL PATH 내에 설정한{serviceId}|
|외부계정 ID	|id	       |Integer	|O	|외부계정 ID,URL PATH내에 설정된 {id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result.content	|id	        |Integer  |		  |외부계정 ID|
|	              |name	      |String	  |O	  |외부계정 구분 명칭|
|	              |active	    |Boolean	|O	  |외부계정 상태(고정 값 : true)|
|               |host	      |String	  |O	  |메일 서버|
|	              |port	      |Integer	|O	  |포트(예:993)|
|	              |ssl	      |Boolean	|O	  |ssl 사용여부(true:사용,false:미사용)|
|	              |mail	      |String	  |O	  |외부계정 주소|
|	              |password	  |String	  |O	  |외부계정 비밀번호|
|	              |mailDel	  |Boolean	|O	  |원본 남기기 기능 사용 여부(true:삭제,false:보류)|
|	              |createdDt	|Long		  |     |생성시간|
|	              |updatedDt	|Long		  |     |수정시간|

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
            "id":21,
            "name":"octest1",
            "active":true
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "mailDel":false,
            "createdDt":1578376856000,
            "updatedDt":1597384423000
        }
    }
```

### 외부계정 비활성화
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/disable.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/disable.json				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|외부계정 비활성화|HTTPS|PUT|UTF-8|JSON|활성화 상태 외부계정을 비활성화|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|---|
|서비스 ID	   |serviceId	|String	 |O	 |서비스 ID，URL PATH 내에 설정한{serviceId}|
|외부계정 ID	|id	       |Integer	|O	|외부계정 ID,URL PATH내에 설정된 {id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result.content	|id	        |Integer	|	  |외부계정 ID|
|	              |name	      |String	  |O	|외부계정 구분 명칭|
|	              |active	    |Boolean	|O	|외부계정 상태(고정 값 : false)|
|	              |host	      |String 	|O	|메일 서버|
|	              |port	      |Integer	|O	|포트(예:993)|
|	              |ssl	      |Boolean	|O	|ssl 사용여부(true:사용,false:미사용)|
|	              |mail	      |String	  |O	|외부계정 주소|
|	              |password	  |String	  |O	|외부계정 비밀번호|
|	              |mailDel	  |Boolean	|O	|원본 남기기 기능 사용 여부(true:삭제,false:보류)|
|               |createdDt	|Long		  |   |생성시간|
|	              |updatedDt	|Long		  |   |수정시간|

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
            "id":21,
            "name":"octest1",
            "active":false
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "mailDel":false,
            "createdDt":1578376856000,
            "updatedDt":1597384423000
        }
    }
```

### 외부계정 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|외부계정 삭제|HTTPS|DELETE|UTF-8|JSON|비활성화 상태 외부계정 삭제|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|---|
|서비스 ID	   |serviceId	|String	 |O	 |서비스 ID，URL PATH 내에 설정한{serviceId}|
|외부계정 ID	|id	       |Integer	|O	|외부계정 ID,URL PATH내에 설정된 {id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|------------|-----|---|
|result.content|		|String|		|"SUCCESS":삭제 성공|

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

### 이메일 정보 저장
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|이메일 정보 저장|HTTPS|POST|UTF-8|JSON|이메일 정보 저장|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|---|
|서비스 ID	        |serviceId	   |String	|O	|서비스 ID|
|이메일 설정 정보	 |request body	|String	 |O	 |이메일 설정 정보(JSON)|
|	                 |name	        |String	 |	 |발신자 이름(길이:min = 0, max = 45)|
|	                 |displayMail	  |String	 |	 |발신자 주소(예：noreply@oc.toast.com)|
|	                 |template	    |String	 |	 |이메일 레이아웃. 예) \<p\>\#\{content\}\<\/p\> 해당 이메일 레이아웃은 모든 이메일에 적용됩니다. #{content} 태그는 반드시 추가해야합니다.|

#### Request Body
```
{
    "name":"noreply",
    "displayMail":"noreply@oc.toast.com",
    "template":"<p>#{content}</p>"
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|result	|		|	        |      |    |

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
