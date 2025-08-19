---
title: Présentation du connecteur Source Azure Blob
description: Découvrez comment connecter votre compte Azure Blob à Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: f659d78eebc1c5e74021f9a41a2a489389a6588e
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 21%

---

# Source [!DNL Azure Blob Storage]

[!DNL Azure Blob Storage] est un service de stockage d’objets basé sur le cloud fourni par [!DNL Microsoft Azure]. Il est conçu pour stocker de grandes quantités de données non structurées, telles que du texte, des images, des vidéos, des sauvegardes et des journaux. Vous pouvez utiliser [!DNL Azure Blob Storage] pour stocker et gérer de grandes quantités de données non structurées telles que des documents, des images, des vidéos et des fichiers audio. Il est idéal pour la sauvegarde et l’archivage des données, la reprise après sinistre et la gestion des charges de travail Big Data pour les analyses.

Utilisez la source de [!DNL Azure Blob Storage] pour connecter votre compte et ingérer des données de [!DNL Azure Blob Storage] vers Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Lisez les sections suivantes pour terminer la configuration requise avant de connecter votre compte [!DNL Azure Blob Storage] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>La source [!DNL Azure Blob] ne prend pas en charge la connectivité de la même région à Experience Platform. Si votre instance [!DNL Azure] utilise la même région réseau qu’Experience Platform, il n’est pas possible d’établir une connexion aux sources Experience Platform. Actuellement, seule la connectivité inter-régions est prise en charge.

### Contraintes de dénomination pour fichiers et répertoires

La liste suivante inclut les contraintes dont vous devez tenir compte lorsque vous nommez votre fichier ou répertoire de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (0x00 à 0x1F, \u0081, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

### Authentification du [!DNL Azure Blob Storage] à Experience Platform {#authentication}

Vous pouvez connecter votre compte [!DNL Azure Blob Storage] à Experience Platform à l’aide des types d’authentification suivants :

- **Authentification de la clé de compte** : utilise la clé d’accès du compte de stockage pour s’authentifier et se connecter à votre compte [!DNL Azure Blob Storage].
- **Signature d’accès partagé (SAS)** : utilise un URI SAS pour fournir un accès délégué et limité dans le temps aux ressources de votre compte [!DNL Azure Blob Storage].
- **Authentification basée sur le principal de service** : utilise un principal de service Azure Active Directory (AAD) (identifiant client et secret) pour s’authentifier en toute sécurité sur votre compte de stockage Blob Azure.

>[!BEGINTABS]

>[!TAB Authentification de la clé de compte]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre compte [!DNL Azure Blob Storage] à Experience Platform à l’aide de l’authentification par clé de compte.

| Informations d’identification | Description |
| --- | --- |
| `connectionString` | Chaîne de connexion [!DNL Azure Blob Storage] pour votre compte de stockage. Cette chaîne contient les informations requises pour s’authentifier et se connecter à votre instance [!DNL Azure Blob Storage]. Exemple de format : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | Nom du conteneur de [!DNL Azure Blob Storage] dans lequel vos fichiers de données sont stockés. Un conteneur organise un ensemble d’objets Blob, comme un répertoire dans un système de fichiers. |
| `folderPath` | Chemin d’accès dans le conteneur spécifié où se trouvent vos fichiers. Il s’agit d’un chemin de sous-répertoire facultatif (dossier virtuel) à l’intérieur du conteneur. Si rien n’est indiqué, la racine du conteneur est utilisée. |
| `connectionSpec.id` | L’identifiant de spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Azure Blob Storage] est `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour en savoir plus sur l’utilisation de l’authentification par clé de compte avec [!DNL Azure Blob Storage], lisez le [guide d’authentification Azure Microsoft officiel](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication).

>[!TAB Signature d’accès partagé]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre compte [!DNL Azure Blob Storage] à Experience Platform à l’aide de la signature d’accès partagé.

| Informations d’identification | Description |
| --- | --- |
| `SasURI` | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre compte. Le modèle URI SAS est le suivant : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. Pour plus d’informations, consultez ce document [!DNL Azure] sur les [URI de signature d’accès partagé](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Nom du conteneur de [!DNL Azure Blob Storage] dans lequel vos fichiers de données sont stockés. Un conteneur organise un ensemble d’objets Blob, comme un répertoire dans un système de fichiers. |
| `folderPath` | Chemin d’accès dans le conteneur spécifié où se trouvent vos fichiers. Il s’agit d’un chemin de sous-répertoire facultatif (dossier virtuel) à l’intérieur du conteneur. Si rien n’est indiqué, la racine du conteneur est utilisée. |
| `connectionSpec.id` | L’identifiant de spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Azure Blob Storage] est `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour en savoir plus sur l’utilisation de la signature d’accès partagé avec [!DNL Azure Blob Storage], lisez le [guide d’authentification Azure Microsoft officiel](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).

>[!TAB Authentification basée sur le principal de service]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre compte [!DNL Azure Blob Storage] à Experience Platform à l’aide de l’authentification principale du service.

| Informations d’identification | Description |
| --- | --- |
| `serviceEndpoint` | URL du point d’entrée de votre compte [!DNL Azure Blob Storage]. Généralement au format : `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `accountKind` | Type de votre compte [!DNL Azure Blob Storage]. Les valeurs courantes comprennent `StorageV2`, `BlobStorage` ou `Storage`. |
| `servicePrincipalId` | Identifiant client/d’application du principal de service Azure Active Directory (AAD) utilisé pour l’authentification. |
| `servicePrincipalKey` | Secret client ou mot de passe associé au principal de service Azure. |
| `tenant` | L’identifiant du client Azure Active Directory (AAD) où le principal de service est enregistré. |
| `container` | Nom du conteneur de stockage Blob Azure où vos fichiers de données sont stockés. |
| `folderPath` | Chemin d’accès dans le conteneur spécifié où se trouvent vos fichiers. Il s’agit d’un chemin de sous-répertoire facultatif (dossier virtuel) à l’intérieur du conteneur. Si rien n’est indiqué, la racine du conteneur est utilisée. |
| `connectionSpec.id` | L’identifiant de spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour le stockage Azure Blob est `4c10e202-c428-4796-9208-5f1f5732b1cf`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour en savoir plus sur l’utilisation de l’authentification basée sur le principal de service avec [!DNL Azure Blob Storage], lisez le [guide d’authentification Azure Microsoft officiel](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication).

>[!ENDTABS]

## Connexion de [!DNL Azure Blob Storage] à [!DNL Experience Platform]

La documentation ci-dessous fournit des informations sur la connexion d’Azure Blob à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Utiliser les API

- [Connexion  [!DNL Azure Blob Storage]  Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [Explorer la structure de données et le contenu d’une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Créer un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utiliser l’interface utilisateur

- [Connexion  [!DNL Azure Blob Storage]  Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [Créer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)
