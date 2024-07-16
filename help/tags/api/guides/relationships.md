---
title: Relations dans l’API Reactor
description: Découvrez comment les relations de ressources sont établies dans l’API Reactor, y compris les exigences de relation pour chaque ressource.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 99%

---

# Relations dans l’API Reactor

Les ressources de l’API Reactor sont souvent liées. Ce document présente la manière dont les relations entre les ressources sont établies dans l’API et les exigences en matière de relation de chaque type de ressource.

Selon le type de ressource en question, certaines relations sont nécessaires. Une relation requise implique que la ressource parent ne peut pas exister sans la relation. Toutes les autres relations sont facultatives.

Qu’elles soient obligatoires ou facultatives, les relations sont soit automatiquement établies par le système lors de la création des ressources appropriées, soit elles doivent être créées manuellement. Dans le cas de la création manuelle de relations, il existe deux méthodes possibles en fonction de la ressource en question :

* [Créer par payload](#payload)
* [Créer par URL](#url) (pour les bibliothèques uniquement)

Reportez-vous à la section [Exigences de relation](#requirements) pour obtenir la liste des relations compatibles pour chaque type de ressource, ainsi que les méthodes nécessaires pour établir ces relations, le cas échéant.

## Création d’une relation par payload {#payload}

Certaines relations doivent être établies manuellement lors de la création initiale d’une ressource. Pour ce faire, vous devez fournir un objet `relationship` dans le payload de la requête lorsque vous créez la ressource parent pour la première fois. Voici quelques exemples de ces relations :

* [Création d’un élément de données](../endpoints/data-elements.md#create) avec les extensions requises
* [Création d’un environnement](../endpoints/environments.md#create) avec la relation d’hôte requise

**Format d’API**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | L’identifiant de la propriété à laquelle appartient la ressource. |
| `{RESOURCE_TYPE}` | Le type de ressource à créer. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée un nouveau `rule_component`, établissant des relations avec les `rules` et une `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `relationships` | Un objet qui doit être fourni lors de la création de relations par payload. Chaque clé de cet objet représente un type de relation spécifique. Dans l’exemple ci-dessus, les relations `extension` et `rules` sont établies, qui sont spécifiques à `rule_components`. Pour plus d’informations sur les types de relation compatibles pour différentes ressources, consultez la section sur les [exigences en matière de relation par ressource](#relationship-requirements-by-resource). |
| `data` | Chaque type de relation fourni sous l’objet `relationship` doit contenir une propriété `data` qui fait référence aux propriétés `id` et `type` de la ressource avec laquelle une relation est établie. Vous pouvez créer une relation avec plusieurs ressources du même type en formatant la propriété `data` en tant que tableau d’objets, chaque objet contenant les éléments `id` et `type` d’une ressource applicable. |
| `id` | L’identifiant unique d’une ressource. Chaque `id` doit être accompagné d’une propriété `type` parente, indiquant le type de ressource en question. |
| `type` | Le type de ressource tel que référencé par un champ `id` parent. Les exemples de valeurs comprennent `data_elements`, `rules`, `extensions` et `environments`. |

{style="table-layout:auto"}

## Création d’une relation par URL {#url}

Contrairement aux autres ressources, les bibliothèques établissent des relations par le biais de leurs propres points d’entrée `/relationship` dédiés. Par exemple :

* [Ajout d’extensions, d’éléments de données et de règles à une bibliothèque](../endpoints/libraries.md#add-resources)
* [Affectation d’une bibliothèque à un environnement](../endpoints/libraries.md#environment)

**Format d’API**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | L’ID de la propriété à laquelle appartient la bibliothèque. |
| `{LIBRARY_ID}` | L’identifiant de la bibliothèque pour laquelle vous souhaitez créer une relation. |
| `{RESOURCE_TYPE}` | Type de ressource que la relation cible. Les exemples de valeurs comprennent `environment`, `data_elements`, `extensions` et `rules`. |

**Requête**

La requête suivante utilise le point d’entrée `/relationships/environment` d’une bibliothèque pour créer une relation avec un environnement.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| Propriété | Description |
| --- | --- |
| `data` | Objet faisant référence à `id` et `type` de la ressource cible pour la relation. Si vous créez une relation avec plusieurs ressources du même type (telles que `extensions` et `rules`), la propriété `data` doit être formatée sous la forme d’un tableau d’objets, chaque objet contenant les éléments `id` et `type` d’une ressource applicable. |
| `id` | L’identifiant unique d’une ressource. Chaque `id` doit être accompagné d’une propriété `type` parente, indiquant le type de ressource en question. |
| `type` | Le type de ressource tel que référencé par un champ `id` parent. Les exemples de valeurs comprennent `data_elements`, `rules`, `extensions` et `environments`. |

{style="table-layout:auto"}

## Exigences de relation par ressource {#requirements}

Les tableaux suivants décrivent les relations disponibles pour chaque type de ressource, si ces relations sont nécessaires ou non, et la méthode acceptée pour créer manuellement la relation, le cas échéant.

>[!NOTE]
>
>Si une relation n’est pas répertoriée comme étant créée par un payload ou une URL, elle est automatiquement attribuée par le système.

### Événements d’audit

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | |
| `entity` | ✓ | | |

{style="table-layout:auto"}

### Versions

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `data_elements` | | | |
| `extensions` | | | |
| `rules` | | | |
| `environment` | ✓ | | |
| `library` | ✓ | | |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Rappels

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Sociétés

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `properties` | | | |

{style="table-layout:auto"}

### Éléments de données

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ | | |
| `notes` | | | |
| `property` | ✓ | | |
| `origin` | ✓ | | |
| `extension` | ✓ | ✓ | |
| `updated_with_extension` | ✓ | | |
| `updated_with_extension_package` | ✓ | | |

{style="table-layout:auto"}

### Environnements

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `library` | | | |
| `builds` | | | |
| `host` | ✓ | ✓ | |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Extensions

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ | | |
| `notes` | | | |
| `property` | ✓ | | |
| `origin` | ✓ | | |
| `extension_package` | ✓ | ✓ | |
| `updated_with_extension_package` | ✓ | | |

{style="table-layout:auto"}

### Hôtes

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Bibliothèques

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `builds` | | | |
| `environment` | | | ✓ |
| `data_elements` | | | ✓ |
| `extensions` | | | ✓ |
| `rules` | | | ✓ |
| `notes` | | | |
| `upstream_library` | ✓ | | |
| `property` | ✓ | | |
| `last_build` | | | |

{style="table-layout:auto"}

### Notes

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ | | |

{style="table-layout:auto"}

### Propriétés

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ | | |
| `callbacks` | | | |
| `environments` | | | |
| `libraries` | | | |
| `data_elements` | | | |
| `extensions` | | | |
| `extensions` | | | |

{style="table-layout:auto"}

### Composants de règle

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ | | |
| `updated_with_extension` | ✓ | | |
| `extension` | ✓ | ✓ | |
| `notes` | | | |
| `origin` | ✓ | | |
| `property` | ✓ | | |
| `rules` | ✓ | ✓ | |
| `revisions` | ✓ | | |

{style="table-layout:auto"}

### Règles

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ | | |
| `notes` | | | |
| `property` | ✓ | | |
| `origin` | ✓ | | |
| `rule_components` | | | |

### Secrets

| Relation | Obligatoire | Créer par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | ✓ |
| `environment` | ✓ | ✓ | |

