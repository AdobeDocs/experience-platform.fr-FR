---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Prise en main
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Guide du développeur de l&#39;API Identity Service

Le service d’identité Adobe Experience Platform gère les  inter-périphériques, entre et l’identification en temps quasi réel de vos clients dans ce qu’on appelle un graphique d’identité dans Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Service](../home.md)d&#39;identité : Résout le problème fondamental posé par la fragmentation des données  des clients. Pour ce faire, il associe les identités entre les périphériques et les systèmes sur lesquels les clients interagissent avec votre marque.
- [](../../profile/home.md)du client en temps réel : Fournit un unifié et en temps réel, basé sur des données agrégées provenant de sources multiples.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir effectuer des appels vers l&#39;API Identity Service.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

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

###  basée sur la région

L’API du service d’identité utilise des points de terminaison spécifiques à une région qui nécessitent l’inclusion d’un élément `{REGION}` dans le chemin de requête. Pendant la mise en service de votre organisation IMS, une région est déterminée et stockée dans votre  d&#39;organisation IMS. L’utilisation de la région appropriée avec chaque point de fin garantit que toutes les demandes effectuées à l’aide de l’API Identity Service sont acheminées vers la région appropriée.

Il existe actuellement deux régions prises en charge par les API du service d’identité : VA7 et NLD2.

Le tableau ci-dessous présente des exemples de chemins utilisant des régions :

| Service | Région : VA7 | Région : NLD2 |
| ------ | -------- |--------- |
| API du service d’identité | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| API de  d&#39;identité  | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] Les demandes effectuées sans spécifier de région peuvent entraîner l’ d’appels vers une région incorrecte ou entraîner l’échec inattendu des appels.

Si vous ne parvenez pas à localiser la région dans votre  d&#39;organisation IMS, contactez votre administrateur système pour obtenir de l&#39;aide.

## Utilisation de l&#39;API Identity Service

Les paramètres d&#39;identité utilisés dans ces services peuvent être exprimés de l&#39;une des deux manières suivantes; composite ou XID.

Les identités composites sont des éléments incluant à la fois la valeur d’ID et  . Lors de l’utilisation d’identités composites, le  de  peut être fourni soit par nom (`namespace.code`), soit par ID (`namespace.id`).

Lorsqu’une identité est conservée, Identity Service génère et affecte un identifiant à cette identité, appelé ID natif, ou XID. Toutes les variations des API de cluster et de mappage prennent en charge les identités composites et XID dans leurs demandes et réponses. L’un des paramètres est requis - `xid` ou une combinaison de [`ns` ou `nsid`] et `id` pour utiliser ces API.

Pour limiter la charge utile dans les réponses, les API adaptent leurs réponses au type de concept d’identité utilisé. En d’autres termes, si vous transmettez XID, vos réponses auront des XID, si vous transmettez des identités composites, la réponse suivra la structure utilisée dans la requête.

Les exemples de ce ne couvrent pas la fonctionnalité complète de l’API Identity Service. Pour obtenir l’API complète, voir le Guide de référence [de l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Swagger.

>[!NOTE] Toutes les identités renvoyées seront dans un formulaire XID natif lorsque le XID natif est utilisé dans la requête. Il est recommandé d’utiliser le formulaire d’ID/  de. Pour plus d’informations, voir la section relative à l’ [obtention du XID pour une identité](./create-custom-namespace.md).

## Étapes suivantes

Maintenant que vous avez rassemblé les informations d’identification requises, vous pouvez continuer à lire le reste du guide du développeur. Chaque section fournit des informations importantes sur leurs points de fin et présente des exemples d’appels d’API pour effectuer des opérations CRUD. Chaque appel comprend le format **général de l’** API, un exemple de **requête** montrant les en-têtes requis et les charges utiles correctement formatées, ainsi qu’un exemple de **réponse** pour un appel réussi.
