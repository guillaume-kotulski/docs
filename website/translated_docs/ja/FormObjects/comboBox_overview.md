---
id: comboBoxOverview
title: コンボボックス
---

## 概要

コンボボックスは [ドロップダウンリスト](dropdownList_Overview.md#概要) と似ていますが、キーボードから入力されたテキストを受けいれる点と、二つの追加オプションがついている点が異なります。

![](assets/en/FormObjects/combo_box.png)

コンボボックスの初期化方法は、ドロップダウンリストとまったく同じです 。 ユーザーがコンボボックスにテキストを入力すると、その値は配列の 0番目の要素に代入されます。 その他の点では、コンボボックスを入力エリアと同じように取り扱い、配列または選択リストを一連のデフォルト値として使用します。

入力エリアへの入力内容は、入力エリアオブジェクトと同様に `On Data Change` イベントを使用して管理します。 For more information, refer to the description of the [Form event code](https://doc.4d.com/4Dv17R5/4D/17-R5/Form-event.301-4127796.en.html) command in the *4D Language Reference* manual.

## コンボボックスのオプション

コンボボックスタイプのオブジェクトには、関連付けられた選択リストに関する 2つのオプションがあります。

- [自動挿入](properties_DataSource.md#自動挿入): このオプションがチェックされていると、オブジェクトに関連付けられた選択リストにない値をユーザーが入力した場合に、その値が自動的にメモリー内のリストに追加されます。
- [除外リスト](properties_RangeOfValues.md#除外リスト) (除外される値のリスト): 除外される値のリストを関連付けることができます。 ユーザーがこのリストに含まれる値を入力したとき、その入力は自動的に却下され、エラーメッセージが表示されます。

> [指定リスト](properties_RangeOfValues.md#指定リスト) はコンボボックスには割り当てることはできません。 ユーザーインターフェースにおいて、オブジェクト内にいくつかの指定された値を表示したいときには、[ポップアップメニュータイプ](dropdownList_Overview.md#概要) のオブジェクトを使用して下さい。

## プロパティ一覧

[Alpha Format](properties_Display.md#alpha-format) - [Bold](properties_Text.md#bold) - [Bottom](properties_CoordinatesAndSizing.md#bottom) - [Choice List](properties_DataSource.md#choice-list) - [Class](properties_Object.md#css-class) - [Date Format](properties_Display.md#date-format) - [Font](properties_Text.md#font) - [Font Color](properties_Text.md#font-color) - [Font Size](properties_Text.md#font-size) - [Height](properties_CoordinatesAndSizing.md#height) - [Help Tip](properties_Help.md#help-tip) - [Horizontal Sizing](properties_ResizingOptions.md#horizontal-sizing) - [Italic](properties_Text.md#italic) - [Left](properties_CoordinatesAndSizing.md#left) - [Object Name](properties_Object.md#object-name) - [Right](properties_CoordinatesAndSizing.md#right)) - [Time Format](properties_Display.md#time-format) - [Top](properties_CoordinatesAndSizing.md#top) - [Type](properties_Object.md#type) - [Underline](properties_Text.md#underline) - [Variable or Expression](properties_Object.md#variable-or-expression) - [Vertical Sizing](properties_ResizingOptions.md#vertical-sizing) - [Visibility](properties_Display.md#visibility) - [Width](properties_CoordinatesAndSizing.md#width)