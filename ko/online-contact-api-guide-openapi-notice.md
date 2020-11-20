## Contact Center > Online Contact > API 가이드 > 공지사항
### 공지사항 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 목록 조회  |HTTPS  |GET    |UTF-8|JSON    |공지사항의 내용 조회, 검색 조건에 따라 공지사항 리스트를 리턴|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|Varchar(50)	|O	|서비스 ID, URL PATH 내에 설정|
|조회 언어	|language	|Varchar(2)	|X	|ko：한국어, zh：중국어, ja：일본어, en：영어|
|날짜 조회 필드	|dateField	|Varchar(20)	|X	|startDt：공지기간 시작일 검색, endDt：공지기간 종료일 검색, startAndEnd：공지기간 시작일 &종료일 검색, createdDt：등록일 검색|
|기간검색 시작시간	|termStart	|Varchar(14)	|X	|공지기간 시작일（yyyyMMddHHmmss）|
|기간검색 종료시간	|termEnd	|Varchar(14)	|X	|공지기간 종료일|（yyyyMMddHHmmss）|
|등록일 시작시간	|startDt	|Varchar(14)	|X	|등록일（yyyyMMddHHmmss）|
|등록일 종료시간	|endDt	        |Varchar(14)	|X	|등록일（yyyyMMddHHmmss）|
|말머리 ID	|categoryId	            |Int	|X	|말머리 ID|
|태그	|tag	                    |Int	|X	|태그 ID，ID가 다수일 경우' , ' 로 분리|
|유저 ID	|userId	                    |Int	|X	|유저ID|
|상단고정	|top	|Boolean	|X	|true：상단고정，false：상단고정 아님|
|유효기간	|term	|Varchar(20)	|X	|reservation：예약중, open：진행중, close：완료|
|상태	|status	|Varchar(1)	|X	|D：초안, O：공개, C：완료|
|키워드	|keyword	|Varchar	|X	|검색문구|
|조회 필드	|searchField	|Varchar	|X	|기본: 내용+제목으로 검색, title：제목만 검색, content：내용만 검색|
|정렬 필드	|sort	|Varchar	|X	|우측 필드로 정렬기준 지정 가능. 여러개 일 경우 ' , '로 분리. isTop, createdDt, updatedDt, displayDt
|페이지	|page	|Int	|X	|페이지 번호，디폴트로 1페이지| 
|페이지 당 건수	|pageSize	|Int	|X	|페이지 당 데이터 건수，디폴트로 10건|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|-----------|-----|---|
|result.contents	|noticeId	|Int	|O	|공지사항 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |language	|String	|O	|ko：한국어, zh：중국어, ja：일본어, en：영어
|	                |status	|String	|O	|공지사항 상태 D：초안, O：공개, C：완료}|
|	                |isTop	|Boolean	|O	|상단고정 표기|
|	                |term	|String	|O	|reservation：예약중, open：진행중, close：완료|
|	                |title	|String	|O	|공지사항 제목|
|	                |startDt	|String	|O	|시작시간（yyyyMMddHHmmss)|
|	                |endDt	|String	|O	|종료시간（yyyyMMddHHmmss)|
| 	              |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|                 |userId	|Int	|O	|등록 유저ID|
|                 |userName	|String	|O	|등록 유저명|
|result.contents.tags	|tags[].tagId	|Int	|O	|태그 ID|
|	                    |tags[].tag	|String	|O	|태그 명|
| 	                  |createdDt	|Long	|O	|공지사항 등록시간|
|	                    |updatedDt	|Long	|O	|공지사항 수정시간|

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
        "isTop": false,
        "term": "open",
        "title": "중국어 제목1",
        "startDt": "20190101000000",
        "endDt": "20990101000000",
        "displayDt": "20190120000000",
        "readCnt": 0,
        "userId": 10063,
        "createdDt": 1547962599000,
        "updatedDt": 1548054677000,
        "tags": [
          {
            "tagId": 94,
            "tag": "중국어 태그1"
          }
        ],
        "userName": "김창홍",
        "categoryName": "중국어 말머리",
        "category": {
          "categoryId": 509,
          "name": "중국어 말머리",
          "names": {
            "ko": "한국어 말머리",
            "ja": "일본어 말머리",
            "zh": "중국어 말머리"
          }
        }
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### 공지사항 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 상세 조회 |HTTPS  |GET    |UTF-8|JSON    |공지사항 ID를 통해 공지사항 상세 내용 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|Varchar(50)	|O	|URL PATH 내에 설정한{serviceId}|
|공지사항 ID	|id	|Int	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|----|----|
|result.contents	|noticeId	|Int	|O	|공지사항 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |status	|String	|O	|공지사항 상태 D：초안, O：공개, C：완료|
|	                |categoryId	|Int	|O	|말머리 ID|
|	                |isTop	|Boolean	|O	|상단고정 표기|
|	                |term	|String	|O	|reservation：예약중, open：진행중, close：완료|
|	                |startDt	|String	|O	|시작시간（yyyyMMddHHmmss）|
|	                |endDt	|String	|O	|종료시간（yyyyMMddHHmmss）|
|	                |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|	                |userId	|Int	|O	|등록 유저 ID| 
|result.content.contents	|{language}.title	|String	|O	|공지사항 제목|
|	                        |{language}.content	|String	|O	|공지사항 내용|
|	                        |{language}.attachments[].attachmentId	|String	|O	|첨부파일 ID|
|	                        |{language}.attachments[].fileName	|String	|O	|파일 명|
|	                        |{language}.attachments[].size	|Long	|O	|파일 사이즈|
|result.content.tags	|tags[].tagId	|Int	|O	|태그ID|
|	                    |tags[].names.{language}	|String	|O	|태그|
|result.content.category	|categoryId	|Int	|X	|말머리 ID|
|	                        |names	|String	|O	|다국어 말머리 명|
|	                        |createdDt	|Long	|O	|공지사항 등록시간|
|	                        |updatedDt	|Long	|O	|공지사항 수정시간|

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
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "중국어 제먹1",
      "content": "중국어 내용1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일본어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      }
    }
  }
}
```

### 공지사항 상세 조회 (여러 건)
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notices.json			 		
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notices.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 상세 조회 (여러 건) |HTTPS  |GET    |UTF-8|JSON    |여러 개의 공지사항 ID를 통해 공지사항 상세 내용 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|Varchar(50)	|O	|URL PATH 내에 설정한{serviceId}|
|공지사항 ID	|id	|String	|O	|공지사항 ID，여러개 일 경우 ','로 분리|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|공지사항 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |status	        |String	|O	|공지사항 상태. D：초안, O：공개, C：완료|
|	                |categoryId	|Int	|O	|말머리 ID|
|	                |isTop	        |Boolean	|O	|상단고정 표기|
|	                |term	        |String	|O	|reservation：예약중, open：진행중, close：완료|
|	                |startDt	|String	|O	|시작시간（yyyyMMddHHmmss）|
|                       |endDt	        |String	|O	|종료시간（yyyyMMddHHmmss）|
|	                |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|                       |userId	        |Int	|O	|등록 유저 ID| 
|result.contents.contents	|{language}.title	|String	|O	|공지사항 제목|
|	                        |{language}.content	|String	|O	|공지사항 내용|
|	                        |{language}.attachments[].attachmentId	|String	|O	|첨부파일 ID|
|	                        |{language}.attachments[].fileName	|String	|O	|파일 명|
|	                        |{language}.attachments[].size	|Long	|O	|파일 사이즈|
|result.contents.tags	|tags[].tagId	|Int	|O	|태그ID|
|	                |tags[].names.{language}	|String	|O	|태그|
|result.contents.category	|categoryId	|Int	|X	|말머리 ID|
|	                        |names	        |String	|O	|다국어 말머리 명|
|	                        |createdDt	|Long	|O	|공지사항 등록시간|
|	                        |updatedDt	|Long	|O	|공지사항 수정시간|

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
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "중국어 제목1",
      "content": "중국어 내용1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일번어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      }
    }
  }]
}
```

### 공지사항 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json					
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 등록 |HTTPS  |POST    |UTF-8|JSON    |신규 공지사항 등록|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|공지사항 내용	|request body	|String	|O	|공지사항 내용（JSON）|
|	             |status	     |String	|O	|공지사항 상태. D：초안, O：공개, C：완료|
|	             |categoryId	|Int	|O	|말머리 ID|
|	             |isTop	|Boolean	|O	|상단고정 표기|
|	             |contents.{language}.title	|String	|O	|공지사항 제목|
|	             |contents.{language}.content	|String	|O	|공지사항 내용|
|	             |startDt	|String	|O	|시작시간（yyyyMMddHHmmss）|
|	             |endDt	|String	|O	|종료시간（yyyyMMddHHmmss）|
|	             |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|	             |tags	|Array	|X	|태그 리스트|
|	             |tags[].tagId	|Int	|O	|태그 ID|
|	             |attachments	|Array	|X	|첨부파일|
|	             |attachments[].attachmentId	|String	|O	|첨부파일 ID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ]
    }
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|result.content	|noticeId	|Int	|O	|공지사항 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |status	        |String	|O	|공지사항 상태. D：초안, O：공개, C：완료|
|	        |categoryId	|Int	|O	|말머리 ID|
|	        |isTop	        |Boolean	|O	|상단고정 표기|
|	        |title	        |String	|O	|공지사항 제목|
|	        |content	|String	|O	|공지사항 내용|
|	        |startDt	|String	|O	|시작시간（yyyyMMddHHmmss）|
|	        |endDt	        |String	|O	|종료시간（yyyyMMddHHmmss）|
|	        |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|	        |attachmentYn	|String	|O	|Y：첨부파일 포함，N：첨부파일 포함 되지 않음|
|	        |userId	        |Int	|O	|등록 유저 ID|
|	        |tags	        |Array	|X	|태그 리스트|
|	        |tags[].tagId	|Int	|O	|태그 ID|
|	        |tags[].tag	|String	|O	|태그 명|
|	        |attachments	|Array	|X	|첨부파일|
|	        |attachments[].attachmentId	|String	|O	|첨부파일 ID|
|	        |attachments[].fileName	        |String	|O	|파일 명|
|	        |attachments[].size	|Long	|O	|파일 사이즈|
|	        |createdDt	        |Long	|O	|공지사항 등록시간|
|	        |updatedDt	        |Long	|O	|공지사항  수정시간|

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
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "중국어 제목1",
      "content": "중국어 내용1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일본어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      }
    }
  }
}
```

### 공지사항 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 수정 |HTTPS  |PUT    |UTF-8|JSON    |ID를 통해 공지사항 수정|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH내에 설정한{serviceId}|
|공지사항 ID	|id	|Int	|O	|URL PATH내에 설정한{id}|
|공지사항 내용	|request body	|String	|O	|공지사항 내용（JSON）|
|	             |status	     |String	|O	|공지사항 상태. D：초안, O：공개, C：완료|
|	             |categoryId	|Int	|O	|말머리 ID|
|	             |isTop	|Boolean	|O	|상단고정 표기|
|	             |contents.{language}.title	|String	|O	|공지사항 제목|
|	             |contents.{language}.content	|String	|O	|공지사항 내용|
|	             |startDt	|String	|O	|시작시간（yyyyMMddHHmmss）|
|	             |endDt	|String	|O	|종료시간（yyyyMMddHHmmss）|
|	             |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|	             |tags	|Array	|X	|태그 리스트|
|	             |tags[].tagId	|Int	|O	|태그 ID|
|	             |attachments	|Array	|X	|첨부파일|
|	             |attachments[].attachmentId	|String	|O	|첨부파일 ID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ]
    }
```

####  결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.content	|noticeId	|Int	|O	|공지사항 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |status	|String	|O	|공지사항 상태. D：초안, O：공개, C：완료|
|	        |categoryId	|Int	|O	|말머리 ID|
|	        |isTop	|Boolean	|O	|상단고정 표기|
|	        |title	|String	|O	|공지사항 제목|
|	        |content	|String	|O	|공지사항 내용|
|	        |startDt	|String	|O	|시작시간（yyyyMMddHHmmss）|
|	        |endDt	|String	|O	|종료시간（yyyyMMddHHmmss）|
|	        |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|               |attachmentYn	|String	|O	|Y：첨부파일 포함，N：첨부파일 포함되지 않음|
|	        |userId	|Int	|O	|등록 유저ID|
|	        |tags	|Array	|X	|태그 리스트|
|	        |tags[].tagId	|Int	|O	|태그 ID|
|	        |tags[].tag	|String	|O	|태그 명|
|               |attachments	|Array	|X	|첨부파일|
|	        |attachments[].attachmentId	|String	|O	|첨부파일 ID|
|               |attachments[].fileName	|String	|O	|파일 명|
|	        |attachments[].size	|Long	|O	|파일 사이즈|
|	        |createdDt	|Long	|O	|공지사항 등록시간|
|	        |updatedDt	|Long	|O	|공지사항 수정시간|

```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": {
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "중국어 제목1",
      "content": "중국어 내용1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일본어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      }
    }
  }
}
```

### 공지사항 삭제
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json						
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json							
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 삭제 |HTTPS  |DELETE    |UTF-8|JSON    |ID를 통해 공지사항 삭제|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|공지사항 ID	|Id	|Int	|O	|URL PATH 내에  설정한{id}|

#### 결과 데이터
- 없음

### 공지사항 템플릿 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json						
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json								
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 템플릿 목록  |HTTPS  |IN(GET)    |UTF-8|JSON    |템플릿 내용 조회, 템플릿 리스트를 리턴|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|Varchar(50)	|O	|서비스 ID，URL PATH 내에 설정|
|조회언어	|language	|Varchar(2)	|X	|ko：한국어, zh：중국어, ja：일본어, en：영어|
|시작시간	|startDt	|Varchar(14)	|X	|등록시간（yyyyMMddHHmmss）|
|종료시간	|endDt	|Varchar(14)	|X	|등록시간（yyyyMMddHHmmss）|
|말머리 ID	 |categoryId	|Int	|X	|말머리 ID|
|태그	|tag	|Int	|X	|태그 ID，ID가 다수일 경우 ','로 분리|
|유저 ID	|userId	|Int	|X	|유저 ID|
|상태	|status	|Varchar(1)	|X	|O：사용, C：미사용|
|키워드	|keyword	|Varchar	|X	|검색문구|
|조회필드	|searchField	|Varchar	|X	|디폴트로 내용+제목 으로 검색, title：제목만 검색, content：내용만 검색|
|페이지	|page	|Int	|X	|페이지 번호，디폴트로 1페이지| 
|페이지 당 건수	|pageSize	|Int	|X	|페이지 당 데이터 건수，디폴트로 10건|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|템플릿 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |language	|Varchar(2)	|O	|ko：한국어, zh：중국어, ja：일본어, en：영어|
|	                |status	|String	|O	|O：사용 C：미사용|
|	                |categoryId	|Int	|O	|말머리 ID|
|	                |categoryName	|String	|O	|말머리 명|
|	                |subject	|String	|O	|템플릿 제목|
|	                |memo	        |String	|O	|템플릿 설명|
|	                |userId	        |Int	|O	|등록 유저 ID|
|	                |userName	|String	|O	|등록 유저 명|
|result.contents.tags	|tags[].tagId	|Int	|O	|태그 ID|
|	                |tags[].tag	|String	|O	|태그 명|
|	                |tags[].names	|String	|O	|다국어 태그 명|
|result.contents.category	|names	|String	|O	|다국어 말머리 명|
|	                        |createdDt	|Long	|O	|템플릿 등록시간|
|	                        |updatedDt	|Long	|O	|템플릿 수정시간|

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
        "noticeId": 256,
        "serviceId": "multilanguage",
        "language":"zh"
        "status": "O",
        "categoryId": 509,
        "readCnt": 1,
        "userId": 10063,
        "createdDt": 1547950366000,
        "updatedDt": 1547961164000,
        "tags": [
          {
            "tagId": 94,
            "tag": "중국어 태그1",
            "names": {
              "ko": "한국어 태그1",
              "ja": "일본어 태그1",
              "zh": "중국어 태그1"
            }
          }
        ],
        "userName": "김창홍",
        "categoryName": "중국어 말머리",
        "category": {
          "categoryId": 509,
          "names": {
            "ko": "한국어 말머리",
            "ja": "일본어 말머리",
            "zh": "중국어 말머리"
          }
        },
        "subject": "템플릿 제목1",
        "memo": "템플릿 설명"
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### 공지사항 템플릿 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json							
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json							
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 템플릿 상세 조회 |HTTPS  |GET    |UTF-8|JSON    |템플릿 ID를 통해 템플릿 상세 내용 조회|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|Varchar(50)	|O	|URL PATH 내에 설정한{serviceId}|
|템플릿 ID	|id	        |Int        |O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|템플릿 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |status	        |String	|O	|O：사용, C：미사용|
|	                |categoryId	|Int	|O	|말머리 ID|
|	                |userId	        |Int	|O	|등록 유저 ID|
|	                |subject	|String	|O	|템플릿 제목|
|	                |memo	        |String	|O	|템플릿 설명|
|result.content.contents	|{language}.title	|String	|O	|공지사항 제목|
|	                        |{language}.content	|String	|O	|공지사항 내용|
|result.content.tags	        |tags[].tagId	|Int	|O	|태그 ID|
|	                        |tags[].names.{language}	|String	|O	|다국어 태그 명|
|result.content.category	|categoryId	|Int	|O	|말머리 ID|
|	                        |names	|String	|O	|다국어 말머리 명|
|	                        |createdDt	|Long	|O	|템플릿 등록시간|
|	                        |updatedDt	|Long	|O	|템플릿 수정시간|

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
      "noticeId": 256,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "title": "중국어 제목1",
      "content": "중국어 내용1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일본어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      },
      "subject": "템플릿 제목1",
      "memo": "템플릿 설명1"
    }
  }
}
```

### 공지사항 템플릿 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json			 						
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json			 				
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 템플릿 등록 |HTTPS  |POST    |UTF-8|JSON    |신규 템플릿 등록|공통 인증|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|템플릿 내용	|status	|String	|O	|O：사용, C：미사용|
|	    |categoryId	|Int	|O	|말머리 ID|
|	    |subject	|String	|O	|템플릿 제목|
|	    |memo	|String	|O	|템플릿 설명|
|	    |contents.{language}.title	|String	|O	|다국어 공지사항 제목|
|	    |contents.{language}.content	|String	|O	|다국어 공지사항 내용|
|	    |tags[].tagId	|Int	|O	|태그 ID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ],
      "subject": "템플릿 제목1",
      "memo": "템플릿 설명1"
    }
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|result.content	|noticeId	|Int	|O	|템플릿 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |status	        |String	|O	|O：사용, C：미사용|
|	        |categoryId	|Int	|O	|말머리 ID|
|	        |subject	|String	|O	|템플릿 제목|
|	        |memo	        |String	|O	|템플릿 설명|
|	        |userId	        |Int	|O	|등록 유저ID|
|result.content.contents	|{language}.title	|String	|O	|공지사항 제목|
|	                        |{language}.content	|String	|O	|공지사항 내용|
|result.content.tags	        |tagId	                |Int	|O	|태그 ID|
|	                        |names.{language}	|String	|O	|다국어 태그 명|
|result.content.category	|categoryId	        |Int	|O	|말머리 ID|
|	                        |names	                |String	|O	|다국어 말머리 명|
|	                        |createdDt	        |Long	|O	|템플릿 등록 시간|
|	                        |updatedDt	        |Long	|O	|템플릿 수정 시간|

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
      "noticeId": 256,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "title": "중국어 제목1",
      "content": "중국어 내용1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일본어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      },
      "subject": "템플릿 제목1",
      "memo": "템플릿 설명1"
    }
  }
}
```

### 공지사항 템플릿 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json								
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 템플릿 수정 |HTTPS  |PUT    |UTF-8|JSON    |ID를 통해 템플릿 수정|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|템플릿 ID	|Id	|Int	|O	|URL PATH 내에 설정한{id}|
|템플릿 내용	|status	|String	|O	|O：사용, C：미사용	
|           |categoryId	|Int	|O	|말머리 ID|
|	    |subject	|String	|O	|템플릿 제목|
|	    |memo	|String	|O	|템플릿 설명|
|	    |contents.{language}.title	|String	|O	|다국어 공지사항 제목|
|	    |contents.{language}.content	|String	|O	|다국어 공지사항 내용|
|	    |tags[].tagId	|Int	|O	|태그 ID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ],
      "subject": "템플릿 제목1",
      "memo": "템플릿 설명1"
    }
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|----|
|result.content	|noticeId	|Int	|O	|템플릿 ID|
|	        |status	        |String	|O	|템플릿 상태. O：사용, C：미사용|
|	        |categoryId	|Int	|O	|말머리 ID|
|	        |subject	|String	|O	|템플릿 제목|
|	        |memo	        |String	|X	|템플릿 설명|
|	        |title	        |String	|O	|공지사항 제목|
|	        |content	|String	|O	|공지사항 내용|
|	        |userId	        |Int	|O	|등록 유저 ID|
|	        |tags	        |Array	|X	|태그 리스트|
|	        |tags[].tagId	|Int	|O	|태그 ID|
|	        |tags[].tag	|String	|O	|태그 명|
|	        |createdDt	|Long	|O	|템플릿 등록시간|
|	        |updatedDt	|Long	|O	|템플릿 수정시간|

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
      "noticeId": 256,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "title": "중국어 제목1",
      "content": "중국어 내용1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일본어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      },
      "subject": "템플릿 제목1",
      "memo": "템플릿 내용1"
    }
  }
}
```

### 공지사항 템플릿 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json										
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 템플릿 삭제 |HTTPS  |DELETE    |UTF-8|JSON    |ID를 통해 템플릿 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|템플릿 ID	|Id	        |Int	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
- 없음


### 공지사항 첨부파일 첨부
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/upload.json			
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/upload.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 첨부파일 업로드 |HTTPS  |POST    |UTF-8|JSON    |서버에 파일 업로드|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|업로드 파일	|file	|File	|O	|업로드 파일을 form으로 통해 제출|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|----|
|result.content	|attachmentId	|String	|O	|업로드 파일 ID|
|	        |fileName	|String	|O	|파일 명|
|	        |contentType	|String	|O	|파일 유형|
|	        |size	        |Long	|O	|파일 byte|

#### Request Body
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": {
      "attachmentId": "b891809a58b94ce3a09c080b81d0d14c",
      "fileName": "file2.jpg",
      "contentType": "image/jpeg",
      "size": 13855
    }
  }
}
```

### 공지사항 첨부파일 열기/다운로드
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}						 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}						

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 첨부파일 열기 및 다운로드 |HTTPS  |GET    |UTF-8|FILE   |서버에 업로드한 공지사항 첨부파일 열기 및 다운로드|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	           |serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|업로드 파일 ID	 |id	      |String  |O	|업로드 파일id| 
|열람방식	          |type	       |String	   |X	|기본 값:열기（download:다운로드, open:열기）|

### 공지사항 첨부파일 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/{id}.json			 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/{id}.json				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 첨부파일 삭제 |HTTPS  |DELETE    |UTF-8|JSON    |서버에 업로드한 파일 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String |O	|URL PATH 내에 설정한{serviceId}|
|업로드 파일 ID	|id	|String	|O	|업로드 파일id| 

#### 결과 데이터
- 없음

#### Response Body
- File

### 공지사항 태그 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag.json					 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag.json					

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 목록 조회 |HTTPS  |GET    |UTF-8|JSON    |공지사항 태그 목록 조회|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 키워드	|tag	|String	|X	|태그 검색 문구|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|--------|---------|------------|--------|----|
|result.contents	|tagId	        |INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|                       |tag		|	|X        |태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|X	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
        "tagId": 94,
        "tag": "한국어 태그1",
        "tagCode": "code",
        "serviceId": "multilanguage",
        "createdDt": 1547960380000,
        "languages": {
          "ko": "한국어 태그1",
          "ja": "일본어 태그1",
          "zh": "중국어 태그1",
          "en": "영어 태그1"
        }
      },
      {
        "tagId": 95,
        "tag": "한국어 태그2",
        "tagCode": "game",
        "serviceId": "multilanguage",
        "createdDt": 1547949797000,
        "names": {
          "ko": "한국어 태그2",
          "ja": "일본어 태그2",
          "zh": "중국어 태그2",
          "en": "영어 태그2"
        }
      }
    ]
  }
}
```

### 공지사항 태그 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json						 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json						

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 상세 조회 |HTTPS  |GET    |UTF-8|JSON    |태그 ID를 통해 공지사항 태그 상세 내용 조회|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 ID / 태그 code	|id	|String	|O	|URL PATH내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|-----|
|result.contents	|tagId	|INT	        |O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	        |X	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|X	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
      "tagId": 94,
      "tag": "한국어 태그1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "한국어 태그1",
        "ja": "일본어 태그1",
        "zh": "중국어 태그1",
        "en": "영어 태그1"
      }
    }
  }
}
```

### 공지사항 태그 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag.json								 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag.json							

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 등록 |HTTPS  |POST    |UTF-8|JSON    |신규 태그 등록|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 Code	|tagCode	|String	|X	|태그 Code|
|태그 내용	|names.{language}	|String	|O	|태그 내용|
|태그 내용(다국어)	|languages.{language}	|String	|O	|태그 내용(다국어)|

#### Request Body
```
단일언어
{
   "tagCode": "code",
   "tag": "한국어 태그1",
}

다국어
{
  "tagCode": "code",
  "languages": {
    "ko": "한국어 태그1",
    "ja": "일본어 태그1",
    "zh": "중국어 태그1",
    "en": "영어 태그1",
  }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|--------|---------|-----------|---------|----|
|result.contents	|tagId	|INT	        |O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	        |X 	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|X	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
      "tagId": 94,
      "tag": "한국어 태그1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "한국어 태그1",
        "ja": "일본어 태그1",
        "zh": "중국어 태그1",
        "en": "영어 태그1"
      }
    }
  }
}
```

### 공지사항 태그 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json											 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json									

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 수정 |HTTPS  |PUT    |UTF-8|JSON    |태그 ID를 통해 공지사항 태그 수정|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 ID / 태그 code	|id	|String	|O	|URL PATH 내에 설정한{id}|
|태그 내용	|names.{language}	|String	|O	|태그 내용|
|태그 내용(다국어)	|languages.{language}	|String	|O	|태그 내용(다국어)|

#### Request Body
```
단일언어
{
   "tag": "한국어 태그1",
}

다국어
{
  "languages": {
    "ko": "한국어 태그1",
    "ja": "일본어 태그1",
    "zh": "중국어 태그1",
    "en": "영어 태그1",
  }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|----|
|result.contents	|tagId	|INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	        |X	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|X	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
      "tagId": 94,
      "tag": "한국어 태그1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "한국어 태그1",
        "ja": "일본어 태그1",
        "zh": "중국어 태그1",
        "en": "영어 태그1"
      }
    }
  }
}
```

### 공지사항 태그 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json											

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 삭제 |HTTPS  |DELETE  |UTF-8|JSON    |태그 ID를 통해 공지사항 태그 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 ID / 태그 code	|id	|String	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
- 없음

### 공지사항 말머리 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/categories.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/categories.json											

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 목록 조회 |HTTPS  |GET  |UTF-8|JSON    |공지사항 말머리 목록  |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에  설정한{serviceId}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|말머리 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |categoryCode	|String	|X	|말머리 Code|
|	                |parent	        |Int	|X	|상위 말머리 ID（고정 값:0）|
|	                |name	        |String	|O	|말머리 명|
|	                |level	        |Int	|X	|뎁스（고정 값:1）|
|	                |path	        |String	|X	|뎁스 경로（고정 값:"\\"）|
|	                |orderNo	|Int	|X	|정렬순서（기본 값:0）|
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
                "name":"한국어 말머리2",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1554949320000,
                "updatedDt":1554949320000,
                "languages":{
                    "ko":"한국어 말머리2"
                }
            },
            {
                "categoryId":509,
                "serviceId":"multilanguage",
                "categoryCode":"code1",
                "parent":0,
                "name":"중국어 말머리1",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1547949603000,
                "updatedDt":1554887489000,
                "languages":{
                    "ko":"한국어 말머리1",
                    "ja":"일본어 말머리1",
                    "en":"영어 말머리1",
                    "zh":"중국어 말머리1"
                }
            }
        ]
    }
}
```

### 공지사항 말머리 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json										

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 상세 조회 |HTTPS  |GET  |UTF-8|JSON    |말머리 ID를 통해 공지사항 상세 내용 조회|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 ID / 말머리 code	|id	|String	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|말머리 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |categoryCode	|String	|X	|말머리 Code|
|	        |parent	        |Int	|X	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|X	|뎁스（고정 값:1）|
|	        |path	        |String	|X	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|X	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|X	|등록시간|
|	        |updatedDt	|Long	|X	|수정시간|
|	        |languages	|String	|X	|다국어|

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
            "name":"중국어 말머리1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"한국어 말머리1",
                "ja":"일본어 말머리1",
                "en":"영어 말머리1",
                "zh":"중국어 말머리1"
            }
        }
    }
}
```

### 공지사항 말머리 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category.json												

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 등록 |HTTPS  |POST  |UTF-8|JSON    |신규 말머리 등록|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 정보	|request body	|String	|O	|말머리 정보（JSON）|
|	    |name	    |String |X		|말머리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|X	|말머리 Code|
|	    |languages	        |String	|X	|다국어|
|	    |orderNo	|Int	|X	|정렬순서（고정 값:0）|

#### Request Body
```
단일 언어
{
    "name":"중국어 말머리3",
    "categoryCode":"game3",
    "orderNo":1
}

다국어
{
    "categoryCode":"game3",
    "parent":0,
    "orderNo":1,
    "languages":{
        "ko":"한국어 말머리3",
        "ja":"일본어 말머리3",
        "en":"영어 말머리3",
        "zh":"중국어 말머리3"
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|말머리 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |categoryCode	|String	|X	|말머리 Code|
|	        |parent	        |Int	|X	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|X	|뎁스（고정 값:1）|
|	        |path	        |String	|X	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|X	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|X	|등록시간|
|	        |updatedDt	|Long	|X	|수정시간|
|	        |languages	|String	|X	|다국어|

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
            "name":"중국어 말머리3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"한국어 말머리3",
                "ja":"일본어 말머리3",
                "en":"영어 말머리3",
                "zh":"중국어 말머리3"
            }
        }
    }
}
```

### 공지사항 말머리 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json			
											
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 수정 |HTTPS  |POST  |UTF-8|JSON    |말머리 ID를 통해 말머리 명 수정|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 ID / 말머리 code	|id	|String	|O	|URL PATH 내에 설정한{id}|
|말머리 정보	|request body	|String	|O	|말머리 정보（JSON）|
|	    |name	    |String |X	    |말머리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|X	|말머리 Code|
|	    |languages	|String	   |X	|다국어|
|	    |orderNo	|Int	   |X	|정렬순서（고정 값:0）|

#### Request Body
```
단일 언어
{
    "name":"중국어 말머리3",
    "categoryCode":"game3",
    "orderNo":1
}

다국어
{
    "categoryCode":"game3",
    "orderNo":1,
    "languages":{
        "ko":"한국어 말머리3",
        "ja":"일본어 말머리3",
        "en":"영어 말머리3",
        "zh":"중국어 말머리3"
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|말머리 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |categoryCode	|String	|X	|말머리 Code|
|	        |parent	        |Int	|X	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|X	|뎁스（고정 값:1）|
|	        |path	        |String	|X	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|X	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|X	|등록시간|
|	        |updatedDt	|Long	|X	|수정시간|
|	        |languages	|String	|X	|다국어|

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
            "name":"중국어 말머리3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"한국어 말머리3",
                "ja":"일본어 말머리3",
                "en":"영어 말머리3",
                "zh":"중국어 말머리3"
            }
        }
    }
}
```

### 공지사항 말머리 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com /{serviceId}/openapi/v1/notice/category/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/notice/category/{id}.json					
											
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 삭제|HTTPS  |DELETE  |UTF-8|JSON    |말머리 ID를 통해 말머리 명 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 ID / 말머리 code	|id	|String	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
- 없음

