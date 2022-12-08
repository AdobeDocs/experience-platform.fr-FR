---
keywords: Amazon S3;destination S3;s3;amazon s3
title: Connexion Amazon S3
description: Créez une connexion sortante active à votre stockage Amazon Web Services (AWS) S3 pour exporter périodiquement des fichiers de données CSV de Adobe Experience Platform vers vos propres compartiments S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: a07557ec398631ece0c8af6ec7b32e0e8593e24b
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 23%

---

# Connexion [!DNL Amazon S3] {#s3-connection}

## Journal des modifications de destination {#changelog}

>[!IMPORTANT]
>
>Avec la version bêta de la fonctionnalité d’exportation des jeux de données et la fonctionnalité améliorée d’exportation de fichiers, vous pouvez maintenant voir deux [!DNL Amazon S3] cartes dans le catalogue des destinations.
>* Si vous exportez déjà des fichiers vers le **[!UICONTROL Amazon S3]** destination, créez de nouveaux flux de données pour le nouveau **[!UICONTROL Amazon S3 bêta]** destination.
>* Si vous n’avez pas encore créé de flux de données pour la variable **[!UICONTROL Amazon S3]** destination, veuillez utiliser la nouvelle **[!UICONTROL Amazon S3 bêta]** carte pour exporter des fichiers vers **[!UICONTROL Amazon S3]**.


![Image des deux cartes de destination Amazon S3 dans une vue côte à côte.](../../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

Améliorations de la nouvelle [!DNL Amazon S3] carte de destination :

* [Prise en charge de l’exportation des jeux de données](/help/destinations/ui/export-datasets.md).
* Additional [options de dénomination de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Possibilité de définir des en-têtes de fichier personnalisés dans vos fichiers exportés via le [étape de mappage améliorée](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilité de personnaliser le formatage des fichiers de données CSV exportés](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Présentation {#overview}

Créer une connexion sortante active à votre [!DNL Amazon S3] le stockage pour exporter régulièrement des fichiers de données de Adobe Experience Platform vers vos propres compartiments S3.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Type d’exportation basé sur les profils Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Clé publique RSA"
>abstract="Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Affichez un exemple de clé correctement formatée dans le lien de documentation ci-dessous."

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!DNL Amazon S3]clé d&#39;accès** et **[!DNL Amazon S3]clé secrète**: Dans [!DNL Amazon S3], générez une `access key - secret access key` pour accorder l’accès à Platform à votre [!DNL Amazon S3] compte . En savoir plus dans la section [Documentation Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Affichez un exemple de clé de chiffrement correctement formatée dans l’image ci-dessous.

   ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nom du compartiment"
>abstract="Doit comporter entre 3 et 63 caractères. Doit commencer et se terminer par une lettre ou un numéro. Ne doit contenir que des lettres minuscules, des chiffres ou des tirets ( - ). Ne doit pas être formaté en tant qu’adresse IP (par exemple, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Chemin du dossier"
>abstract="Doit contenir uniquement les caractères A-Z, a-z, 0-9 et peut contenir les caractères spéciaux suivants : `/!-_.'()"^[]+$%.*"`. Pour créer un dossier par fichier de segment, insérez la macro `/%SEGMENT_NAME%` ou `/%SEGMENT_ID%` ou `/%SEGMENT_NAME%/%SEGMENT_ID%` dans le champ de texte. Les macros ne peuvent être insérées qu’à la fin du chemin du dossier. Affichez des exemples de macro dans la documentation."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="Utilisez les macros pour créer un dossier à l’emplacement de stockage"

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]**: saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]**: saisissez une description de cette destination.
* **[!UICONTROL Nom du compartiment]**: saisissez le nom du [!DNL Amazon S3] compartiment à utiliser par cette destination.
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL Type de fichier]**: sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Cette option n’est disponible que pour la variable **[!UICONTROL Amazon S3 bêta]** destination. Lorsque vous sélectionnez la variable [!UICONTROL CSV] , vous pouvez également [configuration des options de formatage de fichier](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Format de compression]**: sélectionnez le type de compression que l’Experience Platform doit utiliser pour les fichiers exportés. Cette option n’est disponible que pour la variable **[!UICONTROL Amazon S3 bêta]** destination.


>[!TIP]
>
>Dans le workflow de connexion à la destination, vous pouvez créer un dossier personnalisé dans le stockage Amazon S3 par fichier de segment exporté. Lecture [Utilisez les macros pour créer un dossier à l’emplacement de stockage](overview.md#use-macros) pour obtenir des instructions.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Obligatoire [!DNL Amazon S3] permissions {#required-s3-permission}

Pour établir une connexion et exporter des données vers votre [!DNL Amazon S3] emplacement de stockage, créez un utilisateur de gestion des identités et des accès (IAM) pour [!DNL Platform] in [!DNL Amazon S3] et attribuez des autorisations pour les actions suivantes :

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## (Version bêta) Exportation de jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez la section [tutoriel sur l’exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Données exportées {#exported-data}

Pour [!DNL Amazon S3] destinations, [!DNL Platform] crée un fichier de données à l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des segments.
