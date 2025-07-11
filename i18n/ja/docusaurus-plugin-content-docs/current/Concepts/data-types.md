---
id: data-types
title: データタイプの概要
---

4D においてデータは、主にデータベースフィールドと 4D ランゲージという2つの場所で、そのタイプに応じて扱われます。

この2つはおおよそ同じものですが、データベースレベルで提供されているいくつかのデータタイプはランゲージにおいては直接利用可能ではなく、自動的に適宜変換されます。 同様に、いくつかのデータタイプはランゲージでしか利用できません。 各場所で利用可能なデータタイプと、ランゲージでの宣言の仕方の一覧です:

| データタイプ                                                | データベース                     | ランゲージ    | [`var` 宣言](variables.md) | [`ARRAY` 宣言](arrays.md) |
| ----------------------------------------------------- | -------------------------- | -------- | ------------------------ | ----------------------- |
| [文字列](dt_string.md)                                   | ◯                          | テキストに変換  | -                        | -                       |
| [テキスト](Concepts/dt_string.md)                         | ◯                          | ◯        | `Text`                   | `ARRAY TEXT`            |
| [日付](Concepts/dt_date.md)                             | ◯                          | ◯        | `Date`                   | `ARRAY DATE`            |
| [時間](Concepts/dt_time.md)                             | ◯                          | ◯        | `Time`                   | `ARRAY TIME`            |
| [ブール](Concepts/dt_boolean.md)                         | ◯                          | ◯        | `Boolean`                | `ARRAY BOOLEAN`         |
| [整数](Concepts/dt_number.md)                           | ◯                          | 倍長整数 に変換 | `Integer`                | `ARRAY INTEGER`         |
| [倍長整数](Concepts/dt_number.md)                         | ◯                          | ◯        | `Integer`                | `ARRAY LONGINT`         |
| [64ビット整数](Concepts/dt_number.md)                      | ◯ (SQL) | 実数に変換    | -                        | -                       |
| [実数](Concepts/dt_number.md)                           | ◯                          | ◯        | `Real`                   | `ARRAY REAL`            |
| [未定義](Concepts/dt_null_undefined.md)                  | -                          | ◯        | -                        | -                       |
| [Null](Concepts/dt_null_undefined.md)                 | -                          | ◯        | -                        | -                       |
| [ポインター](Concepts/dt_pointer.md)                       | -                          | ◯        | `Pointer`                | `ARRAY POINTER`         |
| [ピクチャー](Concepts/dt_picture.md)                       | ◯                          | ◯        | `Picture`                | `ARRAY PICTURE`         |
| [BLOB](Concepts/dt_blob.md)                           | ◯                          | ◯        | `Blob`, `4D.Blob`        | `ARRAY BLOB`            |
| [オブジェクト](Concepts/dt_object.md)                       | Yes(3)  | ◯        | `Object`                 | `ARRAY OBJECT`          |
| [コレクション](Concepts/dt_collection.md)                   | -                          | ◯        | `Collection`             |                         |
| [バリアント](Concepts/dt_variant.md)(2) | -                          | ◯        | `Variant`                |                         |

(1) ORDA では、オブジェクト (エンティティ) を介してデータベースフィールドを扱うため、オブジェクトにおいて利用可能なデータタイプのみがサポートされます。 詳細については [オブジェクト](Concepts/dt_object.md) のデータタイプの説明を参照ください。

(2) バリアントは実際のところ *データ* タイプではなく、あらゆるデータタイプの値を格納することのできる *変数* タイプです。

(3) You can [assign a class](../Develop/field-properties.md) to an object field in the structure editor.

## コマンド

以下のコマンドを使用することで、フィールドや変数の型を調べることができます:

- フィールドやスカラー変数に対しては、[`Type`](../commands-legacy/type.md) コマンド
- 式対しては、[`Value type`](../commands-legacy/value-type.md) コマンド

## デフォルト値

[明示的な宣言](variables.md#変数の宣言) によって [変数](variables.md) または [引数](parameters.md) の型が決まるとき、変数はデフォルトの値を受け取り、割り当てがされない限りセッション中はその値を保ち続けます。

デフォルト値は変数の型に依存します:

| 型          | デフォルト値                                   |
| ---------- | ---------------------------------------- |
| ブール        | false                                    |
| Date       | 00-00-00                                 |
| Integer    | 0                                        |
| Time       | 00:00:00 |
| Picture    | ピクチャーサイズ=0                               |
| Real       | 0                                        |
| Pointer    | Nil=true                                 |
| Text       | ""                                       |
| BLOB       | BLOB サイズ=0                               |
| Object     | null                                     |
| Collection | null                                     |
| Variant    | undefined                                |

### デフォルト値としての Null

Object型、Collection型、Pointer型、Picture型の変数は、デフォルト値として **null** を持ちますが、実際には宣言後で割り当て前の場合には中間的 な状態になります。 これらは **null** 値の *ように振る舞います* が、コードがそれらにアクセスしようとしたときに発生するエラーが少なくなるなど、多少の違いがあります。

## データタイプの変換

4D ランゲージには、データタイプ間の変換をおこなう演算子やコマンドがあります。 4D ランゲージはデータタイプをチェックします。 たとえば、"abc"+0.5+!12/25/96!-?00:30:45?のように記述することはできません。 これは、シンタックス (構文) エラーになります。

次の表は、基本のデータタイプ、変換できるデータタイプ、それを実行する際に使用するコマンドを示しています:

| データタイプ                     | 文字列に変換   | 数値に変換 | 日付に変換  | 時間に変換  | ブールに変換 |
| -------------------------- | -------- | ----- | ------ | ------ | ------ |
| 文字列 (1) |          | `Num` | `Date` | `Time` | `Bool` |
| 数値 (2)  | `String` |       |        |        | `Bool` |
| Date                       | `String` |       |        |        | `Bool` |
| Time                       | `String` |       |        |        | `Bool` |
| Boolean                    |          | `Num` |        |        |        |

(1) JSON形式の文字列は `JSON Parse` コマンドを使ってスカラーデータ、オブジェクト、あるいはコレクションに変換することができます。

(2) 時間は数値として扱うことができます。

**注:** この表に示すデータ変換の他に、演算子と他のコマンドを組み合せることで、より洗練されたデータ変換を実行することができます。
