---
keywords: Experience Platform;accueil;rubriques les plus consultées;flow service;supprimer des comptes;supprimer;api
solution: Experience Platform
title: Supprimer un compte à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment supprimer un compte à l’aide de l’API Flow Service.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 92%

---

# Supprimer un compte à l’aide de l’API Flow Service

Vous pouvez supprimer des comptes sources contenant des erreurs ou obsolètes à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Suivez les étapes du tutoriel suivant pour supprimer un compte à l’aide de l’API.

## Prise en main

Ce tutoriel nécessite que vous disposiez d’un identifiant de connexion valide. Si vous ne disposez pas d’un identifiant de connexion valide, sélectionnez le connecteur de votre choix dans la [présentation des sources](../../home.md) et suivez les étapes décrites avant de lancer ce tutoriel.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources &#x200B;](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../landing/api-guide.md).

## Supprimer un compte

>[!TIP]
>
>Avant de supprimer le compte source, vous devez d’abord supprimer les flux de données existants associés à ce compte source. Pour supprimer des flux de données existants, consultez le tutoriel [Supprimer des flux de données sources](./delete-dataflows.md).

Pour supprimer un compte, envoyez une requête DELETE à l’API [!DNL Flow Service] en fournissant l’identifiant de connexion de base qui correspond au compte que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Paramètre | Description |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base du compte source que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la connexion.

## Étapes suivantes

Vous êtes arrivé au bout de ce tutoriel, félicitations ! Grâce à celui-ci, vous avez réussi à utiliser l’API [!DNL Flow Service] pour supprimer des comptes existants.

Pour savoir comment effectuer ces opérations à l’aide de l’interface utilisateur, consultez le tutoriel [Supprimer des comptes dans l’interface utilisateur](../../tutorials/ui/delete-accounts.md).
