---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;API;api;supprimer;supprimer les flux de données de destination
solution: Experience Platform
title: Suppression d’un flux de données de destination à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment supprimer des flux de données vers des destinations de lot et de diffusion en continu à l’aide de l’API Flow Service.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 49%

---

# Suppression d’un flux de données de destination à l’aide de l’API Flow Service

Vous pouvez supprimer les flux de données qui contiennent des erreurs ou qui sont devenus obsolètes à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Ce tutoriel décrit les étapes de suppression des flux de données vers les destinations de lot et de diffusion en continu à l’aide de [!DNL Flow Service].

## Prise en main {#get-started}

Pour suivre ce tutoriel, vous devez disposer d’un identifiant de flux valide. Si vous ne disposez pas d’un ID de flux valide, sélectionnez la destination de votre choix dans le [catalogue des destinations](../catalog/overview.md) et suivez les étapes décrites à [se connecter à la destination](../ui/connect-destination.md) et [activer les données](../ui/activation-overview.md) avant de lancer ce tutoriel.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Destinations](../home.md) : [!DNL Destinations] sont des intégrations préconfigurées avec des plateformes de destination qui permettent l’activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
* [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour supprimer correctement un flux de données à l’aide de l’API [!DNL Flow Service].

### Lecture d’exemples d’appels API {#reading-sample-api-calls}

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis {#gather-values-for-required-headers}

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si l’en-tête `x-sandbox-name` n’est pas spécifié, les requêtes sont résolues sous l’environnement de test `prod`.

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Supprimer un flux de données de destination {#delete-destination-dataflow}

Avec un identifiant de flux existant, vous pouvez supprimer un flux de données de destination en adressant une requête de DELETE à l’API [!DNL Flow Service].

**Format d’API**

```http
DELETE /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | La valeur `id` unique du flux de données de destination que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 202 (pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au flux de données. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le flux de données a été supprimé.

## Gestion des erreurs d’API {#api-error-handling}

Les points de terminaison d’API de ce tutoriel suivent les principes généraux des messages d’erreur de l’API d’Experience Platform. Pour plus d’informations sur l’interprétation des réponses d’erreur, reportez-vous aux [codes d’état d’API](/help/landing/troubleshooting.md#api-status-codes) et [ erreurs d’en-tête de requête](/help/landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez réussi à utiliser l’API [!DNL Flow Service] pour supprimer un flux de données existant vers une destination.

Pour savoir comment effectuer ces opérations à l’aide de l’interface utilisateur, reportez-vous au tutoriel sur la [suppression de flux de données dans l’interface utilisateur](../ui/delete-destinations.md).

Vous pouvez désormais [ supprimer des comptes de destination ](/help/destinations/api/delete-destination-account.md) à l’aide de l’API [!DNL Flow Service].
