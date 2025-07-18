---
id: license-info
title: License info
displayed_sidebar: docs
---

<!--REF #_command_.License info.Syntax-->**License info** : Object<!-- END REF-->

<!--REF #_command_.License info.Params-->

| Parâmetro | Tipo   |                             | Descrição                            |
| --------- | ------ | --------------------------- | ------------------------------------ |
| Resultado | Object | &#8592; | Information about the active licence |

<!-- END REF-->

## Descrição

<!--REF #_command_.License info.Summary-->O comando **License info** retorna um objeto que fornece informações detalhadas sobre a licença ativa.<!-- END REF-->

If the command is executed on a 4D application that does not use locally a license (e.g. 4D remote), the command returns a Null object.

O objeto retornado contém as propriedades abaixo:

```json
{
    "name": "string",
    "key": 0,
    "licenseNumber": "string",
    "version": "string",
    "attributes": ["string1", "string2"], // optional
    "userName": "string",
    "userMail": "string",
    "companyName": "string",
    "platforms": ["string1", "string2"],
    "expirationDate": { 
        // details here 
    }, // optional
    "renewalFailureCount": 0, // optional
    "products": [
        { // for each registered expansion product
            "id": 0,
            "name": "string",
            "usedCount": 0,
            "allowedCount": 0,
            "rights": [
                {
                    "count": 0,
                    "expirationDate": { 
                        // details here 
                    } // optional
                }
            ]
        }
    ]
}
```

| **Propriedade**     | **Tipo**               | **Description**                                                                                                                                                                                                                                                                  | **Exemplo**                                                                                                                                       |
| ------------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| name                | string                 | Nome comercial                                                                                                                                                                                                                                                                   | "4D Developer Professional vXX"                                                                                                                   |
| \|                  | number                 | ID of the installed product. A unique number is associated to a 4D application (such as 4D Server, 4D in local mode, 4D Desktop, etc.) Instalado em uma máquina. Esse número é criptografado. | 12356789                                                                                                                                          |
| licenseNumber       | string                 | Número de licença                                                                                                                                                                                                                                                                | "4DDP16XXXXX1123456789"                                                                                                                           |
| version             | string                 | Número de versão do produto                                                                                                                                                                                                                                                      | "16", "16R2"                                                                                                                                      |
| attributes          | coleção de strings     | License type(s) when applicable (optional)                                                                                                                                                                                                 | \["application","OEM"], ["evaluation"\] |
| userName            | string                 | Nome da conta de 4D store                                                                                                                                                                                                                                                        | "John Smith"                                                                                                                                      |
| userMail            | string                 | Email da conta de 4D store                                                                                                                                                                                                                                                       | "john.smith@gmail.com"                                                                               |
| companyName         | string                 | Company name of 4D store account                                                                                                                                                                                                                                                 | "Alpha Cie"                                                                                                                                       |
| platforms           | coleção de strings     | Plataforma(s) de licença                                                                                                                                                                                                                                      | \["macOS", "windows"\]                                                                      |
| expirationDate      | object                 | Date of expiration (optional)                                                                                                                                                                                                                                 | {"day":2, "month":6, "year":2026}                                                                 |
| renewalFailureCount | number                 | Number of unsuccessful automatic renewal attempts for at least one of the product licenses (optional)                                                                                                                                                         | 3                                                                                                                                                 |
| products            | uma coleção de objetos | Description of product license (one element per product license). Ver abaixo.                                                                                                                                                 |                                                                                                                                                   |

Cada objeto da coleção `products` pode ter as seguintes propriedades:

| **Propriedade** |                                                                                            | **Tipo**               | **Description**                                                             | **Exemplo**                                                                                                              |
| --------------- | ------------------------------------------------------------------------------------------ | ---------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| id              |                                                                                            | number                 | Número de licença                                                           | Para saber os valores disponíveis, consulte o comando [Is license available](../commands-legacy/is-license-available.md) |
| name            |                                                                                            | string                 | Nome da licença                                                             | "4D Write - 4D Write Pro"                                                                                                |
| usedCount       |                                                                                            | number                 | Number of consumed connections                                              | 8                                                                                                                        |
| allowedCount    |                                                                                            | number                 | Total connections allowed for the product against the expiry dates          | 15                                                                                                                       |
| rights          |                                                                                            | uma coleção de objetos | Rights for the product (one element per expiration date) |                                                                                                                          |
|                 | \[ \].count          | number                 | Number of allowed connections                                               | 15 (32767 significa ilimitado)                                                                        |
|                 | \[ \].expirationDate | object                 | Date of expiration (optional, same format as above)      | {"day":1, "month":11, "year":2017}                                       |

## Exemplo

You want to get information on your current 4D Server license:

```4d
 var $obj : Object
 $obj:=License info
```

*$obj* pode conter, por exemplo:

```json
{
    "name": "4D Server v16 R3",
    "key": 123456789,
    "licenseNumber": "xxxx",
    "version": "16R3",
    "userName": "John DOE",
    "userMail": "john.doe@alpha.com",
    "companyName": "Alpha",
    "platforms": ["macOS", "windows"],
    "expirationDate": {"day":1, "month":1, "year":2018},
    "products":[
        {
            "allowedCount": 15,
            "id": 808464697,
            "name": "4D Write - 4D Write Pro",
            "rights": [
                {
                    "count": 5,
                    "expirationDate": {"day":1, "month":2, "year":2018}
                }, {
                    "count": 10,
                    "expirationDate": {"day":1, "month":11, "year":2017}
                }, {
                    "count": 10,
                    "expirationDate": {"day":1, "month":11, "year":2015} //expired, not counted
                }
            ],
            "usedCount": 12
        },
        {...}
    ]
}
```

## Veja também

[CHANGE LICENSES](../commands-legacy/change-licenses.md)\
[Is license available](../commands-legacy/is-license-available.md)\
[WEB Get server info](../commands-legacy/web-get-server-info.md)

## Propriedades

|                   |                             |
| ----------------- | --------------------------- |
| Número de comando | 1489                        |
| Thread safe       | &check; |


