---
title: "（Webアプリ開発者のための）ぼくがかんがえたさいきょうの趣味Webサービス公開"
emoji: "🍣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

みなさんは趣味で何か作ってWebに公開していますか？

私は、とてもじゃないけれどここには載せられないようなクオリティのサイトを作って、誰も来ないのにAmazonへのリンクを貼っています。

そんな体たらくでも、やはり何かを作るだけでなく、**公開すること**は創作活動のモチベーションとしては大事なものです。

そして「公開する」ということは**当然インフラが必要**で、趣味のサービス開発者にとって、金銭的にも、作業のモチベーションとしても、Webアプリ開発者にとって最も大きな壁として立ちはだかるものです。（インフラエンジニアの方には楽しい作業かもしれませんが）

我々Webアプリ開発者にとっての**本質**は「サービスを作り込むこと」であり、他のことはなるべく考えずに済ませたいものなのです。

例えば、

- 月額固定で使えないだろうか
- デプロイする前に確認できる環境欲しいなあ
- クラウドを使うと知らないうちにサービスを使っていて、余計なお金がかかってそうで心配だ！フルマネージドは敵だ！^[[ぜいたくは敵だ!](https://ja.wikipedia.org/wiki/%E5%9B%BD%E6%B0%91%E7%B2%BE%E7%A5%9E%E7%B7%8F%E5%8B%95%E5%93%A1)]）
- 万が一バズっちまった時にどうスケールさせようか
- マネタイズしたいなぁ（主に広告）
- etc...

ということを考えなくてはいけないわけです。

**分かりました。私が代わりに考えましょう。しかも"さいきょう"のを。**

幸い昨今においては、DockerやTerraformの存在や、GithubのDevOps関連の進化のおかげで、ぼーっと空を見ている間に作ったアプリが世間に公開されるような、とにかく楽をできる下地が整ってまいりました。

私のような非インフラエンジニアでも、最低限のものは作れるようになってきたのです。

「Webアプリ開発者が考えたインフラなんて心配で使えない！」という方もいらっしゃるでしょう。

ごもっともです。

しかし、あくまで**趣味の開発のための知見共有**でございますので、そのあたり了解した上で読んでもらえればと思います。（というか、おかしいところあったら教えて貰いたい）

ちなみに「お金はあまり気にしない」という方は、Google CloudのCloud Runを使うとあっという間にデプロイできて、スケールも簡単なのでそちらをご利用ください。（Cloud Runが高額なわけでは無いのですが、月額固定ではないので心配になる可能性あり、DB使わないならむしろ安上りかも）

# とにかくさっさとWebサービスを公開したい方へ

Github上にボイラプレートのリポジトリを作ったので、READMEの手順を何も考えずに進めてもらうこともできます。

ただし、バックエンドの言語を変更したい場合（例えば、Goメインで書きたい方）は、Dockerfileの書き方を知っている必要があるのでご注意ください。（リポジトリはNode.jsです）

※ GoやRustバージョンのブランチとか作ってPR送ってもらえたら泣いて喜びます

# ざっと説明

1. バニラのサーバーをLinodeで調達
2. サーバーのセットアップはTerraformで自動化
3. Github Actionsでテスト、Dockerイメージのビルド、プッシュ
4. 3.の後、Github ActionsでサーバーにSSHして、Docker Swarmのクラスタを更新（デプロイ）
5. Docker Swarmでクラスタ管理
6. Github Actionsと環境変数で必要に応じてスケール
7. mainへのPRごとに確認用の環境生成（マージ後に削除）
8. ドメインは一つだけ取得して、Webサービスごとにサブドメインを割り振る