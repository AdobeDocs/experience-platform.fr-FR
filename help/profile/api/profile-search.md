---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur de l’API de Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 1%

---


# Recherche de Profil

La recherche par Profil permet de rechercher et d’indexer des champs configurables contenus dans diverses sources de données et de les renvoyer en temps quasi réel.

Ce guide fournit des informations pour vous aider à mieux comprendre la recherche de Profil et inclut des exemples d&#39;appels d&#39;API pour exécuter des actions de base à l&#39;aide de l&#39;API.

## Prise en main

Les points de terminaison API utilisés dans ce guide font partie de l’API Profil client en temps réel. Avant de continuer, veuillez consulter le guide [du développeur de Profil client en temps](getting-started.md)réel.

En particulier, la section [](getting-started.md) Prise en main du guide du développeur de Profils contient des liens vers des rubriques connexes, un guide de lecture des exemples d’appels d’API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API de plateforme d’expérience.

### Obtenir les résultats de recherche

Le point de terminaison de la recherche peut être utilisé pour obtenir les résultats de la recherche en fonction des valeurs du `schema.name` paramètre requis et des autres paramètres de requête facultatifs. Plusieurs paramètres peuvent être utilisés, séparés par des esperluettes (&amp;).

**Format d’API**

```http
GET /search?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `schema.name` | **Obligatoire.** Nom de la classe de schéma contenant le contenu à rechercher, écrit au format de notation par point. Actuellement, seul `schema.name=_xdm.context.segmentdefinition` est pris en charge. |
| `limit` | Nombre de résultats de recherche à renvoyer. La valeur par défaut est 50. |
| `page` | Numéro de page utilisé pour paginer les résultats de la requête recherchée. |
| `s` | requête conforme à la mise en oeuvre par Microsoft de la syntaxe [de recherche de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Si aucun terme de recherche n&#39;est spécifié, tous les enregistrements associés `schema.name` seront renvoyés. Vous trouverez une explication plus détaillée dans la section Paramètres [de](#search-parameters) recherche de ce document. |
| `namespace` | Identifie les données réelles à rechercher dans la classe de schéma spécifiée dans le `schema.name` paramètre. |
| `organization.type` | Détermine le contenu de la réponse. Le format du contenu renvoyé dépend des valeurs utilisées dans `schema.name`. Par exemple, `_xdm.context.segmentdefinition`les valeurs valides sont `hierarchy` ou `hierarchyinfo`. |
| `organization.id` | **Obligatoire si`organization.type`est spécifié.** Donne la hiérarchie de l&#39;organisation spécifiée lorsqu&#39;elle est utilisée avec la hiérarchie `organization.type` de. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau d&#39;objets qui correspondent à vos critères de recherche. Dans cet exemple, étant donné que le `schema.name` paramètre était `_xdm.context.segmentdefinition`défini, une liste de définitions de segment est renvoyée.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### Création de demandes de mise en service

Vous pouvez créer des requêtes de mise en service pour activer la recherche de Profil sur les schémas en exécutant une requête POST sur le point de `/search/provisioning/component/init` terminaison.

**Requête**

>[!CAUTION]
>Cette requête POST ne contient pas de charge utile et ne nécessite donc pas d’en-tête Content-Type. En outre, il n’existe pas d’en-tête Sandbox, car toutes les données sont envoyées dans un sandbox global.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et le message suivant :

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### Gestion des demandes de configuration

Le point de terminaison de configuration peut être utilisé pour configurer les index, indexeurs et connexions de source de données appropriés pour une nouvelle organisation IMS. Deux propriétés sont requises pour gérer les demandes de configuration : `databaseName` et `containerName`.

`databaseName` représente le nom de la base de données de Profil de l&#39;organisation qui sera configurée.

`containerName` représente le nom du conteneur renseigné par un connecteur de données, qui est lu pendant la configuration. Il existe deux valeurs pour `containerName`: une ou les deux peuvent être utilisées dans la requête POST :
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### Créer une demande de configuration

L’appel d’API suivant génère la source de données, l’indexeur et l’index requis en fonction des paramètres fournis dans la charge utile de la demande.

**Format d’API**

```http
POST /search/configure
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) et un message en texte brut.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### Suppression d’une demande de configuration

L’appel d’API suivant supprime les entrées d’index correspondantes et supprime l’indexeur et la source de données en fonction des paramètres fournis dans la charge utile de la demande.

>[!NOTE]
>L&#39;index lui-même ne sera pas supprimé car il s&#39;agit d&#39;une ressource partagée.

**Format d’API**

```http
DELETE /search/configure
```

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 202 (Accepté) et un message en texte brut.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment fonctionne la recherche de Profil client en temps réel. Pour plus d&#39;informations sur le Profil client en temps réel, veuillez lire la présentation [du Profil client en temps](../home.md)réel. Pour plus d’informations sur la segmentation, consultez la présentation [de la](../../segmentation/home.md)segmentation.

## Annexe {#appendix}

### Paramètres de recherche {#search-parameters}

Le tableau suivant liste les détails du fonctionnement du paramètre de recherche lors de l&#39;utilisation de l&#39;API de recherche.

| Requête de recherche | Description |
|------------ | -----------|
| foo | Recherchez n&#39;importe quel mot. Cela renverra des résultats si le mot &quot;foo&quot; se trouve dans l’un des champs recherchés. |
| foo AND bar | Recherche booléenne. Cela retournera des résultats si **** les mots &quot;foo&quot; et &quot;bar&quot; se trouvent dans l’un des champs recherchés. |
| barre d’état OU | Recherche booléenne. Cela retournera des résultats si **** le mot &quot;foo&quot; ou le mot &quot;bar&quot; se trouvent dans l’un des champs disponibles pour la recherche. |
| barre FOI NOT | Recherche booléenne. Cela retournera des résultats si le mot &quot;foo&quot; est trouvé mais que le mot &quot;bar&quot; ne se trouve dans aucun des champs recherchés. |
| name: foo AND bar | Recherche booléenne. Cela retournera des résultats si **les deux** mots &quot;foo&quot; et &quot;bar&quot; se trouvent dans le champ &quot;name&quot;. |
| run* | Recherche de caractères génériques. L’utilisation d’un astérisque (*) correspond à 0 caractère ou plus, ce qui signifie qu’il renvoie des résultats si le contenu de l’un des champs recherchés contient un mot qui début avec &quot;run&quot;. Par exemple, les résultats seront renvoyés si les mots &quot;run&quot;, &quot;running&quot;, &quot;runner&quot; ou &quot;runt&quot; apparaissent. |
| cam ? | Recherche de caractères génériques. Utilisation d’un point d’interrogation (?) ne correspond qu’à un seul caractère, ce qui signifie qu’il renvoie des résultats si le contenu de l’un des champs recherchés est début avec &quot;cam&quot; et une lettre supplémentaire. Par exemple, les résultats seront renvoyés si les mots &quot;camp&quot; ou &quot;cams&quot; apparaissent, mais pas si les mots &quot;caméra&quot; ou &quot;feu de camp&quot; apparaissent. |
| &quot;parapluie bleu&quot; | Recherche d&#39;expression. Cela retournera des résultats si le contenu de l&#39;un des champs recherchés contient l&#39;expression complète &quot;parapluie bleu&quot;. |
| bleu\~ | Une recherche floue. Vous pouvez éventuellement placer un nombre compris entre 0 et 2 après le tilde (~) pour spécifier la distance de modification. Par exemple, &quot;blue\~1&quot; renvoie &quot;blue&quot;, &quot;blues&quot; ou &quot;colle&quot;. La recherche floue ne peut **être appliquée qu** &#39;aux termes, et non aux expressions. Cependant, vous pouvez ajouter des tildes à la fin de chaque mot d’une phrase. Par exemple, &quot;camping\~ à\~ l\~ été\~&quot; correspond à &quot;camping en été&quot;. |
| &quot;aéroport de l&#39;hôtel&quot;\~5 | Recherche de proximité. Ce type de recherche permet de rechercher des termes proches les uns des autres dans un document. Par exemple, l&#39;expression `"hotel airport"~5` trouvera les termes &quot;hôtel&quot; et &quot;aéroport&quot; à moins de 5 mots l&#39;un de l&#39;autre dans un document. |
| `/a[0-9]+b$/` | Recherche d’expressions régulière. Ce type de recherche trouve une correspondance basée sur le contenu entre les barres obliques &quot;/&quot;, comme indiqué dans la classe RegExp. Par exemple, pour rechercher des documents contenant &quot;motel&quot; ou &quot;hotel&quot;, spécifiez `/[mh]otel/`. Les recherches d’expressions régulières sont comparées à des mots simples. |

Pour obtenir une documentation plus détaillée sur la syntaxe de la requête, veuillez lire la documentation [sur la syntaxe de la requête](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene.
