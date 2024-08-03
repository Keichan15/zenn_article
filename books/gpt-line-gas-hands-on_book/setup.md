---
title: "各種セットアップ"
---

## Googleアカウントの準備
GASを使用するためにはGoogleアカウントが必要です。
詳しい作成方法についてはここでは省略します。

https://support.google.com/accounts/answer/27441?hl=ja-JP

## OpenAI APIキー取得
次にChatGPTを使用するためのOpenAI APIキーを取得します。

取得方法については以前の勉強会資料を使用するので、以下のリンクをご覧ください。
初めて登録される方・継続利用の方含めクレジットカードの登録が必須です。使用しなければ課金されることはありません。

:::message
既に作成されている方は LINE Developers アカウント作成 にお進みください。
:::

https://zenn.dev/keichan_15/books/gpt-api_nodejs_book/viewer/chatgpt_api_lesson#openai-%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88%E4%BD%9C%E6%88%90

OpenAI APIキーは以降の実装時に使用するので、必ずどこかにコピーしておくようにお願いします。

## LINE Developers アカウント作成

まずはLINE Developersのアカウント登録が必要です。
以下のリンクからLINE Developersのサイトにアクセスします。

https://developers.line.biz/ja/

![alt text](image.png)

右上の```コンソールにログイン```をクリック。

![alt text](image-1.png)

```LINEアカウントでログイン```をクリック。

![alt text](image-2.png)

お好きな方法でログインしてください。
個人的にはQRコードログインが簡単でした。

ログインが完了し以下の画面が表示されていればOKです。

![alt text](image-3.png)

## 基本情報設定とチャンネルアクセストークンの取得
ログインしたついでに基本情報の設定と、GASの実装時に必要なチャンネルアクセストークンを取得します。

```新規プロバイダー作成```をクリックします。

![alt text](image-4.png)

プロバイダー名を入力します。今回は**test_gpt_bot**としました。

![alt text](image-5.png)

```作成```ボタンをクリックするとプロバイダーが作成されます。

```プロバイダー設定```のタブを開き、作成したプロバイダーが確認できればOKです。

![alt text](image-6.png)

続いて```チャネル設定```のタブを開き、左から2番目の```Messaging API```をクリックします。

![alt text](image-7.png)

クリックすると基本情報を入力する箇所があるので、こちらは任意の内容を入力しましょう。
自分はこんな感じで入力しました。

![alt text](image-8.png)

![alt text](image-9.png)

ちなみに僕は有名人でもコメディアンでもないです・・。

最後にチェックボックスにチェックを入れるのをお忘れなく！

![alt text](image-10.png)

```作成```を押すと以下のモーダルウィンドウが表示されるので、問題なければ```OK```をクリックしましょう。

![alt text](image-11.png)

```同意する```をクリック。

![alt text](image-12.png)

```同意する```をクリック。

![alt text](image-13.png)

これでGPTくんのBotが作れました。

![alt text](image-14.png)

```Messaging API設定```のタブを開くとQRコードが表示されています。
このQRコードを読み取ると、GPTくんの公式アカウントを友達追加できます。

つまりこのGPTくんの公式アカウントにメッセージを送り、返信が来るといった仕組みになります。

![alt text](image-15.png)

続いて少し下にスクロールすると```応答メッセージ```と```あいさつメッセージ```を編集する画面が表示されます。
こちらはそれぞれ無効にしておきます。

![alt text](image-16.png)

![alt text](image-17.png)

最後に```チャンネルアクセストークン```を取得します。
このトークンがGASで必要になるので、必ずどこかにメモしておいてくださいね。

![alt text](image-18.png)


## GASの準備
最後にGASの準備をしましょう。

GASはGoogleスプレッドシート内から開くことができます。
まずはご自身のGoogleアカウントにログインいただき、以下のリンクにアクセスしてGoogleスプレッドシートを作成します。
