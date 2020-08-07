---
id: queryplan
title: '$queryplan'
---


Retourne la requête telle qu'elle a été passée au 4D Server (par exemple, `$queryplan=true`)

## Description
$queryplan returns the query plan as it was passed to 4D Server.

| Propriété | Type    | Description                                                                                 |
| --------- | ------- | ------------------------------------------------------------------------------------------- |
| item      | Chaine  | Actual query executed                                                                       |
| subquery  | Tableau | If there is a subquery, an additional object containing an item property (as the one above) |

For more information about query plans, refer to [queryPlan and queryPath](genInfo.md#querypath-and-queryplan).

## Exemple
If you pass the following query:

 `GET  /rest/People/$filter="employer.name=acme AND lastName=Jones"&$queryplan=true`

#### Response:

```
__queryPlan: {
    And: [
        {
            item: "Join on Table : Company : People.employer = Company.ID",
            subquery: [
                {
                    item: "Company.name = acme"
                }
            ]
        },
        {
            item: "People.lastName = Jones"
        }
    ]
}
```
