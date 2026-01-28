---
title: "VMWare Workstation ProとUbuntu Desktopのインストール"
---

## Broadcomのアカウント作成
以下の公式ドキュメントを参考に、Broadcomのアカウント登録を行ってください。

https://knowledge.broadcom.com/external/article/226420

画像も差し込みながら解説します。

1. Broadcomのサポートページにアクセスする
https://support.broadcom.com/

![](/images/vmware_and_ai_knkwledge_book/image-1.png)

2. 右上の「Register」をクリック
![](/images/vmware_and_ai_knkwledge_book/image-2.png)

3. メールアドレスと画像に表示されている文字列を入力し、「Next」をクリック
![](/images/vmware_and_ai_knkwledge_book/image-3.png)

4. Verification Codeがメールに届くので、確認して入力し「Verify & Continue」をクリック
![](/images/vmware_and_ai_knkwledge_book/image-4.png)

![](/images/vmware_and_ai_knkwledge_book/image-5.png)

5. 基本情報を入力して、「Create Account」をクリック
特にパスワードは要件がかなり厳しいです。

- パスワード要件：
    - 8 文字以上
    - 英字小文字
    - 英字大文字
    - 数字
    - 記号
    - ユーザー名の一部をパスワードに使用することは出来ません
![](/images/vmware_and_ai_knkwledge_book/image-6.png)

6．「I'll do it later」をクリック
![](/images/vmware_and_ai_knkwledge_book/image-7.png)

これでベーシックユーザーアカウントの作成が完了しました。
次にVMWare Workstation Proをインストールしてみましょう。

## VMWare Workstation Proのインストール
こちらも公式ドキュメントを参考に導入します。
https://knowledge.broadcom.com/external/article/226522

1. サポートポータルサイトにアクセスし、右上の「Login」ボタンを押下する
![](/images/vmware_and_ai_knkwledge_book/image-8.png)

2. サインインします。UsernameはメールアドレスでOK
![](/images/vmware_and_ai_knkwledge_book/image-9.png)

3. パスワードを入力する
![](/images/vmware_and_ai_knkwledge_book/image-10.png)

以下の画面が表示されていればログインは完了です。
![](/images/vmware_and_ai_knkwledge_book/image-11.png)

4. ポータルサイト右上のボタンから「VMWare Cloud Foundation」をクリック
![](/images/vmware_and_ai_knkwledge_book/image-12.png)

5. searchに「workstation」と入力して検索する
![](/images/vmware_and_ai_knkwledge_book/image-13.png)

6. VMWare workstation Pro 17.0をダウンロードする
途中で住所等の情報を入力する必要が有ります。
![](/images/vmware_and_ai_knkwledge_book/image-14.png)

![](/images/vmware_and_ai_knkwledge_book/image-15.png)

![](/images/vmware_and_ai_knkwledge_book/image-16.png)

![](/images/vmware_and_ai_knkwledge_book/image-17.png)

![](/images/vmware_and_ai_knkwledge_book/image-18.png)

![](/images/vmware_and_ai_knkwledge_book/image-19.png)

7. VMWare Workstation Proのexe実行
※途中でアップグレードのキャプチャがありますが、私の環境には既に入っているためです。
　初めてインストールされる方はインストールの表記になると思います
![](/images/vmware_and_ai_knkwledge_book/image-20.png)
![](/images/vmware_and_ai_knkwledge_book/image-21.png)
![](/images/vmware_and_ai_knkwledge_book/image-22.png)
![](/images/vmware_and_ai_knkwledge_book/image-23.png)
![](/images/vmware_and_ai_knkwledge_book/image-24.png)
![](/images/vmware_and_ai_knkwledge_book/image-25.png)
![](/images/vmware_and_ai_knkwledge_book/image-26.png)

これでVMWare Workstation Proのインストールも完了しました。
最後にUbuntu Serverを入れましょう。

## Ubuntu Desktop仮想マシン構築
各種OS共通して、仮想マシンの構築には以下が必要です。

- USBメモリ(8GB以上)
- ネットワークにつながるPC

またダウンロードするisoファイルはサイズがどえらいので、勉強会の間でダウンロードするのは不可能に近いです。
そのため私の資料では、過去にisoをダウンロードしていたのでそれを使用して話を進めます。

1. 左上のファイル > 新しい仮想マシン を選択
![](/images/vmware_and_ai_knkwledge_book/image-27.png)

2. ゲストOSのインストールで「インストーラ ディスクイメージファイル」を選択し、ダウンロードしたisoファイルを指定する
![](/images/vmware_and_ai_knkwledge_book/image-28.png)
![](/images/vmware_and_ai_knkwledge_book/image-29.png)

3. 画面表記に沿ってボタンポチポチ
![](/images/vmware_and_ai_knkwledge_book/image-30.png)
![](/images/vmware_and_ai_knkwledge_book/image-31.png)
![](/images/vmware_and_ai_knkwledge_book/image-32.png)

4. 起動確認
![](/images/vmware_and_ai_knkwledge_book/image-33.png)

本当はGitLabの導入までやりたかったんですが、時間がないので今回は割愛します。
これでUbuntu Serverの仮想マシン構築ができました！

誰でも簡単に作成でき、不要になればすぐ削除できるのはVMWare Workstation Proならではのメリットですので
是非是非使ってみてください！
