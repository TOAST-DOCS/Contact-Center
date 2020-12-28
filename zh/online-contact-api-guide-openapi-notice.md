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
            "tag": "Chinese tag1",
            "names": {
              "ko": "Korean tag1",
              "ja": "Japanese tag1",
              "zh": "Chinese tag1"
            }
          }
        ],
        "userName": "example",
        "categoryName": "Chinese heading",
        "category": {
          "categoryId": 509,
          "names": {
            "ko": "Korean heading",
            "ja": "Japanese heading",
            "zh": "Chinese heading"
          }
        },
        "subject": "Template title1",
        "memo": "Template description"
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### Detailed Query of Notice Template
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json							
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json							
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Detailed query of notice template |HTTPS  |GET    |UTF-8|JSON    |Detailed query of notice template through template ID|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|Varchar(50)	|O	|{serviceId} set in URL path|
|Template ID	|id	        |Int        |O	|{id} set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|Template ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |status	        |String	|O	|O：In use, C：Not in use|
|	                |categoryId	|Int	|O	|Heading ID|
|	                |userId	        |Int	|O	|Registered user ID|
|	                |subject	|String	|O	|Title|
|	                |memo	        |String	|O	|Description|
|result.content.contents	|{language}.title	|String	|O	|Notice title|
|	                        |{language}.content	|String	|O	|Notice contents|
|result.content.tags	        |tags[].tagId	|Int	|O	|Tag ID|
|	                        |tags[].names.{language}	|String	|O	|Multilingual tag name|
|result.content.category	|categoryId	|Int	|O	|Heading ID|
|	                        |names	|String	|O	|Multilingual heading name|
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
          "title": "Korean title1",
          "content": "Korean contents1",
        },
        "ja": {
          "title": "Japanese title1",
          "content": "Japanese contents1",
        },
        "zh": {
          "title": "Chinese title1",
          "content": "Chinese contents1",
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
      },
      "subject": "Template title1",
      "memo": "Template description1"
    }
  }
}
```

### Register Notice Template
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json			 						
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json			 				
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Register Notice Template |HTTPS  |POST    |UTF-8|JSON    |Register new template|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Template contents	|status	|String	|O	|O：In use, C：Not in use|
|	    |categoryId	|Int	|O	|Heading ID|
|	    |subject	|String	|O	|Title|
|	    |memo	|String	|O	|Description|
|	    |contents.{language}.title	|String	|O	|Multilingual title|
|	    |contents.{language}.content	|String	|O	|Multilingual contents|
|	    |tags[].tagId	|Int	|O	|Tag ID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "contents": {
        "ko": {
          "title": "Korean title1",
          "content": "Korean contents1",
        },
        "ja": {
          "title": "Japanese title1",
          "content": "Japanese contents1",
        },
        "zh": {
          "title": "Chinese title1",
          "content": "Chinese contents1",
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ],
      "subject": "Template title1",
      "memo": "Template description1"
    }
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|result.content	|noticeId	|Int	|O	|Template ID|
|	        |serviceId	|String	|O	|Service ID|
|	        |status	        |String	|O	|O： Use, C：Not in use|
|	        |categoryId	|Int	|O	|Heading ID|
|	        |subject	|String	|O	|Template title|
|	        |memo	        |String	|O	|Template description|
|	        |userId	        |Int	|O	|Registered user ID|
|result.content.contents	|{language}.title	|String	|O	|Notice title|
|	                        |{language}.content	|String	|O	|Notice contents|
|result.content.tags	        |tagId	                |Int	|O	|Tag ID|
|	                        |names.{language}	|String	|O	|Multilingual tag names|
|result.content.category	|categoryId	        |Int	|O	|Heading ID|
|	                        |names	                |String	|O	|Multilingual heading names|
|	                        |createdDt	        |Long	|O	|Template registered time|
|	                        |updatedDt	        |Long	|O	|Template edited time|

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
      "title": "Chinese title1",
      "content": "Chinese contents1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "Korean title1",
          "content": "Korean contents1",
        },
        "ja": {
          "title": "Japanese title1",
          "content": "Japanese contents1",
        },
        "zh": {
          "title": "Chinese title1",
          "content": "Chinese contents1",
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
      },
      "subject": "Template title1",
      "memo": "Template description1"
    }
  }
}
```

### Edit Notice Template
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json								
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|Edit notice template |HTTPS  |PUT    |UTF-8|JSON    |Edit template by ID|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Template ID	|Id	|Int	|O	|{id} set in URL path|
|Template contents	|status	|String	|O	|O：In use, C：Not in use|
|	    |categoryId	|Int	|O	|Heading ID|
|	    |subject	|String	|O	|Title|
|	    |memo	|String	|O	|Description|
|	    |contents.{language}.title	|String	|O	|Multilingual title|
|	    |contents.{language}.content	|String	|O	|Multilingual contents|
|	    |tags[].tagId	|Int	|O	|Tag ID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "contents": {
        "ko": {
          "title": "Korean title1",
          "content": "Korean contents1",
        },
        "ja": {
          "title": "Japanese title1",
          "content": "Japanese contents1",
        },
        "zh": {
          "title": "Chinese title1",
          "content": "Chinese contents1",
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ],
      "subject": "Template title1",
      "memo": "Template description1"
    }
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|------------|--------|----|
|result.content	|noticeId	|Int	|O	|Template ID|
|	        |status	        |String	|O	|Template status. O：In use, C：Not in use|
|	        |categoryId	|Int	|O	|Heading ID|
|	        |subject	|String	|O	|Template title|
|	        |memo	        |String	|X	|Template description|
|	        |title	        |String	|O	|Notice title|
|	        |content	|String	|O	|Notice contents|
|	        |userId	        |Int	|O	|Registered user ID|
|	        |tags	        |Array	|X	|Tag list|
|	        |tags[].tagId	|Int	|O	|Tag ID|
|	        |tags[].tag	|String	|O	|Tag name|
|	        |createdDt	|Long	|O	|Template registered time|
|	        |updatedDt	|Long	|O	|Template edited time|

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
      "title": "Chinese title1",
      "content": "Chinese contents1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "Korean title1",
          "content": "Korean contents1",
        },
        "ja": {
          "title": "Japanese title1",
          "content": "Japanese contents1",
        },
        "zh": {
          "title": "Chinese title1",
          "content": "Chinese contents1",
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
      },
      "subject": "Template title1",
      "memo": "Template contents1"
    }
  }
}
```

### Delete Notice Template
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json										
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|Delete notice template |HTTPS  |DELETE    |UTF-8|JSON    |Delete template by ID|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Template ID	|Id	        |Int	|O	|{id} set in URL path|

#### Result Data
- None


### Attach File to Notice
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/upload.json			
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/upload.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|Attach file to notice |HTTPS  |POST    |UTF-8|JSON    |Upload file to server|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|File	|file	|File	|O	|Submit file through form|

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|------------|--------|----|
|result.content	|attachmentId	|String	|O	|Uploaded file ID|
|	        |fileName	|String	|O	|File name|
|	        |contentType	|String	|O	|File type|
|	        |size	        |Long	|O	|File byte|

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

### Open/Download Notice Attachment
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}						 		
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}						

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|Open/download notice attachment |HTTPS  |GET    |UTF-8|FILE   |Open/download notice attachment uploaded in server|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	           |serviceId	|String	|O	|{serviceId} set in URL path|
|File ID	 |id	      |String  |O	|File id| 
|Open method	          |type	       |String	   |	|Default:Open（download:Download, open:Open）|

### Delete Notice Attachment
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/{id}.json			 		
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/{id}.json				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Delete notice attachment |HTTPS  |DELETE    |UTF-8|JSON    |Delete file uploaded in server|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String |O	|{serviceId} set in URL path|
|File ID	|id	|String	|O	|File id| 

#### Result Data
- None

### View Notice Tag List
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tags.json					 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tags.json				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|View notice tag list |HTTPS  |GET    |UTF-8|JSON    |View notice tag list|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Tag keyword	|tag	|String	|X	|Tag search term|

#### Result Data
|Name |Variable |Data type |Required | Description|
|--------|---------|------------|--------|----|
|result.contents	|tagId	        |INT	|O	|Tag ID|
|	                |serviceId	|String	|O	|Service ID|
|                       |tag		|	|        |Tag contents|
|	                |createdDt	|Long	|O	|Registered time|
|	                |tagCode	|	|	|Tag Code|
|	                |languages.{language}	|String	|O	|Tag contents（Multilingual）|

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
        "tag": "Korean Tag1",
        "tagCode": "code",
        "serviceId": "multilanguage",
        "createdDt": 1547960380000,
        "languages": {
          "ko": "Korean Tag1",
          "ja": "Japanese Tag1",
          "zh": "Chinese Tag1",
          "en": "English Tag1"
        }
      },
      {
        "tagId": 95,
        "tag": "Korean Tag2",
        "tagCode": "game",
        "serviceId": "multilanguage",
        "createdDt": 1547949797000,
        "names": {
          "ko": "Korean Tag2",
          "ja": "Japanese Tag2",
          "zh": "Chinese Tag2",
          "en": "English Tag2"
        }
      }
    ]
  }
}
```

### Detailed Query for Notice Tags
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json						 		
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json						

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Detailed query for notice tags |HTTPS  |GET    |UTF-8|JSON    |Detailed query for notice tags by tag ID|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Tag ID / Tag code	|id	|String	|O	|{id} set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|------------|--------|-----|
|result.contents	|tagId	|INT	|O	|Tag ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |tag	|	|	|Tag contents|
|	                |createdDt	|Long	|O	|Registered time|
|	                |tagCode	|	|	|Tag Code|
|	                |languages.{language}	|String	|O	|Tag contents（Multilingual）|

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
      "tag": "Korean tag1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "Korean tag1",
        "ja": "Japanese tag1",
        "zh": "Chinese tag1",
        "en": "English tag1"
      }
    }
  }
}
```

### Register Notice Tag
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag.json								 		
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag.json							

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Register notice tag |HTTPS  |POST    |UTF-8|JSON    |Register new tag|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Tag Code	|tagCode	|String	|X	|Tag code|
|Tag Contents |names.{language}	|String	|O	|Tag contents|
|Tag Contents(Multilingual)	|languages.{language}	|String	|O	|Tag contents(Multilingual)|

#### Request Body
```
Single language
{
   "tagCode": "code",
   "tag": "Korean Tag1",
}

Multilingual
{
  "tagCode": "code",
  "languages": {
    "ko": "Korean Tag1",
    "ja": "Japanese Tag1",
    "zh": "Chinese Tag1",
    "en": "English Tag1",
  }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|--------|---------|-----------|---------|----|
|result.contents	|tagId	|INT	|O	|Tag ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |tag	|	|	|Tag contents|
|	                |createdDt	|Long	|O	|Registered time|
|	                |tagCode	|	|	|Tag Code|
|	                |languages.{language}	|String	|O	|Tag contents（Multilingual）|

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
      "tag": "Korean Tag1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "Korean Tag1",
        "ja": "Japanese Tag1",
        "zh": "Chinese Tag1",
        "en": "English Tag1"
      }
    }
  }
}
```

### Edit Notice Tag
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json											 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json									

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|Edit notice tag |HTTPS  |PUT    |UTF-8|JSON    |Edit notice tag through tag ID|

#### #### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Tag ID / Tag code	|id	|String	|O	|{id} set in URL path|
|Tag Contents	|names.{language}	|String	|O	|Tag contents|
|Tag Contents(Multilingual)	|languages.{language}	|String	|O	|Tag contents(Multilingual)|

#### Request Body
```
Single language
{
   "tag": "Korean Tag1",
}

Multilingual
{
  "languages": {
    "ko": "Korean Tag1",
    "ja": "Japanese Tag1",
    "zh": "Chinese Tag1",
    "en": "English Tag1",
  }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|------------|--------|----|
|result.contents	|tagId	|INT	|O	|Tag ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |tag	|	|	|Tag contents|
|	                |createdDt	|Long	|O	|Registered time|
|	                |tagCode	|	|	|Tag Code|
|	                |languages.{language}	|String	|O	|Tag contents（Multilingual）|

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
      "tag": "Korean tag1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "Korean tag1",
        "ja": "Japanese tag1",
        "zh": "Chinese tag1",
        "en": "English tag1"
      }
    }
  }
}
```

### Delete Notice Tag
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json												 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json											

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Delete notice tag |HTTPS  |DELETE  |UTF-8|JSON    |Delete notice tag through tag ID|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Tag ID / Tag code	|id	|String	|O	|{id} set in URL path|

#### Result Data
- None

### View Notice Heading List
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/categories.json												 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/categories.json											

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|View notice heading list |HTTPS  |GET  |UTF-8|JSON    |Notice heading list  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|Heading ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|	|Heading Code|
|	                |parent	        |Int	|	|Upper depth heading ID（Default:0）|
|	                |name	        |String	|O	|Heading name|
|	                |level	        |Int	|	|Depth（Fixed value:1）|
|	                |path	        |String	|	|Depth path（Fixed value:"\\\\"）|
|	                |orderNo	|Int	|	|Sort order（Default:0）|
|	                |createdDt	|Long	|	|Registered time|
|	                |updatedDt	|Long	|	|Edited time|
|	                |languages	|String	|	|Multilingual|

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
                "name":"Korean heading2",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1554949320000,
                "updatedDt":1554949320000,
                "languages":{
                    "ko":"Korean heading2"
                }
            },
            {
                "categoryId":509,
                "serviceId":"multilanguage",
                "categoryCode":"code1",
                "parent":0,
                "name":"Chinese heading1",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1547949603000,
                "updatedDt":1554887489000,
                "languages":{
                    "ko":"Korean heading1",
                    "ja":"Japanese heading1",
                    "en":"English heading1",
                    "zh":"Chinese heading1"
                }
            }
        ]
    }
}
```

### Detailed Query of Notice Heading
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json												 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json										

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Detailed query of notice heading |HTTPS  |GET  |UTF-8|JSON    |Detailed query of notice heading by heading ID|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Heading ID / Heading code	|id	|String	|O	|{id} set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|Heading ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|	|Heading Code|
|	                |parent	        |Int	|	|Upper depth heading ID（Default:0）|
|	                |name	        |String	|O	|Heading name|
|	                |level	        |Int	|	|Depth（Fixed value:1）|
|	                |path	        |String	|	|Depth path（Fixed value:"\\\\"）|
|	                |orderNo	|Int	|	|Sort order（Default:0）|
|	                |createdDt	|Long	|	|Registered time|
|	                |updatedDt	|Long	|	|Edited time|
|	                |languages	|String	|	|Multilingual|

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
            "name":"Chinese heading1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"Korean heading1",
                "ja":"Japanese heading1",
                "en":"English heading1",
                "zh":"Chinese heading1"
            }
        }
    }
}
```

### Register Notice Heading
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category.json												 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category.json							

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Register notice heading |HTTPS  |POST  |UTF-8|JSON    |Register new heading|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Heading Information	|request body	|String	|O	|Heading information（JSON）|
|	    |name	    |String |		|Heading name（Unique value:yes ; Length:min = 0, max = 50 ; Format:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|Heading Code|
|	    |languages	        |String	|	|Multilingual|
|	    |orderNo	|Int	|	|Sort order（Fixed value:0）|

#### Request Body
```
Single Language
{
    "name":"Chinese heading3",
    "categoryCode":"game3",
    "orderNo":1
}

Multilingual
{
    "categoryCode":"game3",
    "parent":0,
    "orderNo":1,
    "languages":{
        "ko":"Korean heading3",
        "ja":"Japanese heading3",
        "en":"English heading3",
        "zh":"Chinese heading3"
    }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|Heading ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|	|Heading Code|
|	                |parent	        |Int	|	|Upper depth heading ID（Default:0）|
|	                |name	        |String	|O	|Heading name|
|	                |level	        |Int	|	|Depth（Fixed value:1）|
|	                |path	        |String	|	|Depth path（Fixed value:"\\\\"）|
|	                |orderNo	|Int	|	|Sort order（Default:0）|
|	                |createdDt	|Long	|	|Registered time|
|	                |updatedDt	|Long	|	|Edited time|
|	                |languages	|String	|	|Multilingual|

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
            "name":"Chinese heading3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"Korean heading3",
                "ja":"Japanese heading3",
                "en":"English heading3",
                "zh":"Chinese heading3"
            }
        }
    }
}
```

### Edit Notice Heading
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json												 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json			
											
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Edit notice heading |HTTPS  |POST  |UTF-8|JSON    |Edit notice heading through heading ID|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Heading ID / Heading code	|id	|String	|O	|{id} set in URL path|
|Heading Information	|request body	|String	|O	|Heading information（JSON）|
|	    |name	    |String |	    |Heading name（Unique value:yes ; Length:min = 0, max = 50 ; Format:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|Heading Code|
|	    |languages	|String	   |	|Multilingual|
|	    |orderNo	|Int	   |	|Sort order（Fixed value:0）|

#### Request Body
```
Single language
{
    "name":"Chinese heading3",
    "categoryCode":"game3",
    "orderNo":1
}

Multilingual
{
    "categoryCode":"game3",
    "orderNo":1,
    "languages":{
        "ko":"Korean heading3",
        "ja":"Japanese heading3",
        "en":"English heading3",
        "zh":"Chinese heading3"
    }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|Heading ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|	|Heading Code|
|	                |parent	        |Int	|	|Upper depth heading ID（Default:0）|
|	                |name	        |String	|O	|Heading name|
|	                |level	        |Int	|	|Depth（Fixed value:1）|
|	                |path	        |String	|	|Depth path（Fixed value:"\\\\"）|
|	                |orderNo	|Int	|	|Sort order（Default:0）|
|	                |createdDt	|Long	|	|Registered time|
|	                |updatedDt	|Long	|	|Edited time|
|	                |languages	|String	|	|Multilingual|

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
            "name":"Chinese heading3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"Korean heading3",
                "ja":"Japanese heading3",
                "en":"English heading3",
                "zh":"Chinese heading3"
            }
        }
    }
}
```

### Delete Notice Heading
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json												 
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json					
											
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Delete notice heading|HTTPS  |DELETE  |UTF-8|JSON    |Delete notice heading through heading ID|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|-----|------------|-----|---|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Heading ID / Heading code	|id	|String	|O	|{id} set in URL path|

#### Result Data
- None

