---
id: POP3TransporterClass
title: POP3Transporter
---

O `POP3Transporter` permite recuperar mensagens de um servidor de email POP3.

### Objeto POP3 transporter

Os objetos POP3 Transporter são instanciados com o comando [`POP3 New transporter`](../commands/pop3-new-transporter.md). Eles oferecem as propriedades abaixo e funções:

|                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [<!-- INCLUDE #transporter.acceptUnsecureConnection.Syntax -->](#acceptunsecureconnection)<br/><!-- INCLUDE #transporter.acceptUnsecureConnection.Summary --> |
| [<!-- INCLUDE #transporter.authenticationMode.Syntax -->](#authenticationmode)<br/><!-- INCLUDE #transporter.authenticationMode.Summary -->                   |
| [<!-- INCLUDE #transporter.checkConnection().Syntax -->](#checkconnection)<br/><!-- INCLUDE #transporter.checkConnection().Summary -->                        |
| [<!-- INCLUDE #transporter.connectionTimeOut.Syntax -->](#connectiontimeout)<br/><!-- INCLUDE #transporter.connectionTimeOut.Summary -->                      |
| [<!-- INCLUDE #POP3TransporterClass.delete().Syntax -->](#delete)<br/><!-- INCLUDE #POP3TransporterClass.delete().Summary -->                                 |
| [<!-- INCLUDE #POP3TransporterClass.getBoxInfo().Syntax -->](#getboxinfo)<br/><!-- INCLUDE #POP3TransporterClass.getBoxInfo().Summary -->                     |
| [<!-- INCLUDE #POP3TransporterClass.getMail().Syntax -->](#getmail)<br/><!-- INCLUDE #POP3TransporterClass.getMail().Summary -->                              |
| [<!-- INCLUDE #POP3TransporterClass.getMailInfo().Syntax -->](#getmailinfo)<br/><!-- INCLUDE #POP3TransporterClass.getMailInfo().Summary -->                  |
| [<!-- INCLUDE #POP3TransporterClass.getMailInfoList().Syntax -->](#getmailinfolist)<br/><!-- INCLUDE #POP3TransporterClass.getMailInfoList().Summary -->      |
| [<!-- INCLUDE #POP3TransporterClass.getMIMEAsBlob().Syntax -->](#getmimeasblob)<br/><!-- INCLUDE #POP3TransporterClass.getMIMEAsBlob().Summary -->            |
| [<!-- INCLUDE #transporter.host.Syntax -->](#host)<br/><!-- INCLUDE #transporter.host.Summary -->                                                             |
| [<!-- INCLUDE #transporter.logFile.Syntax -->](#logfile)<br/><!-- INCLUDE #transporter.logFile.Summary -->                                                    |
| [<!-- INCLUDE #transporter.port.Syntax -->](#port)<br/><!-- INCLUDE #transporter.port.Summary -->                                                             |
| [<!-- INCLUDE #POP3TransporterClass.undeleteAll().Syntax -->](#undeleteall)<br/><!-- INCLUDE #POP3TransporterClass.undeleteAll().Summary -->                  |
| [<!-- INCLUDE #transporter.port.Syntax -->](#port)<br/><!-- INCLUDE #transporter.port.Summary -->                                                             |

## 4D.POP3Transporter.new()

<!-- REF #4D.POP3Transporter.new().Syntax -->**4D.POP3Transporter.new**( *server* : Object ) : 4D.POP3Transporter<!-- END REF -->

<!-- REF #4D.POP3Transporter.new().Params -->

| Parâmetro  | Tipo                               |                             | Descrição                                          |
| ---------- | ---------------------------------- | :-------------------------: | -------------------------------------------------- |
| server     | Object                             |              ->             | Informação de servidor de correio                  |
| Resultados | 4D.POP3Transporter | <- | [Objeto POP3 Transporter](#objet-pop3-transporter) |

<!-- END REF -->

#### Descrição

A função `4D.POP3Transporter.new()` <!-- REF #4D.POP3Transporter.new().Summary --> cria e retorna um novo objeto do tipo `4D.POP3Transporter`<!-- END REF -->. É idêntico ao comando [`POP3 New transporter`](../commands/pop3-new-transporter.md) (atalho).

<!-- INCLUDE transporter.acceptUnsecureConnection.Desc -->

<!-- INCLUDE transporter.authenticationModePOP3.Desc -->

<!-- INCLUDE transporter.checkConnection().Desc -->

#### Exemplo

```4d
 var $pw :  Text
 var $options : Object
 $options:=New object

 $pw:=Request("Please enter your password:")
 if(OK=1)
    $options.host:="pop3.gmail.com"

    $options.user:="test@gmail.com"
    $options.password:=$pw

    $transporter:=POP3 New transporter($options)

    $status:=$transporter.checkConnection()
    If($status.success)
       ALERT("POP3 connection check successful!")
    Else
       ALERT("Error: "+$status.statusText)
    End if
 End if
```

<!-- INCLUDE transporter.connectionTimeOut.Desc -->

## .delete()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R2   | Adicionado |

</details>

<!-- REF #POP3TransporterClass.delete().Syntax -->**.delete**( *msgNumber* : Integer )<!-- END REF -->

<!-- REF #POP3TransporterClass.delete().Params -->

| Parâmetro | Tipo    |     | Descrição                              |
| --------- | ------- | :-: | -------------------------------------- |
| msgNumber | Integer |  -> | Número da mensagem que vai ser apagada |

<!-- END REF -->

##### Descrição

A função `.delete( )` <!-- REF #POP3TransporterClass.delete().Summary -->flags do e-mail *msgNumber* para exclusão do servidor POP3 <!-- END REF -->.

No parâmetro *msgNumber*, passe o número do email a apagar. Esse número é retornado na propriedade number pelo método [`.getMailInfoList()`](#getmailinfolist).

Executar esse método não remove de verdade qualquer email. O email marcado será apagado do servidor POP3 apenas quando o `POP3_transporter` (criado com `POP3 New transporter`) for destruído. A marcação pode ser removida com o método `.undeleteAll()`.

> Se a sessão atual terminar de forma inesperada e perder a conexão (por exemplo timeout, falha de rede, etc), uma mensagem de erro é gerada e mensagens marcadas para serem apagadas continuam no servidor POP3.

##### Exemplo

```4d
 $mailInfoList:=$POP3_transporter.getMailInfoList()
 For each($mailInfo;$mailInfoList)
  // Marca seu email a "to be deleted at the end of the session"
    $POP3_transporter.delete($mailInfo.number)
 End for each
  // Força que o fechamento da sessão apague os emails marcados para serem eliminados
 CONFIRM("Selected messages will be deleted.";"Delete";"Undo")
 If(OK=1) //eliminação confirmada
    $POP3_transporter:=Null
 Else
    $POP3_transporter.undeleteAll() //remove marcas de eliiminação
 End if
```

## .getBoxInfo()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R2   | Adicionado |

</details>

<!-- REF #POP3TransporterClass.getBoxInfo().Syntax -->**.getBoxInfo()** : Object<!-- END REF -->

<!-- REF #POP3TransporterClass.getBoxInfo().Params -->

| Parâmetro  | Tipo   |                             | Descrição       |
| ---------- | ------ | :-------------------------: | --------------- |
| Resultados | Object | <- | objecto boxInfo |

<!-- END REF -->

##### Descrição

A função `.getBoxInfo()` <!-- REF #POP3TransporterClass.getBoxInfo().Summary -->retorna um objeto `boxInfo` correspondente à caixa de correio designada pelo [`transporter POP3 `](#pop3-transporter-object)<!-- END REF -->. Essa função permite que recupere informação sobre o mailbox.

O objeto `boxInfo` retornado contém as seguintes propriedades:

| Propriedade | Tipo   | Descrição                             |
| ----------- | ------ | ------------------------------------- |
| mailCount   | Number | Número de mensagens na caixa de email |
| size        | Number | Tamanho da mensagem em bytes          |

##### Exemplo

```4d
 var $server; $boxinfo : Object

 $server:=New object
 $server.host:="pop.gmail.com" //Obrigatório
 $server.port:=995
 $server.user:="4d@gmail.com"
 $server.password:="XXXXXXXX"

 $transporter:=POP3 New transporter($server)

  //mailbox informação
 $boxInfo:=$transporter.getBoxInfo()
 ALERT("The mailbox contains "+String($boxInfo.mailCount)+" messages.")
```

## .getMail()

<details><summary>História</summary>

| Release | Mudanças                          |
| ------- | --------------------------------- |
| 20      | Suporte ao parâmetro *headerOnly* |
| 18 R2   | Adicionado                        |

</details>

<!-- REF #POP3TransporterClass.getMail().Syntax -->**.getMail**( *msgNumber* : Integer { ; *headerOnly* : Boolean } ) : Object<!-- END REF -->

<!-- REF #POP3TransporterClass.getMail().Params -->

| Parâmetro  | Tipo       |                             | Descrição                                                                                                  |
| ---------- | ---------- | :-------------------------: | ---------------------------------------------------------------------------------------------------------- |
| msgNumber  | Integer    |              ->             | Número da mensagem que na lista                                                                            |
| headerOnly | Parâmetros |              ->             | True para descarregar apenas os cabeçalhos de correio electrónico (por defeito é False) |
| Resultados | Object     | <- | [Objeto email](EmailObjectClass.md#email-object)                                                           |

<!-- END REF -->

##### Descrição

A função `.getMail()` <!-- REF #POP3TransporterClass.getMail().Summary -->retorna o objeto `Email` correspondente ao *msgNumber* na caixa de correio designada pelo [`transporter POP3`](#pop3-transporter-object)<!-- END REF -->. Essa função permite manejar localmente os conteúdos de email.

Passe em *msgNumber* o número da mensagem a recuperar. Esse número é retornado na propriedade `number` pela função [`.getMailInfoList()`](#getmailinfolist).

Opcionalmente, você pode passar `true` no parâmetro *headerOnly* para excluir as partes do corpo do objeto `Email` retornado. Somente propriedades de cabeçalhos ([`headers`](EmailObjectClass.md#headers), [`to`](EmailObjectClass.md#to), [`from`](EmailObjectClass.md#from)...) são então retornados. Esta opção permite-lhe optimizar a etapa de descarregamento quando muitos e-mails estão no servidor.

:::note

A opção *headerOnly* pode não ser suportada pelo servidor.

:::

O método retorna Null se:

- *msgNumber* determina uma mensagem não existente,
- a mensagem foi marcada para exclusão usando [`.delete()`](#delete).

**Objeto devolvido**

`.getMail()` retorna um [`objeto email`](EmailObjectClass.md#email-object).

##### Exemplo

Se quiser saber o emissário do primeiro email da mailbox:

```4d
 var $server; $transporter : Object
 var $mailInfo : Collection
 var $sender : Variant

 $server:=New object
 $server.host:="pop.gmail.com" //Obrigatório
 $server.port:=995
 $server.user:="4d@gmail.com"
 $server.password:="XXXXXXXX"

 $transporter:=POP3 New transporter($server)

 $mailInfo:=$transporter.getMailInfoList()
 $sender:=$transporter.getMail($mailInfo[0].number).from
```

## .getMailInfo()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R2   | Adicionado |

</details>

<!-- REF #POP3TransporterClass.getMailInfo().Syntax -->**.getMailInfo**( *msgNumber* : Integer ) : Object<!-- END REF -->

<!-- REF #POP3TransporterClass.getMailInfo().Params -->

| Parâmetro  | Tipo    |                             | Descrição                       |
| ---------- | ------- | :-------------------------: | ------------------------------- |
| msgNumber  | Integer |              ->             | Número da mensagem que na lista |
| Resultados | Object  | <- | mailInfo object                 |

<!-- END REF -->

##### Descrição

A função `.getMailInfo()` <!-- REF #POP3TransporterClass.getMailInfo().Summary -->retorna um objeto `mailInfo` correspondente ao *msgNumber* na caixa de correio designada pelo [`transporter POP3`](#pop3-transporter-object)<!-- END REF -->. Essa função permite que recupere informação sobre o email.

Passe em *msgNumber* o número da mensagem a recuperar. Esse número é retornado na propriedade number pelo método [`.getMailInfoList()`](#getmailinfolist).

O objeto `mailInfo` retornado contém as funcionalidades abaixo:

| Propriedade | Tipo   | Descrição                    |
| ----------- | ------ | ---------------------------- |
| size        | Number | Tamanho da mensagem em bytes |
| id          | Text   | ID única da mensagem         |

O método retorna **Null** se:

- *msgNumber* determina uma mensagem não existente,
- a mensagem foi marcada para apagar usando `.delete( )`.

##### Exemplo

```4d
 var $server; $mailInfo : Object
 var $mailNumber : Integer

 $server.host:="pop.gmail.com" //Obrigatório
 $server.port:=995
 $server.user:="4d@gmail.com"
 $server.password:="XXXXXXXX"

 var $transporter : 4D.POP3Transporter
 $transporter:=POP3 New transporter($server)

  //informações da mensagem
 $mailInfo:=$transporter.getMailInfo(1) //receber a primeira correspondência
 If($mailInfo #Null)
    ALERT("First mail size is:"+String($mailInfo.size)+" bytes.")
 End if
```

## .getMailInfoList()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R2   | Adicionado |

</details>

<!-- REF #POP3TransporterClass.getMailInfoList().Syntax -->**.getMailInfoList()** : Collection<!-- END REF -->

<!-- REF #POP3TransporterClass.getMailInfoList().Params -->

| Parâmetro  | Tipo       |                             | Descrição                     |
| ---------- | ---------- | :-------------------------: | ----------------------------- |
| Resultados | Collection | <- | Coleção de objetos `mailInfo` |

<!-- END REF -->

##### Descrição

A função `.getMailInfoList()` <!-- REF #POP3TransporterClass.getMailInfoList().Summary --> retorna uma coleção de objetos `mailInfo` descrevendo todas as mensagens na caixa de correio designada pelo [`transporter POP3 `](#pop3-transporter-object)<!-- END REF -->. Essa função permite gerenciar localmente a lista de mensagens localizadas no servidor POP3.

Cada objeto `mailInfo` na coleção retornada contém as propriedades abaixo:

| Propriedade                                                                      | Tipo   | Descrição                                                                         |
| -------------------------------------------------------------------------------- | ------ | --------------------------------------------------------------------------------- |
| \[ ].size   | Number | Tamanho da mensagem em bytes                                                      |
| \[ ].number | Number | Número da mensagem                                                                |
| \[ ].id     | Text   | ID único da mensagem (útil se armazenar a mensagem localmente) |

Se a mailbox não conter uma mensagem, uma coleção vazia é retornada.

#### número e propriedades ID

*number* é o número de uma mensagem no mailbox no momento em que`POP3_transporter` for criado. A propriedade *number* não é um valor estático em relação a qualquer mensagem específica e vai mudar de sessão a sessão dependendo de sua relação com outras mensagens no mailibox na hora em que a sessão for aberta. Os números atribuídos às mensagens só são válidos durante o tempo de vida do objeto [`POP3_transporter`](#pop3-transporter-object). No momento em que `POP3_transporter` for apagado qualquer mensagem marcada para ser apagada será removida. Quando o usuário se registrar de volta no servidor, as mensagens atuais no mailbox serão numeradas de 1 a x.

Entretanto, *id* é um número único atribuído à mensagem quando for recebida pelo servidor. Esse número é calculado usando a hora e data que a mensagem for recebida e é um valor atribuído ao seu servidor POP3. Infelizmente, servidores POP3 não usam a referência primária *id* para suas mensagens. Através das sessões POP3 precisa especificar o *number* como a referência às mensagens no servidor. Desenvolvedores podem precisar ter cuirdado se desenvolverem soluções que trazem referências às mensagens na database mas deixam o corpo da mensagem no servidor.

##### Exemplo

Se quiser saber o número total e tamanho dos emails nas mailbox:

```4d
 var $server : Object
 $server:=New object
 $server.host:="pop.gmail.com" //Obrigatório
 $server.port:=995
 $server.user:="4d@gmail.com"
 $server.password:="XXXXXXXX"

 var $transporter : 4D.POP3Transporter
 $transporter:=POP3 New transporter($server)

 C_COLLECTION($mailInfo)
 C_LONGINT($vNum;$vSize)

 $mailInfo:=$transporter.getMailInfoList()
 $vNum:=$mailInfo.length
 $vSize:=$mailInfo.sum("size")

 ALERT("The mailbox contains "+String($vNum)+" message(s) for "+String($vSize)+" bytes.")
```

## .getMIMEAsBlob()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R3   | Adicionado |

</details>

<!-- REF #POP3TransporterClass.getMIMEAsBlob().Syntax -->**.getMIMEAsBlob**( *msgNumber* : Integer ) : Blob<!-- END REF -->

<!-- REF #POP3TransporterClass.getMIMEAsBlob().Params -->

| Parâmetro  | Tipo    |                             | Descrição                                      |
| ---------- | ------- | :-------------------------: | ---------------------------------------------- |
| msgNumber  | Integer |              ->             | Número da mensagem que na lista                |
| Resultados | Blob    | <- | Blob da string MIME retornado do servidor mail |

<!-- END REF -->

##### Descrição

A função `.getMIMEAsBlob()` <!-- REF #POP3TransporterClass.getMIMEAsBlob().Summary -->retorna um BLOB contendo o conteúdo MIME da mensagem correspondente ao *msgNumber* na caixa de correio designada pelo [`POP3_transportter`](#pop3-transporter-object)<!-- END REF -->.

Passe em *msgNumber* o número da mensagem a recuperar. Esse número é retornado na propriedade number pelo método [`.getMailInfoList()`](#getmailinfolist).

O método retorna uma BLOB vazia se:

- *msgNumber* determina uma mensagem não existente,
- a mensagem foi marcada para apagar usando `.delete()`.

**BLOB devolvido**

`.getMIMEAsBlob()` retorna um `BLOB` que pode ser arquivado em um banco de dados ou convertido a um objeto [`Email`](EmailObjectClass.md#email-object) com o comando `MAIL Convert from MIME`.

##### Exemplo

Se quiser saber o número total e tamanho dos emails nas mailbox:

```4d
 var $server : Object
 var $mailInfo : Collection
 var $blob : Blob
 var $transporter : 4D.POP3Transporter

 $server:=New object
 $server.host:="pop.gmail.com"
 $server.port:=995
 $server.user:="4d@gmail.com"
 $server.password:="XXXXXXXX"

 $transporter:=POP3 New transporter($server)

 $mailInfo:=$transporter.getMailInfoList()
 $blob:=$transporter.getMIMEAsBlob($mailInfo[0].number)
```

<!-- INCLUDE transporter.host.Desc -->

<!-- INCLUDE transporter.logFile.Desc -->

<!-- INCLUDE transporter.port.Desc -->

<!-- REF POP3TransporterClass.undeleteAll().Desc -->

## .undeleteAll()

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 18 R2   | Adicionado |

</details>

<!-- REF #POP3TransporterClass.undeleteAll().Syntax -->**.undeleteAll()**<!-- END REF -->

<!-- REF #POP3TransporterClass.undeleteAll().Params -->

| Parâmetro | Tipo |     | Descrição                  |
| --------- | ---- | :-: | -------------------------- |
|           |      |     | Não exige nenhum parâmetro |

<!-- END REF -->

##### Descrição

A função `.undeleteAll()` <!-- REF #POP3TransporterClass.undeleteAll().Summary -->remove todos os sinalizadores de exclusão definidos nos e-mails no [`POP3_transporter`](#pop3-transporter-object)<!-- END REF -->.

<!-- END REF -->

<!-- INCLUDE transporter.user.Desc -->
