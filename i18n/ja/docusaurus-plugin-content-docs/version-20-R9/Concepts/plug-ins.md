---
id: plug-ins
title: プラグイン
---

4Dアプリケーションの開発を進めていくと、最初は気付かなかった数多くの機能を発見することでしょう。 それだけでなく、**プラグイン** を4D開発環境に追加することで、標準の4Dの機能を高めることもできます。

## プラグインとは何か

プラグインとは、C や C++ などの言語で書かれた、4D 起動時にロードされるコードのことです。 プラグインは、4D に機能を追加します。 プラグインには通常複数のルーチンが含まれています。 プラグインは外部エリアを操作でき、外部プロセスを実行できます。

## プラグインの見つけ方

4Dコミュニティによって多数のプラグインが作成されています。 公開されたプラグインは [GitHub](https://github.com/search?q=4d-plugin&type=Repositories) で確認できます。 また、[独自のプラグインを開発](Extensions/develop-plug-ins.md) することもできます。

## プラグインのインストール

4D環境にプラグインをインストールするには、プラグインファイルを [Projectフォルダーと同じ階層](../Project/architecture.md#plugins) の **Plugins** フォルダーにコピーします。

プラグインは 4D 起動時にロードされるので、これらをインストールする際には 4Dアプリケーションを終了する必要があります。 プラグインの利用に特別なライセンスが必要な場合、プラグインはロードされますが、ライセンスをインストールするまで使用することはできません。

## プラグインの使い方

プラグインコマンドは、4D開発において通常の 4Dコマンドと同様に使用できます。 プラグインコマンドは、エクスプローラーの **プラグイン** ページに表示されます。


