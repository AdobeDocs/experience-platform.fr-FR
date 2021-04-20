---
keywords: Experience Platform ; accueil ; rubriques populaires ; api du service d'identité ; guide du développeur du service d'identité ; région
solution: Experience Platform
title: Guide de l'API du service d'identité
topic: API guide
description: L'API Identity Service permet aux développeurs de gérer l'identification inter-périphériques, entre canaux et quasi en temps réel de vos clients à l'aide de graphiques d'identité dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
translation-type: tm+mt
source-git-commit: 69c3106070e31377ea8571cd14dc33aa9b6f7037
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 67%

---


# [!DNL Identity Service] Guide de l’API

Adobe Experience Platform [!DNL Identity Service] gère l&#39;identification inter-périphériques, entre canaux et quasi en temps réel de vos clients dans ce qu&#39;on appelle un graphique d&#39;identité au sein de Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Identity Service]](../home.md) : résout le problème fondamental posé par la fragmentation des données de profil des clients. Pour ce faire, il rapproche les identités entre les appareils et les systèmes sur lesquels les clients interagissent avec votre marque.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fournit un profil unifié et en temps réel pour les consommateurs, basé sur des données agrégées provenant de sources multiples.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir invoquer l&#39;API [!DNL Identity Service].

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

### Acheminement basé sur la région

L&#39;API [!DNL Identity Service] utilise des points de terminaison spécifiques à la région qui nécessitent l&#39;inclusion d&#39;un `{REGION}` dans le chemin de requête. Pendant la mise en service de votre organisation IMS, une région est déterminée et stockée dans votre profil d’organisation IMS. L’utilisation de la région appropriée avec chaque point de terminaison garantit que toutes les requêtes effectuées à l’aide de l’API [!DNL Identity Service] sont acheminées vers la région appropriée.

Deux régions sont actuellement prises en charge par les API [!DNL Identity Service] : VA7 et NLD2.

Le tableau ci-dessous présente des exemples de chemins qui utilisent les régions :

| Service | Région : VA7 | Région : NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Les requêtes effectuées sans spécifier de région peuvent entraîner le routage des appels vers une région incorrecte ou entraîner l’échec inattendu des appels.

Si vous ne parvenez pas à localiser la région dans votre profil d’organisation IMS, contactez votre administrateur système pour obtenir de l’aide.

## Utilisation de l&#39;API [!DNL Identity Service]

Les paramètres d’identité utilisés dans ces services peuvent être exprimés de l’une des deux manières suivantes : composite ou XID.

Les identités composites sont des éléments incluant à la fois la valeur d’identifiant et l’espace de noms. Lors de l’utilisation d’identités composites, l’espace de noms peut être fourni soit par nom (`namespace.code`), soit par identifiant (`namespace.id`).

Lorsqu&#39;une identité est conservée, [!DNL Identity Service] génère et affecte un identifiant à cette identité, appelé ID natif, ou XID. Toutes les variations des API de cluster et de mappage prennent en charge les identités composites et les XID dans leurs requêtes et leurs réponses. L’un des paramètres est requis pour utiliser ces API : `xid` ou une combinaison de [`ns` ou `nsid`] et `id`.

Pour limiter le payload dans les réponses, les API adaptent leurs réponses au type de construction d’identité utilisée. En d’autres termes, si vous transmettez un XID, vos réponses auront des XID, si vous transmettez des identités composites, la réponse suivra la structure utilisée dans la requête.

Les exemples de ce document ne couvrent pas la fonctionnalité complète de l&#39;API [!DNL Identity Service]. Pour l’API complète, voir le [guide de référence de l’API Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE]
>
>Toutes les identités renvoyées seront compilées dans un formulaire XID natif lorsque le XID natif est utilisé dans la requête. Il est recommandé d’utiliser le formulaire d’identifiant ou d’espace de noms. Pour plus d’informations, voir la section relative à l’[obtention du XID d’une identité](./create-custom-namespace.md).

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points de terminaison et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.
