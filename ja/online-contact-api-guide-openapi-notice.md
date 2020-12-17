## Contact Center > Online Contact > API ガイド > お知らせ

### お知らせリスト照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせリスト照会  |HTTPS  |GET    |UTF-8|JSON    |お知らせの内容照会、検索条件によってお知らせリストをリターン|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	|Varchar(50)	|O	|サービスID, URL PATH内に設定|
|照会言語|language	|Varchar(2)	|X	|ko：韓国語, zh：中国語, ja：日本語, en：英語|
|日付照会フィールド	|dateField	|Varchar(20)	|X	|startDt：お知らせ期間開始日検索, endDt：お知らせ期間終了日検索, startAndEnd：お知らせ期間開始日 &　お知らせ期間終了日検索, createdDt：登録日検索|
|期間検索開始時間	|termStart	|Varchar(14)	|X	|お知らせ期間開始日（yyyyMMddHHmmss）|
|期間検索終了時間	|termEnd	|Varchar(14)	|X	|お知らせ期間終了日（yyyyMMddHHmmss）|
|登録日開始時間	|startDt	|Varchar(14)	|X	|登録日（yyyyMMddHHmmss）|
|登録日終了時間	|endDt	        |Varchar(14)	|X	|登録日（yyyyMMddHHmmss）|
|テーマID	|categoryId	            |Int	|X	|テーマID|
|タグ	|tag	                    |Int	|X	|タグID，IDが多数の場合' , 'で分離|
|ユーザーID	|userId	                    |Int	|X	|ユーザーID|
|上段固定	|top	|Boolean	|X	|true：上段固定，false：上段固定ではない|
|有効期間	|term	|Varchar(20)	|X	|reservation：予約中, open：進行中, close：完了|
|状態	|status	|Varchar(1)	|X	|D：草案, O：公開, C：完了|
|キーワード	|keyword	|Varchar	|X	|検索文句|
|照会フィールド	|searchField	|Varchar	|X	|基本: 内容+タイトルで検索, title：タイトルのみ検索, content：内容のみ検索|
|整列フィールド	|sort	|Varchar	|X	|右側のフィールドを使用して整列基準を指定可能. 数の場合' , 'で分離. isTop, createdDt, updatedDt, displayDt
|ページ	|page	|Int	|X	|ページ番号，基本は1ページ| 
|ページあたりの件数	|pageSize	|Int	|X	|ページあたりのデータ件数，基本は10件|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|-----------|-----|---|
|result.contents	|noticeId	|Int	|O	|お知らせID|
|	                |serviceId	|String	|O	|サービスID|
|	                |language	|String	|O	|ko：韓国語, zh：中国語, ja：日本語, en：英語|
|	                |status	|String	|O	|お知らせ状態 {D：草案, O：公開, C：完了}|
|	                |isTop	|Boolean	|O	|上段固定表記|
|	                |term	|String	|O	|reservation：予約中, open：進行中, close：完了|
|	                |title	|String	|O	|お知らせタイトル|
|	                |startDt	|String	|O	|開始時間（yyyyMMddHHmmss)|
|	                |endDt	|String	|O	|終了時間（yyyyMMddHHmmss)|
| 	              |displayDt	|String	|X	|出力時間（yyyyMMddHHmmss）|
|                 |userId	|Int	|O	|登録ユーザーID|
|                 |userName	|String	|O	|登録ユーザー名|
|result.contents.tags	|tags[].tagId	|Int	|O	|タグID|
|	                    |tags[].tag	|String	|O	|タグ名|
| 	                  |createdDt	|Long	|O	|お知らせ登録時間|
|	                    |updatedDt	|Long	|O	|お知らせ修正時間|

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
        "isTop": false,
        "term": "open",
        "title": "中国語タイトル1",
        "startDt": "20190101000000",
        "endDt": "20990101000000",
        "displayDt": "20190120000000",
        "readCnt": 0,
        "userId": 10063,
        "createdDt": 1547962599000,
        "updatedDt": 1548054677000,
        "tags": [
          {
            "tagId": 94,
            "tag": "中国語タグ1"
          }
        ],
        "userName": "example",
        "categoryName": "中国語テーマ",
        "category": {
          "categoryId": 509,
          "name": "中国語テーマ",
          "names": {
            "ko": "韓国語テーマ",
            "ja": "日本語テーマ",
            "zh": "中国語テーマ"
          }
        }
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### お知らせ詳細照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json	
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせ詳細照会|HTTPS  |GET    |UTF-8|JSON    |お知らせIDでお知らせ詳細を照会|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|Varchar(50)	|O	|URL PATH内に設定した{serviceId}|
|お知らせID	|id	|Int	|O	|URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|----|----|
|result.contents	|noticeId	|Int	|O	|お知らせID|
|	                |serviceId	|String	|O	|サービスID|
|	                |status	|String	|O	|お知らせ状態 {D：草案, O：公開, C：完了}|
|	                |categoryId	|Int	|O	|テーマID|
|	                |isTop	|Boolean	|O	|上段固定表記|
|	                |term	|String	|O	|reservation：予約中, open：進行中, close：完了|
|	                |startDt	|String	|O	|開始時間（yyyyMMddHHmmss）|
|	                |endDt	|String	|O	|終了時間（yyyyMMddHHmmss）|
|	                |displayDt	|String	|X	|出力時間（yyyyMMddHHmmss）|
|	                |userId	|Int	|O	|登録ユーザーID| 
|result.content.contents	|{language}.title	|String	|O	|お知らせタイトル|
|	                        |{language}.content	|String	|O	|お知らせ内容|
|	                        |{language}.attachments[].attachmentId	|String	|O	|添付ファイルID|
|	                        |{language}.attachments[].fileName	|String	|O	|ファイル名|
|	                        |{language}.attachments[].size	|Long	|O	|ファイルサイズ|
|result.content.tags	|tags[].tagId	|Int	|O	|タグID|
|	                    |tags[].names.{language}	|String	|O	|タグ|
|result.content.category	|categoryId	|Int	|X	|テーマID|
|	                        |names	|String	|O	|多言語テーマ名|
| 	                  |createdDt	|Long	|O	|お知らせ登録時間|
|	                    |updatedDt	|Long	|O	|お知らせ修正時間|

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
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "中国語タイトル1",
      "content": "中国語内容1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "韓国語タグ1",
            "ja": "日本語タグ1",
            "zh": "中国語タグ1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "韓国語テーマ",
          "ja": "日本語テーマ",
          "zh": "中国語テーマ"
        }
      }
    }
  }
}
```

### お知らせ詳細照会(複数件)
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notices.json			 	
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notices.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせ詳細照会(複数件) |HTTPS  |GET    |UTF-8|JSON    |複数のお知らせIDでお知らせ詳細を照会|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|Varchar(50)	|O	|URL PATH内に設定した{serviceId}|
|お知らせID	|id	|String	|O	|お知らせID，多数の場合' , 'で分離|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|お知らせID|
|	                |serviceId	|String	|O	|サービスID|
|	                |status	|String	|O	|お知らせ状態 {D：草案, O：公開, C：完了}|
|	                |categoryId	|Int	|O	|テーマID|
|	                |isTop	|Boolean	|O	|上段固定表記|
|	                |term	|String	|O	|reservation：予約中, open：進行中, close：完了|
|	                |startDt	|String	|O	|開始時間（yyyyMMddHHmmss）|
|	                |endDt	|String	|O	|終了時間（yyyyMMddHHmmss）|
|	                |displayDt	|String	|X	|出力時間（yyyyMMddHHmmss）|
|	                |userId	|Int	|O	|登録ユーザーID| 
|result.contents.contents	|{language}.title	|String	|O	|お知らせタイトル|
|	                        |{language}.content	|String	|O	|お知らせ内容|
|	                        |{language}.attachments[].attachmentId	|String	|O	|添付ファイルID|
|	                        |{language}.attachments[].fileName	|String	|O	|ファイル名|
|	                        |{language}.attachments[].size	|Long	|O	|ファイルサイズ|
|result.contents.tags	|tags[].tagId	|Int	|O	|タグID|
|	                    |tags[].names.{language}	|String	|O	|タグ|
|result.contents.category	|categoryId	|Int	|X	|テーマID|
|	                        |names	|String	|O	|多言語テーマ名|
| 	                  |createdDt	|Long	|O	|お知らせ登録時間|
|	                    |updatedDt	|Long	|O	|お知らせ修正時間|

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
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "中国語タイトル1",
      "content": "中国語内容1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "韓国語タグ1",
            "ja": "日本語タグ1",
            "zh": "中国語タグ1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "韓国語テーマ",
          "ja": "日本語テーマ",
          "zh": "中国語テーマ"
        }
      }
    }
  }]
}
```

### お知らせ登録
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせ登録|HTTPS  |POST    |UTF-8|JSON    |新規お知らせ登録|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|お知らせ内容	|request body	|String	|O	|お知らせ内容（JSON）|
|	             |status	     |String	|O	|お知らせ状態 {D：草案, O：公開, C：完了}|
|	             |categoryId	|Int	|O	|テーマID|
|	             |isTop	|Boolean	|O	|上段固定表記|
|	             |contents.{language}.title	|String	|O	|お知らせタイトル|
|	             |contents.{language}.content	|String	|O	|お知らせ内容|
|	             |startDt	|String	|O	|開始時間（yyyyMMddHHmmss）|
|	             |endDt	|String	|O	|終了時間（yyyyMMddHHmmss）|
|	             |displayDt	|String	|X	|出力時間（yyyyMMddHHmmss）|
|	             |tags	|Array	|X	|タグリスト|
|	             |tags[].tagId	|Int	|O	|タグID|
|	             |attachments	|Array	|X	|添付ファイル|
|	             |attachments[].attachmentId	|String	|O	|添付ファイルID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ]
    }
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|result.content	|noticeId	|Int	|O	|お知らせID|
|	        |serviceId	|String	|O	|サービスID|
|	        |status	        |String	|O	|お知らせ状態 {D：草案, O：公開, C：完了}|
|	        |categoryId	|Int	|O	|テーマID|
|	        |isTop	        |Boolean	|O	|上段固定表記|
|	        |title	        |String	|O	|お知らせタイトル|
|	        |content	|String	|O	|お知らせ内容|
|	        |startDt	|String	|O	|開始時間（yyyyMMddHHmmss）|
|	        |endDt	        |String	|O	|終了時間（yyyyMMddHHmmss）|
|	        |displayDt	|String	|X	|出力時間（yyyyMMddHHmmss）|
|	        |attachmentYn	|String	|O	|Y：添付ファイルを含む，N：添付ファイル含まれてない|
|	        |userId	        |Int	|O	|登録ユーザーID|
|	        |tags	        |Array	|X	|タグリスト|
|	        |tags[].tagId	|Int	|O	|タグID|
|	        |tags[].tag	|String	|O	|タグ名|
|	        |attachments	|Array	|X	|添付ファイル|
|	        |attachments[].attachmentId	|String	|O	|添付ファイルID|
|	        |attachments[].fileName	        |String	|O	|ファイル名|
|	        |attachments[].size	|Long	|O	|ファイルサイズ|
|	        |createdDt	        |Long	|O	|お知らせ登録時間|
|	        |updatedDt	        |Long	|O	|お知らせ修正時間|

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
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "中国語タイトル1",
      "content": "中国語内容1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "韓国語タグ1",
            "ja": "日本語タグ1",
            "zh": "中国語タグ1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "韓国語テーマ",
          "ja": "日本語テーマ",
          "zh": "中国語テーマ"
        }
      }
    }
  }
}
```

### お知らせ修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせ修正|HTTPS  |PUT    |UTF-8|JSON    |IDでお知らせを修正|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|お知らせID	|id	|Int	|O	|URL PATH内に設定した{id}|
|お知らせ内容	|request body	|String	|O	|お知らせ内容（JSON）|
|	             |status	     |String	|O	|お知らせ状態 {D：草案, O：公開, C：完了}|
|	             |categoryId	|Int	|O	|テーマID|
|	             |isTop	|Boolean	|O	|上段固定表記|
|	             |contents.{language}.title	|String	|O	|お知らせタイトル|
|	             |contents.{language}.content	|String	|O	|お知らせ内容|
|	             |startDt	|String	|O	|開始時間（yyyyMMddHHmmss）|
|	             |endDt	|String	|O	|終了時間（yyyyMMddHHmmss）|
|	             |displayDt	|String	|X	|出力時間（yyyyMMddHHmmss）|
|	             |tags	|Array	|X	|タグリスト|
|	             |tags[].tagId	|Int	|O	|タグID|
|	             |attachments	|Array	|X	|添付ファイル|
|	             |attachments[].attachmentId	|String	|O	|添付ファイルID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a"
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ]
    }
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|-----------|---------|----|
|result.content	|noticeId	|Int	|O	|お知らせID|
|	        |serviceId	|String	|O	|サービスID|
|	        |status	        |String	|O	|お知らせ状態 {D：草案, O：公開, C：完了}|
|	        |categoryId	|Int	|O	|テーマID|
|	        |isTop	        |Boolean	|O	|上段固定表記|
|	        |title	        |String	|O	|お知らせタイトル|
|	        |content	|String	|O	|お知らせ内容|
|	        |startDt	|String	|O	|開始時間（yyyyMMddHHmmss）|
|	        |endDt	        |String	|O	|終了時間（yyyyMMddHHmmss）|
|	        |displayDt	|String	|X	|出力時間（yyyyMMddHHmmss）|
|	        |attachmentYn	|String	|O	|Y：添付ファイルを含む，N：添付ファイル含まれてない|
|	        |userId	        |Int	|O	|登録ユーザーID|
|	        |tags	        |Array	|X	|タグリスト|
|	        |tags[].tagId	|Int	|O	|タグID|
|	        |tags[].tag	|String	|O	|タグ名|
|	        |attachments	|Array	|X	|添付ファイル|
|	        |attachments[].attachmentId	|String	|O	|添付ファイルID|
|	        |attachments[].fileName	        |String	|O	|ファイル名|
|	        |attachments[].size	|Long	|O	|ファイルサイズ|
|	        |createdDt	        |Long	|O	|お知らせ登録時間|
|	        |updatedDt	        |Long	|O	|お知らせ修正時間|
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": {
      "noticeId": 258,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "isTop": false,
      "term": "open",
      "title": "中国語タイトル1",
      "content": "中国語内容1",
      "startDt": "20190101000000",
      "endDt": "",
      "displayDt": "20190120000000",
      "readCnt": 0,
      "attachmentYn": "Y",
      "userId": 10063,
      "createdDt": 1547962599000,
      "updatedDt": 1548054677000,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
          "attachments": [
            {
              "attachmentId": "e981516df5da4b1cbf25af403b3a622a",
              "fileName": "file.jpg",
              "contentType": "application/octet-stream",
              "size": 10645
            }
          ]
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "韓国語タグ1",
            "ja": "日本語タグ1",
            "zh": "中国語タグ1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "韓国語テーマ",
          "ja": "日本語テーマ",
          "zh": "中国語テーマ"
        }
      }
    }
  }
}
```

### お知らせ削除
#### インターフェース説明
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/{id}.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせ削除|HTTPS  |DELETE    |UTF-8|JSON    |IDを通じてお知らせ削除|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|お知らせID	|Id	|Int	|O	|URL PATH内に設定した{id}|

#### 結果データ
- なし

### お知らせテンプレートリスト照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテンプレートリスト照会|HTTPS  |IN(GET)    |UTF-8|JSON    |テンプレート内容照会, テンプレートリストをリターン|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|Varchar(50)	|O	|サービスID，URL PATH内に設定|
|照会言語	|language	|Varchar(2)	|X	|ko：韓国語, zh：中国語, ja：日本語, en：英語|
|開始時間	|startDt	|Varchar(14)	|X	|登録時間（yyyyMMddHHmmss）|
|終了時間	|endDt	|Varchar(14)	|X	|登録時間（yyyyMMddHHmmss）|
|テーマID	 |categoryId	|Int	|X	|テーマID|
|タグ	|tag	|Int	|X	|タグID，IDが多数の場合' , 'で分離|
|ユーザーID	|userId	|Int	|X	|ユーザーID|
|状態	|status	|Varchar(1)	|X	|O：使用, C：未使用|
|キーワード	|keyword	|Varchar	|X	|検索文句|
|照会フィールド	|searchField	|Varchar	|X	|基本は内容+タイトルで検索, title：タイトルのみ検索, content：内容のみ検索|
|ページ	|page	|Int	|X	|ページ番号，基本は1ページ| 
|ページあたりの件数	|pageSize	|Int	|X	|ページあたりのデータ件数，基本は10件|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|テンプレートID|
|	                |serviceId	|String	|O	|サービスID|
|	                |language	|Varchar(2)	|O	|ko：韓国語, zh：中国語, ja：日本語, en：英語|
|	                |status	|String	|O	|O：使用 C：未使用|
|	                |categoryId	|Int	|O	|テーマID|
|	                |categoryName	|String	|O	|テーマ名|
|	                |subject	|String	|O	|テンプレートタイトル|
|	                |memo	        |String	|O	|テンプレート説明|
|	                |userId	        |Int	|O	|登録ユーザーID|
|	                |userName	|String	|O	|登録ユーザー名|
|result.contents.tags	|tags[].tagId	|Int	|O	|タグID|
|	                |tags[].tag	|String	|O	|タグ名|
|	                |tags[].names	|String	|O	|多言語タグ名|
|result.contents.category	|names	|String	|O	|多言語テーマ名|
|	                        |createdDt	|Long	|O	|テンプレート登録時間|
|	                        |updatedDt	|Long	|O	|テンプレート修正時間|

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
        "noticeId": 256,
        "serviceId": "multilanguage",
        "language":"zh"
        "status": "O",
        "categoryId": 509,
        "readCnt": 1,
        "userId": 10063,
        "createdDt": 1547950366000,
        "updatedDt": 1547961164000,
        "tags": [
          {
            "tagId": 94,
            "tag": "中国語タグ1",
            "names": {
              "ko": "韓国語タグ1",
              "ja": "日本語タグ1",
              "zh": "中国語タグ1"
            }
          }
        ],
        "userName": "example",
        "categoryName": "中国語テーマ",
        "category": {
          "categoryId": 509,
          "names": {
            "ko": "韓国語テーマ",
            "ja": "日本語テーマ",
            "zh": "中国語テーマ"
          }
        },
        "subject": "テンプレートタイトル1",
        "memo": "テンプレート説明"
      }
    ],
    "total": 1,
    "pages": 1,
    "pageNum": 1,
    "pageSize": 10
  }
}
```

### お知らせテンプレート詳細照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json		
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせテンプレート詳細照会|HTTPS  |GET    |UTF-8|JSON    |テンプレートIDを通じてお知らせテンプレート詳細照会|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|Varchar(50)	|O	|URL PATH内に設定した{serviceId}|
|テンプレートID	|id	        |Int        |O	|URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|result.contents	|noticeId	|Int	|O	|テンプレートID|
|	                |serviceId	|String	|O	|サービスID|
|	                |status	        |String	|O	|O：使用, C：未使用|
|	                |categoryId	|Int	|O	|テーマID|
|	                |userId	        |Int	|O	|登録ユーザーID|
|	                |subject	|String	|O	|テンプレートタイトル|
|	                |memo	        |String	|O	|テンプレート説明|
|result.content.contents	|{language}.title	|String	|O	|お知らせタイトル|
|	                        |{language}.content	|String	|O	|お知らせ内容|
|result.content.tags	        |tags[].tagId	|Int	|O	|タグID|
|	                        |tags[].names.{language}	|String	|O	|多言語タグ名|
|result.content.category	|categoryId	|Int	|O	|テーマID|
|	                        |names	|String	|O	|多言語テーマ名|
|	                        |createdDt	|Long	|O	|テンプレート登録時間|
|	                        |updatedDt	|Long	|O	|テンプレート修正時間|

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
      "noticeId": 256,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "title": "中国語タイトル1",
      "content": "中国語内容1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
        },
        "zh": {
          "title": "中国語タイトル",
          "content": "中国語内容1",
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "韓国語タグ1",
            "ja": "日本語タグ1",
            "zh": "中国語タグ1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "韓国語テーマ",
          "ja": "日本語テーマ",
          "zh": "中国語テーマ"
        }
      },
      "subject": "テンプレートタイトル1",
      "memo": "テンプレート説明1"
    }
  }
}
```

### お知らせテンプレート登録
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせテンプレート登録|HTTPS  |POST    |UTF-8|JSON    |新規テンプレート登録|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テンプレート内容	|status	|String	|O	|O：使用, C：未使用|
|	    |categoryId	|Int	|O	|テーマID|
|	    |subject	|String	|O	|テンプレートタイトル|
|	    |memo	|String	|O	|テンプレート説明|
|	    |contents.{language}.title	|String	|O	|多言語お知らせタイトル|
|	    |contents.{language}.content	|String	|O	|多言語お知らせ内容|
|	    |tags[].tagId	|Int	|O	|タグID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ],
      "subject": "テンプレートタイトル1",
      "memo": "テンプレート説明1"
    }
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|result.content	|noticeId	|Int	|O	|テンプレートID|
|	        |serviceId	|String	|O	|サービスID|
|	        |status	        |String	|O	|O：使用, C：未使用|
|	        |categoryId	|Int	|O	|テーマID|
|	        |subject	|String	|O	|テンプレートタイトル|
|	        |memo	        |String	|O	|テンプレート説明|
|	        |userId	        |Int	|O	|登録ユーザーID|
|result.content.contents	|{language}.title	|String	|O	|お知らせタイトル|
|	                        |{language}.content	|String	|O	|お知らせ内容|
|result.content.tags	        |tagId	                |Int	|O	|タグID|
|	                        |names.{language}	|String	|O	|多言語タグ名|
|result.content.category	|categoryId	        |Int	|O	|テーマID|
|	                        |names	                |String	|O	|多言語テーマ名|
|	                        |createdDt	        |Long	|O	|テンプレート登録時間|
|	                        |updatedDt	        |Long	|O	|テンプレート修正時間|

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
      "noticeId": 256,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "title": "中国語タイトル1",
      "content": "中国語内容1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "韓国語タグ1",
            "ja": "日本語タグ1",
            "zh": "中国語タグ1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "韓国語テーマ",
          "ja": "日本語テーマ",
          "zh": "中国語テーマ"
        }
      },
      "subject": "テンプレートタイトル1",
      "memo": "テンプレート説明1"
    }
  }
}
```

### お知らせテンプレート修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテンプレート修正|HTTPS  |PUT    |UTF-8|JSON    |IDを通じてテンプレート修正|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テンプレートID	|Id	|Int	|O	|URL PATH内に設定した{id}|
|テンプレート内容	|status	|String	|O	|O：使用, C：未使用|
|           |categoryId	|Int	|O	|テーマID|
|	    |subject	|String	|O	|テンプレートタイトル|
|	    |memo	|String	|O	|テンプレート説明|
|	    |contents.{language}.title	|String	|O	|多言語お知らせタイトル|
|	    |contents.{language}.content	|String	|O	|多言語お知らせ内容|
|	    |tags[].tagId	|Int	|O	|タグID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ],
      "subject": "テンプレートタイトル1",
      "memo": "テンプレート説明1"
    }
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|------------|--------|----|
|result.content	|noticeId	|Int	|O	|テンプレートID|
|	        |status	        |String	|O	|テンプレート状態. O：使用, C：未使用|
|	        |categoryId	|Int	|O	|テーマID|
|	        |subject	|String	|O	|テンプレートタイトル|
|	        |memo	        |String	|X	|テンプレート説明|
|	        |title	        |String	|O	|お知らせタイトル|
|	        |content	|String	|O	|お知らせ内容|
|	        |userId	        |Int	|O	|登録ユーザーID|
|	        |tags	        |Array	|X	|タグリスト|
|	        |tags[].tagId	|Int	|O	|タグID|
|	        |tags[].tag	|String	|O	|タグ名|
|	        |createdDt	|Long	|O	|テンプレート登録時間|
|	        |updatedDt	|Long	|O	|テンプレート修正時間|

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
      "noticeId": 256,
      "serviceId": "multilanguage",
      "status": "O",
      "categoryId": 509,
      "title": "中国語タイトル1",
      "content": "中国語内容1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "韓国語タイトル1",
          "content": "韓国語内容1",
        },
        "ja": {
          "title": "日本語タイトル1",
          "content": "日本語内容1",
        },
        "zh": {
          "title": "中国語タイトル1",
          "content": "中国語内容1",
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "韓国語タグ1",
            "ja": "日本語タグ1",
            "zh": "中国語タグ1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "韓国語テーマ",
          "ja": "日本語テーマ",
          "zh": "中国語テーマ"
        }
      },
      "subject": "テンプレートタイトル1",
      "memo": "テンプレート内容1"
    }
  }
}
```

### お知らせテンプレート削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテンプレート削除|HTTPS  |DELETE    |UTF-8|JSON    |IDを通じてテンプレート削除|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テンプレートID	|Id	        |Int	|O	|URL PATH内に設定した{id}|

#### 結果データ
- なし


### お知らせ添付ファイル添付
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/upload.json			
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/upload.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせ添付ファイルアップロード|HTTPS  |POST    |UTF-8|JSON    |サーバーにファイルアップロード|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|アップロードファイル|file	|File	|O	|アップロードファイルをformで提出|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|------------|--------|----|
|result.content	|attachmentId	|String	|O	|アップロードファイルID|
|	        |fileName	|String	|O	|ファイル名|
|	        |contentType	|String	|O	|ファイルタイプ|
|	        |size	        |Long	|O	|ファイルbyte|

#### Request Body
```
{
  "header": {
    "resultCode": 200,
    "resultMessage": "",
    "isSuccessful": true
  },
  "result": {
    "content": {
      "attachmentId": "b891809a58b94ce3a09c080b81d0d14c",
      "fileName": "file2.jpg",
      "contentType": "image/jpeg",
      "size": 13855
    }
  }
}
```

### お知らせ添付ファイルを開く/ダウンロード
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせ添付ファイルを開く/ダウンロード|HTTPS  |GET    |UTF-8|FILE   |サーバーにアップロードしたお知らせ添付ファイルを開く/ダウンロード|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	           |serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|アップロードファイルID	 |id	      |String  |O	|アップロードファイルID| 
|閲覧方式	          |type	       |String	   |	|基本:開く（download:ダウンロード, open:開く）|

### お知らせ添付ファイル削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせ添付ファイル削除|HTTPS  |DELETE    |UTF-8|JSON    |サーバーにアップロードしたファイル削除|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String |O	|URL PATH内に設定した{serviceId}|
|アップロードファイルID	|id	|String	|O	|アップロードファイルid| 

#### 結果データ
- なし

### お知らせタグリスト照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせタグリスト照会|HTTPS  |GET    |UTF-8|JSON    |お知らせタグリスト照会|

#### 요リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|タグキーワード|tag	|String	|X	|タグ検索フレーズ|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|--------|---------|------------|--------|----|
|result.contents	|tagId	        |Int	|O	|タグID|
|	                |serviceId	|String	|O	|サービスID|
|                       |tag		|	|        |タグ内容|
|	                |createdDt	|Long	|O	|登録時間|
|	                |tagCode	|	|	|タグCode|
|	                |languages.{language}	|String	|O	|タグ内容（多言語）|

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
        "tagId": 94,
        "tag": "韓国語タグ1",
        "tagCode": "code",
        "serviceId": "multilanguage",
        "createdDt": 1547960380000,
        "languages": {
          "ko": "韓国語タグ1",
          "ja": "日本語タグ1",
          "zh": "中国語タグ1",
          "en": "英語タグ1"
        }
      },
      {
        "tagId": 95,
        "tag": "韓国語タグ2",
        "tagCode": "game",
        "serviceId": "multilanguage",
        "createdDt": 1547949797000,
        "names": {
          "ko": "韓国語タグ2",
          "ja": "日本語タグ2",
          "zh": "中国語タグ2",
          "en": "英語タグ2"
        }
      }
    ]
  }
}
```

### お知らせタグの詳細照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせタグの詳細照会|HTTPS  |GET    |UTF-8|JSON    |タグIDを通じてお知らせタグの詳細照会|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|タグID / タグcode	|id	|String	|O	|URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|------------|--------|-----|
|result.contents	|tagId	        |Int	|O	|タグID|
|	                |serviceId	|String	|O	|サービスID|
|                       |tag		|	|        |タグ内容|
|	                |createdDt	|Long	|O	|登録時間|
|	                |tagCode	|	|	|タグCode|
|	                |languages.{language}	|String	|O	|タグ内容（多言語）|

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
      "tagId": 94,
      "tag": "韓国語タグ1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "韓国語タグ1",
        "ja": "日本語タグ1",
        "zh": "中国語タグ1",
        "en": "英語タグ1"
      }
    }
  }
}
```

### お知らせタグ登録
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせタグ登録|HTTPS  |POST    |UTF-8|JSON    |新規タグ登録|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|タグCode	|tagCode	|String	|X	|タグCode|
|タグ内容	|names.{language}	|String	|O	|タグ内容|
|タグ内容(多言語)	|languages.{language}	|String	|O	|タグ内容(多言語)|

#### Request Body
```
単一言語
{
   "tagCode": "code",
   "tag": "韓国語タグ1",
}

多言語
{
  "tagCode": "code",
  "languages": {
    "ko": "韓国語タグ1",
    "ja": "日本語タグ1",
    "zh": "中国語タグ1",
    "en": "英語タグ1",
  }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|--------|---------|-----------|---------|----|
|result.contents	|tagId	        |Int	|O	|タグID|
|	                |serviceId	|String	|O	|サービスID|
|                       |tag		|	|        |タグ内容|
|	                |createdDt	|Long	|O	|登録時間|
|	                |tagCode	|	|	|タグCode|
|	                |languages.{language}	|String	|O	|タグ内容（多言語）|

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
      "tagId": 94,
      "tag": "韓国語タグ1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "韓国語タグ1",
        "ja": "日本語タグ1",
        "zh": "中国語タグ1",
        "en": "英語タグ1"
      }
    }
  }
}
```

### お知らせタグ修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせタグ修正|HTTPS  |PUT    |UTF-8|JSON    |タグIDを通じてお知らせタグ修正|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|タグID / タグcode	|id	|String	|O	|URL PATH内に設定した{id}|
|タグ内容	|names.{language}	|String	|O	|タグ内容|
|タグ内容(多言語)	|languages.{language}	|String	|O	|タグ内容(多言語)|

#### Request Body
```
単一言語
{
   "tag": "韓国語タグ1",
}

多言語
{
  "languages": {
    "ko": "韓国語タグ1",
    "ja": "日本語タグ1",
    "zh": "中国語タグ1",
    "en": "英語タグ1",
  }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|------------|--------|----|
|result.contents	|tagId	        |Int	|O	|タグID|
|	                |serviceId	|String	|O	|サービスID|
|                       |tag		|	|        |タグ内容|
|	                |createdDt	|Long	|O	|登録時間|
|	                |tagCode	|	|	|タグCode|
|	                |languages.{language}	|String	|O	|タグ内容（多言語）|

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
      "tagId": 94,
      "tag": "韓国語タグ1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "韓国語タグ1",
        "ja": "日本語タグ1",
        "zh": "中国語タグ1",
        "en": "英語タグ1"
      }
    }
  }
}
```

### お知らせタグ削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json		
- URL（開発）: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせタグ削除|HTTPS  |DELETE  |UTF-8|JSON    |タグIDを通じてお知らせタグ削除|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|タグID / タグcode	|id	|String	|O	|URL PATH内に設定した{id}|

#### 結果データ
- なし

### お知らせテーマリスト照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/categories.json	
- URL（開発）: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/categories.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテーマリスト照会|HTTPS  |GET  |UTF-8|JSON    |お知らせテーマリスト |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|テーマID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|	|テーマCode|
|	                |parent	        |Int	|	|上位テーマID（固定値:0）|
|	                |name	        |String	|O	|テーマ名|
|	                |level	        |Int	|	|段階（固定値:1）|
|	                |path	        |String	|	|段階経路（固定値:"\\\\"）|
|	                |orderNo	|Int	|	|整列順序（基本:0）|
|	                |createdDt	|Long	|	|登録時間|
|	                |updatedDt	|Long	|	|修正時間|
|	                |languages	|String	|	|多言語|

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
                "name":"韓国語テーマ2",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1554949320000,
                "updatedDt":1554949320000,
                "languages":{
                    "ko":"韓国語テーマ2"
                }
            },
            {
                "categoryId":509,
                "serviceId":"multilanguage",
                "categoryCode":"code1",
                "parent":0,
                "name":"中国語テーマ1",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1547949603000,
                "updatedDt":1554887489000,
                "languages":{
                    "ko":"韓国語テーマ1",
                    "ja":"日本語テーマ1",
                    "en":"英語テーマ1",
                    "zh":"中国語テーマ1"
                }
            }
        ]
    }
}
```

### お知らせテーマ詳細照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json
- URL（開発）: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテーマ詳細照会|HTTPS  |GET  |UTF-8|JSON    |テーマIDを通じてお知らせテーマ詳細照会|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テーマID / テーマcode	|id	|String	|O	|URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|テーマID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|	|テーマCode|
|	                |parent	        |Int	|	|上位テーマID（固定値:0）|
|	                |name	        |String	|O	|テーマ名|
|	                |level	        |Int	|	|段階（固定値:1）|
|	                |path	        |String	|	|段階経路（固定値:"\\\\"）|
|	                |orderNo	|Int	|	|整列順序（基本:0）|
|	                |createdDt	|Long	|	|登録時間|
|	                |updatedDt	|Long	|	|修正時間|
|	                |languages	|String	|	|多言語|

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
            "name":"中国語テーマ1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"韓国語テーマ1",
                "ja":"日本語テーマ1",
                "en":"英語テーマ1",
                "zh":"中国語テーマ1"
            }
        }
    }
}
```

### お知らせテーマ登録
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category.json
- URL（開発）: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテーマ登録 |HTTPS  |POST  |UTF-8|JSON    |新規テーマ登録|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テーマ情報	|request body	|String	|O	|テーマ情報（JSON）|
|	    |name	    |String |		|テーマ名（唯一の値:はい ; 長さ:min = 0, max = 50 ; 形式:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|テーマCode|
|	    |languages	        |String	|	|多言語|
|	    |orderNo	|Int	|	|整列順序（固定値:0）|

#### Request Body
```
単一言語
{
    "name":"中国語テーマ3",
    "categoryCode":"game3",
    "orderNo":1
}

多言語
{
    "categoryCode":"game3",
    "parent":0,
    "orderNo":1,
    "languages":{
        "ko":"韓国語テーマ3",
        "ja":"日本語テーマ3",
        "en":"英語テーマ3",
        "zh":"中国語テーマ3"
    }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|テーマID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|	|テーマCode|
|	                |parent	        |Int	|	|上位テーマID（固定値:0）|
|	                |name	        |String	|O	|テーマ名|
|	                |level	        |Int	|	|段階（固定値:1）|
|	                |path	        |String	|	|段階経路（固定値:"\\\\"）|
|	                |orderNo	|Int	|	|整列順序（基本:0）|
|	                |createdDt	|Long	|	|登録時間|
|	                |updatedDt	|Long	|	|修正時間|
|	                |languages	|String	|	|多言語|

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
            "categoryId":1577,
            "serviceId":"multilanguage",
            "categoryCode":"game3",
            "parent":0,
            "name":"中国語テーマ3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"韓国語テーマ3",
                "ja":"日本語テーマ3",
                "en":"英語テーマ3",
                "zh":"中国語テーマ3"
            }
        }
    }
}
```

### お知らせテーマ修正
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json
- URL（開発）: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json	
											
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテーマ修正|HTTPS  |POST  |UTF-8|JSON    |テーマIDを通じてお知らせテーマ修正|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テーマID / テーマcode	|id	|String	|O	|URL PATH内に設定した{id}|
|テーマ情報	|request body	|String	|O	|テーマ情報（JSON）|
|	    |name	    |String |		|テーマ名（唯一の値:はい ; 長さ:min = 0, max = 50 ; 形式:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|テーマCode|
|	    |languages	        |String	|	|多言語|
|	    |orderNo	|Int	|	|整列順序（固定値:0）|

#### Request Body
```
単一言語
{
    "name":"中国語テーマ3",
    "categoryCode":"game3",
    "orderNo":1
}

多言語
{
    "categoryCode":"game3",
    "orderNo":1,
    "languages":{
        "ko":"韓国語テーマ3",
        "ja":"日本語テーマ3",
        "en":"英語テーマ3",
        "zh":"中国語テーマ3"
    }
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|テーマID|
|	                |serviceId	|String	|O	|サービスID|
|	                |categoryCode	|String	|	|テーマCode|
|	                |parent	        |Int	|	|上位テーマID（固定値:0）|
|	                |name	        |String	|O	|テーマ名|
|	                |level	        |Int	|	|段階（固定値:1）|
|	                |path	        |String	|	|段階経路（固定値:"\\\\"）|
|	                |orderNo	|Int	|	|整列順序（基本:0）|
|	                |createdDt	|Long	|	|登録時間|
|	                |updatedDt	|Long	|	|修正時間|
|	                |languages	|String	|	|多言語|

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
            "categoryId":1577,
            "serviceId":"multilanguage",
            "categoryCode":"game3",
            "parent":0,
            "name":"中国語テーマ3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"韓国語テーマ3",
                "ja":"日本語テーマ3",
                "en":"英語テーマ3",
                "zh":"中国語テーマ3"
            }
        }
    }
}
```

### お知らせテーマ削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com /{serviceId}/openapi/v1/notice/category/{id}.json
- URL（開発）: https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/notice/category/{id}.json
											
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|
|------------|-------|--------|-----|--------|--------------|
|お知らせテーマ削除|HTTPS  |DELETE  |UTF-8|JSON    |テーマIDを通じてお知らせテーマ削除|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テーマID / テーマcode	|id	|String	|O	|URL PATH内に設定した{id}|

#### 結果データ
- なし

