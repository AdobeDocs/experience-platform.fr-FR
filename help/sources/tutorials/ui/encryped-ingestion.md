---
title: Ingestion de données chiffrées dans l’interface utilisateur de sources Workspace
description: Découvrez comment ingérer des données chiffrées dans l’espace de travail de l’interface utilisateur des sources.
badge: Version bêta
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 70bfebc747c7e6267939eb313048cb2d0e132202
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 9%

---

# Ingestion de données chiffrées dans l’interface utilisateur des sources

>[!AVAILABILITY]
>
>La prise en charge de l’ingestion de données chiffrées dans l’interface utilisateur des sources est en version bêta. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

Vous pouvez ingérer des fichiers de données et des dossiers chiffrés dans Adobe Experience Platform à l’aide de sources par lots de stockage dans le cloud. Avec l’ingestion de données chiffrées, vous pouvez utiliser des mécanismes de chiffrement asymétrique pour transférer en toute sécurité des données par lots dans Experience Platform. Les mécanismes de cryptage asymétrique pris en charge sont PGP et GPG.

Lisez ce guide pour savoir comment ingérer des données chiffrées avec des sources par lots de stockage dans le cloud à l’aide de l’interface utilisateur.

## Commencer

Avant de poursuivre ce tutoriel, veuillez lire les documents suivants pour mieux comprendre les fonctionnalités et concepts Experience Platform suivants.

* [Sources](../../home.md) : utilisez des sources en Experience Platform pour ingérer des données à partir d’une application d’Adobe ou d’une source de données tierce.
* [Flux de données](../../../dataflows/home.md) : les flux de données sont des représentations des tâches de données qui déplacent les données entre Experience Platform. Vous pouvez utiliser l’espace de travail des sources pour créer des flux de données qui assimilent des données d’une source donnée à un Experience Platform.
* [Environnements de test](../../../sandboxes/home.md) : utilisez des environnements de test dans Experience Platform pour créer des partitions virtuelles entre vos instances Experience Platform et créez des environnements dédiés au développement ou à la production.

### Composition de haut niveau

* Créez une paire de clés de chiffrement à l’aide de l’espace de travail des sources dans l’interface utilisateur de l’Experience Platform.
   * Vous pouvez également créer votre propre paire de clés de vérification des signes afin de fournir une couche supplémentaire de sécurité à vos données chiffrées.
* Utilisez la clé publique de votre paire de clés de chiffrement pour chiffrer vos données.
* Placez vos données chiffrées dans votre espace de stockage dans le cloud. Au cours de cette étape, vous devez également vous assurer que vous disposez d’un fichier d’exemple de vos données dans votre espace de stockage dans le cloud qui peut être utilisé comme référence pour mapper vos données source à un schéma de modèle de données d’expérience (XDM).
* Utilisez votre source par lots de stockage dans le cloud et commencez le processus d’ingestion des données dans l’espace de travail des sources de l’interface utilisateur Experience Platform.
* Pendant le processus de création de la connexion source, indiquez l’identifiant de la clé qui correspond à la clé publique que vous avez utilisée pour chiffrer vos données.
   * Si vous avez également utilisé le mécanisme de paire de clés de vérification des signes, vous devez également fournir l’identifiant de clé de vérification des signes qui correspond à vos données chiffrées.
* Passez aux étapes de création du flux de données.

## Créer une paire de clés de chiffrement {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID de clé de chiffrement"
>abstract="Indiquez l’ID de clé de chiffrement correspondant à la clé de chiffrement qui a été utilisée pour chiffrer vos données source."

>[!BEGINSHADEBOX]

**Qu’est-ce qu’une paire de clés de chiffrement ?**

Une paire de clés de cryptage est un mécanisme de cryptographie asymétrique constitué d’une clé publique et d’une clé privée. La clé publique est utilisée pour crypter les données et la clé privée est ensuite utilisée pour décrypter ces données.

Vous pouvez créer votre paire de clés de chiffrement via l’interface utilisateur de l’Experience Platform. Une fois généré, vous recevez une clé publique et un identifiant de clé correspondant. Utilisez la clé publique pour crypter vos données, puis utilisez l’identifiant de clé pour confirmer votre identité, lorsque vous êtes en train d’ingérer vos données chiffrées. La clé privée est automatiquement envoyée à l’Experience Platform, où elle est stockée dans un coffre sécurisé, et ne sera utilisée qu’une fois vos données prêtes pour le décryptage.

>[!ENDSHADEBOX]

Dans l’interface utilisateur de Platform, accédez à l’espace de travail des sources, puis sélectionnez [!UICONTROL Paires de clés] dans l’en-tête supérieur.

![Catalogue des sources avec l&#39;en-tête &quot;Paires clés&quot; sélectionné.](../../images/tutorials/edi/catalog.png)

Vous accédez à une page qui affiche une liste des paires de clés de chiffrement existantes dans votre entreprise. Cette page fournit des informations sur le titre, l’identifiant, le type, l’algorithme de chiffrement, l’expiration et l’état d’une clé donnée. Pour créer une paire de clés, sélectionnez **[!UICONTROL Créer une clé]**.

![La page des paires de clés, avec &quot;clé de chiffrement&quot; sélectionnée comme type de clé et le bouton &quot;créer la clé&quot; sélectionné.](../../images/tutorials/edi/encryption_key_page.png)

Sélectionnez ensuite le type de clé à créer. Pour créer une clé de chiffrement, sélectionnez **[!UICONTROL Clé de chiffrement]**, puis **[!UICONTROL Continuer]**.

![ La fenêtre de création de la clé, avec la clé de chiffrement sélectionnée.](../../images/tutorials/edi/choose_encryption_key_type.png)

Indiquez un titre et un mot de passe pour votre clé de chiffrement. La phrase secrète est une couche supplémentaire de protection pour vos clés de chiffrement. Lors de sa création, Experience Platform stocke la phrase secrète dans un coffre sécurisé différent de celui de la clé publique. Vous devez fournir une chaîne non vide comme mot de passe. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

![ Fenêtre de création de clé de chiffrement, dans laquelle un titre et un mot de passe sont fournis.](../../images/tutorials/edi/create_encryption_key.png)

En cas de réussite, une nouvelle fenêtre s’affiche, affichant votre nouvelle clé de chiffrement, y compris son titre, sa clé publique et son identifiant de clé. Utilisez la valeur de clé publique pour chiffrer vos données. Vous utiliserez l’identifiant de clé à une étape ultérieure pour prouver votre identité lors de l’ingestion de vos données chiffrées pendant le processus de création du flux de données.

![Fenêtre qui affiche des informations sur la paire de clés de chiffrement que vous venez de créer.](../../images/tutorials/edi/encryption_key_details.png)

Pour afficher des informations sur une clé de chiffrement existante, sélectionnez les ellipses (`...`) en regard du titre de la clé. Sélectionnez **[!UICONTROL Détails de la clé]** pour afficher la clé publique et l’ID de la clé. Si vous souhaitez également supprimer votre clé de chiffrement, sélectionnez **[!UICONTROL Supprimer]**.

![Page des paires de clés, où une liste des clés de chiffrement s’affiche. Les points de suspension en regard de &quot;acme-encryption-key&quot; sont sélectionnés et la liste déroulante affiche des options pour afficher les détails de la clé ou supprimer les clés.](../../images/tutorials/edi/configuration_options.png)

### Créer une clé de vérification de signe {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID de clé de vérification de signe"
>abstract="Fournissez l’ID de clé de vérification de signe qui correspond à vos données source signées et chiffrées."

>[!BEGINSHADEBOX]

**Qu’est-ce qu’une clé de vérification des signes ?**

Une clé de vérification des signes est un autre mécanisme de chiffrement qui implique une clé privée et une clé publique. Dans ce cas, vous pouvez créer votre paire de clés de vérification de signature et utiliser la clé privée pour signer et fournir une couche de chiffrement supplémentaire à vos données. Vous partagerez ensuite la clé publique correspondante à l’Experience Platform. Pendant l’ingestion, l’Experience Platform utilisera la clé publique pour vérifier la signature associée à votre clé privée.

>[!ENDSHADEBOX]

Pour créer une clé de vérification des signes, sélectionnez **[!UICONTROL Sign Verification Key]** dans la fenêtre de sélection du type de clé, puis **[!UICONTROL Continue]** (Continuer).

![Fenêtre de sélection du type de clé dans laquelle la clé de vérification de signature est sélectionnée.](../../images/tutorials/edi/choose_sign_verification_key_type.png)

Ensuite, fournissez un titre et une clé PGP codée [!DNL Base64] comme clé publique, puis sélectionnez **[!UICONTROL Créer]**.

![ La fenêtre Créer une clé de vérification des signes.](../../images/tutorials/edi/create_sign_verification_key.png)

En cas de réussite, une nouvelle fenêtre s’affiche, affichant votre nouvelle clé de vérification de signature, y compris son titre et son identifiant de clé.

![Détails de la clé de vérification de signe nouvellement créée.](../../images/tutorials/edi/sign_verification_key_details.png)

## Ingérer des données chiffrées {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Le fichier est-il chiffré ?"
>abstract="Sélectionnez ce bouton (bascule) si vous ingérez un fichier déjà chiffré."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Sélectionner le fichier d’exemple"
>abstract="Vous devez ingérer un fichier d’exemple lors de l’ingestion de données chiffrées afin de créer un mapping."

Vous pouvez ingérer des données chiffrées à l’aide des sources par lots de stockage dans le cloud suivantes :

* [[!DNL Amazon S3]](../ui/create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../ui/create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../ui/create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../ui/create/cloud-storage/azure-file-storage.md)
* [[!DNL Data Landing Zone]](../ui/create/cloud-storage/data-landing-zone.md)
* [[!DNL FTP]](../ui/create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../ui/create/cloud-storage/google-cloud-storage.md)
* [[!DNL HDFS]](../ui/create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../ui/create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../ui/create/cloud-storage/sftp.md)

Authentifiez-vous avec la source de stockage dans le cloud de votre choix. Lors de l’étape de sélection des données du workflow, sélectionnez le fichier ou le dossier chiffré à ingérer, puis activez le bouton d’activation/désactivation **[!UICONTROL Is the file encrypted]**.

![L&#39;étape &quot;sélectionner les données&quot; du workflow des sources, où un fichier de données chiffré est sélectionné pour être ingéré.](../../images/tutorials/edi/select_data.png)

Sélectionnez ensuite un fichier d’exemple parmi vos données source. Puisque vos données sont chiffrées, Experience Platform aura besoin d’un fichier d’exemple pour créer un schéma XDM pouvant être mappé à vos données source.

![ &quot;Ce fichier est-il chiffré ?&quot; Activez l’option et le bouton &quot;Sélectionner un fichier d’exemple&quot; sélectionné. ](../../images/tutorials/edi/select_sample_file.png)

Une fois le fichier d’exemple sélectionné, configurez les paramètres de vos données, tels que le format de données, le délimiteur et le type de compression correspondants. Laissez un certain temps à l’interface d’aperçu pour un rendu complet, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Un exemple est sélectionné pour l’ingestion et l’aperçu du fichier est entièrement chargé.](../../images/tutorials/edi/file_preview.png)

À partir de là, utilisez le menu déroulant pour sélectionner le titre de la clé publique de l’ID de clé publique correspondant à la clé publique que vous avez utilisée pour chiffrer vos données.

![Titre de la clé publique de l’ID de la clé publique correspondant à la clé publique utilisée pour chiffrer vos données.](../../images/tutorials/edi/public_key_id.png)

Si vous avez également utilisé la paire de clés de vérification des signes pour fournir une couche supplémentaire de chiffrement, activez le bouton bascule de la clé de vérification des signes puis, de la même manière, utilisez la liste déroulante pour sélectionner l’identifiant de clé de vérification des signes correspondant à la clé que vous avez utilisée pour chiffrer vos données.

![Titre de la clé de vérification de signature de l’identifiant de clé qui correspond à votre chiffrement de vérification de signature.](../../images/tutorials/edi/custom_key_id.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

Suivez les étapes restantes du workflow des sources pour terminer la création de votre flux de données.

* [Fournir des détails sur le flux de données et le jeu de données](../ui/dataflow/batch/cloud-storage.md#provide-dataflow-details)
* [Mappage des données source à un schéma XDM](../ui/dataflow/batch/cloud-storage.md#map-data-fields-to-an-xdm-schema)
* [Configuration d’un planning d’ingestion pour votre flux de données](../ui/dataflow/batch/cloud-storage.md#schedule-ingestion-runs)
* [Vérifier le flux de données](../ui/dataflow/batch/cloud-storage.md#review-your-dataflow)

Vous pouvez continuer à [mettre à jour votre flux de données](../ui/update-dataflows.md) une fois qu’il a été créé.

## Étapes suivantes

En lisant ce document, vous pouvez désormais ingérer des données chiffrées à partir de votre source de lot de stockage dans le cloud vers Experience Platform. Pour plus d’informations sur l’ingestion de données chiffrées à l’aide des API, lisez le guide sur l’[ingestion de données chiffrées à l’aide de l’ [!DNL Flow Service] API](../api/encrypt-data.md). Pour obtenir des informations générales sur les sources sur Experience Platform, consultez la [présentation des sources](../../home.md).
