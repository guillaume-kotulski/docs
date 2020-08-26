---
id: datastores
title: リモートデータストアの利用
---

4D アプリケーション上で公開された [データストア](dsMapping.md#データストア) は、異なるクライアントにより同時にアクセスすることができます:

- 4D リモートアプリケーションは ORDA を使っていれば、`ds` コマンドでメインデータストアにアクセスできます。 この 4D リモートアプリケーションは従来のモードでもデータベースにアクセスできます。 これらのアクセスを処理するのは **4Dアプリケーションサーバー** です。
- 他の 4Dアプリケーション (4Dリモート、4D Server) は、`Open datastore` コマンドを使ってリモートデータストアのセッションを開始できます。 アクセスを処理するのは **HTTP REST サーバー** です。
- iOS アプリケーションを更新するため、4D for iOS のクエリでアクセスできます。 アクセスを処理するのは **HTTP サーバー** です。


`Open datastore` コマンドによって参照されるリモートデータストアの場合、リクエスト元プロセスとリモートデータストア間の接続はセッションにより管理されます。


## セッションの開始

4Dアプリケーション (のプロセス) が `Open datastore` コマンドを使って外部のデータストアを開くと、この接続を管理するためにリモートデータストアではセッションが開始されます。 このセッションは内部的にセッションID によって識別され、4Dアプリケーション上では ` localID` と紐づいています。 データ、エンティティセレクション、エンティティへのアクセスはこのセッションによって自動的に管理されます。

`localID` はリモートデータストアに接続しているマシンにおけるローカルな識別IDです:

*   同じアプリケーションの別プロセスが同じリモートデータストアに接続する場合、`localID` とセッションは共有することができます。
*   同じアプリケーションの別プロセスが別の `localID` を使って同じデータストアに接続した場合、リモートデータストアでは新しいセッションが開始されます。
*   他のマシンが同じ `localID` を使って同じデータストアに接続した場合、新しいセッションが新しい cookie で開始されます。

これらの原則を下図に示します:

![](assets/en/Orda/sessions.png)

> REST リクエストによって開かれたセッションについては、[ユーザーとセッション](REST/authUsers.md) を参照ください。

## セッションの監視

データストアアクセスを管理しているセッションは 4D Server の管理画面に表示されます:

*   プロセス名: "REST Handler: \<process name>"
*   タイプ: HTTP Server Worker
*   セッション: `Open datastore` コマンドに渡されたユーザー名

次の例では、1つのセッション上で 2つのプロセスが実行中です:

![](assets/en/Orda/sessionAdmin.png)

## ロッキングとトランザクション

エンティティロッキングやトランザクションに関連した ORDA 機能は、ORDA のクライアント / サーバーモードと同様に、リモートデータストアにおいてもプロセスレベルで管理されます:

*   あるプロセスがリモートデータストアのエンティティをロックした場合、セッションの共有如何に関わらず、他のすべてのプロセスに対してそのエンティティはロックされた状態です ([エンティティロッキング](entities.md#エンティティロッキング) 参照)。 If several entities pointing to a same record have been locked in a process, they must be all unlocked in the process to remove the lock. If a lock has been put on an entity, the lock is removed when there is no more reference to this entity in memory.
*   Transactions can be started, validated or cancelled separately on each remote datastore using the `dataStore.startTransaction()`, `dataStore.cancelTransaction()`, and `dataStore.validateTransaction()` functions. They do not impact other datastores.
*   Classic 4D language commands (`START TRANSACTION`, `VALIDATE TRANSACTION`, `CANCEL TRANSACTION`) only apply to the main datastore (returned by `ds`). If an entity from a remote datastore is hold by a transaction in a process, other processes cannot update it, even if these processes share the same session.
*   Locks on entities are removed and transactions are rollbacked:
    *   when the process is killed.
    *   when the session is closed on the server
    *   when the session is killed from the server administration window.

## Closing sessions

A session is automatically closed by 4D when there has been no activity during its timeout period. The default timeout is 60 mn, but this value can be modified using the `connectionInfo` parameter of the `Open datastore` command.

If a request is sent to the remote datastore after the session has been closed, it is automatically re-created if possible (license available, server not stopped...). However, keep in mind that the context of the session regarding locks and transactions is lost (see above). 
