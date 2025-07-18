---
id: classes
title: Clases
---

## Generalidades

El lenguaje 4D soporta el concepto de **clases**. En un lenguaje de programación, el uso de una clase permite definir el comportamiento de un objeto con propiedades y funciones asociadas.

Una vez definida una clase usuario, puede <strong x-id="1">instanciar</strong> los objetos de esta clase en cualquier parte de su código. Una vez definida una clase usuario, puede <strong x-id="1">instanciar</strong> los objetos de esta clase en cualquier parte de su código. Una clase puede [`extend`](#class-extends-classname) otra clase, y luego hereda sus [funciones](#function) y propiedades ([declaradas](#property) y [calculadas](#function-get-and-function-set)).

> El modelo de clases en 4D es similar al de las clases en JavaScript, y se basa en una cadena de prototipos.

Por ejemplo, puede crear una clase `Person` con la siguiente definición:

```4d
//Class: Person.4dm
Class constructor($firstname : Text; $lastname : Text)
 This.firstName:=$firstname
 This.lastName:=$lastname

Function get fullName() -> $fullName : Text
 $fullName:=This.firstName+" "+This.lastName

Function sayHello() -> $welcome : Text

 $welcome:="Hello "+This.fullName
```

En un método, creando una "Persona":

```4d
var $person : cs.Person //object of Person class  
var $hello : Text
$person:=cs.Person.new("John";"Doe")
// $person:{firstName: "John"; lastName: "Doe"; fullName: "John Doe"}
$hello:=$person.sayHello() //"Hello John Doe"
```

## Gestión de clases

### Definición de una clase

Una clase usuario en 4D está definida por un archivo [método ](methods.md) específico (.4dm), almacenado en la carpeta `/Project/Sources/Classes/`. El nombre del archivo es el nombre de la clase.

Al nombrar las clases, debe tener en cuenta las siguientes reglas:

- Un [nombre de clase](identifiers.md#classes) debe cumplir con [reglas de denominación de las propiedades](identifiers.md#object-properties).
- .
- No se recomienda dar el mismo nombre a una clase y a una tabla de la base, para evitar conflictos.

Por ejemplo, si quiere definir una clase llamada "Polygon", tiene que crear el siguiente archivo:

```
Project folder Project Sources Classes Polygon.4dm
```

### Borrar una clase

Para eliminar una clase existente, puede:

- en su disco, elimine el archivo de clase .4dm de la carpeta "Classes",
- en el Explorador 4D, seleccione la clase y haga clic ![](../assets/en/Users/MinussNew.png) o elija **Mover a la Papelera** en el menú contextual.

### Utilizar la interfaz 4D

Los archivos de clase se almacenan automáticamente en la ubicación adecuada cuando se crean a través de la interfaz de 4D, ya sea a través del menú **Archivo** o del Explorador.

#### Menú Archivo y barra de herramientas

Puede crear un nuevo archivo de clase para el proyecto seleccionando **Nueva > Clase...** en el menú **Archivo** de 4D Developer o en la barra de herramientas.

También puede utilizar el atajo **Ctrl+Mayús+Alt+k**.

#### Explorador

En la página **Métodos** del Explorador, las clases se agrupan en la categoría **Clases**.

Para crear una nueva clase, puede:

- seleccione la categoría **Clases** y haga clic en el botón ![](../assets/en/Users/PlussNew.png).
- seleccione **Nueva clase...** en el menú de acciones de la parte inferior de la ventana del Explorador, o en el menú contextual del grupo Clases.
  ![](../assets/en/Concepts/newClass.png)
- seleccione **Nueva > Clase...** en el menú contextual de la página de inicio del Explorador.

#### Soporte del código de clase

En las diferentes ventanas 4D (editor de código, compilador, depurador, explorador de ejecución), el código de la clase se maneja básicamente como un método proyecto con algunas especificidades:

- En el editor de código:
  - una clase no puede ser ejecutada
  - una función de clase es un bloque de código
  - **Ir a la definición** en un objeto miembro busca las declaraciones de función de clase; por ejemplo, "$o.f()" encontrará "Function f".
  - **Buscar referencias** en la declaración de función de clase busca la función utilizada como miembro de objeto; por ejemplo, "Function f" encontrará "$o.f()".
- En el explorador de Ejecución y Depurador, las funciones clase se muestran con el formato `<ClassName>` constructor o `<ClassName>.<FunctionName>`.

## Class stores

Las clases disponibles son accesibles desde sus class stores. Hay dos class stores disponibles:

- [`cs`](../commands/cs.md) para el almacén de clases de usuario
- [`4D`](../commands/4d.md) para el almacén de clases integrado

### `cs`

<!-- REF #_command_.cs.Syntax -->**cs** : Object<!-- END REF -->

<!-- REF #_command_.cs.Params -->

| Parámetros | Tipo   |                             | Descripción                                       |                  |
| ---------- | ------ | --------------------------- | ------------------------------------------------- | ---------------- |
| classStore | Object | &#8592; | Class store usuario para el proyecto o componente | <!-- END REF --> |

El comando `cs` <!-- REF #_command_.cs.Summary -->devuelve el almacén de clases de usuario para el proyecto o componente actual<!-- END REF -->. Devuelve todas las clases de usuario [definidas](#class-definition) en el proyecto o componente abierto. Por defecto, sólo las [clases ORDA](ORDA/ordaClasses.md) están disponibles.

#### Ejemplo

Quiere crear una nueva instancia de un objeto de `myClass`:

```4d
$instance:=cs.myClass.new()
```

### `4D`

<!-- REF #_command_.4D.Syntax -->**4D** : Object <!-- END REF -->

<!-- REF #_command_.4D.Params -->

| Parámetros | Tipo   |                             | Descripción    |                  |
| ---------- | ------ | --------------------------- | -------------- | ---------------- |
| classStore | Object | &#8592; | Class store 4D | <!-- END REF --> |

El comando `4D` <!-- REF #_command_.4D.Summary -->devuelve el almacén de clases para las clases 4D integradas<!-- END REF -->. Ofrece acceso a las APIs específicas como [CryptoKey](API/CryptoKeyClass.md).

#### Ejemplos

Quiere crear una nueva llave en la clase `CryptoKey`:

```4d
$key:=4D.CryptoKey.new(New object("type";"ECDSA";"curve";"prime256v1"))
```

Quiere listar las clases integradas en 4D:

```4d
 var $keys : collection
 $keys:=OB Keys(4D)
 ALERT("There are "+String($keys.length)+" built-in classes.")
```

## El objeto clase

Cuando una clase es [definida](#class-definition) en el proyecto, se carga en el entorno del lenguaje 4D. Una clase es un objeto de la [clase "Class"](API/ClassClass.md). Un objeto clase tiene las siguientes propiedades y funciones:

- cadena [`name`](API/ClassClass.md#name)
- objeto [`superclass`](API/ClassClass.md#superclass) (null si no hay)
- función [`new()`](API/ClassClass.md#new), que permite instanciar objetos de clase
- propiedad [`isShared`](API/ClassClass.md#isshared), true si la clase es [compartida](#clases-compartidas)
- propiedad [`isSingleton`](API/ClassClass.md#issingleton), verdadero si la clase define una [clase singleton](#singleton-classes).
- propiedad [`isSectionSingleton`](API/ClassClass.md#issectionsingleton), true si la clase define un [sesión singleton](#singleton-classes).
- Propiedad [`me`](API/ClassClass.md#me), que permite instanciar y acceder a [singletons](#singleton-classes).

Además, un objeto clase puede hacer referencia a un objeto [`constructor`](#class-constructor) (opcional).

Un objeto de clase en sí mismo es un [objeto compartido](shared.md) y, por tanto, se puede acceder a él desde diferentes procesos de 4D simultáneamente.

### Herencia

Si una clase hereda de otra clase (es decir, se utiliza la palabra clave [Class extends](classes.md#class-extends-classname) en su definición), la clase padre es su [`superclass`](API/ClassClass.md#superclass).

Cuando 4D no encuentra una función o una propiedad en una clase, la busca en su [`superclass`](API/ClassClass.md#superclass); si no la encuentra, 4D sigue buscando en la superclase de la superclase, y así sucesivamente hasta que no haya más superclase (todos los objetos heredan de la superclase "Object").

## Palabras clave de clase

En las definiciones de clase se pueden utilizar palabras claves específicas de 4D:

- `Function <Name>` para definir las funciones de clase de los objetos.
- `Class constructor` para inicializar nuevos objetos de la clase.
- `property` para definir propiedades estáticas de los objetos con un tipo.
- `Function get <Name>` y `Function set <Name>` para definir las propiedades calculadas de los objetos.
- `Class extends <ClassName>` para definir la herencia.
- `This` y `Super` son comandos que tienen funcionalidades especiales dentro de clases.

### `Function`

#### Sintaxis

```4d
{shared} Function <name>({$parameterName : type; ...}){->$parameterName : type}
// code
```

:::note

No hay palabra clave final para el código de una función. El lenguaje 4D detecta automáticamente el final del código de una función por la siguiente palabra clave `Function` o el final del archivo de clase.

:::

Las funciones de clase son propiedades específicas de la clase. Son objetos de la clase [4D.Function](API/FunctionClass.md). En el archivo de definición de clase, las declaraciones de función utilizan la palabra clave `Function` seguida del nombre de la función.

Si las funciones se declaran en una [clase compartida](#shared-class-constructor), puede utilizar la palabra clave `shared` con ellas para que puedan ser llamadas sin la estructura [`Use...End use`](shared.md#useend-use). Para obtener más información, consulte el párrafo [Funciones compartidas](#shared-functions) a continuación.

El nombre de la función debe ser compatible con las [reglas de nomenclatura de objetos](Concepts/identifiers.md#object-properties).

:::note

Dado que las propiedades y las funciones comparten el mismo espacio de nombres, no está permitido utilizar el mismo nombre para una propiedad y una función de la misma clase (en este caso se produce un error).

:::

:::tip

Comenzar el nombre de la función con un caracter guión bajo ("_") excluirá la función de las funcionalidades de autocompletado en el editor de código 4D. Por ejemplo, si declara `Function _myPrivateFunction` en `MyClass`, no se propondrá en el editor de código cuando digite en `"cs.MyClass. "`.

:::

Inmediatamente después del nombre de la función, los [parámetros](#parameters) de la función se pueden declarar con un nombre y un tipo de datos asignados, incluido el parámetro de retorno (opcional). Por ejemplo:

```4d
Function computeArea($width : Integer; $height : Integer)->$area : Integer
```

En una función de clase, el comando `This` se utiliza como instancia del objeto. Por ejemplo:

```4d
Function setFullname($firstname : Text; $lastname : Text)
 This.firstName:=$firstname
 This.lastName:=$lastname

Function getFullname()->$fullname : Text
 $fullname:=This.firstName+" "+Uppercase(This.lastName)
```

Para una función clase, el comando `Current method name` devuelve: `<ClassName>.<FunctionName>`, por ejemplo "MyClass.myFunction".

En el código de la aplicación, las funciones de clases se llaman como los métodos miembros de las instancias de objetos y pueden recibir [parámetros](#parameters) si los hay. Se soportan las siguientes sintaxis:

- uso del operador `()`. Por ejemplo, `myObject.methodName("hello")`
- utilización de un método miembro de la clase "4D.Function":
  - [`apply()`](API/FunctionClass.md#apply)
  - [`call()`](API/FunctionClass.md#call)

:::warning Aviso de seguridad del hilo

Si una función de clase no es hilo seguro y es llamada por un método con el atributo "Puede ejecutarse en proceso apropiativo":

- el compilador no genera ningún error (lo que es diferente en comparación con los métodos regulares),
- un error es lanzado por 4D sólo en tiempo de ejecución.

:::

#### Parámetros

Los parámetros de las funciones se declaran utilizando el nombre del parámetro y su tipo, separados por dos puntos. El nombre del parámetro debe cumplir con las [reglas de nomenclatura de las propiedades](Concepts/identifiers.md#object-properties). Múltiples parámetros (y tipos) están separados por punto y coma (;).

```4d
Function add($x; $y : Variant; $z : Integer; $xy : Object)
```

:::note

Si no se declaró el tipo, el parámetro se definirá como `Variant`.

:::

#### Valor devuelto

Se declara el parámetro de retorno (opcional) añadiendo una flecha (`->`) y la definición del parámetro de retorno después de la lista de parámetros de entrada, o dos puntos (`:`) y el tipo de parámetro de retorno únicamente. Por ejemplo:

```4d
Function add($x : Variant; $y : Integer)->$result : Integer
 $result:=$x+$y
```

También puedes declarar el parámetro de retorno añadiendo sólo `: type` y utilizar la [`expresión return`](parameters.md#return-expression) (también terminará la ejecución de la función). Por ejemplo:

```4d
Function add($x : Variant; $y : Integer): Integer
 // algo de código
 return $x+$y
```

#### Ejemplo 1

```4d
property name : Text
property height; width : Integer

// Clase: Rectangle
Class constructor($width : Integer; $height : Integer)
 This.name:="Rectangle"
 This.height:=$height
 This.width:=$width

// Definición de función
Function getArea()->$result : Integer
 $result:=(This.height)*(This.width)
```

```4d
// En un método proyecto

var $rect : cs.Rectangle
var $area : Real

$rect:=cs.Rectangle.new(50;100)  
$area:=$rect.getArea() //5000
```

#### Ejemplo 2

Este ejemplo utiliza la [`expresión return`](parameters.md#return-expression):

```4d
Function getRectArea($width : Integer; $height : Integer) : Integer
 If ($width > 0 && $height > 0)
  return $width * $height
 Else
  return 0
 End if
```

### `Class constructor`

#### Sintaxis

```4d
// Class: MyClass
{shared} {{session} singleton} Class constructor({$parameterName : type; ...})
// código
```

:::note

No hay palabra clave final para el código de función class constructor. El lenguaje 4D detecta automáticamente el final del código de una función por la siguiente palabra clave `Function` o el final del archivo de clase.

:::

Una función constructora de clase acepta [parámetros](#parameters) opcionales y puede ser utilizada para crear e inicializar objetos de la clase del usuario.

Cuando llama a la función [`new()`](API/ClassClass.md#new), el constructor de clase es llamado con los parámetros opcionalmente pasados a la función `new()`.

Sólo puede haber una función constructora en una clase (de lo contrario se devuelve un error). El comando [`Super`](../commands/super.md) permite realizar llamadas a [`superclass`](../API/ClassClass#superclass), es decir, a la clase padre de la función.

Puede crear y escribir propiedades de instancia dentro del constructor (ver ejemplo). Alternativamente, si los valores de las propiedades de instancia no dependen de los parámetros pasados al constructor, puede definirlos utilizando la palabra clave [`property`](#property).

Utilizando la palabra clave `shared` se crea una **clase compartida**, utilizada para instanciar únicamente objetos compartidos. Para obtener más información, consulte el párrafo [Clases compartidas](#shared-classes).

Utilizando la palabra clave `singleton` se crea un **singleton**, utilizado para crear una sola instancia de la sesión. Un `session singleton` crea una sola instancia por sesión. Para obtener más información, consulte el párrafo [Clases singleton](#singleton-classes).

:::note

Las [clases de entidad ORDA](../ORDA/ordaClasses.md#entity-class) también pueden beneficiarse de una función `Class constructor`. La implementación es similar a la de las clases normales pero [con algunas diferencias](../ORDA/ordaClasses.md#class-constructor-1).

:::

#### Ejemplo

```4d
// Class: MyClass
// Class constructor of MyClass
Class constructor ($name : Text ; $age : Integer)
 This.name:=$name
 This.age:=$age
```

```4d
// En un método proyecto
// Se puede instanciar un objeto
var $o : cs.MyClass
$o:=cs.MyClass.new("John";42)  
// $o = {"name":"John";"age":42}
```

### `propiedad`

#### Sintaxis

`property <propertyName>{; <propertyName2>;...}{ : <propertyType>}`

La palabra clave`property` se puede utilizar para declarar una propiedad dentro de una clase usuario. Una propiedad de clase tiene un nombre y un tipo.

La declaración de propiedades de clase mejora las sugerencias del editor de código, las funciones de tecleo predictivo y la detección de errores.

Las propiedades se declaran para nuevos objetos cuando llama a [`new()`](API/ClassClass.md#new), sin embargo, no se añaden automáticamente a los objetos (sólo se añaden cuando se les asigna un valor).

:::note

Una propiedad se añade automáticamente al objeto cuando se [inicializa en la línea de declaración](#initializing-the-property-in-the-declaration-line).

:::

Los nombres de las propiedades deben cumplir [las normas de denominación de propiedades](Concepts/identifiers.md#object-properties).

:::note

Dado que las propiedades y las funciones comparten el mismo espacio de nombres, no está permitido utilizar el mismo nombre para una propiedad y una función de la misma clase (en este caso se produce un error).

:::

El tipo de propiedad puede ser uno de los siguientes tipos soportados:

| propertyType                 | Contenido                                                                   |
| ---------------------------- | --------------------------------------------------------------------------- |
| `Text`                       | Valor texto                                                                 |
| `Date`                       | Valor fecha                                                                 |
| `Time`                       | Valor Hora                                                                  |
| `Boolean`                    | Valor booleano                                                              |
| `Integer`                    | Valor entero largo                                                          |
| `Real`                       | Valor real                                                                  |
| `Pointer`                    | Valor puntero                                                               |
| `Picture`                    | Valor imagen                                                                |
| `Blob`                       | Valeor Blob escalar                                                         |
| `Collection`                 | Valor colección                                                             |
| `Variant`                    | Valor variant                                                               |
| `Object`                     | Objeto con clase por defecto (4D.object) |
| `4D.<className>`             | Objeto del nombre de la clase 4D                                            |
| `cs.<className>`             | Objeto del nombre de la clase usuario                                       |
| `cs.<namespace>.<className>` | Objeto del componente `<namespace>` nombre de la clase                      |

Si omite el tipo en la línea de declaración, la propiedad se crea como una variante.

:::info

La palabra clave `property` sólo puede utilizarse en métodos clase y fuera de cualquier bloque `Function` o `Class constructor`.

:::

#### Inicialización de la propiedad en la línea de declaración

Al declarar una propiedad, tiene la flexibilidad de especificar su tipo de datos y proporcionar su valor en una sola declaración. La sintaxis soportada es:

`property <propertyName> { : <propertyType>} := <Propertyvalue>`

:::note

Cuando se utiliza esta sintaxis, no se pueden declarar varias propiedades en la línea de declaración.

:::

Puede omitir el tipo en la línea de declaración, en cuyo caso el tipo se deducirá cuando sea posible. Por ejemplo:

```4d
// Class: MyClass

property name : Text := "Smith"
property age : Integer := 42

property birthDate := !1988-09-29! //se deduce la fecha
property fuzzy //variant
```

Cuando inicializa una propiedad en su línea de declaración, se agrega al objeto de la clase después de su instanciación con la función [`new()`](API/ClassClass.md#new) pero antes de llamar al constructor.

Si una clase [extiende a](#class-extends-classname) otra, las propiedades de la clase padre se instancian antes que las propiedades de la clase hija.

:::note

Si inicializa una propiedad en su línea de declaración con un objeto o una colección en una [clase compartida](#clases-compartidas), el valor se transforma automáticamente en un valor compartido:

```4d
// en una clase compartida
property myCollection := ["something"]
// myCollection será una colección compartida
// equivalente a:
myCollection := New shared collection("something")
```

:::

#### Ejemplo

```4d
// Clase: MyClass

property name : Text
property age : Integer
property color : Text := "Blue"
```

En un método:

```4d
var $o : cs.MyClass
$o:=cs.MyClass.new() //$o:{"color" : "Blue"}
$o.name:="Juan" //$o:{"color" : "Azul"; "name" : "John"}
$o.age:="Smith" //error con la sintaxis de verificación
```

### `Function get` y `Function set`

#### Sintaxis

```4d
{shared} Function get <name>()->$result : type
// código
```

```4d
{shared} Function set <name>($parameterName : type)
// código
```

`Function get` y `Function set` son accesos que definen las **propiedades calculadas** en la clase. Una propiedad calculada es una propiedad nombradas con un tipo de datos que enmascara un cálculo. Cuando se accede a un valor de propiedad calculado, 4D sustituye el código del accesor correspondiente:

- cuando se lee la propiedad, `Function get` se ejecuta,
- cuando se escribe la propiedad, `Function get` se ejecuta.

Si no se accede a la propiedad, el código nunca se ejecuta.

:::note

Las [clases de entidad ORDA](../ORDA/ordaClasses.md#entity-class) se benefician de una implementación extendida de propiedades computadas con [dos funciones adicionales](../ORDA/ordaClasses.md#computed-attributes-1): `query` y `orderBy`.

:::

Las propiedades calculadas están diseñadas para manejar datos que no necesitan ser guardados en memoria. Generalmente se basan en propiedades persistentes. Por ejemplo, si un objeto de clase contiene como propiedad persistente el *precio bruto* y el *tipo de IVA*, El *precio neto* podría ser manejado por una propiedad calculada.

En el archivo de definición de la clase, las declaraciones de propiedades calculadas utilizan las palabras claves `Function get` (*getter*) y `Function set` (*setter*) seguido por el nombre de la propiedad. El nombre debe cumplir con las [reglas de nomenclatura de las propiedades](Concepts/identifiers.md#object-properties).

`Función get` devuelve un valor del tipo de la propiedad y `Function set` toma un parámetro del tipo de la propiedad. Ambos argumentos deben cumplir con los [parámetros de función](#parameters) estándar.

Cuando ambas funciones están definidas, la propiedad calculada es **read-write**. Si solo se define una `Function get`, la propiedad calculada es **de solo lectura**. En este caso, se devuelve un error si el código intenta modificar la propiedad. En este caso, se devuelve un error si el código intenta modificar la propiedad.

Si las funciones se declaran en una [clase compartida](#shared-classes), puede utilizar la palabra clave `shared` con ellas para que puedan ser llamadas sin la estructura [`Use...End use`](shared.md#useend-use). Para obtener más información, consulte el párrafo [Funciones compartidas](#shared-functions) a continuación.

El tipo de la propiedad calculada es definido por la declaración de tipo `$return` del \*getter \*. Puede ser de cualquier [tipo de propiedad válido](dt_object.md).

> Asignar *undefined* a una propiedad de objeto limpia su valor mientras se preserva su tipo. Para ello, la `Function get` es llamada primero para recuperar el tipo de valor, luego `Function set` es llamado con un valor vacío de ese tipo.

:::note

Las clases de entidad ORDA también pueden beneficiarse de una función `Class constructor`. La implementación es similar a la de las clases normales pero [con algunas diferencias](../ORDA/ordaClasses.md#class-constructor-1).

:::

#### Ejemplo 1

```4d
//Clase: Person.4dm
property firstName; lastName : Text

Class constructor($firstname : Text; $lastname : Text)
 This.firstName:=$firstname
 This.lastName:=$lastname

Function get fullName() -> $fullName : Text
 $fullName:=This.firstName+" "+This.lastName

Function set fullName( $fullName : Text )
 $p:=Position(" "; $fullName)
 This.firstName:=Substring($fullName; 1; $p-1)
 This.lastName:=Substring($fullName; $p+1)
```

```4d
//en un método proyecto
$fullName:=$person.fullName // Function get fullName() is called
$person.fullName:="John Smith" // Function set fullName() is called
```

#### Ejemplo 2

```4d
Function get fullAddress()->$result : Object

 $result:=New object

 $result.fullName:=This.fullName
 $result.address:=This.address
 $result.zipCode:=This.zipCode
 $result.city:=This.city
 $result.state:=This.state
 $result.country:=This.country
```

### `Class extends <ClassName>`

#### Sintaxis

```4d
// Class hijo
Class extends <ParentClass>
```

La palabra clave `Class extends` se utiliza en la declaración de clase para crear una clase usuario que es hijo de otra clase usuario. La clase hijo hereda todas las funciones de la clase padre.

La extensión de clase debe respetar las siguientes reglas:

- Una clase de usuario no puede extender una clase integrada (excepto las 4D.Object y [clases ORDA](../ORDA/ordaClasses.md) que se extienden por defecto para las clases de usuario).
- Una clase usuario no puede extender una clase usuario de otro proyecto o componente.
- Una clase usuario no puede extenderse a sí misma.
- No es posible extender las clases de una manera circular (es decir, "a" extiende "b" que extiende "a").
- No es posible definir una [clase usuario compartida](#shared-classes) extendida a partir de una clase usuario no compartida.

La ruptura de tal regla no es detectada por el editor de código o el intérprete, solo el compilador y `comprobar sintaxis` arrojará un error en este caso.

Una clase extendida puede llamar al constructor de su clase padre utilizando el comando [`Super`](#super).

#### Ejemplo

Este ejemplo crea una clase llamada `Square` de una clase llamada `Polygon`.

```4d
//Clase: Square

//ruta: Classes/Square.4dm

Class extends Polygon

Class constructor ($side : Integer)

Llama al constructor de la clase padre con las longitudes
 // suministradas para el ancho y alto del polígono
 Super($side;$side)
 // En las clases derivadas, Super debe ser llamado antes de 
 // utilizar 'This'
 This.name:="Square"



  Function getArea() -> $area : Integer
  $area:=This.height*This.width
```

## Comandos de función clase

Los siguientes comandos tienen características específicas cuando se utilizan dentro de las funciones clase:

### `Super`

El comando [`Super`](../commands/super.md) permite realizar llamadas a [`superclass`](../API/ClassClass#superclass), es decir, a la clase padre de la función. Sólo puede haber una función constructora en una clase (de lo contrario se devuelve un error).

Para más detalles, vea la descripción del comando [`Super`](../commands/super.md).

### `This`

El comando [`This`](../commands/this.md) devuelve una referencia al objeto procesado actualmente. En la mayoría de los casos, el valor de `This` está determinado por cómo se llama una función clase. Normalmente, `This` se refiere al objeto al que la función fue llamada, como si la función estuviera sobre el objeto.

Ejemplo:

```4d
//Clase: ob

Function f() : Integer
 return This.a+This.b
```

A continuación, puede escribir en un método:

```4d
$o:=cs.ob.new()
$o.a:=5
$o.b:=3
$val:=$o.f() //8
```

Para más detalles, vea la descripción del comando [`This`](../commands/this.md).

## Comandos de clases

Varios comandos del lenguaje 4D permiten manejar las funcionalidades de las clases.

### `OB Class`

#### `OB Class ( object ) -> Object | Null`

`OB Class` devuelve la clase del objeto pasado como parámetro.

### `OB Instance of`

#### `OB Instance of ( object ; class ) -> Boolean`

`OB Instance of` devuelve `true` si `object` pertenece a la `class` o a una de las clases heredadas y `false` de lo contrario.

## Clases compartidas

Puede crear **clases compartidas**. Una clase compartida es una clase usuario que instancia un [objeto compartido](shared.md) cuando se llama a la función [`new()`](../API/ClassClass.md#new) en la clase. Una clase compartida sólo puede crear objetos compartidos.

Las clases compartidas también admiten **funciones compartidas** que pueden llamarse sin estructuras [`Use...End use`](shared.md#useend-use).

La propiedad [`.isShared`](../API/ClassClass.md#isshared) de los objetos de la Clase permite saber si la clase está compartida.

:::info

- Una clase [que hereda](#class-extends-classname) de una clase no compartida no puede definirse como compartida.
- Las clases compartidas no están soportadas por las [clases basadas en ORDA](../ORDA/ordaClasses.md).

:::

### Creación de una clase compartida

Para crear una clase compartida, añada la palabra clave `shared` antes del [Class constructor](#class-constructor). Por ejemplo:

```4d
	//shared class: Person
shared Class constructor($firstname : Text; $lastname : Text)
 This.firstName:=$firstname
 This.lastName:=$lastname

```

```4d
//myMethod
var $person := cs.Person.new("John"; "Smith")
OB Is shared($person) // true
cs.Person.isShared //true
```

### Funciones compartidas

Si una función definida al interior de una clase compartida modifica objetos de la clase, debería llamar a la estructura [`Use...End use`](shared.md#useend-use) para proteger el acceso a los objetos compartidos. Sin embargo, para simplificar el código, puede definir la función como **compartida**, de modo que active automáticamente un `Use...End use` interno cuando se ejecute.

Para crear una función compartida, añada la palabra clave `shared` antes de la palabra clave [Function](#function) en una clase compartida. Por ejemplo:

```4d
//clase compartida Foo
shared Class constructor()
  This.variable:=1

shared Function Bar($value : Integer)
  This.variable:=$value //no es necesario llamar use/end use
```

:::note

Si se utiliza la palabra clave `shared` en una clase usuario no compartida, se ignora.

:::

## Clases Singleton

Una **clase singleton** es una clase usuario que sólo produce una única instancia. Para más información sobre el concepto de singletons, por favor consulte la [página Wikipedia sobre los singletons](https://en.wikipedia.org/wiki/Singleton_pattern).

### Tipos de Singletons

4D soporta tres tipos de singletons:

- un **singleton proceso** tiene una instancia única para el proceso en el que se instancia,
- un **singleton compartido** tiene una instancia única para todos los procesos en la máquina.
- un **singleton de sesión** es un singleton compartido pero con una instancia única para todos los procesos en la [sesión](../API/SessionClass.md). Los singletons de sesión son compartidos dentro de una sesión completa, pero varían entre sesiones. En el contexto de un cliente-servidor o una aplicación web, los singletons de sesión hacen posible crear y utilizar una instancia diferente para cada sesión, y por lo tanto para cada usuario.

Los singletons son útiles para definir los valores que necesitan estar disponibles desde cualquier parte de una aplicación, una sesión o un proceso.

:::info

Las clases Singleton no están soportadas por las [clases ORDA](../ORDA/ordaClasses.md).

:::

La siguiente tabla indica el alcance de una instancia singleton dependiendo de donde se creó:

| Singleton creado en | Alcance del proceso singleton                                                                                   | Alcance del singleton compartido | Alcance del singleton de sesión                                                |
| ------------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------- | ------------------------------------------------------------------------------ |
| **4D monopuesto**   | Proceso                                                                                                         | Aplicación                       | Aplicación o sesión Web/REST                                                   |
| **4D Server**       | Proceso                                                                                                         | Máquina 4D Server                | Sesión cliente/servidor o sesión Web/REST o sesión de procedimiento almacenado |
| **Modo remoto 4D**  | Proceso (*nota*: los singletons no están sincronizados en el proceso gemelo) | Máquina remota 4D                | Máquina remota 4D o sesión Web/REST                                            |

Una vez instanciado, existe una clase singleton (y su singleton) siempre que exista una referencia a ella en algún lugar de la aplicación que se ejecuta en la máquina.

### Crear y utilizar singletons

Se declaran clases singleton añadiendo la(s) palabra(s) clave(s) apropiada(s) antes del [`Class constructor`](#class-constructor):

- Para declarar una clase singleton (proceso), escriba `singleton Class constructor()`.
- Para declarar una clase singleton compartida, escribe `shared singleton Class constructor()`.
- Para declarar una clase singleton de sesión, escriba `session singleton Class constructor()`.

:::note

- Los singletons de sesión son automáticamente singletons compartidos (no hay necesidad de usar la palabra clave `shared` en el constructor de clases).
- Las funciones compartidas Singleton soportan [palabra clave `onHTTPGet`](../ORDA/ordaClasses.md#onhttpget-keyword).

:::

La clase singleton está instanciada en la primera llamada de la propiedad [`cs.<class>.me`](../API/ClassClass.md#me). El singleton instanciado de la clase se devuelve siempre cuando se utiliza la propiedad [`me`](../API/ClassClass.md#me).

Si necesita instanciar un singleton con parámetros, también puede llamar la función [`new()`](../API/ClassClass.md#new). En este caso, se recomienda instanciar el singleton en algún código ejecutado al inicio de la aplicación.

La propiedad [`isSingleton`](../API/ClassClass.md#issingleton) de los objetos Clase permite saber si la clase es un singleton.

La propiedad [`.isSessionSingleton`](../API/ClassClass.md#issessionsingleton) de los objetos Class permite saber si la clase es un singleton de sesión.

### Ejemplos

#### Singleton Proceso

```4d
	//class: ProcessTag
singleton Class constructor()
 This.tag:=Random
```

Para utilizar el singleton:

```4d
	//en otro proceso
var $mySingleton := cs.ProcessTag.me //Primera instanciación
	//$mySingleton.tag = 5425 por ejemplo  
...  
var $myOtherSingleton := cs.ProcessTag.me
	//$myOtherSingleton.tag = 5425

```

```4d
	//en otro proceso
var $mySingleton := cs.ProcessTag.me //Primera instanciación
	//$mySingleton.tag = 14856 por ejemplo  
...  
var $myOtherSingleton := cs.ProcessTag.me  
	//$myOtherSingleton.tag = 14856
```

#### Singleton compartido

```4d
//Class VehicleFactory

property vehicleBuilt : Integer

shared singleton Class constructor()
  This.vehicleBuilt := 0 //Número de vehículos construidos por la fábrica

shared Function buildVehicle ($type : Text) -> $vehicle : cs.Vehicle

  Case of
    : $type="car"
      $vehicle:=cs.Car.new()
    : $type="truck"
      $vehicle:=cs.Truck.new()
    : $type="sport car"
      $vehicle:=cs.SportCar.new()
    : $type="motorbike"
      $vehicle:=cs.Motorbike.new()
  Else
    $vehicle:=cs.Car.new()
  End case
  This.vehicleBuilt+=1
```

Luego puede llamar al singleton **cs.VehicleFactory** para obtener un nuevo vehículo desde cualquier lugar de la aplicación en su máquina con una sola línea:

```4d
$vehicle:=cs.VehicleFactory.me.buildVehicle("truck")
```

Dado que la función *buildVehicle()* modifica el singleton **cs.VehicleFactory** (incrementando `This.vehicleBuilt`), debe agregar la palabra clave `shared`.

#### Singleton de sesión

En una aplicación de inventario, desea implementar un inventario de artículos utilizando singletons de sesión.

```4d
//class ItemInventory

property itemList : Collection:=[]

session singleton Class constructor()

shared function addItem($item:object)
    This.itemList.push($item)
```

Al definir la clase ItemInventory como un singleton de sesión, asegúrese de que cada sesión y por lo tanto cada usuario tiene su propio inventario. Acceder al inventario del usuario es tan simple como:

```4d
//en una sesión usuario
$myList := cs.ItemInventory.me.itemList
//lista de elemento del usuario actual

```

#### Ver también

[Singletons en 4D](https://blog.4d.com/singletons-in-4d) (post del blog) <br/> [Singletons de sesión](https://blog.4d.com/introducing-session-singletons) (post del blog).
