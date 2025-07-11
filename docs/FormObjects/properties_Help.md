---
id: propertiesHelp
title: Help 
---

## Help Tip

This property allows associating help messages with active objects in your forms. They can be displayed at runtime:

![](../assets/en/FormObjects/property_helpTip.png)

> - The display delay and maximum duration of help tips can be controlled using the ``Tips delay`` and ``Tips duration`` selectors of the **[SET DATABASE PARAMETER](../commands-legacy/set-database-parameter.md)** command.
> - Help tips can be globally disabled or enabled for the application using the Tips enabled selector of the [**SET DATABASE PARAMETER**](../commands-legacy/set-database-parameter.md) command.

You can either:

- designate an existing help tip, previously specified in the [Help tips](https://doc.4d.com/4Dv20/4D/20.2/Help-tips.200-6750100.en.html) editor of 4D.
- or enter the help message directly as a string. This allows you to take advantage of XLIFF architecture. You can enter an XLIFF reference here in order to display a message in the application language (for more information about XLIFF, refer to [Appendix B: XLIFF architecture](https://doc.4d.com/4Dv20/4D/20.2/Appendix-B-XLIFF-architecture.300-6750166.en.html). You can also use 4D references ([see Using references in static text](https://doc.4d.com/4Dv20/4D/20.2/Using-references-in-static-text.300-6750154.en.html)).

>In macOS, displaying help tips is not supported in pop-up type windows.

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|tooltip|text| additional information to help a user|

#### Objects Supported

[Button](button_overview.md) - [Button Grid](buttonGrid_overview.md) - [Check Box](checkbox_overview.md)  - [Drop-down List](dropdownList_Overview.md) - [Combo Box](comboBox_overview.md) - [Hierarchical List](list_overview.md) - [List Box Header](listbox_overview.md#list-box-headers) - [List Box Footer](listbox_overview.md#list-box-footers) - [Picture Button](pictureButton_overview.md) - [Picture Pop-up menu](picturePopupMenu_overview.md) - [Radio Button](radio_overview.md)

#### Other help features

You can also associate help messages with form objects in two other ways:

- at the level of the database structure (fields only). In this case, the help tip of the field is displayed in every form where it appears. For more information, refer to “Help Tips” in [Field properties](https://doc.4d.com/4Dv20/4D/20.2/Field-properties.300-6750280.en.html#3367486).
- using the **[OBJECT SET HELP TIP](../commands-legacy/object-set-help-tip.md)** command, for the current process.

When different tips are associated with the same object in several locations, the following priority order is applied:

1. structure level (lowest priority)
2. form editor level
3. **[OBJECT SET HELP TIP](../commands-legacy/object-set-help-tip.md)** command (highest priority)


#### Commands

[`OBJECT Get help tip`](../commands-legacy/object-get-help-tip.md) - [`OBJECT SET HELP TIP`](../commands-legacy/object-set-help-tip.md)


#### See also

[Placeholder](properties_Entry.md#placeholder)
