---
title: "オブジェクト指向モデリングのためのドキュメントテンプレート"
emoji: "🍣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---

- 設計と実装の仕方について（Wiki 管理）
  - ドメインモデル設計
    - エンティティ
      - 設計
      - 実装
        - [cakephp4 application rule](https://book.cakephp.org/4/ja/orm/validation.html#application-rules)
        - Active Record Pattern
    - 値オブジェクト
      - 設計
      - 実装
        - [cakephp4 data type](https://book.cakephp.org/4/ja/orm/database-basics.html#id8)
        - [cakephp4 data validation](https://book.cakephp.org/4/ja/orm/validation.html#validating-request-data)
    - 関係
      - 設計
      - 実装
        - [cakephp4 association](https://book.cakephp.org/4/ja/orm/associations.html)
  - ユースケース設計
    - S（主語＝システム的なユーザー、権限制御は目的語で表現する）
      - 設計（システム的なユーザー種別）
      - 実装
    - V（動詞＝アクション、リクエストメソッド）
      - 設計
      - 実装
        - [cakephp4 routes](https://book.cakephp.org/4/ja/development/routing.html)
        - [cakephp4 controller](https://book.cakephp.org/4/ja/controllers.html)
    - O（目的語＝エンティティの集合）
      - 設計
      - 実装
        - [cakephp4 query builder](https://book.cakephp.org/4/ja/orm/query-builder.html)
        - [cakephp4 controller](https://book.cakephp.org/4/ja/controllers.html)
  - 認証設計

- 実際の設計（リポジトリ管理）
  - ドメインモデル
  - ユースケース
  - 認証
