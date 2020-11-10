## Contact Center > Online Contact > API 가이드 > 공지사항
### 공지사항 목록 조회
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com /{serviceId}/openapi/v1/multilanguage/notice.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/multilanguage/notice.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 목록 조회  |HTTPS  |GET    |UTF-8|JSON    |공지사항의 내용 조회, 검색 조건에 따라 공지사항 리스트를 리턴|공통 인증   |

|담당자 이름	|담당자 이메일	|담당자 부서	|
|-----------|--------------|-----------|
|赫荣刚|he.ronggang@nhn-st.com|OC TF|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|----------|-----|----|
|서비스 ID	|serviceId	|VARCHAR(50)	|O	|서비스 ID, URL PATH 내에 설정|
|조회 언어	|language	|VARCHAR(2)	|X	|ko：한국어, zh：중국어, ja：일본어, en：영어|
|날짜 조회 필드	|dateField	|VARCHAR(20)	|X	|startDt：공지기간 시작일 검색, endDt：공지기간 종료일 검색, startAndEnd：공지기간 시작일 &종료일 검색, createdDt：등록일 검색|
|기간검색 시작시간	|termStart	|VARCHAR(14)	|X	|공지기간 시작일（yyyyMMddHHmmss）|
|기간검색 종료시간	|termEnd	|VARCHAR(14)	|X	|공지기간 종료일|（yyyyMMddHHmmss）|
|등록일 시작시간	|startDt	|VARCHAR(14)	|X	|등록일（yyyyMMddHHmmss）|
|등록일 종료시간	|endDt	|VARCHAR(14)	|X	|등록일（yyyyMMddHHmmss）|
|말머리 ID	|categoryId	|INT	|X	|말머리 ID|
|태그	|tag	|INT	|X	|태그 ID，ID가 다수일 경우' , ' 로 분리|
|유저 ID	|userId	|INT	|X	|유저ID|
|상단고정	|top	|Boolean	|X	|true：상단고정，false：상단고정 아님|
|유효기간	|term	|VARCHAR(20)	|X	|reservation：예약중, open：진행중, close：완료|
|상태	|status	|VARCHAR(1)	|X	|D：초안, O：공개, C：완료|
|키워드	|keyword	|VARCHAR	|X	|검색문구|
|조회 필드	|searchField	|VARCHAR	|X	|기본: 내용+제목으로 검색, title：제목만 검색, content：내용만 검색|
|정렬 필드	|sort	|VARCHAR	|X	|우측 필드로 정렬기준 지정 가능. 여러개 일 경우 ' , '로 분리. isTop, createdDt, updatedDt, displayDt
|페이지	|page	|INT	|X	|페이지 번호，디폴트로 1페이지| 
|페이지 당 건수	|pageSize	|INT	|X	|페이지 당 데이터 건수，디폴트로 10건|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|-----------|-----|---|
|result.contents	|noticeId	|INT	|O	|공지사항 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |language	|String	|O	|ko：한국어, zh：중국어, ja：일본어, en：영어
|	                |status	|String	|O	|공지사항 상태 D：초안, O：공개, C：완료}|
|	                |isTop	|Boolean	|O	|상단고정 표기|
|	                |term	|String	|O	|reservation：예약중, open：진행중, close：완료|
|	                |title	|String	|O	|공지사항 제목|
|	                |startDt	|String	|O	|시작시간（yyyyMMddHHmmss)|
|	                |endDt	|String	|O	|종료시간（yyyyMMddHHmmss)|
| 	              |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|                 |userId	|INT	|O	|등록 유저ID|
|                 |userName	|String	|O	|등록 유저명|
|result.contents.tags	|tags[].tagId	|INT	|O	|태그 ID|
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

### 공지사항 내용 취득
#### 인터페이스 설명
- URL:	https://{domain}.oc.toast.com /{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
- URL (개발):	https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
		
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|공지사항 내용 취득 |HTTPS  |GET    |UTF-8|JSON    |공지사항 ID를 통해 공지사항 내용 취득|공통 인증   |

|담당자 이름	|담당자 이메일	|담당자 부서	|
|-----------|--------------|-----------|
|赫荣刚|he.ronggang@nhn-st.com|OC TF|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|VARCHAR(50)	|O	|URL PATH 내에 설정한{serviceId}|
|공지사항 ID	|id	|INT	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|----|----|
|result.contents	|noticeId	|INT	|O	|공지사항 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |status	|String	|O	|공지사항 상태 D：초안, O：공개, C：완료|
|	                |categoryId	|INT	|O	|말머리 ID|
|	                |isTop	|Boolean	|O	|상단고정 표기|
|	                |term	|String	|O	|reservation：예약중, open：진행중, close：완료|
|	                |startDt	|String	|O	|시작시간（yyyyMMddHHmmss）|
|	                |endDt	|String	|O	|종료시간（yyyyMMddHHmmss）|
|	                |displayDt	|String	|X	|출력시간（yyyyMMddHHmmss）|
|	                |userId	|INT	|O	|등록 유저 ID| 
|result.content.contents	|{language}.title	|String	|O	|공지사항 제목|
|	                        |{language}.content	|String	|O	|공지사항 내용|
|	                        |{language}.attachments[].attachmentId	|String	|O	|첨부파일 ID|
|	                        |{language}.attachments[].fileName	|String	|O	|파일 명|
|	                        |{language}.attachments[].size	|Long	|O	|파일 사이즈|
|result.content.tags	|tags[].tagId	|INT	|O	|태그ID|
|	                    |tags[].names.{language}	|String	|O	|태그|
|result.content.category	|categoryId	|INT	|X	|말머리 ID|
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

