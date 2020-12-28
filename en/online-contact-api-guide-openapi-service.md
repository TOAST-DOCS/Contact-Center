## Contact Center > Online Contact > API Guide for Developers > Service 

### Contract Item Code
- ticket: Ticket (Enabled by default, Cannot change)
- chat: Chat
- telticket: Ticket (Call included - Use of CTI included)
- endusermanagement: Customer Information Management
- callback: Callback
- helpdoc: FAQ
- knowledge: Knowledge Management
- issuetransferstatistics: Issue Escalation Statistics (Will be added)
- reinquiryrate: Re-inquiry rate (Will be added)
- smssend: SMS (Will be added)
- smssendingstatus: SMS Sending Status (Will be added)
- electronicboard: Dashboard (Will be added)
- ticketevaluation: Ticket Evaluation (Will be added)
- happycall: Happy call (Will be added)
- security: Security Service (Will be added)

### Add service
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/add.json
- URL(Dev): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/add.json

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Add service |HTTPS  |POST    |UTF-8|JSON    |Add new service|Common Authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|Service Information	|request body	|String	|O	|Service Information (JSON)|
|	          |serviceId	  |String	|O	|Service ID (Unique value:yes ; length:min = 0, max = 45 ; format:english)|
|	          |name	        |String	|O	|Service name (Unique value:yes; length:min = 0, max = 100)|
|	          |language	    |String	|O	|Service language (Value:zh\|ja\|ko\|en, ko:Korean, ja:Japanese, en:English, zh:Chinese)|
|				    |timeZone	    |String	|X	|Time Zone (Value:Asia/Seoul\|Asia/Tokyo\|...)|

Default values for variable timeZone are as follows:
- language=ko: timeZone=Asia/Seoul
- language=ja: timeZone=Asia/Tokyo
- language=en: timeZone=America/New_York
- language=zh: timeZone=Asia/Shanghai

#### Request Body
```
{
    "serviceId":"GameBaseService",
    "name":"GameBaseServiceAPI",
    "language":"ko",
    "timeZone":"Asia/Seoul"
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|------|----------|-----|----|
|result.content	|serviceId	|String	|O	|Service ID|
|	              |name	      |String	|O	|Service name|
|	              |active	    |Boolean	|X	|Service status(true:Enabled, false:Disabled)|
|	              |language	  |String	  |O	|Service language（Value:zh\|ja\|ko\|en, ko:Korean, ja:Japanese, en:English, zh:Chinese)|
|	              |timeZone 	|String	  |X	|Time Zone (Value:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|Service created time|
|	              |updatedDt	|Long	    |X	|Service updated time|
|               |securityKey	|String	|X	|Open API Key|

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

### Service detail
#### Interface Description
- URL:	https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json			
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Service detail  |HTTPS  |GET    |UTF-8|JSON    |View service information by service ID|Common Authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|result.content	|serviceId	|String	|O	|Service ID|
|	              |name	      |String	|O	|Service name|
|	              |active	    |Boolean	|X	|Service status(true:Enabled, false:Disabled)|
|	              |language	  |String	  |O	|Service language（Value:zh\|ja\|ko\|en, ko:Korean, ja:Japanese, en:English, zh:Chinese)|
|	              |timeZone 	|String	  |X	|Time Zone (Value:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|Service created time|
|	              |updatedDt	|Long	    |X	|Service updated time|
|               |securityKey	|String	|X	|Open API Key|

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

### Edit service
#### Interface Description
- URL:	https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json 						
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json 				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Edit service  |HTTPS  |PUT    |UTF-8|JSON    |Edit service information through service ID|Common Authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Service Information	|request body	|String	|O	|Service information（JSON）|
|	          |name	|String	|O	|Service name (Unique value:yes; length:min = 0, max = 100)|
|	          |language	|String	|O	|Service language（Value:zh\|ja\|ko\|en, ko:Korean, ja:Japanese, en:English, zh:Chinese)|
|	          |timeZone	|String	|X	|Time Zone(Value:Asia/Seoul\|Asia/Tokyo\|...)|

Default values for variable timeZone are as follows:
- language=ko: timeZone=Asia/Seoul
- language=ja: timeZone=Asia/Tokyo
- language=en: timeZone=America/New_York
- language=zh: timeZone=Asia/Shanghai

#### Request Body
```
{
    "name":"GameBaseServiceAPI",
    "language":"ko",
    "timeZone":"Asia/Seoul"
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|result.content	|serviceId	|String	|O	|Service ID|
|	              |name	      |String	|O	|Service name|
|	              |active	    |Boolean	|X	|Service status(true:Enabled, false:Disabled)|
|	              |language	  |String	  |O	|Service language（Value:zh\|ja\|ko\|en, ko:Korean, ja:Japanese, en:English, zh:Chinese)|
|	              |timeZone 	|String	  |X	|Time Zone (Value:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|Service created time|
|	              |updatedDt	|Long	    |X	|Service updated time|
|               |securityKey	|String	|X	|Open API Key|

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
            "active":null,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "createdDt":null,
            "updatedDt":1586761475102,
            "securityKey":null
        }
    }
}
```

### Disable service
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/disable.json							
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/disable.json			 				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Disable service|HTTPS  |PUT    |UTF-8|JSON    |Disable service through service ID   |Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|serviceId	|String	|O	|Service ID（query）|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|result.content	|serviceId	|String	|O	|Service ID|
|	              |name	      |String	|O	|Service name|
|	              |active	    |Boolean	|X	|Service status(true:Enabled, false:Disabled)|
|	              |language	  |String	  |O	|Service language（Value:zh\|ja\|ko\|en, ko:Korean, ja:Japanese, en:English, zh:Chinese)|
|	              |timeZone 	|String	  |X	|Time Zone (Value:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|Service created time|
|	              |updatedDt	|Long	    |X	|Service updated time|
|               |securityKey	|String	|X	|Open API Key|

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
            "active":false,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "updatedDt":1586745222000,
            "updatedDt":1586761475000,
            "securityKey":null
        }
    }
}

```

### Enable service
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/enable.json					
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/enable.json					 				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Enable service  |HTTPS  |PUT    |UTF-8|JSON    |Enable service through service ID  |Common Authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|serviceId	|String	|O	|Service ID（query）|

#### Result Data
|Name |Variable |Data type |Required | Description|
|----|-----|------------|----|----|
|result.content	|serviceId	|String	|O	|Service ID|
|	              |name	      |String	|O	|Service name|
|	              |active	    |Boolean	|X	|Service status(true:Enabled, false:Disabled)|
|	              |language	  |String	  |O	|Service language（Value:zh\|ja\|ko\|en, ko:Korean, ja:Japanese, en:English, zh:Chinese)|
|	              |timeZone 	|String	  |X	|Time Zone (Value:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|Service created time|
|	              |updatedDt	|Long	    |X	|Service updated time|
|               |securityKey	|String	|X	|Open API Key|


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
            "serviceId":"GameBaseService",
            "name":"GameBaseServiceAPI",
            "active":true,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "updatedDt":1586745222000,
            "updatedDt":1586761475000,
            "securityKey":null
        }
    }
}
```

### Delete service
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json					
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json							 			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Delete service  |HTTPS  |DELETE    |UTF-8|JSON    |Delete disabled service by service ID | Common Authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|result.content	|	|String	|X	|"SUCCESS":Deleted, "ENABLE":Service enabled, cannot delete. Can delete after service is disabled.|

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

### Reissue Service API Key
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/apikey/refresh.json						
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/apikey/refresh.json							

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Reissue Service API Key|HTTPS  |PUT    |UTF-8|JSON    |Reissue API key generated to the service through the service ID|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|serviceId	|String	|O	|Service ID（query）|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|result.content		|String	|X	|New API Key|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":"bd7a45aa764f4936a43ef0c4500da7ba"
    }
}
```

### List of services
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/list.json			 			
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/list.json								 				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|List of services |HTTPS  |GET    |UTF-8|JSON    |View all services created in the organization|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Page	|page	|Int	|	|Default:1|
|Exposure per page	|pageSize	|Int	|	|Default:100|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|result.contents	|serviceId	|String	|O	|Service ID|
|	                |name	|String	|O	|Service name|
|	                |active	|Boolean	|X	|Service status. true:Enabled, false:Disabled|
|	                |language	|String	|O	|Service language（Value:zh\|ja\|ko\|en）ko:Korean, ja:Japanese, en:English, zh:Chinese|
|	                |timeZone	|String	|X	|Time Zone(Value:Asia/Seoul\|Asia/Tokyo\|...）|
|	                |createdDt	|Long	|X	|Service created time|
|	                |updatedDt	|Long	|X	|Service updated time|
|	                |securityKey	|String	|X	|Open API Key|
|result.total	|total	|Long	|X	|Total number of cases|
|result.pages	|pages	|Int	|X	|Total number of pages|
|result.pageNum	|pageNum	|Int	|X	|Current page|
|result.pageSize	|pageSize	|Int	|X	|Exposure per page|

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
                "serviceId":"gamebase",
                "name":"Gamebase",
                "active":true,
                "language":"ko",
                "timeZone":"Asia/Shanghai",
                "createdDt":1552901051000,
                "updatedDt":1566203644000,
                "securityKey":"1b7426d5821b42bc9e1503bfb2979aee"
            },
            {
                "serviceId":"GameBaseService",
                "name":"GameBaseServiceAPI",
                "active":true,
                "language":"ko",
                "timeZone":"Asia/Seoul",
                "createdDt":1586745222000,
                "updatedDt":1586765984000,
                "securityKey":"bd7a45aa764f4936a43ef0c4500da7ba"
            },
        ],
        "total":2,
        "pages":1,
        "pageNum":1,
        "pageSize":100
    }
}
```

### Register service contract
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/reg.json			
- URL (Dev):	https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/reg.json						 				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Register service contract |HTTPS  |POST    |UTF-8|JSON    |Register new service contract|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service Contract Information	|request body	|String	|O	|Service information(JSON)|
|	                |serviceId	   |String	|O	|Service ID(Unique value:yes; Length:min = 0, max = 45;Format: English)|
|	                |billingSettings	|List	|X	  |Contract item configuration list|
|	                |    billingSettingCode	|String	|O	|Item code(Refer contract item code)|
|	                |    active	            |Boolean	|X	|Enable:true, Disable:false|

#### Request Body
```
{
        "serviceId": "example",
        "billingSettings": [{
                "billingItemCode": "callback",
                "active": false
        }, {
                "billingItemCode": "chat",
                "active": true
        }, {
                "billingItemCode": "endusermanagement",
                "active": false
        }, {
                "billingItemCode": "helpdoc",
                "active": false
        }, {
                "billingItemCode": "knowledge",
                "active": true
        }, {
                "billingItemCode": "telticket",
                "active": false
        }]
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|----|-----|
|result.content	|id	|Long	|O	|Contract ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |organizationId	|String	|O	|Organization ID|
|	              |type	          |Int	  |O	|Service type(1:Consulation management, 2:Issue management), Default:1|
|	              |status	        |String	|O	|Contract status(Creating:create, In use:inuse, Stop use:pause, Terminate:stop)|
|	              |startDt	      |String	|O	|Start date of service use(Korean Time)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|Discount rate(%)|
|	              |freeExtension	|Int	  |O	|Free trial extension date|
|	              |active	        |Boolean	|O	|Service contract(Enabled:true, Disabled:false)|
|	              |freeTrial	    |Boolean	|O	|Free trial period(Yes:true, No:false)|
|	              |billingSettings	|List	  |O	|Contract item configuration list|
|	              |    id	              |Long	  |O	|Contract item configuration ID|
|	              |    billingId	      |Long	  |O	|Contract ID|
|	              |    billingSettingCode	|String	|O	|Item code(Refer contract item code)|
|	              |    active	            |Boolean	|O	|Enabled:true, Disabled:false|

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
                        "id": 214,
                        "organizationId": "WopqM8euoYw89B7i",
                        "organizationName": "NHN-CS",
                        "serviceId": "example",
                        "serviceName": "example",
                        "type": 1,
                        "language": "zh",
                        "status": "inuse",
                        "startDt": "20201204090910",
                        "discountRate": 0,
                        "freeExtension": 0,
                        "email": "xxxxxxxxxxxx@nhn.com",
                        "active": true,
                        "createdDt": 1607044142000,
                        "updatedDt": 1607044150934,
                        "freeTrial": false,
                        "billingSettings": [{
                                "id": 656,
                                "billingId": 214,
                                "billingItemCode": "callback",
                                "active": false
                        }, {
                                "id": 657,
                                "billingId": 214,
                                "billingItemCode": "chat",
                                "active": true
                        }, {
                                "id": 658,
                                "billingId": 214,
                                "billingItemCode": "endusermanagement",
                                "active": false
                        }, {
                                "id": 659,
                                "billingId": 214,
                                "billingItemCode": "helpdoc",
                                "active": false
                        }, {
                                "id": 660,
                                "billingId": 214,
                                "billingItemCode": "knowledge",
                                "active": true
                        }, {
                                "id": 661,
                                "billingId": 214,
                                "billingItemCode": "telticket",
                                "active": false
                        }, {
                                "id": 662,
                                "billingId": 214,
                                "billingItemCode": "ticket",
                                "active": true
                        }]
                }
        }
}
```

### Change service contract
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/update/{billingId}.json						
- URL (Dev): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/update/{billingId}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Change service contract (Only once a day) |HTTPS  |PUT    |UTF-8|JSON    |Change contract|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service Contract Information	|request body	|String	|O	|Service Information(JSON)|
|	                |id	          |Long	  |O	|Contract ID|
|	                |serviceId	  |String	|O	|Service ID(Unique Value:Yes; Length:min = 0, max = 45; Format:English)|
|	                |billingSettings	|List	|O	|Contract item configuration list|
|	                |id	              |Long	|O	|Contract item configuration ID|
|	                |billingId	      |Long	|X	|Contract ID|
|	                |    billingSettingCode	|String	|O	|Item code(Refer contract item code)|
|	                |    active	            |Boolean	|X	|Enable:true  Disable:false|

#### Request Body
```
{
        "id": 205,
        "serviceId": "qwqwqw",
        "billingSettings": [{
                "id": 620,
                "billingId": 205,
                "billingItemCode": "callback",
                "active": false
        }, {
                "id": 621,
                "billingId": 205,
                "billingItemCode": "chat",
                "active": false
        }, {
                "id": 622,
                "billingId": 205,
                "billingItemCode": "endusermanagement",
                "active": false
        }, {
                "id": 623,
                "billingId": 205,
                "billingItemCode": "helpdoc",
                "active": false
        }, {
                "id": 624,
                "billingId": 205,
                "billingItemCode": "knowledge",
                "active": false
        }, {
                "id": 625,
                "billingId": 205,
                "billingItemCode": "telticket",
                "active": false
        }]
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|Contract ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |organizationId	|String	|O	|Organization ID|
|	              |type	          |Int	  |O	|Service type(1:Consulation management, 2:Issue management), Default:1|
|	              |status	        |String	|O	|Contract status(Creating:create, In use:inuse, Stop use:pause, Terminate:stop)|
|	              |startDt	      |String	|O	|Start date of service use(Korean Time)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|Discount rate(%)|
|	              |freeExtension	|Int	  |O	|Free trial extension date|
|	              |active	        |Boolean	|O	|Service contract(Enabled:true, Disabled:false)|
|	              |freeTrial	    |Boolean	|O	|Free trial period(Yes:true, No:false)|
|	              |billingSettings	|List	  |O	|Contract item configuration list|
|	              |    id	              |Long	  |O	|Contract item configuration ID|
|	              |    billingId	      |Long	  |O	|Contract ID|
|	              |    billingSettingCode	|String	|O	|Item code(Refer contract item code)|
|	              |    active	            |Boolean	|O	|Enabled:true, Disabled:false|

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
            "id": 205,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "qwqwqw",
            "serviceName": "qwqwqw",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201202115045",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606877440000,
            "updatedDt": 1607046392063,
            "freeTrial": false,
            "billingSettings": [{
                "id": 620,
                "billingId": 205,
                "billingItemCode": "callback",
                "active": false
            }, {
                "id": 621,
                "billingId": 205,
                "billingItemCode": "chat",
                "active": false
            }, {
                "id": 622,
                "billingId": 205,
                "billingItemCode": "endusermanagement",
                "active": false
            }, {
                "id": 623,
                "billingId": 205,
                "billingItemCode": "helpdoc",
                "active": false
            }, {
                "id": 624,
                "billingId": 205,
                "billingItemCode": "knowledge",
                "active": false
            }, {
                "id": 625,
                "billingId": 205,
                "billingItemCode": "telticket",
                "active": false
            }]
        }
    }
}

When changed more than once a day，Response：
{
    "header": {
        "resultCode": 9015,
        "resultMessage": "billing.setting.today.already.changed",
        "isSuccessful": false
    },
    "result": {
        "content": {
            "exception": "OcException",
            "message": "billing.setting.today.already.changed"
        }
    }
}
```

### List of service contracts
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/list.json									
- URL (Dev): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/list.json									 				

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|List of service contracts|HTTPS  |GET    |UTF-8|JSON    |Obtain list of service contracts|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Obtain list of service contracts	|page	|Int	|X	|Page, default:1|
|	                              |pageSize	|Int	|X	|Exposure by page，default:10|
|	                              |billingSettingCode	|		|   |   |
|	                              |active			        |   |   |   |

#### Request URL
```
/openapi/v1/admin/billing/list.json?page=1&pageSize=10	
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|----|
|result.contents	|id	|Long	|O	|Contract ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |organizationId	|String	|O	|Organization ID|
|	              |type	          |Int	  |O	|Service type(1:Consulation management, 2:Issue management), Default:1|
|	              |status	        |String	|O	|Contract status(Creating:create, In use:inuse, Stop use:pause, Terminate:stop)|
|	              |startDt	      |String	|O	|Start date of service use(Korean Time)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|Discount rate(%)|
|	              |freeExtension	|Int	  |O	|Free trial extension date|
|	              |active	        |Boolean	|O	|Service contract(Enabled:true, Disabled:false)|
|	              |freeTrial	    |Boolean	|O	|Free trial period(Yes:true, No:false)|

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
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000
        }, {
            "id": 212,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201203154729",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606981630000,
            "updatedDt": 1606981649000
        }, {
            "id": 205,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "qwqwqw",
            "serviceName": "qwqwqw",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201202115045",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606877440000,
            "updatedDt": 1607046392000
        }, {
            "id": 196,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example2",
            "serviceName": "example2",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201201105044",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606787441000,
            "updatedDt": 1606875428000
        }, {
            "id": 192,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example3",
            "serviceName": "example3",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201127082852",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606436928000,
            "updatedDt": 1606436933000
        }, {
            "id": 191,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example4",
            "serviceName": "example4",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201127072001",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606432792000,
            "updatedDt": 1606432802000
        }, {
            "id": 154,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example5",
            "serviceName": "example5",
            "type": 1,
            "language": "ja",
            "status": "inuse",
            "startDt": "20201124103657",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606181811000,
            "updatedDt": 1606783784000
        }, {
            "id": 153,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "testfour",
            "serviceName": "testfour",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201124090639",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606179981000,
            "updatedDt": 1606181786000
        }, {
            "id": 152,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "testthird",
            "serviceName": "testthird",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201124093856",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606178332000,
            "updatedDt": 1606180298000
        }, {
            "id": 146,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "aaammm",
            "serviceName": "aaammm",
            "type": 1,
            "language": "zh",
            "status": "pause",
            "startDt": "20201119142206",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": false,
            "createdDt": 1605762562000,
            "updatedDt": 1606093890000
        }],
        "total": 70,
        "pages": 7,
        "pageNum": 1,
        "pageSize": 10
    }
}
```

### Service Contract Details - Service ID
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/service/{serviceId}.json									
- URL (Dev): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/service/{serviceId}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Service Contract Details - Service ID|HTTPS  |GET    |UTF-8|JSON    |Obtain contract details by service ID|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service contract detailed information	|serviceId	|String	|O	|Service ID|

#### Request URL
```
/openapi/v1/admin/billing/service/example.json	
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|Contract ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |organizationId	|String	|O	|Organization ID|
|	              |type	          |Int	  |O	|Service type(1:Consulation management, 2:Issue management), Default:1|
|	              |status	        |String	|O	|Contract status(Creating:create, In use:inuse, Stop use:pause, Terminate:stop)|
|	              |startDt	      |String	|O	|Start date of service use(Korean Time)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|Discount rate(%)|
|	              |freeExtension	|Int	  |O	|Free trial extension date|
|	              |active	        |Boolean	|O	|Service contract(Enabled:true, Disabled:false)|
|	              |freeTrial	    |Boolean	|O	|Free trial period(Yes:true, No:false)|
|	              |billingSettings	|List	  |O	|Contract item configuration list|
|	              |    id	              |Long	  |O	|Contract item configuration ID|
|	              |    billingId	      |Long	  |O	|Contract ID|
|	              |    billingSettingCode	|String	|O	|Item code(Refer contract item code)|
|	              |    active	            |Boolean	|O	|Enabled:true, Disabled:false|
|	              |    billingItem	      |Object	  |X	|Charged service item details|
|	              |        code	              |String	  |O	|Item Code|
|	              |        open	              |Boolean	|O	|Enabled:true, Disabled:false|

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
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000,
            "freeTrial": false,
            "billingSettings": [{
                "id": 656,
                "billingId": 214,
                "billingItemCode": "callback",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "callback",
                    "parentCode": "additional",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "",
                    "sumCounterName": "onlinecontact.callback_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "14"
                }
            }, {
                "id": 657,
                "billingId": 214,
                "billingItemCode": "chat",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "chat",
                    "parentCode": "chat",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.chat_lisence",
                    "sumCounterName": "onlinecontact.chat_count",
                    "resourceIdSuffix1": "06",
                    "resourceIdSuffix2": "07"
                }
            }, {
                "id": 658,
                "billingId": 214,
                "billingItemCode": "endusermanagement",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "endusermanagement",
                    "parentCode": "endusermanagement",
                    "baseAmount": 250000,
                    "dayAmount": 8333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.customer_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "19"
                }
            }, {
                "id": 659,
                "billingId": 214,
                "billingItemCode": "helpdoc",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "helpdoc",
                    "parentCode": "helpcenter",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.faq_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "10"
                }
            }, {
                "id": 660,
                "billingId": 214,
                "billingItemCode": "knowledge",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "knowledge",
                    "parentCode": "guide",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.knowledge_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "09"
                }
            }, {
                "id": 661,
                "billingId": 214,
                "billingItemCode": "telticket",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "telticket",
                    "parentCode": "ticket",
                    "baseAmount": 70000,
                    "dayAmount": 2333,
                    "useUserCount": true,
                    "countFree": 6000,
                    "countLevel1": 40000,
                    "countLevel1Unit": 3.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 1.5,
                    "open": true,
                    "licenceCounterName": "onlinecontact.call_licence",
                    "sumCounterName": "onlinecontact.call_seconds",
                    "resourceIdSuffix1": "02",
                    "resourceIdSuffix2": "03"
                }
            }, {
                "id": 662,
                "billingId": 214,
                "billingItemCode": "ticket",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "ticket",
                    "parentCode": "ticket",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.ticket_licence",
                    "sumCounterName": "onlinecontact.ticket_count",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "01"
                }
            }, {
                "billingItemCode": "ticketevaluation",
                "active": false,
                "billingItem": {
                    "code": "ticketevaluation",
                    "parentCode": "additional",
                    "baseAmount": 100000,
                    "dayAmount": 3333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": false,
                    "sumCounterName": "onlinecontact.ticket.evaluation_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "17"
                }
            }]
        }
    }
}
```

### Service Contract Details - Contract ID
#### Interface Description
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/{billingId}.json											
- URL (Dev): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/{billingId}.json					

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Service Contract Details - Contract ID|HTTPS  |GET    |UTF-8|JSON    |Obtain contract details by contract ID|Common authentication|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service contract detailed information	|billingId	|Long	|O	|Contract ID|

#### Request URL
```
/openapi/v1/admin/billing/214.json
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|Contract ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |organizationId	|String	|O	|Organization ID|
|	              |type	          |Int	  |O	|Service type(1:Consulation management, 2:Issue management), Default:1|
|	              |status	        |String	|O	|Contract status(Creating:create, In use:inuse, Stop use:pause, Terminate:stop)|
|	              |startDt	      |String	|O	|Start date of service use(Korean Time)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|Discount rate(%)|
|	              |freeExtension	|Int	  |O	|Free trial extension date|
|	              |active	        |Boolean	|O	|Service contract(Enabled:true, Disabled:false)|
|	              |freeTrial	    |Boolean	|O	|Free trial period(Yes:true, No:false)|
|	              |billingSettings	|List	  |O	|Contract item configuration list|
|	              |    id	              |Long	  |O	|Contract item configuration ID|
|	              |    billingId	      |Long	  |O	|Contract ID|
|	              |    billingSettingCode	|String	|O	|Item code(Refer contract item code)|
|	              |    active	            |Boolean	|O	|Enabled:true, Disabled:false|
|	              |    billingItem	      |Object	  |X	|Charged service item details|
|	              |        code	              |String	  |O	|Item Code|
|	              |        open	              |Boolean	|O	|Enabled:true, Disabled:false|

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
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000,
            "freeTrial": false,
            "billingSettings": [{
                "id": 656,
                "billingId": 214,
                "billingItemCode": "callback",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "callback",
                    "parentCode": "additional",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "",
                    "sumCounterName": "onlinecontact.callback_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "14"
                }
            }, {
                "id": 657,
                "billingId": 214,
                "billingItemCode": "chat",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "chat",
                    "parentCode": "chat",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.chat_lisence",
                    "sumCounterName": "onlinecontact.chat_count",
                    "resourceIdSuffix1": "06",
                    "resourceIdSuffix2": "07"
                }
            }, {
                "id": 658,
                "billingId": 214,
                "billingItemCode": "endusermanagement",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "endusermanagement",
                    "parentCode": "endusermanagement",
                    "baseAmount": 250000,
                    "dayAmount": 8333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.customer_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "19"
                }
            }, {
                "id": 659,
                "billingId": 214,
                "billingItemCode": "helpdoc",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "helpdoc",
                    "parentCode": "helpcenter",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.faq_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "10"
                }
            }, {
                "id": 660,
                "billingId": 214,
                "billingItemCode": "knowledge",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "knowledge",
                    "parentCode": "guide",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.knowledge_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "09"
                }
            }, {
                "id": 661,
                "billingId": 214,
                "billingItemCode": "telticket",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "telticket",
                    "parentCode": "ticket",
                    "baseAmount": 70000,
                    "dayAmount": 2333,
                    "useUserCount": true,
                    "countFree": 6000,
                    "countLevel1": 40000,
                    "countLevel1Unit": 3.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 1.5,
                    "open": true,
                    "licenceCounterName": "onlinecontact.call_licence",
                    "sumCounterName": "onlinecontact.call_seconds",
                    "resourceIdSuffix1": "02",
                    "resourceIdSuffix2": "03"
                }
            }, {
                "id": 662,
                "billingId": 214,
                "billingItemCode": "ticket",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "ticket",
                    "parentCode": "ticket",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.ticket_licence",
                    "sumCounterName": "onlinecontact.ticket_count",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "01"
                }
            }, {
                "billingItemCode": "ticketevaluation",
                "active": false,
                "billingItem": {
                    "code": "ticketevaluation",
                    "parentCode": "additional",
                    "baseAmount": 100000,
                    "dayAmount": 3333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": false,
                    "sumCounterName": "onlinecontact.ticket.evaluation_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "17"
                }
            }]
        }
    }
}
```
