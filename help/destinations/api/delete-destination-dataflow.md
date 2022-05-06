---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;API;api;supprimer;supprimer les flux de données de destination
solution: Experience Platform
title: Suppression d’un flux de données de destination à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment supprimer des flux de données vers des destinations de lot et de diffusion en continu à l’aide de l’API Flow Service.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 56%

---

# Suppression d’un flux de données de destination à l’aide de l’API Flow Service

Vous pouvez supprimer les flux de données qui contiennent des erreurs ou qui sont devenus obsolètes à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Ce tutoriel décrit les étapes à suivre pour supprimer des flux de données vers des destinations par lots et en flux continu à l’aide de [!DNL Flow Service].

## Prise en main {#get-started}

Pour suivre ce tutoriel, vous devez disposer d’un identifiant de flux valide. Si vous ne disposez pas d’un identifiant de flux valide, sélectionnez votre destination de choix dans la [destinations](../catalog/overview.md) et suivez les étapes décrites à la section [se connecter à la destination](../ui/connect-destination.md) et [activer les données](../ui/activation-overview.md) avant de tester ce tutoriel.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Les destinations sont des intégrations préconfigurées à des plateformes de destination qui permettent dʼactiver facilement des données provenant dʼAdobe Experience Platform. ](../home.md)[!DNL Destinations] Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
* [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour supprimer correctement un flux de données à l’aide de la variable [!DNL Flow Service] API.

### Lecture d’exemples d’appels API {#reading-sample-api-calls}

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis {#gather-values-for-required-headers}

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si la variable `x-sandbox-name` n’est pas spécifié, les requêtes sont résolues sous `prod` sandbox.

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Suppression d’un flux de données de destination {#delete-destination-dataflow}

Avec un identifiant de flux existant, vous pouvez supprimer un flux de données de destination en adressant une requête de DELETE au [!DNL Flow Service] API.

**Format d’API**

```http
DELETE /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | L’unique `id` pour le flux de données de destination que vous souhaitez supprimer. |

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

Une réponse réussie renvoie un statut HTTP 202 (Pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au flux de données. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le flux de données a été supprimé.

## Gestion des erreurs d’API {#api-error-handling}

Les points de terminaison d’API de ce tutoriel suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez utilisé avec succès la méthode [!DNL Flow Service] API permettant de supprimer un flux de données existant vers une destination.

Pour savoir comment effectuer ces opérations à l’aide de l’interface utilisateur, reportez-vous au tutoriel sur [suppression de flux de données dans l’interface utilisateur](../ui/delete-destinations.md).

Vous pouvez maintenant poursuivre et [suppression des comptes de destination](/help/destinations/api/delete-destination-account.md) en utilisant la variable [!DNL Flow Service] API.
