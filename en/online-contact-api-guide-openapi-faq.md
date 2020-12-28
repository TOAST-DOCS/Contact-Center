## Contact Center > Online Contact > API Guide for Developers > FAQ

### View FAQ List
#### Interface Description
- URL: https://{domain}.oc.toast.com /{serviceId}/openapi/v1/helpdoc.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/helpdoc.json			
	
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|View FAQ list |HTTPS  |GET    |UTF-8|JSON    |Retrun FAQ list by query conditions|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|Service ID	|serviceId	|Varchar(50)	|O	|Service ID, Set in URl path|
|Query Language	|language	|Varchar(2)	|X	|ko：Korean, zh：Chinese, ja：Japanese, en：English|
|Category ID	|category	|Int	|X	|Category ID|
|Recommendation	|recommend	|Boolean	|X	|true：Recommended，false：Not recommended|
|Top Fix	|top	|Boolean	|X	|true：Fixed into top，false：Not fixed into top|
|Status	|status	|Varchar(1)	|X	|D：Draft, O：In progress, C：Done|
|Keyword	|query	|Varchar	|X	|Search term|
|Query Field	|searchField	|Varchar	|X	|Default: Search by contents+title, title：Search by title, content：Search by contents|
|Sort Field	|sort	|Varchar	|X	|Can select sort condition by following fields : isTop, isRecommend, createdDt, updatedDt. If fields are multiple, separate by comma|
|Page	|page	|Int	|X	|Number of pages，Default value is 1| 
|Items by page	|pageSize	|Int	|X	|Data items by page，Default value is 10|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|------|---|
|result.contents	|helpDocId	|Long	|O	|FAQ ID|
|                 |serviceId	        |String	|O	|Service ID|
|	                |language	|String	|O	|ko：Korean, zh：Chinese, ja：Japanese, en：English|
| 	              |status	        |String	|O	|FAQ status. D：Draft, O：In progress, C：Done|
|	                |categoryId	|Int	|O	|Category ID|
|	                |categoryName	|String	|O	|Category name|
|	                |isRecommend	|Boolean	|O	|Recommend|
|	                |isTop	        |Boolean	|O	|Fixed top|
|	                |title	        |String	|O	|FAQ title|
|	                |userId	        |Int	|O	|Registered user ID|
|	                |userName	|String	|O	|Registered user name|
|	                |createdDt	|Long	|O	|FAQ registered time|
|	                |updatedDt	|Long	|O	|FAQ edited time|

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
        "title": "Chinese title1",
        "userId": 10063,
        "createdDt": 1547962599000,
        "updatedDt": 1548054677000,
        "userName": "Example",
        "categoryName": "Chinese category",
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### FAQ Detailed Query
#### Interface Description
- URL: https://{domain}.oc.toast.com /{serviceId}/openapi/v1/helpdoc/{id}.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/helpdoc/{id}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ detailed query |HTTPS  |GET    |UTF-8|JSON    |View detailed FAQ contents through FAQ ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|FAQ ID	|id	|Long	|O	|{id} set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |title	|String	|O	|FAQ title|
|	              |content	|String	|O	|FAQ contents|
| 	            |isRecommend	|Boolean	|O	|Recommendation|
| 	            |isTop	|Boolean	|O	|Top fix|
| 	            |status	|String	|O	|FAQ status. D：Draft, O：In progress, C：Done|
|	              |readCnt	|Int	|O	|Views|
|	              |userId	|Int	|O	|Registered user ID|
|	              |username	|String	|O	|Registered user name|
|	              |attachmentYn	|Boolean	|O	|Whether attachment is included |
|	              |createdDt	|Long	|O	|FAQ registered time|
|	              |updatedDt	|Long	|O	|FAQ edited time|
|	              |categories.categoryId	|Int	|O	|Category ID|
|	              |categories.parent	|String	|O	|Upper depth category ID|
|	              |categories.name	|String	|O	|Category name|
|	              |categories.level	|String	|O	|Category depth（1\|2\|3）|
|	              |contents.{language}.title	|String	|O	|Multilingual FAQ title|
|	              |contents.{language}.content	|String	|O	|Multilingual FAQ contents|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|Multilingual attachment ID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|Multilingual attachment name|
|	              |contents.{language}.attachments[].size	|Long	|O	|Multilingual attachment size|
|	              |attachments[].attachmentId	|String	|O	|Attachment ID|
|	              |attachments[].fileName	|String	|O	|Attachment name|
|	              |attachments[].size	|Long	|O	|Attachment size|

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
            "title":"Chinese title1",
            "content":"Chinese contents1",
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
                    "title":"Korean title1",
                    "content":"Korean contents1",
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
                    "title":"Japanese title1",
                    "content":"Japanese contents1",
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
                    "title":"Chinese title1",
                    "content":"Chinese contents1",
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
                    "title":"English title1",
                    "content":"English contents1",
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

### Register FAQ
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc.json			
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Register FAQ|HTTPS  |POST    |UTF-8|JSON    |Register new FAQ|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|request body	|categoryId	|String	|O	|Category ID|
|	        |title	        |String	|O	|FAQ title（Single language：Service language）|
|	        |content	|String	|O	|FAQ contents（Single language：Service language）|
|	        |status	        |String	|O	|FAQ status. D：Draft, O：In progress, C：Done|
|	        |isRecommend	|Boolean	|O	|Recommendation. true：Recommend, false：Do not recommend|
|	        |isTop	        |Boolean	|O	|Top fix. true：Fix into top, false：Do not fix into top|
|	        |contents.{language}.title	|String	|O	|FAQ title(Multilingual)|
| 	        |contents.{language}.content	|String	|O	|FAQ contents(Multilingual)|
|	        |contents.{language}.attachments[].attachmentId	|Array	|	|Attachment ID（Multilingual）|
|	        |attachments[].attachmentId	|String	|   	|Attachment ID（Multilingual）|

#### Request Body
```
Single Language
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

Multilingual
{
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "contents":{
        "ko":{
            "title":"Korean title1",
            "content":"Korean contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "ja":{
            "title":"Japanese title1",
            "content":"Japanese contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "zh":{
            "title":"Chinese title1",
            "content":"Chinese contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "en":{
            "title":"English title1",
            "content":"English contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        }
    }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|---------|-----------|---------|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |title	|String	|O	|FAQ title|
|	              |content	|String	|O	|FAQ contents|
| 	            |isRecommend	|Boolean	|O	|Recommendation. true：Recommended, false：Not recommended|
| 	            |isTop	|Boolean	|O	|Top fix. true：Fixed into top, false：Not fixed into top|
| 	            |status	|String	|O	|FAQ status. D：Draft, O：In progress, C：Done|
|	              |readCnt	|Int	|O	|Views|
|	              |userId	|Int	|O	|Registered user ID|
|	              |username	|String	|O	|Registered user name|
|	              |attachmentYn	|Boolean	|O	|Whether attachment is included |
|	              |createdDt	|Long	|O	|FAQ registered time|
|	              |updatedDt	|Long	|O	|FAQ edited time|
|	              |categories.categoryId	|Int	|O	|Category ID|
|	              |categories.parent	|String	|O	|Upper depth category ID|
|	              |categories.name	|String	|O	|Category name|
|	              |categories.level	|String	|O	|Category depth（1\|2\|3）|
|	              |contents.{language}.title	|String	|O	|Multilingual FAQ title|
|	              |contents.{language}.content	|String	|O	|Multilingual FAQ contents|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|Multilingual attachment ID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|Multilingual attachment name|
|	              |contents.{language}.attachments[].size	|Long	|O	|Multilingual attachment size|
|	              |attachments[].attachmentId	|String	|O	|Attachment ID|
|	              |attachments[].fileName	|String	|O	|Attachment name|
|	              |attachments[].size	|Long	|O	|Attachment size|

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
            "title":"Chinese title1",
            "content":"Chinese contents1",
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
                    "title":"Korean title1",
                    "content":"Korean contents1",
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
                    "title":"Japanese title1",
                    "content":"Japanese contents1",
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
                    "title":"Chinese title1",
                    "content":"Chinese contents1",
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
                    "title":"English title1",
                    "content":"English contents1",
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

### Edit FAQ
#### Interface Descripton
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json					
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json			
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Edit FAQ |HTTPS  |PUT    |UTF-8|JSON    |Edit contents through FAQ ID|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|FAQ ID	   |helpDocId	   |Long	|O	|{id} set in URL path|
|request body	|categoryId	|String	|O	|Category ID|
|	        |title	        |String	|O	|FAQ title（Single language: Service language）|
|	        |content	|String	|O	|FAQ contents（Single language: Service language）|
|	        |status	        |String	|O	|FAQ status. D：Draft, O：In progress, C：Done|
|	        |isRecommend	|Boolean	|O	|Recommendation. true：recommend, false：Do not recommend|
|	        |isTop	        |Boolean	|O	|Top fix. true：Fix in top, false：Do not fix in top|
|	        |contents.{language}.title	|String	|O	|FAQ title(Multilingual)|
|	        |contents.{language}.content	|String	|O	|FAQ contents(Multilingual)|
|	        |contents.{language}.attachments[].attachmentId	|Array	  |	|Attachment ID（Multilingual）|
|	        |attachments[].attachmentId	|String	    |	|Attachment ID（Single language）|

#### Request Body
```
Single Language
{
    "title":"Chinese title1",
    "content":"Chinese contents1",
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

Multilingual
{
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "contents":{
        "ko":{
            "title":"Korean title1",
            "content":"Korean contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "ja":{
            "title":"Japanese title1",
            "content":"Japanese contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "zh":{
            "title":"Chinese title1",
            "content":"Chinese contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "en":{
            "title":"English title1",
            "content":"English contents1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        }
    }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|------------|---------|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |title	|String	|O	|FAQ title|
|	              |content	|String	|O	|FAQ contents|
| 	            |isRecommend	|Boolean	|O	|Recommendation. true：Recommended, false：Not recommended|
| 	            |isTop	|Boolean	|O	|Top fix. true：Fixed into top, false：Not fixed into top|
| 	            |status	|String	|O	|FAQ status. D：Draft, O：In progress, C：Done|
|	              |readCnt	|Int	|O	|Views|
|	              |userId	|Int	|O	|Registered user ID|
|	              |username	|String	|O	|Registered user name|
|	              |attachmentYn	|Boolean	|O	|Whether attachment is included |
|	              |createdDt	|Long	|O	|FAQ registered time|
|	              |updatedDt	|Long	|O	|FAQ edited time|
|	              |categories.categoryId	|Int	|O	|Category ID|
|	              |categories.parent	|String	|O	|Upper depth category ID|
|	              |categories.name	|String	|O	|Category name|
|	              |categories.level	|String	|O	|Category depth（1\|2\|3）|
|	              |contents.{language}.title	|String	|O	|Multilingual FAQ title|
|	              |contents.{language}.content	|String	|O	|Multilingual FAQ contents|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|Multilingual attachment ID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|Multilingual attachment name|
|	              |contents.{language}.attachments[].size	|Long	|O	|Multilingual attachment size|
|	              |attachments[].attachmentId	|String	|O	|Attachment ID|
|	              |attachments[].fileName	|String	|O	|Attachment name|
|	              |attachments[].size	|Long	|O	|Attachment size|

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
            "title":"Chinese title1",
            "content":"Chinese contents1",
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
                    "title":"Korean title1",
                    "content":"Korean contents1",
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
                    "title":"Japanese title1",
                    "content":"Japanese contents1",
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
                    "title":"Chinese title1",
                    "content":"Chinese contents1",
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
                    "title":"English title1",
                    "content":"English contents1",
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

### Set FAQ Fix by Category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/recommend.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/recommend.json		

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Set FAQ fix by category |HTTPS  |PUT    |UTF-8|JSON    |Set the FAQ document to be pinned to the top of the category to which it belongs to|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|FAQ ID	|Id	          |Int	|O	|{id} set in URL path|
|Recommendation	|recommend	|Boolean	|O	|true：recommend, false：Do not recommend|

#### Result Data
- None

### Set FAQ fixed by Main
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/top.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/top.json			
		
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Set FAQ fixed by main |HTTPS  |PUT    |UTF-8|JSON    |Set the FAQ document to be pinned to the top of the help center main screen|Common authentication |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|FAQ ID	|Id	          |Int	|O	|{id} set in URL path|
|Fix to top	|top	|Boolean	|O	|true：Fix to top, false：Do not fix to top|

#### Result Data
- None

### Set FAQ to be Done
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/close.json				
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/close.json		

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Set FAQ to be done |HTTPS  |PUT    |UTF-8|JSON    |Change FAQ status to done(status = C)|Common authentication |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|FAQ ID	   |Id	           |Int	   |O	   |{id} set in URL path|

#### Result Data
- None

### Delete FAQ
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json					
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Delete FAQ |HTTPS  |DELETE    |UTF-8|JSON    |Delete FAQ through FAQ ID|Common authentication |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|FAQ ID	|Id	          |Int	|O	|{id} set in URL path|

#### Result Data
- None

### View FAQ Category List
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/helpdoc/categories.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/categories.json			
			
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|View FAQ category list |HTTPS  |GET    |UTF-8|JSON    |View FAQ category list|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	  |String	|O	|{serviceId} set in URL path|
|Lower Depth Category ID	|child	|Int	|X	|Lower depth category ID sent when upper depth category ID obtained| 
|Upper Depth Category ID	|parent	|Int	|X	|Upper depth category ID sent when lower depth category ID obtained|

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|---------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|Category ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|X	|Category Code|
|	                |parent	        |Int	|X	|Upper depth category ID（Default:0）|
|	                |name	        |String	|O	|Category name|
|	                |level	        |Int	|X	|Depth（1\|2\|3）|
|	                |path	        |String	|X	|Depth path（"\level1\level2\"）|
|	                |orderNo	|Int	|X	|Sort order（Default:0）|
|	                |createdDt	|Long	|X	|Registered time|
|	                |updatedDt	|Long	|X	|Edited time|
|	                |languages	|String	|X	|Multilingual|

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
                "name":"Korean Category2",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1554949320000,
                "updatedDt":1554949320000,
                "languages":{
                    "ko":"Korean Category2"
                }
            },
            {
                "categoryId":509,
                "serviceId":"multilanguage",
                "categoryCode":"code1",
                "parent":0,
                "name":"Chinese Category1",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1547949603000,
                "updatedDt":1554887489000,
                "languages":{
                    "ko":"Korean Category1",
                    "ja":"Japanese Category1",
                    "en":"English Category1",
                    "zh":"Chinese Category1"
                }
            }
        ]
    }
}
```

### Detailed View of FAQ Category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/helpdoc/category/{id}.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json		
						
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Detailed view of FAQ category |HTTPS  |GET    |UTF-8|JSON    |View detailed contents of FAQ through category ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Category ID or Category Code	|id	|String	|O	|{id} set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|------------|---------|----|
|result.contents	|categoryId	|Int	|O	|Category ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|X	|Category code|
|	                |parent	        |Int	|X	|Upper depth category ID（Default:0）|
|	                |name	        |String	|O	|Category name|
|	                |level	        |Int	|X	|Depth（1\|2\|3）|
|	                |path	        |String	|X	|Depth path（"\level1\level2\"）|
|	                |orderNo	|Int	|X	|Sort order（Default: 0）|
|	                |createdDt	|Long	|X	|Registered time|
|	                |updatedDt	|Long	|X	|Edited time|
|	                |languages	|String	|X	|Multilingual|

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
            "name":"Chinese category1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"Korean category1",
                "ja":"Japanese category1",
                "en":"English category1",
                "zh":"Chinese category1"
            }
        }
    }
}
```

### Add FAQ Category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category.json			
							
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Add FAQ category |HTTPS  |POST    |UTF-8|JSON    |Add new FAQ category|Common authentication |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Category Information	|request body	|String	    |O	|Category information（JSON）|
|	             |name	     |String     |		|Category name（Unique value:yes ; Length:min = 0, max = 50 ; Format:^(\_\|-\|[^\\pP])+$）|
|	              |categoryCode	|String	 |	|Category code|
|	              |languages	|String	 |	|Multilingual|
|	              |parent	        |Int	 |	|Upper depth category ID（Default:0）|
|	              |orderNo	        |Int	 |	|Sort order（Default:0）|

#### Request Body
```
Single Language
{
    "name":"Chinese category3",
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
        "ko":"Korean category3",
        "ja":"Japanese category3",
        "en":"English category3",
        "zh":"Chinese category3"
    }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|result.contents	|categoryId	|Int	|O	|Category ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|X	|Category code|
|	                |parent	        |Int	|X	|Upper depth category ID（Default:0）|
|	                |name	        |String	|O	|Category name|
|	                |level	        |Int	|X	|Depth（1\|2\|3）|
|	                |path	        |String	|X	|Depth path（"\level1\level2\"）|
|	                |orderNo	|Int	|X	|Sort order（Default: 0）|
|	                |createdDt	|Long	|X	|Registered time|
|	                |updatedDt	|Long	|X	|Edited time|
|	                |languages	|String	|X	|Multilingual|

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
            "name":"Chinese Category3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"Korean Category3",
                "ja":"Japanese Category3",
                "en":"English Category3",
                "zh":"Chinese Category3"
            }
        }
    }
}
```

### Edit FAQ Category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
									
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Edit FAQ category |HTTPS  |PUT    |UTF-8|JSON    |Edit category name through category ID|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Category ID or Category Code	|Id	|String	|O	|{id} set in URL path|
|Category Information	            |request body	|String	|O	|Category information（JSON）|
|	                         |name	             |String  |	     |Category name（Unique value:yes ; Length:min = 0, max = 50 ; Format:^(\_\|-\|[^\\pP])+$）|
|	                         |categoryCode	     |String  |	     |Category Code|
|	                         |languages	     |String  |	     |Multilingual|
|	                         |parent	     |Int     |	     |Upper depth category ID（Default:0）|
|	                         |orderNo	     |Int     |	     |Sort order（Default:0）|

#### Request Body
```
Single Language
{
    "name":"Chinese category2",
    "categoryCode":"game0",
    "orderNo":2,
    "parent":509
}

Multilingual
{
    "categoryCode":"game0",
    "parent":509,
    "orderNo":2,
    "languages":{
        "ko":"Korean category2",
        "ja":"Japanese category2",
        "en":"English category2",
        "zh":"Chinese category2"
    }
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|---------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|Category ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |categoryCode	|String	|X	|Category code|
|	                |parent	        |Int	|X	|Upper depth category ID（Default:0）|
|	                |name	        |String	|O	|Category name|
|	                |level	        |Int	|X	|Depth（1\|2\|3）|
|	                |path	        |String	|X	|Depth path（"\level1\level2\"）|
|	                |orderNo	|Int	|X	|Sort order（Default: 0）|
|	                |createdDt	|Long	|X	|Registered time|
|	                |updatedDt	|Long	|X	|Edited time|
|	                |languages	|String	|X	|Multilingual|

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
            "name":"Korean category",
            "level":1,
            "path":"\",
            "orderNo":1,
            "createdDt":1587349288181,
            "updatedDt":1587349288181,
            "languages":{
                "ko":"Korean category",
                "ja":"Japanese category",
                "zh":"Chinese category",
                "en":"English category"
            }
        }
    }
}
```

### Delete FAQ category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
									
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Delete FAQ category |HTTPS/80  |DELETE    |UTF-8|JSON    |Delete FAQ category through category ID|Common authentication |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URL path|
|Category ID or Category Code	|id	|String	|O	|{id} set in URL path|

#### Result Data
- None

### Attach File in FAQ
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/help/upload.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/help/upload.json	
									
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Attach file in FAQ |HTTPS  |POST    |UTF-8|JSON    |Upload file in server|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set in URl path|
|File	|file	|File	|O	|Submit file through form|

####Result Data
|Name |Variable |Data type |Required | Description|
|---------|--------|------------|--------|-----|
|result.content	|attachmentId	|String	|O	|Attachment ID|
|	        |fileName	|String	|O	|File name|
|	        |contentType	|String	|O	|File type|
|	        |size 	        |Long	|O	|File size|

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

### Open/Download FAQ Attachment
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/attachments/help/{id}
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/attachments/help/{id}			
									
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Open/download FAQ attachment |HTTPS  |GET    |UTF-8|FILE    |Open/download server uploaded FAQ attachment|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	          |serviceId	|String	|O	|{serviceId} set in URL path|
|Uploaded File ID	|id	      |String  |O     |Uploaded file id| 
|Open Method         |type	       |String	       |Default: Open（download:Download,open:Open）|

#### Result Data
- None

#### Response Body
- File

### Delete FAQ Attachment
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/help/{id}.json				
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/help/{id}.json	
									
|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Delete FAQ attachment |HTTPS  |DELETE    |UTF-8|JSON    |Delete server uploaded file|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|----|------|-----------|----|----|
|Service ID	          |serviceId	|String	|O	|{serviceId} set in URL path|
|Uploaded File ID	|id	      |String  |O     |Uploaded file id| 

#### Result Data
- None

