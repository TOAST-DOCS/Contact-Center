## Contact Center > Online Contact > プログラマーのためのAPIガイド > チケット管理

### チケット作成
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/add.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット作成|HTTPS  |POST    |UTF-8|JSON    |新規チケット作成|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|----------|-----|----|
|サービスID	|serviceId	     |String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|チケット情報 |request body	|String	|O	|チケット情報JSON)|
|    	     |categoryId	|Int	|X	|受付タイプID，ない場合は指定しなくてもよい|
|   	     |subject	    |String	|O	|チケットのタイトル（max=255）|
|          |content	        |String	|O	|チケット内容|
| 	       |endUser.usercode	|String	|O	|ユーザーコード（唯一の値）|
|	         |endUser.email	    |String	|X	|ユーザーメール（チケット処理の際、該当メールに返答が送信されます。 ない場合はメールが送信されません。)|
|	         |endUser.username	|String	|X	|ユーザー名|
|          |endUser.phone	    |String	|X	|ユーザー電話番号|
|	         |addition	        |String	|X	|基本フィールドの他に追加されたフィールド情報|
|	         |attachments[].attachmentId	|String	|X	|添付ファイルID|

#### Request Body
```
{
    "categoryId":1567,
    "subject":"This is a new ticket",
    "content":"I have a question for you",
    "endUser":{
        "usercode":"gamebaseuser1",
        "username":"TestUser",
        "email":"gamebaseuser1@toast.com",
        "phone":"13333333333"
    },
    "addition":"{'sex':'male','age':20}" ,
    "attachments":[
       {
            "attachmentId":"5a13cbfd3c574f7dae644536d3e4159c"
        },
       {
            "attachmentId":"43f035ea67554ceab7f11535ee7ac5ac"
        }
    ]
}
```

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|result.content	|ticketId	    |String	|O	|チケットID|
|	              |serviceId	|String	|O	|サービスID|
|	              |subject	    |String	|O	|チケットタイトル|
|	              |categoryId	|Int	|X	|受付タイプID|
|               |categoryName	|String	|X	|受付タイプ名|
|	              |status	    |String	|O	|チケットの状況（open:新規チケット; closed:処理完了）|
|	              |endUser.usercode	|String	|O	|ユーザーコード（唯一の値）|
|	              |endUser.email	|String	|X	|ユーザーメール（チケット処理の際、該当メールに返答が送信されます。 ない場合はメールが送信されません。)|
|	              |endUser.username	|String	|X	|ユーザー名|
|	              |endUser.phone	|String	|X	|ユーザー電話番号|
| 	            |content	|String	|O	|チケットのお問い合わせ内容|
|	              |createdDt	|Long	|O	|チケット作成時間|
|	              |updatedDt	|Long	|O	|チケットアップデート時間|
|               |contents	|String	|X	|チケット処理情報|
|	              |attachments[].attachmentId	|String	|X	|添付ファイル ID|
|	              |addition	|String	|X	|基本フィールドの他に追加されたフィールド情報|

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
            "ticketId":"T1586918360295gJrtI",
            "serviceId":"GameBaseService",
            "subject":"This is a new ticket",
            "categoryId":1567,
            "categoryName":null,
            "status":"open",
            "endUser":{
                "usercode":"gamebaseuser1",
                "username":"TestUser",
                "email":"gamebaseuser1@toast.com",
                "phone":"13333333333"
            },
            "content":"I have a question for you",
            "createdDt":1586918360291,
            "updatedDt":1586918360291,
            "contents":null,
            "attachments":[
                {
                    "attachmentId":"5a13cbfd3c574f7dae644536d3e4159c",
                    "fileName":null,
                    "contentType":null,
                    "disposition":null,
                    "size":null,
                    "createdDt":null
                },
                {
                    "attachmentId":"43f035ea67554ceab7f11535ee7ac5ac",
                    "fileName":null,
                    "contentType":null,
                    "disposition":null,
                    "size":null,
                    "createdDt":null
                }
            ],
            "addition":"{'sex':'male','age':20}"
        }
    }
}
```

### チケット処理
#### インターフェース説明
- URL:	https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/solve.json			
- URL (開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/solve.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット処理 |HTTPS  |POST    |UTF-8|JSON    |チケットIDでチケット処理|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|チケットID	|id	|String	|O	|チケットID|
|添付ファイル	|attachments	|String	|X	|添付ファイルID（形式（ファイルIDは　,で分離）：ファイルID1,ファイルID2,…,ファイルIDn）|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|----|-----------|-----|----|
|result.content	|id	|String	|O	|チケットID|
|	              |serviceId	|String	|O	|サービスID|
|	              |subject	|String	|O	|チケットタイトル|
|	              |categoryId	|Int	|X	|受付タイプID|
|               |categoryName	|String	|X	|受付タイプ名|
|	              |status	    |String	|O	|チケットの状況（open:新規チケット; closed:処理完了）|
|	              |endUser.usercode	|String	|O	|ユーザーコード（唯一の値）|
|	              |endUser.email	|String	|X	|ユーザーメール（チケット処理の際、該当メールに返答が送信されます。 ない場合はメールが送信されません。)|
|	              |endUser.username	|String	|X	|ユーザー名|
|	              |endUser.phone	|String	|X	|ユーザー電話番号|
|	              |content	|String	|O	|チケットのお問い合わせ内容|
|	              |createdDt	|Long	|O	|チケット作成時間|
|	              |updatedDt	|Long	|O	|チケットアップデート時間|
|	              |contents.content	|String	|X	|チケット処理内容|
|	              |contents.createdDt	|Long	|X	|チケット処理時間|
|	              |contents.attachments	|String	|X	|チケット処理添付ファイルID|
|	              |attachments[].attachmentId	|String	|X	|添付ファイルID|
|               |addition	|String	|X	|基本フィールドの他に追加されたフィールド情報|


#### Request Body
- 形式: application/json;charset=UTF-8
```
{"comment":"comment content.XXXXXXXXX"}
```

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
            "ticketId":"T1586918360295gJrtI",
            "serviceId":"GameBaseService",
            "subject":"This is a new ticket",
            "categoryId":1567,
            "categoryName":"bug",
            "status":"closed",
            "endUser":null,
            "content":null,
            "createdDt":1586918360000,
            "updatedDt":1586927308531,
            "contents":[
                {
                    "content":"I solve it",
                    "createdDt":1586927311120,
                    "attachments":null
                }
            ],
            "attachments":null,
            "addition":null
        }
    }
}
```

### チケット詳細
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/{id}.json			
- URL (開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/{id}.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット詳細 |HTTPS  |GET    |UTF-8|JSON    |チケットIDを通じてチケット照会|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|チケットID	|id	|String	|O	|チケットID，URL PATH内に設定した{id}|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|result.content	|ticketId	|String	|O	|チケットID|
|	            |serviceId	|String	|O	|サービスID|
|	            |subject	|String	|O	|チケットタイトル|
|	            |categoryId	|Int	|X	|受付タイプID|
|	            |categoryName	|String	|X	|受付タイプ名|
|	            |status	        |String	|O	|チケットの状態（open:新規チケット; closed:処理完了）|
|	            |endUser.usercode	|String	|O	|ユーザーコード（唯一の値）|
|	            |endUser.email	    |String	|X	|ユーザーメール（チケット処理の際、該当メールに返答が送信されます。 ない場合はメールが送信されません。)|
|	            |endUser.username	|String	|X	|ユーザー名|
|	            |endUser.phone	    |String	|X	|ユーザー電話番号|
|	            |content	        |String	|O	|チケットのお問い合わせ内容|
|	            |createdDt	        |Long	|O	|チケット作成時間|
|	            |updatedDt	        |Long	|O	|チケットアップデート時間|
|	            |contents.content	|String	|X	|チケット処理内容|
|	            |contents.createdDt	|Long	|X	|チケット処理時間|
|	            |contents.attachments.attachmentId	|String	|X	|チケット処理添付ファイルID|
|	            |contents.attachments.fileName	|String	|X	|チケット処理添付ファイル名|
|	            |contents.attachments.contentType	|String	|X	|チケット処理添付ファイルタイプ|
|	            |contents.attachments.disposition	|String	|X	|チケット処理添付ファイル処理方式（attachment:添付ファイル）|
|	            |contents.attachments.size	|Long	|X	|チケット処理添付ファイルサイズ|
|	            |contents.attachments.createdDt	|Long	|X	|チケット処理添付ファイルのアップロード時間|
|	            |attachments.attachmentId	|String	|X	|チケットお問い合わせ添付ファイルID|
|	            |attachments.fileName	|String	|X	|チケットお問い合わせ添付ファイル名|
|	            |attachments.contentType	|String	|X	|チケットお問い合わせ添付ファイルタイプ|
|	            |attachments.disposition	|String	|X	|チケット問い合わせ添付ファイル処理方式（attachment:添付ファイル）|
|	            |attachments.size	|Long	|X	|チケットお問い合わせ添付ファイルのサイズ|
|	            |attachments.createdDt	|Long	|X	|チケットお問い合わせ添付ファイルのアップロード時間|
|	            |addition	|String	|X	|基本フィールドの他に追加されたフィールド情報|

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
            "ticketId":"T1586918360295gJrtI",
            "serviceId":"GameBaseService",
            "subject":"This is a new ticket",
            "categoryId":1567,
            "categoryName":"bug",
            "status":"closed",
            "endUser":{
                "usercode":"gamebaseuser1",
                "username":"TestUser",
                "email":"gamebaseuser1@toast.com",
                "phone":"13333333333"
            },
            "content":"I have a question for you",
            "createdDt":1586918360000,
            "updatedDt":1586927309000,
            "contents":[
                {
                    "content":"I solve it",
                    "createdDt":1586927311000,
                    "attachments":[
                        {
                            "attachmentId":"bb7109b2ebd14780ae5403f17de88246",
                            "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3 (1).zip",
                            "contentType":"application/x-zip-compressed",
                            "disposition":"attachment",
                            "size":223573,
                            "createdDt":1586918795000
                        },
                        {
                            "attachmentId":"914cd0fb61934c0698655118158d84d5",
                            "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3.zip",
                            "contentType":"application/x-zip-compressed",
                            "disposition":"attachment",
                            "size":223573,
                            "createdDt":1586918801000
                        }
                    ]
                }
            ],
            "attachments":[
                {
                    "attachmentId":"5a13cbfd3c574f7dae644536d3e4159c",
                    "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3 (1).zip",
                    "contentType":"application/x-zip-compressed",
                    "disposition":"attachment",
                    "size":223573,
                    "createdDt":1586918296000
                },
                {
                    "attachmentId":"43f035ea67554ceab7f11535ee7ac5ac",
                    "fileName":"jp.gr.java_conf.ussiy.app.propedit_5.3.3.zip",
                    "contentType":"application/x-zip-compressed",
                    "disposition":"attachment",
                    "size":223573,
                    "createdDt":1586918300000
                }
            ],
            "addition":"{'sex':'male','age':20}"
        }
    }
}
```

### チケットリスト
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/list.json						
- URL (開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/list.json				

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット目録  |HTTPS  |GET    |UTF-8|JSON    |検索条件を通じて条件に合うチケットリストを照会|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|サービスID	|serviceId	|String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|開始時間	|startDt	|String	|X	|検索範囲の開始時間(チケット作成時間)(形式:yyyyMMddHHmmss）|
|終了時間	|endDt	|String	|X	|検索範囲の終了時間(チケット作成時間)(形式:yyyyMMddHHmmss）|
|チケットID	|ticketId	|String	|X	|チケットID|
|タイトル	|subject	|String	|X	|タイトル|
|チケット状態	|status	|String	|X	|チケット状態（open:新規チケット; closed:処理完了）|
|受付タイプ	|categoryId	|Int	|X	|受付タイプID（IDが複数ある場合 , で分離）|
|ユーザーコード	|usercode	|String	|X	|ユーザーコード（唯一の値）|
|ユーザー名	|username	|String	|X	|ユーザー名|
|ユーザーメール	|email	  |String	|X	|ユーザーメール|
|並び順	|sort	   |String	|X	|並び順(基本値:updatedDt:desc; 形式変数:整列（昇順:asc, 降順:desc))|
|ページ	|page	    |Int	|X	|基本値:1|
|ページあたりの露出件数|pageSize	|Int	|X	|基本値:10;max=200|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|result.contents	|ticketId	|String	|O	|チケットID|
|	                |serviceId	|String	|O	|サービスID|
|	                |subject	|String	|O	|チケットタイトル|
|	                |categoryId	|Int	|X	|受付タイプID|
|	                |categoryName	|String	|X	|受付タイプ名|
|	                |status	|String	|O	|チケット状態（open:新規チケット; closed:処理完了）|
|	                |createdDt	|Long	|O	|チケット作成時間|
|	                |updatedDt	|Long	|O	|チケットアップデート時間|
|	                |addition	|String	|X	|基本フィールドの他に追加されたフィールド情報|
|result.total	|total	        |Long	|O	|総件数|
|result.pages	|pages	        |Int	|O	|総ページ数|
|result.pageNum	|pageNum	    |Int	|O	|現在ページ|
|result.pageSize	|pageSize	|Int	|O	|ページあたりの露出件数|

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
                "ticketId":"T1586918360295gJrtI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586918360000,
                "updatedDt":1586927309000,
                "addition":null
            },
            {
                "ticketId":"T1586915418254WQQM9",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586915418000,
                "updatedDt":1586915505000,
                "addition":null
            },
            {
                "ticketId":"T1586914789452LJEcI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586914789000,
                "updatedDt":1586915162000,
                "addition":null
            },
            {
                "ticketId":"T1586846795949Ij1xA",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846796000,
                "updatedDt":1586852906000,
                "addition":null
            },
            {
                "ticketId":"T1586846821052WKmoK",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846821000,
                "updatedDt":1586852382000,
                "addition":null
            },
            {
                "ticketId":"T1586849274901SZ94B",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586849275000,
                "updatedDt":1586851357000,
                "addition":null
            }
        ],
        "total":6,
        "pages":1,
        "pageNum":1,
        "pageSize":10
    }
}
```

### ユーザーチケットリスト
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/{usercode}/list.json							
- URL (開発):	https://{domain}.alpha-oc.toast.co/{serviceId}/openapi/v1/ticket/{usercode}/list.json	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|ユーザーチケットリスト|HTTPS  |GET    |UTF-8|JSON    |検索条件を通じて条件に合うユーザーのチケットリスト照会|共通認証   |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|サービスID	|serviceId	 |String	|O	|サービスID，URL PATH内に設定した{serviceId}|
|ユーザーコード|usercode	|String	|O	|ユーザーコード(唯一の値)，URL PATH内に設定した{usercode}|
|開始時間	|startDt	|String	|X	|検索範囲の開始時間(チケット作成時間)(形式:yyyyMMddHHmmss）|
|終了時間	|endDt	|String	|X	|検索範囲の終了時間(チケット作成時間)(形式:yyyyMMddHHmmss）|
|チケットID	|ticketId	  |String	|X	|チケットID|
|タイトル	|subject	      |String	|X	|タイトル|
|チケット状態	|status	    |String	|X	|チケット状態（open:新規チケット; closed:処理完了）|
|受付タイプ	|categoryId	|Int	|X	|受付タイプID（IDが複数ある場合 , で分離）|
|整列方式	|sort	    |String	|X	|並び順(基本値:updatedDt:desc; 形式変数:整列（昇順:asc, 降順:desc))|
|ページ	|page	    |Int	|X	|基本値:1|
|ページあたりの露出件数|pageSize	|Int	|X	|基本値:10;max=200|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|result.contents	|ticketId	|String	|O	|チケットID|
|	                |serviceId	|String	|O	|サービスID|
|	                |subject	|String	|O	|チケットタイトル|
|	                |categoryId	|Int	|X	|受付タイプID|
|	                |categoryName	|String	|X	|受付タイプ名|
|	                |status	|String	|O	|チケット状態（open:新規チケット; closed:処理完了）|
|                   |createdDt	|Long	|O	|チケット作成時間|
|	                |updatedDt	|Long	|O	|チケットアップデート時間|
|	                |addition	|String	|X	|基本フィールドの他に追加されたフィールド情報|
|result.total	|total	        |Long	|O	|総件数|
|result.pages	|pages	        |Int	|O	|総ページ数|
|result.pageNum	|pageNum	    |Int	|O	|現在ページ|
|result.pageSize	|pageSize	|Int	|O	|ページあたりの露出件数|

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
                "ticketId":"T1586918360295gJrtI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586918360000,
                "updatedDt":1586927309000,
                "addition":null
            },
            {
                "ticketId":"T1586915418254WQQM9",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586915418000,
                "updatedDt":1586915505000,
                "addition":null
            },
            {
                "ticketId":"T1586914789452LJEcI",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586914789000,
                "updatedDt":1586915162000,
                "addition":null
            },
            {
                "ticketId":"T1586846795949Ij1xA",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846796000,
                "updatedDt":1586852906000,
                "addition":null
            },
            {
                "ticketId":"T1586846821052WKmoK",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586846821000,
                "updatedDt":1586852382000,
                "addition":null
            },
            {
                "ticketId":"T1586849274901SZ94B",
                "serviceId":"GameBaseService",
                "subject":"This is a new ticket",
                "categoryId":1567,
                "categoryName":"bug",
                "status":"closed",
                "createdDt":1586849275000,
                "updatedDt":1586851357000,
                "addition":null
            }
        ],
        "total":6,
        "pages":1,
        "pageNum":1,
        "pageSize":10
    }
}
```

### チケットに添付ファイル添付
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json			 			
- URL (開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json			

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|添付ファイル添付|HTTPS  |GET    |UTF-8|JSON    |サーバーへのファイルアップロード|共通認証 |

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|添付したファイル	|file	|File	|O	|添付したファイルはform形式で提出|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|添付したファイルのID|
|	            |fileName	    |String	|O	|ファイル名|
|	            |contentType	|String	|O	|ファイルのタイプ|
|	            |disposition	|String	|O	|ファイル処理方式（attachment:添付ファイル）|
|	            |size	|Long	|O	|ファイルサイズ|
|               |createdDt	|Long	|O	|ファイル添付時間|

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
            "attachmentId":"e5f0eab5cf694d4fb356c21a9bdaee48",
            "fileName":"1.jpeg",
            "contentType":"image/jpeg",
            "disposition":"attachment",
            "size":40375,
            "createdDt":null
        }
    }
}
```

### チケット添付ファイルを開く/ダウンロード
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}					 	
- URL (開発):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}		

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|添付ファイルを開く/ダウンロード  |HTTPS  |GET    |UTF-8|JSON    |サーバーにアップロードされたファイルを開く/ダウンロード|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|添付したファイルID	|id	|String	|O	|添付したファイルid| 
|処理方式|type	|String	|X	|デフォルト値はブラウザで開く（download:ダウンロード, open:ブラウザで開く）|

#### 結果データ
- なし

#### Response Body
- File

### チケット添付ファイル削除
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json		
- URL (開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json	

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|添付ファイル削除|HTTPS  |DELETE    |UTF-8|JSON    |サーバーにアップロードされたファイル削除|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|サービスID	|serviceId	|String	|O	|URL PATH内に設定した{serviceId}|
|添付したファイルID	 |id	|String	|O	|添付したファイルid|

#### 結果データ
|名称|変数|データタイプ|必須|説明|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|添付したファイルID| 
|	            |fileName	|String	|O	|ファイル名|
|	            |contentType	|String	|O	|ファイルタイプ|
|	            |size	|Long	|O	|ファイルサイズ|

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
            "attachmentId":"e5f0eab5cf694d4fb356c21a9bdaee48",
            "fileName":"1.jpeg",
            "contentType":"image/jpeg",
            "disposition":"attachment",
            "size":40375,
            "createdDt":1586849962000a
        }
    }
}
```
