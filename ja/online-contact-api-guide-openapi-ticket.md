## Contact Center > Online Contact > プログラマーのためのAPIガイド > お問合せ履歴 

### 顧客チケットリスト
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/enduser/{usercode}/list.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/enduser/{usercode}/list.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|顧客チケットリスト |HTTPS  |POST    |UTF-8|JSON    |検索条件により、条件に合った顧客のチケットリストを露出|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	       |serviceId	|String	    |path	|O	|サービスID，URL PATH内に設定した{serviceId}|
|ユーザーコード	       |usercode	|String	    |path	|O	|ユーザーコード(唯一の値)，URL PATH内に設定した{usercode}|
|カテゴリーID	   |categoryId	|Integer	|query	|X	|カテゴリー（受付タイプ）ID|
|チケットの状態	       |status	    |String  	|query	|X	|チケットの状態. new: アサイン待ち, open: 処理中, reply: 保留, solved: 解決, closed: 完了|
|言語コード	       |language	|String	    |query	|X	|サービスヘルプセンターの基本言語コード|
|チャンネル	           |source  	|String 	|query	|X	|お問い合わせチャンネル(web:PCウェブ、spweb:モバイルウェブ、api:API)。 複数のチャンネル照会時にコンマを通じて使い分け（例:web,spweb,api）。 デフォルト値はweb,spweb,api|
|整列方式	       |sort	     |String	|query	|X	|整列順序(デフォルト:updatedDt:desc;整列形式:昇順:asc、降順:desc)|
|ページ	           |page	     |Integer	|query	|X	|基本値: 1|
|1ページあたりの露出件数	|pageSize	  |Integer	 |query	 |X	 |基本値: 10; max=200|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|ticketId	        |String		    |チケットID|
|	                |subject	        |String		    |チケットのタイトル|
|	                |categoryId	        |Integer		|受付タイプID|
|	                |categoryName	    |String		    |受付タイプ名|
|	                |categoryFullName	|String		    |カテゴリー全体経路(>で各レベルを接続)|
|	                |status 	        |String		    |チケットの状態. new: アサイン待ち, open: 処理中, reply: 保留, solved: 解決, closed: 完了|
|	                |statusName	        |String		    |チケットの状態名|
|	                |createdDt	        |Long		    |チケット作成時間|
|	                |updatedDt	        |Long		    |チケットアップデート時間|
|	                |displayDt	        |String		    |露出時間(yyyy.MM.dd)|
|result 	        |total	            |Integer		|総件数|
|	                |pages	            |Integer		|総ページ数|
|	                |pageNum	        |Integer		|現在のページ|
|                   |pageSize	        |Integer		|1ページあたりの露出件数|

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
        "ticketId": "T1658213182227yb9hI",		
        "subject": "유형11",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "reply",		
        "statusName": "추가 확인",		
        "content": null,		
        "createdDt": 1658213182000,		
        "updatedDt": 1658215682000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T16582131010751o8BM",		
        "subject": "유형10",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "solved",		
        "statusName": "답변 완료",		
        "content": null,		
        "createdDt": 1658213101000,		
        "updatedDt": 1658215702000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T1658213078429EFmxm",		
        "subject": "유형9",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "closed",		
        "statusName": "최종 완료",		
        "content": null,		
        "createdDt": 1658213078000,		
        "updatedDt": 1658215720000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T1658213060072Witj6",		
        "subject": "유형8",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "open",		
        "statusName": "문의 확인",		
        "content": null,		
        "createdDt": 1658213060000,		
        "updatedDt": 1658215646000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T1658212816320fVxqS",		
        "subject": "유형7",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "new",		
        "statusName": "접수 완료",		
        "content": null,		
        "createdDt": 1658212816000,		
        "updatedDt": 1658212816000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T1658211072628h00Qf",		
        "subject": "유형6",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "new",		
        "statusName": "접수 완료",		
        "content": null,		
        "createdDt": 1658211073000,		
        "updatedDt": 1658211073000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T1658211058049HP1U0",		
        "subject": "유형5",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "new",		
        "statusName": "접수 완료",		
        "content": null,		
        "createdDt": 1658211058000,		
        "updatedDt": 1658211058000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T165821104308563aoM",		
        "subject": "유형4",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "new",		
        "statusName": "접수 완료",		
        "content": null,		
        "createdDt": 1658211043000,		
        "updatedDt": 1658211043000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T1658211028245FwMKd",		
        "subject": "유형3",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "new",		
        "statusName": "접수 완료",		
        "content": null,		
        "createdDt": 1658211028000,		
        "updatedDt": 1658211028000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      },		
      {		
        "ticketId": "T1658211012753VCyy2",		
        "subject": "유형2",		
        "categoryId": 2542,		
        "categoryName": "유형1-1-1-1-1",		
        "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
        "status": "new",		
        "statusName": "접수 완료",		
        "content": null,		
        "createdDt": 1658211013000,		
        "updatedDt": 1658211013000,		
        "contents": null,		
        "attachments": null,		
        "displayDt": "2022.07.19"		
      }		
    ],		
    "total": 12,		
    "pages": 2,		
    "pageNum": 1,		
    "pageSize": 10		
  }		
}		
```

### チケット詳細
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/detail.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/detail.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット詳細  |HTTPS  |GET    |UTF-8|JSON    |顧客が受け付けたチケット詳細照会|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	|String	|path	|O	|サービスID，URL PATH内に設定した{serviceId}|
|ID	    |usercode	|String	|path	|O	|ID(ユーザー固有ID)、お問い合わせ受付時のusercode|
|チケットID	|ticketId	|String	|path	|O	|チケットID|
|言語コード	|language	 |String	|query	|X	|サービスヘルプセンターの基本言語コード|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|ticketId	|String		    |チケットID|
|	            |subject	|String		    |サービスID|
|	            |categoryId	|Integer		|カテゴリー（受付タイプ）ID|
|	            |categoryName	|String		|カテゴリー名|
|	            |categoryFullName	|String		|カテゴリー全体経路(>で各レベルを接続)|
|	            |status	            |String		|チケットの状態. new: アサイン待ち, open: 処理中, reply: 保留, solved: 解決, closed: 完了|
|	            |statusName	        |String		|チケットの状態名|
|	            |content	        |String		|問い合わせ内容|
|	            |createdDt	        |Long		|作成時間|
|	            |updatedDt	        |Long		|修正時間|
|	            |contents	        |Array		|チケット詳細|
|	            |contents.content	|String		|内容詳細|
|	            |contents.type	    |String		|お問い合わせタイプ。enduser:お問い合わせ(受付完了)、csuser:回答(受付完了)|
|	            |contents.typeName	|String		|内容タイプ名|
|	            |contents.createdDt	|Long		|チケット処理時間|
|	            |contents.displayDt	|String		|内容露出時間(yyyy.MM.dd)|
|	            |contents.attachments	|Array		|チケット処理内容の添付ファイル|
|	            |contents.attachments.attachmentId	|String		|チケット処理内容の添付ファイルID|
|	            |contents.attachments.fileName	    |String		|チケット処理内容の添付ファイル名|
|	            |contents.attachments.contentType	|String		|チケット処理内容の添付ファイルタイプ|
|	            |contents.attachments.disposition	|String		|チケット処理内容の添付ファイル処理方式(attachment:添付ファイル)|
|	            |contents.attachments.size	        |Long		|チケット処理内容の添付ファイルサイズ|
|	            |contents.attachments.createdDt	    |Long		|チケット処理内容の添付ファイルのアップロード時間|
|	            |attachments	                    |Array		|チケットお問い合わせの添付ファイル|
|	            |attachments.attachmentId	        |String		|チケットお問い合わせの添付ファイルID|
|               |attachments.fileName	            |String		|チケットお問い合わせの添付ファイル名|
|	            |attachments.contentType	        |String		|チケットお問い合わせの添付ファイルタイプ|
|	            |attachments.disposition	        |String		|チケットお問い合わせの添付ファイル処理方式(attachment:添付ファイル)|
|	            |attachments.size	                |Long		|チケットお問い合わせの添付ファイルサイズ|
|	            |attachments.createdDt	            |Long		|チケットお問い合わせの添付ファイルのアップロード時間|
|	            |displayDt	                        |String		|露出時間(yyyy.MM.dd)|
|result	        |total	                            |Integer	|総件数|
|	            |pages	                            |Integer	|総ページ数|
|	            |pageNum	                        |Integer	|ページ|
|	            |pageSize	                        |Integer	|1ページあたりの露出件数|

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
      "ticketId": "T1658199661153IXTfw",		
      "subject": "유형",		
      "categoryId": 2542,		
      "categoryName": "유형1-1-1-1-1",		
      "categoryFullName": "유형1>유형1-1>유형1-1-1>유형1-1-1-1>유형1-1-1-1-1",		
      "status": "solved",		
      "statusName": "답변 완료",		
      "content": "문의내용",		
      "createdDt": 1658199661000,		
      "updatedDt": 1658279983000,		
      "contents": [		
        {		
          "content": "<p>solved</p>",		
          "type": "reply",		
          "typeName": "답변",		
          "createdDt": 1658279983000,		
          "displayDt": "2022.07.20",		
          "attachments": [		
            {		
              "attachmentId": "a9e126cf01654631acc2d1e56e8c694e",		
              "fileName": "image.png",		
              "contentType": "image/png",		
              "disposition": "attachment",		
              "size": 90576,		
              "createdDt": 1658279969000		
            }		
          ]		
        },		
        {		
          "content": "<p>append commnet</p>",		
          "type": "enduser",		
          "typeName": "질문",		
          "createdDt": 1658279813000,		
          "displayDt": "2022.07.20",		
          "attachments": null		
        },		
        {		
          "content": "<p>append comment</p>",		
          "type": "enduser",		
          "typeName": "질문",		
          "createdDt": 1658216460000,		
          "displayDt": "2022.07.19",		
          "attachments": null		
        },		
        {		
          "content": "<p>solved</p>",		
          "type": "reply",		
          "typeName": "답변",		
          "createdDt": 1658216406000,		
          "displayDt": "2022.07.19",		
          "attachments": null		
        }		
      ],		
      "attachments": null,		
      "displayDt": "2022.07.19"		
    }		
  }		
}		
```

### チケット添付ファイルを開く/ダウンロード
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/api/v2/ticket/attachments/{id}		
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/api/v2/ticket/attachments/{id}									

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット添付ファイルを開く/ダウンロード  |HTTPS  |GET    |UTF-8|JSON    |チケット添付ファイルを開く/ダウンロード|必要なし  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	    |serviceId	|String	|path   |O	|サービスID，URL PATH内に設定した{serviceId}|
|添付ファイルID	|id	        |String	|path   |O	|添付ファイルID, URL PATH内に設定した{id}| 
|処理方式	    |type	    |String	|query  |X	|デフォルト値:ブラウザで開く。（download:ダウンロード、open:ブラウザで開く）|

#### 結果データ
File

### 顧客再問合せ
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/comment.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/enduser/{usercode}/{ticketId}/comment.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|顧客再問合せ  |HTTPS  |POST    |UTF-8|JSON    |チケットIDを基準に再お問い合わせ|共通認証|

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	|String	|path	|O	|サービスID，URL PATH内に設定した{serviceId}|
|ID    |usercode	|String	|path	|O	|ID(ユーザー固有ID)、お問い合わせ受付時のusercode|
|チケットID	|ticketId	|String	|path	|O	|チケットID|
|内容	    |comment	|String	|body	|O	|再問合せの内容|
|첨부파일	|attachments	|String	|query	|X	|添付ファイルID。複数のファイル添付時にファイルIDを(,)から分離、maxは5件(ファイルID1,ファイルID2,...、ファイルID5)|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|content	|String		|再問合せの内容|
|	            |type	    |String		|固定値: enduser|
|               |typeName	|String		|タイプ名称|
|	            |createdDt	|Long		|提出時間|
|	            |displayDt	|String		|露出時間(yyyy.MM.dd)|
|	            |attachments	|Array		|添付ファイル|
|	            |attachments.attachmentId	|String		|添付ファイルID|
|	            |attachments.fileName	    |String		|添付ファイル名|
|	            |attachments.contentType	|String		|添付ファイルタイプ|
|	            |attachments.disposition	|String		|添付ファイル処理方式(attachment:添付ファイル)|
|	            |attachments.size	        |Long		|添付ファイルサイズ|
|	            |attachments.createdDt	    |Long		|添付ファイルのアップロード時間|

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
      "content": "<p>append comnment</p>",		
      "type": "enduser",		
      "typeName": null,		
      "createdDt": 1658286589999,		
      "displayDt": null,		
      "attachments": [		
        {		
          "attachmentId": "a9e126cf01654631acc2d1e56e8c694e",		
          "fileName": "image.png",		
          "contentType": "image/png",		
          "disposition": "attachment",		
          "size": 90576,		
          "createdDt": 1658279969000		
        }		
      ]		
    }		
  }		
}		
```