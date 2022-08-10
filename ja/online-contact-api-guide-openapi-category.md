## Contact Center > Online Contact > プログラマーのためのAPIガイド > お問合せ

### 受付タイプリスト
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/api/v2/ticket/categories.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/api/v2/ticket/categories.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|受付タイプリスト |HTTPS  |GET    |UTF-8|JSON    |サービス内の受付タイプリスト照会|必要なし   |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	       |serviceId	|String	   |path	|O	|サービスID，URL PATH内に設定した{serviceId}|
|上位カテゴリーID	|parent	     |Integer	|query	 |X	 |上位カテゴリーに所属する下位カテゴリーリスト|
|下位カテゴリーID	|child	     |Integer	|query	 |X	 |下位カテゴリーに所属する上位カテゴリーリスト|
|言語コード	        |language	 |String	|query	 |X	 |サービスヘルプセンターの基本言語コード|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|categoryId	|Integer		|受付タイプID|
|	                |parent	    |Integer		|上位受付タイプID|
|	                |name	    |String		    |受付タイプ名|
|	                |level	    |Integer		|受付タイプレベル(1, 2, 3, 4, 5)|
|	                |path	    |String		    |受付タイプ経路(\\で各レベルのカテゴリーIDを接続)|
|	                |orderNo	|Integer		|表示手順|
|	                |languages	|Object		    |カテゴリー多言語名|

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
                "categoryId": 2536,	
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
                "categoryId": 2537,	
                "parent": 0,	
                "name": "유형2",	
                "level": 1,	
                "path": "\\",	
                "orderNo": 0,	
                "languages": {	
                    "ko": "유형2",	
                    "th": "พิมพ์2",	
                    "ja": "タイプ2",	
                    "en": "Type2",	
                    "zh": "类型2"	
                }	
            },	
            {	
                "categoryId": 2538,	
                "parent": 2536,	
                "name": "유형1-1",	
                "level": 2,	
                "path": "\\2536\\",	
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
                "categoryId": 2539,	
                "parent": 2536,	
                "name": "유형1-2",	
                "level": 2,	
                "path": "\\2536\\",	
                "orderNo": 0,	
                "languages": {	
                    "ko": "유형1-2",	
                    "th": "พิมพ์1-2",	
                    "ja": "タイプ1-2",	
                    "en": "Type1-2",	
                    "zh": "类型1-2"	
                }	
            },	
            {	
                "categoryId": 2540,	
                "parent": 2538,	
                "name": "유형1-1-1",	
                "level": 3,	
                "path": "\\2536\\2538\\",	
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
                "categoryId": 2541,	
                "parent": 2540,	
                "name": "유형1-1-1-1",	
                "level": 4,	
                "path": "\\2536\\2538\\2540\\",	
                "orderNo": 0,	
                "languages": {	
                    "ko": "유형1-1-1-1",	
                    "th": "พิมพ์1-1-1-1",	
                    "ja": "タイプ1-1-1-1",	
                    "en": "Type1-1-1-1",	
                    "zh": "类型1-1-1-1"	
                }	
            },	
            {	
                "categoryId": 2542,	
                "parent": 2541,	
                "name": "유형1-1-1-1-1",	
                "level": 5,	
                "path": "\\2536\\2538\\2540\\2541\\",	
                "orderNo": 0,	
                "languages": {	
                    "ko": "유형1-1-1-1-1",	
                    "th": "พิมพ์1-1-1-1-1",	
                    "ja": "タイプ1-1-1-1-1",	
                    "en": "Type1-1-1-1-1",	
                    "zh": "类型1-1-1-1-1"	
                }	
            }	
        ]	
    }	
}	
```

### 受付タイプフィールドリスト
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/api/v2/ticket/field/user/{categoryId}.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/api/v2/ticket/field/user/{categoryId}.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|受付タイプフィールドリスト |HTTPS  |GET    |UTF-8|JSON    |受付タイプで対応するフィールドリストを確認|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	    |serviceId	|String	   |path	 |O	|サービスID，URL PATH内に設定した{serviceId}|
|受付タイプID	|categoryId	|Integer   |path 	 |O	|受付タイプID, URL PATH内に設定した{categoryId}|
|言語コード	    |language	|String	   |query	 |X	|サービスヘルプセンターの基本言語コード|

#### 結果データ
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|fieldId	    |Integer		|顧客フィールドID|	
|                   |code	        |String  		|項目コード|
|	                |type	        |String		    |項目タイプ|
|	                |title	        |String		    |項目名|
|	                |description	|String		    |案内文句|
|	                |placeholder	|String		    |題語|
|	                |length	        |Integer		|最大長さ(0:長さ制限なし)|
|	                |required	    |Boolean		|必須項目かどうか(true: yes, false: no)|
|	                |encrypt	    |Boolean	 	|保存時に暗号化されているかどうか(true: yes, false: no)|
|	                |holdingText	|Boolean		|クリック時に削除するかどうか(true: yes, false: no)|
|	                |options	    |Array   		|テキストボックス, チェックボックス, ドロップボックス, 例:[区分1、区分2、...]|
|	                |value	        |String		    |ユーザー入力値|

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
                "fieldId": 1,		
                "code": "category",		
                "type": "dropdown",		
                "title": "유형",		
                "description": "",		
                "placeholder": "",		
                "length": 0,		
                "required": true,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 3,		
                "code": "mail",		
                "type": "text",		
                "title": "이메일",		
                "description": "",		
                "placeholder": "",		
                "length": 100,		
                "required": true,		
                "encrypt": true,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 5,		
                "code": "subject",		
                "type": "text",		
                "title": "제목",		
                "description": "",		
                "placeholder": "",		
                "length": 200,		
                "required": true,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 6,		
                "code": "content",		
                "type": "textarea",		
                "title": "문의내용",		
                "description": "",		
                "placeholder": "",		
                "length": 5000,		
                "required": true,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 2,		
                "code": "name",		
                "type": "text",		
                "title": "이름",		
                "description": "",		
                "placeholder": "",		
                "length": 100,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 4,		
                "code": "phone",		
                "type": "text",		
                "title": "전화번호",		
                "description": "",		
                "placeholder": "",		
                "length": 30,		
                "required": false,		
                "encrypt": true,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 9,		
                "code": "attachment",		
                "type": "file",		
                "title": "첨부파일",		
                "description": "10MB 이내 모든 이미지 및 허용된 문서 (MS office, hwp, pdf, txt)와 zip 파일을 5개까지 첨부가능합니다.",		
                "placeholder": "",		
                "length": 0,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 18,		
                "code": "typeOne",		
                "type": "text",		
                "title": "구분1",		
                "description": "",		
                "placeholder": "",		
                "length": 200,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 19,		
                "code": "typeTwo",		
                "type": "text",		
                "title": "구분2",		
                "description": "",		
                "placeholder": "",		
                "length": 200,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 720,		
                "code": "caption",		
                "type": "caption",		
                "title": "단순 텍스트 이름",		
                "description": "<div style=\"color:red\">단순 텍스트 설명</div>",		
                "placeholder": "<div style=\"font-size:20px;color:red\">단순 텍스트 내용</div>",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 721,		
                "code": "textbox",		
                "type": "text",		
                "title": "텍스트 박스 이름",		
                "description": "<div style=\"color:red\">텍스트 박스 설명</div>",		
                "placeholder": "텍스트 박스 자리 표시자",		
                "length": 50,		
                "required": true,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 722,		
                "code": "checkbox",		
                "type": "checkbox",		
                "title": "체크박스 이름",		
                "description": "체크박스 설명",		
                "placeholder": "",		
                "length": 50,		
                "required": false,		
                "encrypt": true,		
                "holdingText": true,		
                "options": [		
                    "옵션1",		
                    "옵션2",		
                    "옵션3"		
                ],		
                "value": null		
            },		
            {		
                "fieldId": 723,		
                "code": "dropdown",		
                "type": "dropdown",		
                "title": "드롭박스 이름",		
                "description": "드롭박스 설명",		
                "placeholder": "",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": [		
                    "옵션1",		
                    "옵션2",		
                    "옵션3"		
                ],		
                "value": null		
            },		
            {		
                "fieldId": 724,		
                "code": "radiobutton",		
                "type": "radio",		
                "title": "라디오 버튼 이름",		
                "description": "라디오 버튼 설명",		
                "placeholder": "",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": [		
                    "옵션1",		
                    "옵션2",		
                    "옵션3"		
                ],		
                "value": null		
            },		
            {		
                "fieldId": 725,		
                "code": "date",		
                "type": "date",		
                "title": "일자 이름",		
                "description": "일자 설명",		
                "placeholder": "2022-07-11",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 726,		
                "code": "datetime",		
                "type": "datetime",		
                "title": "일시",		
                "description": "일시",		
                "placeholder": "2022-07-11 00:00",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 727,		
                "code": "dateperiod",		
                "type": "date_period",		
                "title": "기간 일자 이름",		
                "description": "기간 일자 설명",		
                "placeholder": "2022-07-01 ~ 2022-07-31",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 728,		
                "code": "datetimeperiod",		
                "type": "datetime_period",		
                "title": "기간 일시 이름",		
                "description": "기간 일시 설명",		
                "placeholder": "2022-07-01 00:00 ~ 2022-07-31 23:59",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 729,		
                "code": "agreetotheterms",		
                "type": "agree",		
                "title": "동의하기 이름",		
                "description": "안내 문구",		
                "placeholder": "동의 문구",		
                "length": 50,		
                "required": false,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            },		
            {		
                "fieldId": 11,		
                "code": "personalAgree",		
                "type": "agree",		
                "title": "개인정보수집",		
                "description": "수집하는 개인 정보[(필수) 이메일, 휴대폰 번호, 문의내용, (선택) 첨부 파일]는 문의 내용 처리 및 고객 불만을 해결하기 위해 사용되며, <b><span style=\"font-size: 11pt;\">관련 법령에 따라 3년간 보관 후 삭제</span></b>됩니다. 문의 접수, 처리 및 회신을 위해 꼭 필요한 정보이므로 동의해 주셔야 서비스를 이용하실 수 있습니다.",		
                "placeholder": "위, 개인정보 수집 및 활용에 동의합니다.",		
                "length": 0,		
                "required": true,		
                "encrypt": false,		
                "holdingText": true,		
                "options": null,		
                "value": null		
            }		
        ]		
    }		
}		
```

### チケット添付ファイルアップロード
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket/attachments/upload.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket/attachments/upload.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット添付ファイルアップロード |HTTPS  |POST    |UTF-8|JSON    |サーバーにファイルアップロード|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID   |serviceId	|String	|path	    |O	|URL PATH内に設定した{serviceId}|
|アップロードファイル	|file	    |File	|formData	|O	|ファイルをformに提出。サポートするファイル形式: jpg, png, gif, bmp, jpeg, tif, tiff, pdf, txt, hwp, xls, xlsx, doc, docx, ppt, pptx, mp3, wav, zip. ファイルサイズ<10M、ファイル名長さ<100|

#### 結果データ(成功)
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|attachmentId	|String		|添付ファイルID|
|	            |fileName	    |String		|添付ファイル名|
|	            |contentType	|String		|添付ファイルタイプ|
|	            |disposition	|String		|ファイル処理方式(attachment: 添付ファイル)|
|	            |size	        |Long		|添付ファイルサイズ(byte)|
|               |createdDt	    |Long		|ファイル添付時間|

#### Response Body(成功)
```
  "header": {	
    "resultCode": 200,	
    "resultMessage": "",	
    "isSuccessful": true	
  },	
  "result": {	
    "content": {	
      "attachmentId": "8f0dc5854d2446b6aa2e6e41a0a2f55c",	
      "fileName": "image.png",	
      "contentType": "image/png",	
      "disposition": "attachment",	
      "size": 90576,	
      "createdDt": null	
    }	
  }	
}	
```

#### 結果データ(失敗)
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|exception	|String		|固定値：OcException|
|	            |message	|String		|エラーメッセージ(10MB以下のファイルのみ添付できます。 / ファイル名最大長超過。(100)/このファイル形式は添付できません。|

#### Response Body(失敗)
```
{
  "header": {
    "resultCode": 400,
    "resultMessage": "해당 파일 격식은 첨부할 수 없습니다.",
    "isSuccessful": false
  },
  "result": {
    "content": {
      "exception": "OcException",
      "message": "해당 파일 격식은 첨부할 수 없습니다."
    }
  }
}
```

### チケット作成
#### インターフェース説明
- URL: https://{domain}.oc.toast.com/{serviceId}/openapi/v1/ticket.json
- URL(開発): https://{domain}.alpha-oc.toast.com/{serviceId}/openapi/v1/ticket.json

|インターフェース名|プロトコル|呼び出し方向|エンコード|結果形式|インターフェース説明|アクセス制限可否|
|------------|-------|--------|-----|--------|--------------|------------|
|チケット作成 |HTTPS  |POST    |UTF-8|JSON    |新規チケットの作成|共通認証  |

#### リクエストパラメータ定義
|名称|変数|データタイプ|変数タイプ|必須|説明|
|----|----|----------|----------|----|---|
|サービスID	|serviceId	        |String	 |path	|O	|URL PATH内に設定した{serviceId}|
|チケット情報	|request body	    |Object	 |body	|O	|チケット情報(JSON)|
|カテゴリー	|categoryId	        |Integer |		|O	|カテゴリー(受付タイプ) ID|
|タイトル	    |subject	        |String	 |	    |O	|タイトル(max=255)|
|説明	    |content	        |String	 |	    |O	|原則として単純テキストのみ許容。Base64内容で提出する場合、チケット確認時の内容が多く問題になることがある。 画像は添付ファイル形式でアップロードするか、ファイルアップロード後htmlの img src=""/{serviceId}/api/v2/ticket/attachments/{attachmentId}""/ と呼んで使用|
|顧客情報	|endUser	        |Object	  |	     |O	 |顧客情報|
|ID	    |endUser.usercode	|String	  |	     |X	 |ID（会員固有ID）。 会員連動機能を使用する場合、プラットフォーム側のユーザー固有IDをusercodeとして使用することができ、該当usercodeを通じて会員の問い合わせ内訳を照会することができる。 非会員問い合わせの場合、値を転送する必要はない。|
|メール	    |endUser.email	    |String	  |	     |O	 |メール(サービス 管理 → チケット → メール設定メニューからメール情報を設定した場合、チケット処理時にそのメールアドレスから顧客にメール送信)|
|名前	    |endUser.username	        |String	  |	     |O	 |名前（メールパラメータ入力時、入力が必要。 入力しない場合はメール送信不可)|
|電話  	    |endUser.phone	            |String	  |	     |X  |電話|
|添付ファイル	|attachments	            |Array	  |      |X	 |添付ファイル(max 5件)|
|添付ファイルID|attachments.attachmentId	|String   |	 	 |O	 |添付ファイルID|
|区分1	    |typeOne	                |String	  |	     |X	 |区分1(拡張システムフィールド1)|
|区分2	    |typeTwo	                |String   |		 |X	 |区分2(拡張システムフィールド2)|
|言語	    |language	                |String	  |	     |X	 |言語|
|チャンネル	    |source	                    |String   |		 |X	 |チケットのチャンネル(web: ウェブ, spweb: モバイルウェブ, api: API, 基本値: web)|
|ユーザーフィールド	|userFields	            |Array	   |	  |X  |ユーザーフィールド|
|項目コード	    |userFields.code	    |String	   |	  |O  |ユーザーフィールド, 項目コード|
|ユーザー入力値	|userFields.value	    |String	   |      |O  |ユーザーフィールドのユーザー入力値|

userFields.value パラメータのフィールドタイプ別形式は下記のとおりです。

- text(単純テキスト): "ユーザー入力値"
- checkbox(チェックボックス): ["区分1"，"区分2"]
- dropdown(ドロップボックス): "区分1"
- radio(ラジオボタン): "区分1"
- date(日付): YYYY-MM-DD("2022-07-11")
- datetime(日時): YYYY-MM-DD HH:mm("2022-07-11 00:00")
- date_period(日付範囲): YYYY-MM-DD ~ YYYY-MM-DD("2022-07-01 ~ 2022-07-31")
- datetime_period(日時範囲): YYYY-MM-DD HH:mm ~ YYYY-MM-DD HH:mm("2022-07-01 00:00 ~ 2022-07-31 23:59")
- agree(同意する): true, false

#### Request Body
```
{	
    "categoryId": "2542", 	
    "subject": "유형", 	
    "content": "문의내용", 	
    "endUser": {	
        "usercode": "st18888", 	
        "email": "enduser_simple@nhn-st.com", 	
        "username": "이름", 	
        "phone": "13333333333"	
    }, 	
    "attachments": [	
        {	
            "attachmentId": "8f0dc5854d2446b6aa2e6e41a0a2f55c"	
        }	
    ], 	
    "typeOne": "구분1", 	
    "typeTwo": "구분2", 	
    "language": "ko", 	
    "source": "web", 	
    "userFields": [	
        {	
            "code": "textbox", 	
            "value": "텍스트 박스 이름"	
        }, 	
        {	
            "code": "checkbox", 	
            "value": [	
                "옵션1", 	
                "옵션2"	
            ]	
        }, 	
        {	
            "code": "dropdown", 	
            "value": "옵션1"	
        }, 	
        {	
            "code": "radiobutton", 	
            "value": "옵션1"	
        }, 	
        {	
            "code": "date", 	
            "value": "2022-07-11"	
        }, 	
        {	
            "code": "datetime", 	
            "value": "2022-07-11 00:00"	
        }, 	
        {	
            "code": "dateperiod", 	
            "value": "2022-07-01 ~ 2022-07-31"	
        }, 	
        {	
            "code": "datetimeperiod", 	
            "value": "2022-07-01 00:00 ~ 2022-07-31 23:59"	
        }, 	
        {	
            "code": "agreetotheterms", 	
            "value": "true"	
        }	
    ]	
}	
```

#### 結果データ(成功)
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.content	|ticketId	    |String		|チケットID|
|	            |categoryId	    |int		|受付タイプID|
|	            |subject	    |String		|チケットのタイトル|
|	            |content	    |String		|チケット内容|
|	            |status	        |String		|チケットの状態(固定値: new(アサイン待ち); open(処理中); closed(処理完了)|
|	            |createdDt	    |Long		|チケット作成時間|
|	            |updatedDt	    |Long		|チケットアップデート時間|
|	            |attachments	|Array		|添付ファイル|
|	            |attachments.attachmentId	|String		|添付ファイルID|
|	            |attachments.fileName	    |String		|添付ファイル名|
|	            |attachments.contentType	|String		|添付ファイルタイプ|
|               |attachments.disposition	|String		|ファイル処理方式(attachment:添付ファイル)|
|	            |attachments.size	        |String		|添付ファイルサイズ(byt)|
|	            |attachments.createdDt	    |String		|チケットアップデート時間|

#### Response Body(成功)
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
      "categoryName": null,	
      "categoryFullName": null,	
      "status": "new",	
      "statusName": null,	
      "content": "문의내용",	
      "createdDt": 1658199661151,	
      "updatedDt": 1658199661151,	
      "contents": null,	
      "attachments": [	
        {	
          "attachmentId": "8f0dc5854d2446b6aa2e6e41a0a2f55c",	
          "fileName": "image.png",	
          "contentType": "image/png",	
          "disposition": "attachment",	
          "size": 90576,	
          "createdDt": 1658192910000	
        }	
      ],	
      "displayDt": null	
    }	
  }	
}	
```

#### 結果データ(失敗)
|名称|変数|データタイプ|説明|
|-----|----|-----------|-------|
|result.contents	|objectName	|String		|ユーザーフィールド:項目コード|
|	                |field	    |String		|ユーザーフィールド:項目ID|
|	                |validate	|String		|invalid:無効な値、length:最大長超過、required:項目を入力してください。|
|	                |key	    |String		|"validate.ticket." + objectName + "." + validate|
|	                |message	|String		|"validate.ticket." + objectName + "." + validate|

#### Response Body(失敗)
```
{		
  "header": {		
    "resultCode": 400,		
    "resultMessage": null,		
    "isSuccessful": false		
  },		
  "result": {		
    "contents": [		
      {		
        "objectName": "mail",		
        "field": "3",		
        "validate": "invalid",		
        "key": "validate.ticket.mail.invalid",		
        "message": "validate.ticket.mail.invalid",		
        "rejectValue": ""		
      },		
      {		
        "objectName": "phone",		
        "field": "4",		
        "validate": "length",		
        "key": "validate.ticket.phone.length",		
        "message": "validate.ticket.phone.length",		
        "rejectValue": ""		
      },		
      {		
        "objectName": "textbox",		
        "field": "721",		
        "validate": "length",		
        "key": "validate.ticket.textbox.length",		
        "message": "validate.ticket.textbox.length",		
        "rejectValue": ""		
      },		
      {		
        "objectName": "checkbox",		
        "field": "722",		
        "validate": "invalid",		
        "key": "validate.ticket.checkbox.invalid",		
        "message": "validate.ticket.checkbox.invalid",		
        "rejectValue": ""		
      },		
      {		
        "objectName": "dropdown",		
        "field": "723",		
        "validate": "invalid",		
        "key": "validate.ticket.dropdown.invalid",		
        "message": "validate.ticket.dropdown.invalid",		
        "rejectValue": ""		
      }		
    ]		
  }		
}		
```
