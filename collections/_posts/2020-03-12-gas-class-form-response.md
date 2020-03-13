---
layout: post
title: Google Apps ScriptドキュメントFormResponseページを和訳する
date: 2020-3-12
tags: [programming, gas]
description: Google Apps Script(GAS)のFormResponseクラスのドキュメントページの日本語訳です。
---
Google Apps Scriptの、[Class FormResponseページ](https://developers.google.com/apps-script/reference/forms/form-response){:target="_blank"_, :rel="noopener"}の和訳です。

## FormResponseクラス

<code>FormResponse</code>はフォームへの回答の全体を表し、3つの使用法があります。
1. 回答者により送信された回答にアクセスする（参照：<code>getItemResponses()</code>）、
2. スクリプト上からフォームの回答を送信する（参照：<code>withItemResponse(response)</code>および<code>submit()</code>）、
3. 回答を事前入力したURLを生成する

の3つです。

<code>FormResponse</code>は<code>Form</code>クラスから作成とアクセスが可能です。

```js
// フォームをIDで開き、質問ごとの回答を表示する
var form = FormApp.openById('abcdefghijklmnopqrstuvwxyz');
var formResponses = form.getResponses();
for (var i = 0; i < formResponses.length; i++) {
  var formResponse = formResponses[i];
  var itemResponses = formResponse.getItemResponses();
  for (var j = 0; j < itemResponses.length; j++) {
    var itemResponse = itemResponses[j];
    Logger.log('#%s番目の質問"%s"への回答は "%s"です',
        (i + 1).toString(),
        itemResponse.getItem().getTitle(),
        itemResponse.getResponse());
  }
}
```

## Methods

<table rules="rows">
  <thead>
    <tr>
      <th scope="col" class="method">メソッド</th>
      <th scope="col" class="return">返り値</th>
      <th scope="col" class="description">概説</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">getEditResponseUrl()</th>
      <td class="return">String</td>
      <td>送信済みの回答を編集するのに必要なURLを生成</td>
    </tr>
    <tr>
      <th scope="row">getGradableItemResponses()</th>
      <td class="return">ItemResponse[]</td>
      <td>フォーム回答内にあるすべての項目の回答を取得。順番はオリジナルのフォームにある通りになる</td>
    </tr>
    <tr>
      <th scope="row">getGradableResponseForItem(item)</th>
      <td class="return">ItemResponse</td>
      <td>フォームへの回答内にある、特定の項目への回答を取得</td>
    </tr>
    <tr>
      <th scope="row">getId()</th>
      <td class="return">String</td>
      <td>回答のIDを取得</td>
    </tr>
    <tr>
      <th scope="row">getItemResponses()</th>
      <td class="return">ItemResponse[]</td>
      <td>フォーム回答内にあるすべての項目の回答を取得。順番はオリジナルのフォームにある通りになる</td>
      <!-- QUESTION: 上のgetGradableItemResponsesと同じ？ -->
    </tr>
    <tr>
      <th scope="row">getRespondentEmail()</th>
      <td class="return">String</td>
      <td>回答者のメールアドレスを取得（ <code>Form.setCollectEmail(collect)</code>が有効になっている場合） </td>
    </tr>
    <tr>
      <th scope="row">getResponseForItem(item)</th>
      <td class="return">ItemResponse</td>
      <td>引数で与えられた項目に対する回答を取得</td>
    </tr>
    <tr>
      <th scope="row">getTimeStamp()</th>
      <td class="return">Date</td>
      <td>フォーム送信時のタイムスタンプを取得</td>
    </tr>
    <tr>
      <th scope="row">submit()</th>
      <td class="return">FormResponse</td>
      <td>回答を送信する</td>
    </tr>
    <tr>
      <th scope="row">toPreFilledUrl()</th>
      <td class="return">String</td>
      <td>このフォームの回答を事前入力したページの短縮URLを生成</td>
    </tr>
    <tr>
      <th scope="row">withItemGrade(gradedResponse)</th>
      <td class="return">FormResponse</td>
      <td>フォームへの回答に、引数で与えられた項目のグレードを追加する。</td>
    </tr>
    <tr>
      <th scope="row">withItemResponse(response)</th>
      <td class="return">FormResponse</td>
      <td>フォームへの回答に、引数で与えられた項目への回答を追加する。</td>
    </tr>
  </tbody>
</table>
