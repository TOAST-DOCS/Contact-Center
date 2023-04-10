## Contact Center > Online Contact > サービスガイド（お問合わせ管理） > 全体管理
お問合わせ管理サービスにおける全体管理メニューは、**契約サービス管理**、**組織管理者**、**会社情報管理**、**CTI管理**、**権限変更ログ管理**、**データ移管**メニューで構成されています。

## 契約サービス管理
### 契約管理

![](http://static.toastoven.net/prod_contact_center/ja/2.1.1-(1)_ja.png)
**契約管理**タブからOnline Contactを使用いただいている組織に**①**サービス追加、**②**サービス基本情報/契約内容の修正、**③**サービス使用の有効/無効切り替え、**④**サービス解約などの機能をご利用いただけます。

![](http://static.toastoven.net/prod_contact_center/2.1.1-(2)_3_ja.png)
**① サービス追加** ボタンをクリックすると、**② サービス追加画面**が表示されますので、基本情報を入力します。入力が必要な項目は次の通りです。

- **タイプ**: サービスのタイプ(お問い合わせ管理、イシュー管理)
- **サービス名**: 使用するサービスの名前
- **サービスID**: サービス識別で使うID(このIDがURLの文字列に含まれます）。英文のみ可能。
- **ヘルプセンター言語**: ヘルプセンター構成時に使用する言語セットの設定 (言語コード:ISO国際標準コードの入力が必要、下記**ISO国際標準コードリスト**参照)
- **タイムゾーン**: ヘルプセンターの属する時間帯
- **サービスバナー**: ファイル添付するとアップロードできます。この画像は、Online Contactの管理画面のサービス名のタブの画像として表示され、チャットサポート時にオペレーターのプロフィールとしても適用されます。
- **エディタタイプ**: 当該サービスで使用するエディタタイプで、**HTML/TEXT**から選択可能。チケットテンプレートや回答の作成、メールレイアウトの設定など、Online Contactの内部で提供されるテキストエディタに共通適用

![](http://static.toastoven.net/prod_contact_center/2.1.1-(2)_2_ja.png)
サービス追加時の設定項目のうち、**① ヘルプセンター言語**が2つ以上追加された場合は、ヘルプセンター上に**② 言語選択ドロップボックス**が追加され、**言語別のヘルプセンター**をお客様に提供することができます。

#### ISO国際標準言語コードリスト
ISO 639は、国際言語分類のために使用される標準化された表記法です。 言語コードを入力する時、以下のリストを参照してください。

<!-- 국가 코드 목록 html -->

<details markdown="1">
<summary> 言語コードリスト </summary>

<table>
<thead>
<tr>
<th>ISO言語名</th>
<th>言語名</th>
<th>言語コード</th>
</tr>
</thead>
<tbody>
<tr>
<td>Korean</td>
<td>한국어</td>
<td>ko</td>
</tr>
<tr>
<td>Japanese</td>
<td>日本語</td>
<td>ja</td>
</tr>
<tr>
<td>English</td>
<td>English</td>
<td>en</td>
</tr>
<tr>
<td>Chinese</td>
<td>中文</td>
<td>zh</td>
</tr>
<tr>
<td>Traditional Chinese</td>
<td>中文(繁體)</td>
<td>zh_TW</td>
</tr>
<tr>
<td>Cantonese</td>
<td>粵語</td>
<td>yue</td>
</tr>
<tr>
<td>Thai</td>
<td>ไทย</td>
<td>th</td>
</tr>
<tr>
<td>Vietnamese</td>
<td>Tiếng Việt</td>
<td>vi</td>
</tr>
<tr>
<td>Indonesian</td>
<td>Indonesia</td>
<td>id</td>
</tr>
<tr>
<td>Malay</td>
<td>Melayu</td>
<td>ms</td>
</tr>
<tr>
<td>Russian</td>
<td>русский</td>
<td>ru</td>
</tr>
<tr>
<td>French</td>
<td>français</td>
<td>fr</td>
</tr>
<tr>
<td>German</td>
<td>Deutsch</td>
<td>de</td>
</tr>
<tr>
<td>Spanish, Castilian</td>
<td>Español</td>
<td>es</td>
</tr>
<tr>
<td>Spanish (Latin America)</td>
<td>Español(Latinoamérica)</td>
<td>es_LA</td>
</tr>
<tr>
<td>Portuguese (Portugal)</td>
<td>Português</td>
<td>pt</td>
</tr>
<tr>
<td>Portuguese (Brazil)</td>
<td>Português(Brasil)</td>
<td>pt_BR</td>
</tr>
<tr>
<td>Italian</td>
<td>Italiano</td>
<td>it</td>
</tr>
<tr>
<td>Arabic</td>
<td>العربية</td>
<td>ar</td>
</tr>
<tr>
<td>Turkish</td>
<td>Türkçe</td>
<td>tr</td>
</tr>
<tr>
<td>Dutch, Flemish</td>
<td>Nederlands</td>
<td>nl</td>
</tr>
<tr>
<td>Polish</td>
<td>polski</td>
<td>pl</td>
</tr>
<tr>
<td>Abkhazian</td>
<td>аҧсшәа</td>
<td>ab</td>
</tr>
<tr>
<td>Afar</td>
<td>Afaraf</td>
<td>aa</td>
</tr>
<tr>
<td>Aragonese</td>
<td>aragonés</td>
<td>an</td>
</tr>
<tr>
<td>Assamese</td>
<td>অসমীয়া</td>
<td>as</td>
</tr>
<tr>
<td>Avaric,Avar</td>
<td>авар мацӀ</td>
<td>av</td>
</tr>
<tr>
<td>Avestan</td>
<td>avesta</td>
<td>ae</td>
</tr>
<tr>
<td>Aymara</td>
<td>aymar aru</td>
<td>ay</td>
</tr>
<tr>
<td>Bambara</td>
<td>bamanankan</td>
<td>bm</td>
</tr>
<tr>
<td>Bislama</td>
<td>Bislama</td>
<td>bi</td>
</tr>
<tr>
<td>Croatian</td>
<td>hrvatsk</td>
<td>hr</td>
</tr>
<tr>
<td>Bashkir</td>
<td>башҡорт теле</td>
<td>ba</td>
</tr>
<tr>
<td>Acoli</td>
<td>Lwo</td>
<td>ach</td>
</tr>
<tr>
<td>Afrikaans</td>
<td>Afrikaans</td>
<td>af</td>
</tr>
<tr>
<td>Akan</td>
<td>Akan</td>
<td>ak</td>
</tr>
<tr>
<td>Chamorro</td>
<td>Chamoru</td>
<td>ch</td>
</tr>
<tr>
<td>Azerbaijani</td>
<td>Azərbaycan</td>
<td>az</td>
</tr>
<tr>
<td>Chechen</td>
<td>нохчийн мотт</td>
<td>ce</td>
</tr>
<tr>
<td>Balinese</td>
<td>Basa Bali</td>
<td>ban</td>
</tr>
<tr>
<td>Sundanese</td>
<td>Basa Sunda</td>
<td>su</td>
</tr>
<tr>
<td>Cebuano</td>
<td>Binisayâ</td>
<td>ceb</td>
</tr>
<tr>
<td>Chuvash</td>
<td>чӑваш чӗлхи</td>
<td>cv</td>
</tr>
<tr>
<td>Bosnian</td>
<td>bosanski</td>
<td>bs</td>
</tr>
<tr>
<td>Cornish</td>
<td>Kernewek</td>
<td>kw</td>
</tr>
<tr>
<td>Breton</td>
<td>Brezhoneg</td>
<td>br</td>
</tr>
<tr>
<td>Catalan; Valencian</td>
<td>català</td>
<td>ca</td>
</tr>
<tr>
<td>Cree</td>
<td>ᓀᐦᐃᔭᐍᐏᐣ</td>
<td>cr</td>
</tr>
<tr>
<td>Czech</td>
<td>čeština</td>
<td>cs</td>
</tr>
<tr>
<td>Shona</td>
<td>chiShona</td>
<td>sn</td>
</tr>
<tr>
<td>Corsican</td>
<td>Corsu</td>
<td>co</td>
</tr>
<tr>
<td>Welsh</td>
<td>Cymraeg</td>
<td>cy</td>
</tr>
<tr>
<td>Divehi, Dhivehi, Maldivian</td>
<td>ދިވެހި</td>
<td>dv</td>
</tr>
<tr>
<td>Danish</td>
<td>dansk</td>
<td>da</td>
</tr>
<tr>
<td>Dzongkha</td>
<td>རྫོང་ཁ</td>
<td>dz</td>
</tr>
<tr>
<td>Yoruba</td>
<td>Èdè Yorùbá</td>
<td>yo</td>
</tr>
<tr>
<td>Estonian</td>
<td>eesti</td>
<td>et</td>
</tr>
<tr>
<td>Esperanto</td>
<td>Esperanto</td>
<td>eo</td>
</tr>
<tr>
<td>Basque</td>
<td>euskara</td>
<td>eu</td>
</tr>
<tr>
<td>Ewe</td>
<td>Èʋegbe</td>
<td>ee</td>
</tr>
<tr>
<td>Tagalog</td>
<td>Tagalog</td>
<td>tl</td>
</tr>
<tr>
<td>Filipino; Pilipino</td>
<td>Filipino</td>
<td>fil</td>
</tr>
<tr>
<td>Fijian</td>
<td>vosa Vakaviti</td>
<td>fj</td>
</tr>
<tr>
<td>Faroese</td>
<td>føroyskt</td>
<td>fo</td>
</tr>
<tr>
<td>Western Frisian</td>
<td>Frysk</td>
<td>fy</td>
</tr>
<tr>
<td>Fulah</td>
<td>Pular</td>
<td>ff</td>
</tr>
<tr>
<td>Ga</td>
<td>Gã</td>
<td>gaa</td>
</tr>
<tr>
<td>Irish</td>
<td>Gaeilge</td>
<td>ga</td>
</tr>
<tr>
<td>Gaelic; Scottish Gaelic</td>
<td>Gàidhlig</td>
<td>gd</td>
</tr>
<tr>
<td>Galician</td>
<td>galego</td>
<td>gl</td>
</tr>
<tr>
<td>Guarani</td>
<td>Avañe'ẽ</td>
<td>gn</td>
</tr>
<tr>
<td>Haitian; Haitian Creole</td>
<td>Kreyòl ayisyen</td>
<td>ht</td>
</tr>
<tr>
<td>Hausa</td>
<td>Hausa</td>
<td>ha</td>
</tr>
<tr>
<td>Hawaiian</td>
<td>ʻŌlelo Hawaiʻi</td>
<td>haw</td>
</tr>
<tr>
<td>Bemba</td>
<td>Chibemba</td>
<td>bem</td>
</tr>
<tr>
<td>Igbo</td>
<td>Igbo</td>
<td>ig</td>
</tr>
<tr>
<td>Herero</td>
<td>Otjiherero</td>
<td>hz</td>
</tr>
<tr>
<td>Rundi</td>
<td>Ikirundi</td>
<td>rn</td>
</tr>
<tr>
<td>Interlingua (International Auxiliary Language Association)</td>
<td>Interlingua</td>
<td>ia</td>
</tr>
<tr>
<td>Hiri Motu</td>
<td>Hiri Motu</td>
<td>ho</td>
</tr>
<tr>
<td>Xhosa</td>
<td>isiXhosa</td>
<td>xh</td>
</tr>
<tr>
<td>Zulu</td>
<td>isiZulu</td>
<td>zu</td>
</tr>
<tr>
<td>Icelandic</td>
<td>íslenska</td>
<td>is</td>
</tr>
<tr>
<td>Javanese</td>
<td>Jawa</td>
<td>jv</td>
</tr>
<tr>
<td>Interlingue, Occidental</td>
<td>Occidental</td>
<td>ie</td>
</tr>
<tr>
<td>Kinyarwanda</td>
<td>Ikinyarwanda</td>
<td>rw</td>
</tr>
<tr>
<td>Swahili</td>
<td>Kiswahili</td>
<td>sw</td>
</tr>
<tr>
<td>Klingon; tlhIngan-Hol</td>
<td>Klingon</td>
<td>tlh</td>
</tr>
<tr>
<td>Inupiaq</td>
<td>Iñupiaq</td>
<td>ik</td>
</tr>
<tr>
<td>Kongo</td>
<td>Kikongo</td>
<td>kg</td>
</tr>
<tr>
<td>Ido</td>
<td>Ido</td>
<td>io</td>
</tr>
<tr>
<td>Latin</td>
<td>Latin</td>
<td>la</td>
</tr>
<tr>
<td>Inuktitut</td>
<td>ᐃᓄᒃᑎᑐᑦ</td>
<td>iu</td>
</tr>
<tr>
<td>Latvian</td>
<td>latviešu</td>
<td>lv</td>
</tr>
<tr>
<td>Tonga (Tonga Islands)</td>
<td>lea fakatonga</td>
<td>to</td>
</tr>
<tr>
<td>Lithuanian</td>
<td>lietuvių</td>
<td>lt</td>
</tr>
<tr>
<td>Kalaallisut, Greenlandic</td>
<td>kalaallisut</td>
<td>kl</td>
</tr>
<tr>
<td>Lingala</td>
<td>lingála</td>
<td>ln</td>
</tr>
<tr>
<td>Lozi</td>
<td>Lozi</td>
<td>loz</td>
</tr>
<tr>
<td>Kanuri</td>
<td>Kanuri</td>
<td>kr</td>
</tr>
<tr>
<td>Luba-Lulua</td>
<td>Tshiluba</td>
<td>lua</td>
</tr>
<tr>
<td>Kashmiri</td>
<td>कॉशुर</td>
<td>ks</td>
</tr>
<tr>
<td>Ganda</td>
<td>Luganda</td>
<td>lg</td>
</tr>
<tr>
<td>Hungarian</td>
<td>magyar</td>
<td>hu</td>
</tr>
<tr>
<td>Malagasy</td>
<td>Malagasy</td>
<td>mg</td>
</tr>
<tr>
<td>Kikuyu, Gikuyu</td>
<td>Gĩkũyũ</td>
<td>ki</td>
</tr>
<tr>
<td>Maltese</td>
<td>Malti</td>
<td>mt</td>
</tr>
<tr>
<td>Norwegian</td>
<td>norsk</td>
<td>no</td>
</tr>
<tr>
<td>Komi</td>
<td>коми кыв</td>
<td>kv</td>
</tr>
<tr>
<td>Norwegian Nynorsk; Nynorsk, Norwegian</td>
<td>norsk nynorsk</td>
<td>nn</td>
</tr>
<tr>
<td>Pedi; Sepedi; Northern Sotho</td>
<td>Northern Sotho</td>
<td>nso</td>
</tr>
<tr>
<td>Chichewa; Chewa; Nyanja</td>
<td>chinyanja</td>
<td>ny</td>
</tr>
<tr>
<td>Kurdish</td>
<td>Kurdî</td>
<td>ku</td>
</tr>
<tr>
<td>Uzbek</td>
<td>Oʻzbek</td>
<td>uz</td>
</tr>
<tr>
<td>Kuanyama, Kwanyama</td>
<td>Kuanyama</td>
<td>kj</td>
</tr>
<tr>
<td>Occitan</td>
<td>Occitan</td>
<td>oc</td>
</tr>
<tr>
<td>Oromo</td>
<td>Oromoo</td>
<td>om</td>
</tr>
<tr>
<td>Luxembourgish, Letzeburgesch</td>
<td>Lëtzebuergesch</td>
<td>lb</td>
</tr>
<tr>
<td>Romanian; Moldavian; Moldovan</td>
<td>Română</td>
<td>ro</td>
</tr>
<tr>
<td>Romansh</td>
<td>Rumantsch</td>
<td>rm</td>
</tr>
<tr>
<td>Limburgan, Limburger, Limburgish</td>
<td>Limburgs</td>
<td>li</td>
</tr>
<tr>
<td>Quechua</td>
<td>Runa Simi</td>
<td>qu</td>
</tr>
<tr>
<td>Nyankole</td>
<td>Runyankore</td>
<td>nyn</td>
</tr>
<tr>
<td>Albanian</td>
<td>Shqip</td>
<td>sq</td>
</tr>
<tr>
<td>Luba-Katanga</td>
<td>Kiluba</td>
<td>lu</td>
</tr>
<tr>
<td>Slovak</td>
<td>slovenčina</td>
<td>sk</td>
</tr>
<tr>
<td>Slovenian</td>
<td>slovenščina</td>
<td>sl</td>
</tr>
<tr>
<td>Manx</td>
<td>Gaelg</td>
<td>gv</td>
</tr>
<tr>
<td>Somali</td>
<td>Soomaali</td>
<td>so</td>
</tr>
<tr>
<td>Sotho, Southern</td>
<td>Sesotho</td>
<td>st</td>
</tr>
<tr>
<td>Serbian</td>
<td>српски</td>
<td>sr</td>
</tr>
<tr>
<td>Serbian (Montenegro)</td>
<td>srpski(Crna Gora)</td>
<td>sr_ME</td>
</tr>
<tr>
<td>Serbian (Latin)</td>
<td>srpski(latinica)</td>
<td>sr_LN</td>
</tr>
<tr>
<td>Finnish</td>
<td>suomi</td>
<td>fi</td>
</tr>
<tr>
<td>Swedish</td>
<td>svenska</td>
<td>sv</td>
</tr>
<tr>
<td>Maori</td>
<td>te reo Māori</td>
<td>mi</td>
</tr>
<tr>
<td>Tswana</td>
<td>Setswana</td>
<td>tn</td>
</tr>
<tr>
<td>Marshallese</td>
<td>Kajin M̧ajeļ</td>
<td>mh</td>
</tr>
<tr>
<td>Tumbuka</td>
<td>Tumbuka</td>
<td>tum</td>
</tr>
<tr>
<td>Turkmen</td>
<td>türkmen dili</td>
<td>tk</td>
</tr>
<tr>
<td>Nauru</td>
<td>Dorerin Naoero</td>
<td>na</td>
</tr>
<tr>
<td>Twi</td>
<td>Twi</td>
<td>tw</td>
</tr>
<tr>
<td>Navajo, Navaho</td>
<td>Diné bizaad</td>
<td>nv</td>
</tr>
<tr>
<td>Wolof</td>
<td>Wolof</td>
<td>wo</td>
</tr>
<tr>
<td>Greek, Modern (1453–)</td>
<td>Ελληνικά</td>
<td>el</td>
</tr>
<tr>
<td>North Ndebele</td>
<td>isiNdebele</td>
<td>nd</td>
</tr>
<tr>
<td>Belarusian</td>
<td>беларуская</td>
<td>be</td>
</tr>
<tr>
<td>Bulgarian</td>
<td>български</td>
<td>bg</td>
</tr>
<tr>
<td>Ndonga</td>
<td>Owambo</td>
<td>ng</td>
</tr>
<tr>
<td>Kirghiz, Kyrgyz</td>
<td>кыргызча</td>
<td>ky</td>
</tr>
<tr>
<td>Norwegian Bokmål</td>
<td>Norsk Bokmål</td>
<td>nb</td>
</tr>
<tr>
<td>Kazakh</td>
<td>қазақ тілі</td>
<td>kk</td>
</tr>
<tr>
<td>Macedonian</td>
<td>македонски</td>
<td>mk</td>
</tr>
<tr>
<td>Sichuan Yi, Nuosu</td>
<td>ꆈꌠ꒿</td>
<td>ii</td>
</tr>
<tr>
<td>Mongolian</td>
<td>монгол</td>
<td>mn</td>
</tr>
<tr>
<td>South Ndebele</td>
<td>isiNdebele</td>
<td>nr</td>
</tr>
<tr>
<td>Tatar</td>
<td>татар</td>
<td>tt</td>
</tr>
<tr>
<td>Ojibwa</td>
<td>ᐊᓂᔑᓈᐯᒧᐎᓐ</td>
<td>oj</td>
</tr>
<tr>
<td>Tajik</td>
<td>тоҷикӣ</td>
<td>tg</td>
</tr>
<tr>
<td>Church&nbsp;Slavic, Old Slavonic, Church Slavonic, Old Bulgarian,&nbsp;Old&nbsp;Church&nbsp;Slavonic</td>
<td>ѩзыкъ словѣньскъ</td>
<td>cu</td>
</tr>
<tr>
<td>Ukrainian</td>
<td>Українська</td>
<td>uk</td>
</tr>
<tr>
<td>Georgian</td>
<td>ქართული</td>
<td>ka</td>
</tr>
<tr>
<td>Armenian</td>
<td>Հայերեն</td>
<td>hy</td>
</tr>
<tr>
<td>Ossetian, Ossetic</td>
<td>ирон ӕвзаг</td>
<td>os</td>
</tr>
<tr>
<td>Yiddish</td>
<td>ייִדיש</td>
<td>yi</td>
</tr>
<tr>
<td>Hebrew</td>
<td>עברית</td>
<td>he</td>
</tr>
<tr>
<td>Pali</td>
<td>पालि</td>
<td>pi</td>
</tr>
<tr>
<td>Uighur, Uyghur</td>
<td>ئۇيغۇرچە‎</td>
<td>ug</td>
</tr>
<tr>
<td>Urdu</td>
<td>اردو</td>
<td>ur</td>
</tr>
<tr>
<td>Pashto, Pushto</td>
<td>پښتو</td>
<td>ps</td>
</tr>
<tr>
<td>Sindhi</td>
<td>سنڌي</td>
<td>sd</td>
</tr>
<tr>
<td>Persian</td>
<td>فارسی</td>
<td>fa</td>
</tr>
<tr>
<td>Tigrinya</td>
<td>ትግርኛ</td>
<td>ti</td>
</tr>
<tr>
<td>Amharic</td>
<td>አማርኛ</td>
<td>am</td>
</tr>
<tr>
<td>Nepali</td>
<td>नेपाली</td>
<td>ne</td>
</tr>
<tr>
<td>Marathi</td>
<td>मराठी</td>
<td>mr</td>
</tr>
<tr>
<td>Hindi</td>
<td>हिन्दी</td>
<td>hi</td>
</tr>
<tr>
<td>Sanskrit</td>
<td>संस्कृतम्,&nbsp;𑌸𑌂𑌸𑍍𑌕𑍃𑌤𑌮𑍍</td>
<td>sa</td>
</tr>
<tr>
<td>Bengali</td>
<td>বাংলা</td>
<td>bn</td>
</tr>
<tr>
<td>Sardinian</td>
<td>sardu</td>
<td>sc</td>
</tr>
<tr>
<td>Punjabi, Panjabi</td>
<td>ਪੰਜਾਬੀ</td>
<td>pa</td>
</tr>
<tr>
<td>Gujarati</td>
<td>ગુજરાતી</td>
<td>gu</td>
</tr>
<tr>
<td>Northern Sami</td>
<td>Davvisámegiella</td>
<td>se</td>
</tr>
<tr>
<td>Oriya</td>
<td>ଓଡ଼ିଆ</td>
<td>or</td>
</tr>
<tr>
<td>Samoan</td>
<td>gagana fa'a Samoa</td>
<td>sm</td>
</tr>
<tr>
<td>Sango</td>
<td>yângâ tî sängö</td>
<td>sg</td>
</tr>
<tr>
<td>Tamil</td>
<td>தமிழ்</td>
<td>ta</td>
</tr>
<tr>
<td>Telugu</td>
<td>తెలుగు</td>
<td>te</td>
</tr>
<tr>
<td>Kannada</td>
<td>ಕನ್ನಡ</td>
<td>kn</td>
</tr>
<tr>
<td>Malayalam</td>
<td>മലയാളം</td>
<td>ml</td>
</tr>
<tr>
<td>Sinhala, Sinhalese</td>
<td>සිංහල</td>
<td>si</td>
</tr>
<tr>
<td>Lao</td>
<td>ລາວ</td>
<td>lo</td>
</tr>
<tr>
<td>Burmese</td>
<td>မြန်မာ</td>
<td>my</td>
</tr>
<tr>
<td>Central Khmer</td>
<td>ខ្មែរ</td>
<td>km</td>
</tr>
<tr>
<td>Cherokee</td>
<td>ᏣᎳᎩ</td>
<td>chr</td>
</tr>
<tr>
<td>Swati</td>
<td>SiSwati</td>
<td>ss</td>
</tr>
<tr>
<td>Tibetan</td>
<td>བོད་ཡིག</td>
<td>bo</td>
</tr>
<tr>
<td>Tsonga</td>
<td>Xitsonga</td>
<td>ts</td>
</tr>
<tr>
<td>Tahitian</td>
<td>Reo Tahiti</td>
<td>ty</td>
</tr>
<tr>
<td>Venda</td>
<td>Tshivenḓa</td>
<td>ve</td>
</tr>
<tr>
<td>Volapük</td>
<td>Volapük</td>
<td>vo</td>
</tr>
<tr>
<td>Walloon</td>
<td>Walon</td>
<td>wa</td>
</tr>
<tr>
<td>Zhuang, Chuang</td>
<td>Saɯ cueŋƅ</td>
<td>za</td>
</tr>
</tbody>
</table>

</details>

基本情報をすべて入力した後、次へボタンを押すと**③ 契約詳細内訳**に進みます。契約詳細の画面ではOnline Contactで提供される各種機能において、サービス内での**使用有無**を選択することができ、該当の選択有無を反映した**予算費用**をシミュレーションすることができます。契約詳細内訳の入力が完了した後、**契約ボタン**を押すと契約完了です。

![](http://static.toastoven.net/prod_contact_center/ja/2.1.1-(3)_ja.png)
サービス追加の時、サービスの基本情報入力や契約詳細内訳の入力のステップをすべて行わずに途中でやめると、サービス使用状態は**未使用**状態で、登録が完了していない状態では**登録**ボタンが表示されることがあります。サービス追加のためのステップを完了したサービスの場合、**①修正** ボタンで基本情報と契約情報を変更することができ、**②状態**ボタンからサービス使用有無の選択を、 **③解約** ボタンでサービス解約を進めることができます。サービスを解約したい時は、ステータスが あらかじめ**利用停止**に設定しておきますと、解約ボタンをクリックできるようになります。

契約情報は**一日に1回**だけ**修正可能**です。

### 料金管理
![](http://static.toastoven.net/prod_contact_center/ja/2.1.1-(4)_ja.png)
**料金管理**タブでは、全体、サービスタイプ別、およびサービス別の月ごとの請求料金を**① 検索**して照会することができます。サービスごとの情報を基準として照会すると、 **② サービスの利用状況**も一緒に表示されます。

✔ **\[FAQ]** [課金基準はどうなりますか。](https://nhn-contact.oc.toast.com/ocjp/hc/article/112/)
✔ **\[FAQ]** [料金はいつ、どのように決済されますか。](https://nhn-contact.oc.toast.com/ocjp/hc/article/111/)

## 組織情報
![](http://static.toastoven.net/prod_contact_center/2.1.1-(5)_ja.png)
**組織情報**タブでは、**① NHN Cloud 組織情報**、**② Online Contact 組織情報**のご確認が可能となります。

### NHN Cloud 組織情報
NHN Cloud 組織情報でご確認いただける内容は以下の通りです。
以下の情報はすべて **NHN Cloud Console → 組織設定 → 組織基本設定** タブでもご確認が可能で、該当タブでは組織名、ドメインを修正することもできます。

- **NHN Cloud 組織名**: 組織作成時に設定した名前
- **NHN Cloud 組織ID**: 組織作成時に各組織に付与される固有のID。Online Contact Open API使用時に必要な認証トークン作成に使用
- **NHN Cloud 組織ドメイン**: 組織作成後、サービス選択時に設定したドメイン名

### Online Contact 組織情報
Online Contact 組織情報でご確認いただける内容は以下の通りです。
**組織Key**は **API Key 変更**ボタンを通じてご変更が可能で、**Online Contact URL**は NHN Cloud 組織ドメインを利用して生成されるため、組織ドメイン変更時に一緒に変更されます。

- **Online Contact 組織Key**: サービスの登録/修正/削除など、組織管理レベルで行われる行為をOnline Contactの外部からAPIで処理しようとする場合、認証段階で使用されるKey
- **Online Contact URL**: Online Contact アクセスURL。https://**組織ドメイン**.oc.toast.com の形に作成

## 組織管理者
![](http://static.toastoven.net/prod_contact_center/ja/2.1.2-(1)_ja.png)
**組織管理者**は Online Contactを使用する組織を管理できる権限を持ち、オペレーターの追加・削除、そしてオペレーターの中から組織管理者を追加・削除等の操作ができます。
組織管理者の権限だけではオペレーション機能とサービス管理機能を利用することはできません。別の作業者にオペレーションの進行やサービスの初期セットアップをさせたい場合は、 [サービス管理 → オペレーター] メニューで管理者またはオペレーターの権限を追加してください。 
組織管理者の権限を持たせるには、あらかじめIAM会員として登録されている必要があります。

✔ **\[FAQ]** [権限の種類と違いを知りたいです。](https://nhn-contact.oc.toast.com/ocjp/hc/article/73/)

### IAM会員登録

- 画面右上の **① 会員招待** ボタン → 名前、ID、メールアドレスを入力
- NHN Cloud CONSOLE → メンバー管理 → IAM会員タブ → **IAM会員登録** ボタン → ID、名前、メール、携帯番号入力

上記の２つの方法のうちどちらかの方法でIAM会員を登録し、 ② 画面左上の **組織管理者追加** ボタン → **オペレーター照会** ボタン → 登録されたIAM会員の名前/アカウント/メールの位置、一部情報を入力して照会することができます。

**会員招待** ボタンまたはNHN Cloud CONSOLEで登録されたIAM会員の場合、入力されたメールアドレスにパスワード変更メールが送信され、該当メールにパスワードを設定してからログインすることができます。

## 会社情報管理
![](http://static.toastoven.net/prod_contact_center/2.2.5-(6)_2_ja.png)
PC、モバイルヘルプセンターのフッター領域に、会社情報および利用約款を表示できるように設定可能な機能です。
**① 追加** ボタンを押すと設定画面が表示され、**② 会社情報**、**③ 商標及び著作権**、**④ 利用規約** 情報を設定できます。
情報入力後、**保存**ボタンを押すと、設定した会社情報構成がリストに追加され、サービス管理 → ヘルプセンター → 基本設定メニューから選択し、実際のヘルプセンターに **⑤ 反映**することができます。

## CTI管理
CTI管理メニューでは、Online  Contactと接続するCTI情報を設定し、電話相談を行う各相談員のCTI  IDとCTI  NOを入力及び修正することができます。
このメニューは、契約情報で**チケット管理→電話含む(❖CTI利用含む)** 機能を**使用**に設定したサービスでのみ照会できます。

### CTI設定
![](http://static.toastoven.net/prod_contact_center/2.1.2-(2)_1_ja.png)
CTI設定メニューからOnline  Contactの電話機能と関連付けるCTIを設定できます。

お選びいただける**① CTIバージョン**は以下のとおりです。

- IPCC (Private): Privateサービスでご利用されたい場合はOnline  Contact顧客センターにて**事前協議**をお願いいたします。([Online Contactお客様センター](https://nhn-contact.oc.toast.com/ocjp/hc/))
- Mobile Contact: NHN Cloud Consoleで**Mobile  Contactサービスを有効化**した後選択することができます。

CTIバージョンを選択し、IPCCまたはMobile  Contact管理担当者から受け取った**テナントID**、**サービス名**を**② テナントID**、**③ テナント名**欄に入力してください。
**④ CTI Log モニタリング**機能有効な場合、一日単位で CTI ログが記録され、記録されたログは、画面右上にあるアカウント名をクリックすると利用できる **CTI Log ダウンロード**機能を通じて、エクセルファイルの形でダウンロードすることができます。

### CTIオペレーター管理
![](http://static.toastoven.net/prod_contact_center/2.1.2-(3)_1_ja.png)
当組織に登録されたオペレーターのうち、電話相談を行うオペレーターにCTI情報を与えることができます。

メニュー接続時にリストには、当該組織に登録されたオペレーターのうち、1つ以上のサービスで電話権限が付与されたオペレーターが表示されます。
名前、メール、CTI ID、CTI NO、サービス情報でオペレーターを **① 検索**することができ、**② 修正**ボタンでCTI IDとCTI NOを入力または修正することができます。（CTI ID、CTI NOはオペレーター間の重複ができません。）オペレーターにCTI情報が正常に入力された場合、電話ウィジェットからCTIログインを進めることができます。

CTI情報の取得が難しい場合は、Online Contactお客様センターまでお問い合わせください。([Online Contactお客様センター](https://nhn-contact.oc.toast.com/oc/hc/))

## 権限変更ログ管理
![](http://static.toastoven.net/prod_contact_center/2.1.4-(1)_ja.png)
① ヘルプセンター組織内部のオペレーター**権限を変更**する時のログが保存されます。組織管理者または管理者が権限の変更を行ったログを管理するメニューです。操作日時、操作内容、名前、IP、サービス、IDの項目から対象を絞りこんで**② 検索**することができます。

## データ移管
![](http://static.toastoven.net/prod_contact_center/2.1.6-(2)_ja.png)
Online Contactへの相談データの移管が必要な場合は、**データ移管**メニューからエクセルファイル形式で整理されたデータをアップロードして、Online Contact内にチケットとして生成することができます。

**① 追加** ボタンをクリックすると、**テンプレートダウンロード** 画面が表示されます。 相談データを移管したいサービスを選択した後、**② ダウンロード**ボタンをクリックすると、当該サービスの移管テンプレートをダウンロードできます。 データ移管テンプレートの場合、ダウンロード当時に当該サービスに設定されたフィールド構成が反映されるため、フィールド構成が変更された場合はテンプレートを新たにダウンロードして作成してください。

テンプレートダウンロード画面で**次**ボタンをクリックすると、**データアップロード**画面が表示されます。 
**③ 追加** ボタンをクリックすると作成したファイルをアップロードでき、データを移管したいサービスとファイル名をもう一度確認した後、 **④ 確認** ボタンをクリックするとデータ登録が完了します。

移管処理前までは、移管予約内訳の**削除**が可能で、データ移管が完了した場合、削除ボタンは無効化処理されます。

## My 業績
![](http://static.toastoven.net/prod_contact_center/2.1.4-(2)_ja.png)
Online Contact画面右上に表示された**① アカウント名**をクリックすると、**② My実績**メニューにアクセスすることができます。

該当メニューより、**現在接続中のサービス**でのチケット、電話、チャット相談に関する詳細な**リアルタイム累積データ**をご照会いただけます。

相談タイプによって表示される詳細な実績区分は以下のとおりです。

**③ チケット実績**

- アサイン待ち
- 処理中
- 解決
- 完了

**④ 電話実績**

- IB通話(件数/時間)
- OB通話(件数/時間)
- 待機
- 転送
- チケット処理
- チャット処理
- 休憩
- 食事
- 教育
- 報告
- 会議
- モニター

**⑤ チャット実績**

- 待機
- オンライン
- 休憩

## ユーザー設定
![](http://static.toastoven.net/prod_contact_center/ja/2.1.5-(1)_ja.png)
Online Contact画面右上に表示されている **① アカウント名**をクリックすると **② 個人情報設定**メニューが開きます。このメニューではヘルプセンターにログインしているユーザー自身の個人情報設定を閲覧・変更できます。

✔ **\[FAQ]** [ID、メール、名前を変更または削除したいです。](https://nhn-contact.oc.toast.com/ocjp/hc/article/70/)
✔ **\[FAQ]** [パスワードを変更したいです。](https://nhn-contact.oc.toast.com/ocjp/hc/article/72/)

### 閲覧可能な情報

- アカウント 
- 名前
- ニックネーム(変更可能): チャットまたはメール処理時に表示される項目
- 電話番号
- メールアドレス
- 言語選択(変更可能): サービスの言語設定とは別にユーザー環境での言語選択
- チケット割当(変更可能): 休暇などでチケットを担当できない場合、チケットの割当可否の設定可能
