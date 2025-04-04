---
keywords: Experience Platform;accueil;rubriques populaires;api identity service;guide de développement identity service;région
solution: Experience Platform
title: Guide de l’API Identity Service
description: L’API Identity Service permet aux développeurs de gérer l’identification inter-appareils, inter-canaux et en temps quasi réel de vos clients à l’aide de graphiques d’identités dans Adobe Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 61%

---

# Guide de l’API [!DNL Identity Service]

Adobe Experience Platform [!DNL Identity Service] gère l’identification inter-appareils, inter-canaux et en temps quasi réel de vos clients, dans ce qu’on appelle un graphique d’identités dans Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Identity Service]](../home.md) : résout le problème fondamental de la fragmentation des données de profil client. Pour ce faire, il rapproche les identités entre les appareils et les systèmes sur lesquels les clients interagissent avec votre marque.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin ou dont vous devrez disposer pour passer avec succès des appels à l’API [!DNL Identity Service].

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

### Acheminement basé sur la région

L’API [!DNL Identity Service] utilise des points d’entrée spécifiques à une région qui nécessitent l’inclusion d’un `{REGION}` dans le chemin d’accès de la requête. Pendant la mise en service de votre organisation, une région est déterminée et stockée dans le profil de votre organisation. L’utilisation de la région appropriée avec chaque point d’entrée garantit que toutes les requêtes effectuées à l’aide de l’API [!DNL Identity Service] sont acheminées vers la région appropriée.

Deux régions sont actuellement prises en charge par les API [!DNL Identity Service] : VA7 et NLD2.

Le tableau ci-dessous présente des exemples de chemins qui utilisent les régions :

| Service | Région : VA7 | Région : NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Les requêtes effectuées sans spécifier de zone géographique peuvent entraîner des appels acheminés vers une zone géographique incorrecte ou des échecs inattendus des appels.

Si vous ne parvenez pas à localiser la région dans le profil de votre organisation, contactez votre administrateur système pour obtenir de l’aide.

## Utilisation de l’API [!DNL Identity Service]

Les paramètres d’identité utilisés dans ces services peuvent être exprimés de l’une des deux manières suivantes : composite ou XID.

Les identités composites sont des éléments incluant à la fois la valeur d’identifiant et l’espace de noms. Lors de l’utilisation d’identités composites, l’espace de noms peut être fourni soit par nom (`namespace.code`), soit par identifiant (`namespace.id`).

Lorsqu’une identité est conservée, [!DNL Identity Service] génère et affecte un identifiant à cette identité, appelé identifiant natif ou XID. Toutes les variations des API de cluster et de mappage prennent en charge les identités composites et les XID dans leurs requêtes et leurs réponses. L’un des paramètres est requis pour utiliser ces API : `xid` ou une combinaison de [`ns` ou `nsid`] et `id`.

Pour limiter le payload dans les réponses, les API adaptent leurs réponses au type de construction d’identité utilisée. En d’autres termes, si vous transmettez un XID, vos réponses auront des XID, si vous transmettez des identités composites, la réponse suivra la structure utilisée dans la requête.

Les exemples de ce document ne couvrent pas l’ensemble des fonctionnalités de l’API [!DNL Identity Service]. Pour l’API complète, voir le [guide de référence de l’API Swagger](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Toutes les identités renvoyées seront sous forme XID native lorsque le XID natif est utilisé dans la requête. Il est recommandé d’utiliser le formulaire d’identifiant ou d’espace de noms. Pour plus d’informations, voir la section relative à l’[obtention du XID d’une identité](./create-custom-namespace.md).

## Étapes suivantes

Maintenant que vous avez collecté les informations d’identification requises, vous pouvez passer au reste du guide de développement. Chaque section fournit des informations importantes sur les points d’entrée et inclut des exemples d’appels API pour effectuer des opérations CRUD. Chaque appel comprend le format général de l’API, un exemple de requête montrant les en-têtes requis et les payloads correctement formatés, ainsi qu’un exemple de réponse pour un appel réussi.
