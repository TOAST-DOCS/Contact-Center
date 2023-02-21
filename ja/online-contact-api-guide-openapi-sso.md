## Contact Center > Online Contact > プログラマーのためのAPIガイド > 会員認証 (POST)

## 会員認証
### 概要
会員認証機能は、顧客会社が提供するサービスの会員認証を Online Contactのヘルプセンターでも適用し、会員のお問い合わせを受け付け、受け付けたお問い合わせ内訳を再確認できるようにするための機能です。
会員連動はGET方式とPOST方式の二つのタイプで提供しており、連動のためには Online Contactが提供する開発明細書に基づいてAPIを開発し、 Online Contact会員認証管理画面に登録する必要があります。

#### POST方式
- 連動させるサービスがPC、MOBILEプラットフォームでWEB基盤で提供される場合に適しています。
- サービスのログイン画面がWEB URL形式で提供されている場合に使用できます。
- 開発明細でCLIENT-SIDE、SERVICER-SIDEの細部2タイプを提供します。

#### GET方式
- WEBベースのログイン画面がないサービスに適しています。
- WEBベースではないNative APPサービスの場合に適した連動方式です。

### 全体的なプロセス(POST方式)
① ユーザーがヘルプセンターの「お問い合わせ」または「お問い合わせ履歴」ページにアクセス
② ヘルプセンターページからログインステータスURLを呼び出し、ログイン状態を確認(ここで「ログインステータスURL」は顧客社がOnline Contactから提供する明細書を参考に開発後、Online Contactの会員認証画面に登録する必要があります。)
③ ログイン状態を確認後、結果によって
③-1. 「未ログイン」の場合は、顧客社サービスの「ログインURL」を呼び出してログインを誘導（ここで「ログインURL」は、顧客企業が提供しているログイン画面のURLであり、Online Contactの会員認証画面に登録する必要があります。）
③-2. 「ログイン」状態の場合は、「遠隔ログインAPI」を呼び出して顧客情報をOCヘルプセンターに伝達
④ 「お問い合わせ」または「お問い合わせ履歴」ページへアクセスします。

### 会員認証の方法
![](http://static.toastoven.net/prod_contact_center/dev_post_(1)_2_ja.png)
① サービス管理  >  ヘルプセンター  >  会員認証 アクセス
② 会員認証「有効」ボタンをクリック
③ 「非会員問い合わせ」活性化可否を選択(有効化時にはログアウト状態でも問い合わせ受付が可能で、無効化時にはログイン状態でのみ問い合わせ受付が可能)
④ サービスの性格に合った「ログインタイプ」を選択
⑤ 各タイプによって必要なAPI開発及びURL設定、保存

## 開発明細書
### 認証トークン作成
Token生成サンプルは以下の通りです。 パラメータ順序は必ず下記と一致している必要があり、全体管理 → 契約サービス管理 → 組織情報メニューからOC組織キーを確認してください。
(※ Sample project > application.properties > oc.apikey= 項目に組織キーを保存)

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
    　if (StringUtils.isNotBlank(memberno)) {
        sb.append(memberno); // 6
        sb.append("&");
    　}
    if (StringUtils.isNotBlank(returnUrl)) {
        sb.append(returnUrl); // 7
        sb.append("&");
    }
    sb.append(time); // 8

    SecretKeySpec signingKey = new SecretKeySpec(apiKey.getBytes("UTF-8"), "HmacSHA256");
    Mac mac = Mac.getInstance(signingKey.getAlgorithm());
    mac.init(signingKey);
    byte[] rawHmac = mac.doFinal(sb.toString().getBytes("UTF-8"));
    return new String(Base64.encodeBase64(rawHmac));
}

// Sample
// Use this same input, the output is : Ah9M58CQ9RFTShjFuqziQr+0MjmJxN6+bzWxMD71moo=
public static void main(String[] args) throws Exception {
    String s = getSHA256Token("hangame", "testusercode", "testUsername", "test@email.com", "123456789",
    null, 1660095873001L, "7cf2828608274a49a3f06152b2188927");
    System.out.println(s); // Output: Ah9M58CQ9RFTShjFuqziQr+0MjmJxN6+bzWxMD71moo=
}
```

### POST遠隔ログインAPI(From client side)
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/v2/enduser/remote.json
- URL(開発): https://{domain}.alpha-oc.toast.com/v2/enduser/remote.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|POST遠隔ログインAPI(From client side)|HTTPS  |POST    |UTF-8|Redirect    |ユーザーシステムで動的にformを生成してブラウザに返し、formは自動的にAPIにform情報を伝達。 APIで配信されたform情報で認証後、成功時ログインCookie値設定。|

**ユーザーシステムでの呼び出し方法**は、下段のSample projectの次のようなclassを参照してください。

- FormLoginController.java
- Method: submitLogin  

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID|service|Varchar(50)|O|サービスID|
|ユーザーID  |usercode|Varchar(50)|O|ユーザーID，唯一のユーザーであることを表示|
|ユーザー名  |username|Varchar(50)|X|ユーザー名|
|ユーザーメールアドレス|email|Varchar(100)|X|ユーザーメールアドレス|
|電話番号        |phone|Varchar(20)|X|電話番号|
|会員番号        |memberno|Varchar(50)|X|会員番号|
|現在時間のtimestamp|time|Long|O|呼び出し時間が3分を超える場合、タイムアウトアラート出力。|
|認証Token           |token|Varchar|O|以下のパラメータ値と組織Keyにより算出されたSHA256 (パラメータ値がnull、または空の値の場合、暗号化文字列に追加する必要はない。注意: 文字列のうち、各値の順序は、以下の例に指定された順序と一致している必要がある。) SHA256Digest(service & usercode & username & email & phone & memberno & returnUrl & time)|
|リターン画面URL|returnUrl|Varchar|X|設定およびログインに成功した場合、そのアドレスに移動|

#### 結果データ
returnUrlパラメータが存在する場合、指定されたreturnUrlに移動、returnUrlがない場合は文字列:SUCCESSを返します。

### POST遠隔ログインAPI(From server side)
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/api/v2/enduser/remote.json
- URL(開発): https://{domain}.alpha-oc.toast.com/api/v2/enduser/remote.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|POST遠隔ログインAPI(From server side)|HTTPS  |POST    |UTF-8|String   |ユーザがサーバーから直接APIを呼び出し。APIログイン成功後にログインCookie値を設定。|

**ユーザーシステムでの呼び出し方法**は、下段のSample projectの次のようなclassを参照してください。

- ApiLoginController.java
- Method: submitLogin

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|サービスID|service|Varchar(50)|O|サービスID|
|ユーザーID   |usercode|Varchar(50)|O|ユーザーID，唯一のユーザーであることを表示|
|ユーザー名  |username|Varchar(50)|X|ユーザー名|
|ユーザーメールアドレス|email|Varchar(100)|X|ユーザーメールアドレス|
|電話番号        |phone|Varchar(20)|X|電話番号|
|会員番号|memberno|Varchar(50)|X|会員番号|
|現在時間のtimestamp|time|Long|O|呼び出し時間が3分を超える場合、タイムアウトアラート出力。|
|認証Token           |token|Varchar|O|以下のパラメータ値と組織Keyにより算出された SHA256 (パラメータ値がnull、または空の値の場合、暗号化文字列に追加する必要はない。注意:文字列のうち、各値の順序は、以下の例に指定された順序と一致している必要がある。) SHA256Digest(service & usercode & username & email & phone & memberno &  time)|

#### Response Data
```
{	
  "header": {	
    "resultCode": 200,	
    "resultMessage": "",	
    "isSuccessful": true	
  },	
  "result": {	
    "content": "xxxxxxaccessTokenxxxxxxx"	
  }	
}	
```

リターンされたcontent値はヘルプセンター呼び出し時、ヘルプセンターURLパラメータ - accessToken値に指定してOCに伝達。
例: https://nhn-cs.alpha-oc.toast.com/hangame/hc/?accessToken=xxxxxxaccessTokenxxxxxxx

### POSTログインURL(ユーザー)
#### インターフェース説明
- URL: 使用者提供
- URL(開発): 使用者提供

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|
|------------|--------|--------|------|--|
|POSTログインURL(ユーザー)|HTTPS|GET|UTF-8|Redirect|

サービス側のログインURLには以下の機能が必要です。

**1) ユーザー未ログイン状況**

- ログイン画面出力
- アカウント・パスワードを使ってログイン
- ログイン成功後、cookie作成とログイン状態記録。ログイン状態チェック時に使用される。
- ログイン成功後、ClientまたはServer団で顧客情報をOnline Contactに伝達(POST遠隔ログインAPI(From client side)、POST遠隔ログインAPI(From server side)参照)

**2) ユーザーログイン状態**

- ログイン成功後、ClientまたはServer団で顧客情報をOnline Contactに伝達(POST遠隔ログインAPI(From client side)、POST遠隔ログインAPI(From server side)参照)

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|---------|---------|-----------|---------|----|
|リターンURL|returnUrl|Varchar|O|ログイン成功後に移動するURL|

#### POSTログイン機能の説明
**1) ユーザー未ログイン状態**

- ① ログイン画面に移動
- ② ユーザーログイン
- ③ サービス側のサーバーからユーザーのログイン処理およびログインユーザー関連クッキー作成
- ④ POST遠隔ログインAPI呼び出し(POST遠隔ログインAPI(From client side)、POST遠隔ログインAPI(From server side)参照)

**2) ユーザーログイン状態**

- ① POST遠隔ログインAPI呼び出し(POST遠隔ログインAPI(From client side)、POST遠隔ログインAPI(From server side)参照)

#### POST遠隔ログインAPI呼び出し方法の説明
**1) POST遠隔ログイン(From client side)**

- ① ユーザー情報とAPI  Key基準でログインtoken作成
- ② ユーザー情報とtokenをブラウザーにリダイレクト
- ③ 画面でForm作成, 詳しいパラメーターはPOST遠隔ログインAPI(From client side)参考
- ④ Form提出
- ⑤ POST遠隔ログインAPIによりユーザー情報とtoken送信
- ⑥ ログインに成功した後、{returnUrl}に移動

**POST遠隔ログイン(From server side)**

- ① ユーザー情報とAPI Key基準でログインtoken作成
- ② サーバーからPOST遠隔ログインAPI(From server side)呼び出し
- ③ API呼び出しパラメータ(usercodeとtime)をreturnUrlの後に追加
  - 例示) https://nhn-cs.alpha-oc.toast.com/multilanguage/hc/ticket/list/?usercode=xxxxxx@163.com&time=1566531359635
- ④ {returnUrl}に移動

### POSTログインステータスURL(ユーザー)
#### インターフェース説明
- URL: 使用者提供
- URL(開発): 使用者提供

|インターフェース名|プロトコル|呼び出し方向|エンコード|インターフェース説明|結果形式|
|------------|--------|--------|------|--|----------|
|POSTログインステータスURL(ユーザー)|HTTPS|GET|UTF-8|ユーザーがクッキー情報を基準にログインを確認した後、JSON形式のデータをリターン。サービス側のServerでresponseにCross domain接続設定が必要|JSON|

**Cross domain接続設定**方法は下記を参照してください。
```
response.addHeader("Access-Control-Allow-Origin", request.getHeader("origin"));
response.addHeader("Access-Control-Allow-Credentials", "true");
```

**ユーザーシステムでの呼び出し方法**は、下段のSample projectの次のようなclassを参照してください。

- FormLoginController.java
- Method: loginStatus

#### リクエストパラメータ定義
- なし

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|---------|-----------|---------|----|
|javascript function|login|Boolean|O|ログイン状態. ログイン: true, 未ログイン: false|
|ユーザーID|usercode|Varchar(50)|X|ユーザーID(ユニーク値). ログイン状態がtrueの場合、ユーザーコードは必須|

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

## 適用例
### Sample Code
✔ [Sample Code ダウンロード](https://static.toastoven.net/prod_contact_center/oc_sso_sample-20220817.zip)

### iframeを利用したヘルプセンターの例
#### 1. iframeを利用してOnline Contactヘルプセンターをユーザーページに挿入
Sample  Codeファイルのうち「oc_sso_sample/src/main/resources/templates/help_frame.ftl」を参照してください。
iframeの名前は必ずid="ocPage"と指定しなければなりません。
```
<iframe src="https://${domain}/hangame/hc/?iframe=true" id="ocPage" frameborder="0" scrolling="no" style="padding-top: 60px; box-sizing: unset; height: 100px; width: 100%">
</iframe>
```  

ページにviewportを設定する際、mobile／webブラウザのどちらでもヘルプセンターを使用できます。
```
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=0">
```

#### 2. parentページ内でOnlineContactヘルプセンターの高さを確認し、iframeのheightを調整
help_frame.ftl ファイルのうち、javascript コードを参照してください。
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

#### 3. ログイン処理後に設定するクッキーは、ユーザーページから取得可能
help_frame.ftl ファイルのうち、javascript コードを参照してください。
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
