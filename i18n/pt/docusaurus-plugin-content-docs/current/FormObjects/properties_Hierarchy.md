---
id: propertiesHierarchy
title: Hierarquia
---

## List box hierárquica

`List boxes de tipo array`

Essa propriedade especifica que o list box deve ser exibido em forma hierárquica. No formulário JSON, esse recurso é acionado [quando o valor da propriedade *dataSource* é um array](properties_Object.md#array-list-box), ou seja, uma coleção.

Opções adicionais (**Variable 1...10**) estão disponíveis quando a opção *List Box hierárquico* é selecionada, correspondendo a cada array *dataSource* a ser usado como coluna de quebra. A cada vez que um valor é digitado em um campo, uma nova linha é adicionada. Podem ser especificadas até 10 variáveis. Essas variáveis estabelecem os níveis hierárquicos a serem exibidos na primeira coluna.

Ver [List box jerárquicos](listbox_overview.md#hierarchical-list-boxes)

#### Gramática JSON

| Nome       | Tipo de dados | Valores possíveis                                   |
| ---------- | ------------- | --------------------------------------------------- |
| datasource | array string  | Coleção de nomes de matriz que definem a hierarquia |

#### Objectos suportados

[List Box](listbox_overview.md)

#### Comandos

[LISTBOX GET HIERARCHY](../commands-legacy/listbox-get-hierarchy.md) - [LISTBOX SET HIERARCHY](../commands-legacy/listbox-set-headers-height.md)


