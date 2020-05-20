---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Prise en main
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# Guide du développeur de l&#39;API Identity Service

Adobe Experience Platform Identity Service gère l’identification inter-périphériques, entre canaux et quasi en temps réel de vos clients dans ce qu’on appelle un graphique d’identité dans Adobe Experience Platform.

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

- [Service](../home.md)d&#39;identité : Résout le défi fondamental posé par la fragmentation des données du profil client. Pour ce faire, il établit des passerelles entre les identités des différents périphériques et systèmes sur lesquels les clients interagissent avec votre marque.
- [Profil](../../profile/home.md)client en temps réel : Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de plusieurs sources.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir invoquer l&#39;API Identity Service.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

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

### routage basé sur la région

L’API du service d’identité utilise des points de terminaison spécifiques à la région qui nécessitent l’inclusion d’un élément dans le chemin d’accès à la demande. `{REGION}` Pendant la mise en service de votre organisation IMS, une région est déterminée et stockée dans votre profil d&#39;organisation IMS. L’utilisation de la région appropriée avec chaque point de terminaison garantit que toutes les demandes effectuées à l’aide de l’API Identity Service sont acheminées vers la région appropriée.

Deux régions sont actuellement prises en charge par les API du service d’identité : VA7 et NLD2.

Le tableau ci-dessous présente des exemples de chemins utilisant des régions :

| Service | Région : VA7 | Région : NLD2 |
| ------ | -------- |--------- |
| API du service d&#39;identité | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| API d&#39;Espace de nommage d&#39;identité | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] Les demandes effectuées sans spécifier de région peuvent entraîner un routage des appels vers la région incorrecte ou entraîner un échec inattendu des appels.

Si vous ne parvenez pas à localiser la région dans votre profil d&#39;organisation IMS, contactez votre administrateur système pour obtenir de l&#39;aide.

## Utilisation de l&#39;API Identity Service

Les paramètres d&#39;identité utilisés dans ces services peuvent être exprimés de deux manières : composite ou XID.

Les identités composites sont des éléments comprenant à la fois la valeur d’ID et l’espace de nommage. Lors de l’utilisation d’identités composites, l’espace de nommage peut être fourni par nom (`namespace.code`) ou par identifiant (`namespace.id`).

Lorsqu’une identité est conservée, Identity Service génère et affecte un identifiant à cette identité, appelé ID natif, ou XID. Toutes les variations des API de cluster et de mappage prennent en charge les identités composites et XID dans leurs demandes et réponses. L&#39;un des paramètres est requis - `xid` ou une combinaison de [`ns` ou `nsid`] et et pour `id` utiliser ces API.

Pour limiter la charge utile dans les réponses, les API adaptent leurs réponses au type de concept d&#39;identité utilisé. En d’autres termes, si vous transmettez XID, vos réponses auront des XID, si vous transmettez des identités composites, la réponse suivra la structure utilisée dans la requête.

Les exemples de ce document ne couvrent pas l&#39;intégralité des fonctionnalités de l&#39;API Identity Service. Pour obtenir l’API complète, voir le Guide de référence [de l’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Swagger.

>[!NOTE] Toutes les identités renvoyées seront dans un formulaire XID natif lorsque le XID natif est utilisé dans la requête. Il est recommandé d’utiliser le formulaire ID/espace de nommage. Pour plus d’informations, voir la section relative à l’ [obtention du XID pour une identité](./create-custom-namespace.md).

## Étapes suivantes

Maintenant que vous avez rassemblé les informations d’identification requises, vous pouvez continuer à lire le reste du guide du développeur. Chaque section fournit des informations importantes sur leurs points de terminaison et présente des exemples d’appels d’API pour effectuer des opérations CRUD. Chaque appel comprend le format **général de l’** API, un exemple de **requête** présentant les en-têtes requis et les charges utiles correctement formatées, ainsi qu’un exemple de **réponse** pour un appel réussi.
