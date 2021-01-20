## Contact Center > Online Contact > API Guide for Developers > Member Integration (POST)

## Overview
### SSO Login Overview
SSO login is a feature that links the user system with the consultation system, and remote authentication is done with API Key. 
The API Key is the only optional string that can be generated and is a secure authentication method that allows remote login to connect to the consultation system.

### Process of SSO Login
1. Customer accesses consultation system for inquiries, chat consultation, etc.
2. When a customer attempts to login from the consulting system, they are directed to the SSO login screen which is set up in the consulting organization.
3. Login from the provided system login screen, not from Online Contact login screen.
4. Create token through user information, API key after login has succeeded.
5. Transfer user information, token to consultation system.
6. Authenticate token in the consultation system and proceed login after success.
7. Go to the pre-login screen.（returnUrl）

### Set SSO Login
#### Register SSO Login
![](http://static.toastoven.net/prod_contact_center/dev3_en.png)
After connecting to Online Contact, register SSO login first from the Global Management → SSO Login menu. Please enter the SSO login URL and login status URL.
Please copy API key after registering SSO Login. It is used as authentication token when calling remote login API.

#### Enable and Select SSO Login
![](http://static.toastoven.net/prod_contact_center/dev4_en.png) 
You can enable or disable SSO Login in Service Management → Authentication → SSO Login menu, and when enabled, you can select SSO login you want to assign to the service you selected.

#### Create Authentication Token
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

## SSO Login API
### SSO Remote Login API (Client Side)
#### Interface Description
- URL: https://{domain}.oc.toast.com/v2/enduser/remote.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/v2/enduser/remote.json		

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|SSO Remote Login API (Client Side)|HTTPS  |POST    |UTF-8|Redirect    |The user system dynamically generates a form and returns it to the browser, which automatically passes form information to the API. Set login cookie value  with form information passed from API after authentication is successful.|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|------------|----|----|
|Service ID	|service	|Varchar(50)	|O	|Service ID|
|User ID 	   |usercode	|Varchar(50)	|O	|User ID, indicates that the user is unique|
|Username	  |username	|Varchar(50)	|X	|Username|
|User Email Address 	|email	|Varchar(100)	|X	|User Email|
|Phone Number 	        |phone	|Varchar(20)	|X	|Phone number |
|Timestamp of Current Time 	|time	|Long	|O	|Timeout alert is displayed when call time exceeded by 3 minutes|
|Authentication Token	           |token	|Varchar	|O	|SHA256 calculated by following parameter values and SSO API key (If non-required parameter values are null or empty, you do not need to add them to the encryption string. Caution: The order of each value in the string must be consistent with the following example.) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|
|Return Screen URL	|returnUrl	|Varchar	|X	|Go to the address upon successful configuration and login|

#### Result Data
If returnUrl parameter exists, move to the specified returnUrl, return SUCCESS string if parameter doesn't exist.

### SSO Remote Login API (Server Side)
#### Interface Description
- URL: https://{domain}.oc.toast.com/api/v2/enduser/remote.json			
- URL (Dev): https://{domain}.alpha-oc.toast.com/api/v2/enduser/remote.json			

|Interface name | Protocol | Call direction | Encoding | Result format | Interface description |
|------------|-------|--------|-----|--------|--------------|
|SSO Remote Login API (Server Side)|HTTPS  |POST    |UTF-8|String   |User directly calls API from server. Set login cookie value after API Login has succeeded.|
  
#### Request Parameters
|Name |Variable |Data type |Required | Description|
|-----|----|-----------|-----|----|
|Service ID	|service	|Varchar(50)	|O	|Service ID|
|User ID	|usercode	|Varchar(50)	|O	|User ID, indicates that the user is unique|
|User Name 	|username	|Varchar(50)	|X	|User name|
|User Email Address	|email	|Varchar(100)	|X	|User email|
|Phone Number	|phone	|Varchar(20)	|X	|Phone number|
|Timestamp of Current Time	|time	|Long	|O	|Timeout alert is displayed when call time exceeded by 3 minutes.|
|Authentication Token 	|token	|Varchar	|O	|SHA256 calculated by following parameter values and SSO API key (If non-required parameter values are null or empty, you do not need to add them to the encryption string. Caution: The order of each value in the string must be consistent with the following example.) SHA256Digest(service + usercode + username + email + phone + time)|

#### Result Data
SUCCESS
 
### SSO Login URL (User)
#### Interface Description
|Interface name|Protocol|Call direction|Encoding|URL|URL(Dev)|Result format|
|------------|--------|--------|------|--|----------|--------|
|SSO Login URL|HTTPS|GET|UTF-8|Provided by user|Provided by user|Redirect|

#### Request Parameters
|Name |Variable |Data type |Required | Description|
|---------|---------|-----------|---------|----|
|Return URL	|returnUrl	|Varchar	|O	|URL to be moved after successfully logged-in|

#### SSO Login Function Description
**User Not Logged In**
- ① Move to login screen
- ② User logs in
- ③ Service-side server processes user to be logged in, and create logged-in user-related cookies
- ④ Call SSO remote login API

**User Logged In**
- ① Call SSO remote login API

#### How to Call SSO Remote Login API
**SSO Remote Login (Client Side)**
- ① Create login token based on user information, API key
- ② Redirect user information, token to browser
- ③ Input Form in screen, Refer SSO Remote Login API (Client Side) about parameter details.
- ④ Submit form
- ⑤ Send user information, token through SSO Remote Login API
- ⑥ Move to {returnUrl} after log-in succeeded

**SSO Remote Login (Server Side)**
- ① Create login token based on user information, API Key
- ② Call “SSO Remote Login API (Server Side)” in server
- ③ Append API call parameters (usercode, time) in the end of returnUrl
  - Example) https://nhn-cs.alpha-oc.toast.com/multilanguage/hc/ticket/list/?usercode=xxxxxx@163.com&time=1566531359635
- ④ Move to {returnUrl}
 
### SSO Login Status API (User)
#### Interface Description
|Interface name|Protocol|Call direction|Encoding|URL|URL(Dev)|Interface Description|Result format|
|------------|--------|--------|------|--|----------|--------|--------------|
|SSO Login status API |HTTPS|GET|UTF-8|Provided by user|Provided by user|User returns JSON data after confirming login based on cookie information|JSON|

#### Request Parameters
- None

#### Result Data
|Name |Variable |Data type |Required | Description|
|---------|---------|-----------|---------|----|
|Javascript Function	|login	|Boolean	|O	|Login status. Logged-in：true, Logged-out：false|
|User Code	|usercode	|Varchar(50)	|X	|User ID (Unique). Required if login status is true|

#### Response Body
```
{
"login": "true",
"usercode":"usercodeXXX"
}

{
"login": "false",
"usercode": null
}
```

## Examples of applications
### Sample Code
✔ [Download Sample Code](http://static.toastoven.net/prod_contact_center/oc_sso_sample.zip)

### Help center example by using iframe
#### 1. Insert Online Contact Help center into user page by ifrmae
Please refer'oc_sso_sample/src/main/resources/templates/help_frame.ftl' in attached Sample Code file.
The name of iframe must be specified into id = "ocPage".
```
<iframe src="https://${domain}/hangame/hc/?iframe=true" id="ocPage" frameborder="0" scrolling="no" style="padding-top: 60px; box-sizing: unset; height: 100px; width: 100%">
</iframe>
```  
 
If you set viewport into page, you could use help center in both mobile/web browsers.
```
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=0">
```

#### 2. Check height of Online Contact Help center page, and adjust height of iframe
Please refer javascript code in help_frame.ftl.
```
// Listener for OC content height change
window.addEventListener('message',function(event){
    // Set iframe height
    if(event.data > 0) {
    updateHeight(event.data);
    }
});

var updateHeight = function(wrapHeight) {
var iframe = window.document.getElementById('ocPage');
if(iframe != null) {
iframe.style.height = '0px'; 
var setHeight = (document.body.clientHeight > document.body.scrollHeight) ? document.body.clientHeight : document.body.scrollHeight;
var margin = 70;
setHeight = setHeight > wrapHeight ? setHeight : wrapHeight;
iframe.style.height = setHeight + margin + "px";
}
};
```

#### 3. Cookies that need to be set after login process could be acquired on user page
Please refer javascript code in help_frame.ftl.
```
// get cookie
function getCookie(name) {
    var arr,reg=new RegExp("(^| )"+name+"=([^;]*)(;|$)");
    if(arr=document.cookie.match(reg))
        return unescape(arr[2]);
    else
        return null;
}
$.when( $.ready ).then(function() {
    var ssotoken = getCookie("sso_test_login");
    var usercode = getCookie("usercode");
    if(ssotoken != null && usercode != null) {
        var signout = $("#signout");
        $("#signout").html("Welcome " + usercode + "! <a href='/logout.nhn'>Sign out</a>");
        $("#signout").show();
        $("#signin").hide();
    }
});
```
