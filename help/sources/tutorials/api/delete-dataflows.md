---
keywords: Experience Platform;accueil;rubriques les plus consultées;flow service;API;api;supprimer;supprimer des flux de données
solution: Experience Platform
title: Supprimer un flux de données à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment supprimer des flux de données de lots et de diffusion en continu à l’aide de l’API Flow Service.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 100%

---

# Supprimer un flux de données à l’aide de l’API Flow Service

Vous pouvez supprimer des flux de données de lots et de diffusion en continu contenant des erreurs ou devenus obsolètes à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Ce tutoriel décrit les étapes à suivre pour supprimer des flux de données créés avec des sources de lots et de diffusion en continu à l’aide de lʼAPI [!DNL Flow Service].

## Prise en main

Pour suivre ce tutoriel, vous devez disposer d’un identifiant de flux valide. Si vous ne disposez pas d’un identifiant de flux valide, sélectionnez le connecteur de votre choix dans la [présentation des sources](../../home.md) et suivez les étapes décrites avant de lancer ce tutoriel.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide de [Prise en main des API Platform](../../../landing/api-guide.md).

## Supprimer un flux de données

À lʼaide dʼun identifiant de flux existant, vous pouvez supprimer un flux de données en adressant une requête DELETE à l’API [!DNL Flow Service].

**Format d’API**

```http
DELETE /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | Valeur `id` unique du flux de données à supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au flux de données. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le flux de données a été supprimé.

## Étapes suivantes

Vous êtes arrivé au bout de ce tutoriel, félicitations ! Grâce à celui-ci, vous avez utilisé lʼAPI [!DNL Flow Service] pour supprimer un flux de données existant.

Pour obtenir des instructions sur la façon dʼeffectuer ces opérations à lʼaide de lʼinterface utilisateur, suivez le tutoriel [Supprimer des flux de données dans l’interface utilisateur](../../tutorials/ui/delete.md).
