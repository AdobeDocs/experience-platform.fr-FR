---
title: Ingestion de données chiffrées dans l’interface utilisateur de sources Workspace
description: Découvrez comment ingérer des données chiffrées dans l’espace de travail de l’interface utilisateur des sources.
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 30%

---

# Ingestion de données chiffrées dans l’interface utilisateur des sources

Lisez ce guide pour savoir comment ingérer des données chiffrées vers Adobe Experience Platform à l’aide de sources de stockage dans le cloud pour les données par lots.

## Conditions préalables

* Chiffrement des données

## Ingérer des données chiffrées {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Le fichier est-il chiffré ?"
>abstract="Sélectionnez ce bouton (bascule) si vous ingérez un fichier déjà chiffré."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Sélectionner le fichier d’exemple"
>abstract="Vous devez ingérer un fichier d’exemple lors de l’ingestion de données chiffrées afin de créer un mapping."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID de clé de chiffrement"
>abstract="Indiquez l’ID de clé de chiffrement correspondant à votre clé de chiffrement qui a été utilisée pour chiffrer vos données source."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Identifiant de clé de vérification de signature"
>abstract="Fournissez l’identifiant de la clé de vérification des signes qui correspond à vos données source signées et chiffrées."

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
