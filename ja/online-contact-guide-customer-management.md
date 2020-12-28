## Contact Center > Online Contact > サービスガイド >　顧客情報管理

![](http://static.toastoven.net/prod_contact_center/ja/2.2.7-(1)_ja.png)
電話でのお問い合わせを受領した時、番号に該当するお客様側の**顧客データ**を**APIに通じて照会**し、Online Contactの画面に表示できるようにするための機能です。
**① OPEN APIを有効化**してから利用できます。入力項目以下の通りです。

-	**②** OC IP情報メール送信: ユーザーを選択してメール送信ボタンを押すと、ファイアウォールオープンのためのOnlice ContactのIPアドレス情報がメールで送信されます。
-	**③** APIルート: APIパスのこと
-	**④** API方法: HTTPメソッドのGET/POSTから選択可能
-	**⑤** 暗号化設定: 暗号化の有無を指定
-	**⑥** 暗号化方式: 上記にチェックを入れた場合に、プルダウンで指定可能。
-	**⑦** 暗号化キー: ApiKey修正ボタンを押すと、新しいAPI Keyが生成されます。

情報の入力後、**保存**ボタンを押すとAPI情報が保存されます。連動のために必要なAPIに関するガイドは[APIガイド → 顧客情報](https://docs.toast.com/ja/Contact%20Center/ja/online-contact-api-guide-openapi-customer-data/)で確認いただけます。

### 顧客情報確認
![](http://static.toastoven.net/prod_contact_center/ja/2.2.7-(2)_ja.png)
顧客情報連動APIが有効になると、受付窓口が**電話**のチケットをクリックした場合、**① 顧客管理**タブが表示されます。
連動したAPIを通じ、照会した顧客情報はそのタブに表示され、電話による問い合わせあった場合、自動的に **① 顧客管理** タブにページが移動し、電話相談をしながら、対象顧客の情報を参照することができます。
