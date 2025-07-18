---
id: set-window-document-icon
title: SET WINDOW DOCUMENT ICON
displayed_sidebar: docs
---

<!--REF #_command_.SET WINDOW DOCUMENT ICON.Syntax-->**SET WINDOW DOCUMENT ICON** ( *winRef* )<br/>**SET WINDOW DOCUMENT ICON** ( *winRef* ; *image* )<br/>**SET WINDOW DOCUMENT ICON** ( *winRef* ; *file* )<br/>**SET WINDOW DOCUMENT ICON** (  *winRef* ; *image* ; *file* )<!-- END REF-->

<!--REF #_command_.SET WINDOW DOCUMENT ICON.Params-->

| Parâmetro | Tipo                                               |                             | Descrição                              |
| --------- | -------------------------------------------------- | --------------------------- | -------------------------------------- |
| winRef    | Integer                                            | &#8594; | Número de referência da janela         |
| image     | Imagem                                             | &#8594; | Ícone personalizado                    |
| file      | 4D.File, 4D.Folder | &#8594; | Caminho do arquivo ou caminho da pasta |

<!-- END REF-->

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 20 R7   | Adicionado |

</details>

## Descrição

The `SET WINDOW DOCUMENT ICON` command <!--REF #_command_.SET WINDOW DOCUMENT ICON.Summary-->allows you to define an icon for windows in multi-window applications using either an *image* and/or *file* with the window reference *winRef*<!-- END REF-->. The icon will be visible within the window itself and on the windows taskbar to help users identify and navigate different windows.

No caso de uma aplicação MDI no Windows, você pode passar `-1` no *winRef* para definir o ícone da janela principal. Em outros contextos (macOS ou [aplicação SDI](../Menus/sdi.md) no Windows), usar -1 não faz nada.

- If only *file* is passed, the window uses the icon corresponding to the file type and the file’s path is displayed in the window’s menu.
- If only *image* is passed, 4D does not show the path and the passed image is used for the window icon.
- If both *file* and *image* are passed, the file’s path is displayed in the window’s menu and the passed image is used for the window icon.
- If only *winRef* is passed or *image* is empty, the icon is removed on macOS and the default icon is displayed on Windows (application icon).

## Exemplo

In this example, we want to create four windows:

1. Use the application icon on Windows and no icon on macOS (default state when no *image* or *file* is used).
2. Use um ícone "user".
3. Associate a document with the window (this uses its file type icon).
4. Customize the icon associated with the document.

```4d
 var $winRef : Integer
 var $userImage : Picture
 var $file : 4D.File
 
  // 1- Open "Contact" form
 $winRef:=Open form window("Contact";Plain form window+Form has no menu bar)
 SET WINDOW DOCUMENT ICON($winRef)
 DIALOG("Contact";*)
 
  // 2- Open "Contact" form with "user" icon
 $winRef:=Open form window("Contact";Plain form window+Form has no menu bar)
 BLOB TO PICTURE(File("/RESOURCES/icon/user.png").getContent();$userImage)
 SET WINDOW DOCUMENT ICON($winRef;$userImage)
 DIALOG("Contact";*)
 
  // 3- Open "Contact" form associated with the document "user"
 $winRef:=Open form window("Contact";Plain form window+Form has no menu bar)
 $file:=File("/RESOURCES/files/user.txt")
 SET WINDOW DOCUMENT ICON($winRef;$file)
 DIALOG("Contact";*)
 
  // 4- Open "Contact" form associated with the document "user" with "user" icon
 $winRef:=Open form window("Contact";Plain form window+Form has no menu bar)
 BLOB TO PICTURE(File("/RESOURCES/icon/user.png").getContent();$userImage)
 $file:=File("/RESOURCES/files/user.txt")
 SET WINDOW DOCUMENT ICON($winRef;$userImage;$file)
 DIALOG("Contact";*)

```

## Veja também

[Create entity selection](create-entity-selection.md)