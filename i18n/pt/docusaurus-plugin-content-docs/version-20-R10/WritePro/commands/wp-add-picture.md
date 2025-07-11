---
id: wp-add-picture
title: WP Add picture
displayed_sidebar: docs
---

<!--REF #_command_.WP Add picture.Syntax-->**WP Add picture** ( *wpDoc* {; *picture*} ) : Object<br/>**WP Add picture** ( *wpDoc* {; *picturePath*} ) : Object<br/>**WP Add picture** ( *wpDoc* {; *pictureFileObj*} ) : Object<!-- END REF-->

<!--REF #_command_.WP Add picture.Params-->

| Parâmetro      | Tipo                     |                             | Descrição                                                  |
| -------------- | ------------------------ | --------------------------- | ---------------------------------------------------------- |
| wpDoc          | Object                   | &#8594; | Documento 4D Write Pro                                     |
| picture        | Imagem                   | &#8594; | Imagem 4D                                                  |
| picturePath    | Text                     | &#8594; | Picture path                                               |
| pictureFileObj | 4D. File | &#8594; | 4D.File object representing a picture file |
| Resultado      | Object                   | &#8592; | Object referencing the picture                             |

<!-- END REF-->

## Descrição

O comando **WP Adicionar imagem** <!--REF #_command_.WP Adicionar imagem. ummary--> ancora a imagem passada como parâmetro em um local fixo dentro do *wpDoc* especificado e retorna sua referência.<!-- END REF--> A referência retornada pode ser passada para o comando [WP SET ATTRIBUTES](wp-set-attributes.md) para mover a imagem para qualquer local em *wpDoc* (página, seção, cabeçalho, rodapé, etc.) with a defined layer, size, etc.

Em *wpDoc*, passe o nome de um objeto documento 4D Write Pro.

For the optional second parameter, you can pass either:

- Em *picture*:  uma imagem 4D
- In *picturePath*:  A string containing a path to a picture file stored on disk (system syntax). You can pass a full pathname, or a pathname relative to the database structure file. You can also pass a file name, in which case the file must be located next to the database structure file. If you pass a file name, you need to indicate the file extension.
- Em *PictureFileObj*: um objeto `4D.File` que representa um arquivo imagem.

:::note

Qualquer formato imagem [suportado por 4D](../../FormEditor/pictures.md#native-formats-supported) pode ser usado. Você pode obter a lista de formatos de imagens disponíveis usando o comando [PICTURE CODEC LIST](../../commands-legacy/picture-codec-list.md). If the picture encapsulates several formats (codecs), 4D Write Pro only keeps one format for display and one format for printing (if different) in the document; the "best" formats are automatically selected.

:::

- Se *imagem* for omitida, uma referência de imagem válida é retornada, e uma imagem vazia é adicionada. Isto permite que você chame [WP SET ATTRIBUTES](wp-set-attributes.md) com o seletor wk image expression para preencher a imagem com uma expressão 4D. If the expression can not be evaluated or does not return a valid picture, an empty image (default black frame image) is displayed.

By default, the added picture is:

- Embedded behind the text
- Displayed at the top left corner of the paper box
- Exibido em todas as páginas

The location, layer (inline, in front/behind text), visibility, and any properties of picture can be modified using the [WP SET ATTRIBUTES](wp-set-attributes.md) command, or via standard actions (see *Using 4D Write Pro standard actions*).

**Nota:** o comando [WP Selection range](../commands-legacy/wp-selection-range.md) retorna um objeto *referência de imagem* se uma imagem ancorada for selecionada e um objeto *alcance* se uma imagem em linha for selecionada. Você pode determinar se um objeto selecionado é um objeto imagem verificando o atributo `wk type`:

- **Value = 2**: o objeto selecionado é um objeto imagem.
- **Value = 0**: o objeto selecionado é um objeto intervalo.

## Exemplo 1

You want to add a picture with default settings using a filepath.

```4d
 var $obPict : Object
 $obPict:=WP Add picture(myDoc;"/PACKAGE/Pictures/Saved Pictures/Sunrise.jpg")
```

O resultado é:

![](../../assets/en/WritePro/commands/pict3617325.en.png)

## Exemplo 2

You want to add a resized picture, centered and anchored to the header:

```4d
 var $obImage : Object
 var $myPictureFile : 4D.File

 $myPictureFile:=File("/PACKAGE/Pictures/Saved Pictures/Sunrise.jpg")
 $obImage:=WP Add picture(myDoc;$myPictureFile)
 WP SET ATTRIBUTES($obImage;wk anchor origin;wk header box)
 WP SET ATTRIBUTES($obImage;wk anchor horizontal align;wk center)
 WP SET ATTRIBUTES($obImage;wk anchor vertical align;wk center)
 WP SET ATTRIBUTES($obImage;wk width;"650px";wk height;"120px")
```

O resultado é:

![](../../assets/en/WritePro/commands/pict3617351.en.png)

## Exemplo 3

You want to use a field expression to add an anchored image to a document displaying some text from the database:

```4d
 QUERY([Flowers];[Flowers]Common_Name="tulip")
 WP SET TEXT(myDoc;[Flowers]Description;wk append) //inserir texto
 var $obImage : Object
 $obImage:=WP Add picture(myDoc)
 WP SET ATTRIBUTES($obImage;wk image formula;Formula([Flowers]Image))
```

![](../../assets/en/WritePro/commands/pict3841719.en.png)

## Veja também

[WP DELETE PICTURE](../commands-legacy/wp-delete-picture.md)</br>
[WP Picture range](../commands-legacy/wp-picture-range.md)