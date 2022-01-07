---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de flux;supprimer des comptes de destination;supprimer;api
solution: Experience Platform
title: Suppression d’un compte de destination à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment supprimer un compte de destination à l’aide de l’API Flow Service.
source-git-commit: df89f8ce8050b26068e0ab7aa01f1c964f5d2422
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 37%

---

# Suppression d’un compte de destination à l’aide de l’API Flow Service

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

Avant d’activer les données, vous devez vous connecter à la destination en configurant d’abord un compte de destination. Ce tutoriel décrit les étapes à suivre pour supprimer des comptes de destination qui ne sont plus nécessaires à l’aide de la méthode [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>La suppression des comptes de destination est actuellement prise en charge dans l’API Flow Service uniquement. Les comptes de destination ne peuvent pas être supprimés à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main {#get-started}

Ce tutoriel nécessite que vous disposiez d’un identifiant de connexion valide. L’identifiant de connexion représente la connexion du compte à la destination. Si vous ne disposez pas d’un identifiant de connexion valide, sélectionnez la destination de votre choix dans la [destinations](../catalog/overview.md) et suivez les étapes décrites à la section [se connecter à la destination](../ui/connect-destination.md) avant de tester ce tutoriel.

Ce tutoriel nécessite également une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Les destinations sont des intégrations préconfigurées à des plateformes de destination qui permettent dʼactiver facilement des données provenant dʼAdobe Experience Platform. ](../home.md)[!DNL Destinations] Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
* [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour supprimer un compte de destination à l’aide de la variable [!DNL Flow Service] API.

### Lecture d’exemples d’appels API {#reading-sample-api-calls}

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis {#gather-values-for-required-headers}

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si la variable `x-sandbox-name` n’est pas spécifié, les requêtes sont résolues sous `prod` sandbox.

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Recherchez l’identifiant de connexion du compte de destination que vous souhaitez supprimer. {#find-connection-id}

>[!NOTE]
>Ce tutoriel utilise la méthode [Destination aérienne](../catalog/mobile-engagement/airship-attributes.md) par exemple, mais les étapes décrites s’appliquent à l’une des [destinations disponibles](../catalog/overview.md).

La première étape de la suppression d’un compte de destination consiste à trouver l’identifiant de connexion correspondant au compte de destination que vous souhaitez supprimer.

Dans l’interface utilisateur de l’Experience Platform, accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Comptes]** et sélectionnez le compte à supprimer en sélectionnant le nombre dans la variable **[!UICONTROL Destinations]** colonne .

![Sélectionner le compte de destination à supprimer](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Vous pouvez ensuite récupérer l’identifiant de connexion du compte de destination à partir de l’URL de votre navigateur.

![Récupération de l’identifiant de connexion à partir de l’URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "imsOrgId": "{IMS_ORG}",
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
>* [Utilisation de l’interface utilisateur de l’Experience Platform](../ui/delete-destinations.md) pour supprimer des flux de données existants ;
>* [Utilisation de l’API Flow Service](delete-destination-dataflow.md) pour supprimer des flux de données existants.


Une fois que vous disposez d’un identifiant de connexion et que vous avez vérifié qu’il n’existe aucun flux de données vers le compte de destination, effectuez une requête de DELETE à la variable [!DNL Flow Service] API.

**Format d’API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | L’unique `id` pour la connexion que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la connexion. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le compte de destination a été supprimé.

## Gestion des erreurs d’API {#api-error-handling}

Les points de terminaison d’API de ce tutoriel suivent les principes généraux des messages d’erreur de l’API Experience Platform. Voir [Codes d’état d’API](../../landing/troubleshooting.md#api-status-codes) et [erreurs d’en-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé avec succès la méthode [!DNL Flow Service] API pour supprimer les comptes de destination existants.
