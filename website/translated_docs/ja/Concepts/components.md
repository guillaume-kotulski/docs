---
id: components
title: コンポーネント
---

4D のコンポーネントとは、他のアプリケーションにインストール可能な、1つ以上の機能を持つ 4D メソッドやフォームの一式です。 たとえば、メールの送受信をおこない、それらを 4D アプリケーションに格納するための機能を持ったコンポーネントを作成できます。

4D コンポーネントの作成とインストールは直接 4D を使用しておこないます。 4D では、コンポーネントは [プラグイン](Concepts/plug-ins.md) のように扱われ、以下の原則が適用されます:

- コンポーネントは、標準のアーキテクチャーまたはパッケージ (.4dbase 拡張子) の形をしたストラクチャーファイル ( コンパイルまたは非コンパイル) で構成されます。
- アプリケーションプロジェクトにコンポーネントをインストールするには、プロジェクトの Project フォルダーと同階層の "Components" フォルダーにコンポーネントをコピーします。
- コンポーネントは次の 4D の要素を呼び出すことができます: プロジェクトメソッド、プロジェクトフォーム、メニューバー、選択リスト、ライブラリピクチャーなど。 反面、コンポーネントが呼び出せないものは、データベースメソッドとトリガーです。
- コンポーネント内で標準のテーブルやデータファイルを使用することはできません。 しかし、外部データベースのメカニズムを使用すればテーブルやフィールドを作成し、そこにデータを格納したり読み出したりすることができます。 外部データベースは、メインの 4D データベースとは独立して存在し、SQLコマンドでアクセスします。


## 定義

4D のコンポーネント管理メカニズムでは、以下の用語とコンセプトを使います:

- **マトリクスプロジェクト**: コンポーネント開発に使用する4D プロジェクト。 マトリクスプロジェクトは特別な属性を持たない標準のプロジェクトです。 マトリクスプロジェクトはひとつのコンポーネントを構成します。 マトリクスプロジェクトは、コンポーネントを使用するプロジェクト (ホストアプリケーションプロジェクト) の Components フォルダーにコピーして使います。コンパイルされていてもいなくてもかまいません。
- **ホストプロジェクト**: コンポーネントがインストールされ、それを使用するアプリケーションプロジェクト。
- **コンポーネント**: ホストアプリケーションによって使用される目的で、同アプリケーションの Components フォルダーにコピーされたマトリクスプロジェクト (コンパイル済みまたは非コンパイル)。

プロジェクトは "マトリクス" にも "ホスト" にもなりえます。言い換えれば、マトリクスプロジェクト自体も1 つ以上のコンポーネントを使用できます。 しかしコンポーネントが "サブコンポーネント" を使用することはできません。


### コンポーネントの保護: コンパイル

コンポーネントとしてインストールされたマトリクスプロジェクトのプロジェクトメソッドは、ホストプロジェクトからデフォルトでアクセス可能です。 特に:

- エクスプローラーのメソッドページに存在する共有のプロジェクトメソッドは、ホストプロジェクトのメソッドから呼び出し可能です。 エクスプローラーのプレビューエリアでそれらの内容を選択してコピーすることが可能です。 また、その内容はデバッガーで見ることもできます。 しかし、それらをメソッドエディター上で開いたり編集したりすることはできません。
- マトリクスプロジェクトの他のプロジェクトメソッドはエクスプローラーに現れません。しかし、ホストプロジェクトのデバッガーには内容が表示されます。

コンポーネントのプロジェクトメソッドを効果的に保護するには、マトリクスプロジェクトをコンパイルして、インタプリターコードを含まない .4dz ファイルとして提供します。 コンパイルされたマトリクスプロジェクトがコンポーネントとしてインストールされると:

- エクスプローラーのメソッドページに存在する共有のプロジェクトメソッドは、ホストプロジェクトのメソッドから呼び出し可能です。 しかし、その内容はプレビューエリアにもデバッガーにも表示されません。
- マトリクスプロジェクトの他のプロジェクトメソッドは一切表示されません。


## プロジェクトメソッドの共有
マトリクスプロジェクトのすべてのプロジェクトメソッドは 、コンポーネントに含まれます。つまり、マトリクスプロジェクトをコンポーネント化しても、これらのプロジェクトメソッドは同コンポーネントにて呼び出して実行することができます。

他方、デフォルトでは、これらのプロジェクトメソッドはホストプロジェクトに表示されず、呼び出すこともできません。 プロジェクトメソッドをホストプロジェクトと共有するには、 マトリクスプロジェクト側でそのメソッドをそのように明示的に設定しなければなりません。 設定することで、それらのプロジェクトメソッドはホストプロジェクトにて呼び出すことができるようになります (しかしホストプロジェクトのメソッドエディターで編集することはできません)。 これらのメソッドはコンポーネントの **エントリーポイント** となります。

**注:** セキュリティのため、デフォルトでは、コンポーネントはホストプロジェクトのプロジェクトメソッドを実行することはできません。 特定の場合に、ホストプロジェクトのプロジェクトメソッドにコンポーネントがアクセスできるようにする必要があるかもしれません。 そうするには、ホストプロジェクトのプロジェクトメソッド側で、コンポーネントからのアクセスを可能にするよう明示的に指定しなければなりません。

![](assets/en/Concepts/pict516563.en.png)

## 変数の渡し方

ローカル、プロセス、インタープロセス変数は、コンポーネントとホストプロジェクト間で共有されません。 ホストプロジェクトからコンポーネントの変数、またはその逆にアクセスする唯一の方法はポインターを使用することです。

配列を使用した例:

```4d
// ホストプロジェクト側:
     ARRAY INTEGER(MyArray;10)
     AMethod(->MyArray)

// コンポーネント側で AMethod プロジェクトメソッドは以下の通りです:
     APPEND TO ARRAY($1->;2)
```

変数を使用した例:

```4d
 C_TEXT(myvariable)
 component_method1(->myvariable)
 C_POINTER($p)
 $p:=component_method2(...)
```


ホストプロジェクトとコンポーネント間でポインターを使用して通信をおこなうには、以下の点を考慮する必要があります:

- `Get pointer` をコンポーネント内で使用した場合、このコマンドはホストプロジェクトの変数へのポインターを返しません。また逆にこのコマンドをホストプロジェクトで使用した場合も同様です。

- The component architecture allows the coexistence, within the same interpreted project, of both interpreted and compiled components (conversely, only compiled components can be used in a compiled project). この場合、ポインターの利用は以下の原則を守らなければなりません: インタープリターモードでは、コンパイルモードにおいて作成されたポインターを解釈できます。逆にコンパイルモードでは、インタープリターモードにて作成されたポインターを解釈することはできません。 Let’s illustrate this principle with the following example: given two components, C (compiled) and I (interpreted), installed in the same host project.
 - コンポーネントC が定義する変数 `myCvar` があるとき、コンポーネントI はポインター `->myCvar` を使用して変数の値にアクセスすることができます。
 - コンポーネントI が定義する変数 `myIvar` があるとき、コンポーネントC はポインター `->myIvar` を使用しても変数の値にアクセスすることはできません。 このシンタックスは実行エラーを起こします。

- The comparison of pointers using the `RESOLVE POINTER` command is not recommended with components since the principle of partitioning variables allows the coexistence of variables having the same name but with radically different contents in a component and the host project (or another component). 両コンテキストで、変数のタイプが違うことさえありえます。 ポインター `myptr1` と `myptr2` がそれぞれ変数を指すとき、以下の比較は正しくない結果となるかもしれません:

```4d
     RESOLVE POINTER(myptr1;vVarName1;vtablenum1;vfieldnum1)
     RESOLVE POINTER(myptr2;vVarName2;vtablenum2;vfieldnum2)
     If(vVarName1=vVarName2)
      // 変数が異なっているにもかかわらず、このテストはtrue を返します
```
このような場合には、ポインターを比較しなければなりません:
```4d
     If(myptr1=myptr2) // このテストはFalse を返します
```

## Access to tables of the host project

Although components cannot use tables, pointers can permit host projects and components to communicate with each other. たとえば、以下はコンポーネントで実行可能なメソッドです:

```4d
// コンポーネントメソッドの呼び出し
methCreateRec(->[PEOPLE];->[PEOPLE]Name;"Julie Andrews")
```

コンポーネント内の `methCreateRec` メソッドのコード:

```4d
C_POINTER($1) //Pointer on a table in host project
C_POINTER($2) //Pointer on a field in host project
C_TEXT($3) // Value to insert

$tablepointer:=$1
$fieldpointer:=$2
CREATE RECORD($tablepointer->)

$fieldpointer->:=$3
SAVE RECORD($tablepointer->)
```

## ランゲージコマンドのスコープ

[使用できないコマンド](#使用できないコマンド) を除き、コンポーネントではすべての 4D ランゲージコマンドが使用できます。

コマンドがコンポーネントから呼ばれると、コマンドはコンポーネントのコンテキストで実行されます。ただし `EXECUTE METHOD` コマンドは除きます。このコマンドは、パラメーターにて指定されたメソッドのコンテキストを使用します。 Also note that the read commands of the “Users and Groups” theme can be used from a component but will read the users and groups of the host project (a component does not have its own users and groups).

The `SET DATABASE PARAMETER` and `Get database parameter` commands are an exception: their scope is global to the application. When these commands are called from a component, they are applied to the host application project.

さらに、`Structure file` と `Get 4D folder` コマンドは、コンポーネントで使用するための設定ができるようになっています。

The `COMPONENT LIST` command can be used to obtain the list of components that are loaded by the host project.


### 使用できないコマンド

(読み込み専用モードで開かれるため) ストラクチャーファイルを更新する以下のコマンドは、コンポーネントで使用することができません。 コンポーネント中で以下のコマンドを実行すると、-10511, "CommandName コマンドをコンポーネントでコールすることはできません" のエラーが生成されます:

- `ON EVENT CALL`
- `Method called on event`
- `SET PICTURE TO LIBRARY`
- `REMOVE PICTURE FROM LIBRARY`
- `SAVE LIST`
- `ARRAY TO LIST`
- `EDIT FORM`
- `CREATE USER FORM`
- `DELETE USER FORM`
- `CHANGE PASSWORD`
- `EDIT ACCESS`
- `Set group properties`
- `Set user properties`
- `DELETE USER`
- `CHANGE LICENSES`
- `BLOB TO USERS`
- `SET PLUGIN ACCESS`

**注:**

- `Current form table` コマンドは、プロジェクトフォームのコンテキストで呼び出されると `Nil` を返します。 ゆえにこのコマンドをコンポーネントで使用することはできません。
- SQL data definition language commands (`CREATE TABLE`, `DROP TABLE`, etc.) cannot be used on the component project. ただし、外部データベースの場合は使用することができます (`CREATE DATABASE` SQL コマンド参照)。

## エラー処理

An [error-handling method](Concepts/error-handling.md) installed by the `ON ERR CALL` command only applies to the running application. In the case of an error generated by a component, the `ON ERR CALL` error-handling method of the host project is not called, and vice versa.

## フォームの使用

- 特定のテーブルに属さない" プロジェクトフォーム" のみが、コンポーネント内で利用できます。 Any project forms present in the matrix project can be used by the component.
- A component can call table forms of the host project. この場合、コンポーネントのコードでフォームを指定するにあたっては、テーブル名ではなく、テーブルへのポインターを使用しなければならないことに注意してください。

**Note:** If a component uses the `ADD RECORD` command, the current Input form of the host project will be displayed, in the context of the host project. したがって、その入力フォーム上に変数が含まれている場合、コンポーネントはその変数にアクセスできません。

- You can publish component forms as subforms in the host projects. これは具体的には、グラフィックオブジェクトを提供するコンポーネントを開発できることを意味します。 たとえば、4D社が提供するウィジェットはコンポーネントのサブフォーム利用に基づいています。

## テーブルやフィールドの利用

A component cannot use the tables and fields defined in the 4D structure of the matrix project. しかし外部データベースを作成し、そのテーブルやフィールドを必要に応じ利用することはできます。 外部データベースの作成と管理は SQL を用いておこないます。 An external database is a 4D project that is independent from the main 4D project, but that you can work with from the main 4D project. 外部データベースの利用は、そのデータベースを一時的にカレントデータベースに指定することです。言い換えれば、4Dが実行する SQL クエリのターゲットデータベースとして外部データベースを指定します。 外部データベースの作成は SQL の `CREATE DATABASE` コマンドを使用します。

### 例題

以下のコードはコンポーネントに実装されており、外部データベースに対して3つの基本的なアクションをおこないます:

- 外部データベースを作成します (存在しない場合)
- 外部データベースにデータを追加します
- 外部データベースからデータを読み込みます

外部データベースの作成:

```4d
<>MyDatabase:=Get 4D folder+"\MyDB" // (Windows) データを許可されているディレクトリに保存します
 Begin SQL
        CREATE DATABASE IF NOT EXISTS DATAFILE :[<>MyDatabase];
        USE DATABASE DATAFILE :[<>MyDatabase];
        CREATE TABLE IF NOT EXISTS KEEPIT
        (
        ID INT32 PRIMARY KEY,
        kind VARCHAR,
        name VARCHAR,
        code TEXT,
        sort_order INT32
        );

        CREATE UNIQUE INDEX id_index ON KEEPIT (ID);

        USE DATABASE SQL_INTERNAL;

 End SQL
```

外部データベースへのデータ書き込み:

```4d
 $Ptr_1:=$2 // retrieves data from the host project through pointers
 $Ptr_2:=$3
 $Ptr_3:=$4
 $Ptr_4:=$5
 $Ptr_5:=$6
 Begin SQL

        USE DATABASE DATAFILE :[<>MyDatabase];

        INSERT INTO KEEPIT
        (ID, kind, name, code, sort_order)
        VALUES
        (:[$Ptr_1], :[$Ptr_2], :[$Ptr_3], :[$Ptr_4], :[$Ptr_5]);

        USE DATABASE SQL_INTERNAL;

 End SQL
```

外部データベースからデータを読み込み:

```4d
 $Ptr_1:=$2 // accesses data of the host project through pointers
 $Ptr_2:=$3
 $Ptr_3:=$4
 $Ptr_4:=$5
 $Ptr_5:=$6

 Begin SQL

    USE DATABASE DATAFILE :[<>MyDatabase];

    SELECT ALL ID, kind, name, code, sort_order
    FROM KEEPIT
    INTO :$Ptr_1, :$Ptr_2, :$Ptr_3, :$Ptr_4, :$Ptr_5;

    USE DATABASE SQL_INTERNAL;

 End SQL
```

## リソースの使用

コンポーネントはリソースを使用することができます。 リソース管理の原則に従い、コンポーネントが .4dbase 形式の場合 (推奨されるアーキテクチャー)、Resources フォルダーは .4dbase フォルダーの中に置かれます。

これによって自動メカニズムが有効となり、コンポーネントの Resources フォルダー内で見つかった XLIFF ファイルは、 同コンポーネントによってロードされます。

In a host project containing one or more components, each component as well as the host projects has its own “resources string.” Resources are partitioned between the different projects: it is not possible to access the resources of component A from component B or the host project.

## コンポーネントのオンラインヘルプ
コンポーネントにオンラインヘルプを追加できるように、専用のメカニズムが実装されています。 The principle is the same as that provided for 4D projects:

- コンポーネントヘルプは拡張子が .htm, .html または (Windows のみ) .chm で提供されます。
- ヘルプファイルはコンポーネントのストラクチャーファイルと同階層に置かれ、ストラクチャーと同じ名前でなくてはなりません。
- このファイルは自動的にアプリケーションのヘルプメニューに、" ヘルプ: ヘルプファイル名" のタイトルでロードされます。 