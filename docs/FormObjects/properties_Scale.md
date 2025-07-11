---
id: propertiesScale
title: Scale
---

## Barber shop

Enables the "barber shop" variant for the thermometer.

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|[max](#maximum)|number |NOT passed = enabled; passed = disabled (basic thermometer)|

#### Objects Supported

[Barber shop](progressIndicator.md#barber-shop)

#### Commands

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT Get indicator type](../commands-legacy/object-get-indicator-type.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md) - [OBJECT SET INDICATOR TYPE](../commands-legacy/object-set-indicator-type.md) 

---

## Display graduation

Displays/Hides the graduations next to the labels.

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|showGraduations|boolean |"true", "false"|

#### Objects Supported

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md)

#### Commands

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Graduation step

Scale display measurement. 

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|graduationStep| integer|minimum: 0|

#### Objects Supported

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md)

#### Commands

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Label Location

Specifies the location of an object's displayed text.

* None - no label is displayed
* Top - Displays labels to the left of or above an indicator
* Bottom - Displays labels to the right of or below an indicator

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|labelsPlacement| string|"none", "top", "bottom", "left", "right"|

#### Objects Supported

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md)

#### Commands

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Maximum

Maximum value of an indicator.

* For numeric steppers, this property represent seconds when the object is associated with a time type value and are ignored when it is associated with a date type value.
* To enable [Barber shop thermometers](progressIndicator.md#barber-shop), this property must be omitted.

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|max| number |Any number|

#### Objects Supported

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md) - [Stepper](stepper.md)

#### Commands

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get maximum-value](../commands-legacy/object-get-maximum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md) - [OBJECT SET MAXIMUM VALUE](../commands-legacy/object-set-maximum-value.md)

---

## Minimum

Minimum value of an indicator. For numeric steppers, this property represent seconds when the object is associated with a time type value and are ignored when it is associated with a date type value.

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|min| number |Any number|

#### Objects Supported

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md) - [Stepper](stepper.md)

#### Commands

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md) - [OBJECT SET MINIMUM VALUE](../commands-legacy/object-set-minimum-value.md)


---

## Step

Minimum interval accepted between values during use. For numeric steppers, this property represents seconds when the object is associated with a time type value and days when it is associated with a date type value.

#### JSON Grammar

|Name|Data Type|Possible Values|
|:---:|:---:|---|
|step| integer|minimum: 1|

#### Objects Supported

[Thermometer](progressIndicator.md#default-thermometer) - [Ruler](ruler.md) - [Stepper](stepper.md)

#### Commands

[OBJECT Get format](../commands-legacy/object-get-format.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)
