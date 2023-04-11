## Contact Center > Online Contact > プログラマーのためのAPIガイド > オペレーター管理

### オペレーター一覧
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/users.json
- URL(開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/users.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|オペレーター一覧|HTTPS  |GET    |UTF-8|JSON    |オペレーター一覧|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|ユーザー権限	|role	|String	|X	|ROLE_FRONT_ADMIN : 管理者, ROLE_FRONT_AGENT : オペレーター|
|ユーザー名	|name	|String	|X	|ユーザー名|
|ページ数	|page	|Int	|X	|基本値 = 1|
|ページあたりの露出件数	|pageSize	|Int	|X	|基本値 = 10|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|----|----|
|result.contents	|userId	|I	|O	|ユーザーID|
|	                |usercode	|String	|O	|ユーザーCode|
|	                |uuid	|String	|O	|IAM |ユーザーID|
|	                |username	|String	|O	|ユーザー名|
|	                |role	|String	|O	|ユーザー権限. ROLE_FRONT_ADMIN : 管理者, ROLE_FRONT_AGENT : オペレーター|

#### Response Body
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "contents": [
      {
        "userId": 10058,
        "usercode": "example",
        "username": "example",
        "uuid": "ef1bd956-6c13-4391-8256-1eb0d840355a",
        "role": "ROLE_FRONT_ADMIN",
      }
    ]
  }
}
```

### オペレーター情報取得
#### インターフェース説明
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/users/{id}.json			
- URL(開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/users/{id}.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|オペレーター情報取得|HTTPS  |GET    |UTF-8|JSON    |ユーザーIDを通じてオペレーター情報取得|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|ユーザーID	|id	        |Int	|O	|URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result.content	|userId	|Int	|O	|ユーザーID|
|	                |usercode	|String	|O	|ユーザーCode|
|	                |uuid	|String	|O	|IAMユーザーID|
|	                |username	|String	|O	|ユーザー名|
|	                |role	|String	|O	|ユーザー権限. ROLE_FRONT_ADMIN : 管理者, ROLE_FRONT_AGENT : オペレーター|

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
        "userId": 10058,
        "usercode": "example",
        "username": "example",
        ""uuid"": ""ef1bd956-6c13-4391-8256-1eb0d840355a"",
        "role": "ROLE_FRONT_ADMIN",
      }
    }
  }
}
```

### オペレーター追加
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/adduser.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/adduser.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|オペレーター追加|HTTPS  |POST    |UTF-8|JSON    |指定したサービスにオペレーターの追加、権限付与|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|	         |id	       |String	|O	|IAMユーザーUUID|
|	         |role	     |String	|O	|ユーザー権限. ROLE_FRONT_ADMIN : 管理者, ROLE_FRONT_AGENT : オペレーター|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|------|---|
|result.content	|userId	|Int	|O	|ユーザーID|
|	                |usercode	|String	|O	|ユーザーCode|
|	                |uuid	|String	|O	|IAMユーザーID|
|	                |username	|String	|O	|ユーザー名|
|	                |role	|String	|O	|ユーザー権限. ROLE_FRONT_ADMIN : 管理者, ROLE_FRONT_AGENT : オペレーター|

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
        "userId": 10058,
        "usercode": "example",
        "username": "example",
        "uuid": "ef1bd956-6c13-4391-8256-1eb0d840355a",
        "role": "ROLE_FRONT_ADMIN",
    }
  }
}
```

### オペレーター権限変更
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/users/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/users/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|オペレーター権限変更|HTTPS  |PUT    |UTF-8|JSON    |サービス内のオペレーター権限変更|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|ユーザーID	|id	|String	|O	|URL PATH内に設定した{id}|
|ユーザー権限	|role	|String	|O	|ROLE_FRONT_ADMIN : 管理者, ROLE_FRONT_AGENT：オペレーター|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|----|
|result.contents	|userId	|Int	|O	|ユーザーID|
|	                |usercode	|String	|O	|ユーザーCode|
|	                |uuid	|String	|O	|IAMユーザーID|
|	                |username	|String	|O	|ユーザー名|
|	                |role	|String	|O	|ユーザー権限. ROLE_FRONT_ADMIN : 管理者, ROLE_FRONT_AGENT : オペレーター|

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
        "userId": 10058,
        "usercode": "example",
        "username": "example",
        "uuid": "ef1bd956-6c13-4391-8256-1eb0d840355a",
        "role": "ROLE_FRONT_ADMIN",
    }
  }
}
```

### オペレーター削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/users/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/users/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|オペレーター削除|HTTPS/80  |IN(DELETE)    |UTF-8|JSON    |指定したサービスでオペレーター削除|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|ユーザーID	|id	|Int	|O	|URL PATH内に設定した{id}|

#### 結果データ
- なし