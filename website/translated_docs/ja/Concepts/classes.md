---
id: classes
title: Classes
---


## 概要

4D ランゲージでは **クラス** の概念がサポートされています。 プログラミング言語では、クラスを利用することによって、属性やメソッドなどを持つ特定のオブジェクト種を定義することができます。

クラスが定義されていれば、そのクラスのオブジェクトをコード内で **インスタンス化** することができます。 各オブジェクトは、それ自身が属するクラスのインスタンスです。 クラスは、別のクラスを継承することで、それらの機能を受け継ぐことができます。

4D におけるクラスモデルは JavaScript のクラスに類似しており、プロトタイプチェーンに基づきます。

### Class オブジェクト

クラスとは、それ自身が "Class" クラスのオブジェクトです。 Class オブジェクトは次のプロパティやメソッドを持ちます:

- `name`: ECMAScript に準拠している必要があります
- `superclass` オブジェクト (任意。無ければ null)
- `new()` メソッド: Class オブジェクトをインスタンス化します

さらに、Class オブジェクトは次を参照できます:
- `constructor` オブジェクト (任意)
- `prototype` オブジェクト: 名前付きのメソッドオブジェクトを格納します (任意)

Class オブジェクトは共有オブジェクトです。したがって、異なる 4D プロセスから同時にアクセスすることができます。


### プロパティ検索とプロトタイプ

4D のすべてのオブジェクトは、なんらかの Class オブジェクトに内部的にリンクしています。 あるプロパティがオブジェクト内で見つからない場合、4D はそのクラスのプロトタイプオブジェクト内を検索します。見つからない場合、4D はそのクラスのスーパークラスのプロトタイプオブジェクト内を探します。これは、スーパークラスが存在しなくなるまで続きます。

すべてのオブジェクトは、継承ツリーの頂点である "Object" クラスを継承します。

```4d
  // クラス: Polygon
Class constructor
C_LONGINT($1;$2)
This.area:=$1*$2

 //C_OBJECT($poly)
C_BOOLEAN($instance)
$poly:=cs.Polygon.new(4;3)

$instance:=OB Instance of($poly;cs.Polygon)  
 // true
$instance:=OB Instance of($poly;4D.Object)
 // true
```

オブジェクトのプロパティを列挙する際には、当該クラスのプロトタイプは列挙されません。 したがって、`For each` ステートメントや `JSON Stringify` コマンドは、クラスプロトタイプオブジェクトのプロパティを返しません。 クラスのプロトタイプオブジェクトプロパティは、内部的な隠れプロパティです。

### クラス定義

ユーザークラスファイルによって、特定のオブジェクト種のひな形を定義します。`new()` クラスメンバーメソッドを呼び出すことで、このひな形に基づいたオブジェクトをインスタンス化することができます。 クラスファイル内では、専用の [クラスキーワード](#クラスキーワード) や [クラスコマンド](#クラスコマンド) を使用します。

たとえば:

```4d  
// クラス: Person.4dm
Class constructor
  C_TEXT($1) // 名前
  C_TEXT($2) // 名字
  This.firstName:=$1
  This.lastName:=$2
```

この "Person" のインスタンスをメソッド内で作成するには、以下のように書けます:

```
C_OBJECT($o)
$o:=cs.Person.new("John";"Doe")  
// $o: {firstName: "John";lastName: "Doe" }
```

空のクラスファイルを作成し、空のオブジェクトをインスタンス化することも可能です。 たとえば、次の `Empty.4dm` クラスファイルを作成します:

```4d  
// Empty.4dm クラスファイル
// 空です
```

メソッドでは次のように書けます:


```4d
$o:=cs.Empty.new()  
// $o : {}
$cName:=OB Class($o).name // "Empty"
```


## クラスストア

定義されたクラスには、クラスストアよりアクセスすることができます。 クラスストアには次のものが存在します:

- ビルトイン 4Dクラス専用のクラスストア:  `4D` コマンドによって返されます。
- 開かれている各データベースおよびコンポーネントのクラスストア:  `cs` コマンドによって返されます。 "ユーザークラス" ともいいます。

たとえば、`cs.myClass.new()` ステートメント (`cs` は *クラスストア (classstore)* を意味します) を使って myClass のオブジェクトインスタンスを新規作成できます。


## ユーザークラス

### クラスファイル

4D においてユーザークラスとは、`/Project/Sources/Classes/` フォルダーに保存された専用のメソッドファイル (.4dm) によって定義されます。 ファイル名がクラス名になります。

たとえば、"Polygon" という名前のクラスを定義するには、次のファイルを作成する必要があります:

- Project フォルダー
    + Project
        * Sources
            - Classes
                + Polygon.4dm

### クラス名

クラスを命名する際には、次のルールに留意してください:

- ECMAScript に準拠した名前であること
- 大文字と小文字が区別されること
- 競合防止のため、データベースのテーブルと同じ名前のクラスを作成するのは推奨されないこと


### 4D 開発インターフェース

**ファイル** メニューまたはエクスプローラーなど、4D 開発インターフェースを介してクラスを作成した場合には、クラスファイルは自動的に適切な場所に保存されます。

#### ファイルメニューとツールバー

4D 開発の **ファイル** メニューまたはツールバーより **新規 > クラス...** を選択することで、開いているプロジェクトにクラスファイルを新規作成することができます。

**Ctrl+Shift+Alt+k** ショートカットも使用できます。

#### エクスプローラー

エクスプローラーの **メソッド** ページにおいて、クラスは **クラス** カテゴリに分類されています。

クラスを新規作成するには次の方法があります:

- **クラス** カテゴリを選択し、![](assets/en/Users/PlussNew.png) ボタンをクリックします。
- エクスプローラーウィンドウの下部にあるアクションメニュー、またはクラスグループのコンテキストメニューから **新規クラス...** を選択します。 ![](assets/en/Concepts/newClass.png)
- エクスプローラーのホームページのコンテキストメニューより **新規 > クラス...** を選択します。

#### クラスのコードサポート

各種 4D 開発ウィンドウ (コードエディター、コンパイラー、デバッガー、ランタイムエクスプローラー) において、クラスコードは "特殊なプロジェクトメソッド" のように扱われます:

- コードエディター:
    - クラスは実行できません
    - クラスメソッドはコードのブロックです
    - オブジェクトメンバーに対する **定義に移動** 操作はクラスの Function 宣言を探します。例: "$o.f()" の場合、"Function f" を見つけます。
    - クラスのメソッド宣言に対する **参照箇所を検索** 操作は、そのメソッドがオブジェクトメンバーとして使われている箇所を探します。例: "Function f" の場合 "$o.f()" を見つけます。
- ランタイムエクスプローラーおよびデバッガーにおいて、クラスメソッドは \<ClassName> コンストラクターまたは \<ClassName>.\<FunctionName> 形式で表示されます。


### クラスの削除

既存のクラスを削除するには:

- ディスク上で "Classes" フォルダーより .4dm クラスファイルを削除します。
- エクスプローラーでは、クラスを選択した状態で ![](assets/en/Users/MinussNew.png) をクリックするか、コンテキストメニューより **移動 > ゴミ箱** を選択します。


## クラスキーワード

クラス定義内では、専用の 4Dキーワードが使用できます:

- `Function <Name>`: オブジェクトのメンバーメソッドを定義します。
- `Class constructor`: オブジェクトのプロパティを定義します (プロトタイプ定義)。
- `Class extends <ClassName>`: 継承を定義します。


### Function

#### シンタックス

```js
Function <name>
// コード
```

クラス関数とは、当該クラスのプロトタイプオブジェクトのプロパティです。 また、クラス関数は "Function" クラスのオブジェクトでもあります。

クラス定義ファイルでは、`Function` キーワードと関数名を使用して宣言をおこないます。 このとき、メンバーメソッド名は ECMAScript に準拠している必要があります。

クラスメソッド内でオブジェクトインスタンスを参照するには `This` を使います。 たとえば:

```4d  
Function getFullName
  C_TEXT($0)
  $0:=This.firstName+" "+Uppercase(This.lastName)

Function getAge
  C_LONGINT($0)
  $0:=(Current date-This.birthdate)/365.25
```

クラスメソッドの場合には、`Current method name` コマンドは次を返します: "*\<ClassName>.\<FunctionName>*" (例: "MyClass.myMethod")。

アプリケーションのコード内では、クラスメソッドはオブジェクトインスタンスのメンバーメソッドとして呼び出され、引数を受け取ることができます。 次のシンタックスがサポートされています:

- `()` 演算子の使用 For example `myObject.methodName("hello")`.
- use of a "Function" class member methods
    - `apply()`
    - `call()`


> **Thread-safety warning:** If a class function is not thread-safe and called by a method with the "Can be run in preemptive process" attribute:  
> - the compiler does not generate any error (which is different compared to regular methods), - an error is thrown by 4D only at runtime.


#### Example

```4d
// Class: Rectangle
Class Constructor
    C_LONGINT($1;$2)
    This.name:="Rectangle"
    This.height:=$1
    This.width:=$2

// Function definition
Function getArea
    C_LONGINT($0)
    $0:=(This.height)*(This.width)

```

```4d
// In a project method
C_OBJECT($o)  
C_REAL($area)

$o:=cs.Rectangle.new()  
$area:=$o.getArea(50;100) //5000
```


### Class constructor

#### Syntax

```js
// Class: MyClass
Class Constructor
// code
```

A class constructor function, which can accept parameters, can be used to define a user class.

In that case, when you call the `new()` class member method, the class constructor is called with the parameters optionally passed to the `new()` function.

For a class constructor function, the `Current method name` command returns: "*\<ClassName>.constructor*", for example "MyClass.constructor".


#### Example:

```4d
// Class: MyClass
// Class constructor of MyClass
Class Constructor
C_TEXT($1)
This.name:=$1
```

```4d
// In a project method
// You can instantiate an object
C_OBJECT($o)
$o:=cs.MyClass.new("HelloWorld")  
// $o = {"name":"HelloWorld"}
```




### Class extends \<ClassName>

#### Syntax

```js
// Class: ChildClass
Class extends <ParentClass>
```

The `Class extends` keyword is used in class declaration to create a user class which is a child of another user class. The child class inherits all functions of the parent class.

Class extension must respect the following rules:

- A user class cannot extend a built-in class (except 4D.Object which is extended by default for user classes)
- A user class cannot extend a user class from another project or component.
- A user class cannot extend itself.
- It is not possible to extend classes in a circular way (i.e. "a" extends "b" that extends "a").

Breaking such a rule is not detected by the code editor or the interpreter, only the compiler and `check syntax` will throw an error in this case.

An extended class can call the constructor of its parent class using the [`Super`](#super) command.

#### Example

This example creates a class called `Square` from a class called `Polygon`.

```4d
  //Class: Square
  //path: Classes/Square.4dm

 Class extends Polygon

 Class constructor
 C_LONGINT($1)

  // It calls the parent class's constructor with lengths
  // provided for the Polygon's width and height
Super($1;$1)
  // In derived classes, Super must be called before you
  // can use 'This'
 This.name:="Square"

Function getArea
C_LONGINT($0)
$0:=This.height*This.width
```

### Super

#### Super {( param{;...;paramN} )} {-> Object}

| Parameter | Type   |    | Description                                    |
| --------- | ------ | -- | ---------------------------------------------- |
| param     | mixed  | -> | Parameter(s) to pass to the parent constructor |
| Result    | object | <- | Object's parent                                |

The `Super` keyword allows calls to the `superclass`, i.e. the parent class.

`Super` serves two different purposes:

- inside a [constructor code](#class-constructor), `Super` is a command that allows to call the constructor of the superclass. コンストラクター内で使用する際には、`Super` コマンドは単独で使用され、また `This` キーワードよりも先に使用される必要があります。
    - 継承ツリーにおいて、すべてのクラスコンストラクターが正しく呼び出されていない場合には、エラー -10748 が生成されます。 呼び出しが有効であることを確認するのは、開発者の役目となります。
    - スーパークラスがコンストラクトされるより先に、`This` コマンドを使った場合には、エラー -10743 が生成されます。
    - `Super` を、オブジェクトのスコープ外で呼び出した場合、または、すでにスーパークラスがコンストラクトされたオブジェクトを対象に呼び出した場合には、エラー -10746 が生成されます。

```4d
  // myClass コンストラクター
 C_TEXT($1;$2)
 Super($1) // テキスト型引数をスーパークラスコンストラクターに渡します
 This.param:=$2 // 2番目の引数を使用します
```

- [クラスメンバーメソッド](#function) 内において、`Super` はスーパークラスのプロトタイプを指し、スーパークラス階層のメンバーメソッドを呼び出すために使用します。

```4d
 Super.doSomething(42) // スーパークラスにて宣言されている
    // "doSomething" メンバーメソッドを呼び出します
```

#### 例題 1

クラスコンストレクター内で `Super` を使う例です。 `Rectangle` と `Square` の共通要素がコンストラクター内で重複しないよう、このコマンドを呼び出します。

```4d
  // クラス: Rectangle

 Class constructor
 C_LONGINT($1;$2)
 This.name:="Rectangle"
 This.height:=$1
 This.width:=$2

 Function sayName
 ALERT("Hi, I am a "+This.name+".")

 Function getArea
 C_LONGINT($0)
 $0:=This.height*This.width
```

```4d
  // クラス: Square

 Class extends Rectangle

 Class constructor
 C_LONGINT($1)

  // 親クラスのコンストラクターを呼び出します
  // 長方形の高さ・幅パラメーターに正方形の一辺の長さを引数として渡します
 Super($1;$1)

  // 派生クラスにおいては、'This' を使用するより先に
  // Super を呼び出しておく必要があります
 This.name:="Square"
```

#### 例題 2

クラスメンバーメソッド内で `Super` を使う例です。 メンバーメソッドを持つ `Rectangle` クラスを作成します:

```4d
  // クラス: Rectangle

 Function nbSides
 C_TEXT($0)
 $0:="I have 4 sides"
```

`Square` クラスには、スーパークラスメソッドを呼び出すメンバーメソッドを定義します:

```4d
  // クラス: Square

 Class extends Rectangle

 Function description
 C_TEXT($0)
 $0:=Super.nbSides()+" which are all equal"
```

すると、プロジェクトメソッド内には次のように書けます:

```4d
 C_OBJECT($square)
 C_TEXT($message)
 $square:=cs.Square.new()
 $message:=$square.description() //I have 4 sides which are all equal
```

### This

#### This -> Object

| 引数  | 型      |    | 説明         |
| --- | ------ | -- | ---------- |
| 戻り値 | object | <- | カレントオブジェクト |

`This` キーワードは、現在処理中のオブジェクトへの参照を返します。 `This` は、4Dにおいて [様々なコンテキスト](https://doc.4d.com/4Dv18/4D/18/This.301-4504875.ja.html) で使用することができます。

`This` の値は、呼ばれ方によって決まります。 It can't be set by assignment during execution, and it may be different each time the function is called.

When a formula is called as a member method of an object, its `This` is set to the object the method is called on. For example:

```4d
$o:=New object("prop";42;"f";Formula(This.prop))
$val:=$o.f() //42
```

When a [class constructor](#class-constructor) function is used (with the `new()` keyword), its `This` is bound to the new object being constructed.

```4d
  //Class: ob

Class Constructor  
    // Create properties on This as
    // desired by assigning to them
    This.a:=42
```

```4d
    // in a 4D method  
$o:=cs.ob.new()
$val:=$o.a //42
```

> When calling the superclass constructor in a constructor using the [Super](#super) keyword, keep in mind that `This` must not be called before the superclass constructor, otherwise an error is generated. [こちらの例題](#例題-1) を参照ください。


基本的に、`This` はメソッドの呼び出し元のオブジェクトを指します。

```4d
 // クラス: ob

 Function f
    $0:=This.a+This.b
```

この場合、プロジェクトメソッドには次のように書けます:

```4d
$o:=cs.ob.new()
$o.a:=5
$o.b:=3
$val:=$o.f() //8
```
この例では、変数 $o に代入されたオブジェクトは *f* プロパティを持たないため、これをクラスより継承します。 Since *f* is called as a method of $o, its `This` refers to $o.


## Class commands

Several commands of the 4D language allows you to handle class features.


### OB Class

#### OB Class ( object ) -> Object | Null

`OB Class` returns the class of the object passed in parameter.


### OB Instance of

#### OB Instance of ( object ; class ) -> Boolean

`OB Instance of` returns `true` if `object` belongs to `class` or to one of its inherited classes, and `false` otherwise.
