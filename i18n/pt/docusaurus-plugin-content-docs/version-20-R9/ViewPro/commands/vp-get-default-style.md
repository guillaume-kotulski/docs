---
id: vp-get-default-style
title: VP Get default style
---

<!-- REF #_method_.VP Get default style.Syntax -->

**VP Get default style** ( *vpAreaName* : Text { ; *sheet* :  Integer } ) : Object<!-- END REF -->

<!-- REF #_method_.VP Get default style.Params -->

| Parâmetro  | Tipo    |                             | Descrição                                                   |                  |
| ---------- | ------- | --------------------------- | ----------------------------------------------------------- | ---------------- |
| vpAreaName | Text    | ->                          | Nome da área 4D View Pro no formulário                      |                  |
| sheet      | Integer | ->                          | Índice da folha (folha atual se omitida) |                  |
| Resultados | Object  | <- | Configurações de estilo padrão                              | <!-- END REF --> |

## Descrição

O comando `VP Get default style` <!-- REF #_method_.VP Get default style.Summary -->retorna um objeto de estilo padrão para uma folha<!-- END REF -->. O objeto retornado contém propriedades básicas de renderização de documentos, bem como as configurações de estilo padrão (se houver) previamente definidas pelo método [VP SET DEFAULT STYLE](vp-set-default-style.md). Para obter mais informações sobre propriedades de estilo, consulte [objetos e folhas de estilo](../configuring.md#style-objects--style-sheets).

Em *vpAreaName*, passe o nome da propriedade da área 4D View Pro. Se passar um nome que não existe, é devolvido um erro.

You can define where to get the column count in the optional *sheet* parameter using the sheet index (counting begins at 0). Se omitido ou se você passar `vk current sheet`, a planilha atual será usada.

## Exemplo

Para obter os detalhes sobre o estilo predefinido para este documento:

![](../../assets/en/ViewPro/cmd_vpGetDefaultStyle.PNG)

Este código:

```4d
$defaultStyle:=VP Get default style("myDoc")
```

devolverá esta informação no objeto *$defaultStyle*:

```4d
{
 backColor:#E6E6FA,
 hAlign:0,
 vAlign:0,
 font:12pt papyrus
}
```

## Veja também

[VP Get cell style](vp-get-cell-style.md)<br/>
[VP SET DEFAULT STYLE](vp-set-default-style.md)
