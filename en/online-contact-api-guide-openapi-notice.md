## Contact Center > Online Contact > API Guide for Developers > Notice

### View Notice List
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|View notice list  |HTTPS  |GET    |UTF-8|JSON    |View notice list, return notice list by search conditions|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|Varchar(50)	|O	|Service ID, set in URL path|
|Query language	|language	|Varchar(2)	|X	|ko：Korean, zh：Chinese, ja：Japanese, en：English|
|Date lookup field	|dateField	|Varchar(20)	|X	|startDt：Search start date, endDt：Search finish date, startAndEnd：Search start&finish date, createdDt：Search registered date|
|Start time of period search	|termStart	|Varchar(14)	|X	|Start date of notice period（yyyyMMddHHmmss）|
|Finish time of period search	|termEnd	|Varchar(14)	|X	|Finish date of notice period（yyyyMMddHHmmss）|
|Start time of register	|startDt	|Varchar(14)	|X	|Registered date（yyyyMMddHHmmss）|
|Finish time of register	|endDt	        |Varchar(14)	|X	|Registered date（yyyyMMddHHmmss）|
|Heading ID	|categoryId	            |Int	|X	|Heading ID|
|Tag	|tag	                    |Int	|X	|Tag ID，If multiple IDs, separate with comma|
|User ID	|userId	                    |Int	|X	|User ID|
|Fix Top	|top	|Boolean	|X	|true：Fixed on top，false：Not fixed on top|
|Validity	|term	|Varchar(20)	|X	|reservation：Reserved, open：In progress, close：Done|
|Status	|status	|Varchar(1)	|X	|D：Draft, O：Distributed, C：Done|
|Keyword	|keyword	|Varchar	|X	|Search term|
|Query field	|searchField	|Varchar	|X	|Default: Search by contents+title, title：Search by title, content：Search by contents|
|Sort field	|sort	|Varchar	|X	|Sort criteria can be specified following fields. If fields are multiple, separate by comma. isTop, createdDt, updatedDt, displayDt|
|Page	|page	|Int	|X	|Page number，Default is 1 page| 
|Items per page	|pageSize	|Int	|X	|Data items per page，default : 10|

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|-----------|-----|---|
|result.contents	|noticeId	|Int	|O	|Notice ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |language	|String	|O	|ko：Korean, zh：Chinese, ja：Japanese, en：English|
|	                |status	|String	|O	|Notice status. D：Draft, O：In progress, C：Done|
|	                |isTop	|Boolean	|O	|If the document is fixed on top|
|	                |term	|String	|O	|reservation：Reserved, open：In progress, close：Done|
|	                |title	|String	|O	|Title|
|	                |startDt	|String	|O	|Start time（yyyyMMddHHmmss)|
|	                |endDt	|String	|O	|Finish time（yyyyMMddHHmmss)|
| 	              |displayDt	|String	|X	|Displayed time（yyyyMMddHHmmss）|
|                 |userId	|Int	|O	|Registered user ID|
|                 |userName	|String	|O	|Registered user name|
|result.contents.tags	|tags[].tagId	|Int	|O	|Tag ID|
|	                    |tags[].tag	|String	|O	|Tag name|
| 	                  |createdDt	|Long	|O	|Notice registered time|
|	                    |updatedDt	|Long	|O	|Notice edited time|

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
        "title": "Chinese title1",
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
            "tag": "Chinese tag1"
          }
        ],
        "userName": "Example",
        "categoryName": "Chinese heading",
        "category": {
          "categoryId": 509,
          "name": "Chinese heading",
          "names": {
            "ko": "Korean heading",
            "ja": "Japanese heading",
            "zh": "Chinese heading"
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

### View Notice Details
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|View Notice Details |HTTPS  |GET    |UTF-8|JSON    |View notice details through notice ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|Varchar(50)	|O	|{serviceId} set in URL path|
|Notice ID	|id	|Int	|O	|{id} set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|----|----|
|result.contents	|noticeId	|Int	|O	|Notice ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |status	|String	|O	|Notice status. D：Draft, O：In progress, C：Done|
|	                |categoryId	|Int	|O	|Heading ID|
|	                |isTop	|Boolean	|O	|If the document is fixed on top|
|	                |term	|String	|O	|reservation：Reserved, open：In progress, close：Done|
|	                |startDt	|String	|O	|Start time（yyyyMMddHHmmss）|
|	                |endDt	|String	|O	|Finish time（yyyyMMddHHmmss）|
|	                |displayDt	|String	|X	|Displayed time（yyyyMMddHHmmss）|
|	                |userId	|Int	|O	|Registered user ID| 
|result.content.contents	|{language}.title	|String	|O	|Title|
|	                        |{language}.content	|String	|O	|Contents|
|	                        |{language}.attachments[].attachmentId	|String	|O	|Attachment ID|
|	                        |{language}.attachments[].fileName	|String	|O	|Attachment name|
|	                        |{language}.attachments[].size	|Long	|O	|Attachment size|
|result.content.tags	|tags[].tagId	|Int	|O	|Tag ID|
|	                    |tags[].names.{language}	|String	|O	|Tag|
|result.content.category	|categoryId	|Int	|X	|Heading ID|
|	                        |names	|String	|O	|Multilingual heading names|
|	                        |createdDt	|Long	|O	|Registered time|
|	                        |updatedDt	|Long	|O	|Edited time|

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
      "title": "Chinese title1",
      "content": "Chinese contents1",
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
          "title": "Korean title1",
          "content": "Korean contents1",
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
          "title": "Japanese title1",
          "content": "Japanese contents1",
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
          "title": "Chinese title1",
          "content": "Chinese contents1",
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
            "ko": "Korean tag1",
            "ja": "Japanese tag1",
            "zh": "Chinese tag1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "Korean heading",
          "ja": "Japanese heading",
          "zh": "Chinese heading"
        }
      }
    }
  }
}
```

### View Notice Details (Multiple)
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notices.json			 		
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notices.json			
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|View Notice Details (Multiple) |HTTPS  |GET    |UTF-8|JSON    |View notice details through multiple notice IDs|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|Varchar(50)	|O	|{serviceId} set in URL path|
|Notice ID	|id	|String	|O	|{id} set in URL path, separate by comma if multiple IDs are being input|

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|Notice ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |status	|String	|O	|Notice status. D：Draft, O：In progress, C：Done|
|	                |categoryId	|Int	|O	|Heading ID|
|	                |isTop	|Boolean	|O	|If the document is fixed on top|
|	                |term	|String	|O	|reservation：Reserved, open：In progress, close：Done|
|	                |startDt	|String	|O	|Start time（yyyyMMddHHmmss）|
|	                |endDt	|String	|O	|Finish time（yyyyMMddHHmmss）|
|	                |displayDt	|String	|X	|Displayed time（yyyyMMddHHmmss）|
|	                |userId	|Int	|O	|Registered user ID| 
|result.contents.contents	|{language}.title	|String	|O	|Title|
|	                        |{language}.content	|String	|O	|Contents|
|	                        |{language}.attachments[].attachmentId	|String	|O	|Attachment ID|
|	                        |{language}.attachments[].fileName	|String	|O	|Attachment name|
|	                        |{language}.attachments[].size	|Long	|O	|Attachment size|
|result.contents.tags	|tags[].tagId	|Int	|O	|Tag ID|
|	                    |tags[].names.{language}	|String	|O	|Tag|
|result.contents.category	|categoryId	|Int	|X	|Heading ID|
|	                        |names	|String	|O	|Multilingual heading names|
|	                        |createdDt	|Long	|O	|Registered time|
|	                        |updatedDt	|Long	|O	|Edited time|

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
      "title": "Chinese title1",
      "content": "Chinese contents1",
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
          "title": "Korean title1",
          "content": "Korean contents1",
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
          "title": "Japanese title1",
          "content": "Japanese contents1",
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
          "title": "Chinese title1",
          "content": "Chinese contents1",
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
            "ko": "Korean tag1",
            "ja": "Japanese tag1",
            "zh": "Chinese tag1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "Korean heading",
          "ja": "Japanese heading",
          "zh": "Chinese heading"
        }
      }
    }
  }]
}
```

### Register Notice
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json					
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Register notice |HTTPS  |POST    |UTF-8|JSON    |Register new notice document|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Notice contents	|request body	|String	|O	|Notice contents（JSON）|
|	             |status	     |String	|O	|Notice status. D：Draft, O：In progress, C：Done|
|	             |categoryId	|Int	|O	|Heading ID|
|	             |isTop	|Boolean	|O	|If the document is fixed on top|
|	             |contents.{language}.title	|String	|O	|Title|
|	             |contents.{language}.content	|String	|O	|Contents|
|	             |startDt	|String	|O	|Start time（yyyyMMddHHmmss）|
|	             |endDt	|String	|O	|Finish timne（yyyyMMddHHmmss）|
|	             |displayDt	|String	|X	|Displayed time（yyyyMMddHHmmss）|
|	             |tags	|Array	|X	|Tag list|
|	             |tags[].tagId	|Int	|O	|Tag ID|
|	             |attachments	|Array	|X	|Attachment|
|	             |attachments[].attachmentId	|String	|O	|Attachment ID|

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
          "title": "Korean title1",
          "content": "Korean contents1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "ja": {
          "title": "Japanese title1",
          "content": "Japanese contents1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "zh": {
          "title": "Chinese title1",
          "content": "Chinese contents1",
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

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|result.content	|noticeId	|Int	|O	|Notice ID|
|	        |serviceId	|String	|O	|Service ID|
|	        |status	        |String	|O	|Notice status. D：Draft, O：In progress, C：Done|
|	        |categoryId	|Int	|O	|Heading ID|
|	        |isTop	        |Boolean	|O	|If the document is fixed on top|
|	        |title	        |String	|O	|Title|
|	        |content	|String	|O	|Contents|
|	        |startDt	|String	|O	|Start time（yyyyMMddHHmmss）|
|	        |endDt	        |String	|O	|Finish time（yyyyMMddHHmmss）|
|	        |displayDt	|String	|X	|Displayed time（yyyyMMddHHmmss）|
|	        |attachmentYn	|String	|O	|Y：Attachment included，N：Attachment not included|
|	        |userId	        |Int	|O	|Registered User ID|
|	        |tags	        |Array	|X	|Tag list|
|	        |tags[].tagId	|Int	|O	|Tag ID|
|	        |tags[].tag	|String	|O	|Tag name|
|	        |attachments	|Array	|X	|Attachment|
|	        |attachments[].attachmentId	|String	|O	|Attachment ID|
|	        |attachments[].fileName	        |String	|O	|Attachment name|
|	        |attachments[].size	|Long	|O	|Attachment size|
|	        |createdDt	        |Long	|O	|Registered time|
|	        |updatedDt	        |Long	|O	|Edited time|

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
      "title": "Chinese title1",
      "content": "Chinese contents1",
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
          "title": "Korean title1",
          "content": "Korean contents1",
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
          "title": "Japanese title1",
          "content": "Japanese contents1",
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
          "title": "Chinese title1",
          "content": "Chinese contents1",
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
            "ko": "Korean tag1",
            "ja": "Japanese tag1",
            "zh": "Chinese tag1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "Korean heading",
          "ja": "Japanese heading",
          "zh": "Chinese heading"
        }
      }
    }
  }
}
```

### Edit Notice
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Edit notice|HTTPS  |PUT    |UTF-8|JSON    |Edit notice through ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Notice ID	|id	|Int	|O	|{id} set in URL path|
|Notice Contents	|request body	|String	|O	|Notice contents（JSON）|
|	             |status	     |String	|O	|Notice status. D：Draft, O：In progress, C：Done|
|	             |categoryId	|Int	|O	|Heading ID|
|	             |isTop	|Boolean	|O	|If the document is fixed on top|
|	             |contents.{language}.title	|String	|O	|Title|
|	             |contents.{language}.content	|String	|O	|Contents|
|	             |startDt	|String	|O	|Start time（yyyyMMddHHmmss）|
|	             |endDt	|String	|O	|Finish time（yyyyMMddHHmmss）|
|	             |displayDt	|String	|X	|Displayed time（yyyyMMddHHmmss）|
|	             |tags	|Array	|X	|Tag list|
|	             |tags[].tagId	|Int	|O	|Tag ID|
|	             |attachments	|Array	|X	|Attachment|
|	             |attachments[].attachmentId	|String	|O	|Attachment ID|

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
          "title": "Korean title1",
          "content": "Korean contents1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "ja": {
          "title": "Japanese title1",
          "content": "Japanese contents1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "zh": {
          "title": "Chinese title1",
          "content": "Chinese contents1",
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

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|-----------|---------|----|
|result.content	|noticeId	|Int	|O	|Notice ID|
|	        |serviceId	|String	|O	|Service ID|
|	        |status	        |String	|O	|Notice status. D：Draft, O：In progress, C：Done|
|	        |categoryId	|Int	|O	|Heading ID|
|	        |isTop	        |Boolean	|O	|If the document is fixed on top|
|	        |title	        |String	|O	|Title|
|	        |content	|String	|O	|Contents|
|	        |startDt	|String	|O	|Start time（yyyyMMddHHmmss）|
|	        |endDt	        |String	|O	|Finish time（yyyyMMddHHmmss）|
|	        |displayDt	|String	|X	|Displayed time（yyyyMMddHHmmss）|
|	        |attachmentYn	|String	|O	|Y：Attachment included，N：Attachment not included|
|	        |userId	        |Int	|O	|Registered User ID|
|	        |tags	        |Array	|X	|Tag list|
|	        |tags[].tagId	|Int	|O	|Tag ID|
|	        |tags[].tag	|String	|O	|Tag name|
|	        |attachments	|Array	|X	|Attachment|
|	        |attachments[].attachmentId	|String	|O	|Attachment ID|
|	        |attachments[].fileName	        |String	|O	|Attachment name|
|	        |attachments[].size	|Long	|O	|Attachment size|
|	        |createdDt	        |Long	|O	|Registered time|
|	        |updatedDt	        |Long	|O	|Edited time|

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
      "title": "Chinese title1",
      "content": "Chinese contents1",
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
          "title": "Korean title1",
          "content": "Korean contents1",
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
          "title": "Japanese title1",
          "content": "Japanese contents1",
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
          "title": "Chinese title1",
          "content": "Chinese contents1",
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
            "ko": "Korean tag1",
            "ja": "Japanese tag1",
            "zh": "Chinese tag1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "Korean heading",
          "ja": "Japanese heading",
          "zh": "Chinese heading"
        }
      }
    }
  }
}
```

### Delete Notice
#### Interface Description
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json						
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json							
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Delete notice |HTTPS  |DELETE    |UTF-8|JSON    |Delete notice through ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URl path|
|Notice ID	|Id	|Int	|O	|{id} set in URL path|

#### Result Data
- None

### View Notice Template List
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json						
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json								
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|View notice template list |HTTPS  |IN(GET)    |UTF-8|JSON    |View template, return template list|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|Varchar(50)	|O	|Service ID，set in URL path|
|Query Language	|language	|Varchar(2)	|X	|ko：Korean, zh：Chinese, ja：Japanese, en：English|
|Start Time	|startDt	|Varchar(14)	|X	|Registered time（yyyyMMddHHmmss）|
|Finish Time	|endDt	|Varchar(14)	|X	|Registered Time（yyyyMMddHHmmss）|
|Heading ID	 |categoryId	|Int	|X	|Heading ID|
|Tag	|tag	|Int	|X	|Tag ID，Separate by comma if multiple tags|
|User ID	|userId	|Int	|X	|User ID|
|Status	|status	|Varchar(1)	|X	|O：In use, C：Not in use|
|Keyword	|keyword	|Varchar	|X	|Search term|
|Query Field	|searchField	|Varchar	|X	|Default: Search by contents+title, title：Search by title, content：Search by contents|
|Page	|page	|Int	|X	|Page number，Default : 1 page| 
|Items by page	|pageSize	|Int	|X	|Item data by page，Default: 10 items|

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|Tempate ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |language	|Varchar(2)	|O	|ko：Korean, zh：Chinese, ja：Japanese, en：English|
|	                |status	|String	|O	|O：In use C：Not in use|
|	                |categoryId	|Int	|O	|Heading ID|
|	                |categoryName	|String	|O	|Heading name|
|	                |subject	|String	|O	|Template title|
|	                |memo	        |String	|O	|Template description|
|	                |userId	        |Int	|O	|Registered user ID|
|	                |userName	|String	|O	|Registered user name|
|result.contents.tags	|tags[].tagId	|Int	|O	|Tag ID|
|	                |tags[].tag	|String	|O	|Tag name|
|	                |tags[].names	|String	|O	|Multilingual tag names|
|result.contents.category	|names	|String	|O	|Multilingual heading names|
|	                        |createdDt	|Long	|O	|Template registered time|
|	                        |updatedDt	|Long	|O	|Template edited time|

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
|열람방식	          |type	       |String	   |	|기본 값:열기（download:다운로드, open:열기）|

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
|                       |tag		|	|        |태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
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
|result.contents	|tagId	|INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	|	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
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
|result.contents	|tagId	|INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	|	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
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
|	                |tag	|	|	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
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
|	                |categoryCode	|String	|	|말머리 Code|
|	                |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	                |name	        |String	|O	|말머리 명|
|	                |level	        |Int	|	|뎁스（고정 값:1）|
|	                |path	        |String	|	|뎁스 경로（고정 값:"\\"）|
|	                |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	                |createdDt	|Long	|	|등록시간|
|	                |updatedDt	|Long	|	|수정시간|
|	                |languages	|String	|	|다국어|

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
|	        |categoryCode	|String	|	|말머리 Code|
|	        |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|	|뎁스（고정 값:1）|
|	        |path	        |String	|	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|	|등록시간|
|	        |updatedDt	|Long	|	|수정시간|
|	        |languages	|String	|	|다국어|

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
|	    |name	    |String |		|말머리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|말머리 Code|
|	    |languages	        |String	|	|다국어|
|	    |orderNo	|Int	|	|정렬순서（고정 값:0）|

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
|	        |categoryCode	|String	|	|말머리 Code|
|	        |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|	|뎁스（고정 값:1）|
|	        |path	        |String	|	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|	|등록시간|
|	        |updatedDt	|Long	|	|수정시간|
|	        |languages	|String	|	|다국어|

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
|	    |name	    |String |	    |말머리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|말머리 Code|
|	    |languages	|String	   |	|다국어|
|	    |orderNo	|Int	   |	|정렬순서（고정 값:0）|

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
|	        |categoryCode	|String	|	|말머리 Code|
|	        |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|	|뎁스（고정 값:1）|
|	        |path	        |String	|	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|	|등록시간|
|	        |updatedDt	|Long	|	|수정시간|
|	        |languages	|String	|	|다국어|

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

