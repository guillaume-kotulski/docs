---
id: vp-get-binding-path
title: VP Get binding path
---

<details><summary>História</summary>

| Release | Mudanças   |
| ------- | ---------- |
| 19 R5   | Adicionado |

</details>

<!-- REF #_method_.VP Get binding path.Syntax -->

**VP Get binding path** ( *rangeObj* : Object ) : Text<!-- END REF -->

<!-- REF #_method_.VP Get binding path.Params -->

| Parâmetro  | Tipo   |                             | Descrição                        |                  |
| ---------- | ------ | --------------------------- | -------------------------------- | ---------------- |
| rangeObj   | Object | ->                          | Objeto intervalo                 |                  |
| Resultados | Text   | <- | Nome do atributo ligado à célula | <!-- END REF --> |

## Descrição

O comando `VP Get binding path` <!-- REF #_method_.VP Get binding path.Summary -->retorna o nome do atributo vinculado à célula especificada no *rangeObj*<!-- END REF -->.

Em *rangeObj*, passe um objeto que seja um intervalo de células ou um intervalo combinado de células. Note que:

- Se *rangeObj* for um intervalo com várias células, o comando retornará o nome do atributo vinculado à primeira célula do intervalo.
- If *rangeObj* contains several ranges of cells, the command returns the attribute name linked to the first cell of the first range.

## Exemplo

```4d
var $p; $options : Object
var $myAttribute : Text

$p:=New object
$p.firstName:="Freehafer"
$p.lastName:="Nancy" VP SET DATA CONTEXT("ViewProArea"; $p) VP SET BINDING PATH(VP Cell("ViewProArea"; 0; 0); "firstName")
VP SET BINDING PATH(VP Cell("ViewProArea"; 1; 0); "lastName")

$myAttribute:=VP Get binding path(VP Cell("ViewProArea"; 1; 0)) // "lastName"
```

## Veja também

[VP SET BINDING PATH](vp-set-binding-path.md)<br/>
[VP Get data context](vp-get-data-context.md)<br/>
[VP SET DATA CONTEXT](vp-get-data-context.md)
