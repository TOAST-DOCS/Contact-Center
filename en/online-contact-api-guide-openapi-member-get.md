## Contact Center > Online Contact > API Guide for Developers > Member Integration (GET)

## Member Integration
### Overview
Member Intergration function is designed to apply membership confirmation process of the client to the Online Contact help center. Through this function, members of the client service could submit member inquiries, and check the history of previous inquiries. Member Integration is provided in two types: GET method and POST method. For integrating, API needs to be developed according to the development specifications Online Contact provide.

#### POST Method
- It is suitable if the service you are trying to integrate is provided based on WEB on both PC and MOBILE platforms.
- The login page of the service must be provided in WEB URL format.
- Client-side API, Servicer-side API are provided.

#### GET Method
- Suitable for services without WEB-based login page.
- Suitable for Native APP services which are not WEB-based.

### Process (GET Method)
① The user accesses to the help center within the APP.
② The APP of the customer company is called in the URL format below when help center is called.
② The client APP calls the help center through the URL format below.
- https://**{org}**.oc.toast.com/**{service}**/hc/?usercode=**{user_id}**&username=**{user_name}**&email=**{user_email}**&phone=**{user_phonenumber}**&token=**{verification_token_value}**
③ Help center calls 'Token Verification URL'. (Token verification URL must be developed according to the specifications provided below, and should be registered in member integration menu.)
④ If the verification result is successful after token verification, access the 'Inquiry' or 'Inquiry History' page. If the verification fails, the inquiry will be submitted as non-member inquiry.

### How to Integrate
![](http://static.toastoven.net/prod_contact_center/dev_post_(2)_en.png)
① Access Service Management > Help Center > Member Integration
② Enable member integration 
③ Select the 'Login Type' which matches the characteristics of the service
④ Develop and register necessary APIs according to the type

## Development Specifications
### Create Verification Token
The authentication token generation sample is as follows. The order of parameters must be consistent with the given example.
OC Organization Key is available at Global Management → Contract Service Status → Organization Information menu.

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

### Method of GET Member Verification
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
|GET Member Verification |HTTPS |GET |UTF-8 | |When the help center is accessed from the service side, the interface is called by adding customer information and token value to the URL as parameters.|

#### Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|service	|VARCHAR(50)	|O	|Service ID|
|User ID 	   |usercode	|VARCHAR(50)	|O	|User ID, indicates that the user is unique|
|Username	  |username	|VARCHAR(50)	|X	|Username|
|User Email Address 	|email	|VARCHAR(100)	|O	|User email|
|Phone Number 	        |phone	|VARCHAR(20)	|X	|Phone number |
|Membership Number	|memberno	|VARCHAR(50)	|X	|Membership number|
|Timestamp of Current Time 	|time	|Long	|O	|Time unit : milliseconds|
|Authentication Token	           |token	|VARCHAR	|O	|Calculated by the following parameters and organization key (SHA256). (If non-required parameter values are null or empty, they need not be added to the encryption string. Caution: The order of each value in the string must be consistent with the following example.) SHA256Digest(service + usercode + username + email + phone + memberno + returnUrl + time)|

##### Precautions for Creating Authentication Token
1. If korean alphabet is within the parameters when creating a token, create it directly in korean alphabet without encoding.
2. Encoding by encodeURIComponent() is required when the generated token is used as URL parameter.

#### Result Data
- Verification Success: Move to member access address
- Verification Fail: Move to non-member access address	
- When accessing 'Inquiry History' page in token verification failure state, it will be moved to 'Inquiry' page.

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
|Token Created by Service Side	|token	|VARCHAR	|O	|Calculated by the following parameters and organization key (SHA256). (If non-required parameter values are null or empty, they need not be added to the encryption string. Caution: The order of each value in the string must be consistent with the following example.) SHA256Digest(service + usercode + username + email + phone + memberno + returnUrl + time)|

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
