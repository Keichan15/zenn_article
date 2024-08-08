---
title: "デプロイと動作確認"
---

では最後にデプロイをしてLINEBotを使用可能な状態にしていきます。
右上の```デプロイ```ボタンから```新しいデプロイ```をクリック。

![](/images/image-27.png)

歯車マークから```ウェブアプリ```を選択します。

![](/images/image-28.png)

以下のデプロイ画面が開きます。

![](/images/image-29.png)

アクセスできるユーザーを**全員**に設定します。
ここを必ず忘れずに設定してください。じゃないとデプロイしても使えない～～。

その後```デプロイ```をクリック。

![](/images/image-30.png)

```アクセスを承認```をクリック

![](/images/image-31.png)

ご自身のGoogleアカウントを選択します。

![](/images/image-32.png)

左下のリンクをクリックすると```Go to プロジェクト名```のリンクがあるので、それをクリックします。

![](/images/image-33.png)

```Allow```をクリック。

![](/images/image-34.png)

GASに戻り、以下の画面が表示されていればデプロイはOKです。
下の**ウェブアプリのURL***をコピーします。

![](/images/image-35.png)

[LINE Developers](https://developers.line.biz/ja/)に戻り、```Messaging API設定```の**Webhook設定**までスクロール。

![](/images/image-36.png)

```編集```をクリックし、先ほどのGASのウェブアプリのURLを貼り付けして```更新```ボタンをクリック。

![](/images/image-37.png)

![](/images/image-38.png)

```検証```ボタンを押下して**成功**と表示されればOKです。

![](/images/image-42.png)

稀に302Foundが出るときもあります。問題はないです。

![](/images/image-39.png)

最後に```Webhookの利用をオン```にしておきます。

![](/images/image-40.png)

これでデプロイのすべての操作が完了しました。

最後にLINE Botにメッセージを送り、返信がこれば完成です！

![](/images/image-41.png)

お疲れさまでした！！

