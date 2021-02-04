---
title: 引数のデータ型にGAS固有オブジェクトを指定する方法
layout: post
tags: GAS
image: /images/at.png
---

この記事では、GASでドキュメンテーションコメントを書く際に、GAS独自のオブジェクトをデータ型に指定するにはどうすればよいかを説明しています。

## ドキュメンテーションコメントとは

GASの中級講座を受けて、小さな関数をドキュメンテーションコメントきちんとつけて書く！にはまっています。

一般に、ドキュメンテーションコメントは次のように書きます。

```js
/**
 * 関数の説明
 * @param {引数のデータ型} 仮引数名 - 仮引数の説明
 * @return {返り値のデータ型} 返り値の変数名 - 返り値の説明
 */
function myFunction(argument) {
  // ...
}
```

こうすることで、関数の呼び出し時にその関数の情報をGASが読み取って教えてくれるようになります。

実は返り値については、ドキュメンテーションコメントなしでもGASがコードからデータ型を予測して教えてくれるようです。GAS、賢い子…！

![show-datatype-1](/images/blog/smart-returnvalue-detection.png){:.img}

ドキュメンテーションコメントで`@return`を指定しなくてもデータ型を予測してくれる
{:.caption}

### 引数はコメントが必要

引数は、ドキュメンテーションコメントを書かないと予測してくれません。

![show-datatype-1](/images/blog/argumenttype-not-showing.png){:.img}

ドキュメンテーションコメントを書いていないので、引数`name`が`any`と表示されている
{:.caption}

`@param {データ型}`を書くことで、引数のデータ型も予測してくれるようになります。

![show-datatype-1](/images/blog/argumenttype-showing.png){:.img}

ドキュメンテーションコメントを書いたので、引数`name`が`string`と表示されるようになった
{:.caption}

## GASの固有オブジェクトだったら？

引数がプリミティブではなく、`CalendarEvent`などのGAS固有のクラスだったらどうすればいいでしょう？

`CalendarEvent`はクラス名なので、`{}`の中にそのまま書いてあげればいいような気がします。
  ```js
  /**
   * ...
   * @param {CalendarEvent} event - カレンダーイベント
   */
   function myFunction(event) {
     // ...
   }
  ```


しかし、これだとデータ型が認識されず、`any`と表示されてしまいます。

![show-datatype-1](/images/blog/datatype-not-showing.png){:.img}

クラス名をそのまま書いても`any`になってしまう
{:.caption}

むむむ…。せっかくドキュメンテーションを書いているんだから、GAS固有のオブジェクトもきちんとデータ型を書きたい！ですよね。どうすればいいでしょうか？

## 最上位のクラス名から書こう

GASの固有オブジェクトを予測に反映させるには、`{CalendarApp.CalendarEvent}`のように、アプリの最上位のオブジェクト名から書きます。

![show-datatype-1](/images/blog/datatype-showing.png){:.img}

型が反映された！
{:.caption}

よいですね☺️


`CalendarEvent`なら`CalendarApp`、`Sheet`や`Range`なら`SpreadSheetApp`のように、そのクラスが属する最上位のクラスオブジェクトから書いてあげればよいです。

ちょっとドキュメンテーションコメントが長くなってしまうのが気になりますが、型がきちんと表示されるのは嬉しいものです。

是非試してみてください☺︎
