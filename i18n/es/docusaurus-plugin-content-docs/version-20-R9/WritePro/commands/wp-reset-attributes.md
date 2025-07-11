---
id: wp-reset-attributes
title: WP RESET ATTRIBUTES
displayed_sidebar: docs
---

<!--REF #_command_.WP RESET ATTRIBUTES.Syntax-->**WP RESET ATTRIBUTES** ( *targetObj* ; *attribName* {; *attribName2* ; ... ; *attribNameN*} )<br/> **WP RESET ATTRIBUTES** ( *sectionOrSubsection* {; *attribName* }{; *attribName2* ; ... ; *attribNameN*} )<br/>**WP RESET ATTRIBUTES** ( *targetObj* ; *attribColl* )<br/> **WP RESET ATTRIBUTES** ( *sectionOrSubsection* {; *attribColl*})<!-- END REF-->

<!--REF #_command_.WP RESET ATTRIBUTES.Params-->

| Parámetros          | Tipo       |                             | Descripción                                         |
| ------------------- | ---------- | --------------------------- | --------------------------------------------------- |
| targetObj           | Object     | &#8594; | Rango o elemento o documento 4D Write Pro           |
| sectionOrSubsection | Object     | &#8594; | Sección o subsección de un documento 4D Write Pro   |
| attribName          | Text       | &#8594; | Nombre de atributo(s) a eliminar |
| attribColl          | Collection | &#8594; | Colección de atributos a eliminar                   |

<!-- END REF-->

## Descripción

El comando **WP RESET ATTRIBUTES** <!--REF #_command_.WP RESET ATTRIBUTES.Summary--> le permite restablecer el valor de uno o más atributos en el rango, elemento o documento pasado como parámetro.<!-- END REF--> This command can remove any kind of 4D Write Pro internal attribute: character, paragraph, document, table, or image. You can pass the attribute name to be reset in *attribName* or you can pass a collection of attributes in *attribColl* to reset multiple attributes at once.

> In the case of a section or a subsection, the *sectionOrSubsection* object can be passed alone and all the attributes are reset at once.

En el parámetro *targetObj*, puede pasar cualquiera de los dos:

- un rango, o
- un elemento (encabezado / pie de página / cuerpo / tabla / párrafo / imagen anclada / sección / subsección / hoja de estilo), o
- un documento 4D Write Pro

Cuando se elimina un valor de atributo mediante el comando **WP RESET ATTRIBUTES**, se aplica el valor por defecto a *targetObj* o *sectionOrSubsection*. Los valores por defecto aparecen en la sección *4D Write Pro Attributes*.

:::note Notas

- Cuando se aplica **WP RESET ATTRIBUTES** a un objeto sección/subsección, los atributos se heredan de la sección o documento padre.
- Cuando se aplica **WP RESET ATTRIBUTES** a un objeto de hoja de estilo, los atributos se eliminan de la hoja de estilo a menos que sea la hoja de estilo por defecto ("Normal"). En este caso, se aplica al atributo el valor por defecto (la hoja de estilo "Normal" define todos los atributos de la hoja de estilo).
- Cuando *sectionOrSubsection* no es una sección ni una subsección y no se proporciona ningún atributo, se produce un error.

:::

Si el atributo a restablecer no estaba definido en el elemento pasado como parámetro, el comando no hace nada.

## Ejemplo 1

Desea eliminar varios atributos de la siguiente selección:

![](../../assets/en/WritePro/commands/pict2643861.en.png)

Puede ejecutar:

```4d
 $range:=WP Get selection(*;"WParea")
 WP RESET ATTRIBUTES($range;wk padding)
 WP RESET ATTRIBUTES($range;wk background color)
 WP RESET ATTRIBUTES($range;wk text underline style)
 WP RESET ATTRIBUTES($range;wk margin)
 WP RESET ATTRIBUTES($range;wk border style)
```

El documento resultante es:

![](../../assets/en/WritePro/commands/pict2643863.en.png)

## Ejemplo 2

Desea eliminar varios atributos utilizando una colección:

```4d
$myRange:=WP Get selection(*;"WParea")
$myCollection:=New collection(wk font size; wk background color; wk border style)
WP RESET ATTRIBUTES($myRange; $myCollection)
 
```

## Ejemplo 3

```4d
$section:=WP Get section($document; 3)
WP RESET ATTRIBUTES($section) // Se eliminan todos los atributos de la sección
$subSection:=WP Get subsection(WP Get section($document; 3); wk left page)
WP RESET ATTRIBUTES($subSection) // Se eliminan todos los atributos de la subsección
```

## Ver también

*4D Write Pro Attributes*\
[WP GET ATTRIBUTES](wp-get-attributes.md)\
[WP SET ATTRIBUTES](wp-set-attributes.md)
