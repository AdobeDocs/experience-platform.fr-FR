---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;supprimer des comptes de destination;supprimer;api
solution: Experience Platform
title: Suppression d’un compte de destination à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment supprimer un compte de destination à l’aide de l’API Flow Service.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 40%

---

# Suppression d’un compte de destination à l’aide de l’API Flow Service

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

Avant d’activer les données, vous devez vous connecter à la destination en configurant d’abord un compte de destination. Ce tutoriel décrit les étapes à suivre pour supprimer les comptes de destination qui ne sont plus nécessaires à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>La suppression des comptes de destination est actuellement prise en charge dans l’API Flow Service uniquement. Les comptes de destination ne peuvent pas être supprimés à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main {#get-started}

Ce tutoriel nécessite que vous disposiez d’un identifiant de connexion valide. L’identifiant de connexion représente la connexion du compte à la destination. Si vous ne disposez pas d’un ID de connexion valide, sélectionnez votre destination de votre choix dans le [catalogue des destinations](../catalog/overview.md) et suivez les étapes décrites à [se connecter à la destination](../ui/connect-destination.md) avant de lancer ce tutoriel.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Destinations](../home.md) : [!DNL Destinations] sont des intégrations préconfigurées avec des plateformes de destination qui permettent l’activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
* [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour supprimer un compte de destination à l’aide de l’API [!DNL Flow Service].

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

## Recherchez l’identifiant de connexion du compte de destination que vous souhaitez supprimer. {#find-connection-id}

>[!NOTE]
>Ce tutoriel utilise comme exemple la [destination de l’Airship](../catalog/mobile-engagement/airship-attributes.md), mais les étapes décrites s’appliquent à l’une des [ destinations disponibles](../catalog/overview.md).

La première étape de la suppression d’un compte de destination consiste à trouver l’identifiant de connexion correspondant au compte de destination que vous souhaitez supprimer.

Dans l’interface utilisateur de l’Experience Platform, accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Comptes]** et sélectionnez le compte à supprimer en sélectionnant le numéro dans la colonne **[!UICONTROL Destinations]**.

![Sélectionner le compte de destination à supprimer](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Vous pouvez ensuite récupérer l’identifiant de connexion du compte de destination à partir de l’URL de votre navigateur.

![ Récupération de l’ID de connexion à partir de l’URL ](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## Supprimer la connexion {#delete-connection}

>[!IMPORTANT]
>
>Avant de supprimer le compte de destination, vous devez supprimer tout flux de données existant vers le compte de destination.
>Pour supprimer des flux de données existants, reportez-vous aux pages ci-dessous :
>* [Utilisez l’interface utilisateur de l’Experience Platform](../ui/delete-destinations.md) pour supprimer les flux de données existants ;
>* [Utilisez l’API Flow Service](delete-destination-dataflow.md) pour supprimer les flux de données existants.

Une fois que vous disposez d’un identifiant de connexion et que vous avez vérifié qu’il n’existe aucun flux de données vers le compte de destination, effectuez une requête de DELETE vers l’API [!DNL Flow Service].

**Format d’API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `id` unique de la connexion que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la connexion. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le compte de destination a été supprimé.

## Gestion des erreurs d’API {#api-error-handling}

Les points de terminaison d’API de ce tutoriel suivent les principes généraux des messages d’erreur de l’API d’Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à utiliser l’API [!DNL Flow Service] pour supprimer des comptes de destination existants. Pour plus d’informations sur l’utilisation des destinations, consultez la [présentation des destinations](/help/destinations/home.md).