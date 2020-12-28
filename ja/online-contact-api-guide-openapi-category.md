## Contact Center > Online Contact > プログラマーのためのAPIガイド > カテゴリー管理

### 受付タイプ追加
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/add.json			
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/add.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|受付タイプ追加  |HTTPS  |POST    |UTF-8|JSON    |新規受付タイプ追加|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|受付タイプ情報	|request body	|String	|O	|受付タイプ情報（JSON)|
|	             |name	|String	|O	|受付タイプ名（唯一の値:はい; 長さ:min = 0, max = 50; 形式:^(\_\|-\|[^\\pP])+$）|
|	             |orderNo	|Int	|X	|受付タイプ露出順序（基本値:0）|

#### Request Body
```
{
    "name":"bug",
    "orderNo":1
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|------------|----|---|
|result.content	|categoryId	|Int	|O	|受付タイプID|
|             	|serviceId	|String	|O	|サービスID|
|	              |parent	|Int	|X	|上位受付タイプID（固定値:0）|
|	              |name	|String	|O	|受付タイプ名|
|	              |level	|Int	|X	|段階（固定値:1）|
|	              |path	|String	|X	|段階の経路（固定値:"\\"）|
|	              |orderNo	|Int	|X	|受付タイプ露出順序（基本値:0）|
|	              |createdDt	|Long	|X	|受付タイプ作成時間|
|	              |updatedDt	|Long	|X	|受付タイプアップデート時間|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"bug",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1586830915532,
            "updatedDt":1586830915532
        }
    }
}
```

### 受付タイプ詳細
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json			
- URL (開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|受付タイプ詳細 |HTTPS  |GET    |UTF-8|JSON    |受付タイプIDで受付タイプを照会|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|受付タイプID	|categoryid	|Int	|O	|受付タイプID，URL PATH内に設定した{categoryid}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result.content	|categoryId	|Int	|O	|受付タイプID|
|	              |serviceId	|String	|O	|サービスID|
|	              |parent	|Int	|X	|上位受付タイプID（고정 값:0）|
|	              |name	|String	|O	|受付タイプ名|
|           	  |level	|Int	|X	|段階（固定値:1）|
|	              |path	|String	|X	|段階の経路（固定値:"\\"）|
|	              |orderNo	|Int	|X	|受付タイプ露出順序（基本値:0）|
|	              |createdDt	|Long	|X	|受付タイプ作成時間|
|	              |updatedDt	|Long	|X	|受付の類型アップデート時間|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"bug",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1586830915532,
            "updatedDt":1586830915532
        }
    }
}

```

### 受付タイプ修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|受付タイプ修正  |HTTPS  |PUT    |UTF-8|JSON    |受付タイプIDで受付タイプを修正|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|受付タイプID	|categoryid	|Int	|O	|受付タイプID，URL PATH内に設定した{categoryid}|
|受付タイプ情報	|request body	|String	|O	|受付タイプ情報（JSON）|
|	             |name	|String	|O	|受付タイプ名（唯一の値:はい; 長さ:min = 0, max = 50; 形式:^(\_\|-\|[^\\pP])+$|
|              |orderNo	|Int	|X	|受付タイプ露出順序（基本値:0）|

#### Request Body
```
{
    "name":"bug",
    "orderNo":1
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result.content	|categoryId	|Int	|O	|受付タイプID|
|	              |serviceId	|String	|O	|サービスID|
|	              |name	|String	|O	|受付タイプ名|
|	              |orderNo	|Int	|X	|受付タイプ露出順序（基本値:0）|

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
            "categoryId":1567,
            "serviceId":"GameBaseService",
            "name":"bug",
            "orderNo":1
        }
    }
}
```

### 受付タイプ削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/{categoryid}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|受付タイプ削除  |HTTPS  |DELETE    |UTF-8|JSON    |受付タイプIDで受付タイプを削除|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|受付タイプID	|categoryid	|Int	|O	|受付タイプID，URL PATH内に設定した{categoryid}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result|		|	|X	|null:削除成功|

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

### 受付タイプ一覧
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/category/list.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/category/list.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|受付タイプ一覧 |HTTPS  |GET    |UTF-8|JSON    |サービス内の受付タイプ一覧|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result.contents	|categoryId	|Int	|O	|受付タイプID|
|                 |serviceId	|String	|O	|サービスID|
|	                |parent	|Int	|X	|上位受付タイプID（固定値:0）|
|	                |name	|String	|O	|受付タイプ名|
|	                |level	|Int	|X	|段階（固定値:1）|
|	                |path	|String	|X	|段階経路（固定値:"\\"）|
|	                |orderNo	|Int	|X	|受付タイプ露出順序（基本値:0）|
|	                |createdDt	|Long	|X	|受付タイプ作成時間|
|	                |updatedDt	|Long	|X	|受付タイプアップデート時間|

- リストの順序は　order by orderNo, name asc

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
                "categoryId":1571,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"help",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1586835618000,
                "updatedDt":1586835618000
            },
            {
                "categoryId":1570,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"chat",
                "level":1,
                "path":"\\",
                "orderNo":1,
                "createdDt":1586835599000,
                "updatedDt":1586835599000
            },
            {
                "categoryId":1567,
                "serviceId":"GameBaseService",
                "parent":0,
                "name":"bug",
                "level":1,
                "path":"\\",
                "orderNo":3,
                "createdDt":1586830916000,
                "updatedDt":1586841262000
            }
        ]
    }
}
```
