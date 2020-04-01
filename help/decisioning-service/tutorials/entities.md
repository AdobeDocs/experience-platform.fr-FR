---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gestion des entités du service de prise de décision à l’aide d’API
topic: tutorial
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Gestion des objets et des règles de prise de décision à l’aide d’API

Ce fournit un didacticiel pour travailler avec les entités commerciales de Decisioning Service à l’aide des API Adobe Experience Platform.

Le didacticiel comporte deux parties :

- Les API de référentiel générique pour la gestion des objets métier sont introduites dans la [première partie](#managing-repository-entities-using-apis). Ces API sont génériques dans le sens où elles fournissent des fonctionnalités de création, de lecture, de mise à jour, de suppression et de recherche pour **tout** type d’objet métier. Le modèle d’API général est décrit et la relation avec le langage d’application hypertexte (HAL) est expliquée.

- En appliquant les connaissances sur les API du référentiel, la [deuxième partie](#creating-and-managing-offer-decisioning-entities-using-apis) se concentre sur les entités commerciales gérées via les API du référentiel. Les mêmes API étant appliquées, la seule différence entre la gestion de deux entités différentes, telles qu’un , et une règle métier est la charge utile de requête et de réponse, plus les valeurs d’en-tête nécessaires qui indiquent le type d’objet géré.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des services Experience Platform et des conventions d’API. Le référentiel de plateformes est un service utilisé par plusieurs autres services de plateformes pour stocker des objets d’entreprise et divers types de métadonnées. Il offre une méthode sécurisée et flexible pour gérer et  ces objets en vue de les utiliser par plusieurs services d’exécution. Le Service de prise de décision en fait partie. Avant de commencer ce didacticiel, veuillez consulter la documentation relative aux éléments suivants :

- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
- [Service](./../home.md)de prise de décision : Explique les concepts et les composants utilisés pour la prise de décision d’expérience en général et  la prise de décision  par les en particulier. Illustre les stratégies utilisées pour choisir la meilleure option à présenter lors de l’expérience d’un client.
- [ langue (PQL)](../../segmentation/pql/overview.md): PQL est un langage puissant pour écrire   de sur des instances XDM. PQL est utilisé pour définir des règles de décision.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels aux API de plateforme.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Conventions de l’API Repository

Le service de prise de décision est contrôlé par un certain nombre d’objets commerciaux qui sont liés les uns aux autres. Tous les objets métier sont stockés dans le référentiel d’objets métier de la plateforme. Une caractéristique clé de ce référentiel est que les API sont orthogonales par rapport au type d’objet métier. Au lieu d’utiliser une API POST, GET, PUT, PATCH ou DELETE qui indique le type de ressource dans son point de terminaison API, il n’y a que 6 points de terminaison génériques, mais ils acceptent ou renvoient un paramètre qui indique le type de l’objet lorsque cette désambiguïté est nécessaire. Le doit être enregistré dans le référentiel, mais au-delà, le référentiel peut être utilisé pour un ensemble illimité de types d’objets.

Outre les en-têtes répertoriés ci-dessus, les API pour créer, lire, mettre à jour, supprimer et des objets de référentiel ont les conventions suivantes :

- Chemins d’accès des points de fin de toutes les API de référentiel  avec `https://platform.adobe.io/data/core/xcore/`.

Les formats de charge utile d’API sont négociés avec un `Accept` en-tête ou `Content-Type` un en-tête. Les formats de message dans l’ `Accept` en-tête ou `Content-Type` l’en-tête sont indiqués par une valeur `application/vnd.adobe.platform.xcore.{FORMAT}+json` où {FORMAT} dépend de la requête ou du message de réponse de l’API du référentiel spécifique, selon le tableau suivant.

| Variante FORMAT | Description de l&#39;entité de demande ou de réponse |
| --- | --- |
| <br>suivi d’un paramètre `schema={schemaId}` | Le message contient une instance décrite par un JSON et indiquée par le du paramètre de format. L’instance est encapsulée dans une propriété JSON `_instance`. Les autres propriétés de niveau supérieur de la charge utile de réponse spécifient les informations du référentiel disponibles pour toutes les ressources.  Les messages conformes au format HAL ont une `_links` propriété qui contient des références au format HAL. |
| `patch.hal` | Le message contient une charge JSON PATCH en supposant que l’instance à corriger soit compatible HAL. Cela signifie que non seulement les propriétés de l’instance, mais aussi les liens HAL de l’instance peuvent être corrigés. Notez qu’il existe des restrictions quant aux propriétés qui peuvent être mises à jour par le client. |
| `home.hal` | Le message contient une représentation au format JSON d’une ressource de d’accueil pour le référentiel. |
| xdm.receive | Le message contient une réponse au format JSON pour une opération de création, de mise à jour (complète et de correctif) ou de suppression. Les reçus contiennent des données de contrôle indiquant la révision de l’instance sous la forme d’un ETag. |

L’utilisation de chaque variante **de** format dépend de l’API spécifique :

| API | En-tête Content-Type | En-tête Accepter |
| --- | --- | --- |
| Créer une instance <br/>Créer un | `hal`<br/>avec le paramètre  | `xdm.receipt` |
| Mettre à jour le<br/>InstanceUpdate | `hal`<br/>avec le paramètre  | `xdm.receipt` |
| Instance de correctif | `patch.hal` | `xdm.receipt` |
| Supprimer<br/>instanceSupprimer le | S.O. | `xdm.receipt` |
| Lire le<br/>InstanceLu | S.O. | `hal` avec `schema` paramètre |
| <br/>instancesListe  | S.O. | `hal` avec un `schema` paramètre spécial `https://ns.adobe.com/experience/xcore/hal/results` |
| Instances de recherche | S.O. | hal avec un `schema` paramètre spécial `https://ns.adobe.com/experience/xcore/hal/results` |
| Lire la racine du repo | S.O. | `home.hal` |

Pour les API de création, de mise à jour et de lecture des  du, le du paramètre de format a la valeur `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` est le premier paramètre de chemin pour les API d’instance. Toutes les entités commerciales résident dans ce qu&#39;on appelle un . Un  est un mécanisme d&#39;isolement qui permet de séparer les différentes préoccupations. Le premier élément de chemin d’accès pour les API d’instance de référentiel suivant le point de fin général est le `containerId`. L’identifiant est obtenu à partir du  de  accessible à l’appelant. Par exemple, l’API permettant de créer une instance dans un  est `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

Le de l’ accessible est obtenu en appelant le point de terminaison racine du référentiel &quot;/&quot; avec une requête HTTP GET utilisant les en-têtes standard.

## Gestion de l&#39;accès aux  de

Un administrateur peut regrouper des entités, des ressources et des autorisations d’accès similaires dans des  de. Cela réduit la charge de gestion et est pris en charge par l’interface utilisateur [de la Console d’administration d’](https://adminconsole.adobe.com)Adobe. Vous devez être un administrateur de produit pour Adobe Experience Platform et   de votre entreprise pour créer des et leur affecter des utilisateurs.

Il suffit de créer des  de produits qui correspondent à certaines autorisations en une seule étape, puis d’ajouter simplement des utilisateurs à ces  de produits. Les  agissent comme des groupes auxquels des autorisations ont été accordées et chaque utilisateur réel ou technique de ce groupe hérite de ces autorisations.

###  accessible aux utilisateurs et aux intégrations

Lorsque l’administrateur a autorisé l’accès aux  pour les utilisateurs réguliers ou les intégrations, ces s’afficheront dans lefameux &quot;Home&quot; du référentiel. Le  de peut être différent pour différents utilisateurs ou intégrations car il s’agit d’un sous-ensemble de tous les  accessibles à l’appelant. Les  de l&#39; de  de peuvent être filtrées par leur association à l&#39;de produit. Le paramètre de filtre est appelé `product` et peut être répété. Si plusieurs filtres contextuels de produit sont donnés, le   de l’qui a des associations avec l’un desde produit donné est renvoyé. Notez qu’un seul  de peut être associé à plusieurs  de produits.

Le contexte de la  du service de prise de décision de plateforme est actuellement `dma_offers`.

>[!NOTE] Le contexte du de décision de plateforme va bientôt changer `acp`. Le filtrage est facultatif, mais les  ne nécessitent des modifications que `dma_offers` dans une version ultérieure. Pour se préparer à ce changement, les clients doivent utiliser aucun  de ou appliquer les deux  de produit comme filtre.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Réponse**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Notez la `instanceId` liste des éléments de résultats. Il est utilisé comme `containerId` paramètre dans les API pour lire et manipuler les objets métier standard.

Le  est déjà filtré pour les utilisateurs en fonction de leurs privilèges d’accès, mais il peut être filtré par un  de propriété.

## API génériques pour gérer les entités

### Création d’instances

L’API permettant de créer une nouvelle instance dans le référentiel utilise un paramètre `containerId` path et identifie le type de l’instance dans l’ `Content-Type` en-tête avec le paramètre .

Les propriétés de l’instance sont données dans la charge utile encapsulée dans la `_instance` propriété. Les propriétés de l’instance doivent être valides par rapport au  JSON avec l’identifiant de donné.

La `_links` propriété HAL doit être présente mais peut être vide. Cela signifie qu’aucun lien personnalisé n’est défini pour cette instance.

**Requête**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Réponse**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

La réponse contient l’instanceId de l’objet qui vient d’être créé. Cet instanceId est immuable, toujours affecté par le référentiel et globalement unique. La valeur sert d’identificateur physique.

En outre, un URI (Universal Resource Identifier) est renvoyé dans la `@id` propriété de la charge utile de réponse si le possède cette propriété. Chaque instance doit avoir une propriété qui sert d’URI et de clé principale de l’instance. Cet identifiant est utilisé par une autre instance pour créer des relations avec la nouvelle instance, y compris entre différents types. Dans la version actuelle, les URI sont générés par le référentiel et sont contenus dans la `@id` propriété. Les futures versions pourront assouplir cette règle et permettre aux clients de gérer leurs propres valeurs URI et de nommer la propriété qui la contient.

Notez que ces URI ne sont pas des URL et ne permettent pas de récupérer directement la ressource. Pour indiquer cet aspect, l’URI est précédé d’un modèle d’URI qui ne spécifie aucun protocole de récupération. Toutefois, les URI peuvent être utilisés pour rechercher l’instance avec un  de.

La réponse REST comporte un en-tête Emplacement contenant un composant URL qui peut être utilisé pour récupérer l’instance qui vient d’être créée. Ce composant est une référence URI relative et doit être appliqué à l’URI de base du référentiel. L’URI de base est renvoyé dans l’ `Content-Base` en-tête.

La `repo:etag` propriété spécifie la révision de l’instance. Cette valeur peut être utilisée dans les opérations de mise à jour pour assurer la cohérence. L’en-tête HTTP `If-Match` peut être utilisé pour ajouter une condition à un appel de l’API PUT ou PATCH qui garantit qu’aucune autre modification de l’instance n’a pu être écrasée accidentellement. La `repo:etag` valeur est renvoyée avec chaque appel create, read, update, delete et. La valeur est utilisée comme valeur dans l’ ` If-Match` en-tête, par [RFC7232 Section 3.1](https://tools.ietf.org/html/rfc7232#section-3.1).

Les autres propriétés indiquent le compte et la clé d’API utilisés pour créer et modifier l’instance en dernier. Puisque l’instance a été créée par cet appel, les valeurs respectives sont celles de la requête.

### Recherche d’une instance par ID

En utilisant l’URL dans l’en-tête Emplacement renvoyé avec l’appel Créer, une application peut rechercher une instance.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE] Bien que `instanceId` soit donné comme paramètre de chemin, les applications doivent, chaque fois que possible, ne pas construire le chemin elles-mêmes et suivre plutôt les liens vers les instances contenues dans les  de et les opérations de recherche. Voir les sections ‎ 6.4.4 et ‎ 6.4.6 pour plus de détails.

**Réponse**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

Les propriétés JSON de l’instance sont encapsulées dans la `_instance` propriété et les autres propriétés de niveau racine contiennent des métadonnées sur l’instance.

La ressource contient également un tableau d’ID de  JSON. Ce tableau indique au JSON  que cette instance est validée.

Chaque instance contient un lien HAL du type de relation self qui correspond à l&#39;auto-relation enregistrée IANA (comme défini par [RFC5988]).

**Tester les nouvelles révisions d’une instance**

La `eTag` valeur actuelle de l’instance est renvoyée avec la réponse. Elle permet aux clients d’exécuter des opérations conditionnelles sur l’instance, soit pour éviter de récupérer le même état de ressource, soit pour éviter de remplacer les valeurs d’une révision ultérieure sans que le client en ait connaissance.

L’API de recherche permet à un client de spécifier un paramètre `If-None-Match` d’en-tête. Voir la définition de ce paramètre HTTP standard [RFC2616]. La valeur de balise d&#39;entité spécifiée par un client est la valeur reçue avec la dernière réponse, provenant d&#39;un appel d&#39;API de mise à jour, de lecture, de ou de recherche. Notez que la `etag` valeur doit être opaque pour le client et doit être fournie sous forme de chaîne, entourée de guillemets.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

L’API du référentiel répondra avec l’état 304 Non modifié lorsque la dernière révision de l’instance est celle avec l’étiquette donnée.

### Instances de  pour un  - Tri et pagination

Les clients ne pourront pas suivre les instances qu’ils créent et, par conséquent, y accéder par leur instanceId physique. L’utilisation de l’API d’instance de lecture constitue l’exception. Les clients ignorent également les instances créées par d’autres clients.

Un modèle d’accès plus classique consiste à parcourir le jeu de toutes les instances.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Réponse**

La réponse dépend du `{schemaId}` paramètre spécifié. Par exemple, pour &quot;https<span></span>://ns.adobe.com/experience/-management/---id=xcore:--:fa24f9e8fc15c73&quot;, la réponse ressemble à ce qui suit.

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE] Le résultat contient les instances pour la  donnée ou la première page de cette  de. Notez que les instances peuvent être conformes à plusieurs  de et peuvent donc apparaître dans plusieurs  de.

Les ressources de page sont transitoires et sont en lecture seule ; elles ne peuvent pas être mises à jour ou supprimées. Le modèle de pagination offre un accès aléatoire aux sous-ensembles d’un grand sur une longue période sans conserver aucun état par client.

Pour accéder à un d’instance par page de cette manière, il doit être possible de définir un tri stable sur les entrées énumérées par ce d’instance. Notez que &quot;stable&quot; ne signifie pas que les instances apparaîtront dans une page prédéterminée. En fait, lorsqu’un ordre de page est formé en triant les instances en fonction d’une propriété P et qu’un client met à jour cette propriété P, un autre client peut accéder à cette instance sur une autre page tout en faisant une pagination dans le . En d&#39;autres termes, le modèle favorise le retour de résultats plus récents.

Cependant, lorsque l’ordre de tri est basé sur une propriété non modifiable, un ordre de tri &quot;stable&quot; garantit que toutes les instances qui existaient au début de l’opération de pagination seront atteintes (sauf si elles ont été supprimées au moment où leur page est atteinte). Lorsque cet ordre de tri est défini sur une propriété qui augmente de manière monotone, les instances créées après le début de l’opération de pagination sont également atteintes.

Un client peut donner des conseils sur la taille de page qu’il souhaite, mais il appartient entièrement au référentiel de fournir plus ou moins d’instances à la page qu’il renvoie. Pour garantir l’ordre stable, le service doit ajouter ou supprimer des éléments de la page afin que la valeur de la propriété de tri soit différente selon les limites de la page. Ainsi, la page suivante ne contiendra plus certains éléments de la dernière page ou, dans le pire des cas, sera bloquée avec les mêmes éléments sur chaque page.

La pagination est contrôlée par les paramètres suivants :

- **`orderBy`**: Contient un de propriétés trié, séparé par des virgules, par lequel le d’instance est trié. La première propriété est utilisée pour le tri principal, la deuxième pour résoudre les liens dans le tri principal, etc. Lorsqu’une propriété est spécifiée avec une valeur unique par instance, les liens ne sont pas possibles et un saut de page peut survenir après chaque élément. Le nom d’une propriété peut être précédé d’un préfixe `+` indiquant un ordre croissant ou `-` un ordre décroissant par cette propriété. Si le nom de la propriété n’est pas précédé d’un préfixe, le résultat est trié par ordre croissant. Si `orderBy` n’est pas spécifié dans la requête, le référentiel utilise la propriété instanceId physique à la place.
- **`start`**: Les clients utilisent le paramètre  de pour définir la page qu’ils souhaitent récupérer. Le paramètre  du détermine le début de la page souhaitée. La réponse contiendra des instances commençant par celles dont la valeur de `orderBy` propriété est strictement supérieure (pour l’ordre croissant) ou strictement inférieure (pour l’ordre décroissant) à la valeur spécifiée. Lorsque le paramètre  n’est pas spécifié, il utilise par défaut une valeur instanceId qui trie avant le premier identifiant d’instance possible. Par conséquent, cette valeur est omise dans la première page.
- **`limit`**: spécifie un entier positif comme indicateur du nombre maximal d’éléments à renvoyer pour une requête donnée. La taille réelle de la réponse peut être plus petite ou plus grande, car elle est limitée par la nécessité de fournir un fonctionnement fiable du paramètre  de l&#39;

### Filtrage des 

Le filtrage  résultats est possible et se produit indépendamment du mécanisme de pagination.  ignorez simplement les instances dans l’ordre du  ou demandez explicitement d’inclure uniquement les instances qui répondent à une condition donnée. Un client peut demander que la propriété  le  être utilisé comme filtre ou il peut spécifier un d’URI à utiliser comme valeurs de la clé primaire des instances.

- **`property`**: Contient un chemin de nom de propriété suivi d’un opérateur de comparaison suivi d’une valeur. <br/>
Le  d’instances renvoyé contient les instances pour lesquelles le  a la valeur true. Par exemple, en supposant que l’instance possède une propriété de charge utile `status` et que les valeurs possibles sont `draft`, `approved`, `archived` puis `deleted` `property=_instance.status==approved` , le paramètre de  ne renvoie que les instances pour lesquelles l’état est approuvé. <br/>
<br/>
La propriété à comparer à la valeur donnée est identifiée comme un chemin d’accès. Les composants de chemin individuels sont séparés par ".", comme par exemple : `_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

Pour les propriétés qui comportent des valeurs de chaîne, numériques ou de date/heure, les opérateurs autorisés sont les suivants : `==`, `!=`, `<`, `<=`, `>` et `>=`. En outre, pour les propriétés avec une valeur de chaîne, un opérateur `~` peut être utilisé. L’ `~` opérateur correspond à la propriété donnée en fonction d’un   régulier. La valeur de chaîne de la propriété doit correspondre à l’ **intégralité** de l’  pour que les entités soient incluses dans les résultats filtrés. Par exemple, si vous recherchez la chaîne `cars` n’importe où à l’intérieur de la valeur de propriété, le  normal doit être `.*cars.*`. Sans les valeurs de début ou de fin `.*`, seules les entités dont la valeur de propriété commence ou se termine par `cars`, respectivement, correspondraient. Pour l’ `~` opérateur, la comparaison des caractères de lettre n’est pas sensible à la casse. Pour tous les autres opérateurs, la comparaison est sensible à la casse.<br/><br/>
Il n’est pas possible d’utiliser uniquement les propriétés de charge utile d’instance dans les  de  de filtre. Les propriétés de l’enveloppe sont comparées de la même manière, par ex. `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>Le paramètre `property` peut être répété afin que plusieurs conditions de filtre soient appliquées, par exemple pour renvoyer toutes les instances qui ont été modifiées pour la dernière fois après une certaine date et avant une certaine date. Les valeurs de ces   doivent être codées dans l’URL. Si aucun   n’est donné et que le nom de la propriété est simplement répertorié, les éléments qui remplissent les conditions sont ceux qui possèdent une propriété portant le nom donné.<br/>
<br/>

- **`id`**: Il arrive qu’un  doive être filtré par l’URI des instances. Le paramètre `property` peut être utilisé pour filtrer une instance, mais pour obtenir plusieurs instances, un d’URI peut être attribué à la requête. Le `id` paramètre est répété et chaque occurrence spécifie une valeur URI, `id={URI_1}&id={URI_2},…` les valeurs URI doivent être codées dans l’URL.

Les résultats de pagination sont renvoyés sous la forme d’un type MIME spécial `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Réponse**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

La réponse contient le  des éléments de résultat dans les résultats de la propriété JSON en regard de deux propriétés qui indiquent le nombre de résultats sur cette page et le nombre total d’éléments dans le filtré  en commençant par la page qui vient d’être renvoyée.

### Recherche de texte intégral et structuré

Dans les cas où les clients souhaitent fournir des conditions de filtre et des instances de recherche plus complexes par termes contenus dans les propriétés de chaîne, le référentiel  une API de recherche plus puissante  une API de recherche plus puissante.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

En plus des paramètres de pagination et de filtrage des API de , cette API permet aux clients d&#39;ajouter du texte intégral et des paramètres de booléens.

La recherche de texte intégral est contrôlée par les paramètres suivants :

- **`q`**: Contient un de termes non triés et séparés par des espaces, normalisés avant d’être associés aux propriétés de chaîne des instances. Les propriétés de chaîne sont analysées pour les termes et ces termes sont également normalisés. Le de recherche tente de faire correspondre un ou plusieurs des termes spécifiés dans le `q` paramètre. Les caractères +, -, =, &amp;&amp;,||, >, &lt;,!, (,), {, }, [,]^, &quot;, ~, *, ?, :, / ont une signification spéciale pour déterminer les limites des mots dans la chaîne de  du et doivent être précédées d’une barre oblique inverse lorsqu’elles apparaissent dans un jeton qui doit correspondre au caractère. La chaîne de  peut être entourée de guillemets  pour une correspondance exacte de chaîne et pour échapper des caractères spéciaux.
- **`field`**: Si les termes de recherche ne doivent correspondre qu’à un sous-ensemble des propriétés, le paramètre field peut alors indiquer le chemin d’accès à cette propriété. Le paramètre peut être répété pour indiquer plusieurs propriétés devant faire l’objet d’une correspondance.
- **`qop`**: Contient un paramètre de contrôle utilisé pour modifier le comportement de correspondance de la recherche. Lorsque le paramètre est défini sur, puis que tous les termes de recherche doivent correspondre et que le paramètre est absent ou que sa valeur est définie sur, ou alors n’importe quel terme peut compter pour une correspondance.

### Mise à jour et correction d’instances

Pour mettre à jour une instance, un client peut soit remplacer le complet des propriétés à la fois, soit utiliser une requête JSON PATCH pour manipuler les valeurs de propriétés individuelles, y compris les  de.

Dans les deux cas, l’URL de la requête spécifie le chemin d’accès à l’instance physique et dans les deux cas, la réponse sera une charge utile de réception JSON, comme celle renvoyée par l’opération [de création](#create-instances). Un client doit de préférence utiliser l’ `Location` en-tête ou le lien HAL qu’il a reçu d’un appel d’API précédent pour cet objet comme chemin d’accès URL complet pour cette API. Si cela n’est pas possible, le client peut construire l’URL à partir de la `containerId` et de la `instanceId`.

**Request** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Requête** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

La requête PATCH applique les instructions, puis valide l&#39;entité résultante par rapport à la  du et les mêmes règles d&#39;intégrité référentielle et d&#39;entité que la requête PUT.

**Contrôle des modifications de valeur de propriété**

Vous pouvez empêcher la définition des propriétés lors de la création et/ou de la mise à jour, à l’aide des annotations suivantes :

- **`"meta:usereditable"`**: Booléen - Lorsqu’une requête provient d’un agent utilisateur qui identifie l’appelant avec un utilisateur ou un de compte technique, les propriétés annotées avec `"meta:usereditable": false` ne doivent pas être présentes dans la charge utile. S’ils le sont, ils ne doivent pas avoir une valeur différente de celle qui est actuellement définie. Si les valeurs diffèrent, la demande de mise à jour ou de correctif est rejetée avec un état 422 Entité non traitable.
- **`"meta:immutable"`**: Booléen : les propriétés annotées avec `"meta:immutable": true` ne peuvent pas être modifiées une fois définies. Cela s&#39;applique aux demandes émanant d&#39;un utilisateur final, de l&#39;intégration d&#39;un compte technique ou d&#39;un service spécial.

**Tester pour une mise à jour simultanée**

Il existe des conditions dans lesquelles plusieurs clients tentent de mettre à jour une instance simultanément. Le référentiel est exploité sur un cluster de noeuds informatiques sans gestion centralisée des transactions. Pour éviter qu’un client écrit une instance simultanément par une autre, les clients peuvent utiliser une mise à jour conditionnelle ou une demande de correctif. En spécifiant la `etag` chaîne dans l’en-tête `If-Match` , le référentiel s’assure que seule la première requête réussit et que les demandes suivantes d’autres clients utilisant la même `etag` valeur échouent. La `etag` valeur change à chaque modification de l’instance. Les clients doivent récupérer l’instance pour obtenir la dernière `etag` valeur, puis un seul client sur plusieurs tentatives de mise à jour peut réussir avec cette valeur. Les autres clients seront rejetés avec un message 409 Conflict.

### Suppression d’instances

Les instances peuvent être supprimées avec un appel DELETE. Un client doit de préférence utiliser l’ `Location` en-tête ou un lien HAL reçu d’un appel d’API précédent pour qu’il s’agisse du chemin d’accès URL complet. Si cela n’est pas possible, le client peut construire l’URL à partir du `containerId` et du physique `instanceId`.

**Requête**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Réponse**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

Lors de la réception d’une demande de suppression, le référentiel vérifie que toutes les autres instances, de tout, font toujours référence à l’instance à supprimer. Dans un système distribué et hautement disponible, l’intégrité référentielle ne peut pas être vérifiée immédiatement. Lorsque des relations de clé étrangère sont définies, les contrôles sont exécutés de manière asynchrone. Cela entraîne un léger retard dans la réponse au résultat de la demande de suppression. Lorsque ces vérifications sont effectuées, la réponse immédiate inclut l’état 202 Accepté et un lien permettant de vérifier le résultat de l’opération de suppression dans l’ `Location` en-tête. Un client doit alors vérifier ce lien pour connaître le résultat.

Si une instance fait référence à l’instance supprimée, le résultat sera un rejet de l’opération de suppression. Si aucune autre référence de clé étrangère n’est découverte, la suppression est terminée. Si le résultat n&#39;est pas encore décidé, la réponse indiquera que d&#39;ici 202 une autre réponse acceptée avec le même `Location` en-tête et demandera au client de continuer à vérifier. Lorsque le résultat est déterminé, la réponse indique qu’avec un état 200 Ok et la charge de la réponse contient le résultat de la demande de suppression initiale. Notez que la réponse 200 Ok signifie uniquement que le résultat est connu et que le corps de la réponse contient la confirmation ou le rejet de la demande de suppression.

## Création de   de et de leurs sous-composants

Les API décrites dans la section précédente s’appliquent uniformément à tous les types d’objets d’entreprise. La seule différence entre, par exemple, la création d’un  de  et d’un  serait l’ `content-type` en-tête notant la charge JSON de la demande qui est conforme à l’JSON. Par conséquent, les sections suivantes ne devront se concentrer que sur ces  et les relations entre eux.

Lors de l’utilisation des API avec le type de contenu `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`, les propriétés de l’instance sont intégrées dans la `_instance` propriété à côté de laquelle il existe une `_links` propriété. Il s’agira du format général dans lequel toutes les instances sont représentées :

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE] Pour des raisons de concision, dans tous les fragments de code JSON, seules les propriétés de l’instance sont illustrées et uniquement lorsqu’elles sont requises, les propriétés d’enveloppe et la section _links sont affichées.

### Propriétés générales   des

  de est un type d’option de prise de décision et le JSON deshérite des propriétés d’option standard que chaque instance d’option aura.

- **`@id`** - Un identifiant unique pour chaque option qui est la clé principale et utilisée pour référencer l&#39;option d&#39;autres objets. Cette propriété est affectée lorsque l’instance est créée, est immuable et ne peut pas être modifiée.
- **`xdm:name`** - Chaque option porte un nom utilisé à des fins de recherche et d&#39;affichage. Le nom n’est pas immuable et ne peut pas être utilisé pour identifier l’instance de manière unique. Le nom peut être sélectionné librement mais doit être unique dans  instances .

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si le  de  est un  de secours.

Chaque instance de   peut comporter un jeu facultatif de propriétés qui sont propres à cette instance seulement.  différents  de peuvent avoir des clés différentes pour ces propriétés, mais les valeurs doivent être des chaînes. Ces propriétés peuvent être utilisées dans les règles de décision et de segmentation. Ils sont également accessibles pour assembler l&#39;expérience décidée afin de personnaliser davantage les messages.

###  cycle de vie 

Il existe un flux simple état- que toutes les options suivront. Ils  dans un état provisoire et quand ils seront prêts, leur état sera approuvé. Une fois leur date de fin dépassée, ils peuvent être déplacés dans l’état archivé. Dans cet état, ils peuvent être supprimés ou réutilisés en les déplaçant à nouveau dans l&#39;état de rédaction.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Cette propriété est utilisée pour la gestion du cycle de vie de l&#39;instance. La valeur représente un état de flux de travail qui est utilisé pour indiquer si le   est toujours en construction (valeur = brouillon), peut généralement être considéré par le moteur d’exécution (valeur = approuvé) ou s’il ne doit plus être utilisé (valeur = archivé).

Une simple opération PATCH sur l’instance est généralement utilisée pour manipuler une `xdm:status` propriété :

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si le  de  est un  de secours.

### Représentations et placements

  sont des options de décision qui comportent des représentations de contenu. Lorsqu’une décision est prise, l’option est sélectionnée et son identifiant est utilisé pour obtenir le contenu ou les références de contenu pour l’emplacement à fournir. Un   peut avoir plusieurs représentations, mais chacune d’elles doit avoir une référence d’emplacement différente. Ainsi, avec un placement donné, la représentation peut être déterminée sans ambiguïté.
Au cours de l’opération de décision, le placement est déterminé en association avec l’objet  du .  les  qui n’ont pas de représentation avec ce placement comme référence sont automatiquement éliminés de l’des choix.

Avant de pouvoir ajouter des représentations à un   les instances de placement doivent exister. Ces instances sont créées avec l’identifiant`https://ns.adobe.com/experience/offer-management/offer-placement`de  du.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si le  de  est un  de secours.

Une instance **Placement** peut avoir les propriétés suivantes :

- **`xdm:name`** - Contient le nom attribué au placement pour y faire référence dans les interactions humaines et les interfaces utilisateur.
- **`xdm:description`** - Utilisé pour transmettre des intentions lisibles pour la façon dont le contenu de cet emplacement est utilisé dans le  de message global. Lorsque les  de l’ définissent de nouveaux emplacements, ils peuvent ajouter des informations supplémentaires dans cette propriété afin qu’un créateur de contenu puisse créer ou sélectionner le contenu en conséquence. Ces instructions ne sont ni interprétées ni appliquées formellement. Cet établissement sert simplement de lieu de communication des intentions.
- **`xdm:channel`** - URI d&#39;un . Le  indique où le contenu dynamique est destiné à être diffusé. La contrainte  est utilisée pour indiquer non seulement où le  sera utilisé, mais aussi pour déterminer l’éditeur de contenu ou le validateur utilisé pour l’expérience.
- **`xdm:componentType`** - Un identifiant de modèle, i.e. URI, pour le contenu qui peut être affiché à l&#39;emplacement décrit par cet emplacement. Les types de composants sont les suivants : lien image, html ou texte brut. Chaque type de composant peut impliquer un ensemble spécifique de propriétés (un modèle) que l’élément de contenu peut avoir. Le des types de composants peut être étendu. Il existe trois valeurs de type de composant prédéfinies :
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, Contrainte pour les types de supports des composants attendus dans cet emplacement. Il peut exister plusieurs types de supports pour un type de composant, par exemple différents formats d’image.

**Les éléments de représentation** dans un   ont une structure d’objet dans la propriété de tableau `xdm:representations`. Chaque élément peut avoir les propriétés suivantes :

- **`xdm:placement`** - Cette propriété contient la référence à l&#39;instance de placement. La valeur est vérifiée lorsque la représentation est ajoutée au  de . Une instance de placement avec cet URI doit exister et ne doit pas être marquée comme supprimée. En outre, une vérification est effectuée pour s’assurer qu’une instance  de ne comporte pas deux représentations avec la même valeur pour la référence de placement.
- **`xdm:components`** - Les composants de contenu sont les fragments associés à un  de particulier. Ces fragments sont ensuite utilisés pour composer l’expérience de l’utilisateur final. Notez que le service de prise de décision ne constitue pas en lui-même l’expérience complète de l’utilisateur final. Les propriétés suivantes font partie du modèle de chaque composant.
   - **`@type`** - cette propriété identifie le type de composant. Un autre nom pour ce concept est &quot;modèle de fragment de contenu&quot;. Le composant `@type` d’un composant est simplement un URI pour un modèle défini par l’application ou le service qui assemble l’expérience de l’utilisateur final.
   - **`repo:id`** - cette propriété contient un identificateur global unique et inaltérable pour la ressource principale du composant dans le référentiel où la ressource est stockée.
   - **`repo:name`** - Cette propriété contient un nom lisible par l&#39;utilisateur pour la ressource dans le référentiel. Ce nom est défini par l’utilisateur et n’est pas garanti comme unique.
   - **`repo:resolveURL`** - cette propriété contient un localisateur de ressources unique pour lire le fichier dans un référentiel de contenu. Il sera ainsi plus facile d’obtenir le fichier sans que le client comprenne les API à appeler. L’URL renvoie les octets de la ressource principale du fichier.
   - **`dc:format`** - cette propriété provient du Dublin Core Metadata Initiative. Le format peut être utilisé pour déterminer le logiciel, le matériel ou tout autre équipement nécessaire pour afficher ou exploiter la ressource. Il est recommandé de sélectionner une valeur dans un vocabulaire contrôlé (par exemple, le des types de supports Internet définissant les formats de supports informatiques).
   - **`dc:language`** - Cette propriété contient la ou les langues de la ressource. Les langues sont spécifiées dans le code de langue tel que défini dans IETF RFC 3066.

Il existe trois types de composants prédéfinis exprimés dans la `@type` propriété :

- https<span></span>://ns.adobe.com/experience/ -management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/ -management/content-component-text
- https<span></span>://ns.adobe.com/experience/ -management/content-component-html

Selon la valeur de la `@type` propriété, `xdm:components` contiendra des propriétés supplémentaires :

- **`xdm:linkURL`** - Présent lorsque le composant est un lien d’image. Cette propriété contiendra le lien associé à l’image et vers lequel l’utilisateur `user-agent` naviguera lorsque l’utilisateur final interagira avec le contenu du  .
- **`xdm:copyline`** - Utilisé lorsque le composant est un texte. Outre le référencement d’une ressource de texte, par exemple pour le texte de formulaire long  les qui peuvent avoir une mise en forme, une chaîne de texte courte peut être directement stockée dans la propriété xdm:copyline.

Des propriétés supplémentaires peuvent être utilisées par les clients pour définir et évaluer les instructions de gestion du contexte. Par exemple, le client de la bibliothèque d’interface utilisateur   ajoute les propriétés facultatives suivantes pour gérer l’affichage plus facilement :

- Dans chaque élément du `xdm:components` tableau, le client de l’interface utilisateur de la  de bibliothèque  ajoute les propriétés suivantes. Ces propriétés ne doivent pas être supprimées ou manipulées sans comprendre l’impact sur l’interface utilisateur :
   - **`offerui:previewThumbnail`** - Il s’agit d’une propriété facultative que l’interface utilisateur de la  bibliothèque de  utilise pour afficher un rendu du fichier. Ce rendu n’est pas le même que la ressource elle-même. Par exemple, le contenu peut être au format HTML et le rendu est une image bitmap montrant uniquement une approximation de ce format. Ce rendu (de qualité inférieure) s’affiche dans le bloc de représentation   du.

Un exemple d’opération PATCH sur une instance de   montre comment manipuler les représentations :

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si le  de  est un  de secours.

L’opération PATCH peut échouer lorsqu’il n’existe pas `xdm:representations` encore de propriété. Dans ce cas, l&#39;opération d&#39;ajout ci-dessus peut être précédée d&#39;une autre opération d&#39;ajout qui crée le `xdm:representations` tableau ou l&#39;opération d&#39;ajout unique définit directement le tableau.
Les  de et les propriétés décrites sont utilisées pour tous les  types de  de, lesde personnalisation ainsi que les de de secours. Les deux sections suivantes sur les contraintes et les règles de décision pour expliquer les aspects de la personnalisation  les .

## Définition  contraintes 

### Contraintes de calendrier

En général, les options de décision peuvent donner une  de et une date et une heure de fin qui servent de contrainte de calendrier. Les propriétés sont incorporées dans la propriété `xdm:selectionConstraint`:

- **`xdm:startDate`** - Cette propriété indique la date et l&#39;heure de  du. La valeur est une chaîne formatée selon les règles RFC 3339, c’est-à-dire comme l’horodatage suivant : &quot;2019-06-13T11:21:23.356Z&quot;.
Les options de décision qui n&#39;ont pas atteint leur date et leur heure de  ne sont pas encore considérées comme admissibles dans la décision.
- **`xdm:endDate`** - Cette propriété indique la date et l&#39;heure de fin. La valeur est une chaîne formatée selon les règles RFC 3339, c’est-à-dire comme l’horodatage suivant : &quot;2019-07-13T11:00:00.000Z&quot;Les options de décision qui ont dépassé leur date et heure de fin ne sont plus considérées comme admissibles dans le processus de décision.

Vous pouvez modifier une contrainte de calendrier à l’aide de l’appel PATCH suivant :

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les abandons  les  n&#39;ont aucune contrainte.

### Contraintes de plafonnement

Une contrainte de plafonnement est un composant d’une option de décision qui définit les paramètres de plafonnement. Le plafonnement est le processus qui consiste à limiter le nombre de fois qu’une option peut être proposée pour un individuel ainsi que pour tous les  de. Les propriétés contiennent une valeur entière qui doit être supérieure ou égale à 1. Les propriétés sont imbriquées dans une propriété `xdm:cappingConstraint`:

- **`xdm:globalCap`** - Un plafond global est une contrainte sur le nombre de fois qu&#39;un   peut être proposé dans sa totalité.
- **`xdm:profileCap`** - Un plafond de  est une contrainte sur le nombre de fois qu&#39;un  peut être proposé à un certain.

La définition ou la modification de la contrainte de plafonnement sur une personnalisation   de peut être effectuée avec l’appel PATCH suivant :

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les abandons  les  n&#39;ont aucune contrainte.

Pour supprimer les valeurs de recouvrement, l’opération &quot;add&quot; est remplacée par l’opération &quot;remove&quot;. Notez que les valeurs de recouvrement existent individuellement et peuvent être définies ou supprimées individuellement.

### Contraintes d’éligibilité

  peut être sélectionné sous condition dans le processus de décision. Lorsqu’une personnalisation   a une référence à un , la condition de la règle doit être vraie pour que l’objet de de soit pris en compte pour un donné. Les  sont créées et gérées indépendamment des options de décision et la même règle peut être référencée à partir de plusieurs personnalisations .

La référence à la règle est incorporée dans la propriété `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** - Cette propriété contient une référence à un . La valeur est la valeur `@id` d’une instance de https://ns.adobe.com/experience/offer-management/eligibility-rule.

Vous pouvez également ajouter et supprimer une règle à l’aide d’une opération PATCH :

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les abandons  les  n&#39;ont aucune contrainte.

Notez que le  est incorporé dans la `xdm:selectionConstraint` propriété avec les contraintes de calendrier. Les opérations PATCH ne doivent pas tenter de supprimer la totalité de la `SelectionConstraint` propriété.

## Définition de la priorité d’un  

Les options de décision admissibles seront classées afin de déterminer la meilleure option pour le  donné. Pour prendre en charge le classement et fournir une valeur par défaut au cas où le classement ne serait pas déterminé par un autre mécanisme, une priorité de base peut être définie pour chaque personnalisation  .
La priorité de base est incorporée dans la propriété `xdm:rank`:

- **`xdm:priority`** - Cette propriété représente l&#39;ordre par défaut dans lequel un   est sélectionné par rapport à un autre, au cas où il n&#39;y aurait pas d&#39;ordre de classement spécifique de l&#39; connu. Si, après avoir comparé la valeur de priorité, deux ou plusieurs personnalisations  les sont toujours liés, on choisit au hasard et on les utilise dans la . La valeur de cette propriété doit être un entier supérieur ou égal à 0.

Vous pouvez ajuster la priorité de base avec l’appel PATCH suivant :

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les de secours   ne possèdent pas de propriétés de classement.

## Gestion des règles de décision

Les  les conditions qui sont évaluées pour déterminer si une option de décision donnée est admissible pour un  donné. L’association d’une règle à une ou plusieurs options de décision définit implicitement que pour cette option, la règle doit être évaluée sur true pour que l’option soit prise en compte pour cet utilisateur. La règle peut contenir des tests sur des attributs , évaluer  impliquant des d’expérience pour ce et peut inclure des données contextuelles transmises à la demande de décision. Par exemple, une condition peut être décrite comme suit :

> &quot;Inclure les personnes qui ont un statut d&#39;élite et qui ont volé trois fois sur un vol au cours des six derniers mois et qui ont le numéro de vol du vol actuel&quot;.

Les instances sont créées à l’aide de l’identifiant de  duhttps://ns.adobe.com/experience/offer-management/eligibility-rule. La `_instance` propriété de l’appel de création ou de mise à jour se présente comme suit :

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

La valeur de la propriété de condition de la règle contient un   PQL. Les données contextuelles sont référencées via le chemin d’accès spécial  @{schemaID}.

Les règles s’alignent naturellement sur les segments de la plateforme d’expérience et, souvent, une règle réutilise simplement l’intention d’un segment en testant la `segmentMembership` propriété d’un. La `segmentMembership` propriété contient les résultats des conditions de segments qui ont déjà été évaluées. Cela permet à une organisation de définir une fois son  spécifique à un domaine, de le nommer et d’évaluer les conditions une fois.

## Gestion des collections  

### Création de balises et balisage  

  de peut être organisé en collections où chaque collection définit la condition de filtre à appliquer.  de filtre actuellement  d’une collection peut avoir l’un des deux formulaires suivants :

1. Le `@id` paramètre du   doit correspondre à un dans un d’identifiants pour que le de soit dans la collection. Ce filtre est simplement un  des URI des  de la collection.
2. Un   peut avoir un de références de balise et le filtre de la collection se compose d’unnombre de balises. Le   se trouve dans la collection lorsque :\
   a. l’une des balises du filtre correspond à l’une des balises du  \
   b. toutes les balises du filtre correspondent à l’une des balises   du

Les balises sont des instances simples auxquelles  instances  peuvent être liées. Ce sont des instances par elles-mêmes avec un nom pour les afficher. Le nom doit être unique pour toutes les instances afin de faciliter leur affichage dans l’interface utilisateur.

Les objets de balise permettent d’établir une classification parmi les options de décision ( ). Une balise peut être liée par de nombreux  de  et un  peut avoir de nombreuses références de balise. Un  de  est établi en faisant référence à tous lesqui sont liés à un ensemble donné d’instances de balise.

Les instances de balise sont créées à l’aide de l’identifiant de  du :https://ns.adobe.com/experience/offer-management/tag. La `_instance` propriété de l’appel de création ou de mise à jour se présente comme suit :

```json
{
  "xdm:name": "credit card"
} 
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/tag`.


Une instance de  de peut être créée avec le de références de balise telles que :

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Une autre solution consiste à appliquer un correctif à un   pour modifier son de balises :

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

Pour les deux cas, voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`.

Notez que la `xdm:tags` propriété doit déjà exister pour que l’opération d’ajout réussisse. Il n’existe aucune balise dans une instance. L’opération PATCH peut d’abord ajouter la propriété array, puis ajouter une référence de balise à ce tableau.

### Définir des  de pour  collections de 

Les instances de filtre sont créées à l’aide de l’identifiant  du https://ns.adobe.com/experience/offer-management/offer-filter. La `_instance` propriété de l’appel de création ou de mise à jour peut se présenter comme suit :

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - Cette propriété indique si le filtre est configuré à l&#39;aide de balises ou fait directement référence à   par leurs identifiants. Lorsque le filtre est configuré pour utiliser des balises, le type de filtre peut indiquer si toutes les balises doivent correspondre aux balises d’un   particulier ou si l’une des balises données est suffisante pour que le  soit admissible au filtre. Les valeurs valides de cette propriété enum sont les suivantes :
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - Une propriété contient un tableau d&#39;URI qui sont des références à des instances de  ou de balise, selon la valeur de `xdm:filterType`. .

L’appel suivant illustre l’aspect de la `_instance` propriété de l’appel de création ou de mise à jour au cas où  serait directement référencé :

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Gestion   des

Un     est utilisé pour contrôler le processus de prise de décision. Il spécifie le filtre   appliqué au stock total pour réduire le  par rubrique/, l’emplacement pour réduire le stock à l’de l’espace réservé et une option de secours si les contraintes combinées disqualifient toutes les options de personnalisation disponibles (deproduits).

Les instances  de  sont créées avec l’identificateur`https://ns.adobe.com/experience/offer-management/offer-activity`. La `_instance` propriété de l’appel de création ou de mise à jour se présente comme suit :

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - Cette propriété obligatoire contient   nom du. Le nom s’affiche dans différentes interfaces utilisateur.
- **`xdm:status`** - Cette propriété est utilisée pour la gestion du cycle de vie de l&#39;instance. La valeur représente un état de flux de travail qui est utilisé pour indiquer si le   est toujours en construction (valeur = brouillon), peut généralement être considéré par le moteur d’exécution (valeur = direct) ou s’il ne doit plus être utilisé (valeur = archivé).
- **`xdm:placement`** - Une propriété obligatoire contenant une référence à un emplacement   qui est appliquée à l&#39;inventaire lorsqu&#39;une décision est prise dans le contexte de ce . La valeur est l’URI (`@id`) de l’emplacement  du  utilisé.
- **`xdm:filter`** - Une propriété obligatoire contenant une référence à un filtre  de  qui est appliquée à l&#39;inventaire lorsqu&#39;une décision est prise dans le cadre de ce  de. La valeur est l’URI (`@id`) du filtre   utilisé.
- **`xdm:fallback`** - Une propriété obligatoire contenant une référence à un de secours  . Un de  de secours est utilisé lors de la prise de décision pour ce  de de  de personnalisation. La valeur est l’URI (`@id`) d’une instance de de secours .

### Gestion des  de secours 

Avant de pouvoir créer  instances  de, il doit exister un de secours qui permette de positionner le. Les instances de de secours  sont créées avec l’identifiant`https://ns.adobe.com/experience/offer-management/fallback-offer`de . La `_instance` propriété de l’appel de création ou de mise à jour contient les mêmes propriétés générales qu’un de personnalisation, mais elle ne peut pas avoir d’autres contraintes.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour connaître la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/fallback-offer`.

