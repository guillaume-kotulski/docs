---
id: propertiesHierarchy
title: 階層
---

## 階層リストボックス

`配列型リストボックス`

このプロパティを使用してリストボックスの階層表示を設定します。 JSON フォームにおいては、この機能は [*dataSource* プロパティの値が配列名のコレクションであるとき](properties_Object.md#配列リストボックス) に有効化され階層化します。

*階層リストボックス* プロパティが選択されると、追加プロパティである **Variable 1...10** が利用可能になります。これらには階層の各レベルとして使用するデータソース配列を指定します。これが *dataSource* の値である配列名のコレクションとなります。 入力欄に値が入力されると、新しい入力欄が追加されます。 10個までの変数を指定できます。 これらの変数は先頭列に表示される階層のレベルを設定します。

[階層リストボックス](listbox_overview.md#階層リストボックス) 参照

#### JSON 文法

| 名称         | データタイプ     | とりうる値             |
| ---------- | ---------- | ----------------- |
| datasource | 文字列のコレクション | 階層を定義する配列名のコレクション |

#### 対象オブジェクト

[リストボックス](listbox_overview.md)

#### コマンド

[LISTBOX GET HIERARCHY](../commands-legacy/listbox-get-hierarchy.md) - [LISTBOX SET HIERARCHY](../commands-legacy/listbox-set-headers-height.md)


