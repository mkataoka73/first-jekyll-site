---
layout: post
title: 新規会員の情報を入力したら、請求書の情報が自動入力されるスクリプトを書いたよ
published_at: 2021-01-25
author: me
tags: GAS
---

こんにちは。ちぇんです。

学習塾で働きながら、プログラミングを勉強しています。Google Apps Script、略してGASという言語をいじっています。GASを使って学習塾業務の自動化に取り組んでいます。

## これを書いたときの動機や思いあれこれ
新規入会があると、いつもおおよそ次のような手順で作業が必要になります。

1. 塾内で使う生徒やご家庭の基本情報を入力（塾内管理 with Google Drive）
2. 口座振替申込のための手続き（外部サービスに委託）

要するに請求のために一連の手続きが必要ということですね。入会があるときは、だいたいいつも、面談→入会→初回授業という流れになるのですが、なんていうんでしょうか… 「入会」というイベントを、もっとわかりやすくしたいです。入会と、それに伴う情報収集/入力が、完全には同期されていないという感じ。

理想的には、入会時にGoogle Formを親御さん、あるいは生徒さんに書いてもらって、スプレッドシートに保存されるようになっていればいいのですが、まだまだそこまで手が回っていません。フォーム作るのなんて決して難しいことではないはずなのですが、入力の端末はどうするんだとか、どの項目を必須にするかとか、いろいろ自動化できない（＝標準化できない）問題があるんですね…。でも、一部の情報でもお客さんに入力してもらったら、きっと楽ですね。

## どんなプログラムなのか

えっと、今回は…

①請求用の会員IDを自動で割り当てて、シートに記入して、  
②自動引き落としに必要な書類を送るのを忘れないようにリマインダーを設定する

というコードを書きました。書きました、といっているんですが、まだ②については書いていません。そういうコードを書きたいです。

最大の難点(?)としては、「入会した」というイベントが、プログラムで再現できなかったということです。まあ、当たり前のはなしなのですが、「入会する」という出来事は現実の中で起きているのであって、PCやネットの中で起きていません。いや、とはいえ、「PCやネット」は「現実」の中にあるので、その現実のなかにうまくそれらを組み込むことができれば、「入会」をプログラム化可能なのかもしれないですが…。だし、自動化進めようぜ、ということなのであれば、どんどんそれを推進していくべきなはずですね。まあ、何を自動化するべきなのか、ということで、この問題は保留。

レイアウトとしてそれっぽいものができたので、これで公開してみようかな。


```js
const SS = SpreadsheetApp.getActiveSpreadsheet();
const SH_ALL_MEMBERS   = SS.getSheetByName('ALL_MEMBERS');
const SH_BILL_NUMBERS  = SS.getSheetByName('BILL_NUMBERS');

/**
 * シートが編集されたとき、値の入力が行われていたら、main関数を発火する
 */
function onEdit(e) {
  if(isInput_(e) && isTargetCell_(e.range)) {
    main();
  }
}

/**
 * 全会員の名簿をウォッチし、現会員が追加されたら、次のことを行う。
 * - 請求番号シートに名前を入力
 * - 前の人の会員番号に1を足して、会員番号を入力
 * - 送付予定日を記入
 * - 送るのを忘れないよう、カレンダーにリマインダーを追加
 */
function main() {

  const student = getLastStudent_();

  // 生徒の名前と入会日が入力されていれば、請求番号を自動入力
  if(isEnrolled_(student)) {
    setGmoMemberInfo_();

    // TODO: 振替申込書送付予定日を自動入力
    // setPaperDueDate_();
    // TODO: カレンダーにリマインダーを追加
    // setPaperDueReminder_();
  }
}

/**
 * 編集されたのが「全会員のA列またはE列」であるか判定
 * @return {boolean}
 */
function isTargetCell_(range) {
  return isAllMembersSheet_(range) && isNameCol_(range) || isEnrollDateCol_(range);
}

/**
 * 編集されたのが「全会員」シートであるか判定
 * @param  {object} range 編集されたRange
 * @return {boolean}
 */
function isAllMembersSheet_(range) {

  const sheetName = range.getSheet().getSheetName();

  return sheetName === 'ALL_MEMBERS';
}

/**
 * 編集されたのが「生徒氏名」カラムであるか判定
 * @param  {object} range 編集されたRange
 * @return {boolean}
 */
function isNameCol_(range) {

  const editedCol = range.getColumn();
  const nameCol   = 1;

  return editedCol === nameCol;
}

/**
 * 編集されたのが「入会日」カラムであるか判定
 * @param  {object} range 編集されたRange
 * @return {boolean}
 */
function isEnrollDateCol_(range) {

  const editedCol       = range.getColumn();
  const enrolledDateCol = 5;

  return editedCol === enrolledDateCol;
}

/**
 * 最終行の会員の、名前と入会日が入力されているかを判定
 * @param {object[]} student 最終行に入力されている生徒
 * @return {boolean}
 */
function isEnrolled_(student) {
  return student[0] && student[4];
}

/**
 * 編集時、データの入力であるかを判定
 * @param  {object} e 編集イベントオブジェクト
 * @return {boolean}
 */
function isInput_(e) {
  return e.value !== undefined;
}

/**
 * 請求番号シートに情報を入力
 */
function setGmoMemberInfo_() {

  const data = [getStudentName_(), getNewGmoId_(), '未'];

  // A列(生徒氏名)とE列(入会日)が入力されたら、請求番号シートを自動入力
  SH_BILL_NUMBERS.appendRow(data);
  setNumberFormat_();
}

/**
 * 請求番号シートの最終行、会員番号セルのフォーマットを "00000" に設定
 */
function setNumberFormat_() {

  const sheet   = SH_BILL_NUMBERS;
  const lastRow = sheet.getLastRow();

  sheet.getRange(lastRow, 2).setNumberFormat("00000");
}

/**
 * 現時点の最終GMO会員Noを取得
 * @return {number} ;
 */
function getCurrentLastId_() {

  const values    = SH_BILL_NUMBERS.getDataRange().getValues();
  const strLastId = values.pop()[1].toString();

  return parseInt(strLastId);
}

/**
 * 新しいGMO会員Noを返す
 * @return {string} 新しいID（5桁
 */
function getNewGmoId_() {

  const newId = (getCurrentLastId_() + 1).toString();

  return '00' + newId;
}

/**
 * 全会員から全ての生徒を取得
 * @return {object[][]} 全生徒の2次元配列
 */
function getStudents_() {

  // ヘッダーと最後の二行（受講料合計とテストユーザー）を除去
  return SH_ALL_MEMBERS.getDataRange().getValues().slice(1, -2);
}

/**
 * 全会員シートの最後の生徒を返す
 * @return {object[]}
 */
function getLastStudent_() {

  const students = getStudents_();
  const stLength = students.length;

  return students[stLength - 1];
}

/**
 * 生徒氏名を取得
 * @return {string} 生徒氏名
 */
function getStudentName_() {

  const lastStudent = getLastStudent_();
  const name        = 0; // A列

  return lastStudent[name].toString();
}
```
