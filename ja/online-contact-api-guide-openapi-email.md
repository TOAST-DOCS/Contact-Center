## Contact Center > Online Contact > プログラマーのためのAPIガイド > メール設定

### 代表アカウント作成
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/create.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/create.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|代表アカウント作成|HTTPS  |POST    |UTF-8|JSON    |サービス代表アカウント作成. (作成後は修正不可) 形式: \*\*@oc.toast.com|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|メール情報	|mail	|String	|O	|メール情報(例:mail@oc.toast.comのmail部分)|

#### Query String
- mail=mail

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result.content	|displayMail	|String	|	  |発信者アドレス|
|	              |external	    |String	|	  |外部アカウントリスト|
|	              |mail	        |String	|O	|代表アカウントアドレス : mail@oc.toast.com|
|	              |name	        |String	|	  |発信者名|
|	              |template	    |String	|	  |メール形式|
|	              |updatedDt	  |Long	  |	  |アップデート時間|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":{
            "displayMail":"noreply@toast.com",
            "external":{},
            "mail":"mail@oc.toast.com",
            "name":"noreply",
            "template":"<p>#{content}</p>",
            "updatedDt":1597369998000
        }
    }
}
```

### メール情報照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|メール情報照会|HTTPS  |GET    |UTF-8|JSON    |該当サービスすべてのメール情報照会|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH　内に設定した{serviceId}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|-----------|-----|----|
|result.content	|displayMail	|String	|	  |発信者アドレス|
|	              |external	    |String	|	  |外部アカウントリスト|
|	              |mail	        |String	|O	|代表アカウントアドレス : mail@oc.toast.com|
|	              |name	        |String	|	  |発信者名|
|	              |template	    |String	|	  |メール形式|
|	              |updatedDt	  |Long	  |	  |アップデート時間|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":{
            "displayMail":"noreply@toast.com",
            "external":{},
            "mail":"mail@oc.toast.com",
            "name":"noreply",
            "template":"<p>#{content}</p>",
            "updatedDt":1597371255000
        }
    }
}
```

### 外部アカウント有効性チェック
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/verify.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/verify.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|外部アカウント有効性チェック|HTTPS  |POST    |UTF-8|JSON    |外部アカウント有効性チェック|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	     |serviceId	   |String	|O	|サービスID，URL PATH　内に設定した{serviceId}|
|外部アカウント情報　|request body	|String	  |O	|外部アカウント情報(JSON)|
|	             |id	         |Integer	 |   |外部アカウントID (新規作成時には必要なく修正時のみ必要)|
|	             |name	       |String	 |O	 |外部アカウント区分名称　(長さ:min=1, max=20)|
|	             |active	     |Boolean	 |O	 |外部アカウント状態(true:有効化 ,false:無効化), 修正時のみ状況伝達が必要|
|	             |host	       |String	 |O	 |メールサーバー|
|	             |port	       |Integer  |O	 |ポート(例:993)|
|	             |ssl	         |Boolean	 |O	 |ssl使用可否(true:使用,false:未使用)|
|	             |mail	       |String	 |O	 |外部アカウントアドレス(正確なメールアドレス)|
|	             |password	   |String	 |O	 |外部アカウントのパスワード(サービス利用期間中に入力したメールアドレスとパスワードが保管されます。)|
|	             |mailDel   	 |Boolean	 |O	 |原本を残す機能の使用可否(true:削除(メールがチケットに切り替えられると、当該メールが自動的に削除される。）,false:保留)|

#### Request Body
```
{
    "id":21,
    "name":"octest1",
    "active":true
    "host":"imap.163.com",
    "port":993,
    "ssl":true
    "mail":"octest1@163.com",
    "password":"yourpassword",
    "mailDel":false
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-------|--------|-------------|-----|---|
|result	|content	|String    	 |O	   |SUCCESS(成功)|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
         "content":"SUCCESS",
    }
}
```

### 外部アカウント登録
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|外部アカウント登録|HTTPS|POST|UTF-8|JSON|外部アカウント登録(有効性チェック後に登録可能)|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|---|
|サービスID	     |serviceId	   |String	|O	|サービスID，URL PATH　内に設定した{serviceId}|
|外部アカウント情報　|request body	|String	  |O	|外部アカウント情報(JSON)|
|	             |name	       |String	 |O	 |外部アカウント区分名称　(長さ:min=1, max=20)|
|	             |host	       |String	 |O	 |メールサーバー|
|	             |port	       |Integer  |O	 |ポート(例:993)|
|	             |ssl	         |Boolean	 |O	 |ssl使用可否(true:使用,false:未使用)|
|	             |mail	       |String	 |O	 |外部アカウントアドレス(正確なメールアドレス)|
|	             |password	   |String	 |O	 |外部アカウントのパスワード(サービス利用期間中に入力したメールアドレスとパスワードが保管されます。)|
|	             |mailDel   	 |Boolean	 |O	 |原本を残す機能の使用可否(true:削除(メールがチケットに切り替えられると、当該メールが自動的に削除される。）,false:保留)|

#### Request Body
```
{
    "name":"octest1",
    "host":"imap.163.com",
    "port":993,
    "ssl":true
    "mail":"octest1@163.com",
    "password":"yourpassword",
    "mailDel":false
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|result.content	|id	      |Integer	|	  |外部アカウントID|
|               |name	    |String	  |O	|外部アカウント区分名称|
|	              |active	  |Boolean	|O	|外部アカウント状態(固定値:true)|
|	              |host	    |String	  |O	|メールサーバー|
|	              |port	    |Integer	|O	|ポート(例:993)|
|               |ssl	    |Boolean	|O	|ssl使用可否(true:使用,false:未使用)|
|	              |mail	    |String	  |O	|外部アカウントアドレス|
|	              |password	|String	  |O	|外部アカウントパスワード|
|	              |mailDel	|Boolean	|O	|原本を残す機能の使用可否(true:削除,　false:保留)|
|	              |createdDt	|Long	  |	  |作成時間|
|	              |updatedDt	|Long   |		|修正時間|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":{
            "id":16,
            "name":"octest1",
            "active":true
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "password":"********",
            "mailDel":false,
            "createdDt":1597382469685,
            "updatedDt":1597382469685
        }
    }
}
```

### 外部アカウント修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|外部アカウント修正|HTTPS|PUT|UTF-8|JSON|外部アカウント修正(有効性チェック後に修正可能)|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|---|
|サービスID	     |serviceId	    |String	  |O	  |サービスID，URL PATH内に設定した{serviceId}|
|外部アカウントID	   |id	         |Integer   |O	 |外部アカウントID,URL PATH内に設定した{id}|
|外部アカウント情報	 |request body	|String	  |O	  |外部アカウント情報(JSON)|
|	             |name	       |String	 |O	 |外部アカウント区分名称　(長さ:min=1, max=20)|
|	             |active	     |Boolean	 |	 |外部アカウント状態(true:有効化 ,false:無効化)|
|	             |host	       |String	 |O	 |メールサーバー|
|	             |port	       |Integer  |O	 |ポート(例:993)|
|	             |ssl	         |Boolean	 |O	 |ssl使用可否(true:使用,false:未使用)|
|	             |mail	       |String	 |O	 |外部アカウントアドレス(正確なメールアドレス)|
|	             |password	   |String	 |O	 |外部アカウントのパスワード(サービス利用期間中に入力したメールアドレスとパスワードが保管されます。)|
|	             |mailDel   	 |Boolean	 |O	 |原本を残す機能の使用可否(true:削除(メールがチケットに切り替えられると、当該メールが自動的に削除される。）,false:保留)|

#### Request Body
```
{
    "name":"octest1",
    "host":"imap.163.com",
    "port":993,
    "ssl":true
    "mail":"octest1@163.com",
    "password":"yourpassword",
    "mailDel":false
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|----|----|
|result.content	|id	      |Integer	|	  |外部アカウントID|
|               |name	    |String	  |O	|外部アカウント区分名称|
|	              |active	|Boolean	|O	|外部アカウント状態(true:有効化,false:無効化)|
|	              |host	    |String	  |O	|メールサーバー|
|	              |port	    |Integer	|O	|ポート(例:993)|
|               |ssl	    |Boolean	|O	|ssl使用可否(true:使用,false:未使用)|
|	              |mail	    |String	  |O	|外部アカウントアドレス|
|	              |password	|String	  |O	|外部アカウントパスワード|
|	              |mailDel	|Boolean	|O	|原本を残す機能の使用可否(true:削除,　false:保留)|
|	              |createdDt	|Long	  |	  |作成時間|
|	              |updatedDt	|Long   |		|修正時間|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":{
            "id":null,
            "name":"octest1",
            "active":null
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "password":"********",
            "mailDel":false,
            "createdDt":null,
            "updatedDt":1597382469685
        }
    }
}
```

### 外部アカウント有効化
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/enable.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/enable.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|外部アカウント有効化|HTTPS|PUT|UTF-8|JSON|無効化ステータス外部アカウントを有効化|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|---|
|サービスID	     |serviceId	    |String	  |O	  |サービスID，URL PATH内に設定した{serviceId}|
|外部アカウントID	   |id	         |Integer   |O	 |外部アカウントID,URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result.content	|id	      |Integer	|	  |外部アカウントID|
|               |name	    |String	  |O	|外部アカウント区分名称|
|	              |active	  |Boolean	|O	|外部アカウント状態(固定値:true)|
|	              |host	    |String	  |O	|メールサーバー|
|	              |port	    |Integer	|O	|ポート(例:993)|
|               |ssl	    |Boolean	|O	|ssl使用可否(true:使用,false:未使用)|
|	              |mail	    |String	  |O	|外部アカウントアドレス|
|	              |password	|String	  |O	|外部アカウントパスワード|
|	              |mailDel	|Boolean	|O	|原本を残す機能の使用可否(true:削除,　false:保留)|
|	              |createdDt	|Long	  |	  |作成時間|
|	              |updatedDt	|Long   |		|修正時間|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":{
            "id":21,
            "name":"octest1",
            "active":true
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "mailDel":false,
            "createdDt":1578376856000,
            "updatedDt":1597384423000
        }
    }
```

### 外部アカウント無効化
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/disable.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}/disable.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|外部アカウント無効化|HTTPS|PUT|UTF-8|JSON|有効化状態の外部アカウントを無効化|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|---|
|サービスID	     |serviceId	    |String	  |O	  |サービスID，URL PATH内に設定した{serviceId}|
|外部アカウントID	   |id	         |Integer   |O	 |外部アカウントID,URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|result.content	|id	      |Integer	|	  |外部アカウントID|
|               |name	    |String	  |O	|外部アカウント区分名称|
|	              |active	  |Boolean	|O	|外部アカウント状態(固定値:false)|
|	              |host	    |String	  |O	|メールサーバー|
|	              |port	    |Integer	|O	|ポート(例:993)|
|               |ssl	    |Boolean	|O	|ssl使用可否(true:使用,false:未使用)|
|	              |mail	    |String	  |O	|外部アカウントアドレス|
|	              |password	|String	  |O	|外部アカウントパスワード|
|	              |mailDel	|Boolean	|O	|原本を残す機能の使用可否(true:削除,　false:保留)|
|	              |createdDt	|Long	  |	  |作成時間|
|	              |updatedDt	|Long   |		|修正時間|


#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":{
            "id":21,
            "name":"octest1",
            "active":false
            "host":"imap.163.com",
            "port":993,
            "ssl":true
            "mail":"octest1@163.com",
            "mailDel":false,
            "createdDt":1578376856000,
            "updatedDt":1597384423000
        }
    }
```

### 外部アカウント削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail/external/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|外部アカウント削除|HTTPS|DELETE|UTF-8|JSON|無効化状態の外部アカウントを削除|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|---|
|サービスID	     |serviceId	    |String	  |O	  |サービスID，URL PATH内に設定した{serviceId}|
|外部アカウントID	   |id	         |Integer   |O	 |外部アカウントID,URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|-----|---|
|result.content|		|String|		|"SUCCESS":削除成功|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":"SUCCESS"
    }
}
```

### メール情報保存
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/mail.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/mail.json	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|メール情報保存|HTTPS|POST|UTF-8|JSON|メール情報保存|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|---|
|サービスID	        |serviceId	   |String	|O	|サービスID|
|メール設定情報	 |request body	|String	 |O	 |メール設定情報(JSON)|
|	                 |name	        |String	 |	 |発信者名(길이:min = 0, max = 45)|
|	                 |displayMail	  |String	 |	 |発信者アドレス(例：noreply@oc.toast.com)|
|	                 |template	    |String	 |	 |メールレイアウト. 例) \<p\>\#\{content\}\<\/p\> このメールレイアウトは、すべてのメールに適用されます。 #{content}タグは必ず追加してください。|

#### Request Body
```
{
    "name":"noreply",
    "displayMail":"noreply@oc.toast.com",
    "template":"<p>#{content}</p>"
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|result	|		|	        |      |    |

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":null
}
```
