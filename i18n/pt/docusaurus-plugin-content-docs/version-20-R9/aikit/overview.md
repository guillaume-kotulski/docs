---
id: overview
title: 4D-AIKit
---

# 4D-AIKit

## Visão Geral

4D AIKit is a built-in 4D component that enables interaction with third-party AI APIs.

## OpenAI

La clase [`OpenAI`](Classes/OpenAI.md) permite realizar peticiones a la [API OpenAI](https://platform.openai.com/docs/api-reference/).

### Configuração

First of all, initialize the OpenAI client using your API key

```4d
var $client:=cs.AIKit.OpenAI.new("your api key")
```

For a [compatible provider](compatible-openai.md) API, you can configure the server URL by setting the `baseURL` parameter.

```4d
var $client:=cs.AIKit.OpenAI.new({apiKey: "your api key"; baseURL: "https://your.server.ai"})
```

ou

```4d
$client.baseURL:="https://your.server.ai"
```

### Fazer solicitações

`OpenAI` provides different endpoints called resources, each offering various functions.

```4d
var $result:=$client.<resource>.<function>(<parameters...>)
```

O `$result` contém o `HTTPRequest`, um status de `sucess`, uma coleção de `erros` e outros. Ver [OpenAIResult](Classes/OpenAIResult.md)

Veja alguns exemplos abaixo.

#### Chat

https://platform.openai.com/docs/api-reference/chat

##### Completions

https://platform.openai.com/docs/api-reference/chat/create

```4d
var $messages:=[{role: "system"; content: "You are a helpful assistant."}]
$messages.push({role: "user"; content: "Could you explain me why 42 is a special number"})
var $result:=$client.chat.completions.create($messages; {model: "gpt-4o-mini"})
// result in $result.choice
```

##### Chat helper

This helper allows you to maintain a list of user messages and assistant responses.

```4d
var $helper:=$client.chat.create("You are a helpful assistant.")
var $result:=$helper.prompt("Could you explain me why 42 is a special number")
$result:=$helper.prompt("and could you decompose this number")
// conversation in $helper.messages
```

##### Vision helper

This helper enables image analysis through the chat.

```4d
var $result:=$client.chat.vision.create($imageUrl).prompt("give me a description of the image")
```

#### Images

https://platform.openai.com/docs/api-reference/images

```4d
var $images:=$client.images.generate("A futuristic city skyline at sunset"; {size: "1024x1024"}).images
```

#### Models

https://platform.openai.com/docs/api-reference/models

Get full list of models

```4d
var $models:=$client.models.list().models // você pode então extrair o `id`
```

Get one model information by id

```4d
var $model:=$client.models.retrieve("a model id").model
```

#### Moderations

https://platform.openai.com/docs/api-reference/moderations

```4d
var $moderation:=$client.moderations.create("This text contains inappropriate language and offensive behavior.").moderation
```

#### Código assíncrono

If you do not want to wait for the OpenAPI response when sending a request to its API, you need to use asynchronous code. The result object will be received in a callback function.

Veja [documentação detalhada para exemplos](asynchronous-call.md)

## Copyright

- This library is not affiliated with, endorsed by, or officially connected to OpenAI in any way.
- "OpenAI" and any related marks are trademarks or registered trademarks of OpenAI, LLC. All rights related to OpenAI's services, APIs, and technologies remain the property of OpenAI.
- This project simply provides an interface to OpenAI’s services and does not claim any ownership over their technology, branding, or intellectual property.

