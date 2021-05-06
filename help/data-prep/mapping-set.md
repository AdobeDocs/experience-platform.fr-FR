---
keywords: Experience Platform ; accueil ; mappeur ; jeu de mappages ; mappage ;
solution: Experience Platform
title: Présentation des jeux de mappages
topic: aperçu
description: Découvrez comment utiliser des jeux de mappage avec Adobe Experience Platform Data Prep.
translation-type: tm+mt
source-git-commit: 4c06f621eb6fba8daa6501d56255cddbbcfdbda2
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 5%

---


# Présentation des jeux de mappages

Un jeu de mappages est un ensemble de mappages qui transforme les données d’un schéma à l’autre. Ce document fournit des informations sur la composition des jeux de mappages, y compris le schéma d’entrée, le schéma de sortie et les mappages.

## Prise en main

Cette présentation nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

- [Prép](./home.md) de données : La préparation des données permet aux ingénieurs de données de mapper, de transformer et de valider les données à partir du modèle de données d’expérience (XDM).
- [Flux](../dataflows/home.md) de données : Les flux de données sont une représentation des tâches de données qui déplacent les données entre les plateformes. Les flux de données sont configurés entre différents services, ce qui permet de déplacer les données des connecteurs source vers des jeux de données de cible, vers [!DNL Identity] et [!DNL Profile] et vers [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Méthodes d’envoi des données à  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.

## Syntaxe de l’ensemble de mappages

Un jeu de mappages comprend un ID, un nom, un schéma d’entrée, un schéma de sortie et une liste de mappages associés.

Le fichier JSON suivant est un exemple de jeu de correspondances type :

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
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
            "name" : "Id",
            "description" : "Identifier field"
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
| `id` | Identificateur unique du jeu de mappages. |
| `name` | Nom de la visionneuse de mappages. |
| `inputSchema` | Schéma XDM pour les données entrantes. |
| `outputSchema` | Schéma XDM auquel les données d’entrée ont été converties pour se conformer. |
| `mappings` | Tableau de correspondances champ par champ entre le schéma source et le schéma de destination. |
| `sourceType` | Pour chaque mappage répertorié, son attribut `sourceType` indique le type de source à mapper. Peut être l&#39;une des valeurs suivantes : `ATTRIBUTE`, `STATIC` ou `EXPRESSION` : <ul><li> `ATTRIBUTE` est utilisée pour toute valeur trouvée dans le chemin source. </li><li>`STATIC` est utilisée pour les valeurs injectées dans le chemin de destination. Cette valeur reste constante et n’est pas affectée par le schéma source.</li><li> `EXPRESSION` est utilisée pour une expression, qui sera résolue lors de l’exécution. Vous trouverez une liste des expressions disponibles dans le [guide des fonctions de mappage](./functions.md).</li> </ul> |
| `source` | Pour chaque mappage répertorié, l&#39;attribut `source` indique le champ à mapper. Pour plus d&#39;informations sur la configuration de votre source, consultez la section [sources](#sources). |
| `destination` | Pour chaque mappage répertorié, l&#39;attribut `destination` indique le champ, ou le chemin d&#39;accès au champ, où sera placée la valeur extraite du champ `source`. Pour plus d&#39;informations sur la configuration de vos destinations, consultez la section [destination](#destination). |
| `mappings.name` | (*Facultatif*) Nom du mappage. |
| `mappings.description` | (*Facultatif*) Description du mappage. |

## Configuration des sources de mappage

Dans un mappage, `source` peut être un champ, une expression ou une valeur statique. En fonction du type de source indiqué, la valeur peut être extraite de différentes manières.

### Champ dans les données de colonne

Lors du mappage d’un champ dans des données de colonne, telles qu’un fichier CSV, utilisez le type de source `ATTRIBUTE`. Si le champ contient `.` dans son nom, utilisez `\` pour échapper la valeur. Vous trouverez un exemple de cette correspondance ci-dessous :

**Exemple de fichier CSV :**

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

Lors du mappage d’un champ dans des données imbriquées, telles qu’un fichier JSON, utilisez le type de source `ATTRIBUTE`. Si le champ contient `.` dans son nom, utilisez `\` pour échapper la valeur. Vous trouverez un exemple de cette correspondance ci-dessous :

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

Lors du mappage d&#39;un champ dans un tableau, vous pouvez récupérer une valeur spécifique à l&#39;aide d&#39;un index. Pour ce faire, utilisez le type de source `ATTRIBUTE` et l’index de la valeur à mapper. Vous trouverez un exemple de cette correspondance ci-dessous :

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

En utilisant le type de source `ATTRIBUTE`, vous pouvez également mapper directement un tableau à un tableau ou à un objet à un objet. Vous trouverez un exemple de cette correspondance ci-dessous :

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

### Opérations itératives sur les baies

En utilisant le type de source `ATTRIBUTE`, vous pouvez effectuer une boucle à travers les tableaux et les mapper à un schéma de cible en utilisant un index générique (`[*]`). Vous trouverez un exemple de cette correspondance ci-dessous :

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

Si vous souhaitez mapper une constante ou une valeur statique, utilisez le type de source `STATIC`.  Lorsque vous utilisez le type de source `STATIC`, `source` représente la valeur codée en dur que vous souhaitez affecter à `destination`. Vous trouverez un exemple de cette correspondance ci-dessous :

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

Si vous souhaitez mapper une expression, utilisez le type de source `EXPRESSION`. Vous trouverez une liste des fonctions acceptées dans le [guide des fonctions de mappage](./functions.md). Lorsque vous utilisez le type de source `EXPRESSION`, `source` représente la fonction à résoudre. Vous trouverez un exemple de cette correspondance ci-dessous :

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

Dans un mappage, `destination` est l&#39;emplacement où la valeur extraite de `source` sera insérée.

### Champ au niveau racine

Pour mapper la valeur `source` au niveau racine de vos données transformées, suivez l’exemple ci-dessous :

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

Pour mapper la valeur `source` à un champ imbriqué dans vos données transformées, suivez l’exemple ci-dessous :

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

Pour mapper la valeur `source` à un index spécifique dans un tableau de données transformées, suivez l&#39;exemple ci-dessous :

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

Lorsque vous souhaitez effectuer une boucle itérative dans les tableaux et mapper les valeurs à la cible, vous pouvez utiliser un index générique (`[*]`). Voici un exemple :

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

En lisant ce document, vous devez maintenant comprendre comment les jeux de mappages sont créés, y compris comment configurer les mappages individuels dans un jeu de mappages. Pour plus d’informations sur les autres fonctionnalités d’aperçu des données, consultez la section [Présentation de l’aperçu de l’aperçu des données ](./home.md). Pour savoir comment utiliser les jeux de mappage dans l’API d’aperçu des données, consultez le [Guide du développeur d’API d’aperçu des données](./api/overview.md).