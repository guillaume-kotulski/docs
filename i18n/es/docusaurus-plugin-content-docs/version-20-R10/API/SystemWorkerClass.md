---
id: SystemWorkerClass
title: SystemWorker
---

Los System workers permiten que el código 4D llame a cualquier proceso externo (un comando shell, PHP, etc.) en la misma máquina. Los trabajadores del sistema se llaman de forma asíncrona. Mediante el uso de retrollamadas, 4D hace posible la comunicación en ambos sentidos.

La clase `SystemWorker` está disponible en el class store `4D`.

### Ejemplo

```4d
    // Ejemplo Windows para acceder a la información de ipconfig
var $myWinWorker : 4D.SystemWorker
var $ipConfig : Text
$myWinWorker:= 4D.SystemWorker.new("ipconfig")
$ipConfig:=$myWinWorker.wait(1).response //timeout 1 segundo

    // ejemplo macOS para cambiar los permisos de un archivo en macOS
    // chmod es el comando macOS utilizado para modificar el acceso a los archivos
var $myMacWorker : 4D.SystemWorker
$myMacWorker:= 4D.SystemWorker.new("chmod +x /folder/myfile.sh")

```

### Resumen

|                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [<!-- INCLUDE #4D.SystemWorker.new().Syntax -->](#4dsystemworkernew)<br/><!-- INCLUDE #4D.SystemWorker.new().Summary -->                          |
| [<!-- INCLUDE #SystemWorkerClass.closeInput().Syntax -->](#closeinput)<br/><!-- INCLUDE #SystemWorkerClass.closeInput().Summary -->               |
| [<!-- INCLUDE #SystemWorkerClass.commandLine.Syntax -->](#commandline)<br/><!-- INCLUDE #SystemWorkerClass.commandLine.Summary -->                |
| [<!-- INCLUDE #SystemWorkerClass.currentDirectory.Syntax -->](#currentdirectory)<br/><!-- INCLUDE #SystemWorkerClass.currentDirectory.Summary --> |
| [<!-- INCLUDE #SystemWorkerClass.dataType.Syntax -->](#datatype)<br/><!-- INCLUDE #SystemWorkerClass.dataType.Summary -->                         |
| [<!-- INCLUDE #SystemWorkerClass.encoding.Syntax -->](#encoding)<br/><!-- INCLUDE #SystemWorkerClass.encoding.Summary -->                         |
| [<!-- INCLUDE #SystemWorkerClass.errors.Syntax -->](#errors)<br/><!-- INCLUDE #SystemWorkerClass.errors.Summary -->                               |
| [<!-- INCLUDE #SystemWorkerClass.exitCode.Syntax -->](#exitcode)<br/><!-- INCLUDE #SystemWorkerClass.exitCode.Summary -->                         |
| [<!-- INCLUDE #SystemWorkerClass.hideWindow.Syntax -->](#hidewindow)<br/><!-- INCLUDE #SystemWorkerClass.hideWindow.Summary -->                   |
| [<!-- INCLUDE #SystemWorkerClass.pid.Syntax -->](#pid)<br/><!-- INCLUDE #SystemWorkerClass.pid.Summary -->                                        |
| [<!-- INCLUDE #SystemWorkerClass.postMessage().Syntax -->](#postmessage)<br/><!-- INCLUDE #SystemWorkerClass.postMessage().Summary -->            |
| [<!-- INCLUDE #SystemWorkerClass.response.Syntax -->](#response)<br/><!-- INCLUDE #SystemWorkerClass.response.Summary -->                         |
| [<!-- INCLUDE #SystemWorkerClass.responseError.Syntax -->](#responseerror)<br/><!-- INCLUDE #SystemWorkerClass.responseError.Summary -->          |
| [<!-- INCLUDE #SystemWorkerClass.terminate().Syntax -->](#terminate)<br/><!-- INCLUDE #SystemWorkerClass.terminate().Summary -->                  |
| [<!-- INCLUDE #SystemWorkerClass.terminated.Syntax -->](#terminated)<br/><!-- INCLUDE #SystemWorkerClass.terminated.Summary -->                   |
| [<!-- INCLUDE #SystemWorkerClass.timeout.Syntax -->](#timeout)<br/><!-- INCLUDE #SystemWorkerClass.timeout.Summary -->                            |
| [<!-- INCLUDE #SystemWorkerClass.wait().Syntax -->](#wait)<br/><!-- INCLUDE #SystemWorkerClass.wait().Summary -->                                 |

<!-- REF 4D.SystemWorker.new().Desc -->

## 4D.SystemWorker.new()

<details><summary>Historia</summary>

| Lanzamiento | Modificaciones |
| ----------- | -------------- |
| 19 R4       | Añadidos       |

</details>

<!-- REF #4D.SystemWorker.new().Syntax -->**4D.SystemWorker.new** ( *commandLine* : Text { ; options : Object } ) : 4D.SystemWorker<!-- END REF -->

<!-- REF #4D.SystemWorker.new().Params -->

| Parámetros  | Tipo                            |                             | Descripción                                                          |
| ----------- | ------------------------------- | :-------------------------: | -------------------------------------------------------------------- |
| commandLine | Text                            |              ->             | Línea de comando a ejecutar                                          |
| options     | Object                          |              ->             | Parámetros worker                                                    |
| resultado   | 4D.SystemWorker | <- | Nuevo System worker asíncrono o null si el proceso no se ha iniciado |

<!-- END REF -->

#### Descripción

La función `4D.SystemWorker.new()` <!-- REF #4D.SystemWorker.new().Summary -->crea y devuelve un objeto `4D.SystemWorker` que ejecutará el *commandLine* que pasó como parámetro para lanzar un proceso externo<!-- END REF -->.

El objeto system worker devuelto puede utilizarse para enviar mensajes al worker y obtener los resultados del worker.

Si se produce un error durante la creación del objeto proxy, la función devuelve un objeto `null` y se lanza un error.

En el parámetro *commandLine*, pase la ruta completa del archivo de la aplicación a ejecutar (sintaxis posix), así como los argumentos necesarios, si es el caso. Si sólo pasa que el nombre de la aplicación, 4D utilizará la variable de entorno `PATH` para localizar el ejecutable.

**Atención:** esta función sólo puede lanzar aplicaciones ejecutables; no puede ejecutar las instrucciones que formen parte del shell (intérprete de comandos). Por ejemplo, en Windows no es posible utilizar este comando para ejecutar la instrucción `dir`.

#### Objeto *options*

En el parámetro *options*, pase un objeto que puede contener las siguientes propiedades:

| Propiedad        | Tipo    | Por defecto | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------- | ------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| onResponse       | Formula | indefinido  | Retrollamada para los mensajes del system worker. Esta retrollamada se llama una vez que se recibe la respuesta completa. Recibe dos objetos como parámetros (ver más abajo)                                                                                                                                                                                                       |
| onData           | Formula | indefinido  | Retrollamada para los datos del system worker. Esta retrollamada se llama cada vez que el system worker recibe los datos. Recibe dos objetos como parámetros (ver más abajo)                                                                                                                                                                                                       |
| onDataError      | Formula | indefinido  | Callback para los errores del proceso externo (*stderr* del proceso externo). Recibe dos objetos como parámetros (ver más abajo)                                                                                                                                                                                                                                                |
| onError          | Formula | indefinido  | Retrollamada para los errores de ejecución, devueltos por el system worker en caso de condiciones de ejecución inusuales (errores del sistema). Recibe dos objetos como parámetros (ver más abajo)                                                                                                                                                                              |
| onTerminate      | Formula | indefinido  | Retrollamada cuando el proceso externo se termina. Recibe dos objetos como parámetros (ver más abajo)                                                                                                                                                                                                                                                                                              |
| timeout          | Number  | indefinido  | Tiempo en segundos antes de que el proceso sea eliminado si aún está activo                                                                                                                                                                                                                                                                                                                                                           |
| dataType         | Text    | "text"      | Tipo de contenido del cuerpo de la respuesta. Valores posibles: "text" (por defecto), "blob".                                                                                                                                                                                                                                                                      |
| encoding         | Text    | "UTF-8"     | Sólo si `dataType="text"`. Codificación del contenido del cuerpo de la respuesta. Para la lista de valores disponibles, consulte la descripción del comando [`CONVERT FROM TEXT`](../commands-legacy/convert-from-text.md)                                                                                                                                                                            |
| variables        | Object  |             | Define las variables de entorno personalizadas para el system worker. Sintaxis: `variables.clave=valor`, donde `key` es el nombre de la variable y `value` su valor. Los valores se convierten en cadenas de caracters cuando es posible. El valor no puede contener un '='. Si no se define, el system worker hereda del entorno 4D. |
| currentDirectory | Folder  |             | Directorio de trabajo en el que se ejecuta el proceso                                                                                                                                                                                                                                                                                                                                                                                 |
| hideWindow       | Boolean | true        | (Windows) Ocultar la ventana de la aplicación (si es posible) o la consola Windows                                                                                                                                                                                                                                                                                                              |

Todas las funciones de retrollamada reciben dos parámetros objeto. Su contenido depende de la retrollamada:

| Parámetros                   | Tipo        | *onResponse* | *onData*        | *onDataError*  | *onError*    | *onTerminate* |
| ---------------------------- | ----------- | ------------ | --------------- | -------------- | ------------ | ------------- |
| $param1                      | Object      | SystemWorker | SystemWorker    | SystemWorker   | SystemWorker | SystemWorker  |
| $param2.type | Text        | "response"   | "data"          | "error"        | "error"      | "termination" |
| $param2.data | Text o Blob |              | datos recibidos | datos de error |              |               |

Esta es la secuencia de llamadas de retorno:

1. `onData` y `onDataError` se ejecutan una o varias veces
2. si se llama, `onError` se ejecuta una vez (detiene el procesamiento del system worker)
3. si no se ha producido ningún error, `onResponse` se ejecuta una vez
4. `onTerminate` se ejecuta siempre una vez

:::info

Para que las funciones de retrollamada se llamen cuando no utilice [`wait()`](#wait) (llamada asíncrona), el proceso debe ser un [worker](../Develop/processes.md#worker-processes) creado con [`CALL WORKER`](../commands-legacy/call-worker.md), NO [`New process`](../commands-legacy/new-process.md).

:::

#### Valor devuelto

La función devuelve un objeto system worker sobre el que se pueden llamar las funciones y las propiedades de la clase SystemWorker.

#### Ejemplos en Windows

1. Para abrir el Bloc de notas y abrir un documento específico:

```4d
var $sw : 4D.SystemWorker
var $options : Object
$options:=New object
$options.hideWindow:= False

$sw:=4D.SystemWorker.new ("C:\\WINDOWS\\notepad.exe C:\\Docs\\new folder\\res.txt";$options)
```

2. Ejecutar npm install en la consola:

```4d
var $folder : 4D.Folder
var $options : Object
var $worker : 4D.SystemWorker

$folder:=Folder(fk database folder)
$options:=New object
$options.currentDirectory:=$folder
$options.hideWindow:=False

$worker:=4D.SystemWorker.new("cmd /c npm install";$options)

```

3. Para lanzar la aplicación Microsoft® Word® y abrir un documento específico:

```4d
$mydoc:="C:\\Program Files\\Microsoft Office\\Office15\\WINWORD.EXE C:\\Tempo\\output.txt"
var $sw : 4D.SystemWorker
$sw:=4D.SystemWorker.new($mydoc)
```

4. Para lanzar un comando con el directorio actual y publicar un mensaje:

```4d
var $param : Object
var $sys : 4D.SystemWorker

$param:=New object
$param.currentDirectory:=Folder(fk database folder)
$sys:=4D.SystemWorker.new("git commit -F -";$param)
$sys.postMessage("This is a postMessage")
$sys.closeInput()
```

5. Para permitir al usuario abrir un documento externo en Windows:

```4d
$docname:=Select document("";"*.*";"Choose the file to open";0)
If(OK=1)
 var $sw : 4D.SystemWorker
 $sw:=4D.SystemWorker.new("cmd.exe /C start \"\" \""+$docname+"\"")
End if
```

#### Ejemplos en macOS

1. Modificar un archivo texto (`cat` es el comando macOS utilizado para editar archivos). En este ejemplo, se pasa la ruta de acceso completa del comando:

```4d

var $sw : 4D.SystemWorker
$sw:=4D.SystemWorker.new("/bin/cat /folder/myfile.txt")
$sw.wait() /ejecución síncrona

```

2. Para lanzar una aplicación "gráfica" independiente, es preferible utilizar el comando sistema `open` (en este caso, el código tiene el mismo efecto que hacer doble clic en la aplicación):

```4d
var $sw : 4D.SystemWorker
$sw:=4D.SystemWorker.new ("open /Applications/Calculator.app")
```

3. Para obtener el contenido de la carpeta "Users" (ls -l es el equivalente en macOS del comando dir en DOS).

```4d
var $systemworker : 4D.SystemWorker
var $output : Text
var $errors : Collection

$systemworker:=4D.SystemWorker.new("/bin/ls -l /Users ")
$systemworker.wait(5)
$output:=$systemworker.response
$error:=$systemworker.errors

```

4. El mismo comando que el anterior, pero utilizando un ejemplo de clase usuario "Params" para mostrar cómo manejar las funciones de retrollamada:

```4d

var $systemworker : 4D.SystemWorker
$systemworker:=4D.SystemWorker.new("/bin/ls -l /Users ";cs.Params.new())


// "Params" class

Class constructor
 This.dataType:="text"
    This.data:=""
    This.dataError:=""

Function onResponse($systemWorker : Object)
     This._createFile("onResponse"; $systemWorker.response)

Function onData($systemWorker : Object; $info : Object)
     This.data+=$info.data
     This._createFile("onData";this.data)

Function onDataError($systemWorker : Object; $info : Object)
     This.dataError+=$info.data
     This._createFile("onDataError";this.dataError)

Function onTerminate($systemWorker : Object)
     var $textBody : Text
     $textBody:="Response: "+$systemWorker.response
     $textBody+="ResponseError: "+$systemWorker.responseError
     This._createFile("onTerminate"; $textBody)

Function _createFile($title : Text; $textBody : Text)
     TEXT TO DOCUMENT(Get 4D folder(Current resources folder)+$title+".txt"; $textBody)

```

<!-- END REF -->

<!-- REF SystemWorkerClass.closeInput().Desc -->

## .closeInput()

<details><summary>Historia</summary>

| Lanzamiento | Modificaciones |
| ----------- | -------------- |
| 19 R4       | Añadidos       |

</details>

<!-- REF #SystemWorkerClass.closeInput().Syntax -->**.closeInput**()<!-- END REF -->

<!-- REF #SystemWorkerClass.closeInput().Params -->

| Parámetros | Tipo |     | Descripción                  |
| ---------- | ---- | :-: | ---------------------------- |
|            |      |     | No requiere ningún parámetro |

<!-- END REF -->

#### Descripción

La función `.closeInput()` <!-- REF #SystemWorkerClass.closeInput().Summary -->cierra el flujo de entrada (*stdin*) del proceso externo<!-- END REF -->.

Cuando el ejecutable espera a recibir todos los datos a través de `postMessage()`, `.closeInput()` es útil para indicar al ejecutable que el envío de datos ha terminado y que puede continuar.

#### Ejemplo

```4D
// Crear algunos datos para gzip
var $input;$output : Blob
var $gzip : Texto
TEXT TO BLOB("¡Hola, Mundo!";$input)
$gzip:="\"C:\\Program Files (x86)\\GnuWin32\bin\gzip.exe\" "

// Crear un system worker asíncrono
var $worker : 4D.SystemWorker
$worker:= 4D.SystemWorker.new($gzip;New object("dataType"; "blob"))

// Envía el archivo comprimido en stdin.
$worker.postMessage($input)
// Observe que llamamos a closeInput() para indicar que hemos terminado.
// gzip (y la mayoría de los programas que esperan datos de stdin) esperarán más datos hasta que se cierre explícitamente la entrada.
$worker.closeInput()
$worker.wait()

$output:=$worker.response

```

<!-- END REF -->

<!-- REF SystemWorkerClass.commandLine.Desc -->

## .commandLine

<!-- REF #SystemWorkerClass.commandLine.Syntax -->**.commandLine** : Text<!-- END REF -->

#### Descripción

La propiedad `.commandLine` <!-- REF #SystemWorkerClass.commandLine.Summary -->contiene la línea de comandos pasada como parámetro a la función [`new()`](#4dsystemworkernew)<!-- END REF -->.

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.currentDirectory.Desc -->

## .currentDirectory

<!-- REF #SystemWorkerClass.currentDirectory.Syntax -->**.currentDirectory** : 4D.Folder<!-- END REF -->

#### Descripción

La propiedad `.currentDirectory` <!-- REF #SystemWorkerClass.currentDirectory.Summary -->contiene el directorio de trabajo en el que se ejecuta el proceso externo<!-- END REF -->.

<!-- END REF -->

<!-- REF SystemWorkerClass.dataType.Desc -->

## .dataType

<!-- REF #SystemWorkerClass.dataType.Syntax -->**.dataType** : Text<!-- END REF -->

#### Descripción

La propiedad `.dataType` <!-- REF #SystemWorkerClass.dataType.Summary -->contiene el tipo de contenido del cuerpo de la respuesta<!-- END REF -->. Valores posibles: "text" o "blob".

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.encoding.Desc -->

## .encoding

<!-- REF #SystemWorkerClass.encoding.Syntax -->**.encoding** : Text<!-- END REF -->

#### Descripción

La propiedad `.encoding` <!-- REF #SystemWorkerClass.encoding.Summary -->contiene la codificación del contenido del cuerpo de la respuesta<!-- END REF -->. Esta propiedad sólo está disponible si el [`dataType`](#datatype) es "text".

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.errors.Desc -->

## .errors

<!-- REF #SystemWorkerClass.errors.Syntax -->**.errors** : Collection<!-- END REF -->

#### Descripción

La propiedad `.errors` <!-- REF #SystemWorkerClass.errors.Summary -->contiene una colección de errores 4D en caso de error(es) de ejecución si los hubiera<!-- END REF -->.

Cada elemento de la colección es un objeto con las siguientes propiedades:

| Propiedad                                                                                  | Tipo   | Descripción                                           |
| ------------------------------------------------------------------------------------------ | ------ | ----------------------------------------------------- |
| [].errorCode           | number | Código de error 4D                                    |
| [].message             | text   | Descripción del error 4D                              |
| [ ].componentSignature | text   | Firma del componente interno que ha devuelto el error |

Si no se ha producido ningún error, `.errors` es indefinido.

<!-- END REF -->

<!-- REF SystemWorkerClass.exitCode.Desc -->

## .exitCode

<!-- REF #SystemWorkerClass.exitCode.Syntax -->**.exitCode** : Integer<!-- END REF -->

#### Descripción

La propiedad `.exitCode` <!-- REF #SystemWorkerClass.exitCode.Summary -->contiene el código de salida devuelto por el proceso externo<!-- END REF -->. Si el proceso no terminó normalmente, `exitCode` es *undefined*.

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.hideWindow.Desc -->

## .hideWindow

<!-- REF #SystemWorkerClass.hideWindow.Syntax -->**.hideWindow** : Boolean<!-- END REF -->

#### Descripción

La propiedad `.hideWindow` <!-- REF #SystemWorkerClass.hideWindow.Summary -->puede utilizarse para ocultar la ventana de la consola DOS o la ventana del ejecutable lanzado (**sólo Windows**)<!-- END REF -->.

<!-- END REF -->

Esta propiedad está en **lectura-escritura**.

<!-- REF SystemWorkerClass.pid.Desc -->

## .pid

<!-- REF #SystemWorkerClass.pid.Syntax -->**.pid**: Integer<!-- END REF -->

#### Descripción

La propiedad `.pid` <!-- REF #SystemWorkerClass.pid.Summary -->contiene el identificador único del proceso externo a nivel de sistema<!-- END REF -->.

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.postMessage().Desc -->

## .postMessage()

<!-- REF #SystemWorkerClass.postMessage().Syntax -->**.postMessage**( *message* : Text)<br/>**.postMessage**( *messageBLOB* : Blob)<!-- END REF -->

<!-- REF #SystemWorkerClass.postMessage().Params -->

| Parámetros  | Tipo |     | Descripción                                                                            |
| ----------- | ---- | :-: | -------------------------------------------------------------------------------------- |
| message     | Text |  -> | Texto a escribir en el flujo de entrada (stdin) del proceso externo |
| messageBLOB | Blob |  -> | Bytes escritos en el flujo de entrada                                                  |

<!-- END REF -->

#### Descripción

La función `.postMessage()` <!-- REF #SystemWorkerClass.postMessage().Summary --> permite escribir en el flujo de entrada (stdin) del proceso externo<!-- END REF -->. En el parámetro *mensaje*, pase el texto a escribir en *stdin*.

La función `.postMessage()` también acepta un valor de tipo Blob en *messageBLOB* para pasar en *stdin*, de forma que se pueden publicar datos binarios.

Puede utilizar la propiedad `.dataType` del objeto [options](#options-object) para hacer que el cuerpo de la respuesta devuelva valores Blob.

<!-- END REF -->

<!-- REF SystemWorkerClass.response.Desc -->

## .response

<!-- REF #SystemWorkerClass.response.Syntax -->**.response** : Text<br/>**.response** : Blob<!-- END REF -->

#### Descripción

La propiedad `.response` <!-- REF #SystemWorkerClass.response.Summary -->contiene la concatenación de todos los datos devueltos una vez finalizada la petición<!-- END REF -->, es decir, el mensaje completo recibido de la salida del proceso.

El tipo del mensaje se define en función del atributo [`dataType`](#datatype).

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.responseError.Desc -->

## .responseError

<!-- REF #SystemWorkerClass.responseError.Syntax -->**.responseError** : Text<!-- END REF -->

#### Descripción

La propiedad `.responseError` <!-- REF #SystemWorkerClass.responseError.Summary -->contiene la concatenación de todos los errores devueltos, una vez finalizada la petición<!-- END REF -->.

<!-- END REF -->

<!-- REF SystemWorkerClass.terminate().Desc -->

## .terminate()

<!-- REF #SystemWorkerClass.terminate().Syntax -->**.terminate**()<!-- END REF -->

<!-- REF #SystemWorkerClass.terminate().Params -->

| Parámetros | Tipo |     | Descripción                  |
| ---------- | ---- | :-: | ---------------------------- |
|            |      |     | No requiere ningún parámetro |

<!-- END REF -->

#### Descripción

La función `.terminate()` <!-- REF #SystemWorkerClass.terminate().Summary -->fuerza al `SystemWorker` a terminar su ejecución<!-- END REF -->.

Esta función envía la instrucción de terminar y devolver el control al script en ejecución.

<!-- END REF -->

<!-- REF SystemWorkerClass.terminated.Desc -->

## .terminated

<!-- REF #SystemWorkerClass.terminated.Syntax -->**.terminated** : Boolean<!-- END REF -->

#### Descripción

La propiedad `.terminated` <!-- REF #SystemWorkerClass.terminated.Summary -->contiene **true** si el proceso externo está terminado<!-- END REF -->.

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.timeout.Desc -->

## .timeout

<!-- REF #SystemWorkerClass.timeout.Syntax -->**.timeout** : Integer<!-- END REF -->

#### Descripción

La propiedad `.timeout` <!-- REF #SystemWorkerClass.timeout.Summary -->contiene la duración en segundos antes de que el proceso externo sea eliminado si sigue vivo<!-- END REF -->.

Esta propiedad es de **solo lectura**.

<!-- END REF -->

<!-- REF SystemWorkerClass.wait().Desc -->

## .wait()

<details><summary>Historia</summary>

| Lanzamiento | Modificaciones |
| ----------- | -------------- |

|19 R4|Añadido|

</details>

<!-- REF #SystemWorkerClass.wait().Syntax -->**.wait**( {*timeout* : Real} ) : 4D.SystemWorker<!-- END REF -->

<!-- REF #SystemWorkerClass.wait().Params -->

| Parámetros | Tipo                            |                             | Descripción                         |
| ---------- | ------------------------------- | :-------------------------: | ----------------------------------- |
| timeout    | Real                            |              ->             | Tiempo máximo de espera en segundos |
| Resultado  | 4D.SystemWorker | <- | Objeto SystemWorker                 |

<!-- END REF -->

#### Descripción

La función `.wait()` <!-- REF #SystemWorkerClass.wait().Summary -->espera hasta el final de la ejecución de `SystemWorker` o se alcanza el *timeout* especificado<!-- END REF -->.

La función `.wait()` espera hasta el final del procesamiento de la fórmula `onTerminate`, excepto si el *timeout* es alcanzado (Si alguno está definido), o ha ocurrido un error. Si se alcanza el *timeout*, no se elimina el `SystemWorker`.

Si pasa un valor de *timeout*, .wait() espera el proceso externo por la cantidad de tiempo definido en el parámetro *timeout*.

:::note

Durante la ejecución de `.wait()`, se ejecutan funciones de retrollamda, tanto si proceden de otras instancias de `SystemWorker`. Puede salir de un `.wait()` llamando a [`terminate()`](#terminate) desde un callback.

:::

> Esta función no es necesaria si creó el `SystemWorker` desde un proceso worker 4D.

<!-- END REF -->
