---
title: Azure Databricks
description: Découvrez les étapes préalables requises pour connecter Azure Databricks à Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 0c8ff1029beee3f58cbf536b11b40551b6f6c2ed
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 3%

---

# [!DNL Azure Databricks]

>[!AVAILABILITY]
>
>* La source [!DNL Azure Databricks] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>* La source [!DNL Azure Databricks] est en version Beta. Lisez les [ termes et conditions ](../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL Azure Databricks] est une plateforme cloud conçue pour l’analyse de données, le machine learning et l’IA. Vous pouvez utiliser [!DNL Databricks] pour intégrer à [!DNL Azure] et fournir un environnement holistique pour créer, déployer et gérer des solutions de données à grande échelle.

Utilisez la source de [!DNL Databricks] pour connecter votre compte et ingérer vos données [!DNL Databricks] vers Adobe Experience Platform.

## Prérequis

Suivez les étapes préalables requises pour connecter votre compte [!DNL Databricks] à Experience Platform.

### Récupérer les informations d’identification du conteneur

Récupérez vos informations d’identification Experience Platform [!DNL Azure Blob Storage] pour permettre à votre compte [!DNL Databricks] d’y accéder ultérieurement.

Pour récupérer vos informations d’identification, envoyez une requête GET au point d’entrée `/credentials` de l’API [!DNL Connectors].

**Format d’API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**Requête**

La requête suivante récupère les informations d’identification de votre [!DNL Azure Blob Storage] Experience Platform.

+++Afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie fournit vos informations d’identification (`containerName`, `SASToken`, `storageAccountName`) pour une utilisation ultérieure dans [!DNL Apache Spark] configuration pour les [!DNL Databricks].

+++Afficher l’exemple de réponse

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Nom de votre conteneur [!DNL Azure Blob Storage]. Vous utiliserez cette valeur ultérieurement lors de la configuration de votre [!DNL Apache Spark] pour [!DNL Databricks]. |
| `SASToken` | Jeton de signature d’accès partagé pour votre [!DNL Azure Blob Storage]. Cette chaîne contient toutes les informations nécessaires pour autoriser une requête. |
| `storageAccountName` | Nom de votre compte de stockage. |
| `SASUri` | URI de signature d’accès partagé pour votre [!DNL Azure Blob Storage]. Cette chaîne est une combinaison de l’URI du [!DNL Azure Blob Storage] auquel vous êtes authentifié et de son jeton SAS correspondant. |
| `expiryDate` | Date d’expiration de votre jeton SAS. Vous devez actualiser votre jeton avant la date d’expiration pour continuer à l’utiliser dans votre application pour charger des données vers le [!DNL Azure Blob Storage]. Si vous n’actualisez pas manuellement votre jeton avant la date d’expiration indiquée, il s’actualisera automatiquement et fournira un nouveau jeton lorsque l’appel des informations d’identification GET sera effectué. |

+++

### Actualiser vos informations d’identification

>[!NOTE]
>
>Vos informations d’identification existantes seront révoquées une fois que vous les aurez actualisées. Par conséquent, vous devez mettre à jour vos configurations [!DNL Spark] en conséquence chaque fois que vous actualisez vos informations d’identification de stockage. Sinon, votre flux de données échouera.

Pour actualiser vos informations d’identification, envoyez une requête POST et incluez `action=refresh` comme paramètre de requête.

**Format d’API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**Requête**

La requête suivante actualise les informations d’identification de votre [!DNL Azure Blob Storage].

+++Afficher l’exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Réponse**

Une réponse réussie renvoie vos nouvelles informations d’identification.

+++Afficher l’exemple de réponse

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### Configuration de l’accès à votre [!DNL Azure Blob Storage]

>[!IMPORTANT]
>
>* Si votre cluster a été arrêté, le service le redémarre automatiquement au cours d’une exécution de flux. Cependant, vous devez vous assurer que votre cluster est actif lors de la création d’une connexion ou d’un flux de données. En outre, votre cluster doit être actif si vous effectuez des actions telles que l’aperçu ou l’exploration des données, car ces actions ne peuvent pas inciter au redémarrage automatique d’un cluster arrêté.
>
>* Votre conteneur [!DNL Azure] comprend un dossier nommé `adobe-managed-staging`. Pour garantir une ingestion transparente des données, **ne modifiez pas** ce dossier.


Ensuite, vous devez vous assurer que votre cluster [!DNL Databricks] a accès au compte [!DNL Azure Blob Storage] Experience Platform. Ce faisant, vous pouvez utiliser [!DNL Azure Blob Storage] comme emplacement intermédiaire pour l’écriture de données de tableau [!DNL delta lake].

Pour fournir l’accès, vous devez configurer un jeton SAS sur le cluster [!DNL Databricks] dans le cadre de votre configuration [!DNL Apache Spark].

Dans l’interface [!DNL Databricks], sélectionnez **[!DNL Advanced options]**, puis saisissez ce qui suit dans la zone de saisie [!DNL Spark config].

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| Propriété | Description |
| --- | --- |
| Nom du conteneur | Nom de votre conteneur. Vous pouvez obtenir cette valeur en récupérant vos informations d’identification [!DNL Azure Blob Storage]. |
| Compte d’enregistrement | Nom de votre compte de stockage. Vous pouvez obtenir cette valeur en récupérant vos informations d’identification [!DNL Azure Blob Storage]. |
| Jeton SAS | Jeton de signature d’accès partagé pour votre [!DNL Azure Blob Storage]. Vous pouvez obtenir cette valeur en récupérant vos informations d’identification [!DNL Azure Blob Storage]. |

![Interface utilisateur des briques de données sur Azure.](../../images/tutorials/create/databricks/databricks-ui.png)

## Connexion de [!DNL Databricks] à Experience Platform à l’aide d’API

Maintenant que vous avez terminé les étapes préalables requises, vous pouvez passer au guide sur la [connexion de votre compte  [!DNL Databricks]  Experience Platform à l’aide de l’API](../../tutorials/api/create/databases/databricks.md).
