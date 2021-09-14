---
title: Relations dans l’API Reactor
description: Découvrez comment les relations de ressources sont établies dans l’API Reactor, y compris les exigences en matière de relation pour chaque ressource.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: ht
source-wordcount: '798'
ht-degree: 100%

---

# Relations dans l’API Reactor

Les ressources de l’API Reactor sont souvent associées les unes aux autres. Ce document présente la manière dont les relations de ressources sont établies dans l’API et les exigences en matière de relation pour chaque type de ressource.

Selon le type de ressource dont il est question, certaines relations s’avèrent obligatoires. Une relation obligatoire implique que la ressource parent ne peut pas exister sans la relation. Toutes les autres relations sont facultatives.

Qu’elles soient obligatoires ou facultatives, les relations sont automatiquement établies par le système lors de la création de ressources pertinentes ou doivent être créées manuellement. En cas de création de relations manuelle, deux méthodes sont possibles, lesquelles dépendent de la ressource en question :

* [Création par payload](#payload)
* [Création par URL](#url) (pour les bibliothèques uniquement)

Reportez-vous à la section sur les [exigences en matière de relation](#requirements) pour obtenir la liste des relations compatibles pour chaque type de ressource ainsi que les méthodes nécessaires à l’établissement de ces relations, le cas échéant.

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
| `{PROPERTY_ID}` | Identifiant de la propriété à laquelle appartient la ressource. |
| `{RESOURCE_TYPE}` | Type de ressource à créer. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante crée un `rule_component`, établissant des relations avec les `rules` et une `extension`.

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
| `relationships` | Objet qui doit être fourni lors de la création de relations par payload. Chaque clé de cet objet représente un type de relation spécifique. Dans l’exemple ci-dessus, les relations entre `extension` et `rules` sont établies. Elles sont spécifiques à `rule_components`. Pour plus d’informations sur les types de relation compatibles pour différentes ressources, consultez la section sur les [exigences en matière de relation par ressource](#relationship-requirements-by-resource). |
| `data` | Chaque type de relation fourni sous l’objet `relationship` doit contenir une propriété `data`, qui fait référence aux propriétés `id` et `type` de la ressource avec laquelle une relation est établie. Vous pouvez créer une relation avec plusieurs ressources du même type en formatant la propriété `data` en tant que tableau d’objets, où chaque objet contient les propriétés `id` et `type` d’une ressource applicable. |
| `id` | Identifiant unique d’une ressource. Chaque `id` doit être accompagné d’une propriété `type` sœur, indiquant le type de ressource en question. |
| `type` | Type de ressource tel que référencé par un champ `id` frère. Les valeurs acceptées incluent `data_elements`, `rules`, `extensions` et `environments`. |

{style=&quot;table-layout:auto&quot;}

## Création d’une relation par URL {#url}

Contrairement à d’autres ressources, les bibliothèques établissent des relations par le biais de leurs propres points d’entrée `/relationship` dédiés. Par exemple :

* [Ajout d’extensions, d’éléments de données et de règles à une bibliothèque](../endpoints/libraries.md#add-resources)
* [Affectation d’une bibliothèque à un environnement](../endpoints/libraries.md#environment)

**Format d’API**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{PROPERTY_ID}` | Identifiant de la propriété à laquelle appartient la bibliothèque. |
| `{LIBRARY_ID}` | Identifiant de la bibliothèque pour laquelle vous souhaitez créer une relation. |
| `{RESOURCE_TYPE}` | Type de ressource ciblé par la relation. Les exemples de valeurs comprennent `environment`, `data_elements`, `extensions` et `rules`. |

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
| `id` | Identifiant unique d’une ressource. Chaque `id` doit être accompagné d’une propriété `type` sœur, indiquant le type de ressource en question. |
| `type` | Type de ressource tel que référencé par un champ `id` frère. Les valeurs acceptées incluent `data_elements`, `rules`, `extensions` et `environments`. |

{style=&quot;table-layout:auto&quot;}

## Exigences de relation par ressource {#requirements}

Les tableaux suivants décrivent les relations disponibles pour chaque type de ressource, que ces relations soient nécessaires ou pas, et la méthode acceptée pour créer manuellement la relation, le cas échéant.

>[!NOTE]
>
>Si une relation n’est pas répertoriée comme étant créée par une payload ou une URL, elle est automatiquement attribuée par le système.

### Événements d’audit

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Versions

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Rappels

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Sociétés

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Éléments de données

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Environnements

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Extensions

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Hôtes

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Bibliothèques

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Notes

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Propriétés

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Composants de   règle

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Règles

| Relation | Obligatoire | Création par payload | Création par URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |
