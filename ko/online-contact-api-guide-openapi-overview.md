## Contact Center > Online Contact > API 가이드 > Open API 개요

### API 인증방법 설명
#### Security Key
##### 조직 레벨
TOAST CONSOLE에서 생성하신 조직 별로 유일한 Security Key를 보유하고 있습니다. Security Key를 통해 API로 전송되는 데이터를 암호화 처리할 수 있으며, 조직 관리와 관련된 Open API를 호출할 수 있습니다. (서비스 등록, 수정, 삭제 등) 사용하고 계시는 조직의 Online Contact에 접속하신 후 전체 관리 → SSO 로그인 → API Key에서 조직 레벨의 Security key를 확인하실 수 있습니다.
![](http://static.toastoven.net/prod_contact_center/dev1.png)

##### 서비스 레벨
하나의 조직에서 여러 개의 서비스를 생성하실 수 있으며, 생성하신 각 서비스 별로 유일한 Security Key를 보유하고 있습니다. Security Key를 통해 API로 전송되는 데이터를 암호화 처리할 수 있으며, 서비스 관리와 관련된 Open API를 호출할 수 있습니다. (티켓 관리, FAQ 등) 서비스 추가 API(/openapi/v1/admin/service/add.json)를 통해 서비스 추가가 가능하며, 서비스 추가 후 리턴 결과 값에서 서비스 레벨의 Security Key를 취득할 수 있습니다. 또한 사용하고 계시는 조직의 Online Contact에 접속하신 후 security key를 확인하고자 하는 서비스를 선택, 서비스 관리 → 인증 → OPEN API → API Key에서도 서비스 레벨의 Security Key 취득이 가능합니다.
![](http://static.toastoven.net/prod_contact_center/dev2.png)

##### Response Body
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

#### 인증 Header
각 Request Header에 아래의 값들을 반드시 설정해야 합니다.
- Authorization：Security Key를 통해 생성된 인증 문자열
- X-TC-Timestamp：현재 UTC 시간 값{new Date().getTime()}
- OUCODE：유저 code（필수 아님，설정하지 않을 경우 기본 값은 Owner）

#### Authorization 문자열 생성 방법
HmacSHA256로 암호화하거나, (조직ID + request URI + 파라미터 값 + 현재 UTC시간 값）문자열에 대해 암호화하여 Authorization 문자열을 생성하실 수 있습니다.

##### Java 예시
```
String URL = "http://nhn-cs.alpha-oc.toast.com/openapi/v1/admin/service/add.json";
String organizationId = "WopqM8euoYw89B7i"; // 조직ID
String securityKey = "0983e74b682b416684d2da59347aec82"; //조직 API Key
String uri = "/openapi/v1/admin/service/add.json"; // request uri
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
sb.append("GameBaseService").append("&").append("GameBaseServiceAPI").append("&").append("ko").append("&").append("Asia/Seoul");// 파라미터 값은 이름 오름차 순, 파라미터 사이는 &로 분리
Date date = new Date();
sb.append(date.getTime());
SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));
```

- request body가 있을 경우 파라미터 뒤에 body 문자열 추가
- 파일 첨부 시, 파일의 MD5는 파라미터 값으로 인증 문자열에 추가
- Security Key
	- /openapi/v1/admin/* 형태의 API 호출 시 조직 레벨 Security Key 사용
	- {serviceId}/openapi/v1/* 형태의 API 호출 시 ，서비스 레벨 Security Key 사용

### 공통 리턴 결과
|명칭	|변수|	데이터 타입	|필수|	설명|
|-----|---|--------------|----|------|
|Header	|resultCode	|VARCHAR(2)	|O	|리턴 결과 Code , 정상은 200|
|	|resultMessage|	VARCHAR(50)|	O|	리턴 오류 메시지|
|	|isSuccessful|	Boolean|	O|	실행 결과(성공：true ，실패：false)|
|Result|	contents|	JSON|	X|	목록 결과 내용|
|	|content|	JSON|	X|	상세 결과 내용

#### 리턴 Code 정보	
- 200 :SUCCESS	
- 400 :Bad Request	
- 403 : Forbidden	
- 404 : Not Data Found	
- 500 : Server Error	
- 9007 : 관련된 데이터가 이미 존재	
- 9005 : 관련된 데이터가 없음	

### API 관련 목록
#### 개발 환경 URL
|환경|	BaseUrl|	
|---|------------|
|알파|	https://{domain}.alpha-oc.toast.com|	
|리얼|	https://{domain}.oc.toast.com	|

#### Security Key URL
|Security Key|	URL|	
|------------|-----|
|조직 레벨|	/openapi/v1/admin/\*|	
|서비스 레벨|	/{serviceId}/openapi/v1/\*|	

#### API 목록
|레벨	|그룹	|명칭	|타입	|URL	|설명|
|---------|--------|---------|---------|-------|---|
|조직 레벨	|서비스	|서비스 추가	|POST	|/openapi/v1/admin/service/add.json	|신규 서비스 추가|
|	   |	      |서비스 상세	|GET	|/openapi/v1/admin/service/{serviceId}.json	|서비스 ID를 통해 서비스 정보 조회|
|  	   |	      |서비스 수정	|PUT	|/openapi/v1/admin/service/{serviceId}.json 	|서비스 ID를 통해 서비스 정보 수정|
|	   |           |서비스 비활성화	|PUT	|/openapi/v1/admin/service/disable.json	       |서비스 ID를 통해 서비스 비활성화|
|	   |	      |서비스 활성화	|PUT	|/openapi/v1/admin/service/enable.json	       |서비스 ID를 통해 서비스 활성화|
|	   |	      |서비스 삭제	|DELETE	|/openapi/v1/admin/service/{serviceId}.json	|서비스 ID를 통해 비활성화 된 서비스 삭제|
|	   |	      |서비스 API Key 다시 발급	|PUT	|/openapi/v1/admin/service/apikey/refresh.json	|서비스 ID를 통해 해당 서비스에 생성된 API Key 다시 발급|
|	   |	      |서비스 리스트	|GET	|/openapi/v1/admin/service/list.json	|조직내에 생성된 모든 서비스 조회|
|서비스 레벨	|접수유형 관리	|접수유형 추가	|POST	|/{serviceId}/openapi/v1/ticket/category/add.json	|신규 접수유형 추가|
|	    |                     |접수유형 상세	|GET	|/{serviceId}/openapi/v1/ticket/category/{categoryid}.json	|접수유형 ID를 통해 접수유형 조회|
|	    |	                 |접수유형 수정	|PUT	|/{serviceId}/openapi/v1/ticket/category/{categoryid}.json	|접수유형 ID를 통해 접수유형 수정|
|	    |	                 |접수유형 삭제	|DELETE	|/{serviceId}/openapi/v1/ticket/category/{categoryid}.json	|접수유형 ID를 통해 접수유형 삭제|
|  	    |	                 |접수유형 리스트	|GET	|/{serviceId}/openapi/v1/ticket/category/list.json	|서비스 내 접수유형 조회|
|           |티켓 관리	|티켓 생성	|POST	|/{serviceId}/openapi/v1/ticket/add.json	|신규 티켓 생성|
|	    |	           |티켓 처리	|POST	|/{serviceId}/openapi/v1/ticket/solve.json	|티켓 ID를 통해 티켓 처리|
|	    |	           |티켓 상세	|GET	|/{serviceId}/openapi/v1/ticket/{id}.json	|티켓 ID를 통해 티켓 조회|
|	    |	           |티켓 리스트	|GET	|/{serviceId}/openapi/v1/ticket/list.json	|검색 조건을 통해 조건에 맞는 티켓 리스트 노출|
|	    |	           |유저 티켓 리스트	|GET	|/{serviceId}/openapi/v1/ticket/{usercode}/list.json	|검색 조건을 통해 조건에 맞는 고객의 티켓 리스트 노출|
|	    |	           |티켓 첨부파일 첨부	|POST	|/{serviceId}/openapi/v1/attachments/ticket/upload.json	|서버에 파일 업로드|
|	    |	           |티켓 첨부파일 열기/다운	|GET	|/{serviceId}/openapi/v1/attachments/ticket/{id}	|서버에 업로드 된 파일 열기/다운|
|	    |	           |티켓 첨부파일 삭제	|DELETE	|/{serviceId}/openapi/v1/attachments/ticket/{id}.json	|서버에 업로드 된 파일 삭제|
|	    |공지사항	|공지사항 조회	|GET	|/{serviceId}/openapi/v1/multilanguage/notice.json	|공지사항의 내용 조회, 검색 조건에 따라 공지사항 리스트를 리턴|
|	    |	           |공지사항  상세	   |GET	|/{serviceId}/openapi/v1/multilanguage/notice/{id}.json	|공지사항 ID를 통해 공지사항 내용 취득|
|	    |	           |공지사항  상세(여러개)	|GET	|/{serviceId}/openapi/v1/multilanguage/notices.json	|여러개의 공지사항 ID를 통해 내용 취득|
|	    |	           |공지사항 등록	|POST	|/{serviceId}/openapi/v1/multilanguage/notice.json	|신규 공지사항 등록|
|	    |	           |공지사항 수정	|PUT	|/{serviceId}/openapi/v1/multilanguage/notice/{id}.json	|ID를 통해 공지사항 수정|
|           |		   |공지사항 삭제	|DELETE	|/{serviceId}/openapi/v1/multilanguage/notice/{id}.json	|ID를 통해 공지사항 삭제|
|	    |	           |템플릿 조회	 |GET	 |/{serviceId}/openapi/v1/multilanguage/notice/template.json	|템플릿 내용 조회，템플릿 리스트를 리턴|
|	    |	           |템플릿 상세	|GET	|/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json	|템플릿 ID를 통해 템플릿 내용 취득|
|	    |	           |템플릿 등록	|POST	|/{serviceId}/openapi/v1/multilanguage/notice/template.json	|신규 템플릿 등록|
|	    |	           |템플릿 수정	|PUT	|/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json	|ID를 통해 템플릿 수정|
|	    |	           |템플릿 삭제	|DELETE	|/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json	|ID를 통해 템플릿 삭제|
|	    |	           |공지사항 첨부파일 첨부	|POST	|/{serviceId}/openapi/v1/attachments/notice/upload.json	|서버에 파일 업로드|
|	    |	           |공지사항 첨부파일 삭제	|DELETE	|/{serviceId}/openapi/v1/attachments/notice/{id}.json	|서버에 업로드 한 파일 삭제|
|	    |	           |태그 리스트	|GET	|/{serviceId}/openapi/v1/notice/tag.json	|공지사항 태그 리스트 취득|
|	    |	           |태그 상세	|GET	|/{serviceId}/openapi/v1/notice/tag/{id}.json	|태그 ID를 통해 공지사항 태그내용 취득|
|	    |	           |태그 등록	|POST	|/{serviceId}/openapi/v1/notice/tag.json	|신규 태그 등록|
|	    |	           |태그 수정	|PUT	|/{serviceId}/openapi/v1/notice/tag/{id}.json	|태그 ID를 통해 공지사항 태그 수정|
|	    |	           |태그 삭제	|DELETE	|/{serviceId}/openapi/v1/notice/tag/{id}.json	|태그 ID를 통해 공지사항 태그 삭제|
|	    |	           |말머리 리스트	|GET	|/{serviceId}/openapi/v1/notice/categories.json	|공지사항 말머리 리스트 취득|
|	    |	           |말머리 상세	|GET	|/{serviceId}/openapi/v1/notice/category/{id}.json	|말머리 ID를 통해 공지사항 말머리 내용 취득|
|	    |	           |말머리 등록	|POST	|/{serviceId}/openapi/v1/notice/category.json	|신규 말머리 등록|
|	    |	           |말머리 수정	|POST	|/{serviceId}/openapi/v1/notice/category/{id}.json	|말머리 ID를 통해 말머리 명 수정|
|	    |	           |말머리 삭제	|DELETE	|/{serviceId}/openapi/v1/notice/category/{id}.json	|말머리 ID를 통해 공지사항 말머리 삭제|
|	    |상담원 관리	|상담원 리스트	|GET	|/{serviceId}/openapi/v1/users.json	|상담원 리스트 취득|
|           |		    |상담원 상세	|GET	|/{serviceId}/openapi/v1/users/{id}.json	|상담원 ID를 통해 상담원 정보 취득|
|	    |	            |상담원 추가	|POST	|/{serviceId}/openapi/v1/adduser.json	|지정한 서비스에 상담원 추가 및 권한 부여|
|           |		    |상담원 권한 변경	|PUT	|/{serviceId}/openapi/v1/users/{id}.json	|서비스 내 상담원 권한 변경|
|	    |	            |상담원 삭제	|DELETE	|/{serviceId}/openapi/v1/users/{id}.json	|지정한 서비스에서 상담원 삭제|
|	    |헬프센터	 |헬프센터 지정 데이터 추가	|POST	|/{serviceId}/hc/openapi/v1/addition.json	|추가 필요한 고객정보를 DB에 저장|
|	    |FAQ	     |FAQ 조회	|GET	|/{serviceId}/openapi/v1/helpdoc.json	|조회 조건 기준으로 FAQ 리스트를 리턴|
|           |		     |FAQ 상세	|GET	|/{serviceId}/openapi/v1/helpdoc/{id}.json	|FAQ ID를 통해 FAQ 내용 취득|
|           |		     |FAQ 등록	|POST	|/{serviceId}/openapi/v1/helpdoc.json	|신규 FAQ 등록|
|           |		     |FAQ 수정	|PUT	|/{serviceId}/openapi/v1/helpdoc/{id}.json	|FAQ ID 기준으로 내용 수정|
|	    |	             |추천 FAQ 설정	|PUT	|/{serviceId}/openapi/v1/helpdoc/{id}/recommend.json	|추천 FAQ 설정|
|	    |	             |상단고정 FAQ 설정	|PUT	|/{serviceId}/openapi/v1/helpdoc/{id}/top.json	|상단고정 FAQ 설정|
|	    |	             |FAQ 완료처리	|PUT	|/{serviceId}/openapi/v1/helpdoc/{id}/close.json	|FAQ 상태를 완료상태로 변경（status=C）|
|	    |	             |FAQ 삭제	|DELETE	/{serviceId}/openapi/v1/helpdoc/{id}.json	|FAQ ID 기준으로 FAQ 삭제|
|	    |	             |카테고리 리스트	|GET	|/{serviceId}/openapi/v1/helpdoc/categories.json	|FAQ 카테고리 리스트 취득|
|	    |	             |카테고리 상세	|GET	|/{serviceId}/openapi/v1/helpdoc/category/{id}.json	|카테고리 ID를 통해 FAQ 카테고리 내용 취득|
|	    |	             |카테고리 추가	|POST	|/{serviceId}/openapi/v1/helpdoc/category.json	|신규 FAQ 카테고리 추가|
|	    |	             |카테고리 수정	|PUT	|/{serviceId}/openapi/v1/helpdoc/category/{id}.json	|ID 기준으로 카테고리 명 수정|
|	    |	             |카테고리 삭제	|DELETE	|/{serviceId}/openapi/v1/helpdoc/category/{id}.json	|카테고리 ID를 통해 FAQ 카테고리 삭제|
|	    |	             |FAQ 첨부파일 첨부	|POST	|/{serviceId}/openapi/v1/attachments/help/upload.json	|서버에 파일 업로드|
|	    |	             |FAQ 첨부파일 삭제	|DELETE	|/{serviceId}/openapi/v1/attachments/help/{id}.json	|서버에 업로드한 파일 삭제|


