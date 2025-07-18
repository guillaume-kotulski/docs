---
id: FileClass
title: File
---

Os objetos `File` são criados com o comando [`File`](../commands/file.md). Contêm referências a ficheiros de disco que podem ou não existir efectivamente no disco. Por exemplo, quando você executa o comando `File` para criar um arquivo, um objeto `File` válido é criado, mas nada é realmente armazenado no disco até que você chame a função [`file.create( )`](#create).

### Exemplo

O exemplo seguinte cria um arquivo de preferências na pasta do projecto:

```code4d
var $created : Boolean
$created:=File("/PACKAGE/SpecialPrefs/"+Current user+".myPrefs").create()
```

### Pathnames

Os objetos `File` suportam vários pathnames, incluindo a sintaxe `filesystems` ou `posix`. Os nomes de caminho compatíveis são detalhados na página [**Rotas de acesso**](../Concepts/paths.md).

### Objeto File

|                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------- |
| [<!-- INCLUDE #document.copyTo().Syntax -->](#copyto)<br/><!-- INCLUDE #document.copyTo().Summary -->                           |
| [<!-- INCLUDE #FileClass.create().Syntax -->](#create)<br/><!-- INCLUDE #FileClass.create().Summary -->                         |
| [<!-- INCLUDE #FileClass.createAlias().Syntax -->](#createalias)<br/><!-- INCLUDE #FileClass.createAlias().Summary -->          |
| [<!-- INCLUDE #document.creationDate.Syntax -->](#creationdate)<br/><!-- INCLUDE #document.creationDate.Summary -->             |
| [<!-- INCLUDE #document.creationTime.Syntax -->](#creationtime)<br/><!-- INCLUDE #document.creationTime.Summary -->             |
| [<!-- INCLUDE #FileClass.delete().Syntax -->](#delete)<br/><!-- INCLUDE #FileClass.delete().Summary -->                         |
| [<!-- INCLUDE #document.exists.Syntax -->](#exists)<br/><!-- INCLUDE #document.exists.Summary -->                               |
| [<!-- INCLUDE #document.extension.Syntax -->](#extension)<br/><!-- INCLUDE #document.extension.Summary -->                      |
| [<!-- INCLUDE #document.fullName.Syntax -->](#fullname)<br/><!-- INCLUDE #document.fullName.Summary -->                         |
| [<!-- INCLUDE #FileClass.getAppInfo().Syntax -->](#getappinfo)<br/><!-- INCLUDE #FileClass.getAppInfo().Summary -->             |
| [<!-- INCLUDE #document.getContent().Syntax -->](#getcontent)<!-- INCLUDE #document.getContent().Summary -->                    |
| [<!-- INCLUDE #document.getIcon().Syntax -->](#geticon)<br/><!-- INCLUDE #document.getIcon().Summary -->                        |
| [<!-- INCLUDE #document.getText().Syntax -->](#gettext)<br/><!-- INCLUDE #document.getText().Summary -->                        |
| [<!-- INCLUDE #document.hidden.Syntax -->](#hidden)<br/><!-- INCLUDE #document.hidden.Summary -->                               |
| [<!-- INCLUDE #document.isAlias.Syntax -->](#isalias)<br/><!-- INCLUDE #document.isAlias.Summary -->                            |
| [<!-- INCLUDE #document.isFile.Syntax -->](#isfile)<br/><!-- INCLUDE #document.isFile.Summary -->                               |
| [<!-- INCLUDE #document.isFolder.Syntax -->](#isfolder)<br/><!-- INCLUDE #document.isFolder.Summary -->                         |
| [<!-- INCLUDE #document.isWritable.Syntax -->](#iswritable)<br/><!-- INCLUDE #document.isWritable.Summary -->                   |
| [<!-- INCLUDE #document.modificationDate.Syntax -->](#modificationdate)<br/><!-- INCLUDE #document.modificationDate.Summary --> |
| [<!-- INCLUDE #document.modificationTime.Syntax -->](#modificationtime)<br/><!-- INCLUDE #document.modificationTime.Summary --> |
| [<!-- INCLUDE #FileClass.moveTo().Syntax -->](#moveto)<br/><!-- INCLUDE #FileClass.moveTo().Summary -->                         |
| [<!-- INCLUDE #document.name.Syntax -->](#name)<br/><!-- INCLUDE #document.name.Summary -->                                     |
| [<!-- INCLUDE #FileClass.open().Syntax -->](#open)<br/><!-- INCLUDE #FileClass.open().Summary -->                               |
| [<!-- INCLUDE #document.original.Syntax -->](#original)<br/><!-- INCLUDE #document.original.Summary -->                         |
| [<!-- INCLUDE #document.parent.Syntax -->](#parent)<br/><!-- INCLUDE #document.parent.Summary -->                               |
| [<!-- INCLUDE #document.path.Syntax -->](#path)<br/><!-- INCLUDE #document.path.Summary -->                                     |
| [<!-- INCLUDE #document.platformPath.Syntax -->](#platformpath)<br/><!-- INCLUDE #document.platformPath.Summary -->             |
| [<!-- INCLUDE #FileClass.rename().Syntax -->](#rename)<br/><!-- INCLUDE #FileClass.rename().Summary -->                         |
| [<!-- INCLUDE #FileClass.setAppInfo().Syntax -->](#setappinfo)<br/><!-- INCLUDE #FileClass.setAppInfo().Summary -->             |
| [<!-- INCLUDE #FileClass.setContent().Syntax -->](#setcontent)<br/><!-- INCLUDE #FileClass.setContent().Summary -->             |
| [<!-- INCLUDE #FileClass.setText().Syntax -->](#settext)<br/><!-- INCLUDE #FileClass.setText().Summary -->                      |
| [<!-- INCLUDE #document.size.Syntax -->](#size)<br/><!-- INCLUDE #document.size.Summary -->                                     |

## 4D. File.new()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R6   | Adicionado |

</details>

<!-- REF #4D.File.new().Syntax -->

**4D.File.new** ( *path* : Text { ; *pathType* : Integer } ) : 4D.File<br/>**4D.File.new** ( *fileConstant* : Integer ) : 4D.File<!-- END REF -->

#### Descrição

A função `4D.File.new()` <!-- REF #4D.File.new().Summary -->cria e retorna um novo objeto do tipo `4D.File`<!-- END REF -->. É idêntico ao comando [`File`](../commands/file.md) (atalho).

> Recomenda-se usar o comando de atalho [`File`](../commands/file.md) em vez de `4D.File.new()`.

<!-- INCLUDE document.copyTo().Desc -->

<!-- REF file.create().Desc -->

## .create()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R5   | Adicionado |

</details>

<!--REF file.create().Note -->

**Não disponível para arquivos ZIP**<!-- END REF -->

<!--REF #FileClass.create().Syntax -->**.create()** : Boolean <!-- END REF -->

<!--REF #FileClass.create().Params -->

| Parâmetro  | Tipo       |                             | Descrição                                                      |
| ---------- | ---------- | --------------------------- | -------------------------------------------------------------- |
| Resultados | Parâmetros | <- | True se o arquivo foi criado com sucesso, false caso contrário |

<!-- END REF -->

#### Descrição

A função `.create()` <!-- REF #FileClass.create().Summary -->cria um arquivo no disco de acordo com as propriedades do objeto `File`<!-- END REF -->.

Se necessário, a função cria a hierarquia de pastas conforme descrito nas propriedades [platformPath](#platformpath) ou [path](#path). Se o arquivo já existir no disco, a função não faz nada (não é atirado nenhum erro) e retorna falso.

**Valor retornado**

- **True** se o arquivo for criado com sucesso;
- **False** se já existir um arquivo com o mesmo nome ou se tiver ocorrido um erro.

#### Exemplo

Criação de um arquivo de preferências na pasta da base de dados:

```4d
 var $created : Boolean
 $created:=File("/PACKAGE/SpecialPrefs/"+Current user+".myPrefs").create()
```

<!-- END REF -->

<!-- REF file.createAlias().Desc -->

## .createAlias()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R5   | Adicionado |

</details>

<!--REF #FileClass.createAlias().Syntax -->**.createAlias**( *destinationFolder* : 4D.Folder ; *aliasName* : Text { ; *aliasType* : Integer } ) : 4D.File<!-- END REF -->

<!--REF #FileClass.createAlias().Params -->

| Parâmetro         | Tipo                       |                             | Descrição                                     |
| ----------------- | -------------------------- | --------------------------- | --------------------------------------------- |
| destinationFolder | 4D. Folder | ->                          | Pasta de destino para o pseudónimo ou atalho  |
| aliasName         | Text                       | ->                          | Nome do pseudónimo ou atalho                  |
| aliasType         | Integer                    | ->                          | Tipo de ligação do pseudónimo                 |
| Resultados        | 4D. File   | <- | Referência a pseudónimo ou ficheiro de atalho |

<!-- END REF -->

#### Descrição

A função `.createAlias()` <!-- REF #FileClass.createAlias().Summary -->cria um alias (macOS) ou um atalho (Windows)<!-- END REF --> para o arquivo com o nome *aliasName* especificado na pasta designada pelo objeto *destinationFolder*.

Passar o nome do alias ou atalho para criar no parâmetro *aliasName*.

Por padrão em macOS, a função cria um pseudónimo padrão. Também pode criar uma ligação simbólica utilizando o parâmetro *aliasType*. Estão disponíveis as seguintes constantes:

| Parâmetros         | Valor | Comentário                                      |
| ------------------ | ----- | ----------------------------------------------- |
| `fk alias link`    | 0     | Alias link (padrão)          |
| `fk symbolic link` | 1     | Link simbólico (só em macOS) |

No Windows, é sempre criado um atalho (arquivo.lnk) (o parâmetro *aliasType* é ignorado).

**Objeto devolvido**

Um objeto `4D.File` com a propriedade `isAlias` definida como **true**.

#### Exemplo

Se quiser criar um alias para um arquivo na sua pasta database:

```4d
 $myFile:=Folder(fk documents folder).file("Archives/ReadMe.txt")
 $aliasFile:=$myFile.createAlias(File("/PACKAGE");"ReadMe")
```

<!-- END REF -->

<!-- INCLUDE document.creationDate.Desc -->

<!-- INCLUDE document.creationTime.Desc -->

<!-- REF file.delete().Desc -->

## .delete()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R5   | Adicionado |

</details>

<!--REF #FileClass.delete().Syntax -->**.delete**()<!-- END REF -->

<!-- REF #FileClass.delete().Params -->

| Parâmetro | Tipo |     | Descrição                  |
| --------- | ---- | :-: | -------------------------- |
|           |      |     | Não exige nenhum parâmetro |

<!-- END REF -->

#### Descrição

A função `.delete()` <!-- REF #FileClass.delete().Summary -->exclui o arquivo<!-- END REF -->.

Se o arquivo não existir no disco, a função não faz nada (não é gerado nenhum erro).

Se o ficheiro estiver atualmente aberto, o resultado depende do sistema operativo:

- no Windows, é gerado um erro,
- no macOS, não é gerado qualquer erro e o ficheiro é eliminado.

:::caution

`.delete()` pode apagar qualquer ficheiro num disco. Isto inclui documentos criados com outras aplicações, bem como as próprias aplicações. `.delete()` deve ser usado com extrema cautela. A eliminação de um arquivo é uma operação permanente e não pode ser desfeita.

:::

#### Exemplo

Se quiser apagar um ficheiro específico na pasta da base de dados:

```4d
 $tempo:=File("/PACKAGE/SpecialPrefs/"+Current user+".prefs")
 If($tempo.exists)
    $tempo.delete()
    ALERT("User preference file deleted.")
 End if
```

<!-- END REF -->

<!-- INCLUDE document.exists.Desc -->

<!-- INCLUDE document.extension.Desc -->

<!-- INCLUDE document.fullName.Desc -->

<!-- REF file.getAppInfo().Desc -->

## .getAppInfo()

<details><summary>História</summary>

| Release | Mudanças                           |
| ------- | ---------------------------------- |
| 20 R9   | Ler os UUIDs nos executáveis macOS |
| 19      | Adicionado                         |

</details>

<!--REF #FileClass.getAppInfo().Syntax -->**.getAppInfo**() : Object<!-- END REF -->

<!--REF #FileClass.getAppInfo().Params -->

| Parâmetro  | Tipo   |                             | Descrição                           |
| ---------- | ------ | --------------------------- | ----------------------------------- |
| Resultados | Object | <- | Informações do arquivo da aplicação |

<!-- END REF -->

#### Descrição

A função `.getAppInfo()` <!-- REF #FileClass.getAppInfo().Summary -->retorna o conteúdo de informações de arquivos de aplicação como um objeto<!-- END REF -->.

A função deve ser usada com um arquivo existente e compatível: **.plist** (todas as plataformas), **.exe**/**.dll** (Windows) ou **macOS executável**. Se o arquivo não existir no disco ou não for um arquivo compatível, a função retornará um objeto vazio (nenhum erro será gerado).

**Objeto retornado com um arquivo .plist (todas as plataformas)**

O conteúdo xml do arquivo é analisado e as chaves são devolvidas como propriedades do objeto, preservando os seus tipos (texto, booleano, número). `.plist dict` é retornado como um objeto JSON e o `.plist array` é retornado como um array JSON.

:::note

A função apenas é compatível com arquivos .plist em formato xml (baseado em texto). Um erro é retornado se usado com um arquivo .plist em formato binário.

:::

**Objeto retornado com um arquivo .exe ou .dll (somente Windows)**

Todos os valores de propriedades são Texto.

| Propriedade      | Tipo |
| ---------------- | ---- |
| InternalName     | Text |
| ProductName      | Text |
| CompanyName      | Text |
| LegalCopyright   | Text |
| ProductVersion   | Text |
| FileDescription  | Text |
| FileVersion      | Text |
| OriginalFilename | Text |

**Objeto retornado com um arquivo executável do macOS (somente macOS)**

:::note

Um arquivo executável macOS está localizado em um pacote (por exemplo, myApp.app/Contents/MacOS/myApp).

:::

A função retorna um objeto `archs` que contém uma coleção de objetos que descrevem cada arquitetura encontrada no executável (um executável fat pode incorporar várias arquiteturas). Cada objeto da coleção contém as seguintes propriedades:

| Propriedade | Tipo   | Descrição                                                                         |
| ----------- | ------ | --------------------------------------------------------------------------------- |
| name        | Text   | Nome da arquitetura ("arm64" ou "x86_64") |
| type        | Number | Identificador numérico da arquitetura                                             |
| uuid        | Text   | Representação textual do uuid do executável                                       |

#### Exemplo 1

```4d
  // exibir informações de direitos autorais de um info.plist (qualquer plataforma)
var $infoPlistFile : 4D.File
var $info : Object
$infoPlistFile:=File("/RESOURCES/info.plist")
$info:=$infoPlistFile.getAppInfo()
ALERT($info.Copyright)
```

#### Exemplo 2

```4d
 // display copyright info of application .exe file (windows)
var $exeFile : 4D.File
var $info : Object
$exeFile:=File(Application file; fk platform path)
$info:=$exeFile.getAppInfo()
ALERT($info.LegalCopyright)
```

#### Exemplo 3

```4d
 // Get uuids of an application (macOS)
var $app:=File("/Applications/myApp.app/Contents/MacOS/myApp")
var $info:=$app.getAppInfo()
```

Resultado em *$info*:

```json
{
  "archs":
  [
      {
        "name":"x86_64",
        "type":16777223,
        "uuid":"3840983CDA32392DA4D1D32F08AB3212"
      },
      {
        "name":"arm64",
        "type":16777228,
        "uuid":"E49F6BA275B931DDA183C0B0CDF0ADAF"
      }
  ]
}
```

#### Veja também

[.setAppInfo()](#setappinfo)

<!-- END REF -->

<!-- INCLUDE document.getContent().Desc -->

<!-- INCLUDE document.getIcon().Desc -->

<!-- INCLUDE document.getText().Desc -->

<!-- INCLUDE document.hidden.Desc -->

<!-- INCLUDE document.isAlias.Desc -->

<!-- INCLUDE document.isFile.Desc -->

<!-- INCLUDE document.isFolder.Desc -->

<!-- INCLUDE document.isWritable.Desc -->

<!-- INCLUDE document.modificationDate.Desc -->

<!-- INCLUDE document.modificationTime.Desc -->

<!-- REF file.moveTo().Desc -->

## .moveTo()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R5   | Adicionado |

</details>

<!--REF #FileClass.moveTo().Syntax -->**.moveTo**( *destinationFolder* : 4D.Folder { ; *newName* : Text } ) : 4D.File<!-- END REF -->

<!--REF #FileClass.moveTo().Params -->

| Parâmetro         | Tipo                       |                             | Descrição                        |
| ----------------- | -------------------------- | --------------------------- | -------------------------------- |
| destinationFolder | 4D. Folder | ->                          | Pasta de destino                 |
| newName           | Text                       | ->                          | Nome completo do ficheiro movido |
| Resultados        | 4D. File   | <- | Arquivo movido                   |

<!-- END REF -->

#### Descrição

A função `.moveTo()` <!-- REF #FileClass.moveTo().Summary -->move ou renomeia o objeto `File` para a *destinationFolder* especificada<!-- END REF -->.

A *destinationFolder* deve existir em disco, senão um erro é gerado.

Por padrão, o arquivo mantém o seu nome quando é movido. Se quiser renomear o arquivo movido, passe o novo nome completo no parâmetro *newName*. O novo nome deve cumprir com as regras de nomenclatura (por exemplo, não deve conter caracteres como ":", "/", etc.), do contrário se devolve um erro.

**Objeto devolvido**

O objeto `File` movido.

#### Exemplo

```4d
$DocFolder:=Folder(fk documents folder)
$myFile:=$DocFolder.file("Current/Infos.txt")
$myFile.moveTo($DocFolder.folder("Archives");"Infos_old.txt")
```

<!-- END REF -->

<!-- INCLUDE document.name.Desc -->

<!-- REF file.open().Desc -->

## .open()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R6   | Adicionado |

</details>

<!--REF #FileClass.open().Syntax -->**.open**( { *mode* : Text } ) : 4D.FileHandle<br/>**.open**( { *options* : Object } ) : 4D.FileHandle<!-- END REF -->

<!--REF #FileClass.open().Params -->

| Parâmetro  | Tipo                                             |                             | Descrição                                                   |
| ---------- | ------------------------------------------------ | --------------------------- | ----------------------------------------------------------- |
| mode       | Text                                             | ->                          | Modo de abertura: "read", "write", "append" |
| options    | Object                                           | ->                          | Opções de abertura                                          |
| Resultados | [4D.FileHandle](FileHandleClass) | <- | Novo objeto File handle                                     |

<!-- END REF -->

#### Descrição

A função `.open()` <!-- REF #FileClass.open().Summary -->cria e retorna um novo objeto [4D.FileHandle](FileHandleClass) no arquivo, no *mode* especificado ou com as *options* especificadas<!-- END REF -->. Pode utilizar funções e propriedades da classe [4D.FileHandle](FileHandleClass) para escrever, ler ou anexar conteúdo ao arquivo.

Se utilizar o parâmetro *mode* (text), passe o modo de abertura para o file handle:

| *mode*   | Descrição                                                                                                                                                                                                                                                                                         |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "read"   | (Padrão) Cria um file handle para ler os valores do arquivo. Se o arquivo não existir em disco, um erro é retornado. Pode abrir quantos file handles quiser em modo "ler" no mesmo objeto File.                                |
| "write"  | Cria um file handle para escrever os valores no arquivo (começando no início do conteúdo do arquivo). Se o arquivo não existir em disco, é criado. Só se pode abrir um único file handle em modo "write" no mesmo objeto File. |
| "append" | Cria um file handle para escrever os valores no arquivo (começando no fim do conteúdo do arquivo). Se o arquivo não existir em disco, é criado. Só se pode abrir um único file handle em modo "append" no mesmo objeto File.   |

> O valor de *modo* diferencia maiúsculas de minúsculas.

Se você usar o parâmetro *options* (objeto), poderá passar mais opções para o identificador de arquivo por meio das seguintes propriedades (essas propriedades podem ser lidas posteriormente a partir do [objeto de identificador de arquivo](FileHandleClass) aberto):

| *opções*          | Tipo           | Descrição                                                                                                                                                                     | Por padrão    |
| ----------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| `.mode`           | Text           | Modo de abertura (consulte *modo* acima)                                                                                                                   | "read"        |
| `.charset`        | Text           | Conjunto de carateres utilizado para ler ou escrever no ficheiro. Utilizar o nome padrão do conjunto (por exemplo "ISO-8859-1" ou "UTF-8") | "UTF-8"       |
| `.breakModeRead`  | Text ou Number | Modo de tratamento das quebras de linha utilizadas na leitura do arquivo (veja abaixo)                                                                     | "native" ou 1 |
| `.breakModeWrite` | Text ou Number | Modo de processamento das quebras de linha utilizadas ao escrever no ficheiro (ver abaixo)                                                                 | "native" ou 1 |

A função substitui todos os delimitadores de fim de linha originais. Por defeito, é utilizado o delimitador nativo, mas é possível definir outro delimitador. `.breakModeRead` e o `.breakModeWrite` indicam o processamento a ser aplicado aos caracteres de fim de linha no documento. Pode utilizar um dos seguintes valores (texto ou número):

| Modo de interrupção no texto | Break mode em numérico (constante) | Descrição                                                                                                                                                                                                                                             |
| ---------------------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "native"                     | 1 (`Document with native format`)  | (Padrão) As quebras de linha são convertidas para o formato nativo do sistema operativo: LF (avanço de linha) no macOS, CRLF (retorno de carro + avanço de linha) no Windows |
| "crlf"                       | 2 (`Document with CRLF`)           | As quebras de linha são convertidas em CRLF (retorno de carro + avanço de linha), o formato predefinido do Windows                                                                                                                 |
| "cr"                         | 3 (`Document with CR`)             | As quebras de linha são convertidas em CR (carriage return), o formato padrão do Mac OS                                                                                                                                            |
| "lf"                         | 4 (`Document with LF`)             | As quebras de linha são convertidas para LF (line feed), o formato padrão Unix e macOS                                                                                                                                             |

> O valor *break mode as text* diferencia maiúsculas de minúsculas.

#### Exemplo

Pretende criar um file handle para a leitura do ficheiro "ReadMe.txt":

```4d
var $f : 4D.File
var $fhandle : 4D.FileHandle

$f:=File("C:\\Documents\\Archives\\ReadMe.txt";fk platform path)
$fhandle:=$f.open("read")

```

<!-- END REF -->

<!-- INCLUDE document.original.Desc -->

<!-- INCLUDE document.parent.Desc -->

<!-- INCLUDE document.path.Desc -->

<!-- INCLUDE document.platformPath.Desc -->

<!-- REF file.rename().Desc -->

## .rename()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R5   | Adicionado |

</details>

<!--REF #FileClass.rename().Syntax -->**.rename**( *newName* : Text ) : 4D.File<!-- END REF -->

<!--REF #FileClass.rename().Params -->

| Parâmetro  | Tipo                     |                             | Descrição                          |
| ---------- | ------------------------ | --------------------------- | ---------------------------------- |
| newName    | Text                     | ->                          | Novo nome completo para o ficheiro |
| Resultados | 4D. File | <- | Ficheiro renomeado                 |

<!-- END REF -->

#### Descrição

A função `.rename()` <!-- REF #FileClass.rename().Summary -->renomeia o arquivo com o nome que você passou em *newName* e retorna o objeto `File` renomeado<!-- END REF -->.

O parâmetro *newName* deve estar em conformidade com as regras de nome (por exemplo, ele não deve conter caracteres como ":", "/", etc.), caso contrário um erro é retornado. Se já existir um ficheiro com o mesmo nome, é devolvido um erro.

Note que a função modifica o nome completo do arquivo, ou seja, se você não passar uma extensão em *newName*, o arquivo terá um nome sem uma extensão.

**Objeto devolvido**

O objeto `File` renomeado.

#### Exemplo

Se quiser renomear "ReadMe.txt" em "ReadMe_new.txt":

```4d
 $toRename:=File("C:\\Documents\\Archives\\ReadMe.txt";fk platform path)
 $newName:=$toRename.rename($toRename.name+"_new"+$toRename.extension)
```

<!-- END REF -->

## .setAppInfo()

<details><summary>História</summary>

| Release | Mudanças                           |
| ------- | ---------------------------------- |
| 20 R9   | Ler os UUIDs nos executáveis macOS |
| 20      | Suporte de WinIcon                 |
| 19      | Adicionado                         |

</details>

<!--REF #FileClass.setAppInfo().Syntax -->**.setAppInfo**( *info* : Object )<!-- END REF -->

<!--REF #FileClass.setAppInfo().Params -->

| Parâmetro | Tipo   |    | Descrição                                                             |
| --------- | ------ | -- | --------------------------------------------------------------------- |
| info      | Object | -> | Propriedades para escrever em informações de um arquivo de aplicativo |

<!-- END REF -->

#### Descrição

A função `.setAppInfo()` <!-- REF #FileClass.setAppInfo().Summary -->escreve as propriedades *info* como o conteúdo da informação de um arquivo de aplicação<!-- END REF -->.

A função só pode ser usada com os seguintes tipos de arquivo: **.plist** (todas as plataformas), **.exe**/**.dll** (Windows), ou **macOS executável**. Se usado com outro tipo de arquivo ou com um arquivo **.exe**/**.dll** que ainda não existem no disco, a função não faz nada (nenhum erro é gerado).

Parâmetro ***info* com um arquivo .plist (todas as plataformas)**

:::note

A função apenas é compatível com arquivos .plist em formato xml (baseado em texto). Um erro é retornado se usado com um arquivo .plist em formato binário.

:::

Se o arquivo .plist já existir no disco, ele será atualizado. Caso contrário, será criado.

Cada propriedade válida definida no parâmetro do objecto info está escrita no arquivo .plist como uma chave. Qualquer nome chave é aceito. Os tipos de valores são preservados sempre que possível.

Se uma chave definida no parâmetro *info* já estiver definida no arquivo .plist, seu valor será atualizado enquanto mantém seu tipo original. Outras chaves existentes no arquivo .plist são deixadas intocadas.

:::note

Para definir um valor de tipo de data, o formato a utilizar é uma string de carimbo temporal json formada em ISO UTC sem milissegundos ("2003-02-01T01:02:03Z") como no editor plist de Xcode.

:::

**Parâmetro objeto *info* com um arquivo .exe ou .dll (somente Windows)**

Cada propriedade válida definida no parâmetro do objeto *info* é escrita no recurso de versão do arquivo .exe ou .dll. As propriedades disponíveis são (qualquer outra propriedade será ignorada):

| Propriedade      | Tipo | Comentário                                                                                                                                                |
| ---------------- | ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| InternalName     | Text |                                                                                                                                                           |
| ProductName      | Text |                                                                                                                                                           |
| CompanyName      | Text |                                                                                                                                                           |
| LegalCopyright   | Text |                                                                                                                                                           |
| ProductVersion   | Text |                                                                                                                                                           |
| FileDescription  | Text |                                                                                                                                                           |
| FileVersion      | Text |                                                                                                                                                           |
| OriginalFilename | Text |                                                                                                                                                           |
| WinIcon          | Text | Caminho Posix do ficheiro .ico. Esta propriedade aplica-se apenas a ficheiros executáveis gerados por 4D. |

Para todas as propriedades, exceto `WinIcon`, se você passar um texto nulo ou vazio como valor, uma sequência vazia é escrita na propriedade. Se passar um tipo de valor diferente de texto, este é transformado em string.

Para a propriedade `WinIcon`, se o arquivo de ícone não existir ou tiver um formato incorreto, um erro é gerado.

**Parâmetro *info* com um arquivo macOS executável (somente macOS)**

*info* devem ser um objeto com uma única propriedade chamada `archs` que é uma coleção de objetos no formato retornado por [`getAppInfo()`](#getappinfo). Each object must contain at least the `type` and `uuid` properties (`name` is not used).

Cada objeto na coleção *info*.archs deve conter as seguintes propriedades:

| Propriedade | Tipo   | Descrição                                          |
| ----------- | ------ | -------------------------------------------------- |
| type        | Number | Numerical identifier of the architecture to modify |
| uuid        | Text   | Textual representation of the new executable uuid  |

#### Exemplo 1

```4d
  // set some keys in an info.plist file (all platforms)
var $infoPlistFile : 4D.File
var $info : Object
$infoPlistFile:=File("/RESOURCES/info.plist")
$info:=New object
$info.Copyright:="Copyright 4D 2023" //text
$info.ProductVersion:=12 //integer
$info.ShipmentDate:="2023-04-22T06:00:00Z" //timestamp
$info.CFBundleIconFile:="myApp.icns" //for macOS
$infoPlistFile.setAppInfo($info)
```

#### Exemplo 2

```4d
  // set copyright, version and icon of a .exe file (Windows)
var $exeFile; $iconFile : 4D.File
var $info : Object
$exeFile:=File(Application file; fk platform path)
$iconFile:=File("/RESOURCES/myApp.ico")
$info:=New object
$info.LegalCopyright:="Copyright 4D 2023"
$info.ProductVersion:="1.0.0"
$info.WinIcon:=$iconFile.path
$exeFile.setAppInfo($info)
```

#### Exemplo 3

```4d
// regenerate uuids of an application (macOS)

// read myApp uuids 
var $app:=File("/Applications/myApp.app/Contents/MacOS/myApp")
var $info:=$app.getAppInfo()

// regenerate uuids for all architectures
For each ($i; $info.archs)
	$i.uuid:=Generate UUID
End for each 

// update the app with the new uuids
$app.setAppInfo($info)
```

#### Veja também

[.getAppInfo()](#getappinfo)

<!-- REF file.setContent().Desc -->

## .setContent()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 17 R5   | Adicionado |

</details>

<!--REF #FileClass.setContent().Syntax -->**.setContent** ( *content* : Blob ) <!-- END REF -->

<!--REF #FileClass.setContent().Params -->

| Parâmetro | Tipo |    | Descrição                      |
| --------- | ---- | -- | ------------------------------ |
| content   | BLOB | -> | Novos conteúdos para o arquivo |

<!-- END REF -->

#### Descrição

A função `.setContent( )` <!-- REF #FileClass.setContent().Summary -->reescreve todo o conteúdo do arquivo usando os dados armazenados no *content* BLOB<!-- END REF -->. Para obter informações sobre BLOBs, consulte a seção [BLOB](Concepts/dt_blob.md).

#### Exemplo

```4d
 $myFile:=Folder(fk documents folder).file("Archives/data.txt")
 $myFile.setContent([aTable]aBlobField)
```

<!-- END REF -->

<!-- REF file.setText().Desc -->

## .setText()

<details><summary>História</summary>

| Release | Mudanças                                                                                      |
| ------- | --------------------------------------------------------------------------------------------- |
| 19 R3   | Padrão para novos projectos: sem BOM e (macOS) LF para EOL |
| 17 R5   | Adicionado                                                                                    |

</details>

<!--REF #FileClass.setText().Syntax -->**.setText** ( *text* : Text {; *charSetName* : Text { ; *breakMode* : Integer } } )<br/>**.setText** ( *text* : Text {; *charSetNum* : Integer { ; *breakMode* : Integer } } )<!-- END REF -->

<!--REF #FileClass.setText().Params -->

| Parâmetro   | Tipo    |    | Descrição                                   |
| ----------- | ------- | -- | ------------------------------------------- |
| text        | Text    | -> | Texto a armazenar no arquivo                |
| charSetName | Text    | -> | Nome do conjunto de caracteres              |
| charSetNum  | Integer | -> | Número de conjuntos de caracteres           |
| breakMode   | Integer | -> | Modo de processamento para quebras de linha |

<!-- END REF -->

#### Descrição

A função `.setText()` <!-- REF #FileClass.setText().Summary -->escreve *text* como o novo conteúdo do arquivo<!-- END REF -->.

Se o arquivo referenciado no objeto `File` não existir no disco, ele será criado pela função. Quando o ficheiro já existir no disco, o seu conteúdo anterior é apagado, exceto se já estiver aberto, caso em que o seu conteúdo é bloqueado e é gerado um erro.

Em *text,* passe o texto a escrever no arquivo. Pode ser um texto literal ("my text"), ou um campo/variável texto 4D.

Opcionalmente, pode designar o conjunto de caracteres a utilizar para escrever o conteúdo. Você pode passar também:

- em *charSetName*, uma string que contém o nome padrão definido (por exemplo "ISO-8859-1" ou "UTF-8"),
- ou em *charSetNum*, o MIBEnum ID (número) do nome de configuração padrão.

> Para a lista de conjuntos de caracteres suportados por 4D, consulte a descrição do comando `CONVERT FROM TEXT`.

Se uma marca de ordem de byte (BOM) existe para o conjunto de caracteres, 4D a insere no ficheiro a menos que o conjunto de caracteres usado contenha o sufixo "-no-bom" (por exemplo, "UTF-8-no-bom"). Se não especificar um conjunto de caracteres, por defeito 4D usa o conjunto de caracteres "UTF-8" sem BOM.

Em breakMode, você pode passar um número indicando o processamento a aplicar aos caracteres de fim de linha no documento. Estão disponíveis as seguintes constantes, encontradas no tema **System Documents**:

| Parâmetros                    | Valor | Comentário                                                                                                                                                                                                                                            |
| ----------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Document unchanged`          | 0     | Não processado                                                                                                                                                                                                                                        |
| `Document with native format` | 1     | (Padrão) As quebras de linha são convertidas para o formato nativo do sistema operativo: LF (avanço de linha) no macOS, CRLF (retorno de carro + avanço de linha) no Windows |
| `Documento com CRLF`          | 2     | As quebras de linha são convertidas em CRLF (retorno de carro + avanço de linha), o formato predefinido do Windows                                                                                                                 |
| `Documento com CR`            | 3     | As quebras de linha são convertidas em CR (carriage return), o formato padrão do Mac OS                                                                                                                                            |
| `Documento com LF`            | 4     | As quebras de linha são convertidas para LF (line feed), o formato padrão Unix e macOS                                                                                                                                             |

Por padrão, ao omitir o parâmetro *breakMode*, as quebras de linha são processadas no modo nativo (1).

> **Nota de compatibilidade**: as opções de compatibilidade estão disponíveis para a gerenciamento da EOL e da BOM. Veja a [Página Compatibilidade](https://doc.4d.com/4Dv20/4D/20.2/Compatibility-page.300-6750362.en.html) em doc.4d.com.

#### Exemplo

```4d
$myFile:=File("C:\\Documents\\Hello.txt";fk platform path)
$myFile.setText("Hello world")
```

<!-- END REF -->

<!-- INCLUDE document.size.Desc -->
