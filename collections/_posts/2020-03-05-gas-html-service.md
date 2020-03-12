---
layout: post
title: Google Apps ScriptドキュメントClass HTMLServiceページを和訳する
date: 2020-3-5
tag: [programming, gas]
description: Google Apps Script(GAS)のHTML Serviceクラスのドキュメントページの日本語訳です。
---
Google Apps Scriptの、[Class HtmlServiceページ](https://developers.google.com/apps-script/reference/html/html-service)の和訳です。

## 背景
Google Apps Scriptで、モーダルウィンドウを持ったシートのアプリを作りたい。英単語テストアプリで、諸々の設定情報を一気に入れられるHTMLフォームを作るのが目標。

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
      <th scope="row">createHtmlOutput()</th>
      <td class="return">HtmlOutput</td>
      <td>新規HtmlOutputを作成</td>
    </tr>
    <tr>
      <th scope="row">createHtmlOutput(blob)</th>
      <td class="return">HtmlOutput</td>
      <td>BlobSourceのリソースから新規HtmlOutputを作成</td>
    </tr>
    <tr>
      <th scope="row">createHtmlOutput(html)</th>
      <td class="return">HtmlOutput</td>
      <td>新規HtmlOutputを作成</td>
    </tr>
    <tr>
      <th scope="row">createHtmlOutputFromFile(filename)</th>
      <td class="return">HtmlOutput</td>
      <td>プロジェクト内のファイルから新規HtmlOutputを作成</td>
    </tr>
    <tr>
      <th scope="row">createTemplate(blob)</th>
      <td class="return">HtmlTemplate</td>
      <td>BlobSourceから新規HTMLテンプレートオブジェクトを作成</td>
    </tr>
    <tr>
      <th scope="row">createTemplate(html)</th>
      <td class="return">HtmlTemplate</td>
      <td>新規HTMLテンプレートオブジェクトを作成</td>
    </tr>
    <tr>
      <th scope="row">createTemplateFromFile(filename)</th>
      <td class="return">HtmlTemplate</td>
      <td>プロジェクト内のファイルから新規HTMLテンプレートオブジェクトを作成</td>
    </tr><tr>
      <th scope="row">getUserAgent()</th>
      <td class="return">String</td>
      <td>現在使用しているブラウザのユーザエージェントを返す</td>
    </tr>
  </tbody>
</table>

<h2>感想</h2>

<p>うーん。かたちだけ訳してはみたけど、正直説明がなんのこっちゃであまり意味ないな…。</p>

<p>ページを作る過程で、Markdownで表を作ったりするリサーチをしたりして勉強にはなったけれど（結局めんどくさかったのでHTMLでタグ付けすることに。そしてそれでもまだ表がきたない）、肝心のGASでモーダルウィンドウでのフォームを表示するという目標にはあまり近づいてない。</p>

<p>まあ、地道にまた勉強しますか。</p>
