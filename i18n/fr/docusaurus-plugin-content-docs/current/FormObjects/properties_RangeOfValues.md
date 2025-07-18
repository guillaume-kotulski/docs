---
id: propertiesRangeOfValues
title: Plage de valeurs
---

## La valeur par défaut

Vous pouvez attribuer une valeur par défaut à saisir dans un objet Zone de saisie. Cette propriété est utile par exemple lorsque la [source de données](properties_Object.md#variable-or-expression) de la zone de saisie est un champ : la valeur par défaut est saisie lors du premier affichage d'un nouvel enregistrement. Vous pouvez modifier la valeur, sauf si la zone de saisie a été définie comme [non saisissable](properties_Entry.md#enterable).

La valeur par défaut ne peut être utilisée que si le [type de source de données](properties_Object.md#expression-type) est :

- text/string
- number/integer
- date
- time
- boolean

4D fournit des balises pour générer des valeurs par défaut pour la date, l'heure et le numéro de séquence. La date et l'heure proviennent de la date et de l'heure du système. 4D génère automatiquement les numéros de séquence nécessaires. Le tableau ci-dessous indique la balise à utiliser pour générer automatiquement des valeurs par défaut :

| Stamp | Description        |
| ----- | ------------------ |
| #D    | Date courante      |
| #H    | Heure courante     |
| #N    | Numéro de séquence |

Vous pouvez utiliser un numéro de séquence pour créer un numéro unique pour chaque enregistrement de la table dans le fichier de données courant. Un numéro de séquence est un entier qui est généré pour chaque nouvel enregistrement. Les numéros commencent à un (1) et s'incrémentent de un (1). Un numéro de séquence n'est jamais répété, même si l'enregistrement auquel il est attribué est supprimé de la table. Chaque table possède son propre compteur interne de numéros de séquence. For more information, refer to the [Autoincrement](https://doc.4d.com/4Dv20/4D/20.2/Field-properties.300-6750280.en.html#976029) paragraph.

> Do not make confusion between this property and the "[default values](properties_DataSource.md#default-list-of-values)" property that allows to fill a list box column with static values.

#### Grammaire JSON

| Nom          | Type de données                     | Valeurs possibles                                                |
| ------------ | ----------------------------------- | ---------------------------------------------------------------- |
| defaultValue | string, number, date, time, boolean | Toute valeur et/ou une balise : "#D", "#H", "#N" |

#### Objets pris en charge

[Zone de saisie](input_overview.md)

---

## Exclusion

Permet de définir une liste dont les valeurs ne peuvent pas être saisies dans l'objet. Si une valeur exclue est saisie, elle n'est pas acceptée et un message d'erreur s'affiche.

> Si une énumération spécifiée est hiérarchique, seuls les éléments du premier niveau sont pris en compte.

#### Grammaire JSON

| Nom          | Type de données | Valeurs possibles                               |
| ------------ | --------------- | ----------------------------------------------- |
| excludedList | list            | Une liste de valeurs à exclure. |

#### Objets pris en charge

[Combo Box](comboBox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [Input](input_overview.md)

#### Commandes

[OBJECT Get list name](../commands-legacy/object-get-list-name.md) - [OBJECT Get list reference](../commands-legacy/object-get-list-reference.md) - [OBJECT SET LIST BY NAME](../commands-legacy/object-set-list-by-name.md) - [OBJECT SET LIST BY REFERENCE](../commands-legacy/object-set-list-by-reference.md)

---

## Obligation

Limite les entrées valides aux éléments de la liste. Par exemple, vous pouvez souhaiter utiliser une liste pour les titres de postes afin que les entrées valides soient limitées aux intitulés qui ont été approuvés par la direction.

La création d'une liste obligatoire n'affiche pas automatiquement la liste lorsque le champ est sélectionné. Si vous souhaitez afficher la liste requise, assignez la même liste à la propriété [Choice List](properties_DataSource.md#choice-list).
Cependant, contrairement à la propriété [Choice List](properties_DataSource.md#choice-list), lorsqu'une liste obligatoire est définie, la saisie au clavier n'est plus possible, seule la sélection d'une valeur de liste à l'aide du pop-up menu est autorisée If different lists are defined using the [Choice List](properties_DataSource.md#choice-list) and Required List properties, the Required List property has priority. If different lists are defined using the [Choice List](properties_DataSource.md#choice-list) and Required List properties, the Required List property has priority.

> Si une énumération spécifiée est hiérarchique, seuls les éléments du premier niveau sont pris en compte.

#### Grammaire JSON

| Nom          | Type de données | Valeurs possibles                                  |
| ------------ | --------------- | -------------------------------------------------- |
| requiredList | list            | Une liste de valeurs obligatoires. |

#### Objets pris en charge

[Combo Box](comboBox_overview.md) - [List Box Column](listbox_overview.md#list-box-columns) - [Input](input_overview.md)

#### Commandes

[OBJECT Get list name](../commands-legacy/object-get-list-name.md) - [OBJECT Get list reference](../commands-legacy/object-get-list-reference.md) - [OBJECT SET LIST BY NAME](../commands-legacy/object-set-list-by-name.md) - [OBJECT SET LIST BY REFERENCE](../commands-legacy/object-set-list-by-reference.md)
