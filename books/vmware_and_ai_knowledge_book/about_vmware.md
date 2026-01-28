---
title: "VMWare/VMWare Workstation Proについて"
---

## VMWareとは
ハンズオンを始める前に、とにもかくにもVMWareについて知るところから始めていきましょう！
実は天下の富士通様が、VMWareについて以下のホームページを公開しています。

https://pfs.nifcloud.com/vmware/about_vmware.htm

VMWare(https://www.vmware.com/)は、複数の仮想マシン・ソフトウェアを提供している企業のことです。

実はVMWareは2023年にBroadcomに買収されています。これは当時ネットではかなり賛否両論がありました。
買収を行ったBroadcomですが、それはまあまあ悪い噂が流れていることで有名で、代表例を挙げるとサポートの質がすこぶる悪いと評判です。（？）
特にこのRedditのコメント欄などを見ていると、いかにサポートの対応が終わっているかを肌で感じて頂けると思います。

https://www.reddit.com/r/sysadmin/comments/1d7yoh7/broadcom_support_is_hot_garbage/?tl=ja

また法人目線に話題を変えると、買収前までは永続ライセンスとして提供されていたサービスがサブスクリプションサービスに切り替わりました。
そのため保守契約におけるライセンス更新などでライセンス料が発生し、結果としてコスト増の懸念が発生します。

またライセンス課金体系もCPUソケット単位からCPUコア単位に切り替わったことで、多コアで稼働しているサーバーなどはサブスクリプション契約によって爆発的に費用が増加する可能性が考えられます。

https://www.jbcc.co.jp/blog/column/vmwaremgn.html

ここまで聞くとVMWareが評判が悪いというより、VMWareを買収したBroadcomの評判が悪いんですよね。
流れ弾を食らっているような状態です。悲しい・・・。

## VMWare Workstation Proとは
反面、Broadcomの買収によって思わぬラッキー要素も舞い込んできました。
それがこの **VMWare Workstation Pro** です。

https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion

なんと買収により、個人・商用利用問わず利用が無償化されました。つまり誰でも気軽に仮想マシンを構築して色々遊べるようになったという訳です。

VMWare Workstation ProはWindowsやLinuxなどのPC上に複数のOSを同時実行できる仮想化ソフトウェアです。
ざっくりとしたイメージとしてはPCの中に別のPCが入っているといった感じでしょうか。

PCを普段使いする上ではまず上記のようなケースを作りたいと思うことは無いと思いますが、
IT業界に生息しているとさまざまなOSに触れる機会も増えてくることでしょう。
その都度対象のOSが入った物理マシンを購入するのは、コスト面などを考えるとあまりにも見合わない投資です。

このような場合にVMWareは1台のPCで複数のOSを気軽に試すことができ、気軽に環境を破壊できるというメリットがあります。

今回は皆さんのPCにVMWare Workstation Proを導入し、Ubuntu Desktopを導入してLinux環境を構築してみましょう！
※当初RHEL9の予定でしたが、isoファイルの取得にRedHatアカウントの作成が必要で面倒なのでやめます