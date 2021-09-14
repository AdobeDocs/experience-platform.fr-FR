---
title: Recherche de ressources dans l’API Reactor
description: Découvrez comment rechercher des ressources dans l’API Reactor.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: ht
source-wordcount: '260'
ht-degree: 100%

---

# Recherche de ressources dans l’API Reactor

Le point d’entrée `/search` de l’API Reactor vous permet de créer des requêtes structurées sur des ressources stockées. Ce document fournit des exemples de différentes requêtes de recherche pour des cas d’utilisation courants.

>[!NOTE]
>
>Avant de lire ce guide, reportez-vous au [guide des points d’entrée de recherche](../endpoints/search.md) pour plus d’informations sur la syntaxe de requête acceptée et d’autres instructions d’utilisation.

## Stratégies de requête de base

Les exemples suivants présentent quelques concepts de base pour l’utilisation de la fonctionnalité de recherche de l’API.

### Recherche dans plusieurs champs

Une recherche peut être effectuée sur plusieurs champs à l’aide de caractères génériques dans le nom du champ. Par exemple, pour effectuer une recherche dans plusieurs champs d’attribut, utilisez `attributes.*` comme nom de champ.

```json
{
  "data" : {
    "query": {
      "attributes.*": {
        "value": "evar7"
      }
    }
  }
}
```

>[!IMPORTANT]
>
>Normalement, les valeurs de recherche doivent correspondre au type de données recherchées. Par exemple, une valeur de requête de `evar7` sur un champ entier échouerait. Lors de la recherche sur plusieurs champs, l’exigence du type de requête fait preuve de tolérance afin d’éviter les erreurs, mais elle peut produire des résultats indésirables.

### Étendue des requêtes à des types de ressources spécifiques

Vous pouvez étendre une recherche à un type de ressource spécifique en fournissant `resource_types` dans la requête. Par exemple, pour effectuer une recherche dans `data_elements` et `rule_components` :

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

### Tri des réponses

La propriété `sort` peut être utilisée pour trier les réponses. Par exemple, pour trier par `created_at` en commençant par la plus récente :

```json
{
  "data" : {
    "from": 0,
    "size": 25,
    "query": {
      "attributes.display_name": {
        "value": "Performance"
      }
    },
    "sort": [
      {
        "attributes.created_at": "desc"
      }
    ],
    "resource_types": [
      "data_elements",
      "rule_components"
    ]
  }
}
```

## Exemples de recherche courants

L’exemple suivant illustre d’autres modèles de recherche courants.

### Toute ressource portant un nom spécifique

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.name": {
              "value": "Adobe"
            }
          }
        }
      }'
```

### Toute ressource référençant « evar7 »

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.*": {
              "value": "evar7"
            }
          }
        }
      }'
```

### Éléments de données d’un type de délégué « code personnalisé »

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.delegate_descriptor_id": {
              "value": "custom-code"
            }
          },
          "resource_types": ["data_elements"]
        }
      }'
```

### Composants de règle référençant un élément de données spécifique

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.settings": {
              "value": "myDataElement8"
            }
          },
          "resource_types": ["rule_components"]
        }
      }'
```

### Règles dans une propriété spécifique

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "relationships.property.data.id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          },
          "resource_types": ["rules"]
        }
      }'
```

### Recherche d’une ressource par identifiant

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "id": {
              "value": "PR3cab070a9eb3423894e4a3038ef0e7b7"
            }
          }
        }
      }'
```

### Exécution d’une recherche à l’aide d’une logique de terme « OR »

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data" : {
          "query": {
            "attributes.display_name": {
              "value": "My Rule Holiday Sale",
              "value_operator: "OR"
            }
          }
        }
      }'
```
