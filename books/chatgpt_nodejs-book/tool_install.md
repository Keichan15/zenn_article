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

次章の[Visual Studio Codeのインストール]()にお進みください。
※この章では以降の内容を実施して頂く必要はありません。

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

次はコードを書く際に必要となるプログラミングエディターの**Visual Studio Code**を導入していきましょう！