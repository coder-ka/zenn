---
title: "めも"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

- データ
  - データ構造・・・データの統語論的側面（コードの見やすさ、審美的側面）
  - データ型・・・データの意味論的側面（コードの正しさ、論理的側面）
- 関数型とかオブジェクト指向とか
  - 関数型プログラミング → 数学的な構造＝データ構造と数学的な演算＝純粋関数によってあらゆる処理を表現する。（代数学）
  - オブジェクト指向 → オブジェクトというデータ構造によって存在を定義づける関係をすべて記述する。（存在は関係の結び目である＝オントロジー）
  - オブジェクト指向関数型プログラミングとは
- サイト
  - 種別的観点
    - 静的サイトホスティング（LP の最初とか）
    - SSG（数が決まってるグッズページとか）
    - Run-time
      - SSR＋CSR（ユーザー投稿のページとか）
      - CSRのみ（アプリページとか）
  - タイミング的観点
    - Build-time
    - Run-time
      - Server-Run-time
      - Client-Run-time
- 物理的に長距離な通信
  - なぜ必要か
    - データ容量の問題
    - セキュリティの問題
      - 暗号化で解消可能？
      - 暗号化されたデータそのものへのアクセスが遮断されていればより安全であるのは間違いではない
    - imaginary infinity VS real finity
    - 思念的世界は無限だが現実的世界は有限
    - ソフトVSハード
    - ディレクティブ
      - 高レベルレイヤーでの表現の自由の実現の為に起きうる低レベルレイヤーでの問題を解決する為の実行指示
