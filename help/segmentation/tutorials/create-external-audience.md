---
title: Création et activation d’une audience externe
type: Tutorial
description: Découvrez comment créer une audience externe dans Adobe Experience Platform à l’aide des API Experience Platform.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 7%

---


# Créer et activer une audience externe à l’aide de l’API

Ce tutoriel décrit les étapes requises pour créer une audience externe à l’aide des API Adobe Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension pratique des différents services Experience Platform impliqués dans la création d’une audience externe. Avant de commencer ce tutoriel, veuillez lire la documentation relative aux services suivants :

- [Sources](../../sources/home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md) : permet de créer des audiences à partir des données externes.
- [Destinations](../../destinations/home.md) : les destinations sont des intégrations préconfigurées aux applications couramment utilisées. Elles permettent l’activation transparente des données d’Experience Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée, etc.

### En-têtes requis

Ce tutoriel nécessite également que vous ayez suivi le [&#x200B; tutoriel sur l’authentification &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour passer avec succès des appels aux API [!DNL Experience Platform]. Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Les requêtes [!DNL Experience Platform] API nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes POST, PUT et PATCH requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Préparation de l’audience externe {#prepare}

Avant de pouvoir créer une audience externe dans Experience Platform, vous devez préparer un fichier contenant les données de l’audience.

Pour cet exemple, vous devez utiliser un fichier CSV. Assurez-vous que votre fichier CSV contient **au moins** une colonne avec une valeur d’identité telle qu’un ECID, un ID d’e-mail ou un ID de gestion de la relation client. En outre, assurez-vous que contient tous les attributs d’enrichissement dont vous aurez besoin pour la segmentation et l’activation.

Vous devez également vous assurer que le fichier est conforme aux exigences de votre schéma Experience Platform. Pour plus d’informations sur la création d’un schéma, consultez le [tutoriel sur la création d’un schéma à l’aide de l’API](/help/xdm/tutorials/create-schema-api.md) ou le [tutoriel sur la création d’un schéma à l’aide de l’interface utilisateur](/help/xdm/tutorials/create-schema-ui.md).

Une fois que vous avez confirmé que votre fichier CSV contient toutes les informations dont vous avez besoin et est conforme au schéma, vous devez charger le fichier CSV vers votre fournisseur de stockage dans le cloud afin de pouvoir utiliser des sources pour ingérer les données dans Experience Platform. Pour plus d’informations sur l’utilisation d’une source de stockage dans le cloud, consultez le [tutoriel sur l’exploration des options de stockage dans le cloud à l’aide de l’API](/help/sources/tutorials/api/explore/cloud-storage.md) ou la [présentation des sources](/help/sources/home.md#cloud-storage).

## Création d’une audience externe {#create}

Après avoir préparé votre fichier CSV, vous pouvez maintenant lancer le processus de création de l’audience externe.

Vous pouvez créer une audience externe en effectuant une requête POST vers le point d’entrée `/external-audience/`.

Lors de l’exécution de cette requête, vous devez spécifier les informations suivantes :

- Nom de l’audience
- Une description pour l’audience
- Les champs correspondants entre le fichier CSV et le schéma
- Informations sur la spécification de source
   - Cela inclut le chemin d’accès au fichier CSV pour l’ingestion
      - Le chemin d’accès au fichier **ne peut pas** contenir d’espaces. Par exemple, si votre chemin d’accès est `activation/sample-source/Example CSV File.csv`, définissez-le sur `activation/sample-source/ExampleCSVFile.csv`.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le guide [guide des points d’entrée des audiences externes](/help/segmentation/api/external-audiences.md#create-audience).

+++Requête

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

Après avoir effectué cette requête, veillez à noter les `operationId` que vous recevez de la réponse afin de pouvoir récupérer l’identifiant d’audience.

## Récupérer l’ID d’audience {#retrieve-audience-id}

Maintenant que vous avez créé l’audience externe, vous devez obtenir l’identifiant de l’audience afin de pouvoir ingérer l’audience dans Experience Platform.

Vous pouvez récupérer l’identifiant de l’audience en adressant une requête GET au point d’entrée `/external-audiences/operations` et en fournissant l’identifiant de l’opération que vous avez précédemment reçue de la réponse de création d’audience externe.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le guide [guide des points d’entrée des audiences externes](/help/segmentation/api/external-audiences.md#retrieve-status).

+++ Requête

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Après avoir effectué cette requête, veillez à noter les `audienceId` que vous recevez de la réponse afin de pouvoir déclencher la tâche d’ingestion pour l’audience.

## Démarrer l’ingestion de l’audience {#start-ingestion}

Puisque vous disposez de vos `audienceId`, vous pouvez désormais déclencher l’ingestion de votre audience externe dans Experience Platform.

Vous pouvez démarrer une ingestion d’audience en adressant une requête POST au point d’entrée suivant tout en fournissant l’identifiant d’audience. De plus, vous devrez spécifier l’heure de début pour déterminer les fichiers qui seront traités.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le guide [guide des points d’entrée des audiences externes](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ Requête

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

Après avoir effectué cette requête, veillez à noter les `runId` que vous recevez de la réponse afin de pouvoir surveiller le statut de l’ingestion.

## Surveillance du statut d’ingestion {#monitor-ingestion}

Une fois que vous avez déclenché l’ingestion de l’audience, vous pouvez surveiller la progression de l’ingestion pour confirmer la réussite de l’ingestion et valider la disponibilité de l’audience pour l’activation en aval.

Vous pouvez récupérer le statut d’une ingestion d’audience en adressant une requête GET au point d’entrée suivant tout en fournissant les identifiants d’audience et d’exécution.

Pour plus d’informations sur l’utilisation de ce point d’entrée, consultez le guide [guide des points d’entrée des audiences externes](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status).

+++ Requête

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## Étapes suivantes {#next-steps}

>[!IMPORTANT]
>
>Pour utiliser l’audience générée en externe, vous **devez** attendre que la tâche de segmentation quotidienne soit terminée.

Une fois que vous avez confirmé que l’audience externe a bien été ingérée, vous pouvez la voir dans Audience Portal et l’utiliser dans les services en aval tels que les destinations.

Pour plus d’informations sur Audience Portal, consultez le [Guide de l’interface utilisateur d’Audience Portal](/help/segmentation/ui/audience-portal.md). Pour plus d’informations sur les destinations, consultez la [présentation des destinations](/help/destinations/home.md).

