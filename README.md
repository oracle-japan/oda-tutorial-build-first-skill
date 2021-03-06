# Oracle Digital Assistant - はじめてのスキル開発

## 目次

<!-- TOC -->
  - [はじめに](#%E3%81%AF%E3%81%98%E3%82%81%E3%81%AB)
  - [スキルの作成](#%E3%82%B9%E3%82%AD%E3%83%AB%E3%81%AE%E4%BD%9C%E6%88%90)
  - [インテントの作成](#%E3%82%A4%E3%83%B3%E3%83%86%E3%83%B3%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)
  - [モデルのテスト](#%E3%83%A2%E3%83%87%E3%83%AB%E3%81%AE%E3%83%86%E3%82%B9%E3%83%88)
  - [エンティティの作成](#%E3%82%A8%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3%E3%81%AE%E4%BD%9C%E6%88%90)
  - [ダイアログ・フローのデザイン](#%E3%83%80%E3%82%A4%E3%82%A2%E3%83%AD%E3%82%B0%E3%83%95%E3%83%AD%E3%83%BC%E3%81%AE%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3)
  - [スキルのテスト](#%E3%82%B9%E3%82%AD%E3%83%AB%E3%81%AE%E3%83%86%E3%82%B9%E3%83%88)

<!-- /TOC -->

## はじめに

Oracle Digital Assistant は、AI を活用したチャットボットの構築をシンプルにするプラットフォームとツールを提供します。

このチュートリアルでは、ピザの注文を受け付ける基本的なスキルの作成をとおして、Oracle Digital Assistant の次の機能について説明します:

* インテントとエンティティの定義
* NLP エンジンのトレーニングとテスト
* ダイアログ・フローの設計と編集、検証
* スキルのテスト

### このチュートリアルの表記方法

このチュートリアルで使用している表記方法は次のとおりです。

| 表記方法 | 説明 |
|---|---|
| **「太字」** | ボタン、各種フィールドのラベルなどの GUI 要素 |
| `固定幅フォント` | サンプルコード、入力するテキスト |

[目次に戻る](#%E7%9B%AE%E6%AC%A1)

## スキルの作成

このチュートリアルでは、スキルを作成する手順を一から説明していきます。
はじめに、新しくスキルを作成します。

**【ステップ 1】**
Oracle Digital Assistant の Designer UI を Web ブラウザで開きます。
画面左上の ![ハンバーガー・アイコン][icon_hamburger] をクリックしてメニューを開きます。

![Oracle Digital Assistant Designer UI](images/screenshot_home-01.png "Oracle Digital Assistant の Designer UI でハンバーガー・アイコンをクリック")

**【ステップ 2】**
メニューから **「Develpment」** をクリックし、 **「Skills」** を選択します。

![Oracle Digital Assistant Designer UI](images/screenshot_home-02.png "Designer UI のメニューから「Development」→「Skills」を選択")

**【ステップ 3】**
メニューを閉じるために、 ![ハンバーガー・アイコン][icon_hamburger] をもう一度クリックします。

**【ステップ 4】**
**「New Skill」** をクリックします。

![Oracle Digital Assistant Designer UI](images/screenshot_skills-01.png)

**「Create Skill」** ボックスが表示されます。

**【ステップ 5】**
**「Create Skill」** ダイアログの **「Display Name」** フィールドに `Pizza King` と入力します。
このチュートリアルを同じ環境で実施する人が他にもいる場合は、区別できるように `Pizza King` の前または後ろにあなたのイニシャルなどを付けてください。
(例: `Pizza King AB`)

**【ステップ 6】**
**「Version」** フィールドに `1.0` と入力します。

![「Create Skill」ボックス](images/screenshot_create_skill-02.png)

**【ステップ 7】**
**「Create」** ボタンをクリックすると、Desginer UI には作成したスキルを設定するための画面が表示されます。
スキルの設定画面の左側はナビゲーション・バーになっており、![「Intents」アイコン][icon_intents_selected] が選択されています。

![インテント編集画面](images/screenshot_intents-01.png)

Here's where we'll begin to express the use case (that is, the PizzaKing-customer activity flow) in terms of the concepts that support Natural Language Processing (NLP): intents and entities.

[目次に戻る](#%E7%9B%AE%E6%AC%A1)

## インテントの作成

Oracle Digital Assistant のベースとなる自然言語言語処理エンジン (Natural Language Processiong; NLP) は、この段階ではどのようなタスクを実行するのか、どのようなリクエストに応えればよいのかを知りません。
それを覚えるために、Oracle Digital Assistant のスキルに対してインテント（意図）を定義していきます。

このチュートリアルでは、次の２つのインテントを定義します:

* OrderPizza: ピザの注文
* CancelPizza: 注文のキャンセル

### インテントの作成 (1) OrderPizza

**【ステップ 1】**
Designer UI の画面左側のナビゲーションで ![「Intents」アイコン][icon_intents_selected] が選択されていることを確認します。

**【ステップ 2】**
![「+ Intent」ボタン][button_create_intent] をクリックします。

**【ステップ 3】**
**「Conversation Name」** と **「Name」** フィールドにそれぞれ `OrderPizza` と入力します。

**【ステップ 4】**
次の箇条書きで表示されている文をコピーし、イタリック体で ***「Enter your example utterances here.」*** と書かれたフィールドに貼り付けたら、キーボードの [Enter] を押します。
複数の文をまとめてコピーし、一度に貼り付けることができます。

* Would you happen to have thin crust options on your Pizzas?
* Let's order a cheese pizza
* Would love a large Pepperoni please!
* I feel like eating some pizza
* I would like to order a pizza
* Can I order a Pizza?
* What's on the menu today?
* I want pizza
* Do you server gluten-free pizza?
* I want to order pizza for lunch
* Do you have deep dish pizzas available?
* Order Pizza!

12の例文が追加され、Designer UI には次のように表示されます。

![インテント編集画面](images/screenshot_intents-02.png)

### インテントの作成 (2) CancelPizza

**【ステップ 1】**
![「+ Intent」ボタン][button_create_intent] をクリックします。

**【ステップ 2】**
**「Conversation Name」** と **「Name」** フィールドにそれぞれ `CancelPizza` と入力します。

**【ステップ 3】**
次の箇条書きで表示されている文をコピーし、イタリック体で ***「Enter your example utterances here.」*** と書かれたフィールドに貼り付けたら、キーボードの [Enter] を押します。

* Can i cancel my order?
* Cancel my order
* Cancel my Pizza please
* How do I cancel my order?
* I don't want my Pizza anymore
* I really don't want the Pizza anymore
* I'd like to cancel my order please
* Its been more than 20 mts. Please cancel my order and issue a refund to my card.
* Need to cancel my order
* Please cancel my pizza order
* Please don't deliver my Pizza

11の例文が追加され、Designer UI には次のように表示されます。

![インテント編集画面](images/screenshot_intents-03.png)

> ***Note:***
> 操作につまってしまったときは、 [PizzaKing-Intents.csv][PizzaKing-Intents] をダウンロードして、**「More」** → **「Import intents」** を実行してみてください。
> 必要な例文が一度に投入できます。

### インテントのトレーニング

インテントとその例文を提示しただけでは、ユーザーのリクエストがピザの注文なのか、キャンセルなのかを判断することはできません。
スキルがユーザーのリクエストを判断できるようにするためには、NLP エンジンのトレーニングが必要です。

Oracle Digital Assistant の NLP エンジンは次の手順でトレーニングを行います。

**【ステップ 1】**
画面の右上に ![「Train」ボタン][button_train] が表示されていることを確認します。

![インテント編集画面](images/screenshot_intents-04.png)

**「Train」** ボタンにはエクスクラメーション・マークのアイコンが表示されており、トレーニングが必要なことを表しています。

**【ステップ 2】**
![「Train」ボタン][button_train] をクリックすると **「Train」** ボックスが表示されます。

![Train ボックス](images/screenshot_train-01.png)

**「Submit」** ボタンをクリックして数秒待つとトレーニングは完了します。
トレーニングが完了すると **「Train」** ボタンのアイコンがチェック・マークに変わります。

[目次に戻る](#%E7%9B%AE%E6%AC%A1)

## モデルのテスト

トレーニングが完了したら、NLP エンジンをテストしてみましょう。

**【ステップ 1】**
Designer UI のインテントの編集ページが表示されていない場合は、画面左側のナビゲーションの ![「Intents」アイコン][icon_intents_enabled] をクリックします。

**【ステップ 2】**
画面の右上の方にある **「Try It Out!」** リンクをクリックします。

![インテント編集画面](images/screenshot_intents-05.png)

画面の右側に **「Try Out Intents/Q&A」** ボックスが表示されます。

![「Try Out Intents/Q&A」ボックス](images/screenshot_try_out_intents-01.png)

**【ステップ 3】**
**「Try Out Intents/Q&A」** ボックスの一番下にある **「Message」** フィールドに次の文を入力します。

```
I want to order pizza
```

**「Send」** ボタンをクリックすると、**「Try Out Intents/Q&A」** ボックスは次のように表示されます。

![「Try Out Intents/Q&A」ボックス](images/screenshot_try_out_intents-02.png)

`I want to order pizza` は、インテント OrderPizza に該当するという判定をしています。
**「Confidence」** のスコア（今回の場合は「100%」）は、NLP エンジンが結果に対する自信を数値化したものです。

**【ステップ 4】**
別の文をテストします。
次の文を **「Try Out Intents/Q&A」** ボックスの **「Message」** フィールドに入力したら、**「Send」** ボタンをクリックします。

```
I feel like eating some pizza
```

ステップ 3 で実行したテストと同様に、インテント OrderPizza と判定されます。

**【ステップ 5】**
次の文をテストします。
今回は、インテント CancelPizza と判定されます。

```
Cancel my order?
```

**【ステップ 6】**
次の文をテストします。

```
Dude, bring me pizza
```

**「Try Out Intents/Q&A」** ボックスには次のように表示されます。

![「Try Out Intents/Q&A」ボックス](images/screenshot_try_out_intents-05.png)

上の図のとおり、NLP エンジンは `Dude, bring me pizza` （日本語訳: 「おい、ピザを持ってきて」）という文がインテント OrderPizza である可能性が最も高いと判定しています。
しかし、**「Confidence」** のスコアはそれほど高くありません。

**【ステップ 7】**
Confidence のスコアが高くない場合は、テストに使用した文をインテントの例文として追加します。
**「OrderPizza」** を選択した状態で **「Add Example」** ボタンをクリックすると、`Dude, bring me pizza` がインテント OrderPizza に例文として追加されます。

![インテント編集画面](images/screenshot_intents-06.png)

**【ステップ 8】**
インテントの例文を追加したので、トレーニングの実行が必要になりました。
画面右上の ![「Train」ボタン][button_train] をクリックしてトレーニングを実行します。

**【ステップ 9】**
**「Reset」** ボタンをクリックしてから、もう一度 `Dude, bring me pizza` という文をテストしてみます。
インテントの例文として追加されたので、インテント OrderPizza の Confidence のスコア上がっていることを確認します。

**【ステップ 10】**
テストが終わったら、![「Close」ボタン][button_close_try_it_out] をクリックして、**「Try Out Intents/Q&A」** ボックスを閉じます。

<!-- > ***Note:***
> Conversational AI does not compare input by exact matches of the words.
> Though "Dude, bring me pizza" is available as an utterance, when entering the sentence as a message, it is the intent model's algorithm that determines the matching intent.

> ***Note:***
> In these examples, you might get slightly different confidence scores than what are shown here.
> And in some cases, the matching intents themselves could vary, should the differing confidence scores push those intents above or below the given confidence thresholds.
> The cause of this variance is the non-deterministic nature of the AI behind the natural language processing and the fact that these skills have a limited number of training utterances (in order to make the lab simpler). -->

### このセクションのまとめ

このチュートリアルでは、NLP エンジンによるインテントの判定のテストを行いました。
実際の Oracle Digital Assistant による開発では、例文の投入 → トレーニング → テスト というサイクルを何度かまわすことで、NLP のエンジンの判定の精度を向上させていきます。

[目次に戻る](#%E7%9B%AE%E6%AC%A1)

## エンティティの作成

ユーザーのリクエストを処理するためには、追加で情報が必要なことがあります。
例えば、ピザの注文では、ピザのサイズや種類、配達時刻などを指定します。
これらの追加情報をエンティティとして定義します。

エンティティを定義することによって、ユーザーから送信されてきたメッセージ内から必要な情報を抽出することができるようになります。
また、メッセージに必要な情報が含まれていなければ、会話形式でユーザーに追加質問していくことが簡単に実現できます。

このチュートリアルでは2つのエンティティを定義します:

* PizzaSize: ピザのサイズ
* PizzaType: ピザの種類

### エンティティの作成 (1) PizzaSize

**【ステップ 1】**
Designer UI の画面左側のナビゲーションで ![「Entities」アイコン][icon_entities_enabled] をクリックします。
エンティティを作成・編集するための画面が表示されます。

**【ステップ 2】**
新しいエンティティを作成するために、![「+ Entitiy」ボタン][button_create_entity] をクリックします。

**【ステップ 3】**
**「Name」** フィールドの値を `PizzaSize` に変更します。

**【ステップ 4】**
**「Configuration」** セクションのドロップダウン・リスト **「Type」** から **「Value list」** を選択します。

**【ステップ 5】**
![「+ Value」ボタン][button_create_value] をクリックします。
**「Create Value」** ボックスが表示されます。

**【ステップ 6】**
**「Value」** フィールドに `Sサイズ` と入力します。

**【ステップ 7】**
**「Synonyms」** フィールドに `Small` と入力したら、キーボードの [Tab] キーを押します。
次に `smallest` を入力してから、キーボードの [Tab] キーを押します。

![「Create Value」ボックス](images/screenshot_create_value-02.png)

**【ステップ 8】**
**「Create Value」** ボックスの **「Create」** ボタンをクリックします。

**【ステップ 9】**
ステップ5～8の操作を繰り返して、エンティティ PizzaSize に次の値を追加します。

| Value | Synonyms |
|-------|----------|
| `Mサイズ` | `Medium`, `middle` |
| `Lサイズ` | `Large`, `Big`, `biggest` |

エンティティ PizzaSize が作成されると、エンティティの編集画面には次のように表示されます。

![エンティティ編集画面](images/screenshot_entities-01.png)

### エンティティの作成 (2) PizzaType

**【ステップ 1】**
新しいエンティティを作成するために、![「+ Entitiy」ボタン][button_create_entity] をクリックします。

**【ステップ 2】**
**「Name」** フィールドの値を `PizzaType` に変更します。

**【ステップ 3】**
**「Configuration」** セクションのドロップダウン・リスト **「Type」** から **「Value list」** を選択します。

**【ステップ 4】**
**「Value」** として、次の4つを追加します。

| Value | Synonyms |
|-------|----------|
| `マルゲリータ` | `Margherita` |
| `シーフード` | `sea food`, `seefood`  |
| `ポテト＆ベーコン` | `poteto and bacon`  |
| `チーズ` | `cheese` |

エンティティが作成されると、Designer UI には次のように表示されます。

![エンティティ編集画面](images/screenshot_entities-02.png)

### インテントとエンティティの関連付け

ユーザーが送信してきたメッセージを解析し、エンティティを抽出するためには、インテントとエンティティを関連付ける必要があります。
インテント OrderPizza と、前のセクションで作成したエンティティを関連付ける手順は次のとおりです。

**【ステップ 1】**
インテントを編集するために、Designer UI の画面左側のナビゲーションの ![「Intents」アイコン][icon_intents_enabled] をクリックします。

**【ステップ 2】**
インテントの一覧から **「OrderPizza」** を選択します。

**【ステップ 3】**
画面右側に表示される ![「+ Entity」ドロップダウン・ボタン][button_intent_entities] をクリックします。

**【ステップ 4】**
エンティティの一覧の中から **「PizzaSize」** を選択します。

![インテント編集画面](images/screenshot_intents-07.png)

**【ステップ 5】**
ステップ3～4の操作を繰り返して、次の２つのエンティティを追加します。

* PizzaType
* TIME

エンティティ TIME は、Oracle Digital Assistant が提供するビルトインのエンティティのひとつです。
今回は、ピザの配達時間を指定するために使用します。

ここまでの操作によって、インテント OrderPizza に関連付けられたエンティティは次のように表示されます。
（実際の画面と表示される順番が異なることがありますが、特に問題はありません）

![インテント編集画面](images/screenshot_intents-08.png)

**【ステップ 6】**
インテントにエンティティが関連付けられたので、トレーニングが必要になります。
画面右上の ![「Train」ボタン][button_train] をクリックしてトレーニングを実行します。

### エンティティのテスト

インテントのテストに使用した **「Try It Out」** ボックスを使用して、ユーザーが送信したメッセージからエンティティの値を抽出できることを確認しましょう。

**【ステップ 1】**
Designer UI の画面左側のナビゲーションで ![「Intents」アイコン][icon_intents_selected] を選択します。

**【ステップ 2】**
**「Try It Out!」** をクリックして、**「Try Out Intents/Q&A」** ボックスを開きます。

**【ステップ 3】**
**「Try Out Intents/Q&A」** ボックスの **「Message」** フィールドに、次の文を入力します。

```
I want to order a small cheese pizza at 7:30 pm
```

**「Send」** ボタンをクリックすると、入力された文から３つのエンティティ（PizzaSize、PizzaType、TIME）の値が抽出されます。
**「Try Out Intents/Q&A」** ボックスには次のように表示されます。

![「Try Out Intents/Q&A」ボックス](images/screenshot_try_out_intents-07.png)

**【ステップ 4】**
他の例についても試してみましょう。
**「Try Out Intents/Q&A」** ボックスの **「Message」** フィールドに次の文を入力し、**「Send」** ボタンをクリックします。

```
I want to order the biggest margherita pizza at noon
```

**「Try Out Intents/Q&A」** ボックスには次のように表示されます。
ユーザーが送信したメッセージでは配達時刻を `at noon` (正午) と指定していますが、`12:00 p.m.` と抽出していることがわかります。

![「Try Out Intents/Q&A」ボックス](images/screenshot_try_out_intents-08.png)

### このセクションのまとめ

このセクションでは、ピザの注文プロセスを実行する上で必要な情報をカスタム・エンティティとして定義し、インテント OrderPizza と関連付けました。
また、ユーザーが送信されたメッセージからエンティティの情報を抽出するテストの手順についても確認しました。

[目次に戻る](#%E7%9B%AE%E6%AC%A1)

## ダイアログ・フローのデザイン

NLP エンジンのためのデータ・モデルを作成できたので、会話の流れを定義していきましょう。
Oracle Digital Assistant のスキルの場合は、この会話の流れを「ダイアログ・フロー」呼び、ユーザーからのインプットやユーザーに対するレスポンスを定義します。

ダイアログ・フローは複数のステートで構成されます。
1つのステートの処理が終わると、次のステートに遷移していきます。
それぞれのステートは、1つのコンポーネントを参照します。
ユーザーに選択肢のメニューを提示したり、テキストの入力を促したり、メッセージを出力したりと、さまざまな機能を持つコンポーネントがあらかじめ提供されています。

### ダイアログ・フローのコンテキスト変数の定義

ダイアログ・フローはコンテキスト変数を定義できます。
コンテキスト変数は主に、一連の会話で共有する情報を保持するために使用します。

今回は5つのコンテキスト変数を定義します。

* `iResult`: NLP エンジンによるインテントの判定およびエンティティの抽出結果
* `pizzaSize`: エンティティ PizzaSize で表された、ピザのサイズ
* `pizzaType`: エンティティ PizzaType で表された、ピザの種類
* `deliveryTime`: ビルトイン・エンティティ TIME で表されたピザの配達時間
* `pizzaOrderMsg`: ピザの注文内容を表す文字列

**【ステップ 1】**
Designer UI のナビゲーションで ![「Flows」アイコン][icon_flows_enabled] をクリックし、ダイアログ・フロー・エディタを開きます。

**【ステップ 2】**
`variables:` と `states:` の間の行 (10～25行目) を削除します。

**【ステップ 3】**
`states:` より下の行を削除します。

ダイアログ・フロー・エディタは次のように表示されます。

![ダイアログ・フロー･エディタ](images/screenshot_flows-01.png)

**【ステップ 4】**
`variables:` の行の下に次の5行を追加します。

```yaml
    iResult: "nlpresult"
    pizzaSize: "PizzaSize"
    pizzaType: "PizzaType"
    deliveryTime: "TIME"
    pizzaOrderMsg: "string"
```

> ***Note:***
> 追加した5行は `variables:` の行よりも半角スペース2個分多くインデントされている必要があります（合計するとスペース4個分）。
> YAML ベースの OBotML では、インデントを使って階層構造を表現するため、正しくインデントされていないと構文エラーになります。

ここまでの編集によって、ダイアログ・フロー・エディタは次のように表示されます。

![ダイアログ・フロー･エディタ](images/screenshot_flows-02.png)

これで、ダイアログ・フローにステートを追加する準備が整いました。

### インテントを判定するステートの追加

このハンズオンでは最初に、ダイアログ・フローに `System.Intent` コンポーネントを追加します。
この `System.Intent` コンポーネントは、ユーザーが送信してきた文を評価して、スキルに定義されているインテントを判定します。
インテントにエンティティが含まれている場合はエンティティをすべて抽出してから、後続のステートに処理を遷移させます。

**【ステップ 1】**
![「Components」ボタン][button_components] をクリックして、コンポーネントのテンプレート・ギャラリを開きます。

**【ステップ 2】**
コンポーネントのテンプレート・ギャラリでは最初にコンポーネントのタイプを選択します。
**「Language」** を選択します。

![テンプレート・ギャラリ](images/screenshot_components-01.png)

**【ステップ 3】**
コンポーネントのテンプレート・ギャラリの左側にコンポーネントのリストが表示されます。
コンポーネントのリストから **「Intent」** を選択し、**「Remove Comments」** のスイッチをオンにします。

![テンプレート・ギャラリ](images/screenshot_components-02.png)

**【ステップ 4】**
コンポーネントのテンプレート・ギャラリの **「Apply」** ボタンをクリックします。

**【ステップ 5】**
`System.Intent` コンポーネントのテンプレートが追加されました。
`System.Intent` コンポーネントの `variable` プロパティの値として `"iResult"` を設定します（`variable:` の後に `"iResult"` を追加）。
ダブル・クォーテーション `"` が必要です。

```yaml
      variable: "iResult"
```

これによって NLP エンジンによるインテントの判定とエンティティの抽出結果が、変数 `iResult` に保存されます。

**【ステップ 6】**
テンプレートによって追加された次のプロパティは削除します。

* botName
* botVersion
* sourceVariable
* autoNumberPostbackActions
* footerText

**【ステップ 7】**
`translate` プロパティの値として `false` に設定します。
ブーリアン型の値 (`true` または `false` のどちらかをセットする値)は、ダブル・クォーテーション (`"`) は不要です。

**【ステップ 8】**
次に遷移するステートを設定するため、`transition.actions` プロパティを次のように編集します。

```yaml
    transitions:
      actions:
        OrderPizza: "startOrderPizza"
        CancelPizza: "startCancelPizza"
        unresolvedIntent: "startUnresolved"
```

これにより、インテントの判定結果に応じて次のステートに遷移します。

| インテント | 遷移先のステート |
|---|---|
| OrderPizza | startOrderPizza |
| CancelPizza | startCancelPizza |
| 該当するインテントがないと判定された場合 (unresolvedIntent) | startUnresolved |

### 各インテントの処理を開始するステートの追加

次に、NLP エンジンが判定したインテントに対応した遷移先となる、３つのステートをダイアログ・フローに追加します。

* startOrderPizza
* startCancelPizza
* startUnresolved

それぞれのステートは、`System.Output` コンポーネントを使用してメッセージを出力した後、`transitions.return` プロパティを使用して会話を終了します。
このチュートリアルでは時間を節約するために、次のコード・ブロックをコピーし、ダイアログ・フロー・エディタの最後尾に貼り付けることにします。

```yaml
  startOrderPizza:
    component: "System.Output"
    properties:
      text: "こんにちは、Pizza King です。ご注文を承ります。"
      keepTurn: false
    transitions:
      return: "done"

  startCancelPizza:
    component: "System.Output"
    properties:
      text: "注文のキャンセルを承りました。"
    transitions:
      return : "done"

  startUnresolved:
    component: "System.Output"
    properties:
      text: "申し訳ありません。おっしゃっていることが理解できませんでした。"
    transitions:
      return: "done"
```

貼り付けられたコード・ブロックが、インデントを保持していることを確認してください。
また、Designer UI の右上にある **「Validate」** ボタンをクリックして、追加したステートの構文が正しいことを確認します。

### ダイアログ・フローのトラブルシューティング

**「Validate」** ボタンをクリックしたときに、エラー・メッセージが表示された場合は、次のどちらかが原因であることが多いです:

* プロパティの名前にスペル・ミスがあった
* インデントが正しく設定されていない

エラーのある行は、ダイアログ・フロー・エディタの左余白（行番号の左）に ![エラー・アイコン][icon_error] が表示されます。
![エラー・アイコン][icon_error] にマウス・ポインタを乗せると、ツールチップで原因が表示されます。

また、Designer UI の画面左のナビゲーション・バーの一番下に表示される ![デバッグ・アイコン][icon_debug] をクリックすると、デバッグ・ウィンドウが表示され、エラーのある行とそのれぞれの原因が表示されます。
デバッグ・ウィンドウには、![エラー・アイコン][icon_error] のツールチップで表示される原因よりも詳細な情報が表示されることがあるので、エラーの修正に役立ちます。
![デバッグ・アイコン][icon_debug] を再度クリックすれば、デバッグ・ウィンドウは非表示になります。

もし、このチュートリアルで作成したダイアログ・フローでエラーが発生し、どうしてもエラーが修正できない場合は、 [your-first-dialog-flow.yaml][your-first-dialog-flow] の内容をコピーし貼り付けることでチュートリアルの続きを実施できます。

### インテントの判定のチューニング

ここでは、インテントの判定について微調整するのに役立つ設定について説明します。

* **Confidence Threshold**:
NLP エンジンの Confidence スコアのしきい値。
定義されたすべてのインテントの Confidence スコアが、どれもしきい値を超えない場合は、該当するインテントがないと判定さます。

* **Confidence Win Margin**:
Confidence スコア 1位と2位の差分。
設定した値より1位と2位の差が開いていない場合に、ユーザーに対してどちらのインテントに該当するのかを確認できるようになります。
例えばこの値 0.1 (10%) と設定した場合に、1位のインテントが60%、2位のインテントが55%だった場合に、メニューを表示させることが可能です。

それでは、これら2つの設定を変更しましょう。

**【ステップ 1】**
Designer UI の画面左側のナビゲーションで ![「Settings」アイコン][icon_settings_enabled] をクリックします。
次に、画面上部にある **「Configuration」** タブを選択します。

**【ステップ 2】**
**「Confidence Threshold」** の値を `0.6` (60% 以上を意味しています) に設定します。

**【ステップ 3】**
**「Confidence Win Margin」** の値を `0.1` (10% 以上を意味しています)に設定します。

![スキルの設定画面](images/screenshot_settings-01.png)

### ダイアログ・フローのテスト

ここまでに設定した内容をテストしてみましょう。
Designer UI の Skill Tester を使用すると、簡単に会話の流れを確認できます。
ここでは、各インテントに応じたメッセージが表示されることを確認します。

**【ステップ 1】**
Designer UI の画面左側のナビゲーション・バーの下部にある ![「Skill Tester」アイコン][icon_skill_tester] をクリックします。
（ディスプレイのサイズによっては、下にスクロールする必要があります）

**【ステップ 2】**
Skill Tester の左下にある **「Message」** フィールドに次の文を入力してから、キーボードの [Enter] キーを押します。

```
I want to order a pizza
```

OrderPizza に対応した（ステート `startOrderPizza` で設定した）メッセージが表示されることを確認します。
Skill Tester の右側の **「Conversation」** タブでは、ステートの遷移が確認できます。

![スキル・テスター](images/screenshot_skill_tester-01.png)

**【ステップ 3】**
Skill Tester の右側にある **「Intent/Q&A」** タブをクリックすると、NLP エンジンによるインテントの判定結果を確認できます。
次のスクリーンショットのように表示されているはずです。

![スキル・テスター](images/screenshot_skill_tester-02.png)

**【ステップ 4】**
Skill Tester の右上にある **「Reset」** ボタンをクリックします。
表示されていた内容がクリアされ、会話がリセットされます。

**【ステップ 5】**
Skill Tester の **「Message」** フィールドに次の文を入力してから、キーボードの [Enter] キーを押します。

```
I want to cancel my order
```

CancelPizza に対応した（ステート `startCancelPizza` で設定した）メッセージが表示されることを確認します。

**【ステップ 6】**
Skill Tester の **「Reset」** ボタンをクリックします。

**【ステップ 7】**
今回作成したインテント（ピザの注文やキャンセル）とは関係のない文も試してみましょう。
Skill Tester の **「Message」** フィールドに次の文を入力してから、キーボードの [Enter] キーを押します。

```
Can you get me a radio taxi now?
```

**【ステップ 9】**
**「Intent/Q&A」** タブをクリックして NLP エンジンの判定結果を確認します。

![スキル・テスター](images/screenshot_skill_tester-03.png)

作成した2つのインテントのどちらも Confidence スコアが 60% を超えていません。
そのため、該当するインテントがないと判定された場合 (unresolvedIntent) に対応したステート `startUnresolved` に遷移しました。

### ピザの注文を受ける会話の作成

このセクションでは、次の５つのステートを追加していきます。
処理の流れと処理内容は次のとおりです。

1. `setPizzaSize`: ピザのサイズを選択
2. `setPizzaType`: ピザの種類を選択
3. `setPizzaDeliveryTime`: ピザの配達時間を指定
4. `setPizzaOrderMessage`: 注文内容の確認メッセージの生成
5. `showPizzaOrder`: 注文内容の確認メッセージの出力

**【ステップ 1】**
Designer UI のナビゲーションで ![「Flows」アイコン][icon_flows_enabled] をクリックし、ダイアログ・フロー・エディタを開きます。
前のセクションで追加したダイアログ・フロー・エディタのステート `startOrderPizza` にナビゲートします。

**【ステップ 2】**
`keepTurn` プロパティの値を `true` に変更します。
通常は、スキルとユーザーが交互にメッセージを送信しますが、`keepTurn` プロパティの値を `true` に設定すると、スキルからユーザーに連続でメッセージを送信できます。

**【ステップ 3】**
`transitions:` の次の行にある `return: "done"` を `next: "setPizzaSize"` に置き換えます。

```yaml
  startOrderPizza:
    component: "System.Output"
    properties:
      text: "こんにちは、Pizza King です。ご注文を承ります。"
      keepTurn: true
    transitions:
      next: "setPizzaSize"
```

#### ピザのサイズの選択: setPizzaSize

**【ステップ 1】**
![「Components」ボタン][button_components] をクリックして、コンポーネントのテンプレート・ギャラリを開きます。

**【ステップ 2】**
コンポーネントのタイプとして **「User Interface」** を選択します。

**【ステップ 3】**
コンポーネントのリストから **「List - set variable」** を選択します。

**【ステップ 4】**
ドロップダウン **「Insert After」** から **「startOrderPizza」** を選択します。

**【ステップ 5】**
**「Remove Comments」** スイッチをオンにします。

![テンプレート・ギャラリ](images/screenshot_components-03.png)

**【ステップ 6】**
**「Apply」** ボタンをクリックします。
追加済みのステート `startOrderPizza` の次に `System.List` のテンプレートが追加されます。

**【ステップ 7】**
追加されたステートの名前を `variableList` から `setPizzaSize` に変更します。

**【ステップ 8】**
テンプレートで追加されたステートを次のように編集します。

```yaml
  setPizzaSize:
    component: "System.List"
    properties:
      options: "${pizzaSize.type.enumValues}"
      prompt: "ピザのサイズをお選びください。"
      variable: "pizzaSize"
      nlpResultVariable: "iResult"
    transitions:
      next: "setPizzaType"
```

#### ピザの種類の選択

次のコード･ブロックをコピーし、ステート `setPizzaSize` の後に貼り付けます。

```yaml
  setPizzaType:
    component: "System.List"
    properties:
      options: "${pizzaType.type.enumValues}"
      prompt: "どのピザにしますか？"
      variable: "pizzaType"
      nlpResultVariable: "iResult"
    transitions:
      next: "setPizzaDeliveryTime"
```

追加されたステート `setPiizaType` は、`setPizzaSize` と同様に `System.List` コンポーネントを使用しています。
表示されるオプションは、エンティティ `PizzaType` の値が使用されます。

#### ピザの配達時間の指定

**【ステップ 1】**
![「Components」ボタン][button_components] をクリックして、コンポーネントのテンプレート・ギャラリを開きます。

**【ステップ 2】**
コンポーネントのタイプとして **「User Interface」** を選択します。

**【ステップ 3】**
コンポーネントのリストから **「Text」** を選択します。

**【ステップ 4】**
ドロップダウン **「Insert After」** から **「setPizzaType」** を選択します。

**【ステップ 5】**
**「Remove Comments」** スイッチをオンにします。

**【ステップ 6】**
**「Apply」** ボタンをクリックします。
ステート `setPizzaType` の次に `System.Text` コンポーネントのテンプレートが追加されます。

**【ステップ 7】**
追加されたステートの名前を `text` から `setPizzaDeliveryTime` に変更します。

**【ステップ 8】**
テンプレートで追加されたステートを次のように編集します。

```yaml
  setPizzaDeliveryTime:
    component: "System.Text"
    properties:
      prompt: "何時にお届けしますか？"
      variable: "deliveryTime"
      nlpResultVariable: "iResult"
      maxPrompts: 3
      translate: false
    transitions:
      actions:
        cancel: "maxError"
        next: "setPizzaOrderMessage"
```

**【ステップ 9】**
ユーザーから送信されたテキストを時刻として解釈できなかった場合は、`maxPrompts` で設定した回数（今回は `3`）ユーザーに入力を促します。
最終的に時刻として解釈できなかった場合は、`transitions.actions.cancel` で指定したステートに遷移します。
次のステートのコードをコピーし、ダイアログ・フローの最後に貼り付けます。

```yaml
  maxError:
    component: "System.Output"
    properties:
      text: "恐れ入りますがお電話でのご注文をお願いします。"
    transitions:
      return: "done"
```

#### 注文内容の確認メッセージの生成

**【ステップ 1】**
![「Components」ボタン][button_components] をクリックして、コンポーネントのテンプレート・ギャラリを開きます。

**【ステップ 2】**
コンポーネントのタイプとして **「Variables」** を選択します。

**【ステップ 3】**
コンポーネントのリストから **「Set variable」** を選択します。

**【ステップ 4】**
ドロップダウン **「Insert After」** から **「setPizzaDeliveryTime」** を選択します。

**【ステップ 5】**
**「Remove Comments」** スイッチをオンにします。

**【ステップ 6】**
**「Apply」** ボタンをクリックします。
ステート `setPizzaDeliveryTime` の次に `System.SetVariable` のテンプレートが追加されます。

**【ステップ 7】**
追加されたステートの名前を `text` から `setPizzaDeliveryTime` に変更します。

**【ステップ 8】**
テンプレートで追加されたステートを次のように編集します。

```yaml
  setPizzaOrderMessage:
    component: "System.SetVariable"
    properties:
      variable: "pizzaOrderMsg"
      value:
      - "ご注文ありがとうございました。次のとおりご注文を承りました。"
      - "サイズ: ${pizzaSize.value}"
      - "種類: ${pizzaType.value}"
      - "配達時刻: ${deliveryTime.value.date?long?number_to_time?string('HH:mm')}"
```

> ***Note:***
> The `text` property value uses the Apache FreeMarker expression |- to print multi-line text in a single response bubble.
> Alternatively, you could have used multiple output text components.

#### 注文内容の確認メッセージの出力

**【ステップ 1】**
![「Components」ボタン][button_components] をクリックして、コンポーネントのテンプレート・ギャラリを開きます。

**【ステップ 2】**
コンポーネントのタイプとして **「User Interface」** を選択します。

**【ステップ 3】**
コンポーネントのリストから **「Output」** を選択します。

**【ステップ 4】**
ドロップダウン **「Insert After」** から **「setPizzaOrderMessage」** を選択します。

**【ステップ 5】**
**「Remove Comments」** スイッチをオンにします。

**【ステップ 6】**
**「Apply」** ボタンをクリックします。
ステート `setPizzaOrderMessage` の次に `System.Output` のテンプレートが追加されます。

**【ステップ 7】**
追加されたステートの名前を `output` から `showPizzaOrder` に変更します。

**【ステップ 8】**
テンプレートで追加されたステートを次のように編集します。

```yaml
  showPizzaOrder:
    component: "System.Output"
    properties:
      text: |-
             <#list pizzaOrderMsg.value as text>${text}

             </#list>
    transitions:
      return: "done"
```

### ダイアログ・フローの検証

ダイアログ・フローの構文が正しいかどうかを確認するために、画面の右上にある **「Validate」** ボタンをクリックします。
エラーが表示された場合は、修正してください。

エラーを修正できない場合は、[complete-dialog-flow.yaml][complete-dialog-flow] を開いて内容をコピーし、ダイアログ・フロー・エディタに貼り付けてみてください。

[目次に戻る](#%E7%9B%AE%E6%AC%A1)

## スキルのテスト

ここまでの操作で、Pizza King のスキルが一通り設定できました。
スキル・テスターを使用して、動作を確認してみましょう。

**【ステップ 1】**
Designer UI の画面左側のナビゲーション・バーの下部にある ![「Skill Tester」アイコン][icon_skill_tester] をクリックします。

**【ステップ 2】**
Skill Tester に以前に実行したテスト結果が表示されている場合は、**「リセット」** ボタンをクリックします。

**【ステップ 3】**
Skill Tester の **「Message」** フィールドに次の文を入力したら、キーボードの [Enter] キーを押します。

```
I want to order pizza
```

ピザのサイズの選択を促すメニューが表示されます。

![スキル・テスター](images/screenshot_skill_tester-04.png)

ピザのサイズを選択するメニューから適当に値を選択します。

**【ステップ 4】**
ピザの種類を選択するメニューが表示されます。
適当な種類を選択します。

**【ステップ 5】**
配達時刻の入力を促されます。`9:00 PM` や `21:00` のように時刻を指定します。

これにより、注文内容の確認メッセージが表示されます。

![スキル・テスター](images/screenshot_skill_tester-05.png)

**【ステップ 7】**
Skill Tester の **「Reset」** ボタンをクリックします。

**【ステップ 8】**
Skill Tester の **「Message」** フィールドに次の文を入力したら、キーボードの [Enter] キーを押します。

```
can you get me the biggest seafood pizza you can make at noon
```

今回は、ユーザーが送信した文にエンティティの情報が含まれているので、すぐに注文内容の確認メッセージが表示されます。

![スキル・テスター](images/screenshot_skill_tester-06.png)

**【ステップ 9】**
Skill Tester の **「Conversation」** タブ・ページを下にスクロールすると、変数に格納されている値を確認することができます。

![スキル・テスター](images/screenshot_skill_tester-07.png)

----

お疲れ様でした! このチュートリアルはこれで終了です。

このチュートリアルでは、ピザの注文を受け付ける基本的なスキルの作成をとおして、Oracle Digital Assistant の次の機能について説明しました:

* インテントとエンティティの定義
* NLP エンジンのトレーニングとテスト
* ダイアログ・フローの設計と編集、検証
* スキルのテスト

<!--- Designer UI のアイコン/ボタンのスクリーンショットへのリファレンス -->
[icon_hamburger]:           images/icon_hamburger.png           "ハンバーガー・アイコン"
[icon_debug]:               images/icon_debug.png               "デバッグ・アイコン"
[icon_entities_enabled]:    images/icon_entities_enabled.png    "「Entities」アイコン"
[icon_entities_selected]:   images/icon_entities_selected.png   "「Entities」アイコン"
[icon_error]:               images/icon_error.png               "エラー・アイコン"
[icon_flows_enabled]:       images/icon_flows_enabled.png       "「Flows」アイコン"
[icon_flows_selected]:      images/icon_flows_selected.png      "「Flows」アイコン"
[icon_intents_enabled]:     images/icon_intents_enabled.png     "「Intents」アイコン"
[icon_intents_selected]:    images/icon_intents_selected.png    "「Intents」アイコン"
[icon_settings_enabled]:    images/icon_settings_enabled.png    "「Settings」アイコン"
[icon_settings_selected]:   images/icon_settings_selected.png   "「Settings」アイコン"
[icon_skill_tester]:        images/icon_skill_tester.png        "「Skill Tester」アイコン"
[button_close_try_it_out]:  images/button_close_try_it_out.png  "「Close」ボタン"
[button_components]:        images/button_components.png        "「Components」ボタン"
[button_create_entity]:     images/button_create_entity.png     "「+ Entity」ボタン"
[button_create_intent]:     images/button_create_intent.png     "「+ Intent」ボタン"
[button_create_value]:      images/button_create_value.png      "「+ Value」ボタン"
[button_intent_entities]:   images/button_intent_entities.png   "「+ Entity」ドロップダウン・ボタン"
[button_train]:             images/button_train.png             "「Train」ボタン"

<!-- 各種リソースへのリファレンス -->
[PizzaKing-Intents]:      resources/PizzaKing-Intents.csv
[complete-dialog-flow]:   resources/complete-dialog-flow.yaml
[your-first-dialog-flow]: resources/your-first-dialog-flow.yaml
