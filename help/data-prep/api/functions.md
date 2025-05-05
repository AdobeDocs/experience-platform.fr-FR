---
keywords: Experience Platform;accueil;rubriques les plus consultées;préparation des données;guide de l’api;schémas;
title: Point de terminaison de l’API des fonctions
description: Vous pouvez utiliser le point d’entrée &grave;/function&grave; dans l’API Data Prep pour valider vos expressions de mappage et répertorier les fonctions d’ensemble de mappages disponibles.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 87%

---

# Points d’entrée des fonctions

Les fonctions de jeux de mappages vous permettent de transformer vos données entre les schémas source et de destination. Vous pouvez utiliser le point d’entrée `/languages/el` pour valider vos expressions et obtenir une liste de toutes les fonctions de jeux de mappages disponibles.

## Validation des expressions

Vous pouvez vérifier si votre expression actuelle est valide en envoyant une requête POST au point d’entrée `/languages/el/validate`.

**Format d’API**

```
POST /languages/el/validate
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec le statut de validation de l’expression.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Liste des fonctions de jeux de mappages

Vous pouvez récupérer une liste de toutes les fonctions de jeux de mappages disponibles en envoyant une requête GET au point d’entrée `/languages/el/functions`.

**Format d’API**

```
GET /languages/el/functions
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec une liste de toutes les fonctions de jeux de mappages disponibles.

>[!NOTE]
>
>Cette réponse a été tronquée pour des raisons de place.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## Liste des opérateurs de jeux de mappages

Vous pouvez récupérer une liste de tous les opérateurs de jeux de mappages disponibles en effectuant une requête GET sur le point d’entrée `/languages/el/operators`.

**Format d’API**

```
GET /languages/el/operators
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec une liste de tous les opérateurs de jeux de mappages disponibles.

>[!NOTE]
>
>Cette réponse a été tronquée pour des raisons de place.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
