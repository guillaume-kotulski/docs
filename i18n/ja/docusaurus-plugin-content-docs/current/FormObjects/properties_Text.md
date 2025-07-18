---
id: propertiesText
title: Text
---

---

## ピッカーの使用を許可

When this property is enabled, the [OPEN FONT PICKER](../commands-legacy/open-font-picker.md) and [OPEN COLOR PICKER](../commands-legacy/open-color-picker.md) commands can be called to display the system font and color picker windows. これらのピッカーウィンドウを使用して、ユーザーはフォームオブジェクトのフォントやカラーをクリックによって変更できます。 このプロパティが無効になっていると (デフォルト)、ピッカーを開くコマンドは使用できません。

#### JSON 文法

| プロパティ                | データタイプ  | とりうる値                                  |
| -------------------- | ------- | -------------------------------------- |
| allowFontColorPicker | boolean | false (デフォルト), true |

#### 対象オブジェクト

[入力](input_overview.md)

---

## 太字

選択テキストの線を太くし、濃く見えるようにします。

You can set this property using the [**OBJECT SET FONT STYLE**](../commands-legacy/object-set-font-style.md) command.

> これは通常のテキストです。<br/>
> **これは太字のテキストです。**

#### JSON 文法

| プロパティ      | データタイプ | とりうる値            |
| ---------- | ------ | ---------------- |
| fontWeight | text   | "normal", "bold" |

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### コマンド

[OBJECT Get font style](../commands-legacy/object-get-font-style.md) - [OBJECT SET FONT STYLE](../commands-legacy/object-set-font-style.md)

---

## イタリック

選択テキストの線を右斜めに傾けます。

You can also set this property via the [**OBJECT SET FONT STYLE**](../commands-legacy/object-set-font-style.md) command.

> これは通常のテキストです。<br/>
> *これはイタリックのテキストです。*

#### JSON 文法

| 名称        | データタイプ | とりうる値              |
| --------- | ------ | ------------------ |
| fontStyle | string | "normal", "italic" |

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### コマンド

[OBJECT Get font style](../commands-legacy/object-get-font-style.md) - [OBJECT SET FONT STYLE](../commands-legacy/object-set-font-style.md)

---

## 下線

選択テキストの下に線を引きます。

#### JSON 文法

| 名称             | データタイプ | とりうる値                 |
| -------------- | ------ | --------------------- |
| textDecoration | string | "normal", "underline" |

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### コマンド

[OBJECT Get font style](../commands-legacy/object-get-font-style.md) - [OBJECT SET FONT STYLE](../commands-legacy/object-set-font-style.md)

---

## フォント

このプロパティは、オブジェクトで使用される **フォントテーマ** または **フォントファミリー** を指定します。

> **フォントテーマ** と **フォントファミリー** プロパティは、どちらか一方しか指定できません。 フォントテーマは、サイズを含めたフォント属性を定めます。 フォントファミリーの場合は、フォント名・フォントサイズ・フォントカラーをそれぞれ定義することができます。

### フォントテーマ

フォントテーマプロパティには、自動スタイルの名前を指定します。 自動スタイルは、オブジェクトに使われるフォントファミリー・フォントサイズ・フォントカラーをシステムパラメーターに応じて動的に定めます。 これらのパラメーターは次に依存します:

- プラットフォーム
- システム言語
- フォームオブジェクトのタイプ

フォントテーマを使うことで、システムの現インターフェース標準に沿うようにタイトルが表示されることが保証されます。 ただし、マシンごとにサイズが変わるかもしれません。

3つのフォントテーマが提供されています:

- **normal**: フォームエディター内で作成された新規オブジェクトにデフォルトで適用される自動スタイルです。
- **main** および **additional** フォントテーマは [テキストエリア](text.md) と [入力](input_overview.md) オブジェクトでのみサポートされています。 これらのテーマは、おもにダイアログボックスのデザインを目的に提供されています。 インターフェースウィンドウにおいて main フォントテーマは本文用、additional テーマは詳細情報を追記するためのものです。 下に macOS および Windows にてこれらのフォントテーマを使ったダイアログボックスの例を示します:

![](../assets/en/FormObjects/FontThemes.png)

> フォントテーマはフォントだけでなく、サイズやカラーも定めます。 一部のカスタムスタイルプロパティ (太字、イタリック、下線) は動作に影響なく適用することができます。

#### JSON 文法

| 名称        | データタイプ | とりうる値                          |
| --------- | ------ | ------------------------------ |
| fontTheme | string | "normal", "main", "additional" |

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### コマンド

[OBJECT Get style sheet](../commands-legacy/object-get-style-sheet) - [OBJECT SET STYLE SHEET](../commands-legacy/object-set-style-sheet)

### フォントファミリー

次の 2種類のフォントファミリーが存在します:

- *フォントファミリー:* "times", "courier", "arial" などのフォントファミリーの名称。
- *総称ファミリー:* "serif", "sans-serif", "cursive", "fantasy", "monospace" などの汎用ファミリーの名称。

You can set this using the [`OBJECT SET FONT`](../commands-legacy/object-set-font.md) command.

#### JSON 文法

| 名称         | データタイプ | とりうる値          |
| ---------- | ------ | -------------- |
| fontFamily | string | CSS フォントファミリー名 |

> 4D では [Webセーフ](https://www.w3schools.com/cssref/css_websafe_fonts.asp) フォントだけを使うことを推奨しています。

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### コマンド

[OBJECT Get font](../commands-legacy/object-get-font.md) - [OBJECT SET FONT](../commands-legacy/object-set-font.md)

## フォントサイズ

文字の大きさをポイントで指定します。

#### JSON 文法

| 名称       | データタイプ  | とりうる値                                                                             |
| -------- | ------- | --------------------------------------------------------------------------------- |
| fontSize | integer | フォントサイズ (ポイント単位) 最小値: 0 最小値: 0 |

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### コマンド

[OBJECT Get font size](../commands-legacy/object-get-font-size.md) - [OBJECT SET FONT SIZE](../commands-legacy/object-set-font-size.md)

---

## フォントカラー

文字の色を指定します。

> This property also sets the color of object's border (if any) when "plain" or "dotted" style is used.

カラーは次の方法で指定できます:

- カラーネーム - 例: "red"
- 16進数値 - 例: "#ff0000"
- RGB値 - 例: "rgb(255,0,0)"

You can also set this property using the [**OBJECT SET RGB COLORS**](../commands-legacy/object-set-rgb-colors.md) command.

#### JSON 文法

| 名称     | データタイプ | とりうる値                                |
| ------ | ------ | ------------------------------------ |
| stroke | string | 任意の css値; "transparent"; "automatic" |

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Progress Indicators](progressIndicator.md) - [Ruler](ruler.md) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### コマンド

[OBJECT GET RBG COLOR](../commands-legacy/object-get-rgb-color.md) - [OBJECT SGET RBG COLOR](../commands-legacy/object-set-rgb-color.md)

---

## フォントカラー式

`セレクションおよびコレクション/エンティティセレクション型のリストボックス`

リストボックスの各行にカスタマイズしたフォントカラーを適用するために使用します。 RGBカラーを使用しなければなりません。 For more information about this, refer to the description of the [`OBJECT SET RGB COLORS`](../commands-legacy/object-set-rgb-colors.md) command.

式または変数 (配列を除く) を入力します。 表示される行ごとに式や変数は評価されます。 You can use the constants described in the [`OBJECT SET RGB COLORS`](../commands-legacy/object-set-rgb-colors.md) command.

You can also set this property using the [`LISTBOX SET PROPERTY`](../commands/listbox-set-property.md) command with `lk font color expression` constant.

> このプロパティは [メタ情報式](properties_Text.md#メタ情報式) を使用しても設定することができます。

以下の例は変数名を使用しています。**フォントカラー式** に *CompanyColor* を入力し、フォームメソッドに以下のコードを書きます:

```4d
CompanyColor:=Choose([Companies]ID;Background color;Light shadow color;   
Foreground color;Dark shadow color)
```

#### JSON 文法

| 名称              | データタイプ | とりうる値    |
| --------------- | ------ | -------- |
| rowStrokeSource | string | フォントカラー式 |

#### 対象オブジェクト

[リストボックス](listbox_overview.md)

#### コマンド

[LISTBOX Get property](../commands/listbox-get-property.md) - [LISTBOX SET PROPERTY](../commands/listbox-set-property.md)

---

## スタイル式

`セレクションおよびコレクション/エンティティセレクション型のリストボックス`

リストボックスの各行にカスタマイズされた文字スタイルを適用するために使用します。

式または変数 (配列を除く) を入力します。 式や変数は、表示行ごと (リストボックスのプロパティの場合) または表示セルごと (リストボックス列のプロパティの場合) に評価されます。 You can use the constants listed in the [`LISTBOX SET ROW FONT STYLE`](../commands-legacy/listbox-set-row-font-style.md) command.

例:

```4d
Choose([Companies]ID;Bold;Plain;Italic;Underline)
```

You can also set this property using the [`LISTBOX SET PROPERTY`](../commands/listbox-set-property.md) command with `lk font style expression` constant.

> このプロパティは [メタ情報式](properties_Text.md#メタ情報式) を使用しても設定することができます。

#### JSON 文法

| 名称             | データタイプ | とりうる値                   |
| -------------- | ------ | ----------------------- |
| rowStyleSource | string | 表示される行/セルごとに評価されるスタイル式。 |

#### 対象オブジェクト

[リストボックス](listbox_overview.md) - [リストボックス列](listbox_overview.md#リストボックス列)

#### コマンド

[LISTBOX Get property](../commands/listbox-get-property.md) - [LISTBOX SET PROPERTY](../commands/listbox-set-property.md)

---

## 横揃え

エリア中のテキストの横位置を指定します。

#### JSON 文法

| 名称        | データタイプ | とりうる値                                             |
| --------- | ------ | ------------------------------------------------- |
| textAlign | string | "right", "center", "left", "automatic", "justify" |

:::note

- "automatic" は、[チェックボックス](checkbox_overview.md) および [ラジオボタン](radio_overview.md) ではサポートされていません。
- "justify" は、[入力](input_overview.md) と [テキストエリア](text.md) でのみサポートされています。

:::

#### 対象オブジェクト

[Button](button_overview.md) - [Check Box](checkbox_overview.md) (all styles except Regular and Flat) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Header](listbox_overview.md#list-box-headers) - [List Box Footer](listbox_overview.md#list-box-footers) - [Radio Button](radio_overview.md) (all styles except Regular and Flat) - [Text Area](text.md)

#### コマンド

[OBJECT Get horizontal alignment](../commands-legacy/object-get-horizontal-alignment.md) - [OBJECT SET HORIZONTAL ALIGNMENT](../commands-legacy/object-set-horizontal-alignment.md)

---

## 縦揃え

エリア中のテキストの縦位置を指定します。

**デフォルト** オプション (JSON値: `automatic`) の場合は、各列のデータ型に基づき整列方向が決定されます:

- ピクチャーを除き、すべて `下` です。
- ピクチャーは `上` です。

This property can also be handled by the [`OBJECT Get vertical alignment`](../commands-legacy/object-get-vertical-alignment.md) and [`OBJECT SET VERTICAL ALIGNMENT`](../commands-legacy/object-set-vertical-alignment.md) commands.

#### JSON 文法

| 名称            | データタイプ | とりうる値                                  |
| ------------- | ------ | -------------------------------------- |
| verticalAlign | string | "automatic", "top", "middle", "bottom" |

#### 対象オブジェクト

[リストボックス](listbox_overview.md)* [リストボックス列](listbox_overview.md#リストボックス列)
* [リストボックスフッター](listbox_overview.md#リストボックスフッター)
* [リストボックスヘッダー](listbox_overview.md#リストボックスヘッダー)

#### コマンド

## [`OBJECT Get vertical alignment`](../commands-legacy/object-get-vertical-alignment.md) - [`OBJECT SET VERTICAL ALIGNMENT`](../commands-legacy/object-set-vertical-alignment.md)

## メタ情報式

`コレクションまたはエンティティセレクション型リストボックス`

表示される行ごとに評価される式あるいは変数を指定します。 行テキスト属性全体を定義することができます。 **オブジェクト変数**、あるいは **オブジェクトを返す式** を指定する必要があります。 以下のプロパティがサポートされています:

| プロパティ名         | 型       | 説明                                                                                                                                                                                                                                                                          |
| -------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| stroke         | string  | フォントカラー。 任意の CSSカラー (例: "#FF00FF"), "automatic", "transparent"                                                                                                                                                                           |
| fill           | string  | 背景色。 任意の CSSカラー (例: "#F00FFF"), "automatic", "transparent"                                                                                                                                                                               |
| fontStyle      | string  | "normal","italic"                                                                                                                                                                                                                                                           |
| fontWeight     | string  | "normal","bold"                                                                                                                                                                                                                                                             |
| textDecoration | string  | "normal","underline"                                                                                                                                                                                                                                                        |
| unselectable   | boolean | 対応する行が選択不可 (つまりハイライトすることができない状態) であることを指定します。 このオプションが有効化されている場合、入力可能エリアは入力可能ではなくなります (ただし "シングルクリック編集" オプションが有効化されている場合を除く)。 チェックボックスやリストといったコントロール類は引き続き稼働します。 この設定はリストボックスの選択モードが "なし" の場合には無視されます。 デフォルト値: false。 |
| disabled       | boolean | 対応する行を無効化します。 このオプションが有効化されると、入力可能エリアは入力可能ではなくなります。 テキストや、(チェックボックス、リストなどの)  コントロール類は暗くなっているかグレーアウトされます。 デフォルト値: false。                                                                                                                  |

特別な "cell" プロパティを使用すると、特定の列にプロパティをまとめて適用することができます:

| プロパティ名 |              |                | 型      | 説明                                                                                                                                                                                                          |
| ------ | ------------ | -------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cell   |              |                | object | 特定の列に適用するプロパティ                                                                                                                                                                                              |
|        | *columnName* |                | object | *columnName* はリストボックス列のオブジェクト名です。                                                                                                                                                                           |
|        |              | *propertyName* | string | "stroke", "fill", "fontStyle", "fontWeight", または "textDecoration" プロパティ (前述参照)。 **注**: "unselectable" および "disabled" プロパティは行レベルでのみ定義可能です。 "セル" オブジェクトに指定した場合、これらは無視されます。 |

> Style settings made with this property are ignored if other style settings are already defined through expressions (*i.e.*, [Style Expression](#style-expression), [Font Color Expression](#font-color-expression), [Background Color Expression](./properties_BackgroundAndBorder.md#background-color-expression)).

**例題**

*Color* プロジェクトメソッドに以下のコードを書きます:

```4d
// Color メソッド
// 特定の行に対してフォントカラーを、そしてカラム Col2 および Col3 に対して背景色を設定します:
Form.meta:=New object
If(This.ID>5) // ID はコレクションオブジェクト/エンティティの属性です
  Form.meta.stroke:="purple"
  Form.meta.cell:=New object("Col2";New object("fill";"black");\
    "Col3";New object("fill";"red"))
Else
  Form.meta.stroke:="orange"
End if
```

**ベストプラクティス:** 最適化のため、このような場合にはフォームメソッド内で `meta.cell` オブジェクトを作成しておくことが推奨されます。

```4d
  // フォームメソッド
 Case of
    :(Form event code=On Load)
       Form.colStyle:=New object("Col2";New object("fill";"black");\
        "Col3";New object("fill";"red"))  
 // 他のスタイルセットも定義できます  
       Form.colStyle2:=New object("Col2";New object("fill";"green");\
        "Col3";New object("fontWeight";"bold"))  
 End case
```

*Color* メソッドには、以下のコードを書きます:

```4d
  // Color メソッド
 ...
 If(This.ID>5)
    Form.meta.stroke:="purple"
    Form.meta.cell:=Form.colStyle // より良いパフォーマンスのため、同じオブジェクトを再利用します
 Else
    Form.meta.stroke:="orange"
    Form.meta.cell:=Form.colStyle2
 End if
```

#### JSON 文法

| 名称         | データタイプ | とりうる値                     |
| ---------- | ------ | ------------------------- |
| metaSource | string | 表示される行/セルごとに評価されるオブジェクト式。 |

#### 対象オブジェクト

[リストボックス](listbox_overview.md)

#### コマンド

[LISTBOX Get property](../commands/listbox-get-property.md) - [LISTBOX SET PROPERTY](../commands/listbox-set-property.md)

---

## マルチスタイル

This property enables the possibility of using [specific styles](https://doc.4d.com/4Dv20/4D/20.6/Supported-tags.300-7488021.en.html) in the selected area. プロパティリストでこのオプションがチェックされていると、4D はエリア中の `<SPAN>` HTMLタグをスタイル属性として解釈します。

デフォルトでは、このオプションは有効化されていません。

#### JSON 文法

| 名称         | データタイプ  | とりうる値       |
| ---------- | ------- | ----------- |
| styledText | boolean | true, false |

#### 対象オブジェクト

[入力](input_overview.md) - [リストボックス列](listbox_overview.md#リストボックス列)

#### コマンド

[LISTBOX Get property](../commands/listbox-get-property.md) - [LISTBOX SET PROPERTY](../commands/listbox-set-property.md) - [OBJECT Is styled text](../commands-legacy/object-is-styled-text.md) -

---

## 方向

テキストエリアの角度 (回転) を変更します。 テキストエリアは、90°単位で回転させることができます。 それぞれの回転角度を適用するとき、オブジェクトの左下の角は固定されたままで回転していきます:

| 戻り値                          | 戻り値                                            |
| ---------------------------- | ---------------------------------------------- |
| 0 (デフォルト) | ![](../assets/en/FormObjects/orientation1.png) |
| 90                           | ![](../assets/en/FormObjects/orientation2.png) |
| 180                          | ![](../assets/en/FormObjects/orientation3.png) |
| 270                          | ![](../assets/en/FormObjects/orientation4.png) |

[スタティックなテキストエリア](text.md) のほかに、[入力不可](properties_Entry.md#入力可) に設定された [入力オブジェクト](input_overview.md) も回転させることが出来ます。 入力オブジェクトの方向プロパティにて 0°以外のオプションを選んだ場合、 入力可プロパティは (選択されていた場合) 自動的に解除されます。 その際、このオブジェクトは入力順から自動的に除外されます。

#### JSON 文法

| 名称        | データタイプ | とりうる値           |
| --------- | ------ | --------------- |
| textAngle | number | 0, 90, 180, 270 |

#### 対象オブジェクト

[入力](input_overview.md) (入力不可) - [テキストエリア](text.md)

#### コマンド

[OBJECT Get text orientation](../commands-legacy/object-get-text-orientation.md) - [OBJECT SET TEXT ORIENTATION](../commands/object-set-text-orientation.md)

---

## 行フォントカラー配列

`配列型リストボックス`

リストボックスの各行/セルにカスタマイズしたフォントカラーを適用するために使用します。

倍長整数型の配列の名前を入力しなければなりません。 配列のそれぞれの要素はリストボックスの行 (あるいは列のセル) に対応します。つまりこの配列は、各列に関連づけられている配列と同じサイズでなければいけません。 You can use the constants described in the [`OBJECT SET RGB COLORS`](../commands-legacy/object-set-rgb-colors.md) command. もし上のレベルで定義されている背景色をそのままセルに継承したい場合には、対応する配列の要素に -255 を渡します。

#### JSON 文法

| 名称              | データタイプ | とりうる値      |
| --------------- | ------ | ---------- |
| rowStrokeSource | string | 倍長整数型配列の名前 |

#### 対象オブジェクト

[リストボックス](listbox_overview.md) - [リストボックス列](listbox_overview.md#リストボックス列)

#### コマンド

[`LISTBOX Get array`](../commands-legacy/listbox-get-array.md) - [`LISTBOX GET ARRAYS`](../commands-legacy/listbox-get-arrays.md) - [`LISTBOX SET ARRAY`](../commands-legacy/listbox-set-array.md)

---

## 行スタイル配列

`配列型リストボックス`

リストボックスの各行/セルにカスタマイズされた文字スタイルを適用するために使用します。

倍長整数型の配列の名前を入力しなければなりません。 配列のそれぞれの要素はリストボックスの行 (あるいは列のセル) に対応します。つまりこの配列は、各列に関連づけられている配列と同じサイズでなければいけません。 To fill the array (using a method), use the constants listed in the [`LISTBOX SET ROW FONT STYLE`](../commands-legacy/listbox-set-row-font-style.md) command. 定数同士を足し合わせてスタイルを組み合わせることもできます。 もし上のレベルで定義されているスタイルをそのままセルに継承したい場合には、対応する配列の要素に -255 を渡します。

#### JSON 文法

| 名称             | データタイプ | とりうる値      |
| -------------- | ------ | ---------- |
| rowStyleSource | string | 倍長整数型配列の名前 |

#### 対象オブジェクト

[リストボックス](listbox_overview.md) - [リストボックス列](listbox_overview.md#リストボックス列)

#### コマンド

[`LISTBOX Get array`](../commands-legacy/listbox-get-array.md) - [`LISTBOX GET ARRAYS`](../commands-legacy/listbox-get-arrays.md) - [`LISTBOX SET ARRAY`](../commands-legacy/listbox-set-array.md)

---

## スタイルタグを全て保存

このプロパティは [マルチスタイル](#マルチスタイル) 入力エリアの場合にのみ提供されます。
このオプションがチェックされている場合には、たとえ変更がおこなわれていなくても、エリアはテキストとともにスタイルタグを格納します。 この場合、タグはデフォルトスタイルが適用されます。 このオプションがチェックされていないと、変更されたスタイルタグのみが格納されます。

たとえば、以下のようにスタイルが変更されたテキストがあります:

![](../assets/en/FormObjects/tagStyle1.png)

このプロパティが無効な場合、エリアは更新されたスタイルのみを格納します。 つまり、格納される内容は以下のようになります:

```
What a <SPAN STYLE="font-size:13.5pt">beautiful</SPAN> day!
```

同プロパティが有効な場合には、エリアはすべてのフォーマット情報を格納します。 先頭の汎用タグはデフォルトスタイルを定義し、変更されたスタイルはネストされたタグに書き込まれます。 格納される内容は以下のようになります:

```
<SPAN STYLE="font-family:'Arial';font-size:9pt;text-align:left;font-weight:normal;font-style:normal;text-decoration:none;color:#000000;background-color:#FFFFFF">What a <SPAN STYLE="font-size:13.5pt">beautiful</SPAN> day!</SPAN>
```

#### JSON 文法

| 名称                | データタイプ  | とりうる値                                  |
| ----------------- | ------- | -------------------------------------- |
| storeDefaultStyle | boolean | true, false (デフォルト) |

#### 対象オブジェクト

[入力](input_overview.md)
