## Contact Center > Online Contact > サービスガイド > 会員登録と基本設定

## クイックスタートガイド
管理者の方がOnline Contactの初期セットアップガイドに従い、Online Contactのさまざまな機能を体験しながら、
サービスの全容を理解できるよう、クイックスタートガイドを作成しています。
各機能の具体的で詳しい説明は、スライド下段右側にあるオンラインガイドのボタンからリンクしている詳細機能マニュアルページで、ご確認いただけます。（日本語版は準備でき次第、順次提供予定ですのでお待ちください。）
✨ <a href="https://docs.toast.com/ko/Contact%20Center/ko/OC_%EB%B9%A0%EB%A5%B8%EC%8B%9C%EC%9E%91%EA%B0%80%EC%9D%B4%EB%93%9C_%EB%B6%81%EB%A7%88%ED%81%AC%EC%B6%94%EA%B0%80.pdf" target="_blank">(管理者向け）クイックスタートガイド【韓国語】</a>


## TOAST会員登録
Online Contactは、TOAST会員登録後にご利用いただけます。
会員登録の際に決済手段の登録が必要ですので、クレジットカードをご用意ください。(**デビッドカード、プリペイド式カード、海外発行のクレジットカードは登録できません。**) 

![](http://static.toastoven.net/prod_contact_center/ja/1.3.1-(1)_ja.png)
**①** 会員登録の手続き: 約款同意 → 会員情報入力 → 登録完了 
**②** 会員登録が終わったら、マイページ → 決済方法に移動してクレジットカードの登録してください。


### 決済方法追加
![](http://static.toastoven.net/prod_contact_center/ja/1.3.1-(2)_ja.png)
![](http://static.toastoven.net/prod_contact_center/ja/1.3.1-(3)_ja.png)

**①** 決済方法としては、日本国内発行のクレジットカードの登録ができます。
デビッドカード、プリペイド式カードは登録できませんので、ご注意ください。


## サービス選択、組織およびドメイン設定
![](http://static.toastoven.net/prod_contact_center/ja/1.3.2-(1)_ja.png)
**①** 決済方法を登録した後、TOASTホームページ上段の**CONSOLE**ボタンをクリックするとCONSOLEに移動します。  


### 組織作成
![](http://static.toastoven.net/prod_contact_center/ja/1.3.2-(2)_ja.png)
**①** 上段のメニューで **組織を作成してください。** ボタンをクリックしてサービス使用のための最初の組織を作成した後、 **②** **サービス選択** タブを押すとサービス一覧を閲覧できます。
すでに組織を作成済みの場合は、サービス選択に移動してください。


### サービス選択
![](http://static.toastoven.net/prod_contact_center/ja/1.3.2-(3)_ja.png)
**①** Contact Center カテゴリ配下の **Online Contact**をクリックしてください。そのまま組織・ドメイン名の設定ステップに進むことができます。


### 組織/ドメイン名設定
![](http://static.toastoven.net/prod_contact_center/ja/1.3.2-(4)_ja.png)
**①** 組織名: 既存の組織名を使用するか、適切な組織名に修正、または追加してください。
**②** ドメイン: 英数字、ハイフン使用(最初の文字は英数字のみ可能、3~40文字以内)

`https://example.OC.toast.com/` という形式のドメインが生成され、このドメインがOnline Contactの **アクセスURL** として使用されます。
組織、ドメインのいずれにも重複する名前が存在する場合は使用できないため、必要に応じて修正してください。 作成完了後、右側の **保存** ボタンを押してください。


## IAM会員
![](http://static.toastoven.net/prod_contact_center/ja/1.3.3-(1)_ja.png)
**①** 組織名とドメイン名を設定した後、IAM会員を登録します。 **IAM会員登録** ボタンを押すと、会員情報を入力できるウィンドウが表示されます。

Online Contactの会員区分は2つです。
- TOAST会員: TOASTサイトに登録されている会員で、 **組織を管理するメンバー**です。
- IAM会員:: 組織内部のメンバーで、 **組織内でのみ有効なメンバー**です。 TOAST CONSOLE組織のメンバー管理→IAM会員タブから、追加登録が可能です。


### IAM会員登録
![](http://static.toastoven.net/prod_contact_center/ja/1.3.3-(2)_ja.png)
**①** IDと氏名、メールアドレスを入力して登録できます。また、複数のメンバーを登録することができます。 登録後、OWNERアカウントで使用するIAM会員に対しては、「権限設定」を編集し、組織単位サービス権限設定 > Online Contact にて**OWNERにチェック**を入れてください。


## サービスの初期設定完了、開通
![](http://static.toastoven.net/prod_contact_center/ja/1.3.4-(1)_ja.png)
Online Contactサービスの初期設定が完了しました。 表示される登録完了ページから
**① Online ContactアクセスURL**と、IAM会員のうち**OWNERに設定したID**を確認してください。今後、この情報を使ってアクセスすることができます。
**②** ログイン時のセキュリティ設定を行う場合、 [ログインセキュリティ設定ガイド](https://docs.toast.com/ja/TOAST/ja/console-guide/#iam)をご参照ください。

登録完了ページで確認したURLにアクセスするか、またはCONSOLEの組織ないのサービス利用状況 → Online Contactをクリックすると、ログインページが表示されます。 
同様に、登録完了ページで確認したOWNER IDでログインしてください。 IDにパスワードが設定されていないため、 **パスワード検索**（パスワード再設定機能）を先に実行してからログインできます。


### OWNER IDでログイン
![](http://static.toastoven.net/prod_contact_center/ja/1.3.4-(2)_ja.png)
**①** パスワードを忘れた時は、ここをクリックしIAM会員登録時に登録したメールアカウントに認証メールが送信することができます。 そのメールに記載されたURLにアクセスしてパスワードを新しく設定してください。
パスワードは、英数字·特殊文字を組み合わせた8~15桁で設定してください。
