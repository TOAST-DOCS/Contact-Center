## Contact Center > Online Contact > プログラマーのためのAPIガイド > ヘルプセンター
### ヘルプセンター指定データ追加
#### インターフェース説明
- URL:	https://{domain}.oc.toast.com/{serviceId}/hc/openapi/v1/addition.json			
- URL (開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/hc/openapi/v1/addition.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|ヘルプセンターに指定データ追加|HTTPS  |POST    |UTF-8|JSON    |追加的に必要な顧客情報をDBに保存|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|	         |content	|String	|O	|追加顧客情報|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|----|----|
|result.content	|additionId	|String	|O	|生成されたID|

#### Response Body
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": ef1bd956
  }
}
```
