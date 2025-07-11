---
id: openaivisionhelper
title: OpenAIVisionHelper
---

# OpenAIVisionHelper

## Funções

### prompt()

**prompt**(*prompt*: Test; *parameters* : OpenAIChatCompletionsParameters)

| Parâmetro    | Tipo                                                                  | Descrição                                                            |
| ------------ | --------------------------------------------------------------------- | -------------------------------------------------------------------- |
| *prompt*     | Text                                                                  | The text prompt to send to the OpenAI chat API.      |
| *parâmetros* | [OpenAIChatCompletionsParameters](OpenAIChatCompletionsParameters.md) | Optional parameters for the chat completion request. |
| Resultado    | [OpenAIChatCompletionsResult](OpenAIChatCompletionsResult.md)         | O resultado da visão.                                |

Sends a prompt to the OpenAI chat API along with an associated image URL, and optionally accepts parameters for the chat completion.

#### Exemplo de uso

```4d
var $helper:=$client.chat.vision.create("http://example.com/image.jpg")

var $result:=$helper.prompt("Could you describe?")

$result:=$helper.prompt("Have any red element?"; {model: "gpt-4o-mini"; max_completion_tokens: 100 })
```