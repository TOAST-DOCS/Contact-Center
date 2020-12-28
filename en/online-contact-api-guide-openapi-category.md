## Contact Center > Online Contact > API Guide for Developers > Category Management

### Add Submission Category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/add.json			
- URL(Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/add.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Add submission category |HTTPS  |POST    |UTF-8|JSON    |Add new submission category|Common authentication  |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Submission Category Information	|request body	|String	|O	|Submission category information（JSON)|
|	             |name	|String	|O	|Submission category name（Unique value:yes; Length:min = 0, max = 50; Format:^(\_\|-\|\[^\\pP])+$）|
|	             |orderNo	|Int	|X	|Submission category order（Default value:0）|

#### Request Body
```
{
    "name":"bug",
    "orderNo":1
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|---|
|result.content	|categoryId	|Int	|O	|Submission category ID|
|             	|serviceId	|String	|O	|Service ID|
|	              |parent	|Int	|X	|Upper submission category ID（Fixed value:0）|
|	              |name	|String	|O	|Submission category name|
|	              |level	|Int	|X	|Depth（Fixed value:1）|
|	              |path	|String	|X	|Depth path（Fixed value:"\\\\"）|
|	              |orderNo	|Int	|X	|Submission category order（Default value:0）|
|	              |createdDt	|Long	|X	|Submission category created time|
|	              |updatedDt	|Long	|X	|Submission category updated time|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"bug",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1586830915532,
            "updatedDt":1586830915532
        }
    }
}
```

### Submission Category Detail
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json			
- URL (Dev):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Submission category detail  |HTTPS  |GET    |UTF-8|JSON    |Query submission category by category ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Submission Category ID	|categoryid	|Int	|O	|Submission category ID，{categoryid} which is set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|result.content	|categoryId	|Int	|O	|Submission category ID|
|             	|serviceId	|String	|O	|Service ID|
|	              |parent	|Int	|X	|Upper submission category ID（Fixed value:0）|
|	              |name	|String	|O	|Submission category name|
|	              |level	|Int	|X	|Depth（Fixed value:1）|
|	              |path	|String	|X	|Depth path（Fixed value:"\\\\"）|
|	              |orderNo	|Int	|X	|Submission category order（Default value:0）|
|	              |createdDt	|Long	|X	|Submission category created time|
|	              |updatedDt	|Long	|X	|Submission category updated time|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"bug",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1586830915532,
            "updatedDt":1586830915532
        }
    }
}

```

### Edit Submission Category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Edit submission category  |HTTPS  |PUT    |UTF-8|JSON    |Edit submission category through category ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Submission Category ID	|categoryid	|Int	|O	|Submission category ID，{categoryid} which is set in URL path|
|Submission Category Information	|request body	|String	|O	|Submission category information（JSON）|
|	             |name	|String	|O	|Category name（Unique value:yes; Length:min = 0, max = 50; Format:^(\_\|-\|[^\\pP])+$|
|              |orderNo	|Int	|X	|Category order（Default value:0）|

#### Request Body
```
{
    "name":"bug",
    "orderNo":1
}
```

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|result.content	|categoryId	|Int	|O	|Category ID|
|	              |serviceId	|String	|O	|Service ID|
|	              |name	|String	|O	|Category name|
|	              |orderNo	|Int	|X	|Category order（Default value:0）|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "name":"bug",
            "orderNo":1
        }
    }
}
```

### Delete Submission Category
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Delete submission category  |HTTPS  |DELETE    |UTF-8|JSON    |Delete submission category by category ID|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|
|Submission Category ID	|categoryid	|Int	|O	|Submission category ID，{categoryid} which is set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|result|		|	|X	|null:Delete success|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":null
}
```

### Submission category list
#### Interface Description
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/list.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/list.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | Access restricted|
|------------|-------|--------|-----|--------|--------------|------------|
|Submission category list |HTTPS  |GET    |UTF-8|JSON    |Query submission category list in service|Common authentication   |

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|Service ID	|serviceId	|String	|O	|Service ID，{serviceId} which is set in URL path|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|----------|-----|----|
|result.contents	|categoryId	|Int	|O	|Submission category ID|
|             	|serviceId	|String	|O	|Service ID|
|	              |parent	|Int	|X	|Upper submission category ID（Fixed value:0）|
|	              |name	|String	|O	|Submission category name|
|	              |level	|Int	|X	|Depth（Fixed value:1）|
|	              |path	|String	|X	|Depth path（Fixed value:"\\\\"）|
|	              |orderNo	|Int	|X	|Submission category order（Default value:0）|
|	              |createdDt	|Long	|X	|Submission category created time|
|	              |updatedDt	|Long	|X	|Submission category updated time|

- The order of list is order by orderNo, name asc

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
                "categoryId":1571,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"help",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1586835618000,
                "updatedDt":1586835618000
            },
            {
                "categoryId":1570,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"chat",
                "level":1,
                "path":"\\",
                "orderNo":1,
                "createdDt":1586835599000,
                "updatedDt":1586835599000
            },
            {
                "categoryId":1567,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"bug",
                "level":1,
                "path":"\\",
                "orderNo":3,
                "createdDt":1586830916000,
                "updatedDt":1586841262000
            }
        ]
    }
}
```
