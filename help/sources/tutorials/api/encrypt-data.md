---
title: Ingestion de données chiffrées
description: Découvrez comment ingérer des fichiers chiffrés par le biais de sources de lots d’espaces de stockage à l’aide de l’API.
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 63%

---

# Ingestion de données chiffrées

Vous pouvez ingérer des fichiers de données chiffrés vers Adobe Experience Platform à l’aide de sources de lots de stockage dans le cloud. Avec l’ingestion de données chiffrées, vous pouvez utiliser des mécanismes de chiffrement asymétrique pour transférer en toute sécurité des données par lots dans Experience Platform. Actuellement, les mécanismes de chiffrement asymétrique pris en charge sont PGP et GPG.

Le processus d’ingestion des données chiffrées est le suivant :

1. [Créer une paire de clés de chiffrement à l’aide des API d’Experience Platform](#create-encryption-key-pair). La paire de clés de chiffrement se compose d’une clé privée et d’une clé publique. Une fois créée, vous pouvez copier ou télécharger la clé publique, ainsi que son identifiant de clé publique correspondant et sa date d’expiration. Au cours de ce processus, la clé privée sera stockée par Experience Platform dans un coffre sécurisé. **REMARQUE :** la clé publique de la réponse est codée en Base64 et doit être décodée avant utilisation.
2. Utilisez la clé publique pour chiffrer le fichier de données à ingérer.
3. Placez votre fichier chiffré dans votre espace de stockage dans le cloud.
4. Une fois le fichier chiffré prêt, [créez une connexion source et un flux de données pour votre source d’espace de stockage dans le cloud](#create-a-dataflow-for-encrypted-data). Lors de l’étape de création de flux, vous devez fournir un paramètre `encryption` et inclure votre identifiant de clé publique.
5. Experience Platform récupère la clé privée dans le coffre sécurisé pour déchiffrer les données au moment de l’ingestion.

>[!IMPORTANT]
>
>La taille maximale d’un seul fichier chiffré est de 1 Go. Par exemple, vous pouvez ingérer 2 Go de données dans une seule exécution de flux de données. Toutefois, les fichiers individuels dans ces données ne peuvent pas dépasser 1 Go.

Ce document décrit les étapes à suivre pour générer une paire de clés de chiffrement pour vos données et ingérer ces données chiffrées sur Experience Platform à l’aide de sources d’espace de stockage dans le cloud.

## Commencer {#get-started}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
   * [Sources d‘espace de stockage dans le cloud](../api/collect/cloud-storage.md) : créez un flux de données pour importer les données par lots de votre source d’espace de stockage dans le cloud vers Experience Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../landing/api-guide.md).

### Extensions de fichiers prises en charge pour les fichiers chiffrés {#supported-file-extensions-for-encrypted-files}

La liste des extensions de fichier prises en charge pour les fichiers chiffrés est la suivante :

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>L’ingestion de fichiers chiffrés dans les sources d’Adobe Experience Platform prend en charge openPGP et non pas une version propriétaire spécifique de PGP.

## Créer une paire de clés de chiffrement {#create-encryption-key-pair}

>[!IMPORTANT]
>
>Les clés de chiffrement sont spécifiques à un sandbox donné. Par conséquent, vous devez créer des clés de chiffrement si vous souhaitez ingérer des données chiffrées dans un autre sandbox, au sein de votre organisation.

La première étape de l’ingestion de données chiffrées sur Experience Platform consiste à créer votre paire de clés de chiffrement en effectuant une requête POST au point d’entrée `/encryption/keys` de l‘API [!DNL Connectors].

**Format d’API**

```http
POST /data/foundation/connectors/encryption/keys
```

**Requête**

+++Afficher un exemple de requête

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
      "name": "acme-encryption",
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Paramètre | Description |
| --- | --- |
| `name` | Nom de votre paire de clés de chiffrement. |
| `encryptionAlgorithm` | Type d’algorithme de chiffrement que vous utilisez. Les types de chiffrement pris en charge sont `PGP` et `GPG`. |
| `params.passPhrase` | La phrase secrète fournit un niveau supplémentaire de protection pour vos clés de chiffrement. Lors de sa création, Experience Platform stocke la phrase secrète dans un coffre sécurisé différent de celui de la clé publique. Vous devez fournir une chaîne non vide comme phrase secrète. |

+++

**Réponse**

+++Afficher l’exemple de réponse

Une réponse réussie renvoie votre clé publique codée en Base64, votre identifiant de clé publique et la date d’expiration de vos clés. La date d’expiration est automatiquement définie sur 180 jours après la date de génération de la clé. La date d’expiration ne peut actuellement pas être configurée.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| Propriété | Description |
| --- | --- |
| `publicKey` | La clé publique permet de chiffrer les données dans votre espace de stockage. Cette clé correspond à la clé privée, qui a également été créée lors de cette étape. Cependant, la clé privée est immédiatement envoyée à Experience Platform. |
| `publicKeyId` | L’identifiant de clé publique permet de créer un flux de données et d’ingérer les données chiffrées provenant de votre espace de stockage dans Experience Platform. |
| `expiryTime` | Le délai d’expiration définit la date d’expiration de votre paire de clés de chiffrement. Cette date est automatiquement définie sur 180 jours après la date de génération de la clé et s’affiche au format de date et heure UNIX. |

+++

### Récupération des clés de chiffrement {#retrieve-encryption-keys}

Pour récupérer toutes les clés de chiffrement de votre organisation, envoyez une requête GET au point d’entrée `/encryption/keys`=nt.

**Format d’API**

```http
GET /data/foundation/connectors/encryption/keys
```

**Requête**

+++Afficher un exemple de requête

La requête suivante récupère toutes les clés de chiffrement de votre organisation.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Réponse**

+++Afficher l’exemple de réponse

Une réponse réussie renvoie l’algorithme de chiffrement, le nom, la clé publique, l’ID de clé publique, le type de clé et l’heure d’expiration correspondante de vos clés.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Récupération des clés de chiffrement par ID {#retrieve-encryption-keys-by-id}

Pour récupérer un ensemble spécifique de clés de chiffrement, envoyez une requête GET au point d’entrée `/encryption/keys` et indiquez votre identifiant de clé publique comme paramètre d’en-tête.

**Format d’API**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Requête**

+++Afficher un exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Réponse**

+++Afficher l’exemple de réponse

Une réponse réussie renvoie l’algorithme de chiffrement, le nom, la clé publique, l’ID de clé publique, le type de clé et l’heure d’expiration correspondante de vos clés.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "name": "{NAME}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "keyType": "{KEY_TYPE}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Créer une paire de clés gérée par le client ou la cliente {#create-customer-managed-key-pair}

Si vous le souhaitez, vous pouvez créer une paire de clés de vérification de signature pour signer et ingérer vos données chiffrées.

Pendant cette étape, vous devez générer votre propre combinaison de clé privée et de clé publique, puis utiliser votre clé privée pour signer vos données chiffrées. Ensuite, vous devez coder votre clé publique en Base64, puis la partager avec Experience Platform pour qu’Experience Platform vérifie votre signature.

### Partager votre clé publique avec Experience Platform

Pour partager votre clé publique, envoyez une requête POST au point d’entée `/customer-keys` en spécifiant l’algorithme de chiffrement et la clé publique codée au format Base64.

**Format d’API**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Requête**

+++Afficher un exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "name": "acme-sign-verification-keys"
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}},
      "params": {
          "passPhrase": {{PASS_PHRASE}}
      }
    }'
```

| Paramètre | Description |
| --- | --- |
| `encryptionAlgorithm` | Type d’algorithme de chiffrement que vous utilisez. Les types de chiffrement pris en charge sont `PGP` et `GPG`. |
| `publicKey` | La clé publique qui correspond aux clés gérées par le client ou la cliente utilisées pour signer vos données chiffrées. Cette clé doit être codée au format Base64. |

+++

**Réponse**

+++Afficher l’exemple de réponse

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Propriété | Description |
| --- | --- |
| `publicKeyId` | Cet identifiant de clé publique est renvoyé en réponse au partage de votre clé gérée par le client ou la cliente avec Experience Platform. Vous pouvez fournir cet ID de clé publique comme ID de clé de vérification de signature lors de la création d’un flux de données pour les données signées et chiffrées. |

+++

### Récupérer une paire de clés gérée par le client

Pour récupérer vos clés gérées par le client, envoyez une requête GET au point d’entrée `/customer-keys`.

**Format d’API**

```http
GET /data/foundation/connectors/encryption/customer-keys
```

**Requête**

+++Afficher un exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Réponse**

+++Afficher l’exemple de réponse

```json
[
    {
        "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
        "name": "{NAME}",
        "publicKeyId": "{PUBLIC_KEY_ID}",
        "publicKey": "{PUBLIC_KEY}",
        "keyType": "{KEY_TYPE}",
    }
]
```

+++

## Connecter votre source d‘espace de stockage dans le cloud à Experience Platform à l’aide de l’API [!DNL Flow Service]

Une fois que vous avez récupéré votre paire de clés de chiffrement, vous pouvez procéder à la création d’une connexion source pour votre source d’espace de stockage dans le cloud et importer vos données chiffrées dans Experience Platform.

Tout d’abord, vous devez créer une connexion de base pour authentifier votre source sur Experience Platform. Pour créer une connexion de base et authentifier votre source, sélectionnez la source que vous souhaitez utiliser dans la liste ci-dessous :

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
>
>* [Identifiant de clé publique](#create-encryption-key-pair)
>* [Identifiant de connexion source](../api/collect/cloud-storage.md#source)
>* [Identifiant de connexion cible](../api/collect/cloud-storage.md#target)
>* [Identifiant de mappage](../api/collect/cloud-storage.md#mapping)

Pour créer un flux de données, envoyez une requête POST au point d’entrée `/flows` de l’API [!DNL Flow Service]. Pour ingérer des données chiffrées, vous devez ajouter une section `encryption` à la propriété `transformations` et inclure l’`publicKeyId` qui a été créé lors d’une précédente étape.

**Format d’API**

```http
POST /flows
```

>[!BEGINTABS]

>[!TAB Créer un flux de données pour l’ingestion de données chiffrées]

**Requête**

+++Afficher un exemple de requête

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
| `sourceConnectionIds` | Identifiant de connexion source. Cet identifiant représente le transfert des données de la source vers Experience Platform. |
| `targetConnectionIds` | Identifiant de connexion cible. Cet identifiant représente l’endroit où les données arrivent une fois qu’elles ont été transférées vers Experience Platform. |
| `transformations[x].params.mappingId` | Identifiant de mappage. |
| `transformations.name` | Lors de l’ingestion de fichiers chiffrés, vous devez fournir `Encryption` comme paramètre de transformations supplémentaire pour votre flux de données. |
| `transformations[x].params.publicKeyId` | Identifiant de clé publique que vous avez créé. Cet identifiant représente la moitié de la paire de clés de chiffrement utilisée pour chiffrer vos données d’espace de stockage dans le cloud. |
| `scheduleParams.startTime` | Heure de début du flux de données en temps Unix. |
| `scheduleParams.frequency` | Fréquence de collecte des données par le flux de données. Les valeurs possibles sont les suivantes : `once`, `minute`, `hour`, `day` ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un nombre entier non nul. L’intervalle n’est pas requis lorsque la fréquence est définie sur `once` et doit être supérieur ou égal à `15` pour d’autres valeurs de fréquence. |

+++

**Réponse**

+++Afficher l’exemple de réponse

Une réponse réussie renvoie l’identifiant (`id`) du nouveau flux de données créé pour vos données chiffrées.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB Créer un flux de données pour ingérer des données chiffrées et signées]

**Requête**

+++Afficher un exemple de requête

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
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
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
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
| `params.signVerificationKeyId` | L’identifiant de clé de vérification de signature est identique à l’identifiant de clé publique récupéré après le partage de votre clé publique encodée en Base64 avec Experience Platform. |

+++

**Réponse**

+++Afficher l’exemple de réponse

Une réponse réussie renvoie l’identifiant (`id`) du nouveau flux de données créé pour vos données chiffrées.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### Supprimer les clés de chiffrement {#delete-encryption-keys}

Pour supprimer vos clés de chiffrement, envoyez une requête DELETE au point d’entrée `/encryption/keys` et indiquez votre identifiant de clé publique comme paramètre d’en-tête.

**Format d’API**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Requête**

+++Afficher un exemple de requête

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

### Validation des clés de chiffrement {#validate-encryption-keys}

Pour valider vos clés de chiffrement, envoyez une requête GET au point d’entrée `/encryption/keys/validate/` et indiquez l’identifiant de clé publique à valider comme paramètre d’en-tête.

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**Requête**

+++Afficher un exemple de requête

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Réponse**

Une réponse réussie renvoie une confirmation que vos identifiants sont valides ou non valides.

>[!BEGINTABS]

>[!TAB Valide]

Un ID de clé publique valide renvoie un statut de `Active` avec votre ID de clé publique.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB Non valide]

Un ID de clé publique non valide renvoie un statut de `Expired` avec votre ID de clé publique.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## Restrictions relatives à l’ingestion récurrente {#restrictions-on-recurring-ingestion}

L’ingestion de données chiffrées ne prend pas en charge l’ingestion de dossiers récurrents ou à plusieurs niveaux dans les sources. Tous les fichiers chiffrés doivent être contenus dans un seul dossier. Les caractères génériques avec plusieurs dossiers dans un seul chemin source ne sont pas non plus pris en charge.

Voici un exemple de structure de dossiers prise en charge, où le chemin d’accès source est `/ACME-customers/*.csv.gpg`.

Dans ce scénario, les fichiers en gras sont ingérés dans Experience Platform.

* ACME-customers
   * **Fichier1.csv.gpg**
   * File2.json.gpg
   * **Fichier3.csv.gpg**
   * File4.json
   * **Fichier5.csv.gpg**

Voici un exemple de structure de dossiers non prise en charge dans laquelle le chemin d’accès source est `/ACME-customers/*`.

Dans ce scénario, l’exécution du flux échoue et renvoie un message d’erreur indiquant que les données ne peuvent pas être copiées à partir de la source.

* ACME-customers
   * File1.csv.gpg
   * File2.json.gpg
   * Sous-dossier1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* ACME-loyalty
   * File6.csv.gpg


## Étapes suivantes

En suivant ce tutoriel, vous avez créé une paire de clés de chiffrement pour vos données d’espace de stockage dans le cloud et un flux de données pour ingérer vos données chiffrées à l’aide de [!DNL Flow Service API]. Pour connaître les mises à jour de statut sur l’exhaustivité, les erreurs et les mesures de votre flux de données, consultez le guide sur la [surveillance de votre flux de données à l’aide de l’API [!DNL Flow Service] ](./monitor.md).