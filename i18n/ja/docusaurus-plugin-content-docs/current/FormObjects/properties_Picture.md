---
id: propertiesPicture
title: Picture
---

## パス名

[ピクチャーボタン](pictureButton_overview.md)、[ピクチャーポップアップメニュー](picturePopupMenu_overview.md)、または [スタティックピクチャー](staticPicture.md) に表示させるピクチャーのパス名です。 POSIX シンタックスを使用します。

ピクチャーパスに指定できる場所は次の 3箇所です:

- プロジェクトの **Resources** フォルダー。 プロジェクト内の複数のフォームで画像を共有する場合に適切です。 この場合、パス名は "/RESOURCES/&lt;picture path&gt;" です。
- フォームフォルダー内の画像用フォルダー (たとえば、**Images** と名付けたフォルダー)。 特定のフォームでしか画像が使われない場合や、そのフォームの全体を複製してプロジェクト内、または別のプロジェクトに移動させたい場合に適切です。 この場合、パス名は "&lt;picture path&gt;" となり、フォームフォルダーを基準とした相対パスです。
- 4D のピクチャー変数。 フォーム実行時に、ピクチャーがメモリに読み込まれている必要があります。 この場合、パス名は "var:&lt;variableName&gt;"。

#### JSON 文法

|    名称   | データタイプ | とりうる値                                                                                                                        |
| :-----: | :----: | ---------------------------------------------------------------------------------------------------------------------------- |
| picture |  text  | POSIXシンタックスの相対パスまたはファイルシステムパス、ピクチャー変数の場合は "var:&lt;variableName&gt;" |

#### 対象オブジェクト

[ピクチャーボタン](pictureButton_overview.md) - [ピクチャーポップアップメニュー](picturePopupMenu_overview.md) - [スタティックピクチャー](staticPicture.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## 表示

### スケーリング

`JSON 文法では: "scaled"`

**スケーリング** を選択すると、ピクチャーはフィールドエリアの大きさに合うようにリサイズされます。

![](../assets/en/FormObjects/property_pictureFormat_ScaledToFit.png)

### 繰り返し

`JSON 文法では: "tiled"`

**繰り返し** フォーマットを持つピクチャーが含まれるエリアが拡大されると、ピクチャーは変形されず、エリア全体を埋めるのに必要なだけピクチャーが繰り返されます。

![](../assets/en/FormObjects/property_pictureFormat_Replicated.png)

フィールドがオリジナルのピクチャーよりも小さいサイズにされた場合、ピクチャーはトランケート (中央合わせなし) されます。

### 中央合わせ / トランケート (中央合わせしない)

`JSON 文法では: "truncatedCenter" / "truncatedTopLeft"`

**中央合わせ** フォーマットを選択すると、4D はエリアの中央にピクチャーを配置し、収まらない部分はエリアからはみ出します。 上下、および左右のはみ出し量は同じになります。

**トランケート (中央合わせしない)** フォーマットを選択すると、4D はピクチャーの左上角をフィールドの左上角に合わせて配置し、フィールドエリアに収まらない部分はエリアからはみ出します。 ピクチャーは右と下にはみ出します。

> ピクチャーフォーマットが **トランケート (中央合わせしない)** の場合、入力エリアにスクロールバーを追加できます。

![](../assets/en/FormObjects/property_pictureFormat_Truncated.png)

#### JSON 文法

| 名称            | データタイプ | とりうる値                                                    |
| ------------- | ------ | -------------------------------------------------------- |
| pictureFormat | string | "scaled", "tiled", "truncatedCenter", "truncatedTopLeft" |

#### 対象オブジェクト

[スタティックピクチャー](staticPicture.md)

#### コマンド

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)
