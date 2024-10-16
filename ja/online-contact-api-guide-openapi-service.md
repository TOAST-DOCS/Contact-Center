## Contact Center > Online Contact > プログラマーのためのAPIガイド > サービス 

### サービス詳細
#### インターフェース説明
- URL: https://{domain}.oc.nhncloud.com/{serviceId}/api/v2/service.json
- URL(開発): https://{domain}.oc.alpha-nhncloud.com/{serviceId}/api/v2/service.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|サービス詳細  |HTTPS  |GET    |UTF-8|JSON    |サービスIDを通じてサービス情報を照会|必要なし|

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	|String	|path  |O	|サービスID，URL PATH内に設定した{serviceId}|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|serviceId	    |String		|サービス ID|
|	            |name	        |String		|サービス名|
|	            |profile	    |String		|サービス背景イメージ|
|	            |language	    |String		|サービス基本言語コード|
|	            |languages	    |Array		|サービス言語リスト|
|	            |languages.code	|String		|言語コード|
|	            |languages.name	|String		|言語名称|
|	            |languages.orderNo	|Integer		|言語露出順序|
|	            |multiLanguage	|Boolean		|多言語であるかどうか, 値(true: 多言語, false: 単一言語)|

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
            "serviceId": "APISample",
            "name": "APISample",
            "profile": {
                "fileUrl": "https://api-storage.cloud.toast.com/v1/AUTH_226f908c769e48b0bad7d32f9a91717f/service_alpha/WopqM8euoYw89B7i/27316eba2a8a4089b72a9cf18a83e144.png"
            },
            "language": "ko",
            "languages": [
                {
                    "code": "ko",
                    "name": "한국어",
                    "orderNo": 0
                },
                {
                    "code": "ja",
                    "name": "日本語",
                    "orderNo": 1
                },
                {
                    "code": "en",
                    "name": "English",
                    "orderNo": 2
                },
                {
                    "code": "zh",
                    "name": "中文",
                    "orderNo": 3
                },
                {
                    "code": "th",
                    "name": "ไทย",
                    "orderNo": 4
                }
            ],
            "multiLanguage": true
        }
    }
}
```