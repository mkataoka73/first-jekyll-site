---
title: 値渡しと参照渡しの違いを理解する
layout: post
date: 2021-02-20
tags: programming
excerpt: プログラミングにおける「値渡し」と「参照渡し」の違いを説明しています
---

[ノンプロ研](https://tonari-it.com/community-nonpro-semi/)中級GAS講座の復習。「値渡しと参照渡し」について、調べたことのメモ。

- [値渡しと参照渡しの違いを理解する（Ruby）](https://magazine.rubyist.net/articles/0032/0032-CallByValueAndCallByReference.html){:target="_blank"}
- [プログラミング基礎 - Qiita](https://qiita.com/TAKUYA-110/items/e289a07d3333199711a2#13-%E3%83%A1%E3%83%A2%E3%83%AA){:target="_blank"}
- [Values, Types, and Operators :: Eloquent JavaScript](https://eloquentjavascript.net/01_values.html#h_sVZPaxUSy/){:target="_blank"}

## 値渡しと参照渡しの違いを理解する（Ruby）

まずはここをみました。Rubyという言語にもとづいているので、GASユーザーの方にとっては見慣れないコードも多いかもしれないです。翻訳？を載せます。

```js
function add(a, b) {
  return a + b;
}
```

```rb
def add(a, b)
  a + b # Rubyは return キーワードが省略可能
end
```

### 理解したこと
- 値の渡し方には、値渡しと参照渡しの2種類がある
- 参照の値渡しというものがあるが、それは値渡しの一種である
- 値渡しの渡すものが参照の値になると、それは参照の値渡しである
- Rubyを含む多くの言語は、値渡しを採用している

## JavaScript参照渡し/値渡しなど存在しない？

- [JavaScriptに参照渡し/値渡しなど存在しない - Qiita](https://qiita.com/yuta0801/items/f8690a6e129c594de5fb){:target="_blank"}
- [【JavaScript】 参照渡し？値渡し？これで悩む必要がなくなる！かも](https://affi-sapo-sv.com/note/js-reference-or-value.php#gsc.tab=0){:target="_blank"}

### 理解したこと
推測も混じっているのですが、おそらくは、

- JavaScriptもRubyと同じく値渡しの言語である
- JSで参照渡しと言われているものは、厳密には参照の値渡しである
- よってJSには値渡ししか存在しない（=値渡し/参照渡しの区別が存在しない。しなくていい）

## メモリについてやもう少し原論的なところ

- [プログラミング基礎 - Qiita](https://qiita.com/TAKUYA-110/items/e289a07d3333199711a2#13-%E3%83%A1%E3%83%A2%E3%83%AA){:target="_blank"}
- [Values, Types, and Operators :: Eloquent JavaScript](https://eloquentjavascript.net/01_values.html#h_sVZPaxUSy/){:target="_blank"}

- メモリとは、コンピュータの短期記憶・ワーキングメモリみたいなものと解釈する
- プログラムが動く時、使われて、終わると解放される
- 長期記憶は、CDとか

こんなふうに理解しました。
