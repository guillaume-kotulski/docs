---
id: propertiesCoordinatesAndSizing
title: Coordinates & Sizing
---

## Automatic Row Height

This property is only available for list boxes with the following [data sources](properties_Object.md#data-source):

- collection or entity selection,
- array (non-hierarchical).

The property is not selected by default. When used for at least one column, the height of every row in the column will automatically be calculated by 4D, and the column contents will be taken into account. Note that only columns with the option selected will be taken into account to calculate the row height.

:::note

When resizing the form, if the "Grow" [horizontal sizing](properties_ResizingOptions.md#horizontal-sizing) property was assigned to the list box, the right-most column will be increased beyond its maximum width if necessary.

:::

When this property is enabled, the height of every row is automatically calculated in order to make the cell contents entirely fit without being truncated (unless the [Wordwrap](properties_Display.md#wordwrap) option is disabled.

* The row height calculation takes into account:
  * any content types (text, numerics, dates, times, pictures (calculation depends on the picture format), objects),
  * any control types (inputs, check boxes, lists, dropdowns),
  * fonts, fonts styles and font sizes,
  * the [Wordwrap](properties_Display.md#wordwrap) option: if disabled, the height is based on the number of paragraphs (lines are truncated); if enabled, the height is based on number of lines (not truncated).

* The row height calculation ignores:
  * hidden column contents
  * [Row Height](#row-height) and [Row Height Array](#row-height-array) properties (if any) set either in the Property list or by programming.

:::caution

Since it requires additional calculations at runtime, the automatic row height option could affect the scrolling fluidity of your list box, in particular when it contains a large number of rows.

:::


#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|rowHeightAuto|boolean |true, false|

#### Objects Supported

[List Box Column](listbox_overview.md#list-box-columns)


#### Commands

[`LISTBOX Get property`](../commands/listbox-get-property.md) - [`LISTBOX SET PROPERTY`](../commands/listbox-set-property.md) 


---

## Bottom

Bottom coordinate of the object in the form.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|bottom|number | minimum: 0|

#### Objects Supported

[4D View Pro Area](viewProArea_overview.md) - [4D Write Pro Area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Dropdown list](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [Line](shapes_overview.md#line) - [List Box Column](listbox_overview.md#list-box-columns) - [Oval](shapes_overview.md#oval) - [Picture Button](pictureButton_overview.md) - [Picture Pop up menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress Indicators](progressIndicator.md) - [Radio Button](radio_overview.md) - [Rectangle](shapes_overview.md#rectangle) - [Ruler](ruler.md) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

#### Commands

[OBJECT GET COORDINATES](../commands-legacy/object-get-coordinates.md) - [OBJECT MOVE](../commands-legacy/object-move.md) - [OBJECT SET COORDINATES](../commands-legacy/object-set-coordinates.md)

---

## Left

Left coordinate of the object on the form.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|left|number |minimum: 0|

#### Objects Supported

[4D View Pro Area](viewProArea_overview.md) - [4D Write Pro Area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Dropdown list](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [Line](shapes_overview.md#line) - [List Box Column](listbox_overview.md#list-box-columns) - [Oval](shapes_overview.md#oval) - [Picture Button](pictureButton_overview.md) - [Picture Pop up menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress Indicators](progressIndicator.md) - [Radio Button](radio_overview.md) - [Ruler](ruler.md) - [Rectangle](shapes_overview.md#rectangle) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

#### Commands

[OBJECT GET COORDINATES](../commands-legacy/object-get-coordinates.md) - [OBJECT MOVE](../commands-legacy/object-move.md) - [OBJECT SET COORDINATES](../commands-legacy/object-set-coordinates.md)

---

## Right

Right coordinate of the object in the form.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|right|number |minimum: 0|

#### Objects Supported

[4D View Pro Area](viewProArea_overview.md) - [4D Write Pro Area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Dropdown list](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [Line](shapes_overview.md#line) - [List Box Column](listbox_overview.md#list-box-columns) - [Oval](shapes_overview.md#oval) - [Picture Button](pictureButton_overview.md) - [Picture Pop up menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress Indicators](progressIndicator.md) - [Radio Button](radio_overview.md) - [Ruler](ruler.md) - [Rectangle](shapes_overview.md#rectangle) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

#### Commands

[OBJECT GET COORDINATES](../commands-legacy/object-get-coordinates.md) - [OBJECT MOVE](../commands-legacy/object-move.md) - [OBJECT SET COORDINATES](../commands-legacy/object-set-coordinates.md)

---

## Top

Top coordinate of the object in the form.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|top |number |minimum: 0|

#### Objects Supported

[4D View Pro Area](viewProArea_overview.md) - [4D Write Pro Area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Dropdown list](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [Line](shapes_overview.md#line) - [List Box Column](listbox_overview.md#list-box-columns) - [Oval](shapes_overview.md#oval) - [Picture Button](pictureButton_overview.md) - [Picture Pop up menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress Indicators](progressIndicator.md) - [Radio Button](radio_overview.md) - [Ruler](ruler.md) - [Rectangle](shapes_overview.md#rectangle) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

#### Commands

[OBJECT GET COORDINATES](../commands-legacy/object-get-coordinates.md) - [OBJECT MOVE](../commands-legacy/object-move.md) - [OBJECT SET COORDINATES](../commands-legacy/object-set-coordinates.md)

---

## Corner Radius

<details><summary>History</summary>

|Release|Changes|
|---|---|
|19 R7|Support for inputs and text areas|

</details>

Defines the corner roundness (in pixels) of the object. By default, the radius value is 0 pixels. You can change this property to draw rounded objects with custom shapes:

![](../assets/en/FormObjects/shape_rectangle.png)

Minimum value is 0, in this case a standard non-rounded object rectangle is drawn.
Maximum value depends on the rectangle size (it cannot exceed half the size of the shortest rectangle side) and is calculated dynamically.

:::note

With [text areas](text.md) and [inputs](input_overview.md):

- the corner radius property is only available with "none", "solid", or "dotted" [border line styles](properties_BackgroundAndBorder.md#border-line-style),
- the corner roundness is drawn outside the area of the object (the object appears larger in the form but its [width](properties_CoordinatesAndSizing.md#width) and [height](properties_CoordinatesAndSizing.md#height) are not extended).

![](../assets/en/FormObjects/radius-text.png)

:::

You can also set this property using the [OBJECT Get corner radius](../commands-legacy/object-get-corner-radius.md) and [OBJECT SET CORNER RADIUS](../commands-legacy/object-set-corner-radius.md) commands.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|borderRadius|integer |minimum: 0|

#### Objects Supported

[Input](input_overview.md) - [Rectangle](shapes_overview.md#rectangle) - [Text Area](text.md)

#### Commands

[OBJECT GET CORNER RADIUS](../commands-legacy/object-get-corner-radius.md) - [OBJECT SET CORNER RADIUS](../commands-legacy/object-set-corner-radius.md)


---

## Height

This property designates an object's vertical size.

>Some objects may have a predefined height that cannot be altered.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|height|number |minimum: 0|

#### Objects Supported

[4D View Pro Area](viewProArea_overview.md) - [4D Write Pro Area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Dropdown list](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [List Box](listbox_overview.md) - [Line](shapes_overview.md#line) - [List Box Column](listbox_overview.md#list-box-columns) - [Oval](shapes_overview.md#oval) - [Picture Button](pictureButton_overview.md) - [Picture Pop up menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress Indicators](progressIndicator.md) - [Radio Button](radio_overview.md) - [Ruler](ruler.md) - [Rectangle](shapes_overview.md#rectangle) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

#### Commands

[OBJECT GET COORDINATES](../commands-legacy/object-get-coordinates.md) - [OBJECT MOVE](../commands-legacy/object-move.md) - [OBJECT SET COORDINATES](../commands-legacy/object-set-coordinates.md)

---

## Width

This property designates an object's horizontal size.

>* Some objects may have a predefined height that cannot be altered.
>* If the [Resizable](properties_ResizingOptions.md#resizable) property is used for a [list box column](listbox_overview.md#list-box-columns), the user can also manually resize the column.
>* When resizing the form, if the ["Grow" horizontal sizing](properties_ResizingOptions.md#horizontal-sizing) property was assigned to the list box, the right-most column will be increased beyond its maximum width if necessary.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|width|number |minimum: 0|

#### Objects Supported

[4D View Pro Area](viewProArea_overview.md) - [4D Write Pro Area](writeProArea_overview.md) - [Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md) - [Combo Box](comboBox_overview.md) - [Dropdown list](dropdownList_Overview.md) - [Group Box](groupBox.md) - [Hierarchical List](list_overview.md) - [Input](input_overview.md) - [Line](shapes_overview.md#line) - [List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [Oval](shapes_overview.md#oval) - [Picture Button](pictureButton_overview.md) - [Picture Pop up menu](picturePopupMenu_overview.md) - [Plug-in Area](pluginArea_overview.md) - [Progress Indicators](progressIndicator.md) - [Radio Button](radio_overview.md) - [Ruler](ruler.md) - [Rectangle](shapes_overview.md#rectangle) - [Spinner](spinner.md) - [Splitter](splitters.md) - [Static Picture](staticPicture.md) - [Stepper](stepper.md) - [Subform](subform_overview.md) - [Tab control](tabControl.md) - [Text Area](text.md) - [Web Area](webArea_overview.md)

#### Commands

[OBJECT GET COORDINATES](../commands-legacy/object-get-coordinates.md) - [OBJECT MOVE](../commands-legacy/object-move.md) - [OBJECT SET COORDINATES](../commands-legacy/object-set-coordinates.md)

---

## Maximum Width

The maximum width of the column (in pixels). The width of the column cannot be increased beyond this value when resizing the column or form.

>When resizing the form, if the ["Grow" horizontal sizing](properties_ResizingOptions.md#horizontal-sizing) property was assigned to the list box, the right-most column will be increased beyond its maximum width if necessary.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|maxWidth|number |minimum: 0|

#### Objects Supported

[List Box Column](listbox_overview.md#list-box-columns)

#### Commands

[LISTBOX Get column width](../commands-legacy/listbox-get-column-width.md) - [LISTBOX SET COLUMN WIDTH](../commands-legacy/listbox-set-column-width.md)

---

## Minimum Width

The minimum width of the column (in pixels). The width of the column cannot be reduced below this value when resizing the column or form.

>When resizing the form, if the ["Grow" horizontal sizing](properties_ResizingOptions.md#horizontal-sizing) property was assigned to the list box, the right-most column will be increased beyond its maximum width if necessary.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|minWidth|number |minimum: 0|

#### Objects Supported

[List Box Column](listbox_overview.md#list-box-columns)

#### Commands

[LISTBOX Get column width](../commands-legacy/listbox-get-column-width.md) - [LISTBOX SET COLUMN WIDTH](../commands-legacy/listbox-set-column-width.md)

---

## Row Height

Sets the height of list box rows (excluding headers and footers). By default, the row height is set according to the platform and the font size.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|rowHeight|string |css value in unit "em" or "px" (default)|

#### Objects Supported

[List Box](listbox_overview.md)

#### Commands

[LISTBOX Get row height](../commands-legacy/listbox-get-row-height.md) - [LISTBOX Get rows height](../commands-legacy/listbox-get-rows-height.md) - [LISTBOX SET ROW HEIGHT](../commands-legacy/listbox-set-row-height.md) - [LISTBOX SET ROWS HEIGHT](../commands-legacy/listbox-set-rows-height.md)



#### See also

[Row Height Array](#row-height-array)

---

## Row Height Array

This property is used to specify the name of a row height array that you want to associate with the list box. A row height array must be of the numeric type (longint by default).

When a row height array is defined, each of its elements whose value is different from 0 (zero) is taken into account to determine the height of the corresponding row in the list box, based on the current Row Height unit.

For example, you can write:

```4d
ARRAY LONGINT(RowHeights;20)
RowHeights{5}:=3
```

Assuming that the unit of the rows is "lines," then the fifth row of the list box will have a height of three lines, while every other row will keep its default height.

>* The Row Height Array property is not taken into account for hierarchical list boxes.
>* For array and collection/entity selection list boxes, this property is available only if the [Automatic Row Height](#automatic-row-height) option is not selected.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|rowHeightSource|string|Name of a 4D array variable.|

#### Objects Supported

[List Box](listbox_overview.md)


#### Commands

[`LISTBOX Get array`](../commands-legacy/listbox-get-array.md) - [`LISTBOX GET ARRAYS`](../commands-legacy/listbox-get-arrays.md) 


#### See also

[Row Height](#row-height)

---

## Horizontal Padding

Sets a horizontal padding for the cells. The value is set in pixels (default = 0).

![](../assets/en/FormObjects/padding.png)

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|horizontalPadding|number |Number of pixels (must be >=0)|

#### Objects Supported

[List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [Footers](properties_Footers.md) - [Headers](properties_Headers.md)


#### Commands

[`LISTBOX Get property`](../commands/listbox-get-property.md) - [`LISTBOX SET PROPERTY`](../commands/listbox-set-property.md) 



#### See also

[Vertical Padding](#vertical-padding)

---

## Vertical Padding

Sets a vertical padding for the cells. The value is set in pixels (default = 0).  

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|verticalPadding|number |Number of pixels (must be >=0)|

#### Objects Supported

[List Box](listbox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [Footers](properties_Footers.md) - [Headers](properties_Headers.md)

#### Commands

[`LISTBOX Get property`](../commands/listbox-get-property.md) - [`LISTBOX SET PROPERTY`](../commands/listbox-set-property.md) 


#### See also

[Horizontal Padding](#horizontal-padding)
