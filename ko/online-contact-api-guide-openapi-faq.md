## Contact Center > Online Contact > API 가이드 > FAQ
### FAQ 목록 조회
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com /{serviceId}/openapi/v1/helpdoc.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/helpdoc.json			

		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 목록 조회 |HTTPS  |GET    |UTF-8|JSON    |조회 조건 기준으로 FAQ 리스트를 리턴|공통 인증   |

|담당자 이름	|담당자 이메일	|담당자 부서	|
|-----------|--------------|-----------|
|赫荣刚|he.ronggang@nhn-st.com|OC TF|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|서비스 ID	|serviceId	|VARCHAR(50)	|O	|서비스 ID, URL PATH내에 설정|
|조회언어	|language	|VARCHAR(2)	|X	|ko：한국어, zh：중국어, ja：일본어, en：영어|
|카테고리 ID	|categoryId	|INT	|X	|카테고리 ID|
|추천	|recommend	|Boolean	|X	|true：추천，false：추천 아님|
|상단고정	|top	|Boolean	|X	|true：상단고정，false：상단고정 아님|
|상태	|status	|VARCHAR(1)	|X	D：초안, O：공개, C：완료|
|키워드	|query	|VARCHAR	|X	|검색문구|
|조회 필드	|searchField	|VARCHAR	|X	|디폴트: 내용+제목으로 검색, title：제목만 검색, content：내용만 검색|
|정렬 필드	|sort	|VARCHAR	|X	|isTop, isRecommend, createdDt, updatedDt 필드로 정렬기준 지정 가능. 여러개 일 경우 ','로 분리|
|페이지	|page	|INT	|X	|페이지 번호，디폴트로 1페이지| 
|페이지 당 건수	|pageSize	|INT	|X	|페이지 당 데이터 건수，디폴트로 10건|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|------|---|
|result.contents	|helpDocId	|Long	|O	|FAQ ID|
|                 |serviceId	|String	|O	|서비스 ID|
|	                |language	|String	|O	|ko：한국어, zh：중국어, ja：일본어, en：영어|
| 	              |status	|String	|O	|FAQ 상태. D：초안, O：공개, C：완료|
|	                |categoryId	|INT	|O	|카테고리 ID|
|	                |categoryName	|String	|O	|카테고리 명|
|	                |isRecommend	|Boolean	|O	|추천|
|	                |isTop	|Boolean	|O	|상단고정|
|	                |title	|String	|O	|FAQ 제목|
|	                |userId	|INT	|O	|등록 유저ID|
|	                |userName	|String	|O	|등록 유저명|
|	                |createdDt	|Long	|O	|FAQ 등록시간|
|	                |updatedDt	|Long	|O	|FAQ 수정시간|

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
        "noticeId": 258,
        "language":"zh"
        "serviceId": "multilanguage",
        "status": "O",
        "categoryId": 509,
        "isRecommend": true,
        "isTop": false,
        "title": "중국어 제목1",
        "userId": 10063,
        "createdDt": 1547962599000,
        "updatedDt": 1548054677000,
        "userName": "김창홍",
        "categoryName": "중국어 카테고리",
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### FAQ 상세내용 취득
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com /{serviceId}/openapi/v1/helpdoc/{id}.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/helpdoc/{id}.json			

		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 상세내용 취득 |HTTPS  |GET    |UTF-8|JSON    |FAQ ID를 통해 FAQ 내용 취득|공통 인증   |

|담당자 이름	|담당자 이메일	|담당자 부서	|
|-----------|--------------|-----------|
|赫荣刚|he.ronggang@nhn-st.com|OC TF|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|FAQ ID	|id	|Long	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |title	|String	|O	|FAQ 제목|
|	              |content	|String	|O	|FAQ 내용|
| 	            |isRecommend	|Boolean	|O	|추천|
| 	            |isTop	|Boolean	|O	|상단고정|
| 	            |status	|String	|O	|FAQ 상태, D：초안, O：공개, C：완료|
|	              |readCnt	|INT	|O	|조회수|
|	              |userId	|INT	|O	|등록 유저 ID|
|	              |username	|String	|O	|등록 유저 명|
|	              |attachmentYn	|Boolean	|O	|첨부파일 포함 여부|
|	              |createdDt	|Long	|O	|FAQ 등록시간|
|	              |updatedDt	|Long	|O	|FAQ 수정시간|
|	              |categories.categoryId	|INT	|O	|카테고리 ID|
|	              |categories.parent	|String	|O	|상위 카테고리 ID|
|	              |categories.name	|String	|O	|카테고리 명|
|	              |categories.level	|String	|O	|카테고리 뎁스（1|2|3）|
|	              |contents.{language}.title	|String	|O	|다국어 FAQ 제목|
|	              |contents.{language}.content	|String	|O	|다국어 FAQ 내용|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|다국어 첨부파일 ID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|다국어 첨부파일 명|
|	              |contents.{language}.attachments[].size	Long	|O	|다국어 첨부차일 크기|
|	              |attachments[].attachmentId	|String	|O	|첨부차일 ID|
|	              |attachments[].fileName	|String	|O	|첨부파일 명|
|	              |attachments[].size	|Long	|O	|첨부파일 크기|

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
            "helpDocId":648,
            "language":null,
            "serviceId":"multilanguage",
            "title":"중국어 제목1",
            "content":"중국어 내용1",
            "isRecommend":false,
            "isTop":false,
            "status":"O",
            "readCnt":2,
            "userId":10060,
            "username":"test1",
            "attachmentYn":"Y",
            "createdDt":1584426136000,
            "updatedDt":1584426136000,
            "categories":[
                {
                    "categoryId":1367,
                    "parent":799,
                    "name":"123",
                    "level":3
                }
            ],
            "contents":{
                "ko":{
                    "title":"한국어 제목1",
                    "content":"한국어 내용1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "ja":{
                    "title":"일본어 제목1",
                    "content":"일본어 내용1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "zh":{
                    "title":"중국어 제목1",
                    "content":"중국어 내용1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "en":{
                    "title":"영어 제목1",
                    "content":"영어 내용1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                }
            },
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                    "fileName":"file.jpg",
                    "contentType":"application/octet-stream",
                    "size":10645
                }
            ]
        }
    }
}

```
