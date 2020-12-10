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
|並び順	|sort	   |String	|X	|並び順(基本値:updatedDt:desc; 形式変数:貞烈（昇順:asc, 降順:desc))|
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

### 유저 티켓 목록
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/{usercode}/list.json							
- URL (개발):	https://{domain}.alpha-oc.toast.co/{serviceId}/openapi/v1/ticket/{usercode}/list.json						

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|유저 티켓 목록 |HTTPS  |GET    |UTF-8|JSON    |검색 조건을 통해 조건에 맞는 사용자의 티켓 목록 조회|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	 |String	|O	|서비스 ID，URL PATH 내에 설정한 {serviceId}|
|유저 코드	|usercode	|String	|O	|유저 코드(유일한 값)，URL PATH 내에 설정한{usercode}|
|시작시간	|startDt	|String	|X	|검색 범위 시작시간(티켓 생성시간)(형식:yyyyMMddHHmmss）|
|종료시간	|endDt	    |String	|X	|검색 범위 종료시간(티켓 생성시간)(형식:yyyyMMddHHmmss）|
|티켓 ID	|ticketId	  |String	|X	|티켓 ID|
|제목	|subject	      |String	|X	|제목|
|티켓 상태	|status	    |String	|X	|티켓 상태（open:신규티켓; closed:처리완료）|
|접수유형	|categoryId	|Int	|X	|접수유형 ID（ID가 여러개 일 경우 , 로 분리）|
|정렬방식	|sort	    |String	|X	|정렬 순서(기본값:updatedDt:desc; 형식 변수:정렬（오름차순:asc, 내림차순:desc))|
|페이지	|page	     |Int	|X	|기본 값:1|
|1페이지 노출 건수	|pageSize	|Int	|X	|기본 값:10;max=200|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.contents	|ticketId	|String	|O	|티켓 ID|
|	                |serviceId	|String	|O	|서비스 ID|
|	                |subject	|String	|O	|티켓 제목|
|	                |categoryId	|Int	|X	|접수유형 ID|
|	                |categoryName	|String	|X	|접수유형 명|
|	                |status	|String	|O	|티켓 상태（open:신규티켓; closed:처리완료）|
|                   |createdDt	|Long	|O	|티켓 생성시간|
|	                |updatedDt	|Long	|O	|티켓 업데이트 시간|
|	                |addition	|String	|X	|기본 필드 외에 추가 된 필드 정보|
|result.total	    |total	|Long	|O	|총 건수|
|result.pages	    |pages	|Int	|O	|총 페이지수|
|result.pageNum	    |pageNum	|Int	|O	|현재 페이지|
|result.pageSize	|pageSize	|Int	|O	|1페이지 노출 건수|

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

### 티켓 첨부파일 첨부
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json			 							
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/upload.json									

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|첨부파일 첨부  |HTTPS  |GET    |UTF-8|JSON    |검색 조건을 통해 조건에 맞는 티켓 리스트 노출|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|첨부한 파일	|file	|File	|O	|첨부한 파일은 form 형태로 제출|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|첨부한 파일 ID|
|	            |fileName	    |String	|O	|파일 명|
|	            |contentType	|String	|O	|파일 유형|
|	            |disposition	|String	|O	|파일 처리방식（attachment:첨부파일）|
|	            |size	|Long	|O	|파일 크기|
|               |createdDt	|Long	|O	|파일 첨부 시간|

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

### 티켓 첨부파일 열기/다운로드
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}					 							
- URL (개발):	https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}												

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|첨부파일 열기/다운로드  |HTTPS  |GET    |UTF-8|JSON    |서버에 업로드된 파일 열기/다운로드|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|첨부한 파일 ID	|id	|String	|O	|첨부한 파일 id| 
|처리방식	|type	|String	|X	|기본 값은 브라우저로 열기（download:다운, open:브라우저로 열기）|

#### 결과 데이터
- 없음

#### Response Body
- File

### 티켓 첨부파일 삭제
#### 인터페이스 설명
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json						 							
- URL (개발): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/attachments/ticket/{id}.json														

|인터페이스 명|프로토콜|호출방향|인코딩|결과 형식|인터페이스 설명|접근제한 여부|
|------------|-------|--------|-----|--------|--------------|------------|
|첨부파일 삭제  |HTTPS  |DELETE    |UTF-8|JSON    |서버에 업로드된 파일 삭제|공통 인증   |

#### 요청 파라미터 정의
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|서비스 ID	|serviceId	|String	|O	|URL PATH 내에 설정한 {serviceId}|
|첨부한 파일 ID	 |id	|String	|O	|첨부한 파일 id|

#### 결과 데이터
|명칭	|변수	|데이터 타입	|필수	|설명|
|-----|-----|-----------|-----|---|
|result.content	|attachmentId	|String	|O	|첨부한 파일 id| 
|	            |fileName	|String	|O	|파일 명|
|	            |contentType	|String	|O	|파일 유형|
|	            |size	|Long	|O	|파일 크기|

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
