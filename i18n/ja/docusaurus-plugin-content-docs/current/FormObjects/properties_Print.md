---
id: propertiesPrint
title: 印刷
---

## 印刷時可変

このプロパティは、レコードの中身に応じてサイズが変化しうるオブジェクトの印刷モードを管理します。 これらのオブジェクト固定長フレームまたは可変長フレームでの印刷を設定することができます。 固定長フレームオブジェクトは、フォーム上でオブジェクト作成するように、オブジェクトのサイズの制限内で印刷をします。 可変長フレームオブジェクトはオブジェクトの中身をすべて印刷するために、印刷時に展開します。 可変サイズとして印刷されるオブジェクト幅 (オブジェクトプロパティによって定義) はこのオプションによって影響はされないという点に注意してください。オブジェクトの中身に応じて、高さのみが変化します。

フォーム内において複数の可変長フレームを隣同士に配置することはできません。 非可変長フレームオブジェクトであれば、可変サイズで印刷されるオブジェクトのどちら側でも配置することができます。ただし、可変長フレームオブジェクトが最低でも横のオブジェクトより一行分長く、すべてのオブジェクトが上揃えで配置されていなければなりません。 この条件が遵守されない場合、可変長フレームオブジェクトの水平方向の部分ごとに、ほかのフィールドのコンテンツが繰り返されます。

> The [`Print object`](../commands-legacy/print-object.md) and [`Print form`](../commands/print-form.md) commands do not support this property.

印刷オプションは次の通りです:

- **可変** オプション (**印刷時可変** 選択時): すべてのサブレコードが印刷されるよう、4D はフォームオブジェクトエリアを拡大あるいは縮小します。

- **固定 (切り捨て)** オプション (**印刷時可変** 非選択時): オブジェクトエリアに表示されている内容のみを 4D は印刷します。 フォームが印刷されるのは一度のみで、印刷されなかった内容は無視されます。

- **固定 (複数レコード)** (サブフォームのみ): サブフォームの初期サイズを維持しますが、4D はすべてのレコードが印刷されるまで複数回にわたってフォームを印刷します。

> This property can be set by programming using the [`OBJECT SET PRINT VARIABLE FRAME`](../commands-legacy/object-set-print-variable-frame.md) command.

#### JSON 文法

|     名称     | データタイプ | とりうる値                                                              |
| :--------: | :----: | ------------------------------------------------------------------ |
| printFrame | string | "fixed", "variable", (サブフォームのみ) "fixedMultiple" |

#### 対象オブジェクト

[入力](input_overview.md) - [サブフォーム](subform_overview.md) (リストサブフォームのみ) - [4D Write Pro エリア](writeProArea_overview.md)

#### コマンド

[`OBJECT GET PRINT VARIABLE FRAME`](../commands-legacy/object-get-print-variable-frame.md) - [`OBJECT SET PRINT VARIABLE FRAME`](../commands-legacy/object-set-print-variable-frame.md)
