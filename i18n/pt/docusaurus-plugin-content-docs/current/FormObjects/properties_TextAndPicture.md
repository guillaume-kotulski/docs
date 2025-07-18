---
id: propertiesTextAndPicture
title: Texto e imagem
---

## Rota de acesso ao Fundo

Define o caminho da imagem que será desenhada no fundo do objeto. Si el objeto utiliza un [icono](#picture-pathname) con [diferentes estados](#number-of-states), la imagen de fondo soportará automáticamente el mismo número de estados.

El nombre de la ruta a introducir es similar al de [ la propiedad Ruta de acceso para las imágenes estáticas](properties_Picture.md#pathname).

#### Gramática JSON

| Nome                    | Tipo de dados | Valores possíveis                                                                                                                                     |
| ----------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| customBackgroundPicture | string        | Caminho relativo na sintaxe POSIX. Deve ser utilizado em conjunto com a opção "Personalizado" da propriedade "Style". |

#### Objectos suportados

[Botón personalizado](button_overview.md#custom) - [Casilla de selección personalizada](checkbox_overview.md#custom) - [Botón radio personalizado](radio_overview.md#custom)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Estilo de botão

Aspeto geral do botão. O estilo do botão também desempenha um papel na disponibilidade de determinadas opções.

#### Gramática JSON

|  Nome | Tipo de dados | Valores possíveis                                                                                                                                                  |
| :---: | :-----------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| style |      text     | "regular", "flat", "toolbar", "bevel", "roundedBevel", "gradientBevel", "texturedBevel", "office", "help", "circular", "disclosure", "roundedDisclosure", "custom" |

#### Objectos suportados

[Botón](button_overview.md) - [Botón radio](radio_overview.md) - [Casilla de selección](checkbox_overview.md) - [Botón Radio](radio_overview.md)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Margem horizontal

Esta propriedade permite definir o tamanho (em píxeis) das margens horizontais do botão. Esta margem delimita a área que o ícone e o título do botão não devem ultrapassar.

Este parâmetro é útil, por exemplo, quando a imagem de fundo contém contornos:

| Com / Sem               | Exemplo                                                      |
| ----------------------- | ------------------------------------------------------------ |
| Sem margem              | ![](../assets/en/FormObjects/property_horizontalMargin1.png) |
| Com margem de 13 píxeis | ![](../assets/en/FormObjects/property_horizontalMargin2.png) |

> Esta propiedad funciona junto con la propiedad [Margen vertical](#vertical-margin).

#### Gramática JSON

| Nome          | Tipo de dados | Valores possíveis                                                                     |
| ------------- | ------------- | ------------------------------------------------------------------------------------- |
| customBorderX | number        | Para utilizar com o estilo "personalizado". Mínimo: 0 |

#### Objectos suportados

[Botón personalizado](button_overview.md#custom) - [Casilla de selección personalizada](checkbox_overview.md#custom) - [Botón radio personalizado](radio_overview.md#custom)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Localização do ícone

Designa a colocação de um ícone em relação ao objeto formulário.

#### Gramática JSON

| Nome          | Tipo de dados | Valores possíveis       |
| ------------- | ------------- | ----------------------- |
| iconPlacement | string        | "none", "left", "right" |

#### Objectos suportados

[Cabeçalho do list box](listbox_overview.md#list-box-headers)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Offset do ícone

Define um valor de desvio personalizado em pixeis, que será utilizado quando se clica no botão

O título do botão será deslocado para a direita e para baixo em função do número de pixeis introduzidos. Isto permite aplicar um efeito 3D personalizado quando o botão é clicado.

#### Gramática JSON

| Nome         | Tipo de dados | Valores possíveis         |
| ------------ | ------------- | ------------------------- |
| customOffset | number        | mínimo: 0 |

#### Objectos suportados

[Botón personalizado](button_overview.md#custom) - [Casilla de selección personalizada](checkbox_overview.md#custom) - [Botón radio personalizado](radio_overview.md#custom)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Número de estados

Esta propiedad define el número exacto de estados presentes en la imagen utilizada como icono para un [botón con icono](button_overview.md), una [casilla de selección](checkbox_overview.md) o un [botón radio](radio_overview.md) personalizado.

A imagem pode conter de 2 a 6 estados.

- 2 estados: false, true
- 3 estados: false, true, rollover,
- 4 estados: false, true, rollover, desativado,
- 5 estados (apenas para caixas de verificação e botões rádio): false, true, false rollover, true rollover, desativado
- 6 estados (apenas para caixas de verificação e botões rádio): false, true, false rollover, true rollover, false desativado, true disable.

:::note

- "false" significa que o botão não foi clicado/não foi selecionado ou que a caixa de seleção não foi marcada (valor da variável=0)
- "true" significa botão clicado/selecionado ou caixa de seleção verificada (variável valor=1)

:::

Cada estado é representado por uma imagem diferente. Na imagem de origem, os estados devem ser empilhados verticalmente:

![](../assets/en/FormObjects/six-states.png)

#### Gramática JSON

| Nome       | Tipo de dados | Valores possíveis                                                               |
| ---------- | ------------- | ------------------------------------------------------------------------------- |
| iconFrames | number        | Número de estados na imagem do ícone. Mínimo: 1 |

#### Objectos suportados

[Botón](button_overview.md) (todos los estilos excepto [Ayuda](button_overview.md#help)) - [Casilla de selección](checkbox_overview.md) - [Botón radio](radio_overview.md)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Caminho da imagem

Define o caminho da imagem que será utilizada como ícone para o objeto.

El nombre de la ruta a introducir es similar al de [ la propiedad Ruta de acceso para las imágenes estáticas](properties_Picture.md#pathname).

> Cuando se utiliza como icono de objetos activos, la imagen debe estar diseñada para soportar un [número de estados](#number-of-states) variable.

#### Gramática JSON

| Nome | Tipo de dados | Valores possíveis                                                |
| ---- | ------------- | ---------------------------------------------------------------- |
| icon | picture       | Caminho relativo ou filesystem na sintaxe POSIX. |

#### Objectos suportados

[Botón](button_overview.md) (todos los estilos excepto [Ayuda](button_overview.md#help)) - [Casilla de selección](checkbox_overview.md) - [Encabezado List Box](listbox_overview.md#list-box-headers) - [Botón radio](radio_overview.md)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Posição título/Imagem

Esta propriedade permite modificar a localização relativa do título do botão em relação ao ícone associado. Esta propriedade não tem efeito quando o botão contém apenas um título (sem imagem associada) ou uma imagem (sem título). Por predefinição, quando um botão contém um título e uma imagem, o texto é colocado por baixo da imagem.

Aqui estão os resultados utilizando as várias opções para esta propriedade:

| Opção        | Descrição                                                                                                                                                             | Exemplo                                                           |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| \*\*Esquerda | O texto é colocado à esquerda do ícone. O conteúdo do botão é alinhado à direita.                                                     | ![](../assets/en/FormObjects/property_titlePosition_left.en.png)  |
| **Superior** | O texto é colocado por cima do ícone. O conteúdo do botão é centrado.                                                                 | ![](../assets/en/FormObjects/property_titlePosition_top.png)      |
| **Direita**  | O texto é colocado à direita do ícone. O conteúdo do botão é alinhado à esquerda.                                                     | ![](../assets/en/FormObjects/property_titlePosition_right.png)    |
| **Fundo**    | O texto é colocado por baixo do ícone. O conteúdo do botão é centrado.                                                                | ![](../assets/en/FormObjects/property_titlePosition_bottom.png)   |
| **Centrado** | O texto do ícone é centrado vertical e horizontalmente no botão. Este parâmetro é útil, por exemplo, para o texto incluído num ícone. | ![](../assets/en/FormObjects/property_titlePosition_centered.png) |

#### Gramática JSON

| Nome          | Tipo de dados | Valores possíveis                          |
| ------------- | ------------- | ------------------------------------------ |
| textPlacement | string        | "left", "top", "right", "bottom", "center" |

#### Objectos suportados

[Botón](button_overview.md) (todos los estilos excepto [Ayuda](button_overview.md#help)) - [Casilla de selección](checkbox_overview.md) - [Botón radio](radio_overview.md)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Image hugs title

Esta propiedad permite definir si el título y la imagen del botón deben estar visualmente contiguos o separados, según las propiedades [Posición del título/imagen](#titlepicture-position) y [Alineación horizontal](properties_Text.md#horizontal-alignment).

Esta propriedade não tem efeito quando o botão contém apenas um título (sem imagem associada) ou uma imagem (sem título).

Por padrão, quando um botão contém um título e uma imagem, os elementos são unidos. El siguiente gráfico muestra el efecto de la propiedad `imageHugsTitle` (true cuando la propiedad está activada) con diferentes alineaciones de los botones:

![](../assets/en/FormObjects/hugs.png)

#### Gramática JSON

| Nome           | Tipo de dados | Valores possíveis                       |
| -------------- | ------------- | --------------------------------------- |
| imageHugsTitle | boolean       | true (padrão), false |

#### Objectos suportados

[Button](button_overview.md) (all styles except Help) - [Check Box](checkbox_overview.md) (all styles except Regular, Flat, Disclosure and Collapse/Expand) - [Radio Button](radio_overview.md) (all styles except Regular, Flat, Disclosure and Collapse/Expand).

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Margem vertical

Esta propriedade permite definir o tamanho (em píxeis) das margens verticais do botão. Esta margem delimita a área que o ícone e o título do botão não devem ultrapassar.

Este parâmetro é útil, por exemplo, quando a imagem de fundo contém contornos.

> Esta propiedad funciona junto con la propiedad [Margen horizontal](#horizontal-margin).

#### Gramática JSON

| Nome          | Tipo de dados | Valores possíveis                                                                     |
| ------------- | ------------- | ------------------------------------------------------------------------------------- |
| customBorderY | number        | Para utilizar com o estilo "personalizado". Mínimo: 0 |

#### Objectos suportados

[Botón personalizado](button_overview.md#custom) - [Casilla de selección personalizada](checkbox_overview.md#custom) - [Botón radio personalizado](radio_overview.md#custom)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

---

## Com menu pop-up

Esta propriedade permite exibir um símbolo que aparece como um triângulo no botão para indicar a presença de um menu pop-up anexado:

![](../assets/en/FormObjects/property_popup.png)

A aparência e o local desse símbolo dependem do estilo do botão e da plataforma atual.

### Ligados e Separados

Para anexar um símbolo de menu pop-up a um botão, há duas opções de exibição disponíveis:

|                          Linked                         |                          Separado                          |
| :-----------------------------------------------------: | :--------------------------------------------------------: |
| ![](../assets/en/FormObjects/property_popup_linked.png) | ![](../assets/en/FormObjects/property_popup_separated.png) |

> A disponibilidade real de um modo "separado" depende do estilo do botão e da plataforma.

Cada opção especifica a relação entre o botão e o menu pop-up anexado:

- Quando o menu pop-up é **separado**, clicar na parte esquerda do botão executa diretamente a ação atual do botão; essa ação pode ser modificada usando o menu pop-up acessível na parte direita do botão.
- Quando o menu pop-up está **vinculado**, um simples clique no botão exibe apenas o menu pop-up. Somente a seleção da ação no menu pop-up causa sua execução.

:::info

Consulte a [descrição do evento `On Alternative Click`](../Events/onAlternativeClick.md) para obter mais informações sobre o tratamento de eventos neste caso.

:::

### Gerir o menu pop-up

É importante notar que a propriedade "Com o Menu Popup" apenas gerencia o aspecto gráfico do botão. The display of the pop-up menu and its values must be handled entirely by the developer, more particularly using [`form events`](../Events/overview.md) and the [`Dynamic pop up menu`](../commands-legacy/dynamic-pop-up-menu.md) and [`Pop up menu`](../commands-legacy/pop-up-menu.md) commands.

#### Gramática JSON

| Nome           | Tipo de dados | Valores possíveis                                    |
| :------------- | ------------- | ---------------------------------------------------- |
| popupPlacement | string        | <li>"none"</li><li>"linked"</li><li>"separated"</li> |

#### Objectos suportados

[Toolbar Button](button_overview.md#toolbar) - [Bevel Button](button_overview.md#bevel) - [Rounded Bevel Button](button_overview.md#rounded-bevel) - [OS X Gradient Button](button_overview.md#os-x-gradient) - [OS X Textured Button](button_overview.md#os-x-textured) - [Office XP Button](button_overview.md#office-xp) - [Circle Button](button_overview.md#circle) - [Custom](button_overview.md#custom)

#### Comandos

[OBJECT Get format](../commands-legacy/object-get-format.md) [OBJECT Get minimum-value](../commands-legacy/object-get-minimum-value.md) - [OBJECT SET FORMAT](../commands-legacy/object-set-format.md)

