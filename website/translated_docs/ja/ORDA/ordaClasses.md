---
id: ordaClasses
title: ORDA データモデルクラス
---

## Preview feature

> ORDA data model class functions are provided as a **preview feature** in 4D v18 R4: all functions you create are exposed without restrictions. Future releases will include more control over the function availability, especially from REST requests. In the next release, **by default all your data model class functions will be set to private**. You will have to specify individually each function that you want to be exposed.

## 概要

ORDA allows you to create high-level class functions above the data model. This allows you to write business-oriented code and "publish" it just like an API. Datastore, dataclasses, entity selections, and entities are all available as class objects that can contain functions.

For example, you could create a `getNextWithHigherSalary()` function in the `EmployeeEntity` class to return employees with a salary higher than the selected one. It would be as simple to call as:

```4d
$nextHigh:=ds.Employee(1).getNextWithHigherSalary()
```

Developers can not only use these functions in local datastores, but also in client/server as well as remote architectures (see the full example [below](#example-with-remote-datastore)):

```4d
 //$cityManager is the reference of a remote datastore
Form.comp.city:=$cityManager.City.getCityName(Form.comp.zipcode)
```

Thanks to this feature, the entire business logic of your 4D application can be stored as a independent layer so that it can be easily maintained or reused:

- it allows you to "hide" the overall complexity of the underlying physical structure and only expose understandable and ready-to-use functions.

- if the physical structure evolves, you simply to adapt function code and client applications will continue to call them transparently.

![](assets/en/ORDA/api.png)

各データモデルオブジェクトに関わるクラスは、4D Developer によって [あらかじめ自動的に作成](#クラスの作成) されます。

## Architecture

ORDA では、**`4D`** [クラスストア](Concepts/classes.md#クラスストア) を介して公開される **汎用クラス** と、**`cs`** [クラスストア](Concepts/classes.md#クラスストア) で公開される **ユーザークラス** が提供されています:

![](assets/en/ORDA/ClassDiagramImage.png)

ORDA データモデルクラスはすべて **`cs`** クラスストアのプロパティとして公開されます。 次の ORDA クラスが提供されています:

| クラス                         | Example name         | Instantiated by                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cs.DataStore                | cs.DataStore         | `ds` command                                                                                                                                                                                                                                                                                                                                                                      |
| cs.*DataClassName*          | cs.Employee          | `dataStore.DataClassName`, `dataStore[DataClassName]`                                                                                                                                                                                                                                                                                                                             |
| cs.*DataClassName*Entity    | cs.EmployeeEntity    | `dataClass.get()`, `dataClass.new()`, `entitySelection.first()`, `entitySelection.last()`, `entity.previous()`, `entity.next()`, `entity.first()`, `entity.last()`, `entity.clone()`                                                                                                                                                                                              |
| cs.*DataClassName*Selection | cs.EmployeeSelection | `dataClass.query()`, `entitySelection.query()`, `dataClass.all()`, `dataClass.fromCollection()`, `dataClass.newSelection()`, `entitySelection.drop()`, `entity.getSelection()`, `entitySelection.and()`, `entitySelection.minus()`, `entitySelection.or()`, `entitySelection.orderBy()`, `entitySelection.orderByFormula()`, `entitySelection.slice()`, `Create entity selection` |


> ORDA ユーザークラスは通常のクラスファイル (.4dm) としてプロジェクトの Classes サブフォルダーに保存されます [(後述参照)](#クラスファイル)。

ORDA データモデルユーザークラスのオブジェクトインスタンスは、それだの親クラスのプロパティや関数を使うことができます。 たとえば、Entity クラスのオブジェクトは [ORDA の Entity 汎用クラス](https://doc.4d.com/4Dv18R4/4D/18-R4/ORDA-Entity.201-4981870.ja.html) の関数を呼び出すことができます。

## Class Description

> **Note**: Keep in mind that ORDA data model functions are always executed on the server. Thus, calling a function generates a request to the server.

### DataStore Class

4D のデータベースは、自身の DataStore クラスを `cs` クラスストアに公開します。

- **親クラス**: 4D.DataStoreImplementation 
- **クラス名**: cs.DataStore

DataStore クラス内には、`ds` オブジェクトを介して使用する関数を作成することができます。

#### 例題

```4d
// cs.DataStore class

Class extends DataStoreImplementation

Function getDesc
  $0:="Database exposing employees and their companies"
```

この関数は次のように使えます:

```4d
$desc:=ds.getDesc() //"Database exposing..."
```

### DataClass Class

ORDA で公開されるテーブル毎に、DataClass クラスが `cs` クラスストアに公開されます。

- **親クラス**: 4D.DataClass 
- **クラス名**: cs.*DataClassName* (*DataClassName* はテーブル名です)
- **例**: cs.Employee

#### 例題

```4D
// cs.Company class


Class extends DataClass

// Returns companies which revenue is over the average
// Returns an entity selection related to the DataClass Company 

Function GetBestOnes()
    $sel:=This.query("revenues >= :1";This.all().average("revenues"));
    $0:=$sel
```

全会社データから平均以上の会社データをエンティティセレクションに抽出するには次を実行します:

```4d
    var $best : cs.CompanySelection
    $best:=ds.Company.GetBestOnes()
```

#### Example with a remote datastore

次の *City* カタログをリモートデータストアとして公開しています:

![](assets/en/ORDA/Orda_example.png)

`City クラス` は API を提供しています:

```4d
// cs.City クラス

Class extends DataClass

Function getCityName()
    var $1; $zipcode : Integer
    var $zip : 4D.Entity
    var $0 : Text

    $zipcode:=$1
    $zip:=ds.ZipCode.get($zipcode)
    $0:="" 

    If ($zip#Null)
        $0:=$zip.city.name
    End if
```

クライアントはまず、リモートデータストアのセッションを開始します:

```4d
$cityManager:=Open datastore(New object("hostname";"127.0.0.1:8111");"CityManager")
```

クライアントアプリケーションは API を使い、たとえばフォームに入力された郵便番号 (zipcode) に合致する都市を取得することができます:

```4d
Form.comp.city:=$cityManager.City.getCityName(Form.comp.zipcode)

```

### EntitySelection Class

ORDA で公開されるテーブル毎に、EntitySelection クラスが `cs` クラスストアに公開されます。

- **親クラス**: 4D.EntitySelection 
- **クラス名**: *DataClassName*Selection (*DataClassName* はテーブル名です)
- **例**: cs.EmployeeSelection

#### 例題

```4d
// cs.EmployeeSelection class


Class extends EntitySelection

//Extract from this entity selection the employees with a salary greater than the average

Function withSalaryGreaterThanAverage
    C_OBJECT($0)
    $0:=This.query("salary > :1";This.average("salary")).orderBy("salary")

```

任意の社員エンティティセレクションより、給与が平均以上の社員を取得するには:

```4d
$moreThanAvg:=ds.Company.all().employees.withSalaryGreaterThanAverage()
```

### Entity Class

ORDA で公開されるテーブル毎に、Entity クラスが `cs` クラスストアに公開されます。

- **親クラス**: 4D.Entity 
- **クラス名**: *DataClassName*Entity (*DataClassName* はテーブル名です)
- **例**: cs.CityEntity

#### 例題

```4d
// cs.CityEntity class


Class extends Entity

Function getPopulation()
    $0:=This.zips.sum("population")


Function isBigCity
C_BOOLEAN($0)
// The function getPopulation() is usable inside the class
$0:=This.getPopulation()>50000
```

次のように関数を呼び出すことができます:

```4d
var $cityManager; $city : Object

$cityManager:=Open datastore(New object("hostname";"127.0.0.1:8111");"CityManager")
$city:=$cityManager.City.getCity("Caguas")

If ($city.isBigCity())
    ALERT($city.name + " は大きな町です。")
End if
```

## Definition Rules

When creating or editing data model classes, you must pay attention to the rules described below.

- Since they are used to define automatic DataClass class names in the **cs** [class store](Concepts/classes.md#class-stores), 4D table names must be compliant in order to avoid any conflict in the **cs** namespace. 特に:
    
    - Do not give the same name to a 4D table and to a [user class name](Concepts/classes.md#class-names). If such a case occurs, the constructor of the user class becomes unusable (a warning is returned by the compiler). 
    - Do not use a reserved name for a 4D table (e.g. "DataClass").
- When defining a class, make sure the [`Class extends`](Concepts/classes.md#class-extends-classnameclass) statement matches exactly the parent class (case sensitive) name. For example, `Class extends EntitySelection` for an entity selection class.

- You cannot instantiate a data model class object with the `new()` keyword (an error is returned). You must use a regular [instantiation method](#architecture).

- You cannot override a native ORDA class method from the **`4D`** [class store](Concepts/classes.md#class-stores) with a data model user class function.

## Support in 4D projects

### クラスファイル

An ORDA data model user class is defined by adding, at the [same location as regular class files](Concepts/classes.md#class-files) (*i.e.* in the `/Sources/Classes` folder of the project folder), a .4dm file with the name of the class. For example, an entity class for the `Utilities` dataclass will be defined through a `UtilitiesEntity.4dm` file.

### Creating classes

4D automatically pre-creates empty classes in memory for each available data model object.

![](assets/en/ORDA/ORDA_Classes-3.png)

> By default, empty ORDA classes are not displayed in the Explorer. You need to show them by selecting **Show all data classes** from the Explorer's options menu: ![](assets/en/ORDA/showClass.png)

ORDA user classes have a different icon from regular classes. Empty classes are dimmed:

![](assets/en/ORDA/classORDA2.png)

To create an ORDA class file, you just need to double-click on the corresponding predefined class in the Explorer. 4D creates the class file and add the `extends` code. For example, for an Entity class:

    Class extends Entity
    

Once a class is defined, its name is no longer dimmed in the Explorer.

### Editing classes

To open a defined ORDA class in the 4D method editor, select or double-click on an ORDA class name and use **Edit...** from the contextual menu/options menu of the Explorer window (like for any class):

![](assets/en/ORDA/classORDA4.png)

For ORDA classes based upon the local datastore (ds), you can directly access the class code from the 4D Structure window:

![](assets/en/ORDA/classORDA5.png)

### メソッドエディター

In the 4D method editor, variables typed as an ORDA class automatically benefit from autocompletion features. Example with an Entity class variable:

![](assets/en/ORDA/AutoCompletionEntity.png)