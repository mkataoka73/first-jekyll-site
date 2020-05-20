---
title: Visual Studio Codeでの TypeScript チュートリアル
layout: post
description: Visual Studio CodeでのTypeScriptチュートリアルです。公式ドキュメントの翻訳です。
tags: [TypeScript, VS Code]
---

[TypeScript](https://www.typescriptlang.org/)はJavaScriptの拡張言語であり、JavaScriptに型付け機能を追加したものです。安定したコンポーネントをつくるためのクラスやモジュール、インターフェイスといった機能が提供されています。詳しくは[TypeScriptの詳細ドキュメント](https://github.com/Microsoft/TypeScript/tree/master/doc)に言語の詳細があります。

## コンパイラをインストールする

Visual Studio Codeは〔入力補完など〕TypeScriptをサポートする機能が含まれていますが、コンパイラ（`tsc`）は含まれていません。コマンド`tsc HelloWorld.ts`を実行してTypeScriptをJavaScriptに変換するには、現在のワークスペースかコンピュータ全体にコンパイラをインストールする必要があります。

npm（[Node.js Package Manager](https://www.npmjs.com/))
を使うのが最も簡単なやり方です。npmがインストールされていれば、次のコマンドでTypeScriptをコンピュータ全体にインストールすることが可能です。

```bash
npm install -g typescript
```

コンパイラがインストールされているか確認するには次のいずれかのコマンドを入力してください。

```bash
tsc --version
tsc --help
```

`npm install --save-dev typescript`と打つことで、ローカルつまり今いる作業フォルダだけにTypeScriptをインストールすることもできます。この場合、コンピュータにある他のTypeScriptプロジェクトに影響が及ぶ可能性を減らすことができ便利です。

### Compiler vs language service

VS Codeの言語サポートと、インストールされたコンパイラとは別の機能であるこということを念頭においておいてください。TypeScriptのファイルをVS Codeで開くとエディタがサポートしているバージョンがウィンドウ右下のステータスバーに表示されます。

<img src="https://code.visualstudio.com/assets/docs/typescript/compiling/version-status-bar.png" width="100%">

VSCodeがチェックするTypeScriptのバージョンを変える方法については、のちにこの記事の中で取り上げています。

## tsconfig.json

TypeScriptのプロジェクトでまず最初に行うことといえば、典型的には`tsconfig.json`ファイルをフォルダに追加することです。これは、プロジェクト内でのコンパイルオプションやコンパイルされるファイルといった、TypeScriptの設定を定義するものです。ソースコードを保存しておきたいファイルを開き、`tsconfig.json`という名前を付けたファイルを保存してください。編集中はIntelliSense（`⌃Space`{: .keybinding}）が手助けしてくれるでしょう。

<img src="https://code.visualstudio.com/assets/docs/typescript/compiling/tsconfigintellisense.png" width="100%">

ES5、CommonJSモジュール、ソースマップを記述した簡単な`tsconfig.json`ファイルは次のようになります。

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "sourceMap": true
  }
}
```

これで`.ts`のついたファイルを作成すれば、豊かなコード編集と構文チェッカーが体験できるでしょう。

## JavaScriptへの変換

VS Codeは`tsc`{:. code}コマンドを実行できるタスクランナーが付属しています。これを通して`.ts`ファイルを`.js`ファイルに変換できます。それだけでなく、関連したエラーや警告のメッセージも表示させることができます。これは[Problems](https://code.visualstudio.com/docs/editor/editingevolved#_errors-warnings)パネルに表示されます。実際に、シンプルなHello Worldプログラムをトランスパイルしてみましょう。

### Step1: ファイルの作成
VS Code上で空のフォルダを開き、`helloworld.ts`{: .code}というファイルを作成しましょう。その中に次のコードを書いてください。

```ts
let message: string = 'Hello World';
console.log(message);
```

コンパイラとコードが正しく動くか確認するために、ターミナルを開き、コマンド`tsc helloworld.ts`{: .code}を実行しましょう。VS Codeでは、ショートカット`` ⌃` ``{: .keybinding}でターミナルを開くことができます。

ファイルが変換され、`helloworld.js`というファイルが表示されるはずです。コンピュータに[Node.js](https://nodejs.org/)がインストールされている状態なら、`node helloworld.js`でこのファイルを実行することができます。

![build and run Hello World](https://code.visualstudio.com/assets/docs/typescript/compiling/build-hello-world.png){: .tutorial-img}

### Step2: TypeScript Build

グローバルターミナルから、**ビルドタスク** の実行をしてみましょう（ショートカット：`⇧⌘B`{: .keybinding}）。前のセクションで`tsconfig.json`を作成していれば、図のように候補が表示されるはずです。

![TypeScript Build](https://code.visualstudio.com/assets/docs/typescript/compiling/typescript-build.png){: .tutorial-img}

**tsc: build** を実行すると、`HelloWorld.js` と `HelloWorld.js.map`というファイルが作成されるはずです。

**tsc: watch** を選択すると、TypeScriptコンパイラはファイルを保存するごとにトランスパイルが行われます。

実際にはこれはコンパイルをタスクとして行ったものです。使っているコマンドは`tsc -p`です。

### Step 3:

### Step 4:


## SavaScript source map support
この項は翻訳中（ソースマップが何だかわからないので）
ソースマップは要するに、元のファイルを示すファイルなのかな
