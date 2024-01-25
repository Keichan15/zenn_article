---
title: "各種インストール"
---

## Node.js導入の前に

ChatGPT-APIに触れるには、まずNode.jsを自身のPCにインストールする必要があります。

本章では、主にWindows端末にNode.jsを導入するパターンを解説していきます。

:::message
Macユーザーの方に関しては申し訳ございませんが、以下のリンクから同様にNode.jsをインストールして頂くようお願い致します。

https://prog-8.com/docs/nodejs-env
:::

## Node.jsがインストール済か確認する

既に何らかによって自身の端末にNode.jsが入っている場合があります。
以下の手順を実施し、Node.jsが自身の端末に導入済みかを確認してみましょう。

```Windowsキー``` + ```Rキー```を入力し、フォームに```cmd```と入力します。

![](/images/cmd.png)

以下のようなターミナルが開くことを確認します。

![](/images/terminal_open.png)

```node -v```と入力し、何らかのバージョンが表示されている場合は、ご自身の端末にNode.jsが既に導入されている状態です。
この場合、基本的にNode.jsの導入に関して何か実施して頂く必要はありません。

![](/images/node_ver.png)

次の[Visual Studio Codeのインストール](#visual-studio-codeのインストール)にお進みください。

:::message alert
既に上記でNode.jsを導入済みの場合、以降の[Node.jsのインストール]()を実施して頂く必要はありません。
:::

逆に```node -v```を入力して以下のような表示が出た場合はNode.jsがご自身の端末にまだ導入されていないことを示しています。

![](/images/node_notinstall.png)

この場合、以降の[Node.jsのインストール]()からNode.jsの導入を実施してください。

## Node.jsのインストール

[Node.jsの公式サイト](https://nodejs.org/en)にアクセスします。

![](/images/nodejs_homepage.png)

2種類表示されているボタンの内、左側の```20.11.0LTS```をクリックしします。
インストール時期によっては多少バージョンが異なる場合がありますが、基本的に左側のボタンをクリックすれば問題ありません。

エクスプローラを開き、ダウンロードしたNode.jsのインストーラをダブルクリックで起動します。
![](/images/msi.png)

以下の画像の通りにNode.jsのセットアップを実施します。
特段こだわり等が無ければ全て脳死```Next```ボタンクリックで問題ありません。

![](/images/setup_1.png)
![](/images/setup_2.png)
![](/images/setup_3.png)
![](/images/setup_4.png)
![](/images/setup_5.png)
![](/images/setup_6.png)
![](/images/setup_7.png)
![](/images/setup_8.png)

セットアップが完了したら、もう一度```Windowsキー``` + ```Rキー```を押下後に```cmd```と入力し、ターミナルに```node -v```と入力します。

![](/images/cmd.png)
![](/images/terminal_open.png)
![Alt text](/images/node_ver_new.png)

インストールしたNode.jsのバージョンが表示されていればOKです！
お疲れ様でした！

次はコードを書く際に必要となるコードエディターの**Visual Studio Code**を導入していきましょう！

## Visual Studio Codeのインストール
**Visual Studio Code**はMicrosoftが提供する、無償のコードエディタです。

各プラットフォーム(Windows, Mac, Linux)に対応しており、豊富な拡張機能を兼ね備えています。

余談ですが、最近このVisual Studio Codeをフォークして開発された新しいコードエディタの```Cursor```が話題沸騰中です。

https://cursor.sh/

AIが実装すべきコードを自動で生成してくれるんですって。。便利な世の中になりましたね。。

ちなみに後の章で取得するAPIキーを使用すれば、実質無制限でこのCursorにChatGPTを搭載してAIとコード書き書きが出来ちゃいます。めっちゃ便利ですよこれ。。

本題に戻り、今回はCursor..ではなく、**Visual Studio Code**をインストールしていこうと思います！

まずは[公式サイト](https://code.visualstudio.com/)にアクセスします。

![](/images/vscode_officialhp.png)

画面中央部の```Downlod for Windows```と書かれた青いボタンをクリックします。

押下すると以下の画面に遷移し、自動でインストーラ―がダウンロードされます。

![](/images/vscode_hp2.png)

ここからはNode.jsを導入した際と実施することはほぼ同じです。
エクスプローラーを開き、ダウンロードしたインストーラーを起動します。

![Alt text](/images/vscode_setup0.png)

画面の案内に沿って進めていきます。
こちらも基本的には脳死でどんどん進んで頂いて問題ありません。

![](/images/vscode_setup1.png)
![](/images/vscode_setup2.png)
![](/images/vscode_setup3.png)

追加タスクの選択は基本的に何も弄る必要は無いですが、ディレクトリやファイルをVSCodeで開くことが自分は多いので、```その他```項目の上2つにチェックを入れました。

![](/images/vscode_setup4.png)
![](/images/vscode_setup5.png)
![](/images/vscode_setup6.png)
![](/images/vscode_setup7.png)

```完了```ボタンを押下後、Visual Studio Codeが自動で起動すれば問題ありません！
(私のはなぜか以前使っていたQiitaのディレクトリが入ってるんですが…笑)

## 拡張機能のインストール

次に今回使用する拡張機能を入れていきましょう。
拡張機能は画面左側のテトリスのようなマークをクリックすると、拡張機能の検索画面に遷移できます。

![](/images/kakuchou_vscode.png)

今回は以下の2つを最低でも入れておけば何とかなります。

1つ目は**Japanese Language Pack for Visual Studio Code**です。
Visual Studio Codeを良い感じに日本語化してくれる拡張機能です。

![](/images/japanese_language.png)

2つ目は今回使用予定の**Thunder Client**です。

APIを手軽にテストできる拡張機能となっています。後々APIを叩く際により直感的にレスポンスを確認することができるので、個人的に良く使っています。

![](/images/Thunder_Client.png)

他にも様々な拡張機能が存在していますが、何を入れるかは皆さん次第です。
インターネットにはVisual Studio Codeの拡張機能が豊富に紹介されていますので、是非この機会に触れてみるのも面白いかもしれませんね。

準備が完了したところで、ようやくお待ちかねのChatGPTのAPIを触っていきましょう！