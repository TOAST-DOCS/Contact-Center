## Contact Center > Online Contact > API Guide for Developers > Ticket Management

### Create Ticket
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Create ticket  |HTTPS  |POST    |UTF-8|JSON    |Create new ticket|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Ticket Information |request body	|String	|O	|Ticket information（JSON)|
|    	     |categoryId	|Int	|X	|Category ID，If none, no need to specify|
|   	     |subject	    |String	|O	|Ticket title（max=255）|
|          |content	        |String	|O	|Ticket contents|
| 	       |endUser.usercode	|String	|O	|User code（Unique value）If usercode value is null because the inquiry was submitted by non-member, create unique value through format such as mail+name+phone number |
|	         |endUser.email	    |String	|X	|User email（When ticket is processed, answer mail would be sent to the email. If none, mail would not be sent.) Required value if ticket inquiry is processed in Online Contact|
|	         |endUser.username	|String	|X	|User name|
|          |endUser.phone	    |String	|X	|User phone number|
|	         |addition	        |String	|X	|Information about fields added in addition to default fields|
|            |status	        |String |X	|Value : open(processing), new(unassigned), default : open(processing)|
|	         |attachments[].attachmentId	|String	|X	|Attachment ID|

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

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|result.content	|ticketId	    |String	|O	|Ticket ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |subject	    |String	|O	|Ticket title|
|	              |categoryId	|Int	|X	|Submission category ID|
|               |categoryName	|String	|X	|Submission category name|
|	              |status	    |String	|O	|Ticket status (new : unassigned ; open : processing ; closed : processed)|
|	              |endUser.usercode	|String	|O	|User code（Unique value）|
|	              |endUser.email	|String	|X	|User email（When ticket is processed, answer mail would be sent to the email. If none, mail would not be sent.)|
|	              |endUser.username	|String	|X	|User name|
|	              |endUser.phone	|String	|X	|User phone number|
| 	            |content	|String	|O	|Ticket inquiry contents|
|	              |createdDt	|Long	|O	|Ticket created time|
|	              |updatedDt	|Long	|O	|Ticket updated time|
|               |contents	|String	|X	|Ticket processing information|
|	              |attachments[].attachmentId	|String	|X	|Attachment ID|
|	              |addition	|String	|X	|Information about fields added in addition to default fields|

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

### Process Ticket
#### Interface Description
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/solve.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/solve.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Process ticket  |HTTPS  |POST    |UTF-8|JSON    |Process ticket by ticket ID|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Ticket ID	|id	|String	|O	|Ticket ID|
|Response Contents|	comment	|String	|O	|{"comment":"Response Contents"} submitted by Request Body|
|Agent Name|	assigneeName	|String	|X	|Agent who will process the ticket, Default value : null|
|Attachment	|attachments	|String	|X	|Attachment ID（Format（File ID seperated by comma）：FileID1, FileID2, …, FileIDn）|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|result.content	|id	|String	|O	|Ticket ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |subject	|String	|O	|Ticket title|
|	              |categoryId	|Int	|X	|Submission category ID|
|	              |categoryName	|String	|X	|Submission category name|
|	              |status	|String	|O	|Ticket status（open:new ticket; closed:processed）|
|	              |endUser.usercode	|String	|O	|User code（unique value）|
|	              |endUser.email	|String	|X	|User email（When ticket is processed, answer mail would be sent to the email. If none, mail would not be sent.)|
|	              |endUser.username	|String	|X	|User name|
|	              |endUser.phone	|String	|X	|User phone number|
|	              |content	|String	|O	|Ticket inquiry contents|
|               |createdDt	|Long	|O	|Ticket created time|
|	              |updatedDt	|Long	|O	|Ticket updated time|
|	              |contents.content	|String	|X	|Ticket processing contents|
|	              |contents.createdDt	|Long	|X	|Processed time|
|	              |contents.attachments	|String	|X	|Ticket processing attachment ID|
|	              |attachments[].attachmentId	|String	|X	|Attachment ID|
|               |addition	|String	|X	|Information about fields added in addition to default fields|
|               |assigneeName	|String	|X	|Assigned agent, Default Value : null|


#### Request URL
?id=**TicketID**&assigneeName=**Ticket Assignee Name**	

#### Request Body
- Format: application/json;charset=UTF-8
```
{
   "comment":"Response Contents"
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
                    "createdDt":1586927311120,
                    "attachments":null
                }
            ],
            "attachments":null,
            "addition":null
           "assigneeName":"Name" 
        }
    }
}
```

### Ticket Detail
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/{id}.json			
- URL (Dev):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/{id}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Ticket detail |HTTPS  |GET    |UTF-8|JSON    |Query ticket through ticket ID|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Ticket ID	|id	|String	|O	|Ticket ID，{id} which is set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|result.content	|ticketId	|String	|O	|Ticket ID|
|	            |serviceId	|String	|O	|Service ID|
|	            |subject	|String	|O	|Ticket title|
|	            |categoryId	|Int	|X	|Submission category ID|
|	            |categoryName	|String	|X	|Submission category name|
|	            |status	        |String	|O	|Ticket status（open:new ticket; closed:processed）|
|	            |endUser.usercode	|String	|O	|User code（unique value)|
|	            |endUser.email	    |String	|X	|User email（When ticket is processed, answer mail would be sent to the email. If none, mail would not be sent.)|
|	            |endUser.username	|String	|X	|User name|
|	            |endUser.phone	    |String	|X	|User phone number|
|	            |content	        |String	|O	|Ticket query contents|
|	            |createdDt	        |Long	|O	|Ticket created time|
|	            |updatedDt	        |Long	|O	|Ticket updated time|
|	            |contents.content	|String	|X	|Ticket processing contents|
|	            |contents.createdDt	|Long	|X	|Ticket processed time|
|	            |contents.attachments.attachmentId	|String	|X	|Ticket processing attachment ID|
|	            |contents.attachments.fileName	|String	|X	|Ticket processing attachment name|
|	            |contents.attachments.contentType	|String	|X	|Ticket processing attachment type|
|	            |contents.attachments.disposition	|String	|X	|Ticket processing attachment process method（attachment:attached file）|
|	            |contents.attachments.size	|Long	|X	|Ticket processing attachment size|
|	            |contents.attachments.createdDt	|Long	|X	|Ticket processing attachment uploaded time|
|	            |attachments.attachmentId	|String	|X	|Ticket inquiry attachment ID|
|	            |attachments.fileName	|String	|X	|Ticket inquiry attachment name|
|	            |attachments.contentType	|String	|X	|Ticket inquiry attachment type|
|	            |attachments.disposition	|String	|X	|Ticket inquiry attachment process method（attachment:attached file）|
|	            |attachments.size	|Long	|X	|Ticket inquiry attachment size|
|	            |attachments.createdDt	|Long	|X	|Ticket inquiry attachment attached time|
|	            |addition	|String	|X	|Information about fields added in addition to default fields|
|               |assigneeName	|String	|X	|Assigned agent, Default Value : null|

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
            "assigneeName":"Name"
        }
    }
}
```

### Ticket List
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/list.json						
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/list.json				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Ticket list  |HTTPS  |GET    |UTF-8|JSON    |View list of tickets which meet search condition|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Start Time	|startDt	|String	|X	|Search scope start time(Ticket created time)(Format:yyyyMMddHHmmss）|
|Finish Time	|endDt	|String	|X	|Search scope finish time(Ticket created time)(Format:yyyyMMddHHmmss）|
|Ticket ID	|ticketId	|String	|X	|Ticket ID|
|Title	|subject	|String	|X	|Title|
|Ticket Status	|status	|String	|X	|Ticket status（open:New ticket; closed:Processed）|
|Submission Type	|categoryId	|Int	|X	|Submission type ID（If ID is multiple, separate by comma）|
|User Code	|usercode	|String	|X	|User code（Unique value）|
|User Name	|username	|String	|X	|User name|
|User Email	|email	  |String	|X	|User email|
|Sort Order	|sort	   |String	|X	|Sort order(Default:updatedDt:desc; Format variable:Sort（ascending order:asc, descending order:desc))|
|Page	|page	    |Int	|X	|Default value:1|
|Exposure by Page|pageSize	|Int	|X	|Default value:10; max=200|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|result.contents	|ticketId	|String	|O	|Ticket ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |subject	|String	|O	|Ticket title|
|	                |categoryId	|Int	|X	|Submission category ID|
|	                |categoryName	|String	|X	|Submission category name|
|	                |status	|String	|O	|Ticket status（open:New ticket; closed:Processed）|
|	                |createdDt	|Long	|O	|Ticket created time|
|	                |updatedDt	|Long	|O	|Ticket updated time|
|	                |addition	|String	|X	|Information about fields added in addition to default fields|
|result.total	|total	        |Long	|O	|Total items|
|result.pages	|pages	        |Int	|O	|Total pages|
|result.pageNum	|pageNum	    |Int	|O	|Current page|
|result.pageSize	|pageSize	|Int	|O	|Exposure by page|

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

### User Ticket List
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/{usercode}/list.json							
- URL (Dev): https://{domain}.alpha-oc.toast.co/{serviceId}/openapi/v1/ticket/{usercode}/list.json	

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|User ticket list |HTTPS  |GET    |UTF-8|JSON    |View user ticket list which meet search condition|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|User Code	|usercode	|String	|O	|User code(Unique value)，{usercode} set in URL path|
|Start Time	|startDt	|String	|X	|Search scope start time(Ticket created time)(Format:yyyyMMddHHmmss）|
|Finish Time	|endDt	|String	|X	|Search scope finish time(Ticket created time)(Format:yyyyMMddHHmmss）|
|Ticket ID	|ticketId	|String	|X	|Ticket ID|
|Title	|subject	|String	|X	|Title|
|Ticket Status	|status	|String	|X	|Ticket status（open:New ticket; closed:Processed）|
|Submission Type	|categoryId	|Int	|X	|Submission type ID（If ID is multiple, separate by comma）|
|Sort Order	|sort	   |String	|X	|Sort order(Default:updatedDt:desc; Format variable:Sort（ascending order:asc, descending order:desc))|
|Page	|page	    |Int	|X	|Default value:1|
|Exposure by Page|pageSize	|Int	|X	|Default value:10; max=200|


#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|result.contents	|ticketId	|String	|O	|Ticket ID|
|	                |serviceId	|String	|O	|Service ID|
|	                |subject	|String	|O	|Ticket title|
|	                |categoryId	|Int	|X	|Submission category ID|
|	                |categoryName	|String	|X	|Submission category name|
|	                |status	|String	|O	|Ticket status（open:New ticket; closed:Processed）|
|	                |createdDt	|Long	|O	|Ticket created time|
|	                |updatedDt	|Long	|O	|Ticket updated time|
|	                |addition	|String	|X	|Information about fields added in addition to default fields|
|result.total	|total	        |Long	|O	|Total items|
|result.pages	|pages	        |Int	|O	|Total pages|
|result.pageNum	|pageNum	    |Int	|O	|Current page|
|result.pageSize	|pageSize	|Int	|O	|Exposure by page|

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

### Attach File to Ticket
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json			 		
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json	

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Attach file to ticket  |HTTPS  |GET    |UTF-8|JSON    |Upload file to server|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|File	|file	|File	|O	|Submit file in form format|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|Attachment ID|
|	            |fileName	    |String	|O	|Attachment name|
|	            |contentType	|String	|O	|Attachment type|
|	            |disposition	|String	|O	|Attachment process method（attachment:Attachment）|
|	            |size	|Long	|O	|File size|
|               |createdDt	|Long	|O	|Attached time|

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

### Open/Download Ticket Attachment
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}		

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Open/Download Ticket Attachment  |HTTPS  |GET    |UTF-8|JSON    |Open/download file uploaded in server|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Attachment ID	|id	|String	|O	|Attachment id| 
|Process Method	|type	|String	|X	|Default is open by browser（download:Download file, open:Open file by browser）|

#### Result Data
- None

#### Response Body
- File

### Delete Attached File from Ticket 
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json		
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Delete Attached File from Ticket  |HTTPS  |DELETE    |UTF-8|JSON    |Delete file uploaded in server|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Attachment ID	|id	|String	|O	|Attachment id| 

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|Attachement id| 
|	            |fileName	|String	|O	|File name|
|	            |contentType	|String	|O	|File type|
|	            |size	|Long	|O	|File size|

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
