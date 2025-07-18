---
id: propertiesWebArea
title: Webエリア
---

---

## 4Dメソッドコールを許可

Webエリアで実行される JavaScript コードから 4Dメソッドおよびクラス関数を呼び出して、戻り値を取得することができます。 4Dメソッドを Webエリアから呼び出せるようにするには、プロパティリストの "4Dメソッドコールを許可" にチェックをする必要があります。

> この機能は Webエリアが [埋め込みWebレンダリングエンジンを使用](#埋め込みwebレンダリングエンジンを使用) している場合に限り、使用可能です。

このプロパティがチェックされている場合、特別な JavaScript オブジェクト `$4d` が Webエリア内にインスタンス化され、これを使用して[4Dプロジェクトメソッドおよび関数の呼び出しを管理](webArea_overview.md#4dオブジェクトの使用) できるようになります。

#### JSON 文法

| 名称                   | データタイプ | とりうる値                                    |
| -------------------- | ------ | ---------------------------------------- |
| methodsAccessibility | string | "none" (デフォルト), "all" |

#### 対象オブジェクト

[Web エリア](webArea_overview.md)

---

## 進捗状況変数

倍長整数型変数の名前です。 この変数には 0 から 100 までの値が格納され、この数値は Webエリアに表示されるページのロードされたパーセンテージを表します。 手動で変更することはできません。

> 4D v19 R5 以降、Windows上では、Web エリアが [ 埋め込みWebレンダリングエンジン](properties_WebArea.md#埋め込みwebレンダリングエンジンを使用) を使用している場合にのみ、この変数が更新されます。

#### JSON 文法

| 名称             | データタイプ | とりうる値      |
| -------------- | ------ | ---------- |
| progressSource | string | 倍長整数型変数の名前 |

#### 対象オブジェクト

[Web エリア](webArea_overview.md)

---

## URL

文字列型の変数で、Webエリアにロードされた URL またはロード中の URL が格納されます。 変数と Webエリア間の連携は双方向でおこなわれます。

- ユーザーが新しい URL を変数に割り当てると、その URL は自動で Webエリアにロードされます。
- Webエリアでブラウズされると、自動で変数の内容が更新されます。

このエリアは Webブラウザーのアドレスバーのように機能します。 Webエリアの上側にテキストエリアを置いて、内容を表示させることができます。

### URL変数と WA OPEN URL コマンド

The URL variable produces the same effects as the [`WA OPEN URL`](../commands-legacy/wa-open-url.md) command. しかしながら、以下の違いに注意してください。

- ドキュメントにアクセスする場合、この変数は RFC準拠 ("file://c:/My%20Doc") な URL のみを受け付け、システムパス名 ("c:\MyDoc") は受け付けません。 The [`WA OPEN URL`](../commands-legacy/wa-open-url.md) command accepts both notations.
- URL変数が空の文字列の場合、Webエリアは URL をロードしません。 The [`WA OPEN URL`](../commands-legacy/wa-open-url.md) command generates an error in this case.
- If the URL variable does not contain a protocol (http, mailto, file, etc.), the Web area adds "http://", which is not the case for the [`WA OPEN URL`](../commands-legacy/wa-open-url.md) command.
- When the Web area is not displayed in the form (when it is located on another page of the form), executing the [`WA OPEN URL`](../commands-legacy/wa-open-url.md) command has no effect, whereas assigning a value to the URL variable can be used to update the current URL.

#### JSON 文法

| 名称        | データタイプ | とりうる値 |
| --------- | ------ | ----- |
| urlSource | string | URL   |

#### 対象オブジェクト

[Web エリア](webArea_overview.md)

#### コマンド

[`WA GET PREFERENCE`](../commands-legacy/wa-get-preference.md) - [`WA SET PREFERENCE`](../commands-legacy/wa-set-preference.md)

---

## 埋め込みWebレンダリングエンジンを使用

このオプションを使用して、Webエリアで使用する描画エンジンを 2つのうちから選択することができます:

- **チェックなし** - `JSON値: system` (デフォルト): この場合、4Dはシステムの最適なエンジンを使用します。 この結果、HTML5 や JavaScript の最新 Web描画エンジンを自動的に利用できることになります。 しかし、プラットフォーム間で若干描画に違いがでることがあります。 Windows では、4Dは Microsoft Edge WebView2 を使用します。 macOS では、カレントバージョンの WebKit (Safari) です。 この結果、HTML5 や JavaScript の最新 Web描画エンジンを自動的に利用できることになります。 しかし、プラットフォーム間で若干描画に違いがでることがあります。 Windows では、4Dは Microsoft Edge WebView2 を使用します。 macOS では、カレントバージョンの WebKit (Safari) です。

> Windows で Microsoft Edge WebView2がインストールされていない場合、4D はシステムのレンダリングエンジンとして埋め込みエンジンを使用します。 システムにインストールされているかどうかを確認するには、アプリケーションパネルで "Microsoft Edge WebView2 Runtime" を検索してください。

- **チェックあり** - `JSON値: embedded`: この場合、4D は Chromium Embedded Framework (CEF) を使用します。 埋め込みWebレンダリングエンジンを使用すると、Webエリアの描画とその動作が (ピクセル単位での若干の相違やネットワーク実装に関連する違いを除き) プラットフォームに関わらず同じになります。 このオプションが選択されると、OS によりおこなわれる自動更新などの利点を得ることができなくなります。使用エンジンの新バージョンは 4D のリリースを通して定期的に提供されます。 埋め込みWebレンダリングエンジンを使用すると、Webエリアの描画とその動作が (ピクセル単位での若干の相違やネットワーク実装に関連する違いを除き) プラットフォームに関わらず同じになります。 このオプションが選択されると、OS によりおこなわれる自動更新などの利点を得ることができなくなります。 使用エンジンの新バージョンは 4D のリリースを通して定期的に提供されます。

CEFエンジンには以下のような制約があります:

- [WA SET PAGE CONTENT](../commands-legacy/wa-set-page-content.md): このコマンドを使用する場合、([`WA OPEN URL`](../commands-legacy/wa-open-url.md) コマンドを呼び出すかあるいはエリアに割り当てられた URL変数への代入を通して) 少なくとも既に 1ページがエリア内に読み込まれている必要があります。
- [WA SET PREFERENCE](../commands-legacy/wa-set-preference.md) コマンドの `WA enable URL drop` セレクターによって URLドロップが許可されている場合、最初のドロップをする前に少なくとも 1度は [WA OPEN URL](../commands-legacy/wa-open-url.md) コマンドを呼び出すか、またはエリアに割り当てられている URL 変数に URL が渡されている必要があります。

:::note

ローカルで [4DCEFParameters.json 設定ファイル](webArea_overview.md#4dcefparametersjson) を作成することで、CEFエリアのパラメーターをカスタマイズできます。

:::

#### JSON 文法

| 名称        | データタイプ | とりうる値                |
| --------- | ------ | -------------------- |
| webEngine | string | "embedded", "system" |

#### 対象オブジェクト

[Web エリア](webArea_overview.md)

#### コマンド

[`WA GET PREFERENCE`](../commands-legacy/wa-get-preference.md) - [`WA SET PREFERENCE`](../commands-legacy/wa-set-preference.md)