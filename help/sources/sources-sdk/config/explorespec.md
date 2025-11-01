---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Configuration des spécifications d’exploration pour les sources en libre-service (SDK par lots)
description: Ce document présente un aperçu des configurations que vous devez préparer pour utiliser des sources en libre-service (SDK par lots).
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 6%

---

# Configuration des spécifications d’exploration pour les sources en libre-service (SDK par lots)

Les spécifications Explorer définissent les paramètres requis pour explorer et inspecter les objets contenus dans votre source. Les spécifications Explorer définissent également le format de réponse renvoyé lorsque des objets sont explorés et inspectés.

>[!TIP]
>
>Les spécifications de l’Explore sont codées en dur et vous pouvez simplement copier et coller la payload ci-dessous dans votre spécification de connexion.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| Explorer les spécifications | Description | Exemple |
| --- | --- | --- |
| `name` | Définit le nom ou l’identifiant de la spécification d’exploration. | `Resource` |
| `type` | Définit le type de spécification d’exploration. | `Resource` |
| `requestSpec` | Contient les paramètres requis pour explorer les objets dans la connexion. |  |
| `requestSpec.type` | Définit le type de données de la spécification de la requête. | `object` |
| `responseSpec` | Contient les paramètres qui définissent le format du message de réponse renvoyé par rapport à un appel d’exploration. |  |
| `responseSpec.type` | Définit le type de données de la spécification de réponse. | `object` |
| `responseSpec.properties` | Contient des informations relatives au format du message de réponse. |  |
| `responseSpec.properties.format` | Définit le formatage du schéma de réponse. | `object` |
| `responseSpec.properties.format.type` | Définit le type de données des propriétés. | `string` |
| `responseSpec.schema` | Contient des informations relatives au format du schéma de réponse. |  |
| `responseSpec.schema.type` | Définit le type de données du schéma. | `object` |
| `responseSpec.schema.properties` | Contient des informations sur les colonnes, le type et les éléments contenus dans un schéma. |  |
| `responseSpec.schema.properties.columns.items.properties.name` | Affiche le nom du fichier. |  |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Définit le type de données du nom de fichier. | `string` |

{style="table-layout:auto"}

## Étapes suivantes

Une fois vos spécifications d’exploration renseignées, vous pouvez procéder à la création d’une spécification de connexion complète à l’aide de l’API [!DNL Flow Service]. Pour plus d’informations[&#x200B; consultez le guide de l’API &#x200B;](../api/api-overview.md) Sources en libre-service (SDK par lots) .
