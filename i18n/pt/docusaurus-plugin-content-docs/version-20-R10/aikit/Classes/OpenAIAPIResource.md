---
id: openaiapiresource
title: OpenAIAPIResource
---

# OpenAIAPIResource

Base class to all api resource.

## Propriedades

| Propriedade | Tipo                | Descrição                              |
| ----------- | ------------------- | -------------------------------------- |
| `_client`   | [OpenAI](OpenAI.md) | Private back link to the OpenAI client |

The client allow to make HTTP Request.

## Classes herdadas

- [OpenAIModelsAPI](OpenAIModelsAPI.md)
- [OpenAIChatAPI](OpenAIChatAPI.md)
- [OpenAIImagesAPI](OpenAIImagesAPI.md)
- [OpenAIModerationsAPI](OpenAIModerationsAPI.md)
