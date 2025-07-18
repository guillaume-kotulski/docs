---
id: propertiesRangeOfValues
title: 値の範囲
---

## デフォルト値

入力オブジェクトにデフォルト値を割り当てることができます。 このプロパティは、入力オブジェクトに設定されている [変数あるいは式](properties_Object.md#変数あるいは式) がフィールドであるときに便利です。新規レコードが作成され、初めて表示されるときにデフォルト値が代入されます。 エリアが [入力不可](properties_Entry.md#入力可) に設定されていなければ、デフォルト値を書き換えることができます。

デフォルト値を指定できるのは、[式の型](properties_Object.md#式の型式タイプ) が次のいずれかの場合です:

- テキスト/文字列
- 数値/整数
- date
- time
- boolean

日付、時刻、シーケンス番号については、4D が提供する記号を使用することができます。 日付と時刻はシステムから取得されます。 シーケンス番号は 4D が自動で生成します。 自動で使用できるデフォルト値の記号は以下の通りです:

| スタンプ | 意味      |
| ---- | ------- |
| #D   | 本日の日付   |
| #H   | 現在の時刻   |
| #N   | シーケンス番号 |

カレントデータファイルの特定のテーブルにおいて、レコード毎のユニーク番号を生成するためにシーケンス番号を使用することができます。 シーケンス番号は倍長整数型で新規レコード毎に生成されます。 番号は 1 から始まり、1ずつ増加します。 シーケンス番号が割り当てられたレコードがテーブルから削除されても、その番号は再利用されません。 シーケンス番号は各テーブルが保有する内部カウンターが管理します。 For more information, refer to the [Autoincrement](https://doc.4d.com/4Dv20/4D/20.2/Field-properties.300-6750280.en.html#976029) paragraph.

> このプロパティと、リストボックス列に固定値を表示させるための
> "[デフォルト値](properties_DataSource.md#デフォルト値)" を混同しないようにしてください。

#### JSON 文法

| 名称           | データタイプ                              | とりうる値                                           |
| ------------ | ----------------------------------- | ----------------------------------------------- |
| defaultValue | string, number, date, time, boolean | 任意の値。 次の記号を含む: "#D", "#H", "#N" |

#### 対象オブジェクト

[入力](input_overview.md)

---

## 除外リスト

除外リストを使用すると、当該リストの項目は入力できなくなります。 ユーザーがこのリストに含まれる値を入力したとき、その入力は自動的に却下され、エラーメッセージが表示されます。

> 階層リストを指定した場合は、第一レベルの項目のみが考慮されます。

#### JSON 文法

| 名称           | データタイプ | とりうる値     |
| ------------ | ------ | --------- |
| excludedList | list   | 除外する値のリスト |

#### 対象オブジェクト

[コンボボックス](comboBox_overview.md) - [リストボックス列](listbox_overview.md#リストボックス列) - [入力](input_overview.md)

#### コマンド

[OBJECT Get list name](../commands-legacy/object-get-list-name.md) - [OBJECT Get list reference](../commands-legacy/object-get-list-reference.md) - [OBJECT SET LIST BY NAME](../commands-legacy/object-set-list-by-name.md) - [OBJECT SET LIST BY REFERENCE](../commands-legacy/object-set-list-by-reference.md)

---

## 指定リスト

有効な入力値のリストを指定するために使用します。 たとえば、役職名のリストを指定リストとして設定できます。こうすると、事前に作成されたリスト中の役職名だけ有効な値となります。

指定リストを指定しても、フィールドが選択されたときにリストは自動で表示されません。 指定リストを表示したい場合は、"データソース"テーマの [選択リスト](properties_DataSource.md#選択リスト) プロパティに同じリストを指定します。
ただし、[選択リスト](properties_DataSource.md#選択リスト) プロパティだけが指定されているときとは異なり、指定リストも設定されている場合にはキーボードによる入力はできません。ポップアップメニューでのリスト項目の選択だけが可能です。 [選択リスト](properties_DataSource.md#選択リスト) と指定リストにそれぞれ別のリストが指定されている場合、指定リストが優先されます。

> 階層リストを指定した場合は、第一レベルの項目のみが考慮されます。

#### JSON 文法

| 名称           | データタイプ | とりうる値      |
| ------------ | ------ | ---------- |
| requiredList | list   | 有効な入力値のリスト |

#### 対象オブジェクト

[コンボボックス](comboBox_overview.md) - [リストボックス列](listbox_overview.md#リストボックス列) - [入力](input_overview.md)

#### コマンド

[OBJECT Get list name](../commands-legacy/object-get-list-name.md) - [OBJECT Get list reference](../commands-legacy/object-get-list-reference.md) - [OBJECT SET LIST BY NAME](../commands-legacy/object-set-list-by-name.md) - [OBJECT SET LIST BY REFERENCE](../commands-legacy/object-set-list-by-reference.md)
