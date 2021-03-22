## Contact Center > Online Contact > API Guide for Developers > Member Integration (GET)

## Member Integration
### Overview
Member Intergration function is designed to apply the membership confirmation process of the service provided by the customer company to the Online Contact help center so that the inquiry of the customer can be received and checked again. Member Integration is provided in two types: GET method and POST method. For integrating, you need to develop the API according to the development specifications Online Contact provide and register it on the Member Integration screen.

#### POST Method
- It is suitable if the service you want to link to is provided based on WEB on both PC and MOBILE platforms.
- The login screen of the service must be provided in WEB URL format to be used.
- In API specifications, two types are provided in detail: CLIENT-SIDE and SERVICER-SIDE.

#### GET Method
- Suitable for services without WEB-based login screen.
- Suitable for Native APP services that are not WEB-based.

### Process (GET Method)
① The user connects to the help center within the APP.
② The APP of the customer company is called in the URL format below when help center is called.
- https://**{org}**.oc.toast.com/**{service}**/hc/?usercode=**{user_id}**&username=**{user_name}**&email=**{user_email}**&phone=**{user_phonenumber}**&token=**{verification_token_value}**
③ Help center calls the 'Token Verification URL'. (Token verification URL must be developed according to the specifications provided below by the customer company, and should be registered on member integration menu of Online Contact.)
④ After verification of the token, access towards the 'Inquiry' or 'Inquiry History' page is allowed if the status is success. If the verification fails, the inquiry will be received as non-member inquiry.

### How to Integrate
![](http://static.toastoven.net/prod_contact_center/dev_post_(2)_en.png)
① Access Service Management > Help Center > Member Integration
② Click Member integration activation > 'Enable' 
③ Select the 'Login Type' that matches the characteristics of the service
④ Develop necessary APIs and set URLs according to each type.

## Development Specifications
### Create Verification Token
Sample of creating token is as follows. The order of parameters must be consistent with the given example, and please check the SSO Login API key.

```
private String getSHA256Token(String serviceId, String usercode, String username, String email, String phone,
        String returnUrl, Long time, String apiKey) throws Exception {
    StringBuilder sb = new StringBuilder();
    // Order by follow number:
    sb.append(serviceId); // 1
    sb.append("&");
    sb.append(usercode); // 2
    sb.append("&");
    if (StringUtils.isNotBlank(username)) {
        sb.append(username); // 3
        sb.append("&");
    }
    if (StringUtils.isNotBlank(email)) {
        sb.append(email); // 4
        sb.append("&");
    }
    if (StringUtils.isNotBlank(phone)) {
        sb.append(phone); // 5
        sb.append("&");
    }
    if (StringUtils.isNotBlank(returnUrl)) {
        sb.append(returnUrl); // 6
        sb.append("&");
    }
    sb.append(time); // 7

    SecretKeySpec signingKey = new SecretKeySpec(apiKey.getBytes("UTF-8"), "HmacSHA256");
    Mac mac = Mac.getInstance(signingKey.getAlgorithm());
    mac.init(signingKey);
    byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
    return new String(Base64.encodeBase64(rawHmac));
}
```

### Method of Token Member Verification
#### Interface Description

URL
- https://{org}.oc.toast.com/{service}/hc/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{org}.oc.toast.com/{service}/hc/ticket/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{org}.oc.toast.com/{service}/hc/ticket/list/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d

URL (Dev)
- https://{domain}.alpha-oc.toast.com/{service}/hc/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{domain}.alpha-oc.toast.com/{service}/hc/ticket/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{domain}.alpha-oc.toast.com/{service}/hc/ticket/list/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|Token Member Verification |HTTPS |GET |UTF-8 | |When accessing help center from service side, the token value generated after customer information encryption is sent in parameter form. |

#### Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|service	|Varchar(50)	|O	|Service ID|
|User ID 	   |usercode	|Varchar(50)	|O	|User ID, indicates that the user is unique|
|Username	  |username	|Varchar(50)	|X	|Username|
|User Email Address 	|email	|Varchar(100)	|O	|User Email|
|Phone Number 	        |phone	|Varchar(20)	|X	|Phone number |
|Timestamp of Current Time 	|time	|Long	|O	|Time unit : milliseconds|
|Authentication Token	           |token	|Varchar	|O	|Calculated by the following parameters and organization key (SHA256). (If non-required parameter values are null or empty, you do not need to add them to the encryption string. Caution: The order of each value in the string must be consistent with the following example.) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|

#### Precautions for Creating Authentication Token
1. When creating token, if there is Hangul, create directly in Korean. No encoding required.
2. When using created token as URL parameter, encoding is required by encodeURIComponent().  

#### Result Data
- Token Verification Success: Move to the member access address
- Token Verification Fail: Move to the non-member access address	
- If the user accesses to 'Inquiry History' in token verification fail status, the screen moves to 'Inquiry' screen.

### Token Verification API (Service Side)
#### Interface Description
- URL: Supported by service side		
- URL (Dev): Supported by service side

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|Token Verfication API |HTTPS |GET |UTF-8 |JSON |Service side checks the login status with token and usercode, and sends JSON format result value|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|---------|---------|-----------|---------|----|
|User ID	|usercode	|VARCHAR(50)	|O	|User ID(Unique value)|
|Token Created by Service Side	|token	|VARCHAR	|O	|Calculated by the following parameters and organization key (SHA256). (If non-required parameter values are null or empty, you do not need to add them to the encryption string. Caution: The order of each value in the string must be consistent with the following example.) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|

#### Response Body
```
Logged in：
{
"login": "true",
"usercode":"usercodeXXX"
}


Not logged in：
{
"login": "false",
"usercode": null
}
```
