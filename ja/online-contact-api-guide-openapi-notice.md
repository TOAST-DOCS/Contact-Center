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
- 없음

### お知らせテンプレートリスト照会
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template.json
		
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
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

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|
|お知らせテンプレート修正|HTTPS  |PUT    |UTF-8|JSON    |IDを通じてテンプレート修正|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|----|-----|------------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|テンプレートID	|Id	|Int	|O	|URL PATH内に設定した{id}|
|テンプレート内容	|status	|String	|O	|O：使用, C：未使用|
|           |categoryId	|Int	|O	|말머리 ID|
|	    |subject	|String	|O	|템플릿 제목|
|	    |memo	|String	|O	|템플릿 설명|
|	    |contents.{language}.title	|String	|O	|다국어 공지사항 제목|
|	    |contents.{language}.content	|String	|O	|다국어 공지사항 내용|
|	    |tags[].tagId	|Int	|O	|태그 ID|

#### Request Body
```
    {
      "status": "O",
      "categoryId": 509,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
        }
      },
      "tags": [
        {
          "tagId": 94,
        }
      ],
      "subject": "템플릿 제목1",
      "memo": "템플릿 설명1"
    }
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|----|
|result.content	|noticeId	|Int	|O	|템플릿 ID|
|	        |status	        |String	|O	|템플릿 상태. O：사용, C：미사용|
|	        |categoryId	|Int	|O	|말머리 ID|
|	        |subject	|String	|O	|템플릿 제목|
|	        |memo	        |String	|X	|템플릿 설명|
|	        |title	        |String	|O	|공지사항 제목|
|	        |content	|String	|O	|공지사항 내용|
|	        |userId	        |Int	|O	|등록 유저 ID|
|	        |tags	        |Array	|X	|태그 리스트|
|	        |tags[].tagId	|Int	|O	|태그 ID|
|	        |tags[].tag	|String	|O	|태그 명|
|	        |createdDt	|Long	|O	|템플릿 등록시간|
|	        |updatedDt	|Long	|O	|템플릿 수정시간|

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
      "title": "중국어 제목1",
      "content": "중국어 내용1",
      "userId": 10063,
      "createdDt": 1547950366000,
      "updatedDt": 1547961165000,
      "contents": {
        "ko": {
          "title": "한국어 제목1",
          "content": "한국어 내용1",
        },
        "ja": {
          "title": "일본어 제목1",
          "content": "일본어 내용1",
        },
        "zh": {
          "title": "중국어 제목1",
          "content": "중국어 내용1",
        }
      },
      "tags": [
        {
          "tagId": 94,
          "names": {
            "ko": "한국어 태그1",
            "ja": "일본어 태그1",
            "zh": "중국어 태그1"
          }
        }
      ],
      "category": {
        "categoryId": 509,
        "names": {
          "ko": "한국어 말머리",
          "ja": "일본어 말머리",
          "zh": "중국어 말머리"
        }
      },
      "subject": "템플릿 제목1",
      "memo": "템플릿 내용1"
    }
  }
}
```

### 공지사항 템플릿 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json										
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/multilanguage/notice/template/{id}.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 템플릿 삭제 |HTTPS  |DELETE    |UTF-8|JSON    |ID를 통해 템플릿 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|템플릿 ID	|Id	        |Int	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
- 없음


### 공지사항 첨부파일 첨부
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/upload.json			
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/upload.json			

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 첨부파일 업로드 |HTTPS  |POST    |UTF-8|JSON    |서버에 파일 업로드|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|업로드 파일	|file	|File	|O	|업로드 파일을 form으로 통해 제출|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|----|
|result.content	|attachmentId	|String	|O	|업로드 파일 ID|
|	        |fileName	|String	|O	|파일 명|
|	        |contentType	|String	|O	|파일 유형|
|	        |size	        |Long	|O	|파일 byte|

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

### 공지사항 첨부파일 열기/다운로드
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}						 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/attachments/notice/{id}						

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 첨부파일 열기 및 다운로드 |HTTPS  |GET    |UTF-8|FILE   |서버에 업로드한 공지사항 첨부파일 열기 및 다운로드|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	           |serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|업로드 파일 ID	 |id	      |String  |O	|업로드 파일id| 
|열람방식	          |type	       |String	   |	|기본 값:열기（download:다운로드, open:열기）|

### 공지사항 첨부파일 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/notice/{id}.json			 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ attachments/notice/{id}.json				

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 첨부파일 삭제 |HTTPS  |DELETE    |UTF-8|JSON    |서버에 업로드한 파일 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String |O	|URL PATH 내에 설정한{serviceId}|
|업로드 파일 ID	|id	|String	|O	|업로드 파일id| 

#### 결과 데이터
- 없음

#### Response Body
- File

### 공지사항 태그 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag.json					 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag.json					

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 목록 조회 |HTTPS  |GET    |UTF-8|JSON    |공지사항 태그 목록 조회|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 키워드	|tag	|String	|X	|태그 검색 문구|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|--------|---------|------------|--------|----|
|result.contents	|tagId	        |INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|                       |tag		|	|        |태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
        "tag": "한국어 태그1",
        "tagCode": "code",
        "serviceId": "multilanguage",
        "createdDt": 1547960380000,
        "languages": {
          "ko": "한국어 태그1",
          "ja": "일본어 태그1",
          "zh": "중국어 태그1",
          "en": "영어 태그1"
        }
      },
      {
        "tagId": 95,
        "tag": "한국어 태그2",
        "tagCode": "game",
        "serviceId": "multilanguage",
        "createdDt": 1547949797000,
        "names": {
          "ko": "한국어 태그2",
          "ja": "일본어 태그2",
          "zh": "중국어 태그2",
          "en": "영어 태그2"
        }
      }
    ]
  }
}
```

### 공지사항 태그 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json						 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json						

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 상세 조회 |HTTPS  |GET    |UTF-8|JSON    |태그 ID를 통해 공지사항 태그 상세 내용 조회|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 ID / 태그 code	|id	|String	|O	|URL PATH내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|-----|
|result.contents	|tagId	|INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	|	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
      "tag": "한국어 태그1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "한국어 태그1",
        "ja": "일본어 태그1",
        "zh": "중국어 태그1",
        "en": "영어 태그1"
      }
    }
  }
}
```

### 공지사항 태그 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag.json								 		
- URL(개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag.json							

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 등록 |HTTPS  |POST    |UTF-8|JSON    |신규 태그 등록|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 Code	|tagCode	|String	|X	|태그 Code|
|태그 내용	|names.{language}	|String	|O	|태그 내용|
|태그 내용(다국어)	|languages.{language}	|String	|O	|태그 내용(다국어)|

#### Request Body
```
단일언어
{
   "tagCode": "code",
   "tag": "한국어 태그1",
}

다국어
{
  "tagCode": "code",
  "languages": {
    "ko": "한국어 태그1",
    "ja": "일본어 태그1",
    "zh": "중국어 태그1",
    "en": "영어 태그1",
  }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|--------|---------|-----------|---------|----|
|result.contents	|tagId	|INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	|	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
      "tag": "한국어 태그1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "한국어 태그1",
        "ja": "일본어 태그1",
        "zh": "중국어 태그1",
        "en": "영어 태그1"
      }
    }
  }
}
```

### 공지사항 태그 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json											 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json									

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 수정 |HTTPS  |PUT    |UTF-8|JSON    |태그 ID를 통해 공지사항 태그 수정|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 ID / 태그 code	|id	|String	|O	|URL PATH 내에 설정한{id}|
|태그 내용	|names.{language}	|String	|O	|태그 내용|
|태그 내용(다국어)	|languages.{language}	|String	|O	|태그 내용(다국어)|

#### Request Body
```
단일언어
{
   "tag": "한국어 태그1",
}

다국어
{
  "languages": {
    "ko": "한국어 태그1",
    "ja": "일본어 태그1",
    "zh": "중국어 태그1",
    "en": "영어 태그1",
  }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|------------|--------|----|
|result.contents	|tagId	|INT	|O	|태그 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |tag	|	|	|태그 내용|
|	                |createdDt	|Long	|O	|등록시간|
|	                |tagCode	|	|	|태그 Code|
|	                |languages.{language}	|String	|O	|태그 내용（다국어）|

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
      "tag": "한국어 태그1",
      "tagCode": "code",
      "serviceId": "multilanguage",
      "createdDt": 1547960380000,
      "languages": {
        "ko": "한국어 태그1",
        "ja": "일본어 태그1",
        "zh": "중국어 태그1",
        "en": "영어 태그1"
      }
    }
  }
}
```

### 공지사항 태그 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/tag/{id}.json											

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 태그 삭제 |HTTPS  |DELETE  |UTF-8|JSON    |태그 ID를 통해 공지사항 태그 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|태그 ID / 태그 code	|id	|String	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
- 없음

### 공지사항 말머리 목록 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/categories.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/categories.json											

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 목록 조회 |HTTPS  |GET  |UTF-8|JSON    |공지사항 말머리 목록  |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에  설정한{serviceId}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.contents	|categoryId	|Int	|O	|말머리 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |categoryCode	|String	|	|말머리 Code|
|	                |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	                |name	        |String	|O	|말머리 명|
|	                |level	        |Int	|	|뎁스（고정 값:1）|
|	                |path	        |String	|	|뎁스 경로（고정 값:"\\"）|
|	                |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	                |createdDt	|Long	|	|등록시간|
|	                |updatedDt	|Long	|	|수정시간|
|	                |languages	|String	|	|다국어|

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
                "name":"한국어 말머리2",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1554949320000,
                "updatedDt":1554949320000,
                "languages":{
                    "ko":"한국어 말머리2"
                }
            },
            {
                "categoryId":509,
                "serviceId":"multilanguage",
                "categoryCode":"code1",
                "parent":0,
                "name":"중국어 말머리1",
                "level":1,
                "path":"\\",
                "orderNo":0,
                "createdDt":1547949603000,
                "updatedDt":1554887489000,
                "languages":{
                    "ko":"한국어 말머리1",
                    "ja":"일본어 말머리1",
                    "en":"영어 말머리1",
                    "zh":"중국어 말머리1"
                }
            }
        ]
    }
}
```

### 공지사항 말머리 상세 조회
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v2/notice/category/{id}.json										

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 상세 조회 |HTTPS  |GET  |UTF-8|JSON    |말머리 ID를 통해 공지사항 상세 내용 조회|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 ID / 말머리 code	|id	|String	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|말머리 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |categoryCode	|String	|	|말머리 Code|
|	        |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|	|뎁스（고정 값:1）|
|	        |path	        |String	|	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|	|등록시간|
|	        |updatedDt	|Long	|	|수정시간|
|	        |languages	|String	|	|다국어|

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
            "name":"중국어 말머리1",
            "level":1,
            "path":"\\",
            "orderNo":0,
            "createdDt":1547949603000,
            "updatedDt":1554887489000,
            "languages":{
                "ko":"한국어 말머리1",
                "ja":"일본어 말머리1",
                "en":"영어 말머리1",
                "zh":"중국어 말머리1"
            }
        }
    }
}
```

### 공지사항 말머리 등록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category.json												

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 등록 |HTTPS  |POST  |UTF-8|JSON    |신규 말머리 등록|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 정보	|request body	|String	|O	|말머리 정보（JSON）|
|	    |name	    |String |		|말머리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|말머리 Code|
|	    |languages	        |String	|	|다국어|
|	    |orderNo	|Int	|	|정렬순서（고정 값:0）|

#### Request Body
```
단일 언어
{
    "name":"중국어 말머리3",
    "categoryCode":"game3",
    "orderNo":1
}

다국어
{
    "categoryCode":"game3",
    "parent":0,
    "orderNo":1,
    "languages":{
        "ko":"한국어 말머리3",
        "ja":"일본어 말머리3",
        "en":"영어 말머리3",
        "zh":"중국어 말머리3"
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|말머리 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |categoryCode	|String	|	|말머리 Code|
|	        |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|	|뎁스（고정 값:1）|
|	        |path	        |String	|	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|	|등록시간|
|	        |updatedDt	|Long	|	|수정시간|
|	        |languages	|String	|	|다국어|

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
            "name":"중국어 말머리3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"한국어 말머리3",
                "ja":"일본어 말머리3",
                "en":"영어 말머리3",
                "zh":"중국어 말머리3"
            }
        }
    }
}
```

### 공지사항 말머리 수정
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/notice/category/{id}.json			
											
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 수정 |HTTPS  |POST  |UTF-8|JSON    |말머리 ID를 통해 말머리 명 수정|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 ID / 말머리 code	|id	|String	|O	|URL PATH 내에 설정한{id}|
|말머리 정보	|request body	|String	|O	|말머리 정보（JSON）|
|	    |name	    |String |	    |말머리 명（유일한 값:예 ; 길이:min = 0, max = 50 ; 형식:^(\_\|-\|[^\\pP])+$）|
|	    |categoryCode	|String	|	|말머리 Code|
|	    |languages	|String	   |	|다국어|
|	    |orderNo	|Int	   |	|정렬순서（고정 값:0）|

#### Request Body
```
단일 언어
{
    "name":"중국어 말머리3",
    "categoryCode":"game3",
    "orderNo":1
}

다국어
{
    "categoryCode":"game3",
    "orderNo":1,
    "languages":{
        "ko":"한국어 말머리3",
        "ja":"일본어 말머리3",
        "en":"영어 말머리3",
        "zh":"중국어 말머리3"
    }
}
```

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|---------|--------|-----------|---------|----|
|result.content	|categoryId	|Int	|O	|말머리 ID|
|	        |serviceId	|String	|O	|서비스 ID|
|	        |categoryCode	|String	|	|말머리 Code|
|	        |parent	        |Int	|	|상위 말머리 ID（고정 값:0）|
|	        |name	        |String	|O	|말머리 명|
|	        |level	        |Int	|	|뎁스（고정 값:1）|
|	        |path	        |String	|	|뎁스 경로（고정 값:"\\\\"）|
|	        |orderNo	|Int	|	|정렬순서（기본 값:0）|
|	        |createdDt	|Long	|	|등록시간|
|	        |updatedDt	|Long	|	|수정시간|
|	        |languages	|String	|	|다국어|

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
            "name":"중국어 말머리3",
            "level":1,
            "path":"\\",
            "orderNo":1,
            "createdDt":1587360957961,
            "updatedDt":1587360957961,
            "languages":{
                "ko":"한국어 말머리3",
                "ja":"일본어 말머리3",
                "en":"영어 말머리3",
                "zh":"중국어 말머리3"
            }
        }
    }
}
```

### 공지사항 말머리 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com /{serviceId}/openapi/v1/notice/category/{id}.json												 
- URL: https://{domain}.alpha-oc.toast.com /{serviceId}/openapi/v1/notice/category/{id}.json					
											
|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|
|------------|-------|--------|-----|--------|--------------|
|공지사항 말머리 삭제|HTTPS  |DELETE  |UTF-8|JSON    |말머리 ID를 통해 말머리 명 삭제|

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|----|-----|------------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한{serviceId}|
|말머리 ID / 말머리 code	|id	|String	|O	|URL PATH 내에 설정한{id}|

#### 결과 데이터
- 없음

