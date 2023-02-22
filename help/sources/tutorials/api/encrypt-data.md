---
title: Ingestion de données chiffrées
description: Adobe Experience Platform vous permet d’ingérer des fichiers chiffrés par le biais de sources par lots de stockage dans le cloud.
hide: true
hidefromtoc: true
source-git-commit: 526c9665843efaeb0e98423dc424a4193434f583
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 21%

---

# Ingestion de données chiffrées

Adobe Experience Platform vous permet d’ingérer des fichiers chiffrés par le biais de sources par lots de stockage dans le cloud. Avec l’ingestion de données chiffrées, vous pouvez utiliser des mécanismes de chiffrement asymétriques pour transférer en toute sécurité des données par lots dans Experience Platform. Actuellement, les mécanismes de cryptage asymétrique pris en charge sont PGP et GPG.

Le processus d’ingestion des données cryptées est le suivant :

1. [Création d’une paire de clés de chiffrement à l’aide des API Experience Platform](#create-encryption-key-pair). La paire de clés de chiffrement se compose d’une clé privée et d’une clé publique. Une fois créée, vous pouvez copier ou télécharger la clé publique, ainsi que son identifiant de clé publique correspondant et l’heure d’expiration. Au cours de ce processus, la clé privée sera stockée par un Experience Platform dans un coffre sécurisé.
2. Utilisez la clé publique pour chiffrer le fichier de données à ingérer.
3. Placez votre fichier chiffré dans votre espace de stockage dans le cloud.
4. Une fois le fichier crypté prêt, [créer une connexion source et un flux de données pour votre source de stockage dans le cloud ;](#create-a-dataflow-for-encrypted-data). Lors de l’étape de création de flux, vous devez fournir un `encryption` et incluez votre ID de clé publique.
5. Experience Platform récupère la clé privée dans le coffre sécurisé pour déchiffrer les données au moment de l’ingestion.

Ce document décrit les étapes à suivre pour générer une paire de clés de chiffrement pour vos données et ingérer ces données chiffrées à Experience Platform à l’aide de sources de stockage dans le cloud.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
   * [Sources de stockage dans le cloud](../api/collect/cloud-storage.md): Créez un flux de données pour importer les données par lots de votre source de stockage dans le cloud vers Experience Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Création d’une paire de clés de chiffrement {#create-encryption-key-pair}

La première étape de l’ingestion de données chiffrées à Experience Platform consiste à créer votre paire de clés de chiffrement en adressant une requête de POST à la variable `/encryption/keys` point d’entrée du [!DNL Connectors] API.

**Format d’API**

```http
POST /data/foundation/connectors/encryption/keys
```

**Requête**

La requête suivante génère une paire de clés de chiffrement à l’aide de l’algorithme de chiffrement PGP.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `encryptionAlgorithm` | Type d’algorithme de chiffrement que vous utilisez. Les types de chiffrement pris en charge sont les suivants : `PGP` et `GPG`. |
| `params.passPhrase` | La phrase secrète fournit une couche supplémentaire de protection pour vos clés de chiffrement. Lors de sa création, Experience Platform stocke la phrase secrète dans un coffre sécurisé différent de la clé publique. Vous devez fournir une chaîne non vide comme mot de passe. |

**Réponse**

Une réponse réussie renvoie votre clé publique, votre identifiant de clé publique et l’heure d’expiration de vos clés. Le délai d’expiration est automatiquement défini sur 180 jours après la date de génération de la clé. L’expiration n’est actuellement pas configurable.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Connectez votre source de stockage dans le cloud à Experience Platform à l’aide du [!DNL Flow Service] API

Une fois que vous avez récupéré votre paire de clés de chiffrement, vous pouvez procéder à la création d’une connexion source pour votre source de stockage dans le cloud et importer vos données chiffrées dans Platform.

Tout d’abord, vous devez créer une connexion de base pour authentifier votre source sur Platform. Pour créer une connexion de base et authentifier votre source, sélectionnez la source que vous souhaitez utiliser dans la liste ci-dessous :

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure File Storage](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud Storage](../api/create/cloud-storage/google.md)
* [Oracle Object Storage](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Après avoir créé une connexion de base, vous devez suivre les étapes décrites dans le tutoriel pour [création d’une connexion source pour une source de stockage dans le cloud](../api/collect/cloud-storage.md) pour créer une connexion source, une connexion cible et un mapping.

## Création d’un flux de données pour les données chiffrées {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Pour créer un flux de données pour l’ingestion de données chiffrée, vous devez disposer des éléments suivants :
>* [Identifiant de clé publique](#create-encryption-key-pair)
>* [ID de connexion source](../api/collect/cloud-storage.md#source)
>* [ID de connexion cible](../api/collect/cloud-storage.md#target)
>* [Identifiant de mappage](../api/collect/cloud-storage.md#mapping)


Pour créer un flux de données, envoyez une requête de POST à la fonction `/flows` point d’entrée du [!DNL Flow Service] API. Pour ingérer des données chiffrées, vous devez ajouter une `encryption` à la section `transformations` et incluez la propriété `publicKeyId` qui a été créé à une étape précédente.

**Format d’API**

```http
POST /flows
```

**Requête**

La requête suivante crée un flux de données pour ingérer des données chiffrées pour une source de stockage dans le cloud.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Customer Data",
      "description: "ACME encrypted data ingestion",
      "flowSpec": {
          "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "26b53912-1005-49f0-b539-12100559f0e2"
      ],
      "targetConnectionIds": [
        "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                  "mappingVersion": 0
              }
          },
          {
              "name": "Encryption",
              "params": {
                  "publicKeyId": 512e686e-543e-4354-bcba-e1403ddcc532
          }
  }
      ],
      "scheduleParams": {
          "startTime": "1597784298",
          "frequency": "once"
      }
  }'
```

| Propriété | Description |
| --- | --- |
| `flowSpec.id` | Identifiant de spécification de flux qui correspond aux sources de stockage dans le cloud. |
| `sourceConnectionIds` | L’identifiant de connexion source. Cet identifiant représente le transfert des données de la source vers Platform. |
| `targetConnectionIds` | Identifiant de connexion cible. Cet identifiant représente l’endroit où les données arrivent une fois qu’elles ont été transférées à Platform. |
| `transformations[x].params.mappingId` | Identifiant du mappage. |
| `transformations.name` | Lors de l’ingestion de fichiers chiffrés, vous devez fournir `Encryption` comme paramètre de transformations supplémentaire pour votre flux de données. |
| `transformations[x].params.publicKeyId` | ID de clé publique que vous avez créé. Cet identifiant représente la moitié de la paire de clés de chiffrement utilisée pour chiffrer vos données de stockage dans le cloud. |
| `scheduleParams.startTime` | Heure de début du flux de données en temps Unix. |
| `scheduleParams.frequency` | Fréquence de collecte des données par le flux de données. Les valeurs possibles sont les suivantes : `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un nombre entier non nul. L’intervalle n’est pas requis lorsque la fréquence est définie sur `once` et doit être supérieur ou égal à `15` pour d’autres valeurs de fréquence. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du nouveau flux de données créé pour vos données chiffrées.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez créé une paire de clés de chiffrement pour vos données de stockage dans le cloud et un flux de données pour ingérer vos données chiffrées à l’aide de la variable [!DNL Flow Service API]. Pour connaître les mises à jour d’état de l’exhaustivité, des erreurs et des mesures de votre flux de données, consultez le guide sur [surveillance de votre flux de données à l’aide de la fonction [!DNL Flow Service] API](./monitor.md).