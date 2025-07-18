---
id: propertiesObject
title: Objects 
---

---

## Type

 `MANDATORY SETTING`

This property designates the type of the [active or inactive form object](formObjects_overview.md).

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|type|string|"button", "buttonGrid", "checkbox", "combo", "dropdown", "groupBox", "input", "line", "list", "listbox", "oval", "picture", "pictureButton", "picturePopup", "plugin", "progress", "radio", "rectangle", "ruler", "spinner", "splitter", "stepper", "subform", "tab", "text", "view", "webArea", "write"|

#### Objects Supported

[4D View Pro area](viewProArea_overview.md) - [4D Write Pro area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Picture Button](pictureButton_overview.md) - [Picture Pop-up Menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress indicator](progressIndicator.md) - [Radio Button](radio_overview.md) -[Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

---

## Object Name

Each active form object is associated with an object name. Each object name must be unique.

>Object names are limited to a size of 255 bytes.

When using 4D’s language, you can refer to an active form object by its object name (see [Object (Forms) commands](../commands/theme/Objects_Forms.md))).

For more information about naming rules for form objects, refer to [Identifiers](Concepts/identifiers.md) section.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|name|string |Any allowed name which does not belong to an already existing object|

#### Objects Supported

[4D View Pro area](viewProArea_overview.md) - [4D Write Pro area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [List Box Header](listbox_overview.md#list-box-headers) - [Picture Button](pictureButton_overview.md) - [Picture Pop-up Menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress indicator](progressIndicator.md) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Radio Button](radio_overview.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)


#### Commands

[FORM GET OBJECTS](../commands-legacy/form-get-objects.md) - [OBJECT Get name](../commands-legacy/object-get-name.md)

---

## Save value

This property is available when the [Save Geometry](FormEditor/properties_FormProperties.md#save-geometry) option is checked for the form.

This feature is only supported for objects that contribute to the overall geometry of the form. For example, this option is available for check boxes because their value can be used to hide or display additional areas in the window.

Here is the list of objects whose value can be saved:

|Object|Saved value|
|---|---|
|[Check Box](checkbox_overview.md)|Value of associated variable (0, 1, 2)|
|[Drop-down List](dropdownList_Overview.md)|Number of selected row|
|[Radio Button](radio_overview.md)|Value of associated variable (1, 0, True or False for buttons according to their type)|
|[Tab control](tabControl.md)|Number of selected tab|

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|memorizeValue|boolean |true, false|

#### Objects Supported

[Check Box](checkbox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Radio Button](radio_overview.md) - [Tab control](tabControl.md)

---

## Variable or Expression

> See also **[Expression](properties_DataSource.md#expression)** for Selection and collection type list box columns.

This property specifies the source of the data. Each active form object is associated with an object name and a variable name. The variable name can be different from the object’s name. In the same form, you can use the same variable several times while each [object name](#object-name) must be unique.

>Variable name size is limited to 31 bytes. See [Identifiers](Concepts/identifiers.md) section for more information about naming rules.

The form object variables allow you to control and monitor the objects. For example, when a button is clicked, its variable is set to 1; at all other times, it is 0. The expression associated with a progress indicator lets you read and change the current setting.

Variables or expressions can be enterable or non-enterable and can receive data of the Text, Integer, Numeric, Date, Time, Picture, Boolean, or Object type.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|dataSource|string, or string array|<li>4D variable, field name, or any expression.</li><li>Empty string for [dynamic variables](#dynamic-variables).</li><li>String array (collection of array names) for a [hierarchical listbox](listbox_overview.md#hierarchical-list-boxes) column]</li>|

### Expressions

You can use an [expression](Concepts/quick-tour.md#expressions) as data source for an object. Any valid 4D expression is allowed: simple expression, object property, formula, 4D function, project method name or field using the standard `[Table]Field` syntax. The expression is evaluated when the form is executed and reevaluated for each form event. Note that expressions can be [assignable or non-assignable](Concepts/quick-tour.md#expressions).

>If the value entered corresponds to both a variable name and a method name, 4D considers that you are indicating the method.

### Dynamic variables

You can leave it up to 4D to create variables associated with your form objects (buttons, enterable variables, check boxes, etc.) dynamically and according to your needs. To do this, simply leave the "Variable or Expression" property (or `dataSource` JSON field) blank.

When a variable is not named, when the form is loaded, 4D creates a new variable for the object, with a calculated name that is unique in the space of the process variables of the interpreter (which means that this mechanism can be used even in compiled mode). This temporary variable will be destroyed when the form is closed.

To get or set the value of form objects that use dynamic variables, you just need to call [`OBJECT Get value`](../commands-legacy/object-get-value.md) and [`OBJECT SET VALUE`](../commands-legacy/object-set-value.md) commands. For example:

```4d
 var $value : Variant
 $value:=OBJECT Get value("comments")
 OBJECT SET VALUE("comments";$value+10) 
```


### Array List Box

For an array list box, the **Variable or Expression** property usually holds the name of the array variable defined for the list box, and for each column. However, you can use a string array (containing arrays names) as *dataSource* value for a list box column to define a [hierarchical list box](listbox_overview.md#hierarchical-list-boxes).

#### Objects Supported

[4D View Pro area](viewProArea_overview.md) - [4D Write Pro area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Hierarchical List](list_overview.md) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Header](listbox_overview.md#list-box-headers) - [List Box Footer](listbox_overview.md#list-box-footers) - [Picture Pop-up Menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress indicator](progressIndicator.md) - [Radio Button](radio_overview.md) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Web Area](webArea_overview.md)


#### Commands

[`LISTBOX Get column formula`](../commands-legacy/listbox-get-column-formula.md) - [`LISTBOX SET COLUMN FORMULA`](../commands-legacy/listbox-set-column-formula.md) - [`OBJECT Get data source`](../commands-legacy/object-get-data-source.md) - [`OBJECT Get data source formula`](../commands/object-get-data-source-formula.md) - [`OBJECT Get value`](../commands-legacy/object-get-value.md) - [`OBJECT Get pointer`](../commands-legacy/object-get-pointer.md) - [`OBJECT SET VALUE`](../commands-legacy/object-set-value.md) - [`OBJECT SET DATA SOURCE`](../commands-legacy/object-set-data-source.md) - [`OBJECT SET DATA SOURCE FORMULA`](../commands/object-set-data-source-formula.md)


---

## Expression Type

> This property is called [**Data Type**](properties_DataSource.md#data-type-expression-type) in the Property List for [selection](listbox_overview.md#selection-list-boxes) and [collection](listbox_overview.md#collection-or-entity-selection-list-boxes) type list box columns and for [Drop-down Lists](dropdownList_Overview.md) associated to an [object](FormObjects/dropdownList_Overview.md#using-an-object) or an [array](FormObjects/dropdownList_Overview.md#using-an-array).

Specify the data type for the expression or variable associated to the object. Note that main purpose of this setting is to configure options (such as display formats) available for the data type. It does not actually type the variable itself. In view of project compilation, you must [declare the variable](Concepts/variables.md#declaring-variables).

However, this property has a typing function in the following specific cases:

- **[Dynamic variables](#dynamic-variables)**: you can use this property to declare the type of dynamic variables.
- **[List Box Columns](listbox_overview.md#list-box-columns)**: this property is used to associate a display format with the column data. The formats provided will depend on the variable type (array type list box) or the data/field type (selection and collection type list boxes). The standard 4D formats that can be used are: Alpha, Numeric, Date, Time, Picture and Boolean. The Text type does not have specific display formats. Any existing custom formats are also available.
- **[Picture variables](input_overview.md)**: you can use this menu to declare the variables before loading the form in interpreted mode. Specific native mechanisms govern the display of picture variables in forms. These mechanisms require greater precision when configuring variables: from now on, they must have already been declared before loading the form — i.e., even before the `On Load` form event — unlike other types of variables. To do this, you need either for the statement `var varName : Picture` to have been executed before loading the form (typically, in the method calling the `DIALOG` command), or for the variable to have been typed at the form level using the expression type property.
Otherwise, the picture variable will not be displayed correctly (only in interpreted mode).

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|dataSourceTypeHint |string  |<li>**standard objects:** "integer", "boolean", "number", "picture", "text", date", "time", "arrayText", "arrayDate", "arrayTime", "arrayNumber", "collection", "object", "undefined"</li><li>**list box columns:** "boolean", "number", "picture", "text", date", "time". *Array/selection list box only*: "integer", "object"</li>|

#### Objects Supported

[Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Input](input_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [List Box Footer](listbox_overview.md#list-box-footers) - [Plug-in Area](pluginArea_overview.md) - [Progress indicator](progressIndicator.md) - [Radio Button](radio_overview.md) - [Ruler](ruler.md) - [Spinner](spinner.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab Control](tabControl.md)

---

## CSS Class

A list of space-separated words used as class selectors in [css files](FormEditor/createStylesheet.md#style-sheet-files).

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|class |string|One string with CSS name(s) separated by space characters|

#### Objects Supported

[4D View Pro area](viewProArea_overview.md) - [4D Write Pro area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Drop-down List](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [List Box](listbox_overview.md) - [Picture Button](pictureButton_overview.md) - [Picture Pop-up Menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Radio Button](radio_overview.md) - [Static Picture](staticPicture.md) - [Subform](subform_overview.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

---

## Collection or entity selection

To use collection elements or entities to define the row contents of the list box.

Enter an expression that returns either a collection or an entity selection. Usually, you will enter the name of a variable, a collection element or a property that contain a collection or an entity selection.

The collection or the entity selection must be available to the form when it is loaded. Each element of the collection or each entity of the entity selection will be associated to a list box row and will be available as an object through the [`This`](../Concepts/classes.md#this) keyword:

- if you used a collection of objects, you can call **This** in the datasource expression to access each property value, for example `This.<propertyPath>`.
- if you used an entity selection, you can call **This** in the datasource expression to access each attribute value, for example `This.<attributePath>`.

>If you used a collection of scalar values (and not objects), 4D allows you to display each value by calling **This.value** in the datasource expression. However in this case you will not be able to modify values or to access the current object (see below).

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|dataSource |string|Expression that returns a collection or an entity selection.|

#### Objects Supported

[List Box](listbox_overview.md)

#### Commands

[`OBJECT Get data source`](../commands-legacy/object-get-data-source.md) - [`OBJECT Get data source formula`](../commands/object-get-data-source-formula.md) - [`OBJECT Get value`](../commands-legacy/object-get-value.md) - [`OBJECT Get pointer`](../commands-legacy/object-get-pointer.md) - [`OBJECT SET VALUE`](../commands-legacy/object-set-value.md) - [`OBJECT SET DATA SOURCE`](../commands-legacy/object-set-data-source.md) - [`OBJECT SET DATA SOURCE FORMULA`](../commands/object-set-data-source-formula.md)

---

## Data Source

Specify the type of list box.

![](../assets/en/FormObjects/listbox_dataSource.png)

- **Arrays**(default): use array elements as the rows of the list box.
- **Current Selection**: use expressions, fields or methods whose values will be evaluated for each record of the current selection of a table.
- **Named Selection**: use expressions, fields or methods whose values will be evaluated for each record of a named selection.
- **Collection or Entity Selection**: use collection elements or entities to define the row contents of the list box. Note that with this list box type, you need to define the [Collection or Entity Selection](properties_Object.md#collection-or-entity-selection) property.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|listboxType|string|"array", "currentSelection", "namedSelection", "collection"|

#### Objects Supported

[List Box](listbox_overview.md)

---

## Plug-in Kind

Name of the [plug-in external area](pluginArea_overview.md) associated to the object. Plug-in external area names are published in the manifest.json file of the plug-in.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|pluginAreaKind|string|Name of the plug-in external area (starts with a % character)|

#### Objects Supported

[Plug-in Area](pluginArea_overview.md)

---

## Radio Group

Enables radio buttons to be used in coordinated sets: only one button at a time can be selected in the set.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
| radioGroup|string  |Radio group name|

#### Objects Supported

[Radio Button](radio_overview.md)

---

## Title

Allows inserting a label on an object. The font and the style of this label can be specified.

You can force a carriage return in the label by using the \ character (backslash).

![](../assets/en/FormObjects/property_title.png)

To insert a \ in the label, enter "&#92;&#92;".

By default, the label is placed in the center of the object. When the object also contains an icon, you can modify the relative location of these two elements using the [Title/Picture Position](properties_TextAndPicture.md#titlepicture-position) property.

For application translation purposes, you can enter an XLIFF reference in the title area of a button (see [Appendix B: XLIFF architecture](https://doc.4d.com/4Dv20/4D/20.2/Appendix-B-XLIFF-architecture.300-6750166.en.html)).

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|text|string |any text |

#### Objects Supported

[Button](button_overview.md) - [Check Box](checkbox_overview.md) - [List Box Header](listbox_overview.md#list-box-headers) - [Radio Button](radio_overview.md) - [Text Area](text.md)

#### Commands

[`OBJECT Get title`](../commands-legacy/object-get-title.md) - [`OBJECT SET TITLE`](../commands-legacy/object-set-title.md) 

---

## Variable Calculation

This property sets the type of calculation to be done in a [column footer](listbox_overview.md#list-box-footers) area.

>The calculation for footers can also be set using the [`LISTBOX SET FOOTER CALCULATION`](../commands-legacy/listbox-set-footer-calculation.md) 4D command.

There are several types of calculations available. The following table shows which calculations can be used according to the type of data found in each column and indicates the type automatically affected by 4D to the footer variable (if it is not typed by the code):

|Calculation|Num|Text|Date|Time|Bool|Pict|footer var type|  
|---|---|---|---|---|---|---|---|
|Minimum|X|X|X|X|X||Same as column type|
|Maximum|X|X|X|X|X||Same as column type|  
|Sum|X|||X|X||Same as column type|  
|Count|X|X|X|X|X|X|Integer|  
|Average|X|||X|||Real|
|Standard deviation(*)|X|||X|||Real|
|Variance(*)|X|||X|||Real|
|Sum squares(*)|X|||X|||Real|
|Custom ("none")|X|X|X|X|X|X|Any|

(*) Only for array type list boxes.

> Only declared or dynamic [variables](Concepts/variables.md) can be used to display footer calculations. Other kinds of [expressions](Concepts/quick-tour.md#expressions) such as `Form.value` are not supported.  

Automatic calculations ignore the shown/hidden state of list box rows. If you want to restrict a calculation to only visible rows, you must use a custom calculation.

*Null* values are not taken into account for any calculations.  

If the column contains different types of values (collection-based column for example):

- Average and Sum only take numerical elements into account (other element types are ignored).
- Minimum and Maximum return a result according to the usual type list order as defined in the [collection.sort()](API/CollectionClass.md#sort) function.

Using automatic calculations in footers of columns based upon expressions has the following limitations:

- it is **supported** with all list box types when the expression is "simple" (such as `[table]field` or `this.attribute`),
- it is **supported but not recommended** for performance reasons with collection/entity selection list boxes when the expression is "complex" (other than `this.attribute`) and the list box contains a large number of rows,
- it is **not supported** with current selection/named selection list boxes when the expression is "complex". You need to use custom calculations.

When **Custom** ("none" in JSON) is set, no automatic calculations are performed by 4D and you must assign the value of the variable in this area by programming.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|variableCalculation|string|"none", "minimum", "maximum", "sum", "count", "average", "standardDeviation", "variance", "sumSquare"|

#### Objects Supported

[List Box Footer](listbox_overview.md#list-box-footers)

#### Commands

[`LISTBOX Get footer calculation`](../commands-legacy/listbox-get-footer-calculation.md) - [`LISTBOX SET FOOTER CALCULATION`](../commands-legacy/listbox-set-footer-calculation.md)