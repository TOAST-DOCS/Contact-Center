## Contact Center > Online Contact > プログラマーのためのAPIガイド ＞ オープンAPI 概要

### API認証方法の説明
#### Security Key
##### 組織レベル
NHN Cloud CONSOLEで生成された組織ごとに唯一のSecurity Keyを有しています。 Security Keyを介してAPIに送信されるデータを暗号化処理でき、組織管理に関連するOpen APIを呼び出すことができます。(サービスの登録、修正、削除等) 
使用している組織のOnline Contactにアクセスし、全体管理→SSOログイン→API Keyで組織レベルのSecurity Keyを確認することができます。
![](http://static.toastoven.net/prod_contact_center/dev1_ja.png)

##### サービスレベル
1つの組織で複数のサービスを作成でき、作成した各サービスごとに唯一のSecurity Keyを保有しています。 Security Keyを通じてAPIに送信されるデータを暗号化処理でき、サービス管理に関連するOpen APIを呼び出すことができます。(チケット管理、FAQなど) サービス追加API(/openapi/v1/admin/service/add.json)を通じてサービス追加が可能で、サービス追加後にリターン結果値からサービスレベルのSecurity Keyを取得できます。 また、使用している組織のOnline Contactにアクセスして、Security Keyを確認しようとするサービスを選択し、サービス管理→認証→OPEN API→API KeyからもサービスレベルのSecurity Keyの取得が可能です。
![](http://static.toastoven.net/prod_contact_center/dev2_ja.png)

##### Response Body
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

#### 認証Header
各リクエストヘッダーに下記の値を必ず設定しなければなりません。
- Authorization：Security Keyで生成された認証文字列
- X-TC-Timestamp：現在のUTC時間値{newDate().getTime()}
- OUCODE：ユーザcode（必須ではない. 設定しない場合、基本値はOwner）

#### Authorization文字列の生成方法
HmacSHA256で暗号化するか、(組織ID + request URI + パラメータ値 + 現在のUTC時間値)　文字列に対して暗号化してAuthorization文字列を生成することができます。

##### Java 예시
```
String URL = "http://nhn-cs.alpha-oc.toast.com/openapi/v1/admin/service/add.json";
String organizationId = "WopqM8euoYw89B7i"; // 조직ID
String securityKey = "0983e74b682b416684d2da59347aec82"; //조직 API Key
String uri = "/openapi/v1/admin/service/add.json"; // request uri
StringBuilder sb = new StringBuilder();
sb.append(organizationId);
sb.append(uri);
sb.append("GameBaseService").append("&").append("GameBaseServiceAPI").append("&").append("ko").append("&").append("Asia/Seoul");// 파라미터 값은 이름 오름차 순, 파라미터 사이는 &로 분리
Date date = new Date();
sb.append(date.getTime());
SecretKeySpec signingKey = new SecretKeySpec(securityKey.getBytes("UTF-8"), "HmacSHA256");
Mac mac = Mac.getInstance(signingKey.getAlgorithm());
mac.init(signingKey);
byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
String authorization = new String(Base64.encodeBase64(rawHmac));
```

- request bodyがある場合、パラメータの後ろにbody文字列を追加
- ファイル添付時、ファイルのMD5はパラメータ値で認証文字列に追加
- Security Key
	- /openapi/v1/admin/* 形態のAPIを呼び出す際に組織レベルSecurity Keyを使用
	- {serviceId}/openapi/v1/* 形態のAPI呼び出し時、サービスレベルSecurity Key使用
	
### 共通リターン結果
|名称	|変数|	データタイプ	|必須|	説明|
|-----|---|--------------|----|------|
|Header	|resultCode	|VARCHAR(2)	|O	|リターン結果コード、頂上は２００|
|	|resultMessage|	VARCHAR(50)|	O|	リターン エラーメッセージ|
|	|isSuccessful|	Boolean|	O|	実行結果(成功:true、失敗:false)|
|Result|	contents|	JSON|	X|	目録結果内容|
|	|content|	JSON|	X|	詳細結果内容|

#### リターンコード情報
- 200 :SUCCESS	
- 400 :Bad Request	
- 403 : Forbidden	
- 404 : Not Data Found	
- 500 : Server Error	
- 9007 : 関連データが既に存在	
- 9005 : 関連データなし

### API関連目録
#### 開発環境URL
|環境|	BaseUrl|	
|---|------------|
|alpha|	https://{domain}.alpha-oc.toast.com|	
|real|	https://{domain}.oc.toast.com	|

#### Security Key URL
|Security Key|	URL|	
|------------|-----|
|組織レベル|	/openapi/v1/admin/\*|	
|サービスレベル|	/{serviceId}/openapi/v1/\*|	

#### API 目録
|レベル	|グループ	|名称	|説明|
|---------|--------|---------|---|
|組織レベル	|[サービス](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-service/)	     |サービス追加	           |新規サービス追加|
|	   |	           |サービス詳細 	         |サービスIDを通じてサービス情報を照会 |
|  	   |	           |サービス修正 	         |サービスIDを通じてサービス情報を修正 |
|	   |               |サービス無効化 	        |サービスIDを通じてサービスを無効化 |
|	   |	           |サービス活性化	         |サービスIDを通じてサービス活性化 |
|	   |	           |サービスの削除 	          |サービスIDを使って無効になったサービスの削除 |
|	   |	           |サービスAPI Key再発行 	 |サービスIDにより当該サービスに生成されたAPI Key再発行|
|	   |	           |サービス一覧 	          |組織内に生成されたすべてのサービス照会 |
|          |               |サービス契約登録            |サービス契約登録 |
|          |               |サービス契約変更            |契約変更 (1日に1回のみ) |
|          |               |サービス契約一覧            |組織内サービス契約一覧 |
|          |               |サービス契約詳細 - サービスID |サービスIDで契約詳細情報取得 |
|          |               |サービス契約詳細 - 契約ID     |契約IDでサービス契約詳細情報を取得 |
|サービスレベル|[メール設定](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-email/)     |代表アカウント作成               |サービス代表アカウント作成。(作成後は修正不可)形式: \*\*@oc.toast.com|       	
|          |               |メール情報照会            |該当サービスすべてのEメール情報照会|
|          |               |外部アカウント有効性チェック 	      |外部アカウント有効性チェック |
|          |               |外部アカウント登録              |外部アカウント登録(有効性チェック後登録可能) |
|          |               |外部アカウント修正               |外部アカウント修正(有効性チェック後修正可能) |
|          |               |外部アカウント有効化             |無効化状態外部アカウントを有効化 |
|          |               |外部アカウントの無効化           |有効化状態外部アカウントを無効化 |
|          |               |外部アカウント削除               |無効化状態外部アカウント削除 |
|          |               |メール情報保存            |メール情報保存 |
|           |[受付タイプ管理](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-category/)  |受付タイプ追加	         |新規受付タイプ追加|
|	    |              |受付タイプの詳細 	          |受付タイプIDで受付タイプの照会 |
|	    |	           |受付タイプ修正 	          |受付タイプIDから受付タイプ修正 |
|	    |	           |受付タイプの削除 	          |受付タイプIDから受付タイプの削除 |
|  	    |	           |受付タイプ一覧	         |サービス内受付タイプ一覧 |
|           |[チケット管理](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-ticket/)	|チケット生成	                |新規チケット生成|
|	    |	           |チケット処理 	           |チケットIDでチケット処理 |
|	    |	           |チケット詳細 	           |チケットIDを通じてチケット照会|
|	    |	           |チケットリスト	          |検索条件を通じて条件に合ったチケットリストを露出 |
|	    |	           |ユーザーチケットリスト          |検索条件を通じて条件に合うお客様のチケットリスト露出 |
|	    |	           |チケット添付ファイル添付	        |サーバーにファイルアップロード|
|	    |	           |チケット添付ファイルを開く/ダウンロード      |サーバーにアップロードされたファイル開く/ダウンロード|
|	    |	           |チケット添付ファイルの削除         |サーバーにアップロードされたファイルの削除 |
|	    |[お知らせ](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-notice/)	|お知らせ目録照会 	      |お知らせ事項の内容照会、検索条件によりお知らせリストをリターン|
|	    |	           |お知らせ詳細照会 	          |お知らせIDからお知らせ内容を取得|
|	    |	           |お知らせ詳細照会(複数件) 	|複数のお知らせIDから内容を取得 |
|	    |	           |お知らせ登録 	          |新規お知らせ登録 |
|	    |	           |お知らせ修正 	          |IDでお知らせ修正 |
|           |		   |お知らせ削除 	          |IDでお知らせ削除 |
|	    |	           |お知らせテンプレートリスト	           | テンプレート内容、テンプレートリスト照会|
|	    |	           |お知らせテンプレート詳細照会 	           |テンプレートIDからテンプレート内容を取得 |
|	    |	           |お知らせテンプレート登録 	           |新規テンプレート登録 |
|	    |	           |お知らせテンプレート修正           |IDでテンプレート修正 |
|	    |	           |お知らせテンプレート削除 	           |IDによりテンプレート削除 |
|	    |	           |お知らせ添付ファイル添付        |サーバーにファイルアップロード |
|	    |	           |お知らせ添付ファイルの削除        |サーバーにアップロードしたファイルの削除 |
|	    |	           |お知らせタグリスト照会 	           |お知らせタグリスト取得 |
|	    |	           |お知らせタグ詳細照会 	            |タグIDからお知らせタグ内容取得 |
|	    |	           |お知らせタグ登録             |新規タグ登録 |
|	    |	           |お知らせタグ修正 	            |タグIDでお知らせタグ修正 |
|	    |	           |お知らせタグの削除 	            |タグIDからお知らせタグの削除 |
|	    |	           |お知らせテーマ一覧 	           |お知らせテーマ一覧|
|	    |	           |お知らせ テーマ詳細照会 	           |テーマIDからお知らせテーマ内容取得|
|	    |	           |お知らせテーマ登録            |新規テーマ登録 |
|	    |	           |お知らせテーマ修正 	           |テーマIDでテーマ名を修正 |
|	    |	           |お知らせテーマ削除 	           |テーマIDを通じてお知らせテーマ削除 |
|	    |[オペレーター管理](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-agent/)	|オペレーターリスト照会	      |オペレーターリスト 取得|
|           |		    |オペレーター詳細照会  	           |オペレーターIDからオペレーター情報を取得 |
|	    |	            |オペレーター追加 	           |指定したサービスにオペレーター追加、権限付与 |
|           |		    |オペレーター権限の変更            |サービス内のオペレーター権限の変更 |
|	    |	            |オペレーター削除 	           |指定したサービスからオペレーター削除 |
|	    |[ヘルプセンター](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-helpcenter/)	 |ヘルプセンター指定データ追加    |追加必要な顧客情報をDBに保存|
|	    |[FAQ](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-faq/)	     |FAQ リスト照会 	              |照会条件基準でFAQリストをリターン |
|           |		     |FAQ詳細照会 	              |FAQ IDからFAQ内容取得 |
|           |		     |FAQ登録 	              |新規FAQ登録 |
|           |		     |FAQ修正 	              |FAQ ID基準で内容修正 |
|	    |	             |FAQカテゴリー別固定設定 	             |FAQ文書が属するカテゴリー上段に固定されるように設定 |
|	    |	             |FAQメイン画面固定設定 	   |FAQ文書がメイン画面カテゴリー上段に固定されるように設定|
|	    |	             |FAQ完了処理 	             |FAQの状態を完了状態に変更（status=C）|
|	    |	             |FAQ 削除 	               |FAQ ID 基準でFAQ 削除 |
|	    |	             |FAQカテゴリーリスト	           |FAQカテゴリーリスト|
|	    |	             |FAQカテゴリー詳細照会 	           |カテゴリーIDからFAQカテゴリー内容取得 |
|	    |	             |FAQカテゴリー追加 	           |新規FAQカテゴリー追加 |
|	    |	             |FAQカテゴリー修正 	           |ID基準でカテゴリー名修正 |
|	    |	             |FAQカテゴリー削除 	           |カテゴリーIDでFAQカテゴリー削除 |
|	    |	             |FAQ添付ファイル添付 	   |サーバーにファイルアップロード |
|	    |	             |FAQ添付ファイルの削除 	   |サーバーにアップロードしたファイルの削除 |
|           |[シングルサインオン](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-sso/)             |シングルサインオン遠隔ログインAPI (Client Side)|ーザーシステムで動的にformを生成してブラウザに返却、formは自動的にAPIにform情報を伝達、認証後に成功した場合ログインクッキー値設定|
|           |                |シングルサインオン遠隔ログインAPI (Server Side)|ユーザーがサーバーから直接APIを呼び出し、APIログイン成功後ログインクッキー値設定|
|           |                |シングルサインオンログイン状態API              |ユーザーがクッキー情報を基準にログインしているかどうかを確認後、JSON形式のデータをリターン |
|           |[顧客情報連動](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-customer-data/)    |顧客情報連動                   |電話問い合わせ引込時、媒体番号から顧客データを照会して画面に表示|

