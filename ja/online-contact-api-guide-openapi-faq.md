## Contact Center > Online Contact > プログラマーのためのAPIガイド > FAQ

### FAQ目録照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc.json			
	
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ目録照会 |HTTPS  |GET    |UTF-8|JSON    |照会条件を基準にFAQリストをリターン|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|サービスID	|serviceId	|Varchar(50)	|O	|サービスID, URL PATH内に設定|
|照会言語	|language	|Varchar(2)	|X	|ko：韓国語, zh：中国語, ja：日本語, en：英語|
|カテゴリーID	|category	|Int	|X	|カテゴリーID|
|推薦	|recommend	|Boolean	|X	|true：推薦，false：推薦ではない|
|上段固定	|top	|Boolean	|X	|true：上段固定，false：上段固定ではない|
|状態	|status	|Varchar(1)	|X	|D：草案, O：公開, C：完了|
|キーワード	|query	|Varchar	|X	|検索文句|
|照会フィールド	|searchField	|Varchar	|X	|基本: 内容+タイトルで検索, title：タイトルだけ検索, content：内容だけ検索|
|整列フィールド	|sort	|Varchar	|X	|isTop, isRecommend, createdDt, updatedDt フィールドを使って 整列基準指定可能. 複数の場合 ','で分離|
|ページ	|page	|Int	|X	|ページ番号，基本は1ページ| 
|ページあたりの件数	|pageSize	|Int	|X	|ページあたりのデータ件数，基本は10件|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|------|---|
|result.contents	|helpDocId	|Long	|O	|FAQ ID|
|                 |serviceId	        |String	|O	|サービスID|
|	                |language	|String	|O	|ko：韓国語, zh：中国語, ja：日本語, en：英語어|
| 	              |status	        |String	|O	|FAQ状態. D：草案, O：公開, C：完了|
|	                |categoryId	|Int	|O	|カテゴリーID|
|	                |categoryName	|String	|O	|カテゴリー名|
|	                |isRecommend	|Boolean	|O	|推薦|
|	                |isTop	        |Boolean	|O	|上段固定|
|	                |title	        |String	|O	|FAQタイトル|
|	                |userId	        |Int	|O	|登録ユーザーID|
|	                |userName	|String	|O	|登録ユーザー名|
|	                |createdDt	|Long	|O	|FAQ登録時間|
|	                |updatedDt	|Long	|O	|FAQ修正時間|

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
        "noticeId": 258,
        "language":"zh"
        "serviceId": "multilanguage",
        "status": "O",
        "categoryId": 509,
        "isRecommend": true,
        "isTop": false,
        "title": "中国語タイトル1",
        "userId": 10063,
        "createdDt": 1547962599000,
        "updatedDt": 1548054677000,
        "userName": "example",
        "categoryName": "中国語カテゴリー１",
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### FAQ詳細照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ詳細照会|HTTPS  |GET    |UTF-8|JSON    |FAQのIDでFAQの詳細を照会|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|FAQ ID	|id	|Long	|O	|URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |title	|String	|O	|FAQタイトル|
|	              |content	|String	|O	|FAQ内容|
| 	            |isRecommend	|Boolean	|O	|推薦|
| 	            |isTop	|Boolean	|O	|上段固定|
| 	            |status	|String	|O	|FAQの状況, D：草案, O：公開, C：完了|
|	              |readCnt	|Int	|O	|閲覧数|
|	              |userId	|Int	|O	|登録ユーザーID|
|	              |username	|String	|O	|登録ユーザー名|
|	              |attachmentYn	|Boolean	|O	|添付ファイルが含まれているかどうか|
|	              |createdDt	|Long	|O	|FAQ登録時間|
|	              |updatedDt	|Long	|O	|FAQ修正時間|
|	              |categories.categoryId	|Int	|O	|カテゴリーID|
|	              |categories.parent	|String	|O	|上位カテゴリーID|
|	              |categories.name	|String	|O	|カテゴリー名|
|	              |categories.level	|String	|O	|カテゴリーの段階（1\|2\|3）|
|	              |contents.{language}.title	|String	|O	|多言語FAQタイトル|
|	              |contents.{language}.content	|String	|O	|多言語FAQ内容|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|多言語添付ファイルID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|多言語添付ファイル名|
|	              |contents.{language}.attachments[].size	|Long	|O	|多言語添付ファイルサイズ|
|	              |attachments[].attachmentId	|String	|O	|添付ファイルID|
|	              |attachments[].fileName	|String	|O	|添付ファイル名|
|	              |attachments[].size	|Long	|O	|添付ファイルサイズ|

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
            "helpDocId":648,
            "language":null,
            "serviceId":"multilanguage",
            "title":"中国語タイトル1",
            "content":"中国語内容1",
            "isRecommend":false,
            "isTop":false,
            "status":"O",
            "readCnt":2,
            "userId":10060,
            "username":"test1",
            "attachmentYn":"Y",
            "createdDt":1584426136000,
            "updatedDt":1584426136000,
            "categories":[
                {
                    "categoryId":1367,
                    "parent":799,
                    "name":"123",
                    "level":3
                }
            ],
            "contents":{
                "ko":{
                    "title":"韓国語タイトル1",
                    "content":"韓国語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "ja":{
                    "title":"日本語タイトル1",
                    "content":"日本語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "zh":{
                    "title":"中国語タイトル1",
                    "content":"中国語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "en":{
                    "title":"英語タイトル1",
                    "content":"英語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                }
            },
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                    "fileName":"file.jpg",
                    "contentType":"application/octet-stream",
                    "size":10645
                }
            ]
        }
    }
}
```

### FAQ登録
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc.json			
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ登録 |HTTPS  |POST    |UTF-8|JSON    |新規FAQ登録|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|request body	|categoryId	|String	|O	|カテゴリーID|
|	        |title	        |String	|O	|FAQタイトル（単一言語：サービス言語）|
|	        |content	|String	|O	|FAQ内容（単一言語：サービス言語）|
|	        |status	        |String	|O	|FAQの状況, D：草案, O：公開, C：完了|
|	        |isRecommend	|Boolean	|O	|推薦の可否. true：推薦, false：推薦ではない|
|	        |isTop	        |Boolean	|O	|上段固定の可否. true：上段固定, false：上段固定ではない|
|	        |contents.{language}.title	|String	|O	|FAQタイトル(多言語)|
| 	        |contents.{language}.content	|String	|O	|FAQ内容(多言語)|
|	        |contents.{language}.attachments[].attachmentId	|Array	|	|添付ファイルID（多言語）|
|	        |attachments[].attachmentId	|String	|   	|添付ファイルID（単一言語）|

#### Request Body
```
単一言語
{
    "title":"中文标题1",
    "content":"中文内容1",
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "attachments":[
        {
            "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
         }
    ]
}

多言語
{
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "contents":{
        "ko":{
            "title":"韓国語タイトル1",
            "content":"韓国語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "ja":{
            "title":"日本語タイトル1",
            "content":"日本語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "zh":{
            "title":"中国語タイトル1",
            "content":"中国語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "en":{
            "title":"英語タイトル1",
            "content":"英語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        }
    }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|---------|-----------|---------|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |title	|String	|O	|FAQタイトル|
|	              |content	|String	|O	|FAQ内容|
| 	            |isRecommend	|Boolean	|O	|推薦の可否. true：推薦, false：推薦ではない|
| 	            |isTop	|Boolean	|O	|上段固定の可否. true：上段固定, false：上段固定ではない|
| 	            |status	|String	|O	|FAQの状況, D：草案, O：公開, C：完了|
|	              |readCnt	|Int	|O	|閲覧数|
|	              |userId	|Int	|O	|登録ユーザーID|
|	              |username	|String	|O	|登録ユーザー名|
|	              |attachmentYn	|Boolean	|O	|添付ファイルが含まれているかどうか|
|	              |createdDt	|Long	|O	|FAQ登録時間|
|	              |updatedDt	|Long	|O	|FAQ修正時間|
|	              |categories.categoryId	|Int	|O	|カテゴリーID|
|	              |categories.parent	|String	|O	|上位カテゴリーID|
|	              |categories.name	|String	|O	|カテゴリー名|
|	              |categories.level	|String	|O	|カテゴリーの段階（1\|2\|3）|
|	              |contents.{language}.title	|String	|O	|多言語FAQタイトル|
|	              |contents.{language}.content	|String	|O	|多言語FAQ内容|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|多言語添付ファイルID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|多言語添付ファイル名|
|	              |contents.{language}.attachments[].size	|Long	|O	|多言語添付ファイルサイズ|
|	              |attachments[].attachmentId	|String	|O	|添付ファイルID|
|	              |attachments[].fileName	|String	|O	|添付ファイル名|
|	              |attachments[].size	|Long	|O	|添付ファイルサイズ|

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
            "helpDocId":648,
            "language":null,
            "serviceId":"multilanguage",
            "title":"中国語タイトル1",
            "content":"中国語内容1",
            "isRecommend":false,
            "isTop":false,
            "status":"O",
            "readCnt":2,
            "userId":10060,
            "username":"test1",
            "attachmentYn":"Y",
            "createdDt":1584426136000,
            "updatedDt":1584426136000,
            "categories":[
                {
                    "categoryId":1367,
                    "parent":799,
                    "name":"123",
                    "level":3
                }
            ],
            "contents":{
                "ko":{
                    "title":"韓国語タイトル1",
                    "content":"韓国語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "ja":{
                    "title":"日本語タイトル1",
                    "content":"日本語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "zh":{
                    "title":"中国語タイトル1",
                    "content":"中国語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "en":{
                    "title":"英語タイトル1",
                    "content":"英語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                }
            },
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                    "fileName":"file.jpg",
                    "contentType":"application/octet-stream",
                    "size":10645
                }
            ]
        }
    }
}
```

### FAQ修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json					
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ修正|HTTPS  |PUT    |UTF-8|JSON    |FAQ ID基準に内容修正|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|FAQ ID	   |helpDocId	   |Long	|O	|URL PATH内に設定した{id}|
|request body	|categoryId	|String	|O	|カテゴリーID|
|	        |title	        |String	|O	|FAQタイトル（単一言語：サービス言語）|
|	        |content	|String	|O	|FAQ内容（単一言語：サービス言語）|
|	        |status	        |String	|O	|FAQの状況, D：草案, O：公開, C：完了|
|	        |isRecommend	|Boolean	|O	|推薦の可否. true：推薦, false：推薦ではない|
|	        |isTop	        |Boolean	|O	|上段固定の可否. true：上段固定, false：上段固定ではない|
|	        |contents.{language}.title	|String	|O	|FAQタイトル(多言語)|
| 	        |contents.{language}.content	|String	|O	|FAQ内容(多言語)|
|	        |contents.{language}.attachments[].attachmentId	|Array	|	|添付ファイルID（多言語）|
|	        |attachments[].attachmentId	|String	|   	|添付ファイルID（単一言語）|


#### Request Body
```
単一言語
{
    "title":"中文标题1",
    "content":"中文内容1",
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "attachments":[
        {
            "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
         }
    ]
}

多言語
{
    "status":"O",
    "categoryId":1367,
    "isTop":false,
    "isRecommend":false,
    "contents":{
        "ko":{
            "title":"韓国語タイトル1",
            "content":"韓国語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "ja":{
            "title":"日本語タイトル1",
            "content":"日本語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "zh":{
            "title":"中国語タイトル1",
            "content":"中国語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        },
        "en":{
            "title":"英語タイトル1",
            "content":"英語内容1",
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a"
                }
            ]
        }
    }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|------------|---------|----|
|result.content	|helpDocId	|Long	|O	|FAQ ID|
|	              |serviceId	|String	|O	|サービスID|
|	              |title	|String	|O	|FAQタイトル|
|	              |content	|String	|O	|FAQ内容|
| 	            |isRecommend	|Boolean	|O	|推薦の可否. true：推薦, false：推薦ではない|
| 	            |isTop	|Boolean	|O	|上段固定の可否. true：上段固定, false：上段固定ではない|
| 	            |status	|String	|O	|FAQの状況, D：草案, O：公開, C：完了|
|	              |readCnt	|Int	|O	|閲覧数|
|	              |userId	|Int	|O	|登録ユーザーID|
|	              |username	|String	|O	|登録ユーザー名|
|	              |attachmentYn	|Boolean	|O	|添付ファイルが含まれているかどうか|
|	              |createdDt	|Long	|O	|FAQ登録時間|
|	              |updatedDt	|Long	|O	|FAQ修正時間|
|	              |categories.categoryId	|Int	|O	|カテゴリーID|
|	              |categories.parent	|String	|O	|上位カテゴリーID|
|	              |categories.name	|String	|O	|カテゴリー名|
|	              |categories.level	|String	|O	|カテゴリーの段階（1\|2\|3）|
|	              |contents.{language}.title	|String	|O	|多言語FAQタイトル|
|	              |contents.{language}.content	|String	|O	|多言語FAQ内容|
|	              |contents.{language}.attachments[].attachmentId	|String	|O	|多言語添付ファイルID|
|	              |contents.{language}.attachments[].fileName	|String	|O	|多言語添付ファイル名|
|	              |contents.{language}.attachments[].size	|Long	|O	|多言語添付ファイルサイズ|
|	              |attachments[].attachmentId	|String	|O	|添付ファイルID|
|	              |attachments[].fileName	|String	|O	|添付ファイル名|
|	              |attachments[].size	|Long	|O	|添付ファイルサイズ|

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
            "helpDocId":648,
            "language":null,
            "serviceId":"multilanguage",
            "title":"中国語タイトル1",
            "content":"中国語内容1",
            "isRecommend":false,
            "isTop":false,
            "status":"O",
            "readCnt":2,
            "userId":10060,
            "username":"test1",
            "attachmentYn":"Y",
            "createdDt":1584426136000,
            "updatedDt":1584426136000,
            "categories":[
                {
                    "categoryId":1367,
                    "parent":799,
                    "name":"123",
                    "level":3
                }
            ],
            "contents":{
                "ko":{
                    "title":"韓国語タイトル1",
                    "content":"韓国語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "ja":{
                    "title":"日本語タイトル1",
                    "content":"日本語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "zh":{
                    "title":"中国語タイトル1",
                    "content":"中国語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                },
                "en":{
                    "title":"英語タイトル1",
                    "content":"英語内容1",
                    "attachments":[
                        {
                            "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                            "fileName":"file.jpg",
                            "contentType":"application/octet-stream",
                            "size":10645
                        }
                    ]
                }
            },
            "attachments":[
                {
                    "attachmentId":"e981516df5da4b1cbf25af403b3a622a",
                    "fileName":"file.jpg",
                    "contentType":"application/octet-stream",
                    "size":10645
                }
            ]
        }
    }
}
```

### FAQカテゴリー別固定設定
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/recommend.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/recommend.json	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQカテゴリー別固定設定|HTTPS  |PUT    |UTF-8|JSON    |FAQ文書が属するカテゴリーの上段に固定されるように設定|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|FAQ ID	|Id	          |Int	|O	|URL PATH内に設定した{id}|
|推薦	|recommend	|Boolean	|O	|推薦の可否. true：推薦, false：推薦ではない|

#### 結果データ
-　なし

### FAQメイン画面固定設定
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/top.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/top.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQメイン画面固定設定|HTTPS  |PUT    |UTF-8|JSON    |FAQ文書がメイン画面上段に固定されるように設定|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|FAQ ID	   |Id	|Int	|O	|URL PATH内に設定した{id}|
|上段固定	|top	|Boolean	|O	|上段固定の可否. true：上段固定, false：上段固定ではない|

#### 結果データ
-　なし

### FAQ完了処理
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/close.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}/close.json		

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ完了処理 |HTTPS  |PUT    |UTF-8|JSON    |FAQステータスを完了に変更 (status = C)|共通認証   |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|FAQ ID	   |Id	           |Int	   |O	   |URL PATH内に設定した{id}|

#### 結果データ
-　なし

### FAQ削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json					
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ削除 |HTTPS  |DELETE    |UTF-8|JSON    |FAQ　ID基準でFAQ削除|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|FAQ ID	   |Id	           |Int	   |O	   |URL PATH内に設定した{id}|


#### 結果データ
-　なし

### FAQカテゴリーリスト照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/helpdoc/categories.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/categories.json	
			
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQカテゴリーリスト照会 |HTTPS  |GET    |UTF-8|JSON    |FAQカテゴリーリスト照会|共通認証   |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	  |String	|O	|URL PATH내에 설정한{serviceId}|
|下位カテゴリーID	|child	|Int	|X	|上位カテゴリー取得時、伝送する下位カテゴリーID| 
|上位カテゴリーID	|parent	|Int	|X	|下位カテゴリー取得時、伝送する上位カテゴリーID|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|---------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|カテゴリーID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|X	|カテゴリーCode|
|	                |parent	        |Int	|X	|上位カテゴリーID（基本値:0）|
|	                |name	        |String	|O	|カテゴリー名|
|	                |level	        |Int	|X	|段階（1\|2\|3）|
|	                |path	        |String	|X	|段階経路（\level1\level2\"）|
|	                |orderNo	|Int	|X	|整列順序（기본 값:0）|
|	                |createdDt	|Long	|X	|登録時間|
|	                |updatedDt	|Long	|X	|修正時間|
|	                |languages	|String	|X	|多言語|

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
                "categoryId":999,
                "serviceId":"multilanguage",
                "categoryCode":"game",
                "parent":0,
                "name":"韓国語カテゴリー2",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1554949320000,
                "updatedDt":1554949320000,
                "languages":{
                    "ko":"韓国語カテゴリー2"
                }
            },
            {
                "categoryId":509,
                "serviceId":"multilanguage",
                "categoryCode":"code1",
                "parent":0,
                "name":"中国語カテゴリー1",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1547949603000,
                "updatedDt":1554887489000,
                "languages":{
                    "ko":"韓国語カテゴリー1",
                    "ja":"日本語カテゴリー1",
                    "en":"英語カテゴリー1",
                    "zh":"中国語カテゴリー1"
                }
            }
        ]
    }
}
```

### FAQカテゴリー詳細照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/helpdoc/category/{id}.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json
						
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQカテゴリー詳細照会 |HTTPS  |GET    |UTF-8|JSON    |カテゴリーIDでFAQカテゴリーの詳細を照会|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|カテゴリーIDあるいはカテゴリーコード	|id	|String	|O	|URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|------------|---------|----|
|result.contents	|categoryId	|Int	|O	|カテゴリーID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|X	|カテゴリーCode|
|	                |parent	        |Int	|X	|上位カテゴリーID（基本値:0）|
|	                |name	        |String	|O	|カテゴリー名|
|	                |level	        |Int	|X	|段階（1\|2\|3）|
|	                |path	        |String	|X	|段階経路（\level1\level2\"）|
|	                |orderNo	|Int	|X	|整列順序（기본 값:0）|
|	                |createdDt	|Long	|X	|登録時間|
|	                |updatedDt	|Long	|X	|修正時間|
|	                |languages	|String	|X	|多言語|

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
            "categoryId":509,
            "serviceId":"multilanguage",
            "categoryCode":"code1",
            "parent":0,
            "name":"中国語カテゴリー1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"韓国語カテゴリー1",
                "ja":"日本語カテゴリー1",
                "en":"英語カテゴリー1",
                "zh":"中国語カテゴリー1"
            }
        }
    }
}
```

### FAQカテゴリー追加
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category.json
							
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQカテゴリー追加 |HTTPS  |POST    |UTF-8|JSON    |新規FAQカテゴリー追加|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|カテゴリー情報	|request body	|String	    |O	|カテゴリー情報（JSON）|
|	             |name	     |String     |		|カテゴリー名（唯一の値:はい ; 長さ:min = 0, max = 50 ; 形式:^(\_\|-\|[^\\pP])+$）|
|	              |categoryCode	|String	 |	|カテゴリーCode|
|	              |languages	|String	 |	|多言語|
|	              |parent	        |Int	 |	|上位カテゴリーID（基本値:0）|
|	              |orderNo	        |Int	 |	|整列順序（基本値:0）|

#### Request Body
```
単一言語
{
    "name":"中国語カテゴリー3",
    "categoryCode":"game3",
    "orderNo":1,
    "parent":0
}

多言語
{
    "categoryCode":"game3",
    "parent":0,
    "orderNo":1,
    "languages":{
        "ko":"韓国語カテゴリー3",
        "ja":"日本語カテゴリー3",
        "en":"英語カテゴリー3",
        "zh":"中国語カテゴリー3"
    }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|result.contents	|categoryId	|Int	|O	|カテゴリーID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|X	|カテゴリーCode|
|	                |parent	        |Int	|X	|上位カテゴリーID（基本値:0）|
|	                |name	        |String	|O	|カテゴリー名|
|	                |level	        |Int	|X	|段階（1\|2\|3）|
|	                |path	        |String	|X	|段階経路（\level1\level2\"）|
|	                |orderNo	|Int	|X	|整列順序（기본 값:0）|
|	                |createdDt	|Long	|X	|登録時間|
|	                |updatedDt	|Long	|X	|修正時間|
|	                |languages	|String	|X	|多言語|

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
            "categoryId":509,
            "serviceId":"multilanguage",
            "categoryCode":"code1",
            "parent":0,
            "name":"中国語カテゴリー1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"韓国語カテゴリー1",
                "ja":"日本語カテゴリー1",
                "en":"英語カテゴリー1",
                "zh":"中国語カテゴリー1"
            }
        }
    }
}
```

### FAQカテゴリー修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
									
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQカテゴリー修正 |HTTPS  |PUT    |UTF-8|JSON    |ID基準でカテゴリー名を修正|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|カテゴリーIDあるいはカテゴリーコード	|Id	|String	|O	|URL PATH内に設定した{id}|
|カテゴリー情報	|request body	|String	    |O	|カテゴリー情報（JSON）|
|	             |name	     |String     |		|カテゴリー名（唯一の値:はい ; 長さ:min = 0, max = 50 ; 形式:^(\_\|-\|[^\\pP])+$）|
|	              |categoryCode	|String	 |	|カテゴリーCode|
|	              |languages	|String	 |	|多言語|
|	              |parent	        |Int	 |	|上位カテゴリーID（基本値:0）|
|	              |orderNo	        |Int	 |	|整列順序（基本値:0）|

#### Request Body
```
単一言語
{
    "name":"中国語カテゴリー3",
    "categoryCode":"game3",
    "orderNo":1,
    "parent":0
}

多言語
{
    "categoryCode":"game3",
    "parent":0,
    "orderNo":1,
    "languages":{
        "ko":"韓国語カテゴリー3",
        "ja":"日本語カテゴリー3",
        "en":"英語カテゴリー3",
        "zh":"中国語カテゴリー3"
    }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|---------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|カテゴリーID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|X	|カテゴリーCode|
|	                |parent	        |Int	|X	|上位カテゴリーID（基本値:0）|
|	                |name	        |String	|O	|カテゴリー名|
|	                |level	        |Int	|X	|段階（1\|2\|3）|
|	                |path	        |String	|X	|段階経路（\level1\level2\"）|
|	                |orderNo	|Int	|X	|整列順序（기본 값:0）|
|	                |createdDt	|Long	|X	|登録時間|
|	                |updatedDt	|Long	|X	|修正時間|
|	                |languages	|String	|X	|多言語|

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
            "categoryId":1576,
            "serviceId":"GameBaseService",
            "parent":0,
            "name":"韓国語カテゴリー",
            "level":1,
            "path":"\",
            "orderNo":1,
            "createdDt":1587349288181,
            "updatedDt":1587349288181,
            "languages":{
                "ko":"韓国語カテゴリー",
                "ja":"日本語カテゴリー",
                "zh":"中国語カテゴリー",
                "en":"英語カテゴリー"
            }
        }
    }
}
```

### FAQカテゴリー削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/helpdoc/category/{id}.json	
									
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQカテゴリー削除 |HTTPS/80  |DELETE    |UTF-8|JSON    |カテゴリーIDでFAQカテゴリーを削除|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|カテゴリーIDあるいはカテゴリーコード	|id	|String	|O	|URL PATH内に設定した{id}|

#### 結果データ
- なし

### FAQ添付ファイル添付
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/help/upload.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/help/upload.json	
									
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ添付ファイル添付|HTTPS  |POST    |UTF-8|JSON    |サーバーへのファイルアップロード|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|アップロードしたファイル	|file	|File	|O	|アップロードしたファイルをformで提出|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|------------|--------|-----|
|result.content	|attachmentId	|String	|O	|添付ファイルID|
|	        |fileName	|String	|O	|ファイル名|
|	        |contentType	|String	|O	|ファイルタイプ|
|	        |size 	        |Long	|O	|ファイルサイズ|

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
            "attachmentId":"b891809a58b94ce3a09c080b81d0d14c",
            "fileName":"file2.jpg",
            "contentType":"image/jpeg",
            "size":13855
        }
    }
}
```

### FAQ添付ファイルを開く／ダウンロード
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/attachments/help/{id}	
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/attachments/help/{id}
									
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ添付ファイルを開く／ダウンロード |HTTPS  |GET    |UTF-8|FILE    |サーバーにアップロードしたFAQ添付ファイルを開く／ダウンロード|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	          |serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|ファイルID	|id	      |String  |O     |アップロードしたファイルid| 
|閲覧方式	         |type	       |String	       |基本: 開く（download:ダウンロード,　open:開く）|

#### 結果データ
- なし

#### Response Body
- File

### FAQ添付ファイル削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/help/{id}.json				
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/help/{id}.json	
									
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ添付ファイル削除 |HTTPS  |DELETE    |UTF-8|JSON    |サーバーにアップロードしたファイル削除|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|------|-----------|----|----|
|サービスID	          |serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|ファイルID	|id	      |String  |O     |アップロードしたファイルid| 

#### 結果データ
- なし


