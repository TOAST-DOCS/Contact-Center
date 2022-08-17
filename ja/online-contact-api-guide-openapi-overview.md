## Contact Center > Online Contact > プログラマーのためのAPIガイド ＞ オープンAPI 概要

### API認証方法
#### Open API 設定
![](http://static.toastoven.net/prod_contact_center/dev2_1_1_ja.png)
一つの組織で複数のサービスを生成することができ、生成した各サービス別に唯一のSecurityKeyである**サービス Key**を保有しています。 サービスKeyを通じてAPIに転送されるデータを暗号化処理することができ、サービス管理に関するOpenAPIを呼び出すことができます。 （チケット管理、FAQなど）

サービス管理 → 認証 → OPEN APIタブでOpen APIを **① 有効化/無効化**することができ、**② サービス Key**を確認/変更することができます。

#### 組織ID
![](http://static.toastoven.net/prod_contact_center/dev1_1_2_ja.png)
全体管理 → 契約サービス管理 → 組織情報タブで **① NHN Cloud 組織ID**を確認することができます。

#### 認証 Header
各リクエストヘッダーに下記の値を必ず設定しなければなりません。

- Authorization: Security Keyで生成された認証文字列
- X-TC-Timestamp: 現在のUTC時間値{newDate().getTime()}
- OUCODE: ユーザcode（必須ではない. 設定しない場合、基本値はOwner）

#### Authorization文字列の生成方法
HmacSHA256で暗号化するか、(NHN Cloud 組織ID + request URI + パラメータ値 + 現在のUTC時間値)　文字列に対して暗号化してAuthorization文字列を生成することができます。

##### Java例題
##### 一般リクエスト(GET,POST)
```
String URL = "http://nhn-cs.alpha-oc.toast.com/APISimple/openapi/v1/ticket/enduser/usercode/list.json?categoryId=1&language=ko";
String organizationId = "WopqM8euoYw89B7i"; // NHN Cloud 組織ID
String securityKey = "431402c0eaaf46d889f243db9e7492e2"; // サービス Key
String uri = "/APISimple/openapi/v1/ticket/enduser/usercode/list.json"; // request uri
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
sb.append("1").append("&").append("ko"); // 媒介変数の順番に従って(categoryId=1&language=ko)媒介変数を使用(1&ko)
sb.append(body);// request bodyがある場合、パラメータの後ろにbody文字列を追加
sb.append(new Date().getTime());// X-TC-Timestampと同一
SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));
```

##### ファイルアップロード
```
String URL = "http://nhn-cs.alpha-oc.toast.com/APISimple/openapi/v1/ticket/attachments/upload.json";
String organizationId = "WopqM8euoYw89B7i"; // NHN Cloud 組織ID
String securityKey = "431402c0eaaf46d889f243db9e7492e2"; // サービス Key
String uri = "/APISimple/openapi/v1/ticket/attachments/upload.json"; // request uri
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
DigestUtils.appendMd5DigestAsHex(file.getInputStream(), sb);// ファイル添付時、ファイルのMD5はパラメータ値として認証文字列に追加
sb.append(new Date().getTime());// X-TC-Timestampと同一
SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));
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
|名称	|変数|	データタイプ	|説明|
|-----|---|--------------|--------|
|Header	|resultCode	  |Integer	    |リターン結果コード、頂上は２００|
|	    |resultMessage|String       |リターン エラーメッセージ|
|	    |isSuccessful |	Boolean	    |実行結果(成功:true、失敗:false)|
|Result |	contents  |	JSON	    |目録結果内容|
|	    |content      |	JSON	    |詳細結果内容|

#### リターンコード情報
- 200: SUCCESS	
- 400: Bad Request	
- 403: Access Denied(Forbidden)
- 404: Not Data Found	
- 500: Server Error	
- 9007: 関連データが既に存在	
- 9005: 関連データなし

#### リターンコード(失敗)詳細
##### 400
1. Authorization is blank
2. X-TC-Timestamp is not numeric
3. X-TC-Timestamp is expired（5分以内有効）
4. Multipart request but file is null
5. Authorization is incorrect
6. Invalid paramter

##### 403
1. securityKey is null
2. clientIp is not allowed

### API目録
#### 開発環境URL
|環境|	BaseUrl|	
|---|------------|
|alpha|	https://{domain}.alpha-oc.toast.com|	
|real|	https://{domain}.oc.toast.com	|

#### Security Key URL
|Security Key|	URL|	
|------------|-----|
|サービスのSecurity Key  |/{serviceId}/openapi/v1/*|	
|認証なしで直接使用可能|/{serviceId}/api/v2/*|	

#### API目録
|グループ	   |名称	    |類型    |URL|説明|
|---------|------------|---------|---|----|
|サービス    |サービス詳細	                     |GET	       |/{serviceId}/api/v2/service.json                                         |サービスIDでサービス情報照会|
|お知らせ |テーマリスト                   |GET	       |/{serviceId}/api/v2/notice/categories.json                               |お知らせテーマリスト取得  |
|	      |タグリスト	                    |GET	      |/{serviceId}/api/v2/notice/tags.json	                                    |お知らせタグリスト取得|
|	      |お知らせリスト                   |GET	      |/{serviceId}/api/v2/notice/list.json   	                                 |ヘルプセンターお知らせリスト          |
|	      |お知らせ詳細                     |GET	      |/{serviceId}/api/v2/notice/detail/{id}.json                               |お知らせIDでお知らせ内容を取得|
|	      |お知らせ添付ファイルを開く/ダウンロード|GET	      |/{serviceId}/api/v2/notice/attachments/{id}	                             |お知らせ添付ファイルを開く/ダウンロード|
|FAQ	  |カテゴリーリスト	                 |GET	      |/{serviceId}/api/v2/helpdoc/categories.json	                             |FAQカテゴリーリスト取得|
|	      |FAQリスト	                    |GET	     |/{serviceId}/api/v2/helpdoc/list.json	                                    |ヘルプセンターFAQリスト|
|	      |FAQ詳細	                        |GET	     |/{serviceId}/api/v2/helpdoc/detail/{id}.json	                           |FAQ IDによりFAQ内容を取得|
|	      |FAQ添付ファイルを開く/ダウンロード      |GET	       |/{serviceId}/api/v2/helpdoc/attachments/{id}	                         |FAQ添付ファイルを開く/ダウンロード|
|お問合せ |受付タイプリスト	                  |GET	       |/{serviceId}/api/v2/ticket/categories.json	                            |サービス内の受付タイプリスト照会|
|	      |受付タイプフィールドリスト	              |GET	       |/{serviceId}/api/v2/ticket/field/user/{categoryId}.json	                |受付タイプで対応するフィールドリストを確認|
|	      |チケット添付ファイルアップロード              |POST	       |/{serviceId}/openapi/v1/ticket/attachments/upload.json	                |サーバーにファイルアップロード|
|	      |チケット作成	                     |POST	      |/{serviceId}/openapi/v1/ticket.json	                                   |新規チケットの作成|
|お問合せ履歴 |顧客チケットリスト	              |GET	       |/{serviceId}/openapi/v1/ticket/enduser/{usercode}/list.json	             |検索条件により、条件に合った顧客のチケットリストを露出|
|	      |チケット詳細	                     |GET	      |/{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/detail.json	|顧客が受け付けたチケット詳細照会|
|	      |チケット添付ファイルを開く/ダウンロード	  |GET	    |/{serviceId}/api/v2/ticket/attachments/{id}	                          |チケット添付ファイルを開く/ダウンロード|
|	      |顧客再問合せ	                     |POST	  |{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/comment.json	 |チケットIDを基準に再お問い合わせ| 