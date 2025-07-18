---
id: propertiesObject
title: Objetos
---

---

## Tipo

`PARÁMETRO OBLIGATORIO`

Esta propiedad designa el tipo del [objeto formulario activo o inactivo](formObjects_overview.md).

#### Gramática JSON

| Nombre | Tipos de datos | Valores posibles                                                                                                                                                                                                                                                                                         |
| ------ | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type   | string         | "button", "buttonGrid", "checkbox", "combo", "dropdown", "groupBox", "input", "line", "list", "listbox", "oval", "picture", "pictureButton", "picturePopup", "plugin", "progress", "radio", "rectangle", "ruler", "spinner", "splitter", "stepper", "subform", "tab", "text", "view", "webArea", "write" |

#### Objetos soportados

[Área 4D View Pro](viewProArea_overview.md) - [Área 4D Write Pro](writeProArea_overview.md) - [Botón](button_overview.md) - [Rejilla de botones](buttonGrid_overview.md) - [Casilla de verificación](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Lista desplegable](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Lista jerárquica](list_overview.md) - [List Box](listbox_overview.md) - [Columna List Box](listbox_overview.md#list-box-columns) - [Pie de List Box](listbox_overview.md#list-box-footers) - [Encabezado de List Box](listbox_overview.md#list-box-headers) - [Botón imagen](pictureButton_overview.md) - [Menú emergente con imagen](picturePopupMenu_overview.md) - [Área de Plug-in](pluginArea_overview.md) - [Indicador de progreso](progressIndicator.md) - [Botón de opción](radio_overview.md) - [Spinner](spinner.md) - [Separador](splitters.md) - [Imagen estática](staticPicture.md) - [Pasos](stepper.md) - [Subformulario](subform_overview.md) - [Control de pestañas](tabControl.md) - [Área de texto](text.md) - [Área web](webArea_overview.md)

---

## Nombre del objeto

Cada objeto de formulario activo está asociado a un nombre de objeto. Cada nombre de objeto debe ser único.

> Los nombres de objetos están limitados a un tamaño de 255 bytes.

Al utilizar el lenguaje de 4D, puede referirse a un objeto formulario activo por su nombre de objeto (ver los comandos [Object (Forms)](../category/object-forms)).

Para más información sobre las reglas de denominación de los objetos de formulario, consulte la sección [Identificadores](Concepts/identifiers.md).

#### Gramática JSON

| Nombre | Tipos de datos | Valores posibles                                                 |
| ------ | -------------- | ---------------------------------------------------------------- |
| name   | string         | Todo nombre permitido que no pertenezca a un objeto ya existente |

#### Objetos soportados

[Área 4D View Pro](viewProArea_overview.md) - [Área 4D Write Pro](writeProArea_overview.md) - [Botón](button_overview.md) - [Rejilla de botones](buttonGrid_overview.md) - [Casilla de verificación](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Lista desplegable](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Lista jerárquica](list_overview.md#overview) - [List Box](listbox_overview.md#overview) - [Columna List Box](listbox_overview.md#list-box-columns) - [Pie de List Box](listbox_overview.md#list-box-footers) - [Encabezado List Box](listbox_overview.md#list-box-headers) - [Botón con imagen](pictureButton_overview.md) - [Menú emergente con imagen](picturePopupMenu_overview.md) - [Área de Plug-in](pluginArea_overview.md#overview) - [Indicador de progreso](progressIndicator.md) - [Selector](spinner.md) - [Separador](splitters.md) - [Imagen estática](staticPicture.md) - [Pasos](stepper.md) - [Botón de opción](radio_overview.md) - [Subformulario](subform_overview.md#overview) - [Control de pestañas](tabControl.md) - [Área de texto](text.md) - [Área web](webArea_overview.md)

---

## Guardar valor

Esta propiedad está disponible cuando la opción [Guardar geometría](FormEditor/properties_FormProperties.md#save-geometry) está marcada para el formulario.

Esta funcionalidad sólo es soportada con los objetos que contribuyen a la geometría general del formulario. Por ejemplo, esta opción está disponible para las casillas de verificación porque su valor puede utilizarse para ocultar o mostrar áreas adicionales en la ventana.

Esta es la lista de objetos cuyo valor se puede guardar:

| Object                                          | Valor guardado                                                                                              |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| [Casilla de verificación](checkbox_overview.md) | Valor de la variable asociada (0, 1, 2)                                                  |
| [Lista desplegable](dropdownList_Overview.md)   | Número de línea seleccionada                                                                                |
| [Botón de radio](radio_overview.md)             | Valor de la variable asociada (1, 0, True o False para los botones de acuerdo a su tipo) |
| [Control de pestañas](tabControl.md)            | Número de pestaña seleccionada                                                                              |

#### Gramática JSON

| Nombre        | Tipos de datos | Valores posibles |
| ------------- | -------------- | ---------------- |
| memorizeValue | boolean        | true, false      |

#### Objetos soportados

[Casilla de selección](checkbox_overview.md) - [Lista desplegable](dropdownList_Overview.md) - [Botón de radio](radio_overview.md) - [Control de pestañas](tabControl.md)

---

## Variable o expresión

> Ver también **[Expression](properties_DataSource.md#expression)** para las columnas de list box de tipo selección y colección.

Esta propiedad especifica la fuente de los datos. Cada objeto de formulario activo está asociado a un nombre de objeto y a un nombre de variable. El nombre de la variable puede ser diferente del nombre del objeto. En el mismo formulario, puede utilizar la misma variable varias veces, mientras que cada [nombre de objeto](#object-name) debe ser único.

> El tamaño del nombre de la variable está limitado a 31 bytes. Consulte la sección [Identificadores](Concepts/identifiers.md) para obtener más información sobre las reglas de asignación de nombres.

Las variables de los objetos del formulario permiten controlar y supervisar los objetos. Por ejemplo, cuando se presiona un botón, su variable se pone en 1; el resto del tiempo, en 0. La expresión asociada a un indicador de progreso permite leer y modificar el parámetro actual.

Las variables o expresiones se pueden introducir o no y pueden recibir datos de tipo Texto, Entero, Numérico, Fecha, Hora, Imagen, Booleano u Objeto.

#### Gramática JSON

| Nombre     | Tipos de datos            | Valores posibles                                                                                                                                                                                                                                          |
| ---------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataSource | cadena o array de cadenas | <li>4D variable, field name, or any expression.</li><li>Empty string for [dynamic variables](#dynamic-variables).</li><li>String array (collection of array names) for a [hierarchical listbox](listbox_overview.md#hierarchical-list-boxes) column]</li> |

### Expresiones

Puede utilizar una [expresión](Concepts/quick-tour.md#expressions) como fuente de datos para un objeto. Se permite toda expresión 4D válida: expresión simple, propiedad de objeto, fórmula, función 4D, nombre de método proyecto o campo que utilice la sintaxis estándar `[Table]Field`. La expresión se evalúa cuando se ejecuta el formulario y se reevalúa para cada evento del formulario. Tenga en cuenta que las expresiones pueden ser [asignables o no asignables](Concepts/quick-tour.md#expressions).

> Si el valor introducido corresponde a la vez a un nombre de variable y a un nombre de método, 4D considera que está indicando el método.

### Variables dinámicas

Puede dejarle a 4D crear variables asociadas con los objetos de su formulario (botones, variables editables, casillas de verificación, etc.) dinámicamente y de acuerdo a sus necesidades. Para ello, basta con dejar en blanco la propiedad "Variable o expresión" (o el campo JSON de `dataSource`).

Cuando una variable no tiene nombre, al cargar el formulario, 4D crea una nueva variable para el objeto, con un nombre calculado que es único en el espacio de las variables de proceso del intérprete (lo que significa que este mecanismo puede utilizarse incluso en modo compilado). Esta variable temporal se destruirá cuando se cierre el formulario.

Obtener o definir el valor de los objetos del formulario que utilizan variables dinámicas, solo necesita llamar a los comandos [`OBJECT Get value`](../commands-legacy/object-get-value.md) y [`OBJECT SET VALUE`](../commands-legacy/object-set-value.md). Por ejemplo:

```4d
 var $value : Variant
 $value:=OBJECT Get value("comments")
 OBJECT SET VALUE("comments";$value+10) 
```

### List box array

Para un list box array, la propiedad **Variable o Expresión** normalmente contiene el nombre de la variable array definida para el list box y para cada columna. Sin embargo, puede utilizar un array de cadenas (que contenga nombres de arrays) como *dataSource* valor de una columna list box para definir un [list box jerárquico](listbox_overview.md#hierarchical-list-boxes).

#### Objetos soportados

[Área 4D View Pro](viewProArea_overview.md) - [Área 4D Write Pro](writeProArea_overview.md) - [Botón](button_overview.md) - [Rejilla de botones](buttonGrid_overview.md) - [Casilla de verificación](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Lista desplegable](dropdownList_Overview.md) - [Lista jerárquica](list_overview.md) - [List Box](listbox_overview.md) - [Columna List Box](listbox_overview.md#list-box-columns) - [Encabezado List Box](listbox_overview.md#list-box-headers) - [Pie de List Box](listbox_overview.md#list-box-footers) - [Menú emergente con imagen](picturePopupMenu_overview.md) - [Área de Plug-in](pluginArea_overview.md) - [Indicador de progreso](progressIndicator.md) - [Botón de opción](radio_overview.md) - [Selector](spinner.md) - [Separador](splitters.md) - [Pasos](stepper.md) - [Subformulario](subform_overview.md) - [Control de pestañas](tabControl.md) - [Área web](webArea_overview.md)

---

## Tipo de expresión

> Esta propiedad se denomina [**Tipo de datos**](properties_DataSource.md#data-type-expression-type) en la Lista de propiedades para [selección](listbox_overview.md#selection-list-boxes) y [colección](listbox_overview.md#collection-or-entity-selection-list-boxes) y para [Listas desplegables](dropdownList_Overview.md) asociadas a un [objeto](FormObjects/dropdownList_Overview.md#using-an-object) o un [array](FormObjects/dropdownList_Overview.md#using-an-array).

Especifique el tipo de datos para la expresión o variable asociada al objeto. Tenga en cuenta que el objetivo principal de este ajuste es configurar las opciones (como los formatos de visualización) disponibles para el tipo de datos. En realidad, no escribe la variable en sí. De cara a la compilación del proyecto, debe [declarar la variable](Concepts/variables.md#declaring-variables).

Sin embargo, esta propiedad tiene una función tipográfica en los siguientes casos específicos:

- **[Variables dinámicas](#dynamic-variables)**: puede utilizar esta propiedad para declarar el tipo de variables dinámicas.
- **[Columnas List Box ](listbox_overview.md#list-box-columns)**: esta propiedad se utiliza para asociar un formato de visualización a los datos de la columna. Los formatos suministrados dependerán del tipo de variable (list box de tipo array) o del tipo dato/campo (list boxes de tipo selección y colección). Los formatos 4D estándar que pueden utilizarse son: Alfa, Numérico, Fecha, Hora, Imagen y Booleano. El tipo Texto no tiene formatos de visualización específicos. Todos los formatos personalizados existentes también están disponibles.
- **[Variables imagen](input_overview.md)**: puede utilizar este menú para declarar las variables antes de cargar el formulario en modo interpretado. Mecanismos nativos específicos rigen la visualización de variables de imagen en los formularios. Estos mecanismos exigen una mayor precisión a la hora de configurar las variables: a partir de ahora, deberán haber sido declaradas antes de cargar el formulario -es decir, incluso antes del evento de formulario `On Load` - a diferencia de otros tipos de  Estos mecanismos exigen una mayor precisión a la hora de configurar las variables: a partir de ahora, deberán haber sido declaradas antes de cargar el formulario -es decir, incluso antes del evento de formulario `On Load` - a diferencia de otros tipos de  Estos mecanismos exigen una mayor precisión a la hora de configurar las variables: a partir de ahora, deberán haber sido declaradas antes de cargar el formulario -es decir, incluso antes del evento de formulario `On Load` - a diferencia de otros tipos de  To do this, you need either for the statement `var varName : Picture` to have been executed before loading the form (typically, in the method calling the `DIALOG` command), or for the variable to have been typed at the form level using the expression type property.
  De lo contrario, la variable imagen no se mostrará correctamente (sólo en modo interpretado).

#### Gramática JSON

| Nombre             | Tipos de datos | Valores posibles                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------ | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dataSourceTypeHint | string         | **<li>Objetos estándar:** "integer", "boolean", "number", "picture", "text", date", "time", "arrayText", "arrayDate", "arrayTime", "arrayNumber", "collection", "object", "undefined"</li><li>**columnas de lista:** "boolean", "number", "picture", "text", date", "time". *Sólo para Array/selección list box*: "integer", "object"</li> |

#### Objetos soportados

[Casilla de verificación](checkbox_overview.md) - [Cuadro combinado](comboBox_overview.md) - [Lista desplegable](dropdownList_Overview.md) - [Entrada](input_overview.md) - [Columna List Box](listbox_overview.md#list-box-columns) - [Pie List Box](listbox_overview.md#list-box-footers) - [Área de Plug-in](pluginArea_overview.md) - [Indicador de progreso](progressIndicator.md) - [Botón de opción](radio_overview.md) - [Regla](ruler.md) - [Selector](spinner.md) - [Pasos](stepper.md) - [Subformulario](subform_overview.md) - [Control de pestaña](tabControl.md)

---

## Clase CSS

Lista de palabras separadas por espacios que se utilizan como selectores de clase en los [archivos css](FormEditor/createStylesheet.md#style-sheet-files).

#### Gramática JSON

| Nombre | Tipos de datos | Valores posibles                                                          |
| ------ | -------------- | ------------------------------------------------------------------------- |
| class  | string         | Una cadena con los nombres de los CSS separados por caracteres de espacio |

#### Objetos soportados

[Área 4D View Pro](viewProArea_overview.md) - [Área 4D Write Pro](writeProArea_overview.md) - [Botón](button_overview.md) - [Rejilla de botones](buttonGrid_overview.md) - [Casilla de verificación](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Lista desplegable](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Lista jerárquica](list_overview.md) - [List Box](listbox_overview.md) - [Botón imagen](pictureButton_overview.md) - [Menú emergente con imagen](picturePopupMenu_overview.md) - [Área de Plug-in](pluginArea_overview.md) - [Botón de opción](radio_overview.md) - [Imagen estática](staticPicture.md) - [Subformulario](subform_overview.md) - [Área de texto](text.md) - [Área web](webArea_overview.md)

---

## Collection o entity selection

Para utilizar elementos de colección o entidades para definir el contenido de las líneas del list box.

Introduzca una expresión que devuelva una colección o una selección de entidades. Normalmente, introducirá el nombre de una variable, un elemento de una colección o una propiedad que contenga una colección o una selección de entidades.

La colección o la selección de entidades debe estar disponible para el formulario cuando se carga. Cada elemento de la colección o cada entidad de la selección de entidades se asociará a una fila del list box y estará disponible como objeto a través de la palabra clave [`This`](../Concepts/classes.md#this):

- si ha utilizado una colección de objetos, puede llamar a **This** en la expresión de la fuente de datos para acceder a cada valor de propiedad, por ejemplo `This.<propertyPath>`.
- si ha utilizado una selección de entidades, puede llamar a **This** en la expresión de la fuente de datos para acceder a cada valor de atributo, por ejemplo `This.<attributePath>`.

> Si ha utilizado una colección de valores escalares (y no objetos), 4D le permite mostrar cada valor llamando a **This.value** en la expresión datasource. Sin embargo, en este caso no podrá modificar valores ni acceder al objeto actual (ver más adelante).

#### Gramática JSON

| Nombre     | Tipos de datos | Valores posibles                                                                   |
| ---------- | -------------- | ---------------------------------------------------------------------------------- |
| dataSource | string         | Expresión que devuelve una colección o una selección de entidades. |

#### Objetos soportados

[List Box](listbox_overview.md)

---

## Fuente de datos

Especifique el tipo de list box.

![](../assets/en/FormObjects/listbox_dataSource.png)

- **Arrays**(por defecto): utiliza elementos de array como líneas del list box.
- **Selección actual**: utiliza expresiones, campos o métodos cuyos valores se evaluarán para cada registro de la selección actual de una tabla.
- **Selección temporal**: utiliza expresiones, campos o métodos cuyos valores se evaluarán para cada registro de una selección temporal.
- **Colección o Selección de entidades**: utilice elementos de colección o entidades para definir el contenido de las líneas del list box. Tenga en cuenta que con este tipo de list box, debe definir la propiedad [Colección o Selección de entidades](properties_Object.md#collection-or-entity-selection).

#### Gramática JSON

| Nombre      | Tipos de datos | Valores posibles                                            |
| ----------- | -------------- | ----------------------------------------------------------- |
| listboxType | string         | "array", "currentSelection", "namedSelection", "collection" |

#### Objetos soportados

[List Box](listbox_overview.md)

---

## Tipo de plug-in

Nombre del [área externa del plug-in](pluginArea_overview.md) asociada al objeto. Los nombres de las áreas externas del plug-in.se publican en el archivo manifest.json del plug-in.

#### Gramática JSON

| Nombre         | Tipos de datos | Valores posibles                                                                    |
| -------------- | -------------- | ----------------------------------------------------------------------------------- |
| pluginAreaKind | string         | Nombre del área externa del plug-in (comienza con un carácter %) |

#### Objetos soportados

[Área de plugin](pluginArea_overview.md)

---

## Grupo radio

Permite utilizar los botones de radio en conjuntos coordinados: sólo se puede seleccionar un botón a la vez en el conjunto.

#### Gramática JSON

| Nombre     | Tipos de datos | Valores posibles       |
| ---------- | -------------- | ---------------------- |
| radioGroup | string         | Nombre del grupo radio |

#### Objetos soportados

[Botón de radio](radio_overview.md)

---

## Título

Permite insertar una etiqueta en un objeto. Se puede especificar la fuente y el estilo de esta etiqueta.

Puede forzar un retorno de carro en la etiqueta utilizando el caracter \ (barra invertida).

![](../assets/en/FormObjects/property_title.png)

Para insertar un \ en la etiqueta, ingrese "&#92;&#92;".

Por defecto, la etiqueta se coloca en el centro del objeto. Cuando el objeto también contiene un icono, puede modificar la ubicación relativa de estos dos elementos utilizando la propiedad [Posición Título/imagen](properties_TextAndPicture.md#titlepicture-position).

Para la traducción de la aplicación, puede introducir una referencia XLIFF en el área del título de un botón (ver [Apéndice B: arquitectura XLIFF](https://doc.4d.com/4Dv20/4D/20.2/Appendix-B-XLIFF-architecture.300-6750166.en.html)).

#### Gramática JSON

| Nombre | Tipos de datos | Valores posibles |
| ------ | -------------- | ---------------- |
| text   | string         | todo texto       |

#### Objetos soportados

[Botón](button_overview.md) - [Casilla de selección](checkbox_overview.md) - [Encabezado List Box](listbox_overview.md#list-box-headers) - [Botón radio](radio_overview.md) - [ÁreaTexto](text.md)

---

## Cálculo de variables

Esta propiedad define el tipo de cálculo que se realizará en un área [pie de columna](listbox_overview.md#list-box-footers).

> El cálculo de los pies de página también puede establecerse utilizando el comando 4D [`LISTBOX SET FOOTER CALCULATION`](../commands-legacy/listbox-set-footer-calculation.md).

Hay varios tipos de cálculos disponibles. La tabla siguiente muestra los cálculos que se pueden utilizar según el tipo de datos que se encuentran en cada columna e indica el tipo afectado automáticamente por 4D a la variable de pie de página (si no está escrita por el código):

| Cálculo                                    | Num | Text | Fecha | Hora | Bool | Imágenes | tipos de variables de pie de página |
| ------------------------------------------ | --- | ---- | ----- | ---- | ---- | -------- | ----------------------------------- |
| Mínimo                                     | X   | X    | X     | X    | X    |          | Igual que el tipo de columna        |
| Máximo                                     | X   | X    | X     | X    | X    |          | Igual que el tipo de columna        |
| Suma                                       | X   |      |       | X    | X    |          | Igual que el tipo de columna        |
| Conteo                                     | X   | X    | X     | X    | X    | X        | Integer                             |
| Promedio                                   | X   |      |       | X    |      |          | Real                                |
| Desviación estándar(\*) | X   |      |       | X    |      |          | Real                                |
| Varianza(\*)            | X   |      |       | X    |      |          | Real                                |
| Suma de cuadrados(\*)   | X   |      |       | X    |      |          | Real                                |
| Personalizado ("None ") | X   | X    | X     | X    | X    | X        | Cualquiera                          |

(\*) Sólo para list boxes de tipo array.

> Sólo las [variables](Concepts/variables.md) declaradas o dinámicas pueden utilizarse para mostrar los cálculos de pie de página. No se soportan otros tipos de [expresiones](Concepts/quick-tour.md#expressions) como `Form.value`.

Los cálculos automáticos ignoran el estado mostrado/oculto de las líneas list box. Si desea restringir un cálculo sólo a las líneas visibles, debe utilizar un cálculo personalizado.

*Null* no se tienen en cuenta para ningún cálculo.

Si la columna contiene distintos tipos de valores (columna basada en colecciones, por ejemplo):

- Promedio y Suma sólo tienen en cuenta elementos numéricos (se ignoran otros tipos de elementos).
- Mínimo y Máximo devuelven un resultado según el orden habitual de las listas de tipos, tal como se define en la función [collection.sort()](API/CollectionClass.md#sort).

El uso de cálculos automáticos en pies de columnas basados en expresiones tiene las siguientes limitaciones:

- es **soportado** con todos los tipos de list boxes cuando la expresión es "simple" (como `[table]field` o `this.attribute`),
- se **soporta pero no se recomienda** por razones de rendimiento con list boxes colección/selección de entidades cuando la expresión es "compleja" (distinta de `this.attribute`) y el list box contiene un gran número de líneas,
- **no se soporta** con list boxes selección actual/selección temporal cuando la expresión es "compleja". Es necesario utilizar cálculos personalizados.

Cuando está configurado **Personalizado** ("none" en JSON), 4D no realiza cálculos automáticos y debe asignar el valor de la variable en esta área por programación.

#### Gramática JSON

| Nombre              | Tipos de datos | Valores posibles                                                                                      |
| ------------------- | -------------- | ----------------------------------------------------------------------------------------------------- |
| variableCalculation | string         | "none", "minimum", "maximum", "sum", "count", "average", "standardDeviation", "variance", "sumSquare" |

#### Objetos soportados

[Pie de List Box](listbox_overview.md#list-box-footers)
