## Contact Center > Online Contact > プログラマーのためのAPIガイド > シングルサインオン

## 概要
### シングルサインオン概要
シングルサインオンを使ったログインはユーザーシステムと相談システムを連動する機能で、遠隔認証はAPI  Keyを通じて行われます。API  Keyは、任意に生成される唯一の文字列で、遠隔ログインを通じて相談システムに接続できる安全な認証方式です。

### シングルサインオンプロセス
1. お客様がお問い合わせ、チャット相談などのため、相談システムに接続
2. お客様が相談システムでログインを試みる際、相談組織で設定しておいたSSOログイン画面に移動
3. Online  Contactのログイン画面ではなく、提供中のシステムのログイン画面からログイン
4. ログインに成功した後、ユーザー情報とAPIキーでトークンを作成
5. ユーザー情報とトークンを相談システムに配信
6. 相談システムでトークンに対して認証、成功後に顧客ログインを実施
7. ログイン前の画面に移動（returnUrl）

### シングルサインオン設定
#### シングルサインオン登録
![](http://static.toastoven.net/prod_contact_center/dev3_ja.png)
Online  Contactに接続した後、全体管理→SSOログインメニューでSSOログインを先に登録します。 SSOログインURL、ログイン状態URLを入力してください。SSOログインを登録した後にAPI  Keyをコピーしてください。 リモートログイン  API  を呼び出す時、認証トークンとして使用されます。

#### シングルサインオン活性化·指定
![](http://static.toastoven.net/prod_contact_center/dev4_ja.png) 
サービス管理  →  認証  →  SSOログインタブで、SSOログインの有効化および無効化が可能で、有効化した場合は、選択したサービスに指定するSSOログインを選択できます。

#### 認証トークン作成
Token生成サンプルは以下の通りです。 パラメータ順序は必ず下記と一致している必要があり、SSOログインAPIキーを確認してください。
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

## シングルサインオンAPI
### SSO遠隔ログインAPI (Client Side)
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/v2/enduser/remote.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/v2/enduser/remote.json		

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|SSO遠隔ログインAPI (Client Side)|HTTPS  |POST    |UTF-8|Redirect    |ユーザーシステムで動的にformを生成してブラウザに返し、formは自動的にAPIにform情報を伝達。 APIで配信されたform情報で認証後、成功時のログインCookie値設定。|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|service	|Varchar(50)	|O	|サービスID|
|ユーザーID	   |usercode	|Varchar(50)	|O	|ユーザーID，唯一のユーザーであることを表示|
|ユーザー名	  |username	|Varchar(50)	|X	|ユーザー名|
|ユーザーメールアドレス	|email	|Varchar(100)	|X	|ユーザーメールアドレス|
|電話番号	        |phone	|Varchar(20)	|X	|電話番号|
|現在時間のtimestamp	|time	|Long	|O	|呼び出し時間が3分を超える場合、タイムアウトアラート出力。|
|認証Token	           |token	|Varchar	|O	|以下のパラメータ値とSSO  API  Keyにより算出された SHA256 (パラメータ値がnull、または空の値の場合、暗号化文字列に追加する必要はない。注意:文字列のうち、各値の順序は、以下の例に指定された順序と一致している必要がある。) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|
|リターン画面URL	|returnUrl	|Varchar	|X	|設定およびログインに成功した場合、そのアドレスに移動|

#### 結果データ
returnUrlパラメータが存在する場合、指定されたreturnUrlに移動、returnUrlがない場合は文字列:SUCCESSを返します。

### SSO遠隔ログインAPI (Server Side)
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/api/v2/enduser/remote.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/api/v2/enduser/remote.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|SSO遠隔ログインAPI(Server Side)|HTTPS  |POST    |UTF-8|String   |ユーザがサーバーから直接APIを呼び出し。 APIログイン成功後にログインCookie値を設定。|
  
#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|サービスID	|service	|Varchar(50)	|O	|サービスID|
|ユーザーID	   |usercode	|Varchar(50)	|O	|ユーザーID，唯一のユーザーであることを表示|
|ユーザー名	  |username	|Varchar(50)	|X	|ユーザー名|
|ユーザーメールアドレス	|email	|Varchar(100)	|X	|ユーザーメールアドレス|
|電話番号	        |phone	|Varchar(20)	|X	|電話番号|
|現在時間のtimestamp	|time	|Long	|O	|呼び出し時間が3分を超える場合、タイムアウトアラート出力。|
|認証Token	           |token	|Varchar	|O	|以下のパラメータ値とSSO  API  Keyにより算出された SHA256 (パラメータ値がnull、または空の値の場合、暗号化文字列に追加する必要はない。注意:文字列のうち、各値の順序は、以下の例に指定された順序と一致している必要がある。) SHA256Digest(service + usercode + username + email + phone + time)|

#### 結果データ
SUCCESS
 
### SSOログインURL (ユーザー)
#### インターフェース説明
|インターフェース名|プロトコル|呼び出し方向|エンコード|URL|URL(開発)|結果形式|
|------------|--------|--------|------|--|----------|--------|
|SSOログインURL|HTTPS|GET|UTF-8|ユーザー提供|ユーザー提供|Redirect|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|---------|---------|-----------|---------|----|
|リターンURL	|returnUrl	|Varchar	|O	|ログイン成功後に移動するURL|

#### SSOログイン機能の説明
**ユーザー未ログイン状態**
- ① ログイン画面に移動
- ② ユーザーログイン
- ③ サービス側のサーバーからユーザーのログイン処理およびログインユーザー関連クッキー作成
- ④ SSO遠隔ログインAPI呼び出し

**ユーザーログイン状態**
- ① SSO遠隔ログインAPI呼び出し

#### SSO遠隔ログインAPI呼び出し方法の説明
**SSO遠隔ログイン(Client Side)**
- ① ユーザー情報とAPI  Key基準でログインtoken作成
- ② ユーザー情報とtokenをブラウザーにリダイレクト
- ③ 画面でForm作成, 詳しいパラメーターは [SSO遠隔ログインAPI (Client Side)]() 参考
- ④ Form提出
- ⑤ SSO遠隔ログインAPIによりユーザー情報とtoken送信
- ⑥ ログインに成功した後、{returnUrl}に移動

**SSO遠隔ログイン(Server Side)**
- ① ユーザー情報とAPI  Key基準でログインtoken作成
- ② サーバーから「SSO遠隔ログインAPI(Server  Side)」呼び出し
- ③ API呼び出しパラメータ(usercodeとtime)をreturnUrlの後に追加 
  - 例示) https://nhn-cs.alpha-oc.toast.com/multilanguage/hc/ticket/list/?usercode=xxxxxx@163.com&time=1566531359635
- ④ {returnUrl}に移動
 
### SSOログイン状態API(ユーザー)
#### 인터페이스 설명
|インターフェース名|プロトコル|呼び出し方向|エンコード|URL|URL(開発)|インターフェース説明|結果形式|
|------------|--------|--------|------|--|----------|--------|--------------|
|SSOログイン状態API|HTTPS|GET|UTF-8|ユーザー提供|ユーザー提供|ユーザーがクッキー情報を基準にログインを確認した後、JSON形式のデータをリターン|JSON|

#### リクエストパラメータ定義
- なし

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|---------|-----------|---------|----|
|javascript function	|login	|Boolean	|O	|ログイン状態. ログイン ：true, 未ログイン ：false|
|ユーザーコード	|usercode	|Varchar(50)	|X	|ユーザーID(ユニーク値). ログイン状態がtrueの場合、ユーザーコードは必須|

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
✔ [Sample Code 다운로드](http://static.toastoven.net/prod_contact_center/oc_sso_sample.zip)

### iframeを利用したヘルプセンターの例
#### 1. iframeを利用してOnline  Contactヘルプセンターをユーザーページに挿入
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

#### 2. Online  Contactヘルプセンターページの高さを確認してiframeのheight調整
help_frame.ftl  ファイルのうち、javascript  コードを参照してください。
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
help_frame.ftl  ファイルのうち、javascript  コードを参照してください。
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
