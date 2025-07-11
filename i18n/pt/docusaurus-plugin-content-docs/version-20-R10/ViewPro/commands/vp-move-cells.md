---
id: vp-move-cells
title: VP MOVE CELLS
---

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 19 R4   | Adicionado |

</details>

<!-- REF #_method_.VP MOVE CELLS.Syntax -->

**VP MOVE CELLS** ( *originRange* : Object ; *targetRange* : Object ; *options* : Object )<!-- END REF -->

<!-- REF #_method_.VP MOVE CELLS.Params -->

| Parâmetro   | Tipo   |    | Descrição                                                   |                  |
| ----------- | ------ | -- | ----------------------------------------------------------- | ---------------- |
| originRange | Object | -> | Intervalo de células a partir do qual copiar                |                  |
| targetRange | Object | -> | Intervalo de destino para os valores, formatação e fórmulas |                  |
| options     | Object | -> | Opções adicionais                                           | <!-- END REF --> |

## Descrição

O comando `VP MOVE CELLS` <!-- REF #_method_.VP MOVE CELLS.Summary --> move ou copia os valores, estilo e fórmulas de *originRange* para *targetRange*<!-- END REF -->.

*originRange* e *targetRange* podem se referir a áreas View Pro diferentes.

In *originRange*, pass a range object containing the values, style, and formula cells to copy or move. Se *originRange* for um intervalo combinado, somente o primeiro será usado.

Em *targetRange*, passe o intervalo de células onde os valores de célula, estilo e fórmulas serão copiados ou movidos.

O parâmetro *options* tem várias propriedades:

| Propriedade  | Tipo       | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------ | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| copy         | Parâmetros | Determines if the values, formatting and formulas of the cells in *originRange* are removed after the command executes:<ul><li>*False* (default) to remove them</li><li>*True* to keep them</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| pasteOptions | Integer    | Especifica o que é colado. Possible values: <p><table><tr><th>Value</th><th>Description</th></tr><tr><td>`vk clipboard options all` (default)</td><td>Pastes all data objects, including values, formatting, and formulas.</td></tr><tr><td>`vk clipboard options formatting`</td><td>Pastes only the formatting.</td></tr><tr><td>`vk clipboard options formulas`</td><td>Pastes only the formulas.</td></tr><tr><td>`vk clipboard options formulas and formatting`</td><td>Pastes the formulas and formatting.</td></tr><tr><td>`vk clipboard options values`</td><td>Pastes only the values.</td></tr><tr><td>`vk clipboard options value and formatting`</td><td>Pastes the values and formatting.</td></tr></table></p> |

As opções de colagem definidas nas [opções de workbook](#vp-set-workbook-options) são tomadas em conta.

## Exemplo

Para copiar os conteúdos, valores, formatação e fórmulas de um intervalo de origem:

```4d
var $originRange; $targetRange; $options : Object

$originRange:=VP Cells("ViewProArea"; 0; 0; 2; 5)

$targetRange:=VP Cells("ViewProArea"; 4; 0; 2; 5)

$options:=New object
$options.copy:=True
$options.pasteOptions:=vk clipboard options all

VP MOVE CELLS($originRange; $targetRange; $options)
```

## Veja também

[VP Copy to object](vp-copy-to-object.md)<br/>
[VP PASTE FROM OBJECT](vp-paste-from-object.md)<br/>
[VP SET WORKBOOK OPTIONS](vp-set-workbook-options.md)