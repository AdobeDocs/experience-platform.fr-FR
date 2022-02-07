---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;API;api;supprimer;supprimer des flux de données
solution: Experience Platform
title: Suppression d’un flux de données à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment supprimer des flux de données par lots et en flux continu à l’aide de l’API Flow Service.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: a51c878bbfd3004cb597ce9244a9ed2f2318604b
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 42%

---

# Suppression d’un flux de données à l’aide de l’API Flow Service

Vous pouvez supprimer les flux de données par lot et en flux continu qui contiennent des erreurs ou qui sont devenus obsolètes à l’aide de la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Ce tutoriel décrit les étapes de suppression des flux de données créés avec des sources par lots et en flux continu à l’aide de [!DNL Flow Service].

## Prise en main

Ce tutoriel nécessite que vous disposiez d’un identifiant de flux valide. Si vous ne disposez pas d’un identifiant de flux valide, sélectionnez votre connecteur de votre choix dans la [présentation des sources](../../home.md) et suivez les étapes décrites avant de lancer ce tutoriel.

Ce tutoriel nécessite également une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md): [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Environnements de test](../../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour supprimer correctement un flux de données à l’aide de la variable [!DNL Flow Service] API.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Suppression d’un flux de données

Avec un identifiant de flux existant, vous pouvez supprimer un flux de données en adressant une requête de DELETE au [!DNL Flow Service] API.

**Format d’API**

```http
DELETE /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | L’unique `id` pour le flux de données que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au flux de données. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le flux de données a été supprimé.

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé avec succès la méthode [!DNL Flow Service] API pour supprimer un flux de données existant.

Pour savoir comment effectuer ces opérations à l’aide de l’interface utilisateur, reportez-vous au tutoriel sur [suppression de flux de données dans l’interface utilisateur](../../tutorials/ui/delete.md)
