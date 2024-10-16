## Contact Center > Online Contact > API ガイド > お知らせ

### テーマリスト
#### インターフェース説明
- URL: https://{domain}.oc.nhncloud.com/{serviceId}/api/v2/notice/categories.json
- URL(開発): https://{domain}.oc.alpha-nhncloud.com/{serviceId}/api/v2/notice/categories.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|テーマリスト |HTTPS  |GET  |UTF-8|JSON    |お知らせテーマリスト取得|必要なし|

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	|String	|path	  |O	|URL PATH内に設定した{serviceId}|
|言語コード	|language	  |String	|query	|X	|サービスヘルプセンターの基本言語コード|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|categoryId	|Integer		|テーマID|
|	                |parent	    |Integer		|上位テーマID(固定値:0)|
|	                |name	      |String		  |テーマ名|
|	                |level	    |Integer		|レベル(固定値:1)|
|	                |path	      |String		  |レベル経路(固定値:"\\\\")|
|	                |orderNo	  |Integer		|整列順序|
|	                |languages	|Object		  |テーマの多言語名称値（言語コード:対応する言語コードの名称）|

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
                "categoryId": 2543,	
                "parent": 0,	
                "name": "유형1",	
                "level": 1,	
                "path": "\\",	
                "orderNo": 0,	
                "languages": {	
                    "ko": "유형1",	
                    "th": "พิมพ์1",	
                    "ja": "タイプ1",	
                    "en": "Type1",	
                    "zh": "类型1"	
                }	
            },	
            {	
                "categoryId": 2544,	
                "parent": 0,	
                "name": "유형2",	
                "level": 1,	
                "path": "\\",	
                "orderNo": 1,	
                "languages": {	
                    "ko": "유형2",	
                    "th": "พิมพ์2",	
                    "ja": "タイプ2",	
                    "en": "Type2",	
                    "zh": "类型2"	
                }	
            },	
            {	
                "categoryId": 2545,	
                "parent": 0,	
                "name": "유형3",	
                "level": 1,	
                "path": "\\",	
                "orderNo": 2,	
                "languages": {	
                    "ko": "유형3",	
                    "th": "พิมพ์3",	
                    "ja": "タイプ3",	
                    "en": "Type3",	
                    "zh": "类型3"	
                }	
            }	
        ]	
    }	
}	
```

### タグリスト
#### インターフェース説明
- URL: https://{domain}.oc.nhncloud.com/{serviceId}/api/v2/notice/tags.json
- URL(開発): https://{domain}.oc.alpha-nhncloud.com/{serviceId}/api/v2/notice/tags.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|タグリスト  |HTTPS  |GET    |UTF-8|JSON    |お知らせタグリスト取得|必要なし|

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	|String	|path  |O	|URL PATH内に設定した{serviceId}|
|タグキーワード |language	|String	|query |X	|タグ検索語|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|tagId	|Integer		|タグID|
|	                |tag	  |String		  |タグ名称|
|	                |languages	|Object		|タグの多言語名称値（言語コード:対応する言語コード名称）|

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
                "tagId": 391,	
                "tag": "태그1",	
                "languages": {	
                    "ko": "태그1",	
                    "th": "แท็ก1",	
                    "ja": "タグ1",	
                    "en": "Tag1",	
                    "zh": "标签1"	
                }	
            },	
            {	
                "tagId": 392,	
                "tag": "태그2",	
                "languages": {	
                    "ko": "태그2",	
                    "th": "แท็ก2",	
                    "ja": "タグ2",	
                    "en": "Tag2",	
                    "zh": "标签2"	
                }	
            }	
        ]	
    }	
}	
```

### お知らせリスト
#### インターフェース説明
- URL: https://{domain}.oc.nhncloud.com/{serviceId}/api/v2/notice/list.json
- URL(開発): https://{domain}.oc.alpha-nhncloud.com/{serviceId}/api/v2/notice/list.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせリスト|HTTPS  |GET    |UTF-8|JSON    |ヘルプセンターお知らせリスト|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	       |serviceId	  |String	    |path	  |O	|URL PATH内に設定した{serviceId}|
|言語コード	         |language	   |String	  |query	|X	|サービスヘルプセンターの基本言語コード|
|カテゴリーID	     |categoryId	 |Integer	  |query	|X	|カテゴリーID|
|タグID	         |tagId	       |Integer	  |query	|X	|タグID|
|キーワード検索	      |query	     |String	  |query	 |X	 |キーワード検索（検索範囲:タイトル·内容）|
|整列順序	        |sort	       |String	  |query	 |X	 |isTop、createdDt、updatedDt、displayDtフィールドに整列可能であり、複数のフィールド整列時に[,]を通じて分離。 asc:上り順; desc:下り順|
|ページ  	          |page   	   |Integer	  |query	 |X	 |基本値: 1|
|1ページあたりの露出件数	 |pageSize	  |Integer	 |query	  |X	|基本値: 10; max=200|

sortパラメータの形式および例は下記のとおりです。

- 形式: フィールド1:整列,フィールド2:整列,……
- 例: isTop:desc,createdDt:asc
- 基本整列: isTop:desc,displayDt:desc,updatedDt:desc

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|noticeId	    |Integer		|お知らせID|
|	                |categoryId	  |Integer		|お知らせのカテゴリーID|
|	                |isTop	      |Boolean		|上段固定表記(true: yes; false: no)|
|	                |title	      |String		  |お知らせのタイトル|
|	                |content	    |String		  |お知らせの内容|
|	                |displayDt	  |String		  |出力時間(yyyyMMddHHmmss)|
|	                |updatedDt	  |Long		    |修正時間|
|	                |categoryName	|String		  |カテゴリー名|
|	                |tagStr	      |Integer		|タグ名|
|	                |isNew	      |String		  |新規お知らせ表示. true:出力時間(displayDt)値が今日、false:出力時間(displayDt)値が今日以外|
|result   	      |total	      |Integer		|総件数|
|	                |pages	      |Integer		|総ページ数|
|	                |pageNum	    |Integer		|ページ|
|	                |pageSize	    |Integer		|ページ当たりの露出件数|

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
                "noticeId": 1241,	
                "categoryId": 2543,	
                "isTop": true,	
                "title": "공지제목7",	
                "content": "공지내용7",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657243026000,	
                "categoryName": "유형1",	
                "tagStr": "태그2",	
                "isNew": false	
            },	
            {	
                "noticeId": 1246,	
                "categoryId": 2543,	
                "isTop": false,	
                "title": "공지제목11",	
                "content": "공지내용11",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657243165000,	
                "categoryName": "유형1",	
                "tagStr": "태그1",	
                "isNew": false	
            },	
            {	
                "noticeId": 1245,	
                "categoryId": 2543,	
                "isTop": false,	
                "title": "공지제목10",	
                "content": "공지내용10",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657243148000,	
                "categoryName": "유형1",	
                "tagStr": "태그1",	
                "isNew": false	
            },	
            {	
                "noticeId": 1244,	
                "categoryId": 2543,	
                "isTop": false,	
                "title": "공지제목9",	
                "content": "공지내용9",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657243129000,	
                "categoryName": "유형1",	
                "tagStr": "태그1",	
                "isNew": false	
            },	
            {	
                "noticeId": 1243,	
                "categoryId": 2543,	
                "isTop": false,	
                "title": "공지제목8",	
                "content": "공지내용8",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657243106000,	
                "categoryName": "유형1",	
                "tagStr": "태그1",	
                "isNew": false	
            },	
            {	
                "noticeId": 1240,	
                "categoryId": 2543,	
                "isTop": false,	
                "title": "공지제목6",	
                "content": "공지내용6",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657242949000,	
                "categoryName": "유형1",	
                "tagStr": "태그2",	
                "isNew": false	
            },	
            {	
                "noticeId": 1239,	
                "categoryId": 2543,	
                "isTop": false,	
                "title": "공지제목5",	
                "content": "공지내용5",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657242735000,	
                "categoryName": "유형1",	
                "tagStr": "태그1",	
                "isNew": false	
            },	
            {	
                "noticeId": 1238,	
                "categoryId": 2543,	
                "isTop": false,	
                "title": "공지제목4",	
                "content": "공지내용4",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657242576000,	
                "categoryName": "유형1",	
                "isNew": false	
            },	
            {	
                "noticeId": 1237,	
                "categoryId": 2545,	
                "isTop": false,	
                "title": "공지제목3",	
                "content": "공지내용3",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657242501000,	
                "categoryName": "유형3",	
                "tagStr": "태그1,태그2",	
                "isNew": false	
            },	
            {	
                "noticeId": 1236,	
                "categoryId": 2544,	
                "isTop": false,	
                "title": "공지제목2",	
                "content": "공지내용2",	
                "displayDt": "2022.07.08",	
                "updatedDt": 1657242420000,	
                "categoryName": "유형2",	
                "tagStr": "태그2",	
                "isNew": false	
            }	
        ],	
        "total": 11,	
        "pages": 2,	
        "pageNum": 1,	
        "pageSize": 10	
    }	
}	
```

### お知らせ詳細
#### インターフェース説明
- URL: https://{domain}.oc.nhncloud.com/{serviceId}/api/v2/notice/detail/{id}.json
- URL(開発): https://{domain}.oc.alpha-nhncloud.com/{serviceId}/api/v2/notice/detail/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせ詳細|HTTPS  |GET    |UTF-8|JSON    |お知らせIDでお知らせ内容を取得|必要なし|

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	  |serviceId	|String	  |path	  |O	|URL PATH内に設定した{serviceId}|
|お知らせID	|id	        |Integer	|path	  |O	|お知らせID|
|言語コード	  |language	  |String	  |query	|X	|サービスヘルプセンターの基本言語コード|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|noticeId	                |Integer	|お知らせID|
|	              |categoryId	              |Integer	|テーマID|
|	              |isTop	                  |Boolean	|上段固定表記|
|	              |title	                  |String		|お知らせのタイトル|
|	              |content	                |String		|お知らせの内容|
|	              |displayDt	              |String		|出力時間(yyyyMMddHHmmss)|
|	              |attachmentYn	            |Boolean	|添付ファイルを含むかどうか（true:含む; false:含まない）|
|	              |readCnt	                |Integer	|照会回数|
|	              |updatedDt	              |Long		  |お知らせ修正時間|
|	              |attachments	            |Array		|お知らせ添付|
|	              |attachments.attachmentId	|String		|添付ファイルID|
|	              |attachments.fileName	    |String		|添付ファイル名|
|	              |attachments.contentType	|String		|添付ファイルタイプ|
|	              |attachments.size	        |Long		  |添付ファイルサイズ|
|	              |tags	                    |Array		|お知らせタグ|
|	              |tags.tagId	              |Integer	|タグID|
|	              |tags.tag	                |String		|タグ名称|
|               |categoryName	            |String		|テーマ名称|
|	              |isNew	                  |String		|新規お知らせ表示. true:露出時間(displayDt)が今日、false:露出時間(displayDt)が今日以外|

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
            "noticeId": 1240,	
            "categoryId": 2543,	
            "isTop": true,	
            "title": "공지제목6",	
            "content": "<p>공지내용6</p>",	
            "displayDt": "2022.07.08",	
            "attachmentYn": "Y",	
            "readCnt": 5,	
            "updatedDt": 1658114209000,	
            "attachments": [	
                {	
                    "attachmentId": "42fb4c8801ed4c278475f70f531b8c92",	
                    "fileName": "logo_footer.png",	
                    "contentType": "image/png",	
                    "size": 1412	
                }	
            ],	
            "tags": [	
                {	
                    "tagId": 391,	
                    "tag": "태그1"	
                },	
                {	
                    "tagId": 392,	
                    "tag": "태그2"	
                }	
            ],	
            "categoryName": "유형1",	
            "isNew": false	
        }	
    }	
}	
```

### お知らせ添付ファイルを開く/ダウンロード
#### インターフェース説明
- URL: https://{domain}.oc.nhncloud.com/{serviceId}/api/v2/notice/attachments/{id}
- URL(開発): https://{domain}.oc.alpha-nhncloud.com/{serviceId}/api/v2/notice/attachments/{id}		

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|お知らせ添付ファイルを開く/ダウンロード|HTTPS  |GET    |UTF-8|JSON    |お知らせ添付ファイルを開く/ダウンロード|必要なし|

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	    |serviceId	|String	  |path	 |O	|URL PATH内に設定した{serviceId}|
|アップロードファイルID	|id	         |String	|path	  |O	|アップロードファイルID|
|閲覧方式	    |type	       |String	|query	|X	|基本値: 開く（download: ダウンロード、open: 開く）|

#### 結果データ
File