---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gestion des entités du service de prise de décision à l’aide d’API
topic: tutorial
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '7249'
ht-degree: 0%

---


# Gestion des objets et des règles de prise de décision à l’aide d’API

Ce document fournit un didacticiel pour travailler avec les entités commerciales de Decisioning Service à l’aide des API Adobe Experience Platform.

Le didacticiel comporte deux parties :

- Les API de référentiel génériques pour la gestion des objets métier sont introduites dans la [première partie](#managing-repository-entities-using-apis). Ces API sont génériques en ce sens qu&#39;elles offrent des fonctionnalités de création, de lecture, de mise à jour, de suppression et de recherche pour **tout** type d&#39;objet métier. Le modèle d’API général est décrit et la relation avec le langage d’application Hypertext (HAL) est expliquée.

- En appliquant les connaissances sur les API du référentiel, la [deuxième partie](#creating-and-managing-offer-decisioning-entities-using-apis) se concentre sur les entités commerciales qui sont gérées via les API du référentiel. Les mêmes API étant appliquées, la seule différence entre la gestion de deux entités différentes, telles qu’une activité et une règle métier, réside dans la charge utile de requête et de réponse, ainsi que dans les valeurs d’en-tête nécessaires pour indiquer le type d’objet géré.

## Prise en main

Ce didacticiel nécessite une bonne compréhension des services Experience Platform et des conventions d’API. Le référentiel de plateformes est un service utilisé par plusieurs autres services de plateformes pour stocker des objets métier et divers types de métadonnées. Il offre un moyen sécurisé et flexible de gérer et de requête ces objets pour plusieurs services d’exécution. Le Service de prise de décision en fait partie. Avant de commencer ce didacticiel, consultez la documentation relative aux éléments suivants :

- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
- [Service](./../home.md)de prise de décision : Explique les concepts et les composants utilisés pour la prise de décision d’expérience en général et la prise de décision d’Offre en particulier. Illustre les stratégies utilisées pour choisir la meilleure option à présenter lors de l’expérience d’un client.
- [Langage de Requête de Profil (PQL)](../../segmentation/pql/overview.md): PQL est un langage puissant pour écrire des expressions sur des instances XDM. PQL est utilisé pour définir des règles de décision.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API de plate-forme.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Conventions de l’API Repository

Le service de prise de décision est contrôlé par un certain nombre d’objets métier qui sont liés les uns aux autres. Tous les objets métier sont stockés dans le référentiel d’objets métier de la plate-forme. L&#39;une des principales fonctionnalités de ce référentiel est que les API sont orthogonales par rapport au type d&#39;objet métier. Au lieu d&#39;utiliser une API POST, GET, PUT, PATCH ou DELETE qui indique le type de ressource dans son point de terminaison API, il n&#39;y a que 6 points de terminaison génériques, mais ils acceptent ou retournent un paramètre qui indique le type de l&#39;objet lorsque cette désambiguïfication est nécessaire. Le schéma doit être enregistré dans le référentiel, mais au-delà, le référentiel est utilisable pour un ensemble ouvert de types d&#39;objet.

Outre les en-têtes répertoriés ci-dessus, les API permettant de créer, lire, mettre à jour, supprimer et requête des objets de référentiel ont les conventions suivantes :

- Chemins d’accès aux points de terminaison pour tous les API de référentiel avec `https://platform.adobe.io/data/core/xcore/`.

Les formats de charge utile d’API sont négociés avec un `Accept` en-tête ou `Content-Type` un en-tête. Les formats de message dans l&#39; `Accept` en-tête ou l&#39; `Content-Type` en-tête sont indiqués par une valeur `application/vnd.adobe.platform.xcore.{FORMAT}+json` où {FORMAT} dépend de la requête ou du message de réponse de l&#39;API du référentiel spécifique, selon le tableau suivant.

| FORMAT, variante | Description de l&#39;entité de demande ou de réponse |
| --- | --- |
| <br>suivi de moitié par un paramètre `schema={schemaId}` | Le message contient une instance décrite par un Schéma JSON qui est indiquée par le schéma de paramètres de format. L’instance est encapsulée dans une propriété JSON `_instance`. Les autres propriétés de niveau supérieur de la charge utile de réponse spécifient les informations de référentiel disponibles pour toutes les ressources.  Les messages conformes au format HAL ont une `_links` propriété qui contient des références au format HAL. |
| `patch.hal` | Le message contient une charge utile JSON PATCH en supposant que l’instance à corriger soit compatible HAL. Cela signifie que non seulement les propriétés d’instance de l’instance, mais aussi les liens HAL de l’instance peuvent être corrigés. Notez qu’il existe des restrictions quant aux propriétés qui peuvent être mises à jour par le client. |
| `home.hal` | Le message contient une représentation au format JSON d’une ressource de document d’accueil pour le référentiel. |
| xdm.receipt | Le message contient une réponse au format JSON pour une opération de création, de mise à jour (complète et de mise à jour) ou de suppression. Les reçus contiennent des données de contrôle indiquant la révision de l&#39;instance sous la forme d&#39;un ETag. |

L’utilisation de chaque variante **de** format dépend de l’API spécifique :

| API | En-tête Content-Type | Accepter l’en-tête |
| --- | --- | --- |
| Créer un Conteneur de <br/>création d’instance | `hal`<br/>avec le paramètre schéma | `xdm.receipt` |
| Mettre à jour le Conteneur<br/>InstanceUpdate | `hal`<br/>avec le paramètre schéma | `xdm.receipt` |
| Instance de correctif | `patch.hal` | `xdm.receipt` |
| Supprimer le conteneur<br/>instanceDelete | S.O. | `xdm.receipt` |
| Conteneur Read<br/>InstanceRead | S.O. | `hal` avec `schema` paramètre |
| conteneurs<br/>instances de ListeList | S.O. | `hal` avec un `schema` paramètre spécial `https://ns.adobe.com/experience/xcore/hal/results` |
| Instances de recherche | S.O. | hal avec un `schema` paramètre spécial `https://ns.adobe.com/experience/xcore/hal/results` |
| Lire la racine du repo | S.O. | `home.hal` |

Pour les API de création, de mise à jour et de lecture du conteneur, le schéma de paramètres de format a la valeur `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` est le premier paramètre de chemin d’accès pour les API d’instance. Toutes les entités commerciales résident dans ce qu&#39;on appelle un conteneur. Un conteneur est un mécanisme d&#39;isolation qui permet de séparer les différentes préoccupations. Le premier élément de chemin d’accès pour les API d’instance de référentiel suivant le point de terminaison général est le `containerId`. L&#39;identifiant est obtenu à partir de la liste des conteneurs accessibles à l&#39;appelant. Par exemple, l’API permettant de créer une instance dans un conteneur est `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

La liste des conteneurs accessibles est obtenue en appelant le point de terminaison racine du référentiel &quot;/&quot; avec une requête HTTP GET utilisant les en-têtes standard.

## Gestion de l&#39;accès aux conteneurs

Un administrateur peut regrouper des entités, des ressources et des autorisations d’accès similaires dans des profils. Cela réduit la charge de gestion et est pris en charge par l’interface utilisateur [de la Console d’administration d’](https://auth.services.adobe.com/fr_FR/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2FONESIE1%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fadminconsole.adobe.com%252Fredirect.html%253Ftarget%253D%25252Foverview%2523from_ims%253Dtrue%2526old_hash%253D%2526api%253Dauthorize&amp;client_id=ONESIE1&amp;scope=openid%2CAdobeID%2Cadditional_info.projectedProductContext%2Cread_organizations%2Cread_members%2Cread_countries_regions%2Cadditional_info.roles%2Cadobeio_api%2Cread_auth_src_domains%2CauthSources.rwd&amp;denied_callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fdenied%2FONESIE1%3Fredirect_uri%3Dhttps%253A%252F%252Fadminconsole.adobe.com%252Fredirect.html%253Ftarget%253D%25252Foverview%2523from_ims%253Dtrue%2526old_hash%253D%2526api%253Dauthorize%26response_type%3Dtoken&amp;relay=6e938255-62f5-42c8-8176-178f6f1ab5bc&amp;locale=fr_FR&amp;flow_type=token&amp;ctx_id=admin_console_logo&amp;idp_flow_type=login#/)Adobe. Pour créer des profils et y affecter des utilisateurs, vous devez être un administrateur de produit pour la plateforme et les Offres Adobe Experience Platform de votre entreprise.

Il suffit de créer des profils de produits qui correspondent à certaines autorisations en une seule étape, puis d’ajouter simplement des utilisateurs à ces profils. Les Profils agissent comme des groupes auxquels des autorisations ont été accordées et chaque utilisateur réel ou technique de ce groupe hérite de ces autorisations.

### conteneurs de Liste accessibles aux utilisateurs et aux intégrations

Lorsque l&#39;administrateur a autorisé l&#39;accès aux conteneurs pour les utilisateurs réguliers ou les intégrations, ces conteneurs apparaîtront dans la liste dite &quot;d&#39;accueil&quot; du référentiel. La liste peut être différente pour différents utilisateurs ou intégrations, car il s’agit d’un sous-ensemble de tous les conteneurs accessibles à l’appelant. La liste des conteneurs peut être filtrée par leur association aux contextes de produits. Le paramètre de filtre est appelé `product` et peut être répété. Si plusieurs filtres contextuels de produits sont donnés, l’union des conteneurs qui ont des associations avec l’un des contextes de produits donnés est renvoyée. Notez qu’un seul conteneur peut être associé à plusieurs contextes de produits.

Le contexte des conteneurs du service de prise de décision de plateforme est actuellement `dma_offers`en cours.

>[!NOTE] Le contexte des Conteneurs de décision de plateforme va bientôt changer `acp`. Le filtrage est facultatif, mais les filtres ne `dma_offers` nécessiteront que des modifications dans une prochaine version. Pour se préparer à ce changement, les clients ne doivent utiliser aucun filtres ou appliquer les deux contextes de produits comme filtre.

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

La liste est déjà filtrée pour les utilisateurs en fonction de leurs privilèges d’accès, mais elle peut être filtrée par une requête de propriétés.

## API génériques pour gérer les entités

### Créer des instances

L’API pour créer une instance dans le référentiel utilise un paramètre `containerId` path et identifie le type de l’instance dans l’ `Content-Type` en-tête avec le paramètre schéma.

Les propriétés de l’instance sont fournies dans la charge utile encapsulée dans la `_instance` propriété. Les propriétés de l’instance doivent être valides par rapport au schéma JSON avec l’identifiant de schéma donné.

La propriété HAL `_links` doit être présente mais peut être vide. Cela signifie qu’aucun lien personnalisé n’est défini pour cette instance.

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

La réponse contient l’instanceId de l’objet qui vient d’être créé. Cet instanceId est immuable, toujours affecté par le référentiel et globalement unique. La valeur sert d’identifiant physique.

En outre, un URI (Universal Resource Identifier) est renvoyé dans la `@id` propriété de la charge utile de réponse si le schéma possède cette propriété. Chaque instance doit disposer d’une propriété qui sert d’URI et de clé principale de l’instance. Cet identifiant est utilisé par une autre instance pour créer des relations avec la nouvelle instance, y compris entre différents types. Dans la version actuelle, les URI sont générés par le référentiel et sont contenus dans la `@id` propriété. Les versions futures pourront assouplir cette règle et permettre aux clients de gérer leurs propres valeurs URI et de nommer la propriété qui la contient.

Notez que ces URI ne sont pas des URL et ne permettent pas de récupérer directement la ressource. Pour indiquer cet aspect, l’URI est précédé d’un schéma d’URI qui ne spécifie aucun protocole de récupération. Cependant, les URI peuvent être utilisés pour rechercher l’instance avec une requête.

La réponse REST comporte un en-tête Emplacement qui contient un composant URL qui peut être utilisé pour récupérer l’instance qui vient d’être créée. Ce composant est une référence d&#39;URI relative et doit être appliqué à l&#39;URI de base du référentiel. L’URI de base est renvoyé dans l’ `Content-Base` en-tête.

La `repo:etag` propriété spécifie la révision de l’instance. Cette valeur peut être utilisée dans les opérations de mise à jour pour assurer la cohérence. L’en-tête HTTP `If-Match` peut être utilisé pour ajouter une condition à un appel d’API PUT ou PATCH qui garantit qu’aucune autre modification de l’instance n’a pu être écrasée par inadvertance. La `repo:etag` valeur est renvoyée avec chaque appel create, read, update, delete et requête. La valeur est utilisée comme valeur dans l’ ` If-Match` en-tête, par [RFC7232 Section 3.1](https://tools.ietf.org/html/rfc7232#section-3.1).

Les autres propriétés indiquent le compte et la clé d’API utilisés pour créer et modifier en dernier l’instance. Puisque l’instance a été créée par cet appel, les valeurs respectives sont celles de la requête.

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

>[!NOTE] Bien que `instanceId` soit donné en tant que paramètre de chemin, les applications doivent, chaque fois que possible, ne pas construire le chemin elles-mêmes et suivre à la place les liens vers les instances contenues dans les opérations de liste et de recherche. Voir les sections ‎ 6.4.4 et ‎ 6.4.6 pour plus de détails.

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

La ressource contient également un tableau d’ID de schéma JSON. Ce tableau indique les schémas JSON par lesquels cette instance est validée.

Chaque instance contient un lien HAL du type de relation self qui correspond à l&#39;auto-relation enregistrée IANA (comme défini par [RFC5988]).

**Tester les nouvelles révisions d’une instance**

La `eTag` valeur actuelle de l’instance est renvoyée avec la réponse, elle permet aux clients d’exécuter des opérations conditionnelles sur l’instance, soit pour éviter de récupérer le même état de ressource, soit pour éviter de remplacer les valeurs d’une révision ultérieure sans que le client en ait connaissance.

L’API de recherche permet à un client de spécifier un paramètre d’ `If-None-Match` en-tête. Voir la définition de ce paramètre HTTP standard [RFC2616]. La valeur de balise d&#39;entité qu&#39;un client spécifie est la valeur qu&#39;il a reçue avec la dernière réponse, que ce soit à partir d&#39;un appel d&#39;API de mise à jour, de lecture, de liste ou de recherche. Notez que la `etag` valeur doit être opaque pour le client et doit être indiquée sous la forme d’une chaîne, entourée de guillemets.

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

### Instances de Liste pour un schéma - Tri et pagination

Les clients ne pourront pas garder le suivi des instances qu’ils créent et, par conséquent, y accéder par leur instanceId physique. L’utilisation de l’API d’instance de lecture constitue l’exception. Les clients ignorent également les instances que d’autres clients ont créées.

Un modèle d’accès plus typique consistera à parcourir le jeu de toutes les instances.

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

La réponse dépend de la `{schemaId}` valeur spécifiée. Par exemple, pour &quot;https<span></span>://ns.adobe.com/experience/offre-management/offre-activité&amp;id=xcore:offre-activité:fa24f9e8fc15c73&quot;, la réponse ressemble à ce qui suit.

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

>[!NOTE] Le résultat contient les instances pour le schéma donné ou la première page de cette liste. Notez que les instances peuvent être conformes à plusieurs schémas et peuvent donc apparaître dans plusieurs listes.

Les ressources de page sont transitoires et sont en lecture seule ; elles ne peuvent pas être mises à jour ou supprimées. Le modèle de pagination permet un accès aléatoire à des sous-ensembles de listes volumineuses sur une longue période sans conserver d’état par client.

Pour accéder à une instance liste par page de cette manière, il doit être possible de définir un tri stable sur les entrées énumérées par cette instance liste. Remarque : &quot;stable&quot; ne signifie pas que les instances s’affichent sur une page prédéterminée. En fait, lorsqu’un ordre de page est formé en triant les instances en fonction d’une propriété P et qu’un client met à jour cette propriété P, un autre client peut à nouveau accéder à cette instance sur une autre page tout en faisant une pagination dans la liste. En d&#39;autres termes, le modèle favorise le retour de résultats plus récents.

Cependant, lorsque l’ordre de tri est basé sur une propriété non modifiable, un ordre de tri &quot;stable&quot; garantit que toutes les instances qui existaient au début de l’opération de pagination seront atteintes (sauf si elles ont été supprimées au moment où leur page est atteinte). Lorsque cet ordre de tri se trouve sur une propriété qui augmente de manière monotone, les instances créées après le démarrage de l’opération de pagination sont également atteintes.

Un client peut fournir des conseils sur la taille de page qu’il souhaite, mais il appartient entièrement au référentiel de fournir plus ou moins d’instances à la page qu’il renvoie. Pour garantir l’ordre stable, le service doit ajouter ou supprimer des éléments de la page afin que la valeur de la propriété de tri soit différente selon les limites de la page. Ainsi, la page suivante ne contiendra plus certains éléments de la dernière page ou, dans le pire des cas, ne sera plus coincée avec les mêmes éléments sur chaque page.

La pagination est contrôlée par les paramètres suivants :

- **`orderBy`**: Contient une liste ordonnée de propriétés séparées par des virgules, selon laquelle la liste d’instance est triée. La première propriété est utilisée pour le tri principal, la deuxième pour résoudre les liens dans le tri principal, etc. Lorsqu’une propriété est spécifiée avec une valeur unique par instance, les liens ne sont pas possibles et un saut de page peut survenir après chaque élément. Le nom d’une propriété peut être précédé d’un préfixe `+` indiquant un ordre croissant ou `-` un ordre décroissant par cette propriété. Si le nom de la propriété n’est pas préfixé, le résultat est trié par ordre croissant. Si `orderBy` la requête ne l’indique pas, le référentiel utilise à la place la propriété instanceId physique.
- **`start`**: Les clients utilisent le paramètre de début pour définir la page à récupérer. Le paramètre début détermine le début de la page souhaitée. La réponse contiendra des instances commençant par celles dont la valeur de `orderBy` propriété est strictement supérieure (pour l’croissant) ou strictement inférieure (pour l’décroissant) à la valeur spécifiée. Si le paramètre de requête n’est pas spécifié, il prend par défaut une valeur instanceId qui est triée avant le premier identifiant d’instance possible et cette valeur est donc omise à partir de la première page.
- **`limit`**: spécifie un entier positif comme indicateur du nombre maximal d’éléments à renvoyer pour une requête donnée. La taille réelle de la réponse peut être plus petite ou plus grande, en raison de la nécessité de fournir un fonctionnement fiable du paramètre de début.

### Filtrage des listes

Le filtrage des résultats des listes est possible et se produit indépendamment du mécanisme de pagination. Les Filtres ignorent simplement les instances dans l’ordre des listes ou demandent explicitement de n’inclure que celles qui répondent à une condition donnée. Un client peut demander que l’expression de propriété soit utilisée comme filtre ou spécifier une liste d’URI à utiliser comme valeurs de la clé primaire des instances.

- **`property`**: Contient un chemin de nom de propriété suivi d’un opérateur de comparaison suivi d’une valeur. <br/>
La liste des instances renvoyées contient celles pour lesquelles l’expression est évaluée comme vraie. Par exemple, en supposant que l’instance possède une propriété de charge utile `status` et que les valeurs possibles soient `draft`, `approved``archived` , puis le paramètre de requête `deleted` `property=_instance.status==approved` renvoie uniquement les instances pour lesquelles l’état est approuvé. <br/>
<br/>
La propriété à comparer à la valeur donnée est identifiée comme un chemin d’accès. Les composants de chemin d'accès individuels sont séparés par ".", par exemple : `_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

Pour les propriétés qui comportent des valeurs de chaîne, numériques ou de date/heure, les opérateurs autorisés sont : `==`, `!=`, `<`, `<=`, `>` et `>=`. En outre, pour les propriétés avec une valeur de chaîne, un opérateur `~` peut être utilisé. L’ `~` opérateur correspond à la propriété donnée en fonction d’une expression régulière. La valeur de chaîne de la propriété doit correspondre à l’expression **entière** pour que les entités soient incluses dans les résultats filtrés. Par exemple, la recherche de la chaîne `cars` n’importe où à l’intérieur de la valeur de la propriété nécessite l’expression régulière `.*cars.*`. Sans le début ou la fin `.*`, seules les entités correspondent avec une valeur de propriété commençant ou se terminant `cars`, respectivement. Pour l’ `~` opérateur, la comparaison des caractères de la lettre n’est pas sensible à la casse. Pour tous les autres opérateurs, la comparaison est sensible à la casse.<br/><br/>
Il n’est pas possible d’utiliser uniquement les propriétés de charge utile d’instance dans les expressions de filtre. Les propriétés de l&#39;enveloppe sont comparées de la même manière, par exemple. `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
Le paramètre de `property` requête peut être répété pour que plusieurs conditions de filtre soient appliquées, par exemple pour renvoyer toutes les instances qui ont été modifiées pour la dernière fois après une certaine date et avant une certaine date. Les valeurs de ces expressions doivent être codées en URL. Si aucune expression n’est fournie et que le nom de la propriété est simplement répertorié, les éléments qui remplissent les conditions sont ceux qui possèdent une propriété portant le nom donné.<br/>
<br/>

- **`id`**: Il arrive qu’une liste doive être filtrée par l’URI des instances. Le paramètre de `property` requête peut être utilisé pour filtrer une instance, mais pour obtenir plusieurs instances, une liste d’URI peut être attribuée à la requête. Le `id` paramètre est répété et chaque occurrence spécifie une valeur URI, `id={URI_1}&id={URI_2},…` les valeurs URI doivent être codées en URL.

Les résultats paginés seront retournés sous la forme d&#39;un type MIME spécial `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

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

La réponse contient la liste des éléments de résultats dans les résultats de la propriété JSON en regard de deux propriétés qui indiquent le nombre de résultats sur cette page et le nombre total d’éléments dans la liste filtrée en commençant par la page qui vient d’être renvoyée.

### Recherche de texte intégral et requêtes structurées

Dans les cas où les clients veulent fournir des conditions de filtrage plus complexes et des instances de recherche par termes contenus dans les propriétés de chaîne, le référentiel offre une API de recherche plus puissante.

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

Outre la pagination et les paramètres de filtrage des API de liste, cette API permet aux clients d&#39;ajouter du texte intégral et des paramètres de requête booléens.

La recherche de texte intégral est contrôlée par les paramètres suivants :

- **`q`**: Contient une liste non ordonnée séparée par des espaces de termes normalisés avant d’être comparés à toute propriété de chaîne des instances. Les propriétés de chaîne sont analysées pour les termes et ces termes sont également normalisés. La requête de recherche tente de correspondre à un ou plusieurs des termes spécifiés dans le `q` paramètre. Les caractères +, -, =, &amp;&amp;, ||, >, &lt;, !, (,), {, }, [,]^, &quot;, ~, *, ?, :, / ont une signification spéciale pour déterminer les limites de mot dans la chaîne de requête et doivent être précédées d’une barre oblique inverse lorsqu’elles apparaissent dans un jeton qui doit correspondre au caractère. La chaîne de requête peut être entourée de guillemets de doublon pour une correspondance exacte de chaîne et pour échapper des caractères spéciaux.
- **`field`**: Si les termes recherchés ne doivent être associés qu’à un sous-ensemble de propriétés, le paramètre field peut alors indiquer le chemin d’accès à cette propriété. Le paramètre peut être répété pour indiquer plusieurs propriétés à comparer.
- **`qop`**: Contient un paramètre de contrôle utilisé pour modifier le comportement de correspondance de la recherche. Lorsque le paramètre est défini sur et que tous les termes recherchés doivent correspondre et que le paramètre est absent ou que sa valeur est définie sur ou alors n’importe lequel des termes peut compter pour une correspondance.

### Mise à jour et correction d’instances

Pour mettre à jour une instance, un client peut soit remplacer simultanément la liste complète des propriétés, soit utiliser une requête JSON PATCH pour manipuler les valeurs de propriété individuelles, y compris les listes.

Dans les deux cas, l’URL de la requête spécifie le chemin d’accès à l’instance physique et dans les deux cas, la réponse sera une charge utile de réception JSON comme celle renvoyée par l’opération [de](#create-instances)création. Un client doit de préférence utiliser l’ `Location` en-tête ou un lien HAL qu’il a reçu d’un appel d’API précédent pour cet objet en tant que chemin d’URL complet pour cette API. Si cela n’est pas possible, le client peut construire l’URL à partir du `containerId` et du `instanceId`.

**Demande** (PUT)

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

**Demande** (PATCH)

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

La requête PATCH applique les instructions, puis valide l&#39;entité résultante par rapport au schéma et applique les mêmes règles d&#39;intégrité référentielle et d&#39;entité que la requête PUT.

**Contrôle des modifications de valeur de propriété**

Vous pouvez empêcher la définition des propriétés lors de la création et/ou de la mise à jour, à l’aide des annotations suivantes :

- **`"meta:usereditable"`**: Booléen - Lorsqu&#39;une requête provient d&#39;un agent utilisateur qui identifie l&#39;appelant avec un jeton d&#39;accès de compte utilisateur ou technique, les propriétés annotées avec `"meta:usereditable": false` ne doivent pas être présentes dans la charge utile. Si tel est le cas, ils ne doivent pas avoir une valeur différente de celle qui est actuellement définie. Si les valeurs diffèrent, la demande de mise à jour ou de correctif est rejetée avec un état 422 Entité non traitable.
- **`"meta:immutable"`**: Boolean : les propriétés annotées avec `"meta:immutable": true` ne peuvent pas être modifiées une fois définies. Cela s&#39;applique aux demandes émanant d&#39;un utilisateur final, d&#39;une intégration de compte technique ou d&#39;un service spécial.

**Tester la mise à jour simultanée**

Dans certaines conditions, plusieurs clients tentent de mettre à jour une instance simultanément. Le référentiel est exploité sur un cluster de noeuds de calcul sans gestion centralisée des transactions. Pour éviter qu’un client écrit une instance simultanément par une autre, les clients peuvent utiliser une mise à jour conditionnelle ou une demande de correctif. En spécifiant la `etag` chaîne dans l’en-tête `If-Match` du référentiel, assurez-vous que seule la première requête réussit et que les demandes suivantes d’autres clients utilisant la même `etag` valeur échouent. La `etag` valeur change à chaque modification de l’instance. Les clients doivent récupérer l’instance pour obtenir la dernière `etag` valeur, puis un seul client sur plusieurs tentatives de mise à jour peut réussir avec cette valeur. Les autres clients seront rejetés avec un message 409 Conflict.

### Suppression d’instances

Les instances peuvent être supprimées avec un appel DELETE. Un client doit de préférence utiliser l’ `Location` en-tête ou un lien HAL qu’il a reçu d’un appel d’API précédent pour qu’il s’agisse du chemin d’accès URL complet. Si cela n’est pas possible, le client peut construire l’URL à partir de la `containerId` et de la page physique `instanceId`.

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

Lors de la réception d’une demande de suppression, le référentiel vérifie si d’autres instances, de tout schéma, font toujours référence à l’instance à supprimer. Dans un système distribué et hautement disponible, l’intégrité référentielle ne peut pas être vérifiée immédiatement. Lorsque des relations de clés étrangères sont définies, les vérifications sont effectuées de manière asynchrone. Ceci entraîne une réponse légèrement retardée au résultat de la demande de suppression. Une fois ces vérifications effectuées, la réponse immédiate comprend l’état 202 Accepté et un lien pour vérifier le résultat de l’opération de suppression dans l’ `Location` en-tête. Un client doit alors vérifier ce lien pour connaître le résultat.

Si une instance qui fait référence à l&#39;instance supprimée est trouvée, le résultat sera un rejet de l&#39;opération de suppression. Si aucune autre référence de clé étrangère n&#39;est trouvée, la suppression est alors terminée. Si le résultat n&#39;est pas encore décidé, la réponse indiquera que d&#39;ici 202 autre réponse acceptée avec le même `Location` en-tête et demandera au client de continuer à vérifier. Lorsque le résultat est déterminé, la réponse indique qu’avec un état 200 Ok et la charge utile de la réponse contient le résultat de la demande de suppression initiale. Notez que la réponse 200 Ok signifie uniquement que le résultat est connu et que le corps de la réponse contient la confirmation ou le rejet de la demande de suppression.

## Création d’offres et de leurs sous-composants

Les API décrites dans la section précédente s’appliquent uniformément à tous les types d’objets d’entreprise. La seule différence entre, par exemple, la création d’une offre et d’une activité serait l’ `content-type` en-tête notant le schéma JSON de la charge utile JSON de la demande qui est conforme au schéma. Par conséquent, les sections suivantes ne devront se concentrer que sur ces schémas et les relations entre eux.

Lors de l’utilisation des API avec le type de contenu `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`, les propriétés de l’instance sont intégrées dans la `_instance` propriété à côté de laquelle se trouve une `_links` propriété. Il s’agira du format général dans lequel toutes les instances sont représentées :

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

>[!NOTE] Pour des raisons de concision, dans tous les fragments JSON, seules les propriétés d’instance sont illustrées et uniquement lorsqu’elles sont requises, les propriétés d’enveloppe et la section _links s’affichent.

### Propriétés d’offre générales

Les Offres sont un type d’option de prise de décision et le schéma JSON des offres hérite des propriétés d’option standard que chaque instance d’option aura.

- **`@id`** - Identificateur unique de chaque option qui est la clé principale et utilisée pour référencer l&#39;option à partir d&#39;autres objets. Cette propriété est affectée lorsque l’instance est créée, est immuable et non modifiable.
- **`xdm:name`** - Chaque option a un nom qui est utilisé à des fins de recherche et d&#39;affichage. Le nom n’est pas immuable et ne peut pas être utilisé pour identifier l’instance de manière unique. Le nom peut être sélectionné librement mais doit être unique dans toutes les instances d’offre.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

Chaque instance d’offre peut comporter un ensemble facultatif de propriétés qui sont caractéristiques de cette instance seulement. Différentes offres peuvent avoir des clés différentes pour ces propriétés, les valeurs doivent, cependant, être des chaînes. Ces propriétés peuvent être utilisées dans les règles de décision et de segmentation. Ils sont également accessibles pour assembler l&#39;expérience décidée afin de personnaliser davantage les messages.

### Offre

Il existe un flux transition-état simple que toutes les options suivront. Ils ont début dans un état provisoire et quand ils seront prêts leur état sera approuvé. Une fois leur date de fin dépassée, ils peuvent être déplacés dans l’état archivé. Dans cet état, ils peuvent être supprimés ou réutilisés en les déplaçant à nouveau dans l&#39;état de rédaction.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Cette propriété est utilisée pour la gestion du cycle de vie de l&#39;instance. La valeur représente un état de flux de travail qui est utilisé pour indiquer si l&#39;offre est encore en construction (valeur = brouillon), peut généralement être considéré par le runtime (valeur = approuvé) ou si elle ne doit plus être utilisée (valeur = archivée).

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

### Représentations et placements

Les Offres sont des options de décision qui comportent des représentations de contenu. Lorsqu’une décision est prise, l’option est sélectionnée et son identifiant est utilisé pour obtenir le contenu ou les références de contenu pour l’emplacement à fournir. Une offre peut avoir plusieurs représentations, mais chacune d&#39;elles doit avoir une référence de placement différente. Ainsi, avec un placement donné, la représentation peut être déterminée sans ambiguïté.
Au cours de l’opération de décision, le placement est déterminé conjointement avec l’objet activité. Les Offres qui n&#39;ont pas de représentation avec ce placement comme référence sont automatiquement éliminées de la liste des choix.

Avant de pouvoir ajouter des représentations à une offre, les instances de placement doivent exister. Ces instances sont créées avec l’identifiant`https://ns.adobe.com/experience/offer-management/offer-placement`de schéma.

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

Une instance **Placement** peut avoir les propriétés suivantes :

- **`xdm:name`** - Contient le nom attribué au placement pour y faire référence dans les interactions humaines et les interfaces utilisateur.
- **`xdm:description`** - Utilisé pour transmettre des intentions lisibles pour la façon dont le contenu de cet emplacement est utilisé dans la diffusion globale du message. Lorsque les canaux de diffusion définissent de nouveaux emplacements, ils peuvent ajouter des informations supplémentaires dans cette propriété afin qu’un créateur de contenu puisse créer ou sélectionner le contenu en conséquence. Ces instructions ne sont ni interprétées ni appliquées officiellement. Cette propriété sert simplement de lieu pour communiquer les intentions.
- **`xdm:channel`** - URI d&#39;un canal. Le canal indique où le contenu dynamique doit être diffusé. La contrainte de canal est utilisée pour transmettre non seulement l’emplacement d’utilisation de l’offre, mais également pour déterminer l’éditeur ou le validateur de contenu utilisé pour l’expérience.
- **`xdm:componentType`** - Un identifiant de modèle, i.e. URI, pour le contenu qui peut être affiché à l&#39;emplacement décrit par cet emplacement. Les types de composants sont les suivants : lien d’image, html ou texte brut. Chaque type de composant peut impliquer un ensemble spécifique de propriétés (un modèle) que l’élément de contenu peut avoir. La liste des types de composants peut être étendue. Il existe trois valeurs de type de composant prédéfinies :
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, contrainte pour les types de supports des composants attendus dans cet emplacement. Il peut y avoir plusieurs types de supports pour un type de composant, tel que différents formats d’image.

**Les éléments de représentation** dans une offre ont une structure d&#39;objet dans la propriété de tableau `xdm:representations`. Chaque élément peut avoir les propriétés suivantes :

- **`xdm:placement`** - Cette propriété contient la référence à l&#39;instance de placement. La valeur est vérifiée lorsque la représentation est ajoutée à l’offre. Une instance de placement avec cet URI doit exister et ne doit pas être marquée comme supprimée. En outre, une vérification est effectuée pour s’assurer qu’une instance d’offre ne comporte pas deux représentations avec la même valeur pour la référence de placement.
- **`xdm:components`** - Les composants de contenu sont les fragments associés à un rendu de l&#39;offre particulier. Ces fragments sont ensuite utilisés pour composer l’expérience de l’utilisateur final. Notez que le service de prise de décision ne constitue pas en lui-même l’expérience complète de l’utilisateur final. Les propriétés suivantes font partie du modèle de chaque composant.
   - **`@type`** - cette propriété identifie le type de composant. Un autre nom pour ce concept est &quot;modèle de fragment de contenu&quot;. Un composant est simplement un URI pour un modèle défini par l’application ou le service qui assemble l’expérience utilisateur finale. `@type`
   - **`repo:id`** - cette propriété contient un identifiant unique global et immuable pour la ressource principale du composant dans le référentiel dans lequel la ressource est stockée.
   - **`repo:name`** - Cette propriété contient un nom lisible pour l&#39;actif dans le référentiel. Ce nom est défini par l’utilisateur et n’est pas garanti unique.
   - **`repo:resolveURL`** - cette propriété contient un localisateur de ressources unique pour lire la ressource dans un référentiel de contenu. Il sera ainsi plus facile d’obtenir la ressource sans que le client comprenne les API à appeler. L’URL renvoie les octets de la ressource principale de la ressource.
   - **`dc:format`** - cette propriété provient de la Dublin Core Metadata Initiative. Le format peut être utilisé pour déterminer le logiciel, le matériel ou tout autre équipement nécessaire pour afficher ou exploiter la ressource. Il est recommandé de sélectionner une valeur dans un vocabulaire contrôlé (par exemple, la liste des types de supports Internet définissant les formats de supports informatiques).
   - **`dc:language`** - Cette propriété contient la ou les langues de la ressource. Les langues sont spécifiées dans le code de langue tel que défini dans le document IETF RFC 3066.

Il existe trois types de composants prédéfinis exprimés dans la `@type` propriété :

- https<span></span>://ns.adobe.com/experience/offre-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/offre-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offre-management/content-component-html

Selon la valeur de la `@type` propriété, `xdm:components` contiendra des propriétés supplémentaires :

- **`xdm:linkURL`** - Présent lorsque le composant est un lien d’image. Cette propriété contient le lien associé à l’image et vers lequel l’ `user-agent` utilisateur final interagit avec le contenu de l’offre.
- **`xdm:copyline`** - Utilisé lorsque le composant est un texte. Outre le référencement d’une ressource de texte, par exemple pour les Offres de texte de formulaire long pouvant comporter une mise en forme, une chaîne de texte courte peut être directement stockée dans la propriété xdm:copyline.

Des propriétés supplémentaires peuvent être utilisées par les clients pour définir et évaluer les instructions de gestion du contexte. Par exemple, le client de bibliothèque de l’interface utilisateur d’Offre ajoute les propriétés facultatives suivantes pour gérer l’affichage plus facilement :

- Dans chaque élément du `xdm:components` tableau, le client de l’interface utilisateur de la bibliothèque d’Offres ajoute les propriétés suivantes. Ces propriétés ne doivent pas être supprimées ou manipulées sans comprendre l’impact sur l’interface utilisateur :
   - **`offerui:previewThumbnail`** - Il s’agit d’une propriété facultative que l’interface utilisateur de la bibliothèque d’Offres utilise pour afficher un rendu du fichier. Ce rendu n’est pas le même que la ressource elle-même. Par exemple, le contenu peut être du code HTML et le rendu est une image bitmap qui n’en montre qu’une approximation. Ce rendu (de qualité inférieure) s’affiche dans le bloc de représentation de l’offre.

Un exemple d’opération PATCH sur une instance d’offre montre comment manipuler les représentations :

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

L&#39;opération PATCH peut échouer lorsqu&#39;il n&#39;y a pas `xdm:representations` encore de propriété. Dans ce cas, l&#39;opération d&#39;ajout ci-dessus peut être précédée d&#39;une autre opération d&#39;ajout qui crée la `xdm:representations` baie ou l&#39;opération d&#39;ajout unique définit directement la baie.
Les schémas et propriétés décrits sont utilisés pour tous les types d’offre, les offres de personnalisation ainsi que les offres de secours. Les deux sections suivantes, consacrées aux contraintes et aux règles de décision, expliquent les aspects des offres de personnalisation.

## Définition des contraintes d’offre

### Contraintes de calendrier

En général, les options de décision peuvent donner un début et une date et une heure de fin qui servent de contrainte de calendrier. Les propriétés sont incorporées dans la propriété `xdm:selectionConstraint`:

- **`xdm:startDate`** - Cette propriété indique la date et l&#39;heure du début. La valeur est une chaîne formatée selon les règles RFC 3339, c’est-à-dire comme cet horodatage : &quot;2019-06-13T11:21:23.356Z&quot;.
Les options de décision qui n&#39;ont pas atteint leur date et leur heure de début ne sont pas encore considérées comme admissibles dans la décision.
- **`xdm:endDate`** - Cette propriété indique la date et l&#39;heure de fin. La valeur est une chaîne formatée selon les règles RFC 3339, c’est-à-dire comme cet horodatage : &quot;2019-07-13T11:00:00.000Z&quot;Les options de décision qui ont dépassé leur date et heure de fin ne sont plus considérées comme admissibles dans le processus de décision.

Vous pouvez modifier une contrainte de calendrier avec l&#39;appel PATCH suivant :

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`défini. Les offres de secours n’ont aucune contrainte.

### Contraintes de plafonnement

Une contrainte de plafonnement est un composant d&#39;une option de décision qui définit les paramètres de plafonnement. Le plafonnement est le processus qui consiste à limiter le nombre de fois où une option peut être proposée, pour un profil donné comme pour tous les profils. Les propriétés contiennent un entier dont la valeur doit être supérieure ou égale à 1. Les propriétés sont imbriquées dans une propriété `xdm:cappingConstraint`:

- **`xdm:globalCap`** - Un plafond global est une contrainte sur le nombre de fois où une offre peut être proposée dans sa totalité.
- **`xdm:profileCap`** - Un plafond de profil est une contrainte sur le nombre de fois où une offre peut être proposée à un profil donné.

La définition ou la modification de la contrainte de plafonnement sur une offre de personnalisation peut être effectuée avec l’appel PATCH suivant :

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`défini. Les offres de secours n’ont aucune contrainte.

Pour supprimer les valeurs de plafonnement, l’opération &quot;add&quot; est remplacée par l’opération &quot;remove&quot;. Notez que les valeurs de plafonnement existent individuellement et peuvent également être définies ou supprimées individuellement.

### Contraintes d’éligibilité

Les Offres peuvent être sélectionnées de façon conditionnelle dans le processus de décision. Lorsqu’une offre de personnalisation comporte une référence à une règle d&#39;éligibilité, la condition de la règle doit être définie sur true pour que l’objet d’offre soit pris en compte pour un profil donné. Les règles d&#39;éligibilité sont créées et gérées indépendamment des options de décision et la même règle peut être référencée à partir de plusieurs offres de personnalisation.

La référence à la règle est incorporée dans la propriété `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** - Cette propriété contient une référence à une règle d&#39;éligibilité. La valeur est celle `@id` d’une instance de schémahttps://ns.adobe.com/experience/offer-management/eligibility-rule.

L’ajout et la suppression d’une règle peuvent également s’effectuer avec une opération PATCH :

```
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`défini. Les offres de secours n’ont aucune contrainte.

Notez que la règle d&#39;éligibilité est incorporée dans la `xdm:selectionConstraint` propriété avec les contraintes de calendrier. Les opérations PATCH ne doivent pas tenter de supprimer la propriété entière `SelectionConstraint` .

## Définition de la priorité d’une offre

Les options de décision admissibles seront classées pour déterminer la meilleure option pour le profil donné. Pour prendre en charge le classement et pour fournir une valeur par défaut au cas où le classement ne serait pas déterminé par un autre mécanisme, une priorité de base peut être définie pour chaque offre de personnalisation.
La priorité de base est incorporée dans la propriété `xdm:rank`:

- **`xdm:priority`** - Cette propriété représente l&#39;ordre par défaut dans lequel une offre est sélectionnée sur une autre au cas où aucun ordre de classement spécifique au profil n&#39;est connu. Si, après la comparaison de la valeur de priorité, deux offres de personnalisation ou plus sont toujours liées, une est choisie au hasard et utilisée dans la Proposition d&#39;offre. La valeur de cette propriété doit être un entier supérieur ou égal à 0.

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`défini. Les offres de secours ne possèdent pas de propriétés de classement.

## Gestion des règles de décision

Les Règles d&#39;éligibilité contiennent les conditions qui sont évaluées pour déterminer si une option de décision donnée est admissible pour un profil donné. Le fait d’associer une règle à une ou plusieurs options de décision définit implicitement que pour cette option, la règle doit être évaluée sur true pour que l’option soit prise en compte pour cet utilisateur. La règle peut contenir des tests sur des attributs de profil, évaluer des expressions impliquant des événements d’expérience pour ce profil et inclure des données contextuelles transmises à la demande de décision. Par exemple, une condition peut être décrite comme suit :

> &quot;Inclure les personnes ayant un statut d&#39;élite et ayant effectué un vol trois fois au cours des 6 derniers mois et ayant le numéro de vol du vol actuel&quot;.

Les instances sont créées avec l’identifiant de schéma https://ns.adobe.com/experience/offer-management/eligibility-rule. La `_instance` propriété de l’appel de création ou de mise à jour se présente comme suit :

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/eligibility-rule`défini.

La valeur de la propriété de condition de la règle contient une expression PQL. Les données contextuelles sont référencées via l’expression de chemin d’accès spécial @{schemaID}.

Les règles s’alignent naturellement sur les segments de la plateforme d’expérience et, souvent, une règle réutilise simplement l’intention d’un segment en testant la `segmentMembership` propriété d’un profil. La `segmentMembership` propriété contient les résultats des conditions de segments qui ont déjà été évaluées. Cela permet à une organisation de définir une fois leurs audiences spécifiques à un domaine, de les nommer et d’évaluer les conditions une seule fois.

## Gestion des collections d’offres

### Création d’une balise et d’une offre de balisage

Les Offres peuvent être organisées en collections dans lesquelles chaque collection définit la condition de filtre à appliquer. Actuellement, l’expression de filtrage d’une collection peut présenter l’un des deux formulaires suivants :

1. Le `@id` paramètre de l’offre doit correspondre à un dans une liste d’identifiants pour que l’offre soit dans la collection. Ce filtre est simplement une énumération des URI des offres de la collection.
2. Une offre peut avoir une liste de références de balise et le filtre de la collection se compose d’une liste de balises. L’offre se trouve dans la collection lorsque :\
   a. toutes les balises de filtre correspondent à l’une des balises de l’offre.\
   b. toutes les balises du filtre correspondent à l’une des balises de l’offre.

Les balises sont des instances simples auxquelles les instances d’offre peuvent être liées. Il s’agit d’instances par elles-mêmes avec un nom pour les afficher. Le nom doit être unique pour toutes les instances afin de faciliter leur affichage dans l’interface utilisateur.

Les objets de balise permettent d’établir une catégorisation entre les options de décision (offres). Une balise peut être liée par de nombreuses offres et une offre peut avoir de nombreuses références à la balise. Une catégorie d’offres est établie en faisant référence à toutes les offres liées à un ensemble donné d’instances de balise.

Les instances de balise sont créées avec l’identifiant de schéma https://ns.adobe.com/experience/offer-management/tag. La `_instance` propriété de l’appel de création ou de mise à jour se présente comme suit :

```json
{
  "xdm:name": "credit card"
} 
```

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/tag`défini.


Une instance d’offre peut être créée avec la liste de références de balise telles que :

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Une autre solution consiste à corriger une offre pour modifier sa liste de balises :

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

Pour les deux cas, voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`défini.

Notez que la `xdm:tags` propriété doit déjà exister pour que l’opération d’ajout réussisse. Il n&#39;existe aucune balise dans une instance où l&#39;opération PATCH peut d&#39;abord ajouter la propriété array, puis ajouter une référence de balise à ce tableau.

### Définition de filtres pour les collections d’offres

Les instances de filtre sont créées avec l’identifiant de schéma https://ns.adobe.com/experience/offer-management/offer-filter. La `_instance` propriété de l’appel de création ou de mise à jour peut se présenter comme suit :

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/offer-filter`défini.

- **`xdm:filterType`** - Cette propriété indique si le filtre est configuré à l&#39;aide de balises ou référence directement les offres par leurs identifiants. Lorsque le filtre est configuré pour utiliser des balises, le type de filtre peut indiquer si toutes les balises doivent correspondre aux balises d’une offre particulière ou si l’une des balises données est suffisante pour que l’offre soit admissible au filtre. Les valeurs valides de cette propriété enum sont les suivantes :
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - Une propriété contient un tableau d&#39;URI qui sont des références à des instances d&#39;offre ou de balise, selon la valeur de `xdm:filterType`. .

L’appel suivant illustre l’aspect de la `_instance` propriété de l’appel de création ou de mise à jour au cas où des offres seraient directement référencées :

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

## Gestion des activités

Une activité d’offre est utilisée pour contrôler le processus de prise de décision. Il spécifie le filtre d’offre appliqué au stock total pour réduire les offres par rubrique/catégorie, l’emplacement pour réduire le stock aux offres qui correspondent à l’espace réservé et spécifie une option de secours si les contraintes combinées excluent toutes les options de personnalisation disponibles (offres).

Les instances d’activité sont créées avec un identifiant`https://ns.adobe.com/experience/offer-management/offer-activity`de schéma. La `_instance` propriété de l’appel de création ou de mise à jour se présente comme suit :

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/offer-activity`défini.

- **`xdm:name`** - Cette propriété obligatoire contient le nom de l&#39;activité. Le nom s’affiche dans différentes interfaces utilisateur.
- **`xdm:status`** - Cette propriété est utilisée pour la gestion du cycle de vie de l&#39;instance. La valeur représente un état de flux de travail qui est utilisé pour indiquer si l&#39;activité est encore en construction (valeur = brouillon), peut généralement être considéré par le runtime (valeur = live) ou si elle ne doit plus être utilisée (valeur = archivée).
- **`xdm:placement`** - Propriété obligatoire contenant une référence à un emplacement d&#39;offre qui est appliquée à l&#39;inventaire lorsqu&#39;une décision est prise dans le contexte de cette activité. La valeur est l’URI (`@id`) du placement d’offre utilisé.
- **`xdm:filter`** - Propriété obligatoire contenant une référence à un filtre d&#39;offre appliqué à l&#39;inventaire lorsqu&#39;une décision est prise dans le cadre de cette activité. La valeur est l’URI (`@id`) du filtre d’offre utilisé.
- **`xdm:fallback`** - Propriété obligatoire contenant une référence à une offre de secours. Une offre de secours est utilisée lorsque la prise de décision pour cette activité ne remplit aucune des offres de personnalisation. La valeur est l’URI (`@id`) d’une instance d’offre de secours.

### Gestion des offres de secours

Avant de pouvoir créer des instances d’activité, une offre de secours doit exister et doit être admissible pour le placement de l’activité. Les instances d’offre de secours sont créées avec un identifiant`https://ns.adobe.com/experience/offer-management/fallback-offer`de schéma. La `_instance` propriété de l’appel de création ou de mise à jour contient les mêmes propriétés générales qu’une offre de personnalisation, mais elle ne peut pas avoir d’autres contraintes.

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

Voir [Mise à jour et correction d’instances](#updating-and-patching-instances) pour obtenir la syntaxe cURL complète. Le `schemaId` paramètre doit être `https://ns.adobe.com/experience/offer-management/fallback-offer`défini.

