## Contact Center > Online Contact > API Guide for Developers > Help Center

### Add Specified Data to Help Center
#### Interface Description
- URL:	https://{domain}.oc.toast.com /{serviceId}/hc/openapi/v1/addition.json			
- URL (Dev):	https://{domain}.alpha-oc.toast.com /{serviceId}/hc/openapi/v1/addition.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description | 
|------------|-------|--------|-----|--------|--------------|
|Add specified data to help center|HTTPS  |POST    |UTF-8|JSON    |Save additionally needed customer information to DB|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|Service ID	|serviceId	|String	|O	|{serviceId} set to URL path|
|	         |content	|String	|O	|Additional customer information|

#### Result Data
|Name |Variable |Data type |Required | Description|
|-----|-----|-----------|----|----|
|result.content	|additionId	|String	|O	|Created ID|

#### Response Body
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": ef1bd956
  }
}
```
