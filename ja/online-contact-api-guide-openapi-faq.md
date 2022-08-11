## Contact Center > Online Contact > プログラマーのためのAPIガイド > FAQ

### カテゴリーリスト
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/api/v2/helpdoc/categories.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/api/v2/helpdoc/categories.json
			
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|カテゴリーリスト|HTTPS  |GET    |UTF-8|JSON    |FAQカテゴリーリスト取得|必要なし|

##### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	|String	|path	|O	|URL PATH内に設定した{serviceId}|
|言語コード	|language	  |String	|query |X	|サービスヘルプセンターの基本言語コード|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|categoryId	|Integer		|カテゴリーID|
|	                |parent	    |Integer		|上位カテゴリーID|
|	                |name	      |String		  |カテゴリー名|
|	                |level	    |Integer		|レベル(1, 2, 3)|
|	                |path	      |String		  |レベル経路(\level1\level2\)|
|	                |orderNo	  |Integer		|整列順序(基本値: 0)|
|	                |languages	|Object		  |多言語|

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
                "categoryId": 2546,	
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
                "categoryId": 2548,	
                "parent": 2546,	
                "name": "유형1-1",	
                "level": 2,	
                "path": "\\2546\\",	
                "orderNo": 0,	
                "languages": {	
                    "ko": "유형1-1",	
                    "th": "พิมพ์1-1",	
                    "ja": "タイプ1-1",	
                    "en": "Type1-1",	
                    "zh": "类型1-1"	
                }	
            },	
            {	
                "categoryId": 2550,	
                "parent": 2548,	
                "name": "유형1-1-1",	
                "level": 3,	
                "path": "\\2546\\2548\\",	
                "orderNo": 0,	
                "languages": {	
                    "ko": "유형1-1-1",	
                    "th": "พิมพ์1-1-1",	
                    "ja": "タイプ1-1-1",	
                    "en": "Type1-1-1",	
                    "zh": "类型1-1-1"	
                }	
            },	
            {	
                "categoryId": 2547,	
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
                "categoryId": 2549,	
                "parent": 2546,	
                "name": "유형1-2",	
                "level": 2,	
                "path": "\\2546\\",	
                "orderNo": 1,	
                "languages": {	
                    "ko": "유형1-2",	
                    "th": "พิมพ์1-2",	
                    "ja": "タイプ1-2",	
                    "en": "Type1-2",	
                    "zh": "类型1-2"	
                }	
            },	
            {	
                "categoryId": 2551,	
                "parent": 2548,	
                "name": "유형1-1-2",	
                "level": 3,	
                "path": "\\2546\\2548\\",	
                "orderNo": 1,	
                "languages": {	
                    "ko": "유형1-1-2",	
                    "th": "พิมพ์1-1-2",	
                    "ja": "タイプ1-1-2",	
                    "en": "Type1-1-2",	
                    "zh": "类型1-1-2"	
                }	
            }	
        ]	
    }	
}	
```

### FAQリスト
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/api/v2/helpdoc/list.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/api/v2/helpdoc/list.json
	
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQリスト|HTTPS  |GET    |UTF-8|JSON    |ヘルプセンターFAQリスト| 必要なし   |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID    |serviceId	|String	  |path	  |O	|URL PATH内に設定した{serviceId}|
|言語コード	    |language	  |String	  |query	|X	|ヘルプセンター言語コード(基本値: 基本言語コード)|
|カテゴリーID	  |categoryId	|Integer	|query	|X	|FAQ カテゴリーID|
|キーワード        |query	    |String	  |query	|X	|検索キーワード（照会範囲:FAQタイトル、内容）|
|整列フィールド  	  |sort	      |String	  |query	|X	|isTop、isRecommend、createdDt、updatedDtフィールドを通じて整列可能であり、複数のフィールド整列時に[,]を通じて分離。 asc:上り順; desc:下り順|
|ページ        |page	      |Integer	|query	|X  |ページ番号（基本値:1）|
|ページ当たりの件数	|pageSize	  |Integer	|query	|X	|ページあたりのデータ件数（基本値:10件、MAX:200）|

sortパラメータの形式および例は下記のとおりです。

- 形式: フィールド1:整列,フィールド2:整列,……
- 例: isTop:desc,createdDt:asc
- 基本整列（カテゴリーIDが空値でない場合）: isTop:desc,isRecommend:desc,updatedDt:desc
- 基本整列（カテゴリーIDが空値の場合）: isTop:desc,updatedDt:desc

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|helpDocId	  |Integer		|FAQ ID|
|	                |title	      |String		  |FAQのタイトル|
|	                |content	    |String		  |FAQの内容|
|	                |isRecommend	|Boolean		|カテゴリー別固定可否(true:固定;false:固定ではない)|
|	                |isTop	      |Boolean		|メイン画面での固定可否（true:固定;false:固定ではない）|
|	                |createdDt	  |Long		    |登録時間|
|	                |updatedDt	  |Long		    |修正時間|
|	                |categoryId	  |Integer		|FAQ カテゴリーID|
|	                |categoryName	|String		  |カテゴリ名称、要請パラメータの言語コードに対応する言語のカテゴリー名称が露出する。|
|	                |isNew	      |String		  |FAQ NEW 表示(true:露出時間(displayDt)値が今日、false:露出時間(displayDt)値が今日以外|
|result	          |total	      |Integer		|総件数|
|	                |pages	      |Integer		|総ページ数|
|	                |pageNum	    |Integer		|ページ|
|	                |pageSize	    |Integer		|ページ当たりの件数|

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
                "helpDocId": 3414,	
                "title": "자주 묻는 질문 제목2",	
                "content": "자주 묻는 질문 내용2",	
                "isRecommend": false,	
                "isTop": true,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657265718000,	
                "updatedDt": 1657265718000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2551,	
                "categoryName": "유형1-1-2",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3413,	
                "title": "자주 묻는 질문 제목1",	
                "content": "자주 묻는 질문 내용1",	
                "isRecommend": true,	
                "isTop": true,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657265403000,	
                "updatedDt": 1657265403000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2550,	
                "categoryName": "유형1-1-1",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3423,	
                "title": "자주 묻는 질문 제목11",	
                "content": "자주 묻는 질문 내용11",	
                "isRecommend": false,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657266235000,	
                "updatedDt": 1657266235000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2550,	
                "categoryName": "유형1-1-1",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3422,	
                "title": "자주 묻는 질문 제목10",	
                "content": "자주 묻는 질문 내용10",	
                "isRecommend": false,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657266185000,	
                "updatedDt": 1657266196000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2550,	
                "categoryName": "유형1-1-1",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3421,	
                "title": "자주 묻는 질문 제목9",	
                "content": "자주 묻는 질문 내용9",	
                "isRecommend": false,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657266110000,	
                "updatedDt": 1657266110000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2550,	
                "categoryName": "유형1-1-1",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3420,	
                "title": "자주 묻는 질문 제목8",	
                "content": "자주 묻는 질문 내용8",	
                "isRecommend": false,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657266059000,	
                "updatedDt": 1657266059000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2550,	
                "categoryName": "유형1-1-1",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3419,	
                "title": "자주 묻는 질문 제목7",	
                "content": "자주 묻는 질문 내용7",	
                "isRecommend": false,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657266009000,	
                "updatedDt": 1657266009000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2550,	
                "categoryName": "유형1-1-1",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3418,	
                "title": "자주 묻는 질문 제목6",	
                "content": "자주 묻는 질문 내용6",	
                "isRecommend": false,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657265956000,	
                "updatedDt": 1657265956000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2547,	
                "categoryName": "유형2",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3417,	
                "title": "자주 묻는 질문 제목5",	
                "content": "자주 묻는 질문 내용5",	
                "isRecommend": false,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657265902000,	
                "updatedDt": 1657265902000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2546,	
                "categoryName": "유형1",	
                "categoryFullName": null,	
                "attachments": null,	
                "isNew": false	
            },	
            {	
                "helpDocId": 3416,	
                "title": "자주 묻는 질문 제목4",	
                "content": "자주 묻는 질문 내용4",	
                "isRecommend": true,	
                "isTop": false,	
                "readCnt": null,	
                "attachmentYn": null,	
                "createdDt": 1657265838000,	
                "updatedDt": 1657265838000,	
                "parentCategoryList": null,	
                "category": null,	
                "categoryId": 2549,	
                "categoryName": "유형1-2",	
                "categoryFullName": null,	
                "attachments": null,	
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

### FAQ詳細
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/api/v2/helpdoc/detail/{id}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/api/v2/helpdoc/detail/{id}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ詳細 |HTTPS  |GET    |UTF-8|JSON    |FAQ IDによりFAQ内容を取得|必要なし |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	|String	 |path	 |O	 |URL PATH内に設定した{serviceId}|
|FAQ ID	    |id	       |Integer	|path	  |O	|URL PATH内に設定した{id}|
|言語コード	|language	  |String	 |query	 |X	 |サービスヘルプセンターの基本言語コード|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|helpDocId	                    |Integer		 |FAQ ID|
|	              |title	                        |String		   |FAQのタイトル|
|	              |content	                      |String		   |FAQの内容|
|               |isRecommend	                  |Boolean		 |推薦|
|	              |isTop	                        |Boolean		 |上段固定|
|	              |readCnt	                      |Integer		 |照会数|
|	              |attachmentYn	                  |Boolean		 |添付ファイルが含まれているかどうか|
|	              |createdDt	                    |Long	     	 |FAQ 登録時間|
|	              |updatedDt	                    |Long		     |FAQ 修正時間|
|	              |parentCategoryList	            |Array	  	 |上位カテゴリー情報|
|	              |parentCategoryList.categoryId	|Integer		 |カテゴリーID|
|	              |parentCategoryList.parent	    |Integer		 |上位カテゴリーID|
|	              |parentCategoryList.name	      |String		   |カテゴリー名|
|	              |parentCategoryList.level	      |Integer		 |カテゴリーレベル(0, 1, 2)|
|	              |parentCategoryList.path	      |String		   |カテゴリーレベル経路(\\\\で各ID接続)|
|	              |parentCategoryList.orderNo	    |Integer		 |カテゴリー表示手順設定|
|	              |parentCategoryList.languages  	|Object		   |多言語カテゴリー名|
|	              |category	                      |Object		   |カテゴリー情報|
|	              |category.categoryId			      |            |カテゴリーID|
|	              |category.parent			          |            |上位カテゴリーID|
|	              |category.name			            |            |カテゴリー名|
|	              |category.level			            |            |カテゴリーレベル(0, 1, 2)|
| 	            |category.languages			        |            |多言語カテゴリー名|
|	              |categoryId	                    |Integer		 |お知らせカテゴリーID|
|	              |categoryName	                  |String		   |カテゴリー名|
|	              |categoryFullName	              |String		   |カテゴリー全経路名|
|	              |attachments	                  |Array		   |添付ファイル|
|	              |attachments.attachmentId	      |String		   |添付ファイルID|
|	              |attachments.fileName	          |String		   |添付ファイル名|
|	              |attachments.contentType	      |String		   |添付ファイルタイプ|
|	              |attachments.size	              |Long		     |添付ファイルサイズ|
|        	      |isNew	                        |String		   |新規のお知らせ表示 true:露出時間(displayDt)値が今日、false:露出時間(displayDt)値が今日以外|

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
            "helpDocId": 3413,		
            "title": "자주 묻는 질문 제목1",		
            "content": "<p>자주 묻는 질문 내용1</p>",		
            "isRecommend": true,		
            "isTop": true,		
            "readCnt": 12,		
            "attachmentYn": "Y",		
            "createdDt": 1657265404000,		
            "updatedDt": 1657265404000,		
            "parentCategoryList": [		
                {		
                    "categoryId": 2546,		
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
                    "categoryId": 2548,		
                    "parent": 2546,		
                    "name": "유형1-1",		
                    "level": 2,		
                    "path": "\\2546\\",		
                    "orderNo": 0,		
                    "languages": {		
                        "ko": "유형1-1",		
                        "th": "พิมพ์1-1",		
                        "ja": "タイプ1-1",		
                        "en": "Type1-1",		
                        "zh": "类型1-1"		
                    }		
                },		
                {		
                    "categoryId": 2550,		
                    "parent": 2548,		
                    "name": "유형1-1-1",		
                    "level": 3,		
                    "path": "\\2546\\2548\\",		
                    "orderNo": 0,		
                    "languages": {		
                        "ko": "유형1-1-1",		
                        "th": "พิมพ์1-1-1",		
                        "ja": "タイプ1-1-1",		
                        "en": "Type1-1-1",		
                        "zh": "类型1-1-1"		
                    }		
                }		
            ],		
            "category": {		
                "categoryId": 2550,		
                "parent": 2548,		
                "name": "유형1-1-1",		
                "level": 3,		
                "languages": {		
                    "ko": "유형1-1-1",		
                    "th": "พิมพ์1-1-1",		
                    "ja": "タイプ1-1-1",		
                    "en": "Type1-1-1",		
                    "zh": "类型1-1-1"		
                }		
            },		
            "categoryId": 2550,		
            "categoryName": "유형1-1-1",		
            "categoryFullName": "유형1>유형1-1>유형1-1-1",		
            "attachments": [		
                {		
                    "attachmentId": "badf8fac176e42cc85e232e19759ad2f",		
                    "fileName": "nhn.png",		
                    "contentType": "image/png",		
                    "size": 9682		
                },		
                {		
                    "attachmentId": "d4f3667f13c14ddea57cd55b71df868c",		
                    "fileName": "logo_footer.png",		
                    "contentType": "image/png",		
                    "size": 1412		
                }		
            ],		
            "isNew": false		
        }		
    }		
}		
```

### FAQ添付ファイルを開く/ダウンロード
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/api/v2/helpdoc/attachments/{id}
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/api/v2/helpdoc/attachments/{id}	
									
|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|FAQ添付ファイルを開く/ダウンロード |HTTPS  |GET    |UTF-8|JSON    |FAQ添付ファイルを開く/ダウンロード|必要なし  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID          |serviceId	|String	|path   |O	    |URL PATH内に設定した{serviceId}|
|アップロードファイルID      |id	        |String  |path   |O     |アップロードファイルID| 
|閲覧方式	          |type	      |String	|query   |X     |基本値: 開く（download: ダウンロード、open: 開く）|

#### 結果データ
File