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
|追加顧客情報	         |content	|String	|O	|追加顧客情報。request bodyの形式に伝送。token作成時、エンコード不要|
|露出の可否	          |visible  |int	  |X	|お問い合わせ内容に露出の可否 1：露出, 0：露出しない, 基本: 0|

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
    "content": "ef1bd9560xxxxx"      // 該当値は　additionId。お問い合わせページ呼び出し時、該当値をパラメータ - additionId値に指定
  }
}
```

#### お問い合わせページURLの例
https://nhn-cs.alpha-oc.toast.com/hangame/hc/ticket/?additionId=ef1bd9560xxxxx
