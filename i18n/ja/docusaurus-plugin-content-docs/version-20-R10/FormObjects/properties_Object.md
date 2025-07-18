---
id: propertiesObject
title: オブジェクト
---

---

## 型

`必須設定です。`

このプロパティは [アクティブまたはスタティックなフォームオブジェクト](formObjects_overview.md) のタイプを指定します。

#### JSON 文法

| 名称   | データタイプ | とりうる値                                                                                                                                                                                                                                                                                                    |
| ---- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type | string | "button", "buttonGrid", "checkbox", "combo", "dropdown", "groupBox", "input", "line", "list", "listbox", "oval", "picture", "pictureButton", "picturePopup", "plugin", "progress", "radio", "rectangle", "ruler", "spinner", "splitter", "stepper", "subform", "tab", "text", "view", "webArea", "write" |

#### 対象オブジェクト

[4D View Pro エリア](viewProArea_overview.md) -
[4D Write Pro エリア](writeProArea_overview.md) -
[ボタン](button_overview.md) -
[ボタングリッド](buttonGrid_overview.md) -
[チェックボックス](checkbox_overview.md) -
[コンボボックス](comboBox_overview.md) -
[ドロップダウンリスト](dropdownList_Overview.md) -
[グループボックス](groupBox.md) -
[階層リスト](list_overview.md) -
[リストボックス](listbox_overview.md) -
[リストボックス列](listbox_overview.md#リストボックス列) -
[リストボックスフッター](listbox_overview.md#リストボックスフッター) -
[リストボックスヘッダー](listbox_overview.md#リストボックスヘッダー) -
[ピクチャーボタン](pictureButton_overview.md) -
[ピクチャーポップアップメニュー](picturePopupMenu_overview.md) -
[プラグインエリア](pluginArea_overview.md) -
[進捗インジケーター](progressIndicator.md) -
[ラジオボタン](radio_overview.md) -
[スピナー](spinner.md) -
[スプリッター](splitters.md) -
[スタティックピクチャー](staticPicture.md) -
[ステッパー](stepper.md) -
[サブフォーム](subform_overview.md) -
[タブコントロール](tabControl.md) -
[テキストエリア](text.md)

---

## オブジェクト名

各アクティブフォームオブジェクトにはオブジェクト名が関連付けられています。 各オブジェクト名はユニークでなければなりません。

> オブジェクト名のサイズ上限は 255バイトです。

4D ランゲージを使用する場合、オブジェクト名を使用してアクティブなフォームオブジェクトを参照することができます([オブジェクト(フォーム)コマンド](../category/object-forms) を参照して下さい)。

フォームオブジェクトの命名規則については [識別子](Concepts/identifiers.md) の章を参照してください。

#### JSON 文法

| 名称   | データタイプ | とりうる値                           |
| ---- | ------ | ------------------------------- |
| name | string | 既存オブジェクトによって使用されていない、命名規則に沿った名称 |

#### 対象オブジェクト

[4D View Pro エリア](viewProArea_overview.md) -
[4D Write Pro エリア](writeProArea_overview.md) -
[ボタン](button_overview.md) -
[ボタングリッド](buttonGrid_overview.md) -
[チェックボックス](checkbox_overview.md) -
[コンボボックス](comboBox_overview.md) -
[ドロップダウンリスト](dropdownList_Overview.md) -
[グループボックス](groupBox.md) -
[階層リスト](list_overview.md) -
[リストボックス](listbox_overview.md) -
[リストボックス列](listbox_overview.md#リストボックス列) -
[リストボックスフッター](listbox_overview.md#リストボックスフッター) -
[リストボックスヘッダー](listbox_overview.md#リストボックスヘッダー) -
[ピクチャーボタン](pictureButton_overview.md) -
[ピクチャーポップアップメニュー](picturePopupMenu_overview.md) -
[プラグインエリア](pluginArea_overview.md) -
[進捗インジケーター](progressIndicator.md) -
[スピナー](spinner.md) -
[スプリッター](splitters.md) -
[スタティックピクチャー](staticPicture.md) -
[ステッパー](stepper.md) -
[ラジオボタン](radio_overview.md) -
[サブフォーム](subform_overview.md) -
[タブコントロール](tabControl.md) -
[テキストエリア](text.md) -
[Web エリア](webArea_overview.md)

---

## 値を記憶

このオプションは、フォームの [配置を記憶](FormEditor/properties_FormProperties.md#配置を記憶) プロパティがチェックされている場合に利用可能です。

この機能は、フォームの全体的な配置に関係するオブジェクトに対してのみサポートされています。 たとえばチェックボックスは、ウィンドウ内の追加エリアを表示/非表示するのに使用することができるため、このオプションが存在します。

「値」を保存できるオブジェクトは以下のとおりです:

| Object                                 | 保存される値                                                          |
| -------------------------------------- | --------------------------------------------------------------- |
| [チェックボックス](checkbox_overview.md)       | 関連付けられた変数の値 (0, 1, 2)                        |
| [ドロップダウンリスト](dropdownList_Overview.md) | 選択されている項目の番号                                                    |
| [ラジオボタン](radio_overview.md)            | 関連付けられた変数の値 (1、0、ボタンにおいては true/false など型による) |
| [タブコントロール](tabControl.md)              | 選択されているタブの番号                                                    |

#### JSON 文法

| 名称            | データタイプ  | とりうる値       |
| ------------- | ------- | ----------- |
| memorizeValue | boolean | true, false |

#### 対象オブジェクト

[チェックボックス](checkbox_overview.md)\* [ドロップダウンリスト](dropdownList_Overview.md)

---

## 変数あるいは式

> セレクションおよびコレクション型のリストボックス列に関しては **[式](properties_DataSource.md#式)** の章も参照ください。

このプロパティは、データのソースを指定します。 各アクティブフォームオブジェクトにはオブジェクト名と変数名が関連付けられています。 変数名とオブジェクト名は違っていてもかまいません。 同じフォーム内で複数のアクティブオブジェクトに同じ変数名を割り当てることができますが、[オブジェクト名](#オブジェクト名) はそれぞれユニークでなければなりません。

> 変数名の上限は 31バイトです。 命名規則については [識別子](Concepts/identifiers.md) の章を参照してください。

フォームオブジェクト変数を使って、オブジェクトを監視・コントロールすることができます。 たとえば、ボタンがクリックされると、その変数の値は 1 に設定されます。 それ以外の場合は 0 です。 進捗インジケーターに関連づけられた式は、現設定の取得・変更を可能にします。

代入可・代入不可の変数および式が使用でき、取得できるデータ型はテキスト、整数、数値、日付、時間、ピクチャー、ブール、そしてオブジェクトです。

#### JSON 文法

| 名称         | データタイプ                   | とりうる値                                                                                                                                                                                                                                                     |
| ---------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataSource | string、または sting のコレクション | <li>4D variable, field name, or any expression.</li><li>Empty string for [dynamic variables](#dynamic-variables).</li><li>String array (collection of array names) for a [hierarchical listbox](listbox_overview.md#hierarchical-list-boxes) column]</li> |

### 式

オブジェクトのデータソースとして、[式](Concepts/quick-tour.md#式) を使用することができます。 シンプルな式、オブジェクトプロパティ、フォーミュラ、4D関数、プロジェクトメソッド名、標準の `[Table]Field` シンタックスを使用したフィールド名を使用できます。 式はフォームが実行されたときに評価され、フォームイベント毎に再評価されます。 式には、[代入可および代入不可の式](Concepts/quick-tour.md#式) があることに注意が必要です。

> 入力された式が、変数名とメソッド名の両方で使用されている場合、4Dはメソッド名が指定されたものと判断します。

### ダイナミック変数

ボタン、入力オブジェクト、チェックボックス等のフォームオブジェクトに割り当てられる変数を、 必要に応じて動的に、4D に作成させることができます。 これをおこなうには、"変あるいは式" プロパティを空にします (あるいは JSON の `dataSource` フィールド):

変数名が与えられていない場合、4D はフォームがロードされたときにインタープリターのプロセス変数の空間内でユニークな名前を計算し、その名前でオブジェクト用の変数を新規作成します (このメカニズムはコンパイルモードでも使用することができます)。 この一時的な変数はフォームが閉じられるときに破棄されます。

ダイナミック変数を使用するフォームオブジェクトの値を取得あるいは設定するためには、[`OBJECT Get value`](../commands-legacy/object-get-value.md) および [`OBJECT SET VALUE`](../commands-legacy/object-set-value.md) コマンドを使用するだけです。 例:

```4d
 var $value : Variant
 $value:=OBJECT Get value("comments")
 OBJECT SET VALUE("comments";$value+10) 
```

### 配列リストボックス

配列型リストボックスの場合、リストボックスおよびリストボックス各列の **変数あるいは式** プロパティには、それぞれに関連付ける配列変数の名前を指定します。 ただし、リストボックスの JSON定義においては、列の *dataSource* 値として、配列名 (文字列) のコレクションを指定すると [階層リストボックス](listbox_overview.md#階層リストボックス) が定義されます。

#### 対象オブジェクト

[4D View Pro area](viewProArea_overview.md) - [4D Write Pro area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Hierarchical List](list_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Header](listbox_overview.md#list-box-headers) - [List Box Footer](listbox_overview.md#list-box-footers) - [Picture Pop-up Menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress indicator](progressIndicator.md) - [Radio Button](radio_overview.md) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Web Area](webArea_overview.md)

---

## 式の型/式タイプ

> [セレクション型](listbox_overview.md#セレクションリストボックス) および [コレクション型](listbox_overview.md#コレクションまたはエンティティセレクションリストボックス) のリストボックス列や、[オブジェクト](FormObjects/dropdownList_Overview.md#オブジェクトの使用) や [配列](FormObjects/dropdownList_Overview.md#配列の使用) に関連付けられた[ドロップダウンリスト](dropdownList_Overview.md) のプロパティリストでは、このプロパティは、[**データタイプ**](properties_DataSource.md#データタイプ-式の型) と呼ばれています。

オブジェクトに関連付けられた式または変数のデータ型を指定します。 この設定の主な目的は、プロパティリスト内で提供されるテーマとオプションが、データの型と対応するようにするためです。 つまり、実際に変数の型そのものを決めるわけではありません。 プロジェクトをコンパイルするには、[変数を宣言](Concepts/variables.md#変数の宣言) する必要があります。

ただし、次の特定の場合には、このプロパティは型宣言の機能を持ちえます:

- **[ダイナミック変数](#ダイナミック変数)**: このプロパティを使って、ダイナミック変数の型を宣言することができます。
- **[リストボックス列](listbox_overview.md#リストボックス列)**: このプロパティは列データに表示フォーマットを関連づけるのに使用されます。  提供されるフォーマットは変数型 (配列型のリストボックス) またはデータ/フィールド型 (セレクションおよびコレクション型のリストボックス) により異なります。 使用できる標準の 4D フォーマットはテキスト、数値、整数、日付、時間、ピクチャー、そしてブールです。 テキストの場合は専用の表示フォーマットがありません。 標準フォーマットのほかに、定義したカスタムフォーマットも選択することができます。
- **[ピクチャー変数](input_overview.md)**: このプロパティを使うと、インタープリタモードにおいてフォームロード前に変数を宣言することができます。  フォーム上のピクチャー変数にピクチャーを表示する際には特別なメカニズムが使用されます。 そのため、他の型の変数とは違って、ピクチャー変数の宣言は、フォームロード前 (`On Load` フォームイベントよりも先) におこなう必要があります。 これを行うためには、フォームのロードより前に`var varName : Picture` 宣言を実行するか(通常、`DIALOG` コマンドを呼び出したメソッド内で行います)、変数をフォームレベルで式タイププロパティを使用して型指定する必要があります。
  このいずれかをおこなわない場合、ピクチャー変数はピクチャーを正しく表示できません (インタープリターモードのみ)。

#### JSON 文法

| 名称                 | データタイプ | とりうる値                                                                                                                                                                                                                                                                                                        |
| ------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| dataSourceTypeHint | string | <li>**標準のオブジェクト**: "integer", "boolean", "number", "picture", "text", date", "time", "arrayText", "arrayDate", "arrayTime", "arrayNumber", "collection", "object", "undefined"</li><li>**リストボックス列:** "boolean", "number", "picture", "text", date", "time"。   *配列/セレクションリストボックスのみ*: "integer", "object"</li> |

#### 対象オブジェクト

[チェックボックス](checkbox_overview.md) -
[コンボボックス](comboBox_overview.md) -
[ドロップダウンリスト](dropdownList_Overview.md) -
[入力](input_overview.md) -
[リストボックス列](listbox_overview.md#リストボックス列) -
[リストボックスフッター](listbox_overview.md#リストボックスフッター) -
[プラグインエリア](pluginArea_overview.md) -
[進捗インジケーター](progressIndicator.md) -
[ラジオボタン](radio_overview.md) -
[ルーラー](ruler.md) -
[スピナー](spinner.md) -
[ステッパー](stepper.md) -
[サブフォーム](subform_overview.md) -
[タブコントロール](tabControl.md)

---

## CSSクラス

[cssファイル](FormEditor/createStylesheet.md#スタイルシートファイル) にてクラスセレクターとして使用される、(複数の場合は半角スペース区切りの) クラス名のリスト。

#### JSON 文法

| 名称    | データタイプ | とりうる値                                          |
| ----- | ------ | ---------------------------------------------- |
| class | string | (複数の場合は半角スペース区切りの) クラス名の文字列 |

#### 対象オブジェクト

[4D View Pro area](viewProArea_overview.md) - [4D Write Pro area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [List Box](listbox_overview.md) - [Picture Button](pictureButton_overview.md) - [Picture Pop-up Menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Radio Button](radio_overview.md) - [Static Picture](staticPicture.md) - [Subform](subform_overview.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

---

## コレクションまたはエンティティセレクション

コレクション要素あるいはエンティティを使用して、リストボックスの行の中身を定義することができます。

コレクションあるいはエンティティセレクションを返す式を入力します。 一般的には、コレクションまたはエンティティセレクションを格納している変数名、コレクション要素、あるいはプロパティを入力します。

コレクションおよびエンティティセレクションは、フォームロード時にフォームから利用可能でなければなりません。 コレクションの各要素、あるいはエンティティセレクションの各エンティティは、リストボックスの行へと割り当てられ、 [`This`](../Concepts/classes.md#this) キーワードを通してオブジェクトとして利用可能です:

- if you used a collection of objects, you can call **This** in the datasource expression to access each property value, for example `This.<propertyPath>`.
- if you used an entity selection, you can call **This** in the datasource expression to access each attribute value, for example `This.<attributePath>`.

> (オブジェクトでない) スカラー値のコレクションを使用した場合、データソース式内で **This.value** を呼び出すことで、各値にアクセスすることが可能です。 ただしこの場合、値の変更や現在のオブジェクトへのアクセスはできません。 ただしこの場合、値の変更や現在のオブジェクトへのアクセスはできません。

#### JSON 文法

| 名称         | データタイプ | とりうる値                      |
| ---------- | ------ | -------------------------- |
| dataSource | string | コレクションあるいはエンティティセレクションを返す式 |

#### 対象オブジェクト

[リストボックス](listbox_overview.md)

---

## データソース

リストボックスの種類を指定します。

![](../assets/en/FormObjects/listbox_dataSource.png)

- **配列** (デフォルト): リストボックスの各行に 配列要素を割り当てます。
- **カレントセレクション**: 指定したテーブルのカレントセレクションの各レコードごとに式、フィールド、メソッドが評価されます。
- **命名セレクション**: 指定した命名セレクションに含まれる各レコードごとに式、フィールド、メソッドが評価されます。
- **コレクションまたはエンティティセレクション**: コレクション要素あるいはエンティティを使用してリストボックスの行の中身を定義します。 この場合 [コレクションまたはエンティティセレクション](properties_Object.md#コレクションまたはエンティティセレクション) プロパティを定義する必要があります。 この場合 [コレクションまたはエンティティセレクション](properties_Object.md#コレクションまたはエンティティセレクション) プロパティを定義する必要があります。

#### JSON 文法

| 名称          | データタイプ | とりうる値                                                       |
| ----------- | ------ | ----------------------------------------------------------- |
| listboxType | string | "array", "currentSelection", "namedSelection", "collection" |

#### 対象オブジェクト

[リストボックス](listbox_overview.md)

---

## プラグインの種類

オブジェクトに関連付ける [プラグインが提供する外部エリア](pluginArea_overview.md) の名称。 ここで指定する名称は、プラグインの manifest.json ファイルにて公開されています。

#### JSON 文法

| 名称             | データタイプ | とりうる値                                                                            |
| -------------- | ------ | -------------------------------------------------------------------------------- |
| pluginAreaKind | string | プラグインが提供する外部エリアの、% 文字で始まる名称 (プロパティリストの候補表示では、この % 文字は表示されません) |

#### 対象オブジェクト

[プラグインエリア](pluginArea_overview.md)

---

## ラジオグループ

同じラジオグループに属している複数のラジオボタンは、一度にその内の一つのみを選択することができます。

#### JSON 文法

| 名称         | データタイプ | とりうる値    |
| ---------- | ------ | -------- |
| radioGroup | string | ラジオグループ名 |

#### 対象オブジェクト

[ラジオボタン](radio_overview.md)

---

## タイトル

オブジェクトにラベルを追加します。 このラベルのフォントとスタイルは指定することができます。

\文字 (バックスラッシュまたは円マーク) を使用すると、ラベル内で強制的に改行することができます。

![](../assets/en/FormObjects/property_title.png)

ラベルに \ を表示したい場合は &#92;&#92; と入力します。

デフォルトでラベルはオブジェクトの中央に置かれます。 またオブジェクトにアイコンも含まれている場合、[タイトル/ピクチャー位置](properties_TextAndPicture.md#タイトルピクチャー位置) プロパティを用いて、これら2 つの要素の相対位置を変更することができます。

For application translation purposes, you can enter an XLIFF reference in the title area of a button (see [Appendix B: XLIFF architecture](https://doc.4d.com/4Dv20/4D/20.2/Appendix-B-XLIFF-architecture.300-6750166.en.html)).

#### JSON 文法

| 名称   | データタイプ | とりうる値     |
| ---- | ------ | --------- |
| text | string | なんらかのテキスト |

#### 対象オブジェクト

[ボタン](button_overview.md) - [チェックボックス](checkbox_overview.md) - [リストボックスヘッダー](listbox_overview.md#リストボックスヘッダー) - [ラジオボタン](radio_overview.md) - [テキストエリア](text.md)

---

## 変数の計算

このプロパティは、[リストボックスフッター](listbox_overview.md#リストボックスフッター) エリアに適用される計算タイプを設定します。

> The calculation for footers can also be set using the [`LISTBOX SET FOOTER CALCULATION`](../commands-legacy/listbox-set-footer-calculation.md) 4D command.

様々な自動計算が利用可能です。 以下の表は、列のデータ型に応じて使用することのできる計算と、(コードで明示的に宣言されていないとき) 4D によってフッター変数に自動で割り当てられる型を示しています:

| 計算タイプ                                    | Num | Text | Date | Time | Bool | ピクチャー | フッター変数の型 |
| ---------------------------------------- | --- | ---- | ---- | ---- | ---- | ----- | -------- |
| 最小                                       | X   | X    | X    | X    | X    |       | 列の型と同じ   |
| 最大                                       | X   | X    | X    | X    | X    |       | 列の型と同じ   |
| 合計                                       | X   |      |      | X    | X    |       | 列の型と同じ   |
| カウント                                     | X   | X    | X    | X    | X    | X     | Integer  |
| 平均                                       | X   |      |      | X    |      |       | Real     |
| 標準偏差(\*)              | X   |      |      | X    |      |       | Real     |
| 分散(\*)                | X   |      |      | X    |      |       | Real     |
| 平方和(\*)               | X   |      |      | X    |      |       | Real     |
| カスタム (JSON では "none") | X   | X    | X    | X    | X    | X     | 制限なし     |

(\*) 配列型のリストボックスのみ

> フッター計算には、宣言された、あるいは動的な [変数](Concepts/variables.md) のみを使用できます。 フッター計算には、宣言された、あるいは動的な [変数](Concepts/variables.md) のみを使用できます。 その他の [式](Concepts/quick-tour.md#式) (例: `Form.value`) はサポートされていません。

自動計算の際、リストボックス行の表示/非表示状態は考慮されません。 表示行だけを計算対象にしたい場合、カスタムを選択してプログラムコードで計算しなくてはなりません。

*Null* 値は計算において無視されます。

異なる型の値がカラムに含まれる場合 (コレクションに基づいている場合など):

- 平均と合計は数値のみを計算に含めます (他の型の値は無視されます)。
- 最小と最大は、[collection.sort()](API/CollectionClass.md#sort) 関数にて定義されるのと同じ最小値と最大値を返します。

式に基づいている列のフッターにおいて自動計算を使用するにあたっては、次の制限があります:

- 式が "単純" なものの場合 (`[table]field` や `this.attribute` など) には、すべてのリストボックスタイプで **サポートされます**
- 式が "複雑" (つまり、`this.attribute` 以外) で、かつリストボックスの行数が多い場合には、コレクション/エンティティセレクションリストボックスにおいて **サポートはされるものの**、パフォーマンス上の理由により **推奨されません**。
- 式が "複雑" な場合には、カレントセレクション/命名セレクションリストボックスにおいて **サポートされません**。  これらの場合には、カスタム計算を使用する必要があります。

**カスタム** (JSON では "none") を選択した場合、4D は自動計算をおこないません。プログラムを使用して表示する値をエリアの変数に代入しなければなりません。

#### JSON 文法

| 名称                  | データタイプ | とりうる値                                                                                                 |
| ------------------- | ------ | ----------------------------------------------------------------------------------------------------- |
| variableCalculation | string | "none", "minimum", "maximum", "sum", "count", "average", "standardDeviation", "variance", "sumSquare" |

#### 対象オブジェクト

[リストボックスフッター](listbox_overview.md#リストボックスフッター)
