---
title: "viteとReactを使ってSSRするのがとても簡単だった（SPAとSSGにも対応）"
emoji: "📑"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [
    "vite",
    "ssr",
    "ssg",
    "react"
]
published: false
---

- SSRとは
  - SSRが必要な理由
  - SSRが難しい理由
- viteを使うとできること
  - viteのバージョン、Reactのバージョン
  - 部分的にSSRしないようにできる
  - SSR側のコードもHot Reload対象
- 実際にやってみる
  - まずはSPAのプロジェクトを作成
  - ホスティングサーバーの挙動をカスタマイズできるようにする
  - SSR
  - SPA
  - SSG
  - キャッシュ
- プロダクション用のサーバーを作る
