---
id: onAfterEdit
title: On After Edit
---

| Code | Peut être appelé par                                                                                                                                                                                                                                                                                                                                                                              | Définition                                                            |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| 45   | [Zone 4D View Pro](../FormObjects/viewProArea_overview.md) - [Zone 4D Write Pro](../FormObjects/writeProArea_overview.md) - [Combo Box](FormObjects/comboBox_overview.md) - Form - [Input](FormObjects/input_overview.md) - [Hierarchical List](FormObjects/list_overview.md) - [List Box](FormObjects/listbox_overview.md) - [List Box Column](FormObjects/listbox_overview.md#list-box-columns) | Le contenu de l'objet saisissable qui a le focus vient d'être modifié |

## Description

### Cas général

Cet événement peut être utilisé pour filtrer la saisie de données dans les objets saisissables au clavier au niveau le plus bas.

Lorsqu'il est utilisé, cet événement est généré après chaque modification apportée au contenu d'un objet saisissable, quelle que soit l'action qui a provoqué la modification, c'est-à-dire :

- Actions d'édition standard qui modifient le contenu comme les actions coller, couper, supprimer ou annuler;
- Déposer une valeur (action similaire à coller);
- Toute saisie au clavier effectuée par l'utilisateur ; dans ce cas, l'événement `On After Edit` est généré après les événements [`On Before Keystroke`](onBeforeKeystroke.md) et [`On After Keystroke`](onAfterKeystroke.md), s'ils sont utilisés.
- Toute modification apportée à l'aide d'une commande de langage qui simule une action de l'utilisateur (c'est-à-dire `POST KEY`).

Dans l'événement `On After Edit`, les données texte saisies sont retournées par la commande [`Get edited text`](../commands-legacy/get-edited-text.md).

### 4D View Pro

L'objet retourné par la commande `FORM Event` contient :

| Propriété   | Type        | Description                                                                                         |
| ----------- | ----------- | --------------------------------------------------------------------------------------------------- |
| code        | entier long | On After Edit                                                                                       |
| Description | text        | "On After Edit"                                                                                     |
| objectName  | text        | Nom de la zone 4D View Pro                                                                          |
| sheetName   | text        | Nom de la feuille de l'événement                                                                    |
| action      | text        | "editChange", "valueChanged", "DragDropBlock", "DragFillBlock", "formulaChanged", "clipboardPasted" |

En fonction de la valeur de la propriété `action`, l'[objet event](overview.md#event-object) contiendra des propriétés supplémentaires.

#### action = editChange

| Propriété   | Type    | Description                              |
| ----------- | ------- | ---------------------------------------- |
| range       | object  | Plage de cellule                         |
| editingText | variant | La valeur provenant de l'éditeur courant |

#### action = valueChanged

| Propriété | Type    | Description                                |
| --------- | ------- | ------------------------------------------ |
| range     | object  | Plage de cellule                           |
| oldValue  | variant | Valeur de la cellule avant la modification |
| newValue  | variant | Valeur de la cellule après la modification |

#### action = DragDropBlock

| Propriété | Type    | Description                                                          |
| --------- | ------- | -------------------------------------------------------------------- |
| fromRange | object  | Plage de cellule source (qui est glissée)         |
| toRange   | object  | Plage de cellule de destination (qui est déposée) |
| copy      | boolean | Indique si la plage source est copiée ou non                         |
| insert    | boolean | Indique si la plage source est insérée ou non                        |

#### action = DragFillBlock

| Propriété     | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fillRange     | object      | Plage utilisée pour le remplissage                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| autoFillType  | entier long | Value used for the fill.<li>0: Cells are filled with all data (values, formatting, and formulas)</li><li>1: Cells are filled with automatically sequential data</li><li>2: Cells are filled with formatting only</li><li>3: Cells are filled with values but not formatting</li><li>4: Values are removed from the cells</li><li>5: Cells are filled automatically</li> |
| fillDirection | entier long | Direction of the fill.<li>0: The cells to the left are filled</li><li>1: The cells to the right are filled</li><li>2: The cells above are filled</li><li>3: The cells below are filled</li>                                                                                                                                                                                                                                |

#### action = formulaChanged

| Propriété | Type   | Description       |
| --------- | ------ | ----------------- |
| range     | object | Plage de cellule  |
| formula   | text   | La formule saisie |

#### action = clipboardPasted

| Propriété   | Type        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ----------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| range       | object      | Plage de cellule                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| pasteOption | entier long | Spécifie ce qui est collé depuis le presse-papiers :<li>0: Tout est collé (valeurs, formatage, et formules)</li><li> 1: Seules les valeurs sont collées</li><li>2: Seul le formatage est collé</li><li>3: Seules les formules sont collées</li><li>4: Les valeurs et le formatage sont collés (pas les formules)</li><li>5: Les formules et le formatage sont collés (pas les valeurs)</li> |
| pasteData   | object      | Les données du presse-papiers à coller<li>"text" (texte) : Le texte du presse-papiers</li><li>"html" (texte) : Le HTML du presse-papiers</li>                                                                                                                                                                                                                                                                                                                                                  |

#### Exemple

Voici un exemple qui gère l'événement `On After Edit` :

```4d
 If(FORM Event.code=On After Edit)
    If(FORM Event.action="valueChanged")
       ALERT("WARNING: You are currently changing the value\  
       from "+String(FORM Event.oldValue)+\  
       " to "+String(FORM Event.newValue)+"!")
    End if
 End if
```

L'exemple ci-dessus pourrait générer un objet événement tel que celui-ci :

```
{

"code":45;
"description":"On After Edit";
"objectName":"ViewProArea"
"sheetname":"Sheet1";
"action":"valueChanged";
"range": {area:ViewProArea,ranges:[{column:1,row:2,sheet:1}]};
"oldValue":"The quick brown fox";
"newValue":"jumped over the lazy dog";
}
```
