---
title: "ライブラリのテストをavaで簡単に作る（TypeScript対応）"
emoji: "💡"
type: "tech"
topics:
  - "typescript"
  - "ライブラリ"
  - "テスト"
  - "ava"
published: false
published_at: "2022-01-08 16:40"
---

以前、esbuildやviteでJSのライブラリを作る方法を紹介しました。

https://zenn.dev/drop_table_user/articles/6aa0b4c706e201

https://zenn.dev/drop_table_user/articles/7b043bef6cec29

avaを使うと簡単にテストを追加できるので紹介しておきます。

# インストール

ava+TypeScriptに対応するためにts-nodeを追加します。

```bash
npm install -D ava ts-node
```

# テストの作成

`/tests/hoge.test.ts` を作ります。

```ts
import test from 'ava';

const fn = () => 'foo';

test('fn() returns foo', t => {
	t.is(fn(), 'foo');
});
```

# 設定ファイルを作成

`/ava.config.cjs` を作ります。

```ts
module.exports = {
  extensions: ["ts"],
  require: ["ts-node/register"],
};
```

ちなみに`ts-node/register/transpile-only`とすると型エラーは無視してくれます。

# tsconfig.jsonのmoduleをCommonJSにしておく

ts-nodeで実行するため、tsconfig.json内のmoduleオプションはCommonJSでないといけません。

```json:tsconfig.json
{
  "compilerOptions": {
    "module": "CommonJS",
  },
}
```

ESMのまま実行するやり方もあるのですが、面倒なので止めました。

CommonJSでもesbuildやviteのバンドルには影響がないので、基本は大丈夫だと思います。

# 実行

最後にpackage.jsonに以下を追加し、`npm test`を実行して終わりです。

```json:package.json
{
  "scripts": {
    "test": "ava"
  }
}
```
