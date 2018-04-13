# やること
Google Forms のフォームの回答が送信された時に、Slack チャンネルに内容が届くようにする

## このやりかたのよいところ
- **どんなフォームにも使える**
- **スクリプト（Google Apps Script）の知識は不要**
- **通知内容がきれいで見やすい**

# やりかた
## Slack に投稿するための URL を得る

まず Slack で、チャンネルに Google フォーム側が内容を送るための URL をもらいます。

- ブラウザで Slack の使いたいチャンネルを開く
    - まだ無かったら新しく作って開く
- チャンネル名をクリック
- 出てきたメニューの「**アプリを追加する**」（英語：**Add apps ...**）をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180403/20180403160604.png" width="252px">
<br/><br/>

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408163626.png" width="793px">

もしもこのような↑画面になったら、「**View App Directory**」をクリック


新しいタブが出たら、

- 検索ボックスに「**Incoming Webhooks**」と入力
- 「**着信 web フック**」（英語：Incoming Webhooks）をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408141130.png" width="795px">
<br/><br/>

- 「**設定を追加**」（英語：**Add Configuration**）をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408141344.png" width="799px">
<br/><br/>

- 使いたいチャンネル名が表示されていることを確認
- 「**着信 Web フック インテグレーションの追加**」（英語：**Add Incoming WebHooks integration**）をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408141609.png" width="801px">
<br/><br/>

- **Webhook URL** をコピーして、どこかに貼り付けておく（後で使います）

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408142322.png">
<br/><br/>

## フォームのスクリプトをつくる

ここまでで Slack での準備は終わりです。
次に Google フォームでの設定をしていきます。

#### スクリプトエディタを開く

- 使いたいフォームを開く
- 右上の点<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408145240.png" width="16px">をクリック
- 出てきたメニューの「**スクリプト エディタ**」をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408145034.png">
<br/><br/>

すると、このような新しいタブが出てきます。これがこのフォーム専用のスクリプトを書くところです。

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408145628.png">
<br/><br/>

#### コピペする

- 最初から書かれているスクリプト

```JavaScript
function myFunction() {

}
```
　　を消す

- その跡地に、[script.gs](./script.gs) をそのまま貼り付ける

#### Slack の情報を貼り付ける

ここまでで大体できたのですが、Slack のチャンネル名などは人それぞれなので、先ほどのコードの該当部分に入力します。

- ■１■ の部分に、**さっきどこかに貼り付けた URL** をコピーして貼り付ける
- ■２■ の部分（**２ヶ所**）に、使う **Slack チャンネル名** （一番最初に開いたチャンネル）を貼り付ける（例「#google-form」）

「■１■」「■２■」の文字は消して同じ位置にこれらを書いてください。

#### 通知のタイトルを設定する

- ★３★ を、**なんのフォームなのかの短い説明**に書き換える

１〜３全部で４ヶ所の書き換えです。

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408165039.png">

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408165042.png">

#### 保存する

- 左上の「**ファイル**」をクリック
- 出てきたメニューの「**保存**」をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408151614.png" width="463px">
<br/><br/>

- 適当な名前（基本的に使いません）を入力
- 「**OK**」をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408152012.png" width="646px">
<br/><br/>

## テスト
### Slack と繋がっていることを確認

- コードの上にある、「**関数を選択**」をクリック
- 出てきたメニューから「**test**」をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408152643.png" width="489px">


- 今のメニューの左の**虫ボタン**をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408153118.png" width="745px">
<br/><br/>

- ログインを求められたらログイン、許可を求められたら許可する

すると、許可が終わった途端に Slack に投稿が来ます。

- Slack を開いてメッセージを確認する

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408153332.png" width="453px">
<br/><br/>

さっき★３★のところに書いたタイトルが出ています。これで Slack との接続成功です。

### 実際の通知のテスト

#### フォーム送信時に自動で送るように設定

あとは、「Google フォームで回答が送信されたときに」Slack に送るという設定をします。

- スクリプト画面を開く
- 「関数を選択」だった部分を、「test」から「**onFormSubmit**」に変更する

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408155255.png" width="489px">
<br/><br/>

- **時計**のようなボタンをクリック
- 「**トリガーが設定されていません。今すぐ追加するにはここをクリックしてください。**」をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408165321.png">
<br/><br/>

- 「実行」のところだけ、「**onFormSubmit**」に変える
- 「保存」をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408160519.png">
<br/><br/>

- 承認を求められたら承認する
- スクリプトをもう一度保存する

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408161254.png" width="400px">
<br/><br/>

これで全て完成しました。

#### 最終確認

実際にフォームを使って、Slack に届くかどうか確かめましょう。
簡単にフォームの回答を行う方法は、フォーム編集画面からプレビューを開くことです。

- さっき開いたフォームのタブに戻る
- 上の**目ボタン**をクリック

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408153854.png" width="380px">
<br/><br/>

- フォームを埋めて送信する
- Slack を確認する

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408170628.png" width="720px">
こんな感じです。完成です。

# カスタマイズ
上の通知の見た目を少しだけ変える方法を紹介します。

#### Slackで表示される、メッセージの送信者名を変更

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408171632.png" width="327px">

スクリプトの、**// 1: bot 名** と書いてある行（５行目）の、`Googleフォーム Bot` を書き換えてください。

#### アイコン画像を変更

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408171639.png" width="305px">

スクリプトの、**// 2: アイコン画像** と書いてある行（12行目）を書き換えます。

- 画像を使う場合
    - 画像をどこかにアップロードしてURLを得る
    - 行をまるごと `"icon_url" : "画像のURL"` に書き換える

- Slack の絵文字を使う場合
    - `:envelope_with_arrow:` を他の絵文字名に書き換える

#### 左線の色を変更

Slack メッセージの画像に緑の縦線がありますが、この色は自由に変えられます。
デフォルトでは Slack が定める「good」色になっています。good な感じを表す色のようです。

スクリプトの、**// 3: 左線の色** と書いてある行（10行目）の `good` を、`#000000` 〜 `#FFFFFF` に変更すれば色が変わります。

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408172551.png" width="356px">

`#000000` （黒色）にした場合

#### 左右２列で表示するようにする

もしかすると、右上のこのへんの空白が無駄だと思われるかもしれません。
<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408172658.png" width="720px">

そこで、Slack では項目を**左右２列に分けて表示**させることができます。
その設定は Google フォームのスクリプトの中でします。

スクリプトの **// 4: 左右２列で表示** の行（66行目）の `false` を以下のように書き換えます。

- **全部２列**で表示する場合 `true`

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408173920.png" width="588px">


- **答えが30文字未満だった項目だけ２列にして、長い項目はそのまま**にする場合 `value.length < 30`
    - 文字数 `30` は自由に書き換えてください。

<img src="https://cdn-ak.f.st-hatena.com/images/fotolife/t/tsukino95/20180408/20180408173612.png" width="689px">

# 参考

[Googleformからのslack通知設定方法 - Qiita](https://qiita.com/pchan52/items/574e930a3cc42cf7f8b9)
