## Contact Center > Online Contact > プログラマーのためのAPIガイド > 会員認証 (GET)

## 会員認証
### 概要
会員認証機能は、顧客会社が提供するサービスの会員認証を Online Contactのヘルプセンターでも適用し、会員のお問い合わせを受け付け、受け付けたお問い合わせ内訳を再確認できるようにするための機能です。
会員連動はGET方式とPOST方式の二つのタイプで提供しており、連動のためには Online Contactが提供する開発明細書に基づいてAPIを開発し、 Online Contact会員認証管理画面に登録する必要があります。

#### POST方式
-  連動させるサービスがPC、MOBILEプラットフォームでWEB基盤で提供される場合に適しています。
-  サービスのログイン画面がWEB URL形式で提供されている場合に使用できます。
-  開発明細でCLIENT-SIDE、SERVICER-SIDEの細部2タイプを提供します。

#### GET方式
-  WEBベースのログイン画面がないサービスに適しています。
-  WEBベースではないNative  APPサービスの場合に適した連動方式です。

### 全体的なプロセス
① USERがAPP内でヘルプセンターに接続します。
② 顧客会社のAPPは、ヘルプセンター呼び出し時に以下のURL形式で呼び出します。
- https://**{org}**.oc.toast.com/**{service}**/hc/?usercode=**{ユーザーID}**&username=**{ユーザー名前}**&email=**{ユーザーメールアドレス}**&phone=**{ユーザー電話番号}**&token=**{認証トークンの値}**
③ ヘルプセンターから「トークン検証URL」を呼び出します。（ここで、「トークン検証URL」は顧客会社が下記の明細書を参考に開発後、Online Contactの会員認証画面に登録してください。）
④ トークン検証後、正常である場合は  「お問い合わせ」  または  「お問い合わせ履歴」  ページにアクセスします。 この際、検証に失敗した場合、「お問い合わせ」は非会員として受け付けられます。

### 会員認証の方法
![](http://static.toastoven.net/prod_contact_center/dev_post_(2)_ja.png)
① サービス管理  >  ヘルプセンター  >  会員認証アクセス
② 会員認証設定項目で「有効」ボタンをクリック
③ サービスの性格に合った「ログインタイプ」を選択
④ 各タイプによって必要なAPI開発及びURL設定、保存

## 開発明細書
### 認証トークン作成
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

### トークン会員認証方法
#### インターフェース説明
URL
- https://{org}.oc.toast.com/{service}/hc/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{org}.oc.toast.com/{service}/hc/ticket/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{org}.oc.toast.com/{service}/hc/ticket/list/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d

URL (開発)
- https://{domain}.alpha-oc.toast.com/{service}/hc/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{domain}.alpha-oc.toast.com/{service}/hc/ticket/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d
- https://{domain}.alpha-oc.toast.com/{service}/hc/ticket/list/?usercode=aaaabbb&username=yzg&email=yzgname@163.com&phone=12345678901&time=12345678&token=8NPaBegAfbSvh1Lna9M0I1wBqjnoRyKO2r2izhuEAng%3d

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|Token 会員認証 |HTTPS |GET |UTF-8 | |サービス側でヘルプセンターに接続する際、顧客情報及び暗号化後に生成されたtoken値をパラメータ形式で送信|

#### パラメータ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|service	|Varchar(50)	|O	|サービスID|
|ユーザーID	   |usercode	|Varchar(50)	|O	|ユーザーID，唯一のユーザーであることを表示|
|ユーザー名	  |username	|Varchar(50)	|X	|ユーザー名|
|ユーザーメールアドレス	|email	|Varchar(100)	|O	|ユーザーメールアドレス|
|電話番号	        |phone	|Varchar(20)	|X	|電話番号|
|timestamp	|time	|Long	|O	|時間単位:ミリ秒|
|認証Token	           |token	|Varchar	|O	|次のパラメータ値と組織キーで計算（SHA256）。 (パラメータ値がnull、または空の値の場合、暗号化文字列に追加する必要はない。注意:文字列のうち、各値の順序は、以下の例に指定された順序と一致している必要がある。) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|

#### 結果データ
-  Token認証成功:会員にアクセスするアドレスに移動		
-  Token認証失敗:非会員でアクセスするアドレスに移動		
-  Token認証失敗状態でお問い合わせ履歴にアクセスすると、お問い合わせ画面に移動

### トークン認証API（サービス側）
#### インターフェース説明
- URL: サービス側から支援 		
- URL (開発): サービス側から支援 		

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|Token認証確認API |HTTPS |GET |UTF-8 |JSON |サービス側がtokenとusercodeでログイン状態を確認後、JSON形式の結果値を送信 |

#### リクエストパラメータ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|ユーザーID	   |usercode	|Varchar(50)	|O	|ユーザーID，唯一のユーザーであることを表示|
|サービス側が作成したToken	           |token	|Varchar	|O	|次のパラメータ値と組織キーで計算（SHA256）。 (パラメータ値がnull、または空の値の場合、暗号化文字列に追加する必要はない。注意:文字列のうち、各値の順序は、以下の例に指定された順序と一致している必要がある。) SHA256Digest(service + usercode + username + email + phone + retunrnUrl + time)|

#### Response Body
```
ログイン状況：
{
"login": "true",
"usercode":"usercodeXXX"
}


未ログイン状況：
{
"login": "false",
"usercode": null
}
```
