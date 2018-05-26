---
title: "コードの接続"
slug: connecting-code
---

このセクションでは、Storyboardとコードがどうつながるのかを見てみます。現時点でアプリを実行すると、シミュレーター内でシェークボタンをクリックしても何も起こらないことに気づくでしょう。

これは、何もコードを書かないと、私たちのアプリは何もしないからです。あなたが書くコードは、ユーザーがアプリを使っているときに、アプリへ何をすべきか伝える指示のようなものです。指示がないと、アプリは何もしません。

ボタンのタップに対応する例では、ユーザーがシェークボタンをタップした時に、アプリに何をすべきなのかを伝えるコードを書く必要があります。

# どう接続されていますか？

初心者が最もつまづきやすい点の一つは、コードがStoryboardとどうつながるのかを理解することです。Xcodeではアイデンティティインスペクター、 _IBOutlets_ そして _IBActions_ の組み合わせを使って、StoryboardをSwiftコードにつなげます。

これを理解するには、まずアシスタントエディタについて学ぶ必要があります。

ツールバーの右側には、トグルできる3つのボタンによって構成されているグループが2つあります。まずは左側の最初のグループに注目します。

![Editor Modes](assets/editor_modes.png)

以上でハイライトされている3つのボタンにより、エディタモードをトグルできます。一度にアクティブな状態になれるのは、これらのモードのうち一つだけです。

ご覧の通り、最初のボタン、またはスタンダードエディタはすでにアクティブな状態です。これは、今までずっとスタンダードエディタを使ってきたからです。スタンダードエディタは何も手の込んだことをしません。このエディタは単純に、単一で大型のエディタウィンドウを表示して、単一のファイルを取り扱います。

2つ目のボタンは、エディタモードをアシスタントエディタに設定します。このエディタモードは、複数のファイルを開いて隣り合わせで編集するためのものです。

> [action]
まだの場合は、スタンダードエディタからアシスタントエディタへとボタンをトグルしてください。次のように表示されます。
>
![Assistant Editor Active](assets/assistant_editor_active.png)

最初に気づくかもしれませんが、アシスタントエディタを使う時、開いている各ファイルの画面スペースが欠如しています。この状態を改善するには、ナビゲーターのような不要なXcodeツールを非表示にしましょう。これは、ツールバーの最右端にある2つ目のグループのボタンを使って実施できます。

![Display Xcode Areas](assets/display_xcode_areas.png)

これらのボタンを使って、ナビゲーター、デバッガー、ユーティリティの非表示と表示をトグルできます。それでは、もう少し画面に余裕を持たせるため、ナビゲーターエリアを閉じましょう。

> [action]
最初のボタンをクリックして ナビゲーターぺインを閉じましょう。ユーティリティエリアはすぐに必要になるので、開いたままにしておいてください。
>
![ms-video](https://s3.amazonaws.com/mgwu-misc/Magic+8+Ball/05-connecting-code/hide_navigator.mp4)

アシスタントエディタで作業をしている時、使っていないXcodeのエリアを非表示にすると、画面のスペースをもっと確保できるので便利だということがよくあります。

2つのファイルを並べて表示する方法が分かったので、XcodeがどうやってStoryboardビューコントローラーと`ViewController.swift`ソースファイルの接続を認識するのか見てみましょう。

# アイデンティティインスペクター

> [action]
1. Storyboardの _Document Outline_ で、 _View Controller_ のStoryboardオブジェクトを選択してください。![Document Outline](assets/document_outline_select_vc.png)
2. 次に、ユーティリティエリアでアイデンティティインスペクターを開いてください。![Identity Inspector Active](assets/identity_inspector_active.png)

アイデンティティインスペクター_では、現在選択されているStoryboardビューコントローラーのカスタムクラスを指定するセクションが表示されるはずです。

![Custom Class Section](assets/custom_class_section.png)

`ViewController.swift`ファイルとアイデンティティインスペクターの両方を参照すると、クラス名が一致することがわかるでしょう。これが、Storyboardオブジェクトのカスタム行動を設定し、定義する方法です。

![Connected Class](assets/connected_class.png)

> [info]
_Single View App_ テンプレートがあらかじめ設定を行なっていたので、このプロジェクトでは設定の必要はありません。今後のプロジェクトでは、アイデンティティインスペクターに含まれる各カスタムビューコントローラーのクラスを構成して、StoryboardビューコントローラーをそれぞれのSwiftソースファイルに接続する必要があります。

# IBOutlets

Storyboardビューコントローラーで、前にラベルとボタンを追加しました。ロジック（Magic 8-Ballに対する指示）を実装するには、ラベルとボタンを参照する方法が必要です。

この問題を解決するには、IBOutletsを作成する必要があります。

IBOutlets は、Storyboardサブビューオブジェク（例えば、ラベル、ボタン、画像ビューなど）から、Swiftコードに対するコネクションを作成します。これにより、プログラムで参照の操作が可能になります。

> [action]
まず、画面のスペースをもっと増やすため、ツールバーを使ってユーティリティペインを閉じましょう。Xcode IDEは次のように表示されるはずです。
>
![Assistant Editor Active](assets/assistant_editor_active_2.png)

`Main.storyboard`と`ViewController.swift`ファイルが並んで開かれている状態で、 最初のIBOutletを作成しましょう。

> [action]
回答ラベル用にIBOutletを作成しましょう。
>
インターフェースビルダーで回答ラベルを選択しましょう。次に、コントロールを押しながら、Storyboardラベルから`ViewController.swift`ファイルへとクリックしながらドラッグしてください。結果のプロンプトで、新しいIBOutlet`answerLabel`に名前を付けてください。![ms-video](https://s3.amazonaws.com/mgwu-misc/Magic+8+Ball/05-connecting-code/answer_label_iboutlet.mp4)

 シェークボタンについても同じ手順を繰り返してください。

> [challenge]
Storyboardボタン用に`shakeButton`という新しいIBOutletを`ViewController.swift`ファイル内で作成してください。

<!-- break -->

> [solution]
インターフェースビルダーでシェークボタンを選択してください。それからコントロールボタンを押しながら、Storyboardボタンから`ViewController.swift`ファイルへ、クリックしながらドラッグしてください。
>
![ms-video](https://s3.amazonaws.com/mgwu-misc/Magic+8+Ball/05-connecting-code/button_iboutlet.mp4)

`ViewController.swift`ファイルで、ラベルやボタンを参照し、アクセスができるよう、IBOutletを両方作成しました。

次に、ユーザーがシェークボタンをタップした時の反応を、IBActionを使って検討していきます。

# IBAction

IBAction は、ユーザーがUIオブジェクトとやりとりをする時に呼び出されるメソッドです。 IBAction の作成は、IBOutletの作成にとてもよく似ています。

ユーザーがシェークボタンをタップした時のためのIBActionを作成しましょう。

> [action]
ビューコントローラーのソースファイルで、シェークボタンのIBActionを作成しましょう：![ms-video](https://s3.amazonaws.com/mgwu-misc/Magic+8+Ball/05-connecting-code/button_ibaction.mp4)
>
ステップバイステップ：
>
1. シェークボタンを選択してください。
1. コントロールボタンを押さえ、IBOutletを作成するかのように、Storyboardボタンからビューコントローラーソースファイルへ、クリックしてドラッグしてください。
1. IBOutletに名前を付けるプロンプトが出たら、ドロップダウンメニューを使って、コネクションのタイプを`Outlet`から`Action`に変更してください。
1. IBActionに`shakeButtonTapped`と名付けてください。

そうすると、ビューコントローラーの中に新しい機能が作成されることに気づくでしょう。シェークボタンがタップされると、いつでもこの関数が呼び出されます。

これが実際に動く姿を確認するため、シェークボタンがタップされるたびに、デバッグコンソールにテキストを表示させるようにしましょう。

## デバッグのプリント

これまで、デバッガーについて話したり、これを使ったりすることはありませんでした。デバッガーは、かなり強力なツールで、アプリに含まれるバグを発見できるようにしてくれます。この場合、ユーザーがボタンとやりとりしたときに、デバッグコンソールへ簡単なログを表示するだけです。

まずは、IBAction の`shakeButtonTapped`内で、printステートメントを追加する必要があります。

> [action]
`ViewController.swift`で、`shakeButtonTapped(_:)`を次のように変更してください：
>
```
@IBAction func shakeButtonTapped(_ sender: Any) {
    print("shake it like a polaroid picture!")
}
```

さて、アプリを実行して試してみましょう。

アプリが起動されてUIが表示されたら、シェークボタンをクリックしてください。Xcodeデバッガーでは、シェークボタンを押すたびにprintステートメントが表示されるはずです！

![Print Debugging](assets/print_debugging.png)

ご覧の通り、ユーザーがボタンをタップするたびに`shakeButtonTapped(_:)`が呼び出されます。

# ラベルのテキストを変更

ボタンがタップされたときに、コンソールにログを表示できるようにしました。もう一歩先に進んで、ボタンタップ上のラベルテキストを変更しましょう。

> [action]
`ViewController.swift`で、以下のコードの行を`shakeButtonTapped(_:)`に追加しましょう：
>
```
@IBAction func shakeButtonTapped(_ sender: Any) {
    print("shake it like a polaroid picture!")
>
    answerLabel.text = "button was tapped"
}
```

アプリをもう一度ビルドして実行しましょう。シェークボタンをタップすると、回答ラベルは次のテキストに変化して表示されるはずです：

![Changed Text](assets/changed_text.png)

これまでに、次の作業を済ませました：

各`UILabel`には、変更、更新することのできるテキスト属性があります。画面上のUIも更新します。`shakeButtonTapped(_:)`が呼び出されたとき、ラベルのテキストプロパティを新たな文字列に設定しました。

ボタンの動作やラベルテキストの変更に関する新しい知識を使って、Magic 8-Ballの回答を無作為に選択し表示するロジックを実装することができます。

# ロジックの実施

これで、Magic 8-Ballを実装するツールがすべて揃いました。まず、アシスタントエディタを閉じ、スタンダードエディタに戻ります。

> [action]
スタンダードエディタにで`ViewController.swift`を表示するには、プロジェクトナビゲーターを使用します。

次にロジックを実装しましょう。まずは、インスタンス変数を追加します。これは、Magic 8-Ballの可能な回答すべてを含む文字列の配列です。どうぞご自由に独自のものを追加してください！

> [action]
IBOutletsの上に、次の文字列の配列を追加してください：
>
```
class ViewController: UIViewController {
>
    // MARK: - プロパティ
>
    let answers = ["はい、もちろん", "確実です", "間違いありません", "はい", "かなりの確率です", "ええ、そうしましょうか？", "同じです", "もっと聞かせてください", "ちょっとおかしい", "ちょっと怪しいので、もう一度試してみてください", "あとでもう一度質問してください", "ケーキなんて嘘", "42", "それは言い過ぎ", "かなり疑わしい", "信用しないで", "答えはノーです", "絶対にムリ"]
>
    @IBOutlet weak var answerLabel: UILabel!
    @IBOutlet weak var shakeButton: UIButton!
>
    // ... 残りのコード
}
```
>
参考までに、以上の回答の配列のプレーンテキスト版は次の通りです：
>
let answers = ["はい、もちろん", "確実です", "間違いありません", "はい", "かなりの確率です", "ええ、そうしましょうか？", "同じです", "もっと聞かせてください", "ちょっとおかしい", "ちょっと怪しいので、もう一度試してみてください", "あとでもう一度質問してください", "ケーキなんて嘘", "42", "それは言い過ぎ", "かなり疑わしい", "信用しないで", "答えはノーです", "絶対にムリ"]

回答の配列を新たに用意したところで、シェークボタンがタップされた場合に、この配列に含まれる項目を無作為に選択し、表示される回答ラベルのテキストを変更できるようになります。

> [action]
無作為に回答を選択するには、`arc4random_uniform(_:)`メソッドを使うことができます。ビューコントローラーの`shakeButtonTapped`を以下に変更してください：
>
```
@IBAction func shakeButtonTapped(_ sender: UIButton) {
    // 1
    let maxIndex = UInt32(answers.count)
    // 2
    let randomIndex = Int(arc4random_uniform(maxIndex))
>
    // 3
    answerLabel.text = answers[randomIndex]
}
```
>
これまでのコードをステップごとに分解しましょう：
>
1. 回答の配列内で無作為にインデックスを生成する際、上限を特定するために使用される`maxIndex`を決定します。`arc4random_uniform`メソッドは`UInt32`型の引数を受け入れるため、`UInt32`型にキャストしなければなりません。
1. 回答のインデックスを無作為に生成するには、`arc4random_uniform`を使用します。指定のインデックスで配列の中の項目を読み出すには整数が必要なので、`Int`型にキャストし直します。
1. 最後に、回答ラベルのテキストと、無作為に生成された回答とを一致させます。

アプリをビルドして実行しましょう！

Magic 8-Ballに2つほど質問をして、動作をテストしましょう。

おめでとうございます。Magic 8-Ballの基本的な機能を実装しました。

次に移る前に、もう一歩先へ進んで、基本的なMagic 8-Ballに付属するシェーク機能を実装しましょう。

# シェークのジェスチャーの実施

iPhoneは、ユーザーに発生する特定のイベントを受け取り、これに基づく行動を起こすためにオーバーライドできる特定のメソッドをデフォルトで実装しています。

シェークのジェスチャーに関しては、システムによって実装された関数をオーバーライドし、独自の機能と取り替えます。これにより、ユーザーがアプリをシェークするとラベルが変わるようになります。

> [action]
以下のメソッドをビューコントローラーに追加してください：
>
```
override func motionEnded(_ motion: UIEventSubtype, with event: UIEvent?) {
    guard motion == .motionShake else { return }
>
    let maxIndex = UInt32(answers.count)
    let randomIndex = Int(arc4random_uniform(maxIndex))
>
    answerLabel.text = answers[randomIndex]
}
```
>
ご覧の通り、`motionEnded(_:with:)`イベントをオーバーライドし、`.motionShake`イベントをチェックしています。トリガーされると、同じロジックを実行して、無作為に回答を選び表示します。

# DRYを保つ

プログラミングに関する一般的な経験則は、 _DRY_ を守ることです。DRYとは、「Don't Repeat Yourself（同じことを繰り返さないこと）」を意味します。つまり、コードベースでは同じコードを何度も何度もコピー＆ペーストすべきではないということです。

> [info]
コードを複数の場所でコピー＆ペーストするのが悪い習慣なのは、なぜだと思いますか？

現在のロジックでは、2回無作為に回答を選んで表示するのに、同じロジックがあることがわかります。これを単一のメソッドへリファクタリングして、代わりにシェークのイベントとボタンのタップの両方からこのメソッドを呼び出すことができます。

> [action]
`ViewController.swift`において以下の方式を追加します：
>
```
func generateAnswer() {
    let maxIndex = UInt32(answers.count)
    let randomIndex = Int(arc4random_uniform(maxIndex))
>
    answerLabel.text = answers[randomIndex]
}
```

次に、コードをリファクタリングして、新しい`generateAnswer`メソッドを利用することができます：

> [action]
`shakeButtonTapped(_:)`および`motionEnded(_:with:)`の両方をそれぞれ、次のように変更してください：
>
```
@IBAction func shakeButtonTapped(_ sender: Any) {
    generateAnswer()
}
>
override func motionEnded(_ motion: UIEventSubtype, with event: UIEvent?) {
    guard motion == .motionShake else { return }
>
    generateAnswer()
}
```

アプリを実行して、新しいMagic 8-Ballをテストします。必ず、新しいシェークのジェスチャーと既存のボタンタップのロジックの両方をテストしてください。

iPhone 7シミュレーターでシェークジェスチャーをテストするには、必ずシミュレーターが有効であることを確認し、ハードウェアメニューを選択してください。ドロップダウンには、`Shake Gesture`のオプションがあります。

![Simulator Shake](assets/simulator_shake.png)

## まとめ

この最後のセクションでは、Storyboardで開発したUIを取り上げて、コードへとつなげました。StoryboardとSwiftソースファイルの関係、そしてこれらが基本的なレベルでどう通信するのかを検討しました。

ユーザーの基本的なジェスチャー（ボタンのタップとシェーク）に対応する方法を突き止めて、Magic 8-Ballを動作させるロジックをようやく実装しました。

次のセクションでは、今まで学んだことを見直してまとめを行います。
