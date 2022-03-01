---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;supprimer des comptes;supprimer;api
solution: Experience Platform
title: Suppression d’un compte à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment supprimer un compte à l’aide de l’API Flow Service.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 14%

---

# Suppression d’un compte à l’aide de l’API Flow Service

Vous pouvez supprimer les comptes de sources qui contiennent des erreurs ou qui sont devenus obsolètes à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Consultez le tutoriel suivant pour savoir comment supprimer un compte à l’aide de l’API.

## Prise en main

Ce tutoriel nécessite que vous disposiez d’un identifiant de connexion valide. Si vous ne disposez pas d’un identifiant de connexion valide, sélectionnez votre connecteur de votre choix dans la [présentation des sources](../../home.md) et suivez les étapes décrites avant de lancer ce tutoriel.

Ce tutoriel nécessite également une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md): [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utilisation des API Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../landing/api-guide.md).

## Supprimer un compte

>[!TIP]
>
>Avant de supprimer le compte source, vous devez d’abord supprimer les flux de données existants associés au compte source. Pour supprimer des flux de données existants, reportez-vous au tutoriel sur [suppression des flux de données sources](./delete-dataflows.md).

Pour supprimer un compte, envoyez une requête de DELETE à la fonction [!DNL Flow Service] tout en fournissant l’identifiant de connexion de base qui correspond au compte que vous souhaitez supprimer.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la connexion.

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé avec succès la méthode [!DNL Flow Service] API pour supprimer des comptes existants.

Pour savoir comment effectuer ces opérations à l’aide de l’interface utilisateur, reportez-vous au tutoriel sur [suppression de comptes dans l’interface utilisateur](../../tutorials/ui/delete-accounts.md).
