## Contact Center > Online Contact > プログラマーのためのAPIガイド ＞ オープンAPI 概要

Online Contactでは、ヘルプセンターのお知らせ、FAQ、チケット情報、チケット作成などのさまざまな相談情報をOpen APIで提供しています。

Open APIを活用することで、外部システムからOnline Contactの相談情報を簡単に確認できます。

### API認証方法

#### Open API 設定
![](http://static.toastoven.net/prod_contact_center/dev2_1_1_ja.png)

Online Contactが提供するOpen APIを使用するには、[サービス管理 → 認証]メニューで機能を有効化する必要があります。

**① OPEN APIの有効化**

- Open API機能を使用するには、**有効**ボタンをクリックしてください。
- 有効化すると、サービス Keyが自動的に生成されます。

**② サービス Key**

- APIを呼び出し、送信されるデータを暗号化するために使用される認証Keyです。
- Open APIが有効化されると自動的に生成され、**API Key変更**をクリックするとKey値を変更できます。

<!--
#### 組織ID
![](http://static.toastoven.net/prod_contact_center/dev1_1_2_ja.png)
全体管理 → 契約サービス管理 → 組織情報タブで **① NHN Cloud 組織ID**を確認することができます。
-->

#### 認証 Header

各リクエストヘッダーに下記の値を必ず設定しなければなりません。

- Authorization: Security Keyで生成された認証文字列
- X-TC-Timestamp: 現在のUTC時間値{newDate().getTime()}

「セキュリティサービス」機能を使用しているサービスの場合、[サービス管理 → セキュリティ管理 → スパム管理]メニューで顧客のIPを基準にスパムポリシーを有効化できます。
Open APIを通じてチケットを作成する際、リクエストヘッダーにOC-Client-IP値を設定すると、該当IPを基準にスパムかどうかが判断されます。

- OC-Client-IP: 顧客のIPアドレス

#### Authorization文字列の生成方法
HmacSHA256で暗号化するか、(NHN Cloud 組織ID + request URI + パラメータ値 + 現在のUTC時間値)文字列に対して暗号化してAuthorization文字列を生成することができます。

> **※ 参考事項**
>
> NHN Cloud組織IDは、**[全体管理 → 契約サービス管理 → 組織情報]** で確認できます。

##### Java例題

##### 一般リクエスト(GET)

```
// 顧客チケットリスト
String URL = "http://nhn-cs.oc.nhncloud.com/APISimple/openapi/v1/ticket/enduser/usercode/list.json?categoryId=1&language=ko";
String organizationId = "WopqM8euoYw89B7i"; // 組織ID
String securityKey = "431402c0eaaf46d889f243db9e7492e2"; // サービス Key
String uri = "/APISimple/openapi/v1/ticket/enduser/usercode/list.json"; // request uri
long timestamp = new Date().getTime();
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
sb.append("1").append("&").append("ko"); // パラメーター名のアルファベット順に従って、"&" 記号でパラメーター値を接続してください (categoryId=1&language=ko) → (1&ko)
sb.append(timestamp);// X-TC-Timestamp値と同一

SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));

Request request = new Request.Builder().url(URL).get()
.header("Content-Type", "application/json")
.header("Authorization", authorization)
.header("X-TC-Timestamp", Long.toString(timestamp))
.build();
Call call = client.newCall(request);
Response response = call.execute();
```

##### 一般リクエスト(POST)

```
// チケット作成
String URL = "http://nhn-cs.oc.nhncloud.com/APISimple/openapi/v1/ticket.json?language=ko";
String organizationId = "WopqM8euoYw89B7i"; // 組織ID
String securityKey = "431402c0eaaf46d889f243db9e7492e2"; // サービス Key
String uri = "/APISimple/openapi/v1/ticket.json"; // request uri
long timestamp = new Date().getTime();
StringBuilder sb = new StringBuilder();

String body = mapper.writeValueAsString(bodyContentObject);

sb.append(organizationId);
sb.append(uri);
sb.append("ko").append("&"); // パラメーター名のアルファベット順に従って、"&" 記号でパラメーター値を接続してください。
sb.append(body);// パラメーターの後に、bodyの文字列内容を追加してください。
sb.append(timestamp);// X-TC-Timestamp値と同一

SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));

RequestBody body = RequestBody.create(MediaType.parse("application/json; charset=utf-8"), body);

Request request = new Request.Builder().url(URL).post(body)
.header("Content-Type", "application/json")
.header("Authorization", authorization)
.header("X-TC-Timestamp", Long.toString(timestamp))
.header("OC-Client-IP", ip)
.build();

Call call = client.newCall(request);
Response response = call.execute();
```

##### ファイルアップロード

```
String URL = "http://nhn-cs.oc.nhncloud.com/APISimple/openapi/v1/ticket/attachments/upload.json";
String organizationId = "WopqM8euoYw89B7i"; // 組織ID
String securityKey = "431402c0eaaf46d889f243db9e7492e2"; // サービス Key
String uri = "/APISimple/openapi/v1/ticket/attachments/upload.json"; // request uri
long timestamp = new Date().getTime();
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
DigestUtils.appendMd5DigestAsHex(file.getInputStream(), sb);// ファイルを添付する際、ファイルのMD5はパラメーター値として認証文字列に追加してください。
sb.append(timestamp);// X-TC-Timestamp値と同一

SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));

RequestBody body = new MultipartBody.Builder().setType(MultipartBody.FORM).addFormDataPart("file", file.getOriginalFilename(),
RequestBody.create(MediaType.parse(file.getContentType()), file.getBytes())).build();
Request request = new Request.Builder().url(ticketUploadUrl).post(body)
.header("Content-Type", "application/json")
.header("Authorization", signString)
.header("X-TC-Timestamp", Long.toString(timestamp))
.build();
Call call = client.newCall(request);
Response response = call.execute();
```

##### OC側認証方法

```
// Generate authorization string sample with request
StringBuilder sb = new StringBuilder();
sb.append(org.getId()); // organization Id
sb.append(request.getRequestURI()); // request URI
// upload file
if (request instanceof MultipartHttpServletRequest) {
	MultipartHttpServletRequest mpRequest = (MultipartHttpServletRequest) request;
	MultipartFile file = mpRequest.getFile("file");
	DigestUtils.appendMd5DigestAsHex(file.getInputStream(), sb);
// other
} else {
	Map<String, String[]> params = request.getParameterMap();
	if (!params.isEmpty()) {
		// Sort parameter
		Map<String, String[]> treeMap = new TreeMap<>(params);
		for (Map.Entry<String, String[]> entry : treeMap.entrySet()) {
			sb.append(entry.getValue()[0]).append("&");
		}
		sb.deleteCharAt(sb.length() - 1); // Delete '&' character
	}	
	if (request instanceof BodyReaderHttpServletRequestWrapper) {
		BodyReaderHttpServletRequestWrapper requestWrapper = (BodyReaderHttpServletRequestWrapper) request;
		if (requestWrapper.hasBody()) {
			String body = new String(requestWrapper.getBody(), StandardCharsets.UTF_8);
			if (!params.isEmpty()) {
				// params is not empty, add '&' character
				sb.append("&");
			}
			sb.append(body);
		}
	}	
}
String time = request.getHeader("X-TC-Timestamp");
// No '&' character
sb.append(time);

return sb.toString();
```
	
### 共通リターン結果
#### リターン結果例題

```
//成功: 詳細
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "content": {
        }
    }
}

//成功: リスト
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "contents": [{
        }]
    }
}

//失敗
{
    "header": {
        "resultCode": 403,
        "resultMessage": "Access Denied",
        "isSuccessful": false
    },
    "result": null
}
```

#### リターン結果説明
|名称|変数|データタイプ|説明|
|-----|---|--------------|--------|
|Header|resultCode  |Integer    |リターン結果コード、頂上は200|
|    |resultMessage|String       |リターン エラーメッセージ|
|    |isSuccessful |Boolean    |実行結果(成功: true、失敗: false)|
|Result |contents  |JSON    |目録結果内容|
|    |content      |JSON    |詳細結果内容|

#### リターンコード情報

- 200: SUCCESS
- 400: Bad Request
- 403: Access Denied(Forbidden)
- 404: Not Data Found
- 500: Server Error
- 9007: 関連データが既に存在
- 9005: 関連データなし
- 1001, 1002: お問い合わせ回数の上限超過（「スパム管理 → スパム問い合わせのブロック」機能使用時）

#### リターンコード(失敗)詳細
##### 400

1. Authorization is blank
2. X-TC-Timestamp is not numeric
3. X-TC-Timestamp is expired(5分以内有効)
4. Multipart request but file is null
5. Authorization is incorrect

##### 403

1. securityKey is null
2. clientIp is not allowed

### API目録
#### 開発環境URL
|環境|BaseUrl|
|---|------------|
|alpha|https://{domain}.oc.alpha-nhncloud.com|
|real|https://{domain}.oc.nhncloud.com|

#### Security Key URL
|Security Key|URL|
|------------|-----|
|サービスのSecurity Key  |/{serviceId}/openapi/v1/*|
|認証なしで直接使用可能|/{serviceId}/api/v2/*|

#### API目録
|グループ   |名称    |類型    |URL|説明|
|---------|------------|---------|---|----|
|サービス    |サービス詳細                     |GET       |/{serviceId}/api/v2/service.json                                         |サービスIDでサービス情報照会|
|お知らせ |テーマリスト                   |GET       |/{serviceId}/api/v2/notice/categories.json                               |お知らせテーマリスト取得  |
|      |タグリスト                    |GET      |/{serviceId}/api/v2/notice/tags.json                                    |お知らせタグリスト取得|
|      |お知らせリスト                   |GET      |/{serviceId}/api/v2/notice/list.json                                    |ヘルプセンターお知らせリスト          |
|      |お知らせ詳細                     |GET      |/{serviceId}/api/v2/notice/detail/{id}.json                               |お知らせIDでお知らせ内容を取得|
|      |お知らせ添付ファイルを開く/ダウンロード|GET      |/{serviceId}/api/v2/notice/attachments/{id}                             |お知らせ添付ファイルを開く/ダウンロード|
|FAQ  |カテゴリーリスト                 |GET      |/{serviceId}/api/v2/helpdoc/categories.json                             |FAQカテゴリーリスト取得|
|      |FAQリスト                    |GET     |/{serviceId}/api/v2/helpdoc/list.json	                                 |ヘルプセンターFAQリスト|
|      |FAQ詳細                        |GET     |/{serviceId}/api/v2/helpdoc/detail/{id}.json                           |FAQ IDによりFAQ内容を取得|
|      |FAQ添付ファイルを開く/ダウンロード      |GET       |/{serviceId}/api/v2/helpdoc/attachments/{id}                         |FAQ添付ファイルを開く/ダウンロード|
|お問合せ |受付タイプリスト                  |GET       |/{serviceId}/api/v2/ticket/categories.json                            |サービス内の受付タイプリスト照会|
|      |受付タイプフィールドリスト              |GET       |/{serviceId}/api/v2/ticket/field/user/{categoryId}.json                |受付タイプで対応するフィールドリストを確認|
|      |チケット添付ファイルアップロード              |POST       |/{serviceId}/openapi/v1/ticket/attachments/upload.json                |サーバーにファイルアップロード|
|      |チケット作成                     |POST      |/{serviceId}/openapi/v1/ticket.json	                                   |新規チケットの作成|
|お問合せ履歴 |顧客チケットリスト              |GET       |/{serviceId}/openapi/v1/ticket/enduser/{usercode}/list.json             |検索条件により、条件に合った顧客のチケットリストを露出|
|      |チケット詳細                     |GET      |/{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/detail.json|顧客が受け付けたチケット詳細照会|
|      |チケット添付ファイルを開く/ダウンロード  |GET    |/{serviceId}/api/v2/ticket/attachments/{id}                          |チケット添付ファイルを開く/ダウンロード|
|      |顧客再問合せ                     |POST  |{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/comment.json |チケットIDを基準に再お問い合わせ|