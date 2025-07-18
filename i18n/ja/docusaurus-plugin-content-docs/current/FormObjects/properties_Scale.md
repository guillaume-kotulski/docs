---
id: propertiesScale
title: スケール
---

## バーバーショップ

このプロパティは、サーモメーターの "バーバーショップ" バリエーションを有効にします。

#### JSON 文法

|     名称     | データタイプ | とりうる値                                                         |
| :--------: | :----: | ------------------------------------------------------------- |
| [max](#最大) | number | プロパティが存在しない = 有効; 存在する = 無効 (デフォルトサーモメーター) |

#### 対象オブジェクト

[バーバーショップ](progressIndicator.md#バーバーショップ)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT Get indicator type](../commands-legacy/object-get-indicator-type.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md) - [OBJECT SET INDICATOR TYPE](../commands-legacy/object-set-indicator-type.md)

---

## 目盛りを表示

ラベルの隣に目盛を表示、または非表示にします。

#### JSON 文法

|        名称       |  データタイプ | とりうる値           |
| :-------------: | :-----: | --------------- |
| showGraduations | boolean | "true", "false" |

#### 対象オブジェクト

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## 目盛りのステップ

目盛の表示単位です。

#### JSON 文法

|       名称       |  データタイプ | とりうる値                  |
| :------------: | :-----: | ---------------------- |
| graduationStep | integer | 最小値: 0 |

#### 対象オブジェクト

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## ラベル位置

ラベルが表示される際の位置です。

- なし - ラベルは表示されません。
- 上 - インジケーターの上または左にラベルを表示します。
- 下 - インジケーターの下または右にラベルを表示します。

#### JSON 文法

|        名称       | データタイプ | とりうる値                                    |
| :-------------: | :----: | ---------------------------------------- |
| labelsPlacement | string | "none", "top", "bottom", "left", "right" |

#### 対象オブジェクト

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## 最大

インジケーターの最大値です。

- 時間型のステッパーの場合、値は秒を表します。日付型のステッパーでは、最小および最大プロパティは無視されます。
- [バーバーショップサーモメーター](progressIndicator.md#バーバーショップ) を有効にするには、このプロパティを取り除きます。

#### JSON 文法

|  名称 | データタイプ | とりうる値 |
| :-: | :----: | ----- |
| max | number | 数値    |

#### 対象オブジェクト

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md) - [Stepper](stepper.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get maximum-value](../commands-legacy/object-get-maximum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md) - [OBJECT SET MAXIMUM VALUE](../commands-legacy/object-set-maximum-value.md)

---

## 最小

インジケーターの最小値です。 時間型のステッパーの場合、値は秒を表します。日付型のステッパーでは、最小および最大プロパティは無視されます。

#### JSON 文法

|  名称 | データタイプ | とりうる値 |
| :-: | :----: | ----- |
| min | number | 数値    |

#### 対象オブジェクト

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md) - [Stepper](stepper.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md) - [OBJECT SET MINIMUM VALUE](../commands-legacy/object-set-minimum-value.md)

---

## ステップ

使用時に各値の間にあけることができる最小の間隔です。 時間型のステッパーの場合、このプロパティは秒を表します。日付型のステッパーでは日数を表します。

#### JSON 文法

|  名称  |  データタイプ | とりうる値                  |
| :--: | :-----: | ---------------------- |
| step | integer | 最小値: 1 |

#### 対象オブジェクト

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md) - [Stepper](stepper.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)
