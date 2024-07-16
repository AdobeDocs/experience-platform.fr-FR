---
solution: Experience Platform
title: Modification des connexions de destination à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment modifier différents composants d’une connexion de destination à l’aide de l’API Flow Service.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: 2a72f6886f7a100d0a1bf963eedaed8823a7b313
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 29%

---

# Modification des connexions de destination à l’aide de l’API Flow Service

Ce tutoriel décrit les étapes à suivre pour modifier différents composants d’une connexion de destination. Découvrez comment mettre à jour les informations d’identification d’authentification, exporter l’emplacement, etc. à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Les opérations de modification décrites dans ce tutoriel ne sont actuellement prises en charge que par le biais de l’API Flow Service.

## Commencer {#get-started}

Ce tutoriel nécessite que vous disposiez d’un identifiant de flux de données valide. Si vous ne disposez pas d’un identifiant de flux de données valide, sélectionnez votre destination de votre choix dans le [catalogue des destinations](../catalog/overview.md) et suivez les étapes décrites à [se connecter à la destination](../ui/connect-destination.md) et [activer les données](../ui/activation-overview.md) avant de lancer ce tutoriel.

>[!NOTE]
>
> Les termes *flow* et *dataflow* sont interchangeables dans ce tutoriel. Dans le cadre de ce tutoriel, ils ont la même signification.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Destinations](../home.md) : [!DNL Destinations] sont des intégrations préconfigurées avec des plateformes de destination qui permettent l’activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
* [Sandbox](../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour mettre à jour votre flux de données avec succès à l’aide de l’API [!DNL Flow Service].

### Lecture d’exemples d’appels API {#reading-sample-api-calls}

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis {#gather-values-for-required-headers}

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources d’Experience Platform, y compris celles appartenant à [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si l’en-tête `x-sandbox-name` n’est pas spécifié, les requêtes sont résolues sous l’environnement de test `prod`.

Toutes les requêtes contenant une payload (`POST`, `PUT`, `PATCH`) nécessitent un en-tête de type de média supplémentaire :

* `Content-Type: application/json`

## Rechercher des détails du flux de données {#look-up-dataflow-details}

La première étape de la modification de votre connexion de destination consiste à récupérer les détails du flux de données à l’aide de votre identifiant de flux. Vous pouvez afficher les détails actuels d’un flux de données existant en adressant une requête GET au point d’entrée `/flows`.

>[!TIP]
>
>Vous pouvez utiliser l’interface utilisateur de l’Experience Platform pour obtenir l’identifiant de flux de données souhaité pour une destination. Accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**, sélectionnez le flux de données de destination de votre choix et recherchez l’ID de destination dans le rail de droite. L’ID de destination est la valeur que vous utiliserez comme ID de flux à l’étape suivante.
>
> ![Obtenir l’ID de destination à l’aide de l’interface utilisateur Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**Format d’API**

```http
GET /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | La valeur `id` unique du flux de données de destination que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère des informations concernant votre ID de flux.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails actuels de votre flux de données, y compris sa version, son identifiant unique (`id`) et d’autres informations pertinentes. Les identifiants de connexion cible et de base les plus pertinents pour ce tutoriel sont mis en évidence dans la réponse ci-dessous. Vous utiliserez ces identifiants dans les sections suivantes pour mettre à jour différents composants de la connexion de destination.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## Modifier les composants de connexion cible (emplacement de stockage et autres composants) {#patch-target-connection}

Les composants d’une connexion cible diffèrent par destination. Par exemple, pour les destinations [!DNL Amazon S3], vous pouvez mettre à jour le compartiment et le chemin d’accès où les fichiers sont exportés. Pour les destinations [!DNL Pinterest], vous pouvez mettre à jour votre [!DNL Pinterest Advertiser ID] et, pour [!DNL Google Customer Match], vous pouvez mettre à jour votre [!DNL Pinterest Account ID].

Pour mettre à jour les composants d’une connexion cible, effectuez une requête `PATCH` vers le point de terminaison `/targetConnections/{TARGET_CONNECTION_ID}` tout en fournissant votre identifiant de connexion cible, votre version et les nouvelles valeurs que vous souhaitez utiliser. Souvenez-vous que vous avez obtenu votre identifiant de connexion cible à l’étape précédente, lorsque vous avez inspecté un flux de données existant vers la destination souhaitée.

>[!IMPORTANT]
>
>L’en-tête `If-Match` est requis lors de l’exécution d’une requête `PATCH`. La valeur de cet en-tête est la version unique de la connexion cible que vous souhaitez mettre à jour. La valeur etag est mise à jour à chaque mise à jour réussie d’une entité de flux, telle que le flux de données, la connexion cible, etc.
>
> Pour obtenir la dernière version de la valeur etag, effectuez une requête de GET sur le point de terminaison `/targetConnections/{TARGET_CONNECTION_ID}`, où `{TARGET_CONNECTION_ID}` est l’identifiant de connexion cible que vous souhaitez mettre à jour.
>
> Veillez à placer la valeur de l’en-tête `If-Match` entre guillemets doubles, comme dans les exemples ci-dessous, lors de l’exécution de requêtes `PATCH`.

Vous trouverez ci-dessous quelques exemples de mise à jour des paramètres dans la spécification de connexion cible pour différents types de destinations. Mais la règle générale pour mettre à jour les paramètres pour n’importe quelle destination est la suivante :

Obtenez l’identifiant de flux de données de la connexion > obtenez l’identifiant de connexion cible > `PATCH` de la connexion cible avec les valeurs mises à jour pour les paramètres souhaités.

>[!BEGINSHADEBOX]

**Format d’API**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Requête**

La requête suivante met à jour les paramètres `bucketName` et `path` d’une connexion de destination [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Définit la partie du flux à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion cible et une balise électronique mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service], tout en fournissant votre identifiant de connexion cible.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager et Google Ad Manager 360]

**Requête**

La requête suivante met à jour les paramètres d’une connexion [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) ou [[!DNL Google Ad Manager 360] destination](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) pour ajouter le nouveau champ [**[!UICONTROL Ajouter un ID d’audience au nom de l’audience]**](/help/release-notes/2023/april-2023.md#destinations).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Définit la partie du flux à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion cible et une balise mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service], tout en fournissant votre identifiant de connexion cible.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Requête**

La requête suivante met à jour le paramètre `advertiserId` d’une [[!DNL Pinterest] connexion de destination](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Définit la partie du flux à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion cible et une balise mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service], tout en fournissant votre identifiant de connexion cible.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Modifier les composants de connexion de base (paramètres d’authentification et autres composants) {#patch-base-connection}

Modifiez la connexion de base lorsque vous souhaitez mettre à jour les informations d’identification d’une destination. Les composants d’une connexion de base diffèrent par destination. Par exemple, pour les destinations [!DNL Amazon S3], vous pouvez mettre à jour la clé d’accès et la clé secrète vers votre emplacement [!DNL Amazon S3].

Pour mettre à jour les composants d’une connexion de base, effectuez une requête `PATCH` vers le point de terminaison `/connections` tout en fournissant votre identifiant de connexion de base, votre version et les nouvelles valeurs que vous souhaitez utiliser.

Souvenez-vous que vous avez obtenu votre identifiant de connexion de base dans une [étape précédente](#look-up-dataflow-details), lorsque vous avez inspecté un flux de données existant vers la destination souhaitée pour le paramètre `baseConnection`.

>[!IMPORTANT]
>
>L’en-tête `If-Match` est requis lors de l’exécution d’une requête `PATCH`. La valeur de cet en-tête est la version unique de la connexion de base que vous souhaitez mettre à jour. La valeur etag est mise à jour à chaque mise à jour réussie d’une entité de flux, telle que le flux de données, la connexion de base, etc.
>
> Pour obtenir la dernière version de la valeur Etag, effectuez une requête de GET sur le point de terminaison `/connections/{BASE_CONNECTION_ID}`, où `{BASE_CONNECTION_ID}` est l’identifiant de connexion de base que vous souhaitez mettre à jour.
>
> Veillez à placer la valeur de l’en-tête `If-Match` entre guillemets doubles, comme dans les exemples ci-dessous, lors de l’exécution de requêtes `PATCH`.

Vous trouverez ci-dessous quelques exemples de mise à jour des paramètres dans la spécification de connexion de base pour différents types de destinations. Mais la règle générale pour mettre à jour les paramètres pour n’importe quelle destination est la suivante :

Obtenez l’identifiant de flux de données de la connexion > obtenez l’identifiant de connexion de base > `PATCH` de la connexion de base avec les valeurs mises à jour pour les paramètres souhaités.

>[!BEGINSHADEBOX]

**Format d’API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Requête**

La requête suivante met à jour les paramètres `accessId` et `secretKey` d’une connexion de destination [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Définit la partie du flux à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion de base et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service], tout en fournissant votre identifiant de connexion de base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Requête**

La requête suivante met à jour les paramètres d’une connexion [[!DNL Azure Blob] destination](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) pour mettre à jour la chaîne de connexion requise pour se connecter à une instance Azure Blob.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| Propriété | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Définit la partie du flux à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion de base et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service], tout en fournissant votre identifiant de connexion de base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Gestion des erreurs d’API {#api-error-handling}

Les points de terminaison d’API de ce tutoriel suivent les principes généraux des messages d’erreur de l’API d’Experience Platform. Pour plus d’informations sur l’interprétation des réponses d’erreur, reportez-vous aux [codes d’état d’API](/help/landing/troubleshooting.md#api-status-codes) et [ erreurs d’en-tête de requête](/help/landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez appris à mettre à jour différents composants d’une connexion de destination à l’aide de l’API [!DNL Flow Service]. Pour plus d’informations sur les destinations, consultez la [présentation des destinations](../home.md).
