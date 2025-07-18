---
id: propertiesHelp
title: Ayuda
---

## Mensaje de ayuda

Esta propiedad permite asociar los mensajes de ayuda a los objetos activos de sus formularios. Se pueden mostrar en ejecución:

![](../assets/en/FormObjects/property_helpTip.png)

> - El retardo de la visualización y la duración máxima de los mensajes de ayuda pueden controlarse utilizando los selectores `Tips delay` y `Tips duration` del comando **[SET DATABASE PARAMETER](../commands-legacy/set-database-parameter.md)**.
> - Los mensajes de ayuda se pueden deshabilitar o habilitar globalmente para la aplicación utilizando el selector del comando [**SET DATABASE PARAMETER**](../commands-legacy/set-database-parameter.md).

Puede:

- designar un mensajes de ayuda existente, previamente especificado en el editor de [mensajes de ayuda](https://doc.4d.com/4Dv20/4D/20.2/Help-tips.200-6750100.en.html) de 4D.
- o introducir el mensaje de ayuda directamente como una cadena. Esto le permite aprovechar la arquitectura XLIFF. Aquí puede introducir una referencia XLIFF para mostrar un mensaje en el lenguaje de la aplicación (para más información sobre XLIFF, consulte el [Apéndice B: Arquitectura XLIFF](https://doc.4d.com/4Dv20/4D/20.2/Appendix-B-XLIFF-architecture.300-6750166.en.html). También puede utilizar referencias 4D ([ver Uso de referencias en texto estático](https://doc.4d.com/4Dv20/4D/20.2/Using-references-in-static-text.300-6750154.en.html)).

> &#062; In macOS, displaying help tips is not supported in pop-up type windows.

#### Gramática JSON

|  Nombre | Tipos de datos | Valores posibles                             |
| :-----: | :------------: | -------------------------------------------- |
| tooltip |      text      | información adicional para ayudar al usuario |

#### Objetos soportados

[Botón](button_overview.md) - [Rejilla de botones](buttonGrid_overview.md) - [Casilla de verificación](checkbox_overview.md)  - [Lista desplegable](dropdownList_Overview.md) - [Combo Box](comboBox_overview.md) - [Lista jerárquica](list_overview.md) - [Encabezado de lista de List Box](listbox_overview.md#list-box-headers) - [Pie de lista de List Box](listbox_overview.md#list-box-footers) - [Botón imagen](pictureButton_overview.md) - [Menú emergente con imagen](picturePopupMenu_overview.md) - [Botón de opción](radio_overview.md)

#### Otras funcionalidades de ayuda

También puede asociar los mensajes de ayuda a los objetos formulario de otras dos maneras:

- a nivel de la estructura de la base de datos (sólo campos). En este caso, la ayuda del campo se muestra en todos los formularios en los que aparece. Para más información, consulte "Consejos de ayuda" en [Propiedades de los campos](https://doc.4d.com/4Dv20/4D/20.2/Field-properties.300-6750280.en.html#3367486).
- utilizando el comando **[OBJECT SET HELP TIP](../commands-legacy/object-set-help-tip.md)**, para el proceso actual.

Cuando se asocian consejos diferentes a un mismo objeto en varias ubicaciones, se aplica el siguiente orden de prioridad:

1. nivel de estructura (prioridad más baja)
2. editor de formulario
3. Comando **[OBJECT SET HELP TIP](../commands-legacy/object-set-help-tip.md)** (alta prioridad)

#### Comandos

[`OBJECT Get help tip`](../commands-legacy/object-get-help-tip.md) - [`OBJECT SET HELP TIP`](../commands-legacy/object-set-help-tip.md)

#### Ver también

[Marcador de posición](properties_Entry.md#placeholder)
