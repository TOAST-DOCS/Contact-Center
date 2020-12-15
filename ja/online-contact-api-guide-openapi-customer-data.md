## Contact Center > Online Contact > プログラマーのためのAPIガイド > 顧客情報連動

**電話でのお問い合わせ**があった時、当該媒体番号に該当する**顧客会社側の顧客データをAPIを通じて照会**して取り込めるように提供する機能です。

Request URL: 顧客社のAPI URL
Response Type: JSON

### リクエストパラメータ定義
|番号|変数|必須|データタイプ|説明|
|----|----|----|---------|----|
|1   |telNo|O  |String   |引き込まれたコールの媒体番号|

### 結果データ
|番号|変数|データタイプ|説明|
|----|---|-----------|---|
|1   |resultCode|String|成功:0, 失敗:other|
|2   |resultMsg |String|結果メッセージ|
|3   |resultData|Map   |結果マップ|

### resultData パラメータ
|番号|変数|データタイプ|説明|
|----|---|-----------|---|
|1  |custId|String   |   |
|2  |custName|String |   |
|...|...     |...    |...|

### Response Body
```
{
   "resultData":{
      "custId": "test",
      "custName": "テスト",
      ..
      ..
   },
   "resultCode": "0",
   "resultMsg": "success"
}
```

resultData変数内のデータは、顧客企業側が希望する通りに設定でき、**APIを通してリターンする全てのデータが画面に表示**されます。

もし、resultData内の変数がOnlineContactチケットフィールドに追加されているなら、その変数の**変数名**と[フィールドの**項目コード値**](https://docs.toast.com/ko/Contact%20Center/ko/online-contact-guide-service-management#_22)が**一致してこそ**、適切なマッピングが可能です。
