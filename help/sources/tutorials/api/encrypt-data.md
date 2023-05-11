---
title: Ingestion de données chiffrées
description: Adobe Experience Platform vous permet d’ingérer des fichiers chiffrés par le biais de sources de lot d’espace de stockage dans le cloud.
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: 8531459da97be648d0a63ffc2af77ce41124585d
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 100%

---

# Ingestion de données chiffrées

Adobe Experience Platform vous permet d’ingérer des fichiers chiffrés par le biais de sources de lot d’espace de stockage dans le cloud. Avec l’ingestion de données chiffrées, vous pouvez utiliser des mécanismes de chiffrement asymétrique pour transférer en toute sécurité des données par lots dans Experience Platform. Actuellement, les mécanismes de chiffrement asymétrique pris en charge sont PGP et GPG.

Le processus d’ingestion des données chiffrées est le suivant :

1. [Créer une paire de clés de chiffrement à l’aide des API d’Experience Platform](#create-encryption-key-pair). La paire de clés de chiffrement se compose d’une clé privée et d’une clé publique. Une fois créée, vous pouvez copier ou télécharger la clé publique, ainsi que son identifiant de clé publique correspondant et sa date d’expiration. Au cours de ce processus, la clé privée sera stockée par Experience Platform dans un coffre sécurisé. **REMARQUE :** la clé publique de la réponse est codée en Base64 et doit être déchiffrée avant utilisation.
2. Utilisez la clé publique pour chiffrer le fichier de données à ingérer.
3. Placez votre fichier chiffré dans votre espace de stockage dans le cloud.
4. Une fois le fichier chiffré prêt, [créez une connexion source et un flux de données pour votre source d’espace de stockage dans le cloud](#create-a-dataflow-for-encrypted-data). Lors de l’étape de création de flux, vous devez fournir un paramètre `encryption` et inclure votre identifiant de clé publique.
5. Experience Platform récupère la clé privée dans le coffre sécurisé pour déchiffrer les données au moment de l’ingestion.

>[!IMPORTANT]
>
>La taille maximale d’un seul fichier chiffré est de 1 Go. Par exemple, vous pouvez ingérer 2 Go de données dans une seule exécution de flux de données. Toutefois, les fichiers individuels dans ces données ne peuvent pas dépasser 1 Go.

Ce document décrit les étapes à suivre pour générer une paire de clés de chiffrement pour vos données et ingérer ces données chiffrées sur Experience Platform à l’aide de sources d’espace de stockage dans le cloud.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform.
   * [Sources d‘espace de stockage dans le cloud](../api/collect/cloud-storage.md) : créez un flux de données pour importer les données par lots de votre source d’espace de stockage dans le cloud vers Experience Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Créer une paire de clés de chiffrement {#create-encryption-key-pair}

La première étape de l’ingestion de données chiffrées sur Experience Platform consiste à créer votre paire de clés de chiffrement en effectuant une requête POST au point d’entrée `/encryption/keys` de l‘API [!DNL Connectors].

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
| `encryptionAlgorithm` | Type d’algorithme de chiffrement que vous utilisez. Les types de chiffrement pris en charge sont `PGP` et `GPG`. |
| `params.passPhrase` | La phrase secrète fournit un niveau supplémentaire de protection pour vos clés de chiffrement. Lors de sa création, Experience Platform stocke la phrase secrète dans un coffre sécurisé différent de celui de la clé publique. Vous devez fournir une chaîne non vide comme phrase secrète. |

**Réponse**

Une réponse réussie renvoie votre clé publique codée en Base64, votre identifiant de clé publique et la date d’expiration de vos clés. La date d’expiration est automatiquement définie sur 180 jours après la date de génération de la clé. La date d’expiration ne peut actuellement pas être configurée.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Connecter votre source d‘espace de stockage dans le cloud à Experience Platform à l’aide de l’API [!DNL Flow Service]

Une fois que vous avez récupéré votre paire de clés de chiffrement, vous pouvez procéder à la création d’une connexion source pour votre source d’espace de stockage dans le cloud et importer vos données chiffrées vers Platform.

Tout d’abord, vous devez créer une connexion de base pour authentifier votre source sur Platform. Pour créer une connexion de base et authentifier votre source, sélectionnez la source que vous souhaitez utiliser dans la liste ci-dessous :

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure File Storage](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud Storage](../api/create/cloud-storage/google.md)
* [Oracle Object Storage](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Après avoir créé une connexion de base, vous devez suivre les étapes décrites dans le tutoriel pour [créer une connexion source pour une source de stockage dans le cloud](../api/collect/cloud-storage.md) afin de créer une connexion source, une connexion cible et un mappage.

## Créer un flux de données pour les données chiffrées {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Afin de créer un flux de données pour l’ingestion de données chiffrée, vous devez disposer des éléments suivants :
>* [Identifiant de clé publique](#create-encryption-key-pair)
>* [Identifiant de connexion source](../api/collect/cloud-storage.md#source)
>* [Identifiant de connexion cible](../api/collect/cloud-storage.md#target)
>* [Identifiant de mappage](../api/collect/cloud-storage.md#mapping)


Pour créer un flux de données, envoyez une requête POST au point d’entrée `/flows` de l’API [!DNL Flow Service]. Pour ingérer des données chiffrées, vous devez ajouter une section `encryption` à la propriété `transformations` et inclure l’`publicKeyId` qui a été créé lors d’une précédente étape.

**Format d’API**

```http
POST /flows
```

**Requête**

La requête suivante crée un flux de données pour ingérer des données chiffrées pour une source d’espace de stockage dans le cloud.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Propriété | Description |
| --- | --- |
| `flowSpec.id` | Identifiant de spécification de flux qui correspond aux sources d’espace de stockage dans le cloud. |
| `sourceConnectionIds` | Identifiant de connexion source. Cet identifiant représente le transfert des données de la source vers Platform. |
| `targetConnectionIds` | Identifiant de connexion cible. Cet identifiant représente l’endroit où les données arrivent une fois qu’elles ont été transférées sur Platform. |
| `transformations[x].params.mappingId` | Identifiant de mappage. |
| `transformations.name` | Lors de l’ingestion de fichiers chiffrés, vous devez fournir `Encryption` comme paramètre de transformations supplémentaire pour votre flux de données. |
| `transformations[x].params.publicKeyId` | Identifiant de clé publique que vous avez créé. Cet identifiant représente la moitié de la paire de clés de chiffrement utilisée pour chiffrer vos données d’espace de stockage dans le cloud. |
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

En suivant ce tutoriel, vous avez créé une paire de clés de chiffrement pour vos données d’espace de stockage dans le cloud et un flux de données pour ingérer vos données chiffrées à l’aide de [!DNL Flow Service API]. Pour connaître les mises à jour de statut sur l’exhaustivité, les erreurs et les mesures de votre flux de données, consultez le guide sur la [surveillance de votre flux de données à l’aide de l’API  [!DNL Flow Service] ](./monitor.md).
