---
keywords: Experience Platform;accueil;mappeur;jeu de mappages;mappage;
solution: Experience Platform
title: Présentation des jeux de mappages
description: Découvrez comment utiliser les jeux de mappages avec la préparation de données Adobe Experience Platform.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 95%

---

# Présentation des jeux de mappages

Un jeu de mappages est un ensemble de mappages qui transforme les données d’un schéma en un autre. Ce document fournit des informations sur la composition des jeux de mappages, y compris le schéma d’entrée, le schéma de sortie et les mappages.

## Prise en main

Cette présentation d’ nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [Préparation de données](./home.md) : la préparation des données permet aux ingénieur(e)s de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).
- [Flux de données](../dataflows/home.md) : les flux de données sont une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers [!DNL Identity] et [!DNL Profile], et vers [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md) : méthodes par lesquelles les données peuvent être envoyées à [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.

## Syntaxe du jeu de mappages

Un jeu de mappages se compose d’un identifiant, d’un nom, d’un schéma d’entrée, d’un schéma de sortie et d’une liste des mappages associés.

Le fichier JSON suivant est un exemple de jeu de mappages type :

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name": "Id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant unique du jeu de mappages. |
| `name` | Nom du jeu de mappages. |
| `inputSchema` | Schéma XDM pour les données entrantes. |
| `outputSchema` | Le schéma XDM des données d’entrée sera transformé pour être conforme. |
| `mappings` | Tableau de mappages champ à champ du schéma source au schéma de destination. |
| `sourceType` | Pour chaque mappage répertorié, son attribut `sourceType` indique le type de source à mapper. Peut être l’une des valeurs suivantes : `ATTRIBUTE`, `STATIC` ou `EXPRESSION` : <ul><li> `ATTRIBUTE` est utilisé pour toute valeur trouvée dans le chemin d’accès source. </li><li>`STATIC` est utilisé pour les valeurs injectées dans le chemin d’accès de destination. Cette valeur reste constante et n’est pas affectée par le schéma source.</li><li> `EXPRESSION` est utilisé pour une expression qui sera résolue au moment de l’exécution. Vous trouverez une liste des expressions disponibles dans le [guide des fonctions de mappage](./functions.md).</li> </ul> |
| `source` | Pour chaque mappage répertorié, l’attribut `source` indique le champ que vous souhaitez mapper. Vous trouverez plus d’informations sur la configuration de votre source dans la [présentation des sources](../sources/home.md). |
| `destination` | Pour chaque mappage répertorié, l’attribut `destination` indique le champ, ou le chemin d’accès au champ, où sera placée la valeur extraite du champ `source`. Vous trouverez plus d’informations sur la configuration de vos destinations dans la [présentation des destinations](../destinations/home.md). |
| `mappings.name` | (*Facultatif*) Nom du mappage. |
| `mappings.description` | (*Facultatif*) Description du mappage. |

## Configuration des sources de mappage

Dans un mappage, la valeur `source` peut être un champ, une expression ou une valeur statique. En fonction du type de source donné, la valeur peut être extraite de différentes manières.

### Champ dans les données en colonnes

Lors du mappage d’un champ dans les données en colonnes, comme un fichier CSV, utilisez le type de source `ATTRIBUTE`. Si le champ contient `.` dans son nom, utilisez `\` pour ignorer la valeur. Voici un exemple de ce mappage :

**Exemple de fichier CSV :**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Exemple de mappage**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Champ dans les données imbriquées

Lors du mappage d’un champ dans des données imbriquées, comme un fichier JSON, utilisez le type de source `ATTRIBUTE`. Si le champ contient `.` dans son nom, utilisez `\` pour ignorer la valeur. Voici un exemple de ce mappage :

**Exemple de fichier JSON**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exemple de mappage**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Champ dans un tableau

Lors du mappage d’un champ dans un tableau, vous pouvez récupérer une valeur spécifique à l’aide d’un index. Pour ce faire, utilisez le type de source `ATTRIBUTE` et l’index de la valeur que vous souhaitez mapper. Voici un exemple de ce mappage :

**Exemple de fichier JSON**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemple de mappage**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### Tableau à tableau ou objet à objet

En utilisant le type de source `ATTRIBUTE`, vous pouvez également mapper directement un tableau à un tableau ou un objet à un objet. Voici un exemple de ce mappage :

**Exemple de fichier JSON**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemple de mappage**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### Opérations itératives sur les tableaux

En utilisant le type de source `ATTRIBUTE`, vous pouvez lire en boucle itérative les tableaux et les mapper à un schéma cible à l’aide d’un index de caractères génériques (`[*]`). Voici un exemple de ce mappage :

**Exemple de fichier JSON**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemple de mappage**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### Valeur constante

Si vous souhaitez mapper une valeur constante ou une valeur statique, utilisez le type de source `STATIC`.  Lors de l’utilisation du type de source `STATIC`, la valeur `source` représente la valeur codée en dur que vous souhaitez affecter à `destination`. Voici un exemple de ce mappage :

**Exemple de fichier JSON**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Exemple de mappage**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**Données transformées**

```json
{
    "userType:": "CUSTOMER"
}
```

### Expressions

Si vous souhaitez mapper une expression, utilisez le type de source `EXPRESSION`. Vous trouverez une liste des fonctions acceptées dans le [guide des fonctions de mappage](./functions.md). Lors de l’utilisation du type de source `EXPRESSION`, `source` représente la fonction que vous souhaitez résoudre. Voici un exemple de ce mappage :

**Exemple de fichier JSON**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Exemple de mappage**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**Données transformées**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## Configuration des destinations de mappage

Dans un mappage, `destination` est l’emplacement où la valeur extraite de `source` sera insérée.

### Champ au niveau racine

Lorsque vous souhaitez mapper la valeur `source` au niveau racine de vos données transformées, suivez l’exemple ci-dessous :

**Exemple de fichier JSON**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exemple de mappage**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "name": "John Smith"
}
```

### Champ imbriqué

Lorsque vous souhaitez mapper la valeur `source` à un champ imbriqué dans vos données transformées, suivez l’exemple ci-dessous :

**Exemple de fichier JSON**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Exemple de mappage**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Champ à un index de tableau spécifique

Lorsque vous souhaitez mapper la valeur `source` à un index spécifique dans un tableau de vos données transformées, suivez l’exemple ci-dessous :

**Exemple de fichier JSON**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exemple de mappage**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "piList": ["John Smith"]
}
```

### Opération de tableau itératif

Lorsque vous souhaitez lire en boucle itérative les tableaux et mapper les valeurs à la cible, vous pouvez utiliser un index de caractère générique (`[*]`). Voici un exemple :

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemple de mappage**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Données transformées**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## Étapes suivantes

En lisant ce document, vous devriez à présent comprendre comment les jeux de mappages sont construits, et notamment comment configurer des mappages individuels dans un jeu de mappages. Pour plus d’informations sur les autres fonctionnalités de la préparation des données, consultez la [présentation de la préparation des données](./home.md). Pour savoir comment utiliser les jeux de mappages dans l’API Data Prep, consultez le [guide de développement de la préparation des données](./api/overview.md).
