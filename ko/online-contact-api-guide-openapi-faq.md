## Contact Center > Online Contact > API 가이드 > FAQ
### FAQ 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com /{serviceId}/openapi/v1/helpdoc.json			
- URL (개발): https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/helpdoc.json			
	
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 목록 조회 |HTTPS  |GET    |UTF-8|JSON    |조회 조건 기준으로 FAQ 목록을 리턴|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|-----|----|
|서비스 ID	|serviceId	|Varchar(50)	|O	|서비스 ID, URL PATH내에 설정|
|조회언어	|language	|Varchar(2)	|X	|ko：한국어, zh：중국어, ja：일본어, en：영어|
|카테고리 ID	|category	|Int	|X	|카테고리 ID|
|추천	|recommend	|Boolean	 |X	|true：추천，false：추천 아님|
|상단고정	|top	|Boolean	       |X	|true：상단고정，false：상단고정 아님|
|상태	|status	|Varchar(1)	         |X	|D：초안, O：공개, C：완료|
|키워드	|query	|Varchar	         |X	|검색문구|
|조회 필드	|searchField	|Varchar	|X	|디폴트: 내용+제목으로 검색, title：제목만 검색, content：내용만 검색|
|정렬 필드	|sort	|Varchar	        |X	|isTop, isRecommend, createdDt, updatedDt 필드로 정렬기준 지정 가능. 여러개 일 경우 ','로 분리|
|페이지	|page	|Int	                 |X	|페이지 번호，디폴트로 1페이지| 
|페이지 당 건수	|pageSize	|Int   |X	|페이지 당 데이터 건수，디폴트로 10건|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|----|-----------|------|---|
|result.contents	|helpDocId	|Long	|O	|FAQ ID|
|                 |serviceId	        |String	|O	|서비스 ID|
|	                |language	|String	|O	|ko：한국어, zh：중국어, ja：일본어, en：영어|
| 	              |status	        |String	|O	|FAQ 상태. D：초안, O：공개, C：완료|
|	                |categoryId	|Int	|O	|카테고리 ID|
|	                |categoryName	|String	|O	|카테고리 명|
|	                |isRecommend	|Boolean	|O	|추천|
|	                |isTop	        |Boolean	|O	|상단고정|
|	                |title	        |String	|O	|FAQ 제목|
|	                |userId	        |Int	|O	|등록 유저ID|
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
        "userName": "홍",
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

### FAQ 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com /{serviceId}/openapi/v1/helpdoc/{id}.json			
- URL (개발): https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/helpdoc/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 상세 조회 |HTTPS  |GET    |UTF-8|JSON    |FAQ ID를 통해 FAQ 상세 내용 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|FAQ ID	|id	|Long	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|result.content	|helpDocId	|Long	        |O	|FAQ ID|
|	              |serviceId	|String	|O	|서비스 ID|
|	              |title	|String	        |O	|FAQ 제목|
|	              |content	|String	        |O	|FAQ 내용|
| 	            |isRecommend	|Boolean	|O	|추천|
| 	            |isTop	|Boolean	|O	|상단고정|
| 	            |status	|String	        |O	|FAQ 상태, D：초안, O：공개, C：완료|
|	              |readCnt	|Int	        |O	|조회수|
|	              |userId	|Int	        |O	|등록 유저 ID|
|	              |username	|String	        |O	|등록 유저 명|
|	              |attachmentYn	|Boolean	|O	|첨부파일 포함 여부|
|	              |createdDt	|Long	|O	|FAQ 등록시간|
|	              |updatedDt	|Long	|O	|FAQ 수정시간|
|	              |categories.categoryId	|Int	|O	|카테고리 ID|
|	              |categories.parent	|String	|O	|상위 카테고리 ID|
|	              |categories.name	|String	|O	|카테고리 명|
|	              |categories.level	|String	|O	|카테고리 뎁스（1\|2\|3）|
|	              |contents.{language}.title	|String	|O	|다국어 FAQ 제목|
|	              |contents.{language}.content	|String	|O	|다국어 FAQ 내용|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|다국어 첨부파일 ID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|다국어 첨부파일 명|
|	              |contents.{language}.attachments[].size	|Long	|O	|다국어 첨부파일 크기|
|	              |attachments[].attachmentId	|String	|O	|첨부파일 ID|
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

### FAQ 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 등록 |HTTPS  |POST    |UTF-8|JSON    |신규 FAQ 등록|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|request body	|categoryId	|String	|O	|카테고리 ID|
|	        |title	        |String	|O	|FAQ 제목（단일언어：서비스 언어）|
|	        |content	|String	|O	|FAQ 내용（단일언어：서비스 언어）|
|	        |status	        |String	|O	|FAQ 상태. D：초안, O：공개, C：완료|
|	        |isRecommend	|Boolean	|O	|추천 여부. true：추천, false：추천 아님|
|	        |isTop	        |Boolean	|O	|상단고정 여부. true：상단고정, false：상단고정 아님|
|	        |contents.{language}.title	|String	|O	|FAQ 제목(다국어)|
| 	        |contents.{language}.content	|String	|O	|FAQ 내용(다국어)|
|	        |contents.{language}.attachments[].attachmentId	|Array	|X	|첨부파일 ID（다국어）|
|	        |attachments[].attachmentId	|String	|X   	|첨부파일 ID（단일언어）|

#### Request Body
```
단일 언어
{
    "title":"中文标题1",
    "content":"中文内容1",
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "attachments":[
        {
            "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
         }
    ]
}

다국어
{
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "contents":{
        "ko":{
            "title":"한국어 제목1",
            "content":"한국어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "ja":{
            "title":"일본어 제목1",
            "content":"일본어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "zh":{
            "title":"중국어 제목1",
            "content":"중국어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "en":{
            "title":"영어 제목1",
            "content":"영어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        }
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|---------|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|			
|	        |serviceId	|String	|O	|서비스 ID|
|	        |title	        |String	|O	|FAQ 제목|
|	        |content	|String	|O	|FAQ 내용|
|	        |isRecommend	|Boolean	|O	|추천 여부. true：추천, false：추천 아님|
|	        |isTop	        |Boolean	|O	|상단고정 여부. true：상단고정, false：상단고정 아님|
|	        |status	        |String	|O	|FAQ 상태. D：초안, O：공개, C：완료|
|	        |readCnt	|Int	|O	|조회수|
|	        |userId	        |Int	|O	|등록 유저 ID|
|	        |username	|String	|O	|등록 유저 명|
|	        |attachmentYn	|Boolean	|O	|첨부파일 포함 여부|
|	        |createdDt	|Long	|O	|FAQ 등록시간|
|	        |updatedDt	|Long	|O	|FAQ 수정시간|
|	        |categories.categoryId	|Int	|O	|카테고리 ID|
|	        |categories.parent	|String	|O	|상위 카테고리 ID|
|	        |categories.name	|String	|O	|카테고리 명|
|	        |categories.level	|String	|O	|카테고리 뎁스（1\|2\|3）|
|	        |contents.{language}.title	|String	|O	|다국어 FAQ 제목|
|	        |contents.{language}.content	|String	|O	|다국어 FAQ 내용|
|	        |contents.{language}.attachments[].attachmentId	|String	|O	|다국어 첨부파일 ID|
|	        |contents.{language}.attachments[].fileName	|String	|O	|다국어 첨부파일 명|
|	        |contents.{language}.attachments[].size	        |Long	|O	|다국어 첨부파일 크기|
|	        |attachments[].attachmentId	|String	|O	|첨부파일 ID|
|	        |attachments[].fileName	        |String	|O	|첨부파일 명|
|	        |attachments[].size	        |Long	|O	|첨부파일 크기|

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
                    "title":"일번어 제목1",
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

### FAQ 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json					
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 수정 |HTTPS  |PUT    |UTF-8|JSON    |FAQ ID 기준으로 내용 수정|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|FAQ ID	   |helpDocId	   |Long	|O	|URL PATH내에 설정한{id}|
|request body	|categoryId	|String	|O	|카테고리 ID|
|	        |title	        |String	|O	|FAQ 제목（단일언어：서비스 언어）|
|	        |content	|String	|O	|FAQ 내용（단일언어：서비스 언어）|
|	        |status	        |String	|O	|FAQ 상태. D：초안, O：공개, C：완료|
|	        |isRecommend	|Boolean	|O	|추천 여부. true：추천, false：추천 아님|
|	        |isTop	        |Boolean	|O	|상단고정 여부. true：상단고정, false：상단고정 아님|
|	        |contents.{language}.title	|String	|O	|FAQ 제목(다국어)|
|	        |contents.{language}.content	|String	|O	|FAQ 내용(다국어)|
|	        |contents.{language}.attachments[].attachmentId	|Array	  |X	|첨부파일 ID（다국어）|
|	        |attachments[].attachmentId	|String	    |X	|첨부파일 ID（단일언어）|

#### Request Body
```
단일언어
{
    "title":"중국어 제목1",
    "content":"중국어 내용1",
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "attachments":[
        {
            "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
         }
    ]
}

다국어
{
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "contents":{
        "ko":{
            "title":"한국어 제목1",
            "content":"한국어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "ja":{
            "title":"일본어 제목1",
            "content":"일본어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "zh":{
            "title":"중국어 제목1",
            "content":"중국어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "en":{
            "title":"영어 제목1",
            "content":"영어 내용1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        }
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|---------|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|				
|	        |serviceId	|String	|O	|서비스 ID|
|	        |title	        |String	|O	|FAQ 제목|
|	        |content	|String	|O	|FAQ 내용|
|	        |isRecommend	|Boolean	|O	|추천 여부. true：추천, false：추천 아님|
|	        |isTop	        |Boolean	|O	|상단고정 여부. true：상단고정, false：상단고정 아님|
|	        |status	        |String	|O	|FAQ 상태. D：초안, O：공개, C：완료|
|	        |readCnt	|Int	|O	|조회수|
|	        |userId	        |Int	|O	|등록 유저 ID|
|	        |username	|String	|O	|등록 유저 명|
|	        |attachmentYn	|Boolean	|O	|첨부파일 포함 여부|
|	        |createdDt	|Long	|O	|FAQ 등록시간|
|	        |updatedDt	|Long	|O	|FAQ 수정시간|
|	        |categories.categoryId	|Int	|O	|카테고리 ID|
|	        |categories.parent	|String	|O	|상위 카테고리 ID|
|	        |categories.name	|String	|O	|카테고리 명|
|	        |categories.level	|String	|O	|카테고리 뎁스（1\|2\|3）|
|	        |contents.{language}.title	|String	|O	|다국어 FAQ 제목|
|	        |contents.{language}.content	|String	|O	|다국어 FAQ 내용|
|	        |contents.{language}.attachments[].attachmentId	|String	|O	|다국어 첨부파일 ID|
|	        |contents.{language}.attachments[].fileName	|String	|O	|다국어 첨부파일 명|
|	        |contents.{language}.attachments[].size	        |Long	|O	|다국어 첨부파일 크기|
|	        |attachments[].attachmentId	|String	|O	|첨부파일 ID|
|	        |attachments[].fileName	        |String	|O	|첨부파일 명|
|	        |attachments[].size	        |Long	|O	|첨부파일 크기|

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

### FAQ 카테고리 별 고정 설정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/recommend.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/recommend.json		

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 카테고리 별 고정 설정 |HTTPS  |PUT    |UTF-8|JSON    |FAQ 문서가 속한 카테고리 상단에 고정되도록 설정|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|FAQ ID	|Id	          |Int	|O	|URL PATH내에 설정한{id}|
|추천	|recommend	|Boolean	|O	|추천 여부. true：추천, false：추천 아님|

#### 결과 데이터
- 없음

### FAQ 메인화면 고정 설정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/top.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/top.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 메인화면 고정 설정 |HTTPS  |PUT    |UTF-8|JSON    |FAQ 문서가 메인화면 상단에 고정되도록 설정|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|FAQ ID	   |Id	|Int	|O	|URL PATH내에 설정한{id}|
|상단고정	|top	|Boolean	|O	|상단고정 여부. true：상단고정, false：상단고정 아님|

#### 결과 데이터
- 없음

### FAQ 완료처리
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/close.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/close.json		

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 완료처리 |HTTPS  |PUT    |UTF-8|JSON    |FAQ 상태를 완료로 변경 (status = C)|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|FAQ ID	   |Id	           |Int	   |O	   |URL PATH내에 설정한{id}|

#### 결과 데이터
- 없음

### FAQ 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json					
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 삭제 |HTTPS  |DELETE    |UTF-8|JSON    |FAQ ID 기준으로 FAQ 삭제|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|FAQ ID	   |Id	           |Int	   |O	   |URL PATH내에 설정한{id}|

#### 결과 데이터
- 없음

### FAQ 카테고리 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/helpdoc/categories.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/categories.json			
			
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 카테고리 목록 조회 |HTTPS  |GET    |UTF-8|JSON    |FAQ 카테고리 목록 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	  |String	|O	|URL PATH내에 설정한{serviceId}|
|하위 카테고리 ID	|child	|Int	|X	|상위 카테고리 취득 시, 전송하는 하위 카테고리 ID| 
|상위 카테고리 ID	|parent	|Int	|X	|하위 카테고리 취득 시, 전송하는 상위 카테고리 ID|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|카테고리 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |categoryCode	|String	|X	|카테고리 Code|
|	                |parent	        |Int	|X	|상위 카테고리 ID（기본 값:0）|
|	                |name	        |String	|O	|카테고리 명|
|	                |level	        |Int	|X	|뎁스（1\|2\|3）|
|	                |path	        |String	|X	|뎁스 경로（\level1\level2\"）|
|	                |orderNo	|Int	|X	|정렬 순서（기본 값:0）|
|	                |createdDt	|Long	|X	|등록시간|
|	                |updatedDt	|Long	|X	|수정시간|
|	                |languages	|String	|X	|다국어|

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
                "categoryId":999,
                "serviceId":"multilanguage",
                "categoryCode":"game",
                "parent":0,
                "name":"한국어 카테고리2",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1554949320000,
                "updatedDt":1554949320000,
                "languages":{
                    "ko":"한국어 카테고리2"
                }
            },
            {
                "categoryId":509,
                "serviceId":"multilanguage",
                "categoryCode":"code1",
                "parent":0,
                "name":"중국어 카테고리1",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1547949603000,
                "updatedDt":1554887489000,
                "languages":{
                    "ko":"한국어 카테고리1",
                    "ja":"일본어 카테고리1",
                    "en":"영어 카테고리1",
                    "zh":"중국어 카테고리1"
                }
            }
        ]
    }
}
```

### FAQ 카테고리 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/helpdoc/category/{id}.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json		
						
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 카테고리 상세 조회 |HTTPS  |GET    |UTF-8|JSON    |카테고리 ID를 통해 FAQ 카테고리 상세 내용 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|카테고리 ID 혹은 카테고리 Code	|id	|String	|O	|URL PATH내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|---------|----|
|result.contents	|categoryId	|Int	|O	|카테고리 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |categoryCode	|String	|X	|카테고리 Code|
|	                |parent	        |Int	|X	|상위 카테고리 ID（기본 값:0）|
|	                |name	        |String	|O	|카테고리 명|
|	                |level	        |Int	|X	|뎁스（1|2|3）|
|	                |path	        |String	|X	|뎁스 경로（\level1\level2\"）|
|	                |orderNo	|Int	|X	|정렬 순서（기본 값:0）|
|	                |createdDt	|Long	|X	|등록시간|
|	                |updatedDt	|Long	|X	|수정시간|
|	                |languages	|String	|X	|다국어|

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
            "categoryId":509,
            "serviceId":"multilanguage",
            "categoryCode":"code1",
            "parent":0,
            "name":"중국어 카테고리1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"한국어 카테고리1",
                "ja":"일본어 카테고리1",
                "en":"영어 카테고리1",
                "zh":"중국어 카테고리1"
            }
        }
    }
}
```

### FAQ 카테고리 추가
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category.json			
							
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 카테고리 추가 |HTTPS  |POST    |UTF-8|JSON    |신규 FAQ 카테고리 추가|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|카테고리 정보	|request body	|String	    |O	|카테고리 정보（JSON）|
|	             |name	     |String     |X		|카테고리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	              |categoryCode	|String	 |X	|카테고리 Code|
|	              |languages	|String	 |X	|다국어|
|	              |parent	        |Int	 |X	|상위 카테고리 ID（기본 값:0）|
|	              |orderNo	        |Int	 |X	|정렬순서（기본 값:0）|

#### Request Body
```
단일언어
{
    "name":"중국어 카테고리3",
    "categoryCode":"game3",
    "orderNo":1,
    "parent":0
}

다국어
{
    "categoryCode":"game3",
    "parent":0,
    "orderNo":1,
    "languages":{
        "ko":"한국어 카테고리3",
        "ja":"일본어 카테고리3",
        "en":"영어 카테고리3",
        "zh":"중국어 카테고리3"
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|result.contents	|categoryId	|Int	|O	|카테고리 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |categoryCode	|String	|X	|카테고리 Code|
|	                |parent	        |Int	|X	|상위 카테고리 ID（기본 값:0）|
|	                |name	        |String	|O	|카테고리 명|
|	                |level	        |Int	|X	|뎁스（1\|2\|3）|
|	                |path	        |String	|X	|뎁스 경로（\level1\level2\"）|
|	                |orderNo	|Int	|X	|정렬 순서（기본 값:0）|
|	                |createdDt	|Long	|X	|등록시간|
|	                |updatedDt	|Long	|X	|수정시간|
|	                |languages	|String	|X	|다국어|

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
            "categoryId":1577,
            "serviceId":"multilanguage",
            "categoryCode":"game3",
            "parent":0,
            "name":"중국어 카테고리3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"한국어 카테고리3",
                "ja":"일본어 카테고리3",
                "en":"영어 카테고리3",
                "zh":"중국어 카테고리3"
            }
        }
    }
}
```

### FAQ 카테고리 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
									
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 카테고리 수정 |HTTPS  |PUT    |UTF-8|JSON    |ID 기준으로 카테고리 명 수정 |공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|카테고리 ID 혹은 카테고리 Code	|Id	|String	|O	|URL PATH내에 설정한{id}|
|카테고리 정보	            |request body	|String	|O	|카테고리 정보（JSON）|
|	                         |name	             |String  |X	     |카테고리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	                         |categoryCode	     |String  |X	     |카테고리 Code|
|	                         |languages	     |String  |X	     |다국어|
|	                         |parent	     |Int     |X	     |상위 카테고리 ID（기본 값:0）|
|	                         |orderNo	     |Int     |X	     |정렬순서（기본 값:0）|

#### Request Body
```
단일언어
{
    "name":"중국어 카테고리2",
    "categoryCode":"game0",
    "orderNo":2,
    "parent":509
}

다국어
{
    "categoryCode":"game0",
    "parent":509,
    "orderNo":2,
    "languages":{
        "ko":"한국어 카테고리2",
        "ja":"일본어 카테고리2",
        "en":"영어 카테고리2",
        "zh":"중국어 카테고리2"
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|---------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|카테고리 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |categoryCode	|String	|X	|카테고리 Code|
|	                |parent	        |Int	|X	|상위 카테고리 ID（기본 값:0）|
|	                |name	        |String	|O	|카테고리 명|
|	                |level	        |Int	|X	|뎁스（1\|2\|3）|
|	                |path	        |String	|X	|뎁스 경로（\level1\level2\"）|
|	                |orderNo	|Int	|X	|정렬 순서（기본 값:0）|
|	                |createdDt	|Long	|X	|등록시간|
|	                |updatedDt	|Long	|X	|수정시간|
|	                |languages	|String	|X	|다국어|

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
            "categoryId":1576,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"한국어 카테고리",
            "level":1,
            "path":"\",
            "orderNo":1,
            "createdDt":1587349288181,
            "updatedDt":1587349288181,
            "languages":{
                "ko":"한국어 카테고리",
                "ja":"일본어 카테고리",
                "zh":"중국어 카테고리",
                "en":"영어 카테고리"
            }
        }
    }
}
```

### FAQ 카테고리 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json				
- URL (개발): https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/helpdoc/category/{id}.json	
									
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 카테고리 삭제 |HTTPS/80  |DELETE    |UTF-8|JSON    |카테고리 ID를 통해 FAQ 카테고리 삭제|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|카테고리 ID 혹은 카테고리 Code	|id	|String	|O	|URL PATH내에 설정한{id}|

#### 결과 데이터
- 없음

### FAQ 첨부파일 첨부
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/help/upload.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/help/upload.json	
									
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 첨부파일 첨부 |HTTPS  |POST    |UTF-8|JSON    |서버에 파일 업로드|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|업로드한 파일	|file	|File	|O	|업로드한 파일을 form로 제출|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|-----|
|result.content	|attachmentId	|String	|O	|첨부파일 ID|
|	        |fileName	|String	|O	|파일 명|
|	        |contentType	|String	|O	|파일 유형|
|	        |size 	        |Long	|O	|파일 크기|

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
            "attachmentId":"b891809a58b94ce3a09c080b81d0d14c",
            "fileName":"file2.jpg",
            "contentType":"image/jpeg",
            "size":13855
        }
    }
}
```

### FAQ 첨부파일 열기/다운로드
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/attachments/help/{id}					
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/attachments/help/{id}			
									
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 첨부파일 열기/다운로드 |HTTPS  |GET    |UTF-8|FILE    |서버에 업로드한 FAQ 첨부파일 열기/다운로드|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	          |serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|업로드 파일 ID	|id	      |String  |O     |업로드 파일id| 
|열람방식	         |type	       |String	|X       |기본 값: 열기（download:다운로드,open:열기）|

#### 결과 데이터
- 없음

#### Response Body
- File

### FAQ 첨부파일 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/help/{id}.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/help/{id}.json	
									
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ 첨부파일 삭제 |HTTPS  |DELETE    |UTF-8|JSON    |서버에 업로드한 파일 삭제|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|------|-----------|----|----|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|업로드한 파일 ID	|id	|String	|O	|업로드한 파일 ID|

#### 결과 데이터
- 없음

