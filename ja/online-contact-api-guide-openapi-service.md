## Contact Center > Online Contact > API ガイド > サービス 

### 契約項目コード
- ticket: チケット (基本的に活性化、変更不可能)
- chat: チャット
- telticket: チケット (電話, CTI利用含む)
- endusermanagement: 顧客情報管理
- callback: コールバック
- helpdoc: FAQ
- knowledge: ナレッジマネジメント
- issuetransferstatistics: イシュー移管統計 (今後追加予定)
- reinquiryrate: 再入信率 (今後追加予定)
- smssend: SMS 発送 (今後追加予定)
- smssendingstatus: SMS発送現況 (今後追加予定)
- electronicboard: 電光板 (今後追加予定)
- ticketevaluation: チケット評価 (今後追加予定)
- happycall: ハッピーコール (今後追加予定)
- security: セキュリティサービス (今後追加予定)


### サービス追加
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/add.json
- URL(開発): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/add.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス追加|HTTPS  |POST    |UTF-8|JSON    |新規サービス追加|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|サービス情報|request body	|String	|O	|サービス情報(JSON)|
|	          |serviceId	  |String	|O	|サービスID（唯一の値：yes, 長さ:min = 0, max = 45; 形式:英文)|
|	          |name	        |String	|O	|サービス名　(唯一の値：yes, 長さ:min = 0, max = 100)|
|	          |language	    |String	|O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|				    |timeZone	    |String	|X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|

変数timeZoneのデフォルト値は以下のとおりです。
- language=ko: timeZone=Asia/Seoul
- language=ja: timeZone=Asia/Tokyo
- language=en: timeZone=America/New_York
- language=zh: timeZone=Asia/Shanghai

#### Request Body
```
{
    "serviceId":"GameBaseService",
    "name":"GameBaseServiceAPI",
    "language":"ko",
    "timeZone":"Asia/Seoul"
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|------|----------|-----|----|
|result.content	|serviceId	|String	|O	|サービス ID|
|	              |name	      |String	|O	|サービス名|
|	              |active	    |Boolean	|X	|サービスの状況(true:有効化, false:無効化)|
|	              |language	  |String	  |O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|	              |timeZone 	|String	  |X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|サービス作成時間|
|	              |updatedDt	|Long	    |X	|サービスアップデート時間|
|               |securityKey	|String	|X	|Open API Key|

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

### サービス詳細
#### インターフェース説明
- URL:	https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json			
- URL (開発):　https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス詳細  |HTTPS  |GET    |UTF-8|JSON    |サービスIDを通じてサービス情報を照会|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|result.content	|serviceId	|String	|O	|サービス ID|
|	              |name	      |String	|O	|サービス名|
|	              |active	    |Boolean	|X	|サービスの状況(true:有効化, false:無効化)|
|	              |language	  |String	  |O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|	              |timeZone 	|String	  |X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|サービス作成時間|
|	              |updatedDt	|Long	    |X	|サービスアップデート時間|
|               |securityKey	|String	|X	|Open API Key|

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

### サービス修正
#### インターフェース説明
- URL:	https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json 				
- URL (開発):　https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json 	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス修正  |HTTPS  |PUT    |UTF-8|JSON    |サービスIDを通じてサービス情報を修正|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|サービス情報	|request body	|String	|O	|サービス情報（JSON）|
|	          |name	        |String	|O	|サービス名　(唯一の値：yes, 長さ:min = 0, max = 100)|
|	          |language	    |String	|O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|				    |timeZone	    |String	|X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|

変数timeZoneのデフォルト値は以下のとおりです。
- language=ko: timeZone=Asia/Seoul
- language=ja: timeZone=Asia/Tokyo
- language=en: timeZone=America/New_York
- language=zh: timeZone=Asia/Shanghai

#### Request Body
```
{
    "name":"GameBaseServiceAPI",
    "language":"ko",
    "timeZone":"Asia/Seoul"
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|result.content	|serviceId	|String	|O	|サービス ID|
|	              |name	      |String	|O	|サービス名|
|	              |active	    |Boolean	|X	|サービスの状況(true:有効化, false:無効化)|
|	              |language	  |String	  |O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|	              |timeZone 	|String	  |X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|サービス作成時間|
|	              |updatedDt	|Long	    |X	|サービスアップデート時間|
|               |securityKey	|String	|X	|Open API Key|

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
            "active":null,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "createdDt":null,
            "updatedDt":1586761475102,
            "securityKey":null
        }
    }
}
```

### サービス無効化
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/disable.json					
- URL (開発): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/disable.json			 

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス無効化  |HTTPS  |PUT    |UTF-8|JSON    |サービスIDを通じてサービスを無効化   |共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|serviceId	|String	|O	|サービスID（query）|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|result.content	|serviceId	|String	|O	|サービス ID|
|	              |name	      |String	|O	|サービス名|
|	              |active	    |Boolean	|X	|サービスの状況(true:有効化, false:無効化)|
|	              |language	  |String	  |O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|	              |timeZone 	|String	  |X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|サービス作成時間|
|	              |updatedDt	|Long	    |X	|サービスアップデート時間|
|               |securityKey	|String	|X	|Open API Key|

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
            "active":false,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "updatedDt":1586745222000,
            "updatedDt":1586761475000,
            "securityKey":null
        }
    }
}
```

### サービス有効化
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/enable.json					
- URL (開発):　https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/enable.json		

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス活性化  |HTTPS  |PUT    |UTF-8|JSON    |サービスIDを通じてサービス有効化|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|serviceId	|String	|O	|サービスID（query）|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|result.content	|serviceId	|String	|O	|サービス ID|
|	              |name	      |String	|O	|サービス名|
|	              |active	    |Boolean	|X	|サービスの状況(true:有効化, false:無効化)|
|	              |language	  |String	  |O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|	              |timeZone 	|String	  |X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|サービス作成時間|
|	              |updatedDt	|Long	    |X	|サービスアップデート時間|
|               |securityKey	|String	|X	|Open API Key|

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
            "serviceId":"GameBaseService",
            "name":"GameBaseServiceAPI",
            "active":true,
            "language":"ko",
            "timeZone":"Asia/Seoul",
            "updatedDt":1586745222000,
            "updatedDt":1586761475000,
            "securityKey":null
        }
    }
}
```

### サービス削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/{serviceId}.json					
- URL (開発):　https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/{serviceId}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス削除  |HTTPS  |DELETE    |UTF-8|JSON    |サービスIDを通じて無効化状況のサービス削除|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|----|-----------|----|----|
|result.content		|String	|X	|"SUCCESS":削除成功, "ENABLE":有効化状況で削除不可能，無効化の後削除可能|

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

### サービスAPI Key再発行
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/apikey/refresh.json				
- URL (開発):　https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/apikey/refresh.json								 	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービスAPI Key再発行  |HTTPS  |PUT    |UTF-8|JSON    |サービスIDを通じて当該サービスに生成されたAPI  Keyを再発行|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|serviceId	|String	|O	|サービスID（query）|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|result.content		|String	|X	|新規API Key|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "content":"bd7a45aa764f4936a43ef0c4500da7ba"
    }
}
```

### サービス一覧
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/service/list.json			 			
- URL (改善):　https://{domain}.alpha-oc.toast.com/openapi/v1/admin/service/list.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス一覧 |HTTPS  |GET    |UTF-8|JSON    |組織内に生成されたすべてのサービス照会|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|ページ	|page	|Int	|X	|基本値:1|
|ページあたりの露出件数 |pageSize	|Int	|X	|基本値:100|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|result.content	|serviceId	|String	|O	|サービス ID|
|	              |name	      |String	|O	|サービス名|
|	              |active	    |Boolean	|X	|サービスの状況(true:有効化, false:無効化)|
|	              |language	  |String	  |O	|サービス言語 (値:zh\|ja\|ko\|en, ko: 韓国語, ja:日本語, en:英語, zh:中国語)|
|	              |timeZone 	|String	  |X	|タイム·ゾーン (값:Asia/Seoul\|Asia/Tokyo\|...)|
|               |createdDt	|Long	    |X	|サービス作成時間|
|	              |updatedDt	|Long	    |X	|サービスアップデート時間|
|               |securityKey	|String	|X	|Open API Key|
|result.total	|total	|Long	|X	|総件数|
|result.pages	|pages	|Int	|X	|総ページ数|
|result.pageNum	|pageNum	|Int	|X	|現在のページ|
|result.pageSize	|pageSize	|Int	|X	|ページあたりの露出件数|

#### Response Body
```
{
    "header":{
        "resultCode":200,
        "resultMessage":"",
        "isSuccessful":true
    },
    "result":{
        "contents":[
            {
                "serviceId":"gamebase",
                "name":"Gamebase",
                "active":true,
                "language":"ko",
                "timeZone":"Asia/Shanghai",
                "createdDt":1552901051000,
                "updatedDt":1566203644000,
                "securityKey":"1b7426d5821b42bc9e1503bfb2979aee"
            },
            {
                "serviceId":"GameBaseService",
                "name":"GameBaseServiceAPI",
                "active":true,
                "language":"ko",
                "timeZone":"Asia/Seoul",
                "createdDt":1586745222000,
                "updatedDt":1586765984000,
                "securityKey":"bd7a45aa764f4936a43ef0c4500da7ba"
            },
        ],
        "total":2,
        "pages":1,
        "pageNum":1,
        "pageSize":100
    }
}
```

### サービス契約登録
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/reg.json			
- URL (開発):　https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/reg.json			 

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス契約登録 |HTTPS  |POST    |UTF-8|JSON    |サービス新規契約登録|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービス契約情報	|request body	|String	|O	|サービス情報(JSON)|
|	                |serviceId	   |String	|O	|サービスID（唯一の値：yes, 長さ:min = 0, max = 45; 形式:英文)|
|	                |billingSettings	|List	|X	  |契約項目設定リスト|
|	                |    billingSettingCode	|String	|O	|項目コード(契約項目コード参照)|
|	                |    active	            |Boolean	|X	|有効化:true  無効化:false|

#### Request Body
```
{
        "serviceId": "example",
        "billingSettings": [{
                "billingItemCode": "callback",
                "active": false
        }, {
                "billingItemCode": "chat",
                "active": true
        }, {
                "billingItemCode": "endusermanagement",
                "active": false
        }, {
                "billingItemCode": "helpdoc",
                "active": false
        }, {
                "billingItemCode": "knowledge",
                "active": true
        }, {
                "billingItemCode": "telticket",
                "active": false
        }]
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|----|-----|
|result.content	|id	|Long	|O	|契約ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |organizationId	|String	|O	|組織ID|
|	              |type	          |Int	  |O	|サービスタイプ(1:お問合せ管理, 2:イシュー管理), 基本値:1|
|	              |status	        |String	|O	|契約状況(作成中:create, 利用中:inuse, 利用停止:pause, 削除:stop)|
|	              |startDt	      |String	|O	|サービス利用開始日(韓国時間)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|割引率(%)|
|	              |freeExtension	|Int	  |O	|無料体験期間延長日|
|	              |active	        |Boolean	|O	|サービス契約(有効化:true, 無効化:false)|
|	              |freeTrial	    |Boolean	|O	|無料体験期間(はい:true, いいえ:false)|
|	              |billingSettings	|List	  |O	|契約項目設定リスト|
|	              |    id	              |Long	  |O	|契約項目設定ID|
|	              |    billingId	      |Long	  |O	|契約ID|
|	              |    billingSettingCode	|String	|O	|項目コード(契約項目コード参照)|
|	              |    active	            |Boolean	|O	|有効化:true  無効化:false|

#### Response Body
```
{
        "header": {
                "resultCode": 200,
                "resultMessage": "",
                "isSuccessful": true
        },
        "result": {
                "content": {
                        "id": 214,
                        "organizationId": "WopqM8euoYw89B7i",
                        "organizationName": "NHN-CS",
                        "serviceId": "example",
                        "serviceName": "example",
                        "type": 1,
                        "language": "zh",
                        "status": "inuse",
                        "startDt": "20201204090910",
                        "discountRate": 0,
                        "freeExtension": 0,
                        "email": "xxxxxxxxxxxx@nhn.com",
                        "active": true,
                        "createdDt": 1607044142000,
                        "updatedDt": 1607044150934,
                        "freeTrial": false,
                        "billingSettings": [{
                                "id": 656,
                                "billingId": 214,
                                "billingItemCode": "callback",
                                "active": false
                        }, {
                                "id": 657,
                                "billingId": 214,
                                "billingItemCode": "chat",
                                "active": true
                        }, {
                                "id": 658,
                                "billingId": 214,
                                "billingItemCode": "endusermanagement",
                                "active": false
                        }, {
                                "id": 659,
                                "billingId": 214,
                                "billingItemCode": "helpdoc",
                                "active": false
                        }, {
                                "id": 660,
                                "billingId": 214,
                                "billingItemCode": "knowledge",
                                "active": true
                        }, {
                                "id": 661,
                                "billingId": 214,
                                "billingItemCode": "telticket",
                                "active": false
                        }, {
                                "id": 662,
                                "billingId": 214,
                                "billingItemCode": "ticket",
                                "active": true
                        }]
                }
        }
}
```

### サービス契約変更
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/update/{billingId}.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/update/{billingId}.json	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス契約変更(1日1回のみ可能) |HTTPS  |PUT    |UTF-8|JSON    |契約変更|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービス契約情報	|request body	|String	|O	|サービス情報(JSON)|
|	                |id	          |Long	  |O	|契約ID|
|	                |serviceId	  |String	|O	|サービスID（唯一の値：yes, 長さ:min = 0, max = 45; 形式:英文)|
|	                |billingSettings	|List	|O	|契約項目設定リスト|
|	                |id	              |Long	|O	|契約項目設定ID|
|	                |billingId	      |Long	|X	|契約ID|
|	                |    billingSettingCode	|String	|O	|項目コード(契約項目コード参照)|
|	                |    active	            |Boolean	|X	|有効化:true  無効化:false|

#### Request Body
```
{
        "id": 205,
        "serviceId": "qwqwqw",
        "billingSettings": [{
                "id": 620,
                "billingId": 205,
                "billingItemCode": "callback",
                "active": false
        }, {
                "id": 621,
                "billingId": 205,
                "billingItemCode": "chat",
                "active": false
        }, {
                "id": 622,
                "billingId": 205,
                "billingItemCode": "endusermanagement",
                "active": false
        }, {
                "id": 623,
                "billingId": 205,
                "billingItemCode": "helpdoc",
                "active": false
        }, {
                "id": 624,
                "billingId": 205,
                "billingItemCode": "knowledge",
                "active": false
        }, {
                "id": 625,
                "billingId": 205,
                "billingItemCode": "telticket",
                "active": false
        }]
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|契約ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |organizationId	|String	|O	|組織ID|
|	              |type	          |Int	  |O	|サービスタイプ(1:お問合せ管理, 2:イシュー管理), 基本値:1|
|	              |status	        |String	|O	|契約状況(作成中:create, 利用中:inuse, 利用停止:pause, 削除:stop)|
|	              |startDt	      |String	|O	|サービス利用開始日(韓国時間)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|割引率(%)|
|	              |freeExtension	|Int	  |O	|無料体験期間延長日|
|	              |active	        |Boolean	|O	|サービス契約(有効化:true, 無効化:false)|
|	              |freeTrial	    |Boolean	|O	|無料体験期間(はい:true, いいえ:false)|
|	              |billingSettings	|List	  |O	|契約項目設定リスト|
|	              |    id	              |Long	  |O	|契約項目設定ID|
|	              |    billingId	      |Long	  |O	|契約ID|
|	              |    billingSettingCode	|String	|O	|項目コード(契約項目コード参照)|
|	              |    active	            |Boolean	|O	|有効化:true  無効化:false|

#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "content": {
            "id": 205,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "qwqwqw",
            "serviceName": "qwqwqw",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201202115045",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606877440000,
            "updatedDt": 1607046392063,
            "freeTrial": false,
            "billingSettings": [{
                "id": 620,
                "billingId": 205,
                "billingItemCode": "callback",
                "active": false
            }, {
                "id": 621,
                "billingId": 205,
                "billingItemCode": "chat",
                "active": false
            }, {
                "id": 622,
                "billingId": 205,
                "billingItemCode": "endusermanagement",
                "active": false
            }, {
                "id": 623,
                "billingId": 205,
                "billingItemCode": "helpdoc",
                "active": false
            }, {
                "id": 624,
                "billingId": 205,
                "billingItemCode": "knowledge",
                "active": false
            }, {
                "id": 625,
                "billingId": 205,
                "billingItemCode": "telticket",
                "active": false
            }]
        }
    }
}

1日1回以上変更した場合，Response：
{
    "header": {
        "resultCode": 9015,
        "resultMessage": "billing.setting.today.already.changed",
        "isSuccessful": false
    },
    "result": {
        "content": {
            "exception": "OcException",
            "message": "billing.setting.today.already.changed"
        }
    }
}
```

### サービス契約一覧
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/list.json		
- URL (開発): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/list.json		

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|組織内サービス契約一覧|HTTPS  |GET    |UTF-8|JSON    |組織内のサービス契約リスト取得|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|組織内のサービス契約リスト取得	|page	|Int	|X	|ページ, 基本値:1|
|	                              |pageSize	|Int	|X	|ページあたりの露出件数，基本値:10|
|	                              |billingSettingCode	|		|   |   |
|	                              |active			        |   |   |   |

#### Request URL
```
/openapi/v1/admin/billing/list.json?page=1&pageSize=10	
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|----|
|result.contents	|id	|Long	|O	|契約ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |organizationId	|String	|O	|組織ID|
|	              |type	          |Int	  |O	|サービスタイプ(1:お問合せ管理, 2:イシュー管理), 基本値:1|
|	              |status	        |String	|O	|契約状況(作成中:create, 利用中:inuse, 利用停止:pause, 削除:stop)|
|	              |startDt	      |String	|O	|サービス利用開始日(韓国時間)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|割引率(%)|
|	              |freeExtension	|Int	  |O	|無料体験期間延長日|
|	              |active	        |Boolean	|O	|サービス契約(有効化:true, 無効化:false)|
|	              |freeTrial	    |Boolean	|O	|無料体験期間(はい:true, いいえ:false)|

#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "contents": [{
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000
        }, {
            "id": 212,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201203154729",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606981630000,
            "updatedDt": 1606981649000
        }, {
            "id": 205,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "qwqwqw",
            "serviceName": "qwqwqw",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201202115045",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606877440000,
            "updatedDt": 1607046392000
        }, {
            "id": 196,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example2",
            "serviceName": "example2",
            "type": 1,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201201105044",
            "discountRate": 100,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606787441000,
            "updatedDt": 1606875428000
        }, {
            "id": 192,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example3",
            "serviceName": "example3",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201127082852",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606436928000,
            "updatedDt": 1606436933000
        }, {
            "id": 191,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example4",
            "serviceName": "example4",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201127072001",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606432792000,
            "updatedDt": 1606432802000
        }, {
            "id": 154,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example5",
            "serviceName": "example5",
            "type": 1,
            "language": "ja",
            "status": "inuse",
            "startDt": "20201124103657",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606181811000,
            "updatedDt": 1606783784000
        }, {
            "id": 153,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "testfour",
            "serviceName": "testfour",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201124090639",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606179981000,
            "updatedDt": 1606181786000
        }, {
            "id": 152,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "testthird",
            "serviceName": "testthird",
            "type": 2,
            "language": "ko",
            "status": "inuse",
            "startDt": "20201124093856",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1606178332000,
            "updatedDt": 1606180298000
        }, {
            "id": 146,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "aaammm",
            "serviceName": "aaammm",
            "type": 1,
            "language": "zh",
            "status": "pause",
            "startDt": "20201119142206",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": false,
            "createdDt": 1605762562000,
            "updatedDt": 1606093890000
        }],
        "total": 70,
        "pages": 7,
        "pageNum": 1,
        "pageSize": 10
    }
}
```

### サービス契約詳細 - サービスID
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/service/{serviceId}.json	
- URL (開発): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/service/{serviceId}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス契約詳細 - サービスID|HTTPS  |GET    |UTF-8|JSON    |サービスIDから契約詳細情報を取得|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービス契約詳細情報|serviceId	|String	|O	|サービスID|

#### Request URL
```
/openapi/v1/admin/billing/service/example.json	
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|契約ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |organizationId	|String	|O	|組織ID|
|	              |type	          |Int	  |O	|サービスタイプ(1:お問合せ管理, 2:イシュー管理), 基本値:1|
|	              |status	        |String	|O	|契約状況(作成中:create, 利用中:inuse, 利用停止:pause, 削除:stop)|
|	              |startDt	      |String	|O	|サービス利用開始日(韓国時間)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|割引率(%)|
|	              |freeExtension	|Int	  |O	|無料体験期間延長日|
|	              |active	        |Boolean	|O	|サービス契約(有効化:true, 無効化:false)|
|	              |freeTrial	    |Boolean	|O	|無料体験期間(はい:true, いいえ:false)|
|	              |billingSettings	|List	  |O	|契約項目設定リスト|
|	              |    id	              |Long	  |O	|契約項目設定ID|
|	              |    billingId	      |Long	  |O	|契約ID|
|	              |    billingSettingCode	|String	|O	|項目コード(契約項目コード参照)|
|	              |    active	            |Boolean	|O	|有効化:true  無効化:false|
|	              |    billingItem	      |Object	  |X	|有料サービス項目詳細|
|	              |        code	              |String	  |O	|項目Code|
|	              |        open	              |Boolean	|O	|有効化:true  無効化:false|

#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "content": {
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000,
            "freeTrial": false,
            "billingSettings": [{
                "id": 656,
                "billingId": 214,
                "billingItemCode": "callback",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "callback",
                    "parentCode": "additional",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "",
                    "sumCounterName": "onlinecontact.callback_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "14"
                }
            }, {
                "id": 657,
                "billingId": 214,
                "billingItemCode": "chat",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "chat",
                    "parentCode": "chat",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.chat_lisence",
                    "sumCounterName": "onlinecontact.chat_count",
                    "resourceIdSuffix1": "06",
                    "resourceIdSuffix2": "07"
                }
            }, {
                "id": 658,
                "billingId": 214,
                "billingItemCode": "endusermanagement",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "endusermanagement",
                    "parentCode": "endusermanagement",
                    "baseAmount": 250000,
                    "dayAmount": 8333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.customer_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "19"
                }
            }, {
                "id": 659,
                "billingId": 214,
                "billingItemCode": "helpdoc",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "helpdoc",
                    "parentCode": "helpcenter",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.faq_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "10"
                }
            }, {
                "id": 660,
                "billingId": 214,
                "billingItemCode": "knowledge",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "knowledge",
                    "parentCode": "guide",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.knowledge_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "09"
                }
            }, {
                "id": 661,
                "billingId": 214,
                "billingItemCode": "telticket",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "telticket",
                    "parentCode": "ticket",
                    "baseAmount": 70000,
                    "dayAmount": 2333,
                    "useUserCount": true,
                    "countFree": 6000,
                    "countLevel1": 40000,
                    "countLevel1Unit": 3.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 1.5,
                    "open": true,
                    "licenceCounterName": "onlinecontact.call_licence",
                    "sumCounterName": "onlinecontact.call_seconds",
                    "resourceIdSuffix1": "02",
                    "resourceIdSuffix2": "03"
                }
            }, {
                "id": 662,
                "billingId": 214,
                "billingItemCode": "ticket",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "ticket",
                    "parentCode": "ticket",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.ticket_licence",
                    "sumCounterName": "onlinecontact.ticket_count",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "01"
                }
            }, {
                "billingItemCode": "ticketevaluation",
                "active": false,
                "billingItem": {
                    "code": "ticketevaluation",
                    "parentCode": "additional",
                    "baseAmount": 100000,
                    "dayAmount": 3333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": false,
                    "sumCounterName": "onlinecontact.ticket.evaluation_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "17"
                }
            }]
        }
    }
}
```

### サービス契約詳細 - 契約ID
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/openapi/v1/admin/billing/{billingId}.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/openapi/v1/admin/billing/{billingId}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス契約詳細 - 契約ID|HTTPS  |GET    |UTF-8|JSON    |契約IDから契約詳細情報を取得|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービス契約詳細情報|billingId	|Long	|O	|契約ID|

#### Request URL
```
/openapi/v1/admin/billing/214.json
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|----|
|result.content	|id	|Long	|O	|契約ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |organizationId	|String	|O	|組織ID|
|	              |type	          |Int	  |O	|サービスタイプ(1:お問合せ管理, 2:イシュー管理), 基本値:1|
|	              |status	        |String	|O	|契約状況(作成中:create, 利用中:inuse, 利用停止:pause, 削除:stop)|
|	              |startDt	      |String	|O	|サービス利用開始日(韓国時間)：yyyyMMddHHmmss|
|	              |discountRate	  |Int	  |O	|割引率(%)|
|	              |freeExtension	|Int	  |O	|無料体験期間延長日|
|	              |active	        |Boolean	|O	|サービス契約(有効化:true, 無効化:false)|
|	              |freeTrial	    |Boolean	|O	|無料体験期間(はい:true, いいえ:false)|
|	              |billingSettings	|List	  |O	|契約項目設定リスト|
|	              |    id	              |Long	  |O	|契約項目設定ID|
|	              |    billingId	      |Long	  |O	|契約ID|
|	              |    billingSettingCode	|String	|O	|項目コード(契約項目コード参照)|
|	              |    active	            |Boolean	|O	|有効化:true  無効化:false|
|	              |    billingItem	      |Object	  |X	|有料サービス項目詳細|
|	              |        code	              |String	  |O	|項目Code|
|	              |        open	              |Boolean	|O	|有効化:true  無効化:false|
#### Response Body
```
{
    "header": {
        "resultCode": 200,
        "resultMessage": "",
        "isSuccessful": true
    },
    "result": {
        "content": {
            "id": 214,
            "organizationId": "WopqM8euoYw89B7i",
            "organizationName": "NHN-CS",
            "serviceId": "example",
            "serviceName": "example",
            "type": 1,
            "language": "zh",
            "status": "inuse",
            "startDt": "20201204090910",
            "discountRate": 0,
            "freeExtension": 0,
            "email": "xxxxxxxxxxxx@nhn.com",
            "active": true,
            "createdDt": 1607044142000,
            "updatedDt": 1607044151000,
            "freeTrial": false,
            "billingSettings": [{
                "id": 656,
                "billingId": 214,
                "billingItemCode": "callback",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "callback",
                    "parentCode": "additional",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "",
                    "sumCounterName": "onlinecontact.callback_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "14"
                }
            }, {
                "id": 657,
                "billingId": 214,
                "billingItemCode": "chat",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "chat",
                    "parentCode": "chat",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.chat_lisence",
                    "sumCounterName": "onlinecontact.chat_count",
                    "resourceIdSuffix1": "06",
                    "resourceIdSuffix2": "07"
                }
            }, {
                "id": 658,
                "billingId": 214,
                "billingItemCode": "endusermanagement",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "endusermanagement",
                    "parentCode": "endusermanagement",
                    "baseAmount": 250000,
                    "dayAmount": 8333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.customer_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "19"
                }
            }, {
                "id": 659,
                "billingId": 214,
                "billingItemCode": "helpdoc",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "helpdoc",
                    "parentCode": "helpcenter",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.faq_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "10"
                }
            }, {
                "id": 660,
                "billingId": 214,
                "billingItemCode": "knowledge",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "knowledge",
                    "parentCode": "guide",
                    "baseAmount": 50000,
                    "dayAmount": 1667,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "sumCounterName": "onlinecontact.knowledge_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "09"
                }
            }, {
                "id": 661,
                "billingId": 214,
                "billingItemCode": "telticket",
                "userCount": 0,
                "active": false,
                "billingItem": {
                    "code": "telticket",
                    "parentCode": "ticket",
                    "baseAmount": 70000,
                    "dayAmount": 2333,
                    "useUserCount": true,
                    "countFree": 6000,
                    "countLevel1": 40000,
                    "countLevel1Unit": 3.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 1.5,
                    "open": true,
                    "licenceCounterName": "onlinecontact.call_licence",
                    "sumCounterName": "onlinecontact.call_seconds",
                    "resourceIdSuffix1": "02",
                    "resourceIdSuffix2": "03"
                }
            }, {
                "id": 662,
                "billingId": 214,
                "billingItemCode": "ticket",
                "userCount": 0,
                "active": true,
                "billingItem": {
                    "code": "ticket",
                    "parentCode": "ticket",
                    "baseAmount": 10000,
                    "dayAmount": 333,
                    "useUserCount": true,
                    "countFree": 3000,
                    "countLevel1": 0,
                    "countLevel1Unit": 50.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": true,
                    "licenceCounterName": "onlinecontact.ticket_licence",
                    "sumCounterName": "onlinecontact.ticket_count",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "01"
                }
            }, {
                "billingItemCode": "ticketevaluation",
                "active": false,
                "billingItem": {
                    "code": "ticketevaluation",
                    "parentCode": "additional",
                    "baseAmount": 100000,
                    "dayAmount": 3333,
                    "useUserCount": false,
                    "countFree": 0,
                    "countLevel1": 0,
                    "countLevel1Unit": 0.0,
                    "countLevel2": 0,
                    "countLevel2Unit": 0.0,
                    "open": false,
                    "sumCounterName": "onlinecontact.ticket.evaluation_days",
                    "resourceIdSuffix1": "",
                    "resourceIdSuffix2": "17"
                }
            }]
        }
    }
}
```
