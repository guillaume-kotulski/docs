---
id: vp-row-autofit
title: VP ROW AUTOFIT
---

<!-- REF #_method_.VP ROW AUTOFIT.Syntax -->

**VP ROW AUTOFIT** ( *rangeObj* : Object) <!-- END REF -->

<!-- REF #_method_.VP ROW AUTOFIT.Params -->

| Parâmetro | Tipo   |    | Descrição        |                  |
| --------- | ------ | -- | ---------------- | ---------------- |
| rangeObj  | Object | -> | Objeto intervalo | <!-- END REF --> |

## Descrição

O comando `VP ROW AUTOFIT` <!-- REF #_method_.VP ROW AUTOFIT.Summary -->dimensiona automaticamente a(s) linha(s) em *rangeObj* de acordo com seu conteúdo<!-- END REF -->.

No *rangeObj*, passe um objeto de alcance que contém um intervalo de linhas cujo tamanho será tratado automaticamente.

## Exemplo

As linhas seguintes não apresentam corretamente o texto:

![](../../assets/en/ViewPro/cmd_vpRowAutoFit1.PNG)

```4d
 VP ROW AUTOFIT(VP Row("ViewProArea";1;2))
```

Resultados:

![](../../assets/en/ViewPro/cmd_vpRowAutoFit2.PNG)

## Veja também

[VP Column autofit](vp-column-autofit.md)

