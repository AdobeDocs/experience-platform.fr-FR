---
title: Ingestion de données chiffrées dans l’interface utilisateur de sources Workspace
description: Découvrez comment ingérer des données chiffrées dans l’espace de travail de l’interface utilisateur des sources.
badge: Version bêta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 18%

---

# Ingestion de données chiffrées dans l’interface utilisateur des sources

>[!AVAILABILITY]
>
>La prise en charge de l’ingestion de données chiffrées dans l’interface utilisateur des sources est en version bêta et peut ne pas être disponible pour votre entreprise. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

Vous pouvez ingérer des fichiers de données et des dossiers chiffrés dans Adobe Experience Platform à l’aide de sources par lots de stockage dans le cloud. Avec l’ingestion de données chiffrées, vous pouvez utiliser des mécanismes de chiffrement asymétrique pour transférer en toute sécurité des données par lots dans Experience Platform. Actuellement, les mécanismes de chiffrement asymétrique pris en charge sont PGP et GPG.

Cette fonctionnalité est disponible pour les sources suivantes :

* [Amazon S3]
* [Azure Blob]
* [Azure Data Lake Storage Gen2]
* [Stockage de fichier Azure]
* [Zone d’atterrissage des données]
* [FTP]
* [Google Cloud Storage]
* [HDFS]
* [Oracle Object Storage]
* [SFTP]

Lisez ce guide pour savoir comment ingérer des données chiffrées avec des sources par lots de stockage dans le cloud à l’aide de l’interface utilisateur.

## Commencer

Il est utile de connaître les fonctions et concepts Experience Platform suivants avant d’utiliser l’ingestion de données chiffrées dans l’interface utilisateur :

* [Sources](../../home.md) : utilisez des sources en Experience Platform pour ingérer des données à partir d’une application d’Adobe ou d’une source de données tierce.
* [Flux de données](../../../dataflows/home.md) : les flux de données sont des représentations des tâches de données qui déplacent les données entre Experience Platform. Vous pouvez utiliser l’espace de travail des sources pour créer des flux de données qui assimilent des données d’une source donnée à un Experience Platform.
* [Environnements de test](../../../sandboxes/home.md) : utilisez des environnements de test dans Experience Platform pour créer des partitions virtuelles entre vos instances Experience Platform et créez des environnements dédiés au développement ou à la production.

### Composition de haut niveau

1. Créez une paire de clés de chiffrement à l’aide de l’espace de travail des sources dans l’interface utilisateur de l’Experience Platform. Vous pouvez également créer une paire de clés de vérification des signes afin de fournir une couche supplémentaire de sécurité à vos données chiffrées.
2. Utilisez la clé publique pour chiffrer vos données.
3. Placez vos données chiffrées dans votre fournisseur de stockage dans le cloud. Au cours de cette étape, vous devez également vous assurer que vous disposez d’un fichier d’exemple qui peut être utilisé comme référence pour mapper vos données source à un schéma de modèle de données d’expérience (XDM).
4. Ingérez vos données cryptées dans Experience Platform en créant une connexion source.
5. Lors de la création de votre connexion source, fournissez l’ID de clé correspondant à la clé publique que vous avez utilisée pour chiffrer vos données. Si vous avez également utilisé le mécanisme de paire de clés de vérification des signes, vous devez également fournir l’identifiant de clé de vérification des signes qui correspond à vos données chiffrées.
6. Passez aux étapes de création du flux de données.

## Création d’une paire de clés de chiffrement {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID de clé de chiffrement"
>abstract="Indiquez l’ID de clé de chiffrement correspondant à votre clé de chiffrement qui a été utilisée pour chiffrer vos données source."

* Dans l’interface utilisateur de Platform, accédez à l’espace de travail des sources, puis sélectionnez [!UICONTROL Paires de clés] dans l’en-tête supérieur.
* Vous accédez à une page qui affiche une liste des paires de clés de chiffrement existantes dans votre entreprise. Cette page fournit des informations sur le titre, l’identifiant, le type, l’algorithme de chiffrement, l’expiration et l’état d’une clé donnée. Pour créer une paire de clés, sélectionnez **[!UICONTROL Créer une clé]**.
* Sélectionnez ensuite le type de clé à créer. Pour créer une clé de chiffrement, sélectionnez **[!UICONTROL Clé de chiffrement]**, puis fournissez un titre et un mot de passe pour votre clé de chiffrement. La phrase secrète est une couche supplémentaire de protection pour vos clés de chiffrement. Lors de sa création, Experience Platform stocke la phrase secrète dans un coffre sécurisé différent de celui de la clé publique. Vous devez fournir une chaîne non vide comme phrase secrète.

### Création d’une clé de vérification des signes {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Identifiant de clé de vérification de signature"
>abstract="Fournissez l’identifiant de la clé de vérification des signes qui correspond à vos données source signées et chiffrées."

## Ingérer des données chiffrées {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Le fichier est-il chiffré ?"
>abstract="Sélectionnez ce bouton (bascule) si vous ingérez un fichier déjà chiffré."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Sélectionner le fichier d’exemple"
>abstract="Vous devez ingérer un fichier d’exemple lors de l’ingestion de données chiffrées afin de créer un mapping."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
