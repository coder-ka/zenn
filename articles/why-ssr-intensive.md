---
title: "なぜSSRなのか"
emoji: "🐙"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

- Client-Server という構図
  - データの論理構造としてのドメイン
  - ドメインを実現するための Client-Server
  - データの可用構造としてのインターフェース
  - インターフェースを実現するための Client-Server
  - それぞれに Client-Server が必要
  - 分業のポイントをどこに設けて、どのようにそれを表現において隠蔽するか
  - なぜフロントエンドの分業観念は難解なのか
  - isomorphicとは
    - 純粋関数はisomorphic
    - windowオブジェクトやフロントエンド固有の副作用を伴う処理はインジェクトして代用可能
- フロントエンドの成立にサーバーが必要な理由
  - データ容量の問題
  - セキュリティの問題
    - 暗号化で解消可能？
    - 暗号化されたデータそのものへのアクセスが遮断されていればより安全であるのは間違いではない
  - システム世界でのリソースは無限だが生活世界でのリソースは有限
    - ソフト VS ハード
    - 高レベルレイヤー VS 低レベルレイヤー
    - ソリューション
      - ディレクティブ
        - 高レベルレイヤーでの表現の自由の実現の為に起きうる低レベルレイヤーでの問題を解決する為の実行指示
        - 低コスト
        - どの単位でディレクティブを要求するか
      - Eager SSR
        - SSRできるところはすべてする
        - 高コスト
- 種別的観点
  - Static
    - SWH(Static Website Hosting)（LP の固定ページ。Aboutページ等）
  - Complile-time
    - SSG(Static Site Generation)（数が決まってるグッズページとか）
  - Run-time
    - Static + SSR + CSR（数が変動的で量も多い可能性が高いユーザー投稿のページとか）
    - Static + CSR（アプリページとか）
