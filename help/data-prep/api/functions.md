---
keywords: Experience Platform ; accueil ; rubriques populaires ; prép. de données ; api guide ; schémas ;
solution: Experience Platform
title: Point de terminaison de l'API schémas
topic-legacy: schemas
description: Vous pouvez utiliser le point de terminaison `/fonctions` dans l’API Adobe Experience Platform pour valider vos expressions de mappage et les fonctions de jeu de mappage disponibles de liste.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 12%

---

# Points de terminaison des fonctions

Les fonctions d’ensemble de mappages vous permettent de transformer vos données entre les schémas source et de destination. Vous pouvez utiliser le point de terminaison `/languages/el` pour valider vos expressions et obtenir une liste de toutes les fonctions de jeu de mappages disponibles.

## Valider les expressions

Vous pouvez vérifier si votre expression actuelle est valide en adressant une requête de POST au point de terminaison `/languages/el/validate`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec l’état de validation de l’expression.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Fonctions de jeu de mappage de listes

Vous pouvez récupérer une liste de toutes les fonctions de jeu de correspondances disponibles en adressant une demande de GET au point de terminaison `/languages/el/functions`.

**Format d’API**

```
GET /languages/el/functions
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec une liste de toutes les fonctions de jeu de correspondances disponibles.

>[!NOTE]
>
>Cette réponse a été tronquée pour l’espace.

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

## Opérateurs de jeu de mappage de listes

Vous pouvez récupérer une liste de tous les opérateurs de jeux de correspondances disponibles en adressant une demande de GET au point de terminaison `/languages/el/operators`.

**Format d’API**

```
GET /languages/el/operators
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec une liste de tous les opérateurs de jeu de mappages disponibles.

>[!NOTE]
>
>Cette réponse a été tronquée pour l’espace.

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
