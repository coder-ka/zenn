---
title: "esbuildでライブラリを作る（TypeScript対応）"
emoji: "📚"
type: "tech"
topics:
  - "npm"
  - "esbuild"
  - "ライブラリ作成"
published: false
published_at: "2022-01-08 16:12"
---

以前、viteでライブラリを作る方法を説明しました。

https://zenn.dev/drop_table_user/articles/7b043bef6cec29

今回はesbuildを利用してライブラリの作成方法を説明します。

esbuildを使うと非常に簡単で爆速な開発体験ができます。

ただし viteで作る場合と違う点としてUMDをサポートしませんので、ブラウザならESM対応(`<script type="module">`)か事前のバンドラーによる処理が必要になります。（CommonJSには対応しているので、Node.jsに関しては特別な処置は不要です。）

# esbuildの導入

まずインストールからです。

```bash
npm install -D esbuild concurrently
```

（concurrentlyは本来不要ですが、最適化のために入れています）

あとは下記のようにscriptを設定すれば終わりです。

```json:package.json
{
  ...
  "scripts": {
    "build": "concurrently --raw \"npm run build:mjs\" \"npm run build:cjs\"",
    "build:mjs": "esbuild lib/main.ts --bundle --minify --format=esm --outfile=dist/lib-name.mjs",
    "build:cjs": "esbuild lib/main.ts --bundle --minify --format=cjs --outfile=dist/lib-name.cjs"
  },
  ...
}
```

`lib/main.ts`はエントリーポイントで、`dist/lib-name.mjs`と`dist/lib-name.cjs`は出力ファイルの指定です。

`npm run build`でビルドされます。

少しオプションの説明をすると、

`--bundle`で変換のみでなくバンドルを行い、`--minify`で最小化をしています。

また、`--format`を使って、esm（ESModule）とcjs（CommonJS）の両方を出力しています。。

では、これらをパッケージファイルとして指定するための`pakcage.json`の設定をしていきましょう。

# package.json

以下のように指定することで、ブラウザとNodeどちらも対応できます。

```json:package.json
{
  "main": "./dist/lib-name.cjs",
  "module": "./dist/lib-name.mjs",
  "exports": {
    "import": "./dist/lib-name.mjs",
    "require": "./dist/lib-name.cjs"
  },
}
```

# TypeScript対応

まずはインストールからです。

```bash
npm install -D typescript
```

そして、`tsconfig.json`を下記のように設定します。

`tsconfig.json` の設定値についてはライブラリ作成に直接関連しないものも含まれています。

詳しくは以下で説明しているのでよかったら読んでみてください。

https://zenn.dev/drop_table_user/articles/7b043bef6cec29#typescript%E3%81%AB%E5%AF%BE%E5%BF%9C

次に、生成される定義ファイルを`package.json`で指定します。

```json:package.json
{
  ...
  "types": "./types/main.d.ts",
  ...
}
```

# パッケージに含めるファイルの指定

dist（配布フォルダ）とtypes（型定義フォルダ）を含める必要があるので、下記のように指定します。

```json:package.json
{
  ...
    "files": [
      "/dist",
      "/types"
  ],
  ...
}
```

# 公開

パッケージの公開については、以下のサイトがうまくまとめているので参照してください。

https://chaika.hatenablog.com/entry/2019/08/15/000000

といっても、

1. [公式サイト](https://www.npmjs.com/)でNPMアカウントの作成
2. `npm login`
3. `npm publish`（scope=@～/を付ける場合は、`--access=public`も必要）

をするだけです。

バージョンとライセンスは好きなものを設定しましょう。


# あわせて読みたい

テストの追加方法も載せているので、是非読んでいただければと思います。

https://zenn.dev/drop_table_user/articles/5287a9b6859a59