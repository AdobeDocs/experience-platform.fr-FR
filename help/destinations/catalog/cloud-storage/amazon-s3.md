---
title: Connexion Amazon S3
description: Créez une connexion sortante active vers votre stockage Amazon Web Services (AWS) S3 pour exporter régulièrement des fichiers de données CSV depuis Adobe Experience Platform vers vos propres compartiments S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 51%

---

# Connexion [!DNL Amazon S3] {#s3-connection}

## Journal des modifications de destination {#changelog}

+++ Afficher le journal des modifications


| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Janvier 2024 | Nouvelles fonctionnalités et mise à jour de la documentation | Le connecteur de destination Amazon S3 prend désormais en charge un nouveau type d’authentification de rôle supposé. Pour en savoir plus, consultez la [section d&#39;authentification](#assumed-role-authentication). |
| Juillet 2023 | Nouvelles fonctionnalités et mise à jour de la documentation | Avec la version Experience Platform de juillet 2023, la destination [!DNL Amazon S3] offre de nouvelles fonctionnalités, comme indiqué ci-dessous : <br><ul><li>[ Prise en charge de l’exportation des jeux de données](/help/destinations/ui/export-datasets.md)</li><li>[Options de dénomination de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) supplémentaires.</li><li>Possibilité de définir des en-têtes de fichier personnalisés dans vos fichiers exportés via l’[étape de mappage améliorée](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Possibilité de personnaliser le formatage des fichiers de données CSV exportés](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Connexion à votre stockage [!DNL Amazon S3] via l’API ou l’interface utilisateur {#connect-api-or-ui}

* Pour vous connecter à votre emplacement de stockage [!DNL Amazon S3] à l’aide de l’interface utilisateur de Platform, lisez les sections [Se connecter à la destination](#connect) et [Activer les audiences vers cette destination](#activate) ci-dessous.
* Pour vous connecter à votre emplacement de stockage [!DNL Amazon S3] par programmation, lisez le guide sur l’ [activation d’audiences vers des destinations basées sur des fichiers à l’aide du tutoriel de l’API Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Type d’exportation Amazon S3 basé sur un profil mis en surbrillance dans l’UU.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Exporter des jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez les tutoriels :

* Comment [exporter des jeux de données à l’aide de l’interface utilisateur de Platform](/help/destinations/ui/export-datasets.md).
* Comment [exporter des jeux de données par programmation à l’aide de l’API Flow Service](/help/destinations/api/export-datasets.md).

## Format de fichier des données exportées {#file-format}

Lors de l’exportation de *données d’audience*, Platform crée un fichier `.csv`, `parquet` ou `.json` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [Formats de fichiers pris en charge pour l’exportation](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) du tutoriel sur l’activation de l’audience.

Lors de l’exportation de *jeux de données*, Platform crée un fichier `.parquet` ou `.json` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [Vérification de l’exportation des jeux de données réussie](../../ui/export-datasets.md#verify) du tutoriel sur l’exportation des jeux de données.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Clé publique RSA"
>abstract="Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Affichez un exemple de clé correctement formatée dans le lien de documentation ci-dessous."

Pour vous authentifier à la destination, remplissez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**. La destination Amazon S3 prend en charge deux méthodes d’authentification :

* Authentification par clé d’accès et clé secrète
* Authentification du rôle assumé

#### Authentification par clé d’accès et clé secrète

Utilisez cette méthode d’authentification lorsque vous souhaitez saisir votre clé d’accès Amazon S3 et votre clé secrète pour permettre à l’Experience Platform d’exporter des données vers vos propriétés Amazon S3.

![Image des champs requis lors de la sélection de l&#39;authentification par clé d&#39;accès et clé secrète.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]Clé d’accès** et **[!DNL Amazon S3]clé secrète** : dans [!DNL Amazon S3], générez une paire `access key - secret access key` pour accorder à Platform l’accès à votre compte [!DNL Amazon S3]. En savoir plus dans la [Documentation Amazon Web Services](https://docs.aws.amazon.com/fr_fr/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Clé de chiffrement]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous.

  ![ Image montrant un exemple de clé PGP correctement formatée dans l&#39;interface utilisateur.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Rôle assumé {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Authentification du rôle assumé"
>abstract="Utilisez ce type d’authentification si vous préférez ne pas partager les clés de compte et les clés secrètes avec Adobe. Au lieu de cela, Experience Platform se connecte à votre emplacement Amazon S3 en utilisant un accès basé sur les rôles. Collez l’ARN (nom de ressource Amazon) du rôle que vous avez créé dans AWS pour l’utilisateur ou l’utilisatrice Adobe. Le modèle est similaire à `arn:aws:iam::800873819705:role/destinations-role-customer`. "

![Image des champs requis lors de la sélection de l’authentification du rôle assumé.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Utilisez ce type d’authentification si vous préférez ne pas partager les clés de compte et les clés secrètes avec Adobe. Experience Platform se connecte plutôt à votre emplacement Amazon S3 à l’aide d’un accès basé sur les rôles.

Pour ce faire, vous devez créer dans la console AWS un utilisateur présumé pour l’Adobe avec les [autorisations requises appropriées](#required-s3-permission) pour écrire dans vos compartiments Amazon S3. Créez une **[!UICONTROL entité approuvée]** dans AWS avec le compte Adobe **[!UICONTROL 670664943635]**. Pour plus d&#39;informations, consultez la [documentation AWS sur la création de rôles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]** : collez l’ARN du rôle que vous avez créé dans AWS pour l’utilisateur Adobe. Le modèle est similaire à `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL Clé de chiffrement]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous.

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nom du compartiment"
>abstract="Doit comporter entre 3 et 63 caractères. Doit commencer et se terminer par une lettre ou un numéro. Ne doit contenir que des lettres minuscules, des chiffres ou des tirets ( - ). Ne doit pas être formaté comme une adresse IP (par exemple, 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Chemin du dossier"
>abstract="Doit contenir uniquement les caractères A-Z, a-z, 0-9 et peut contenir les caractères spéciaux suivants : `/!-_.'()"^[]+$%.*"`. Pour créer un dossier par fichier d’audience, insérez la macro `/%SEGMENT_NAME%` ou `/%SEGMENT_ID%` ou `/%SEGMENT_NAME%/%SEGMENT_ID%` dans le champ de texte. Les macros ne peuvent être insérées qu’à la fin du chemin du dossier. Affichez des exemples de macro dans la documentation."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=fr#use-macros" text="Utiliser les macros pour créer un dossier à votre emplacement de stockage"

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : entrez une description de cette destination.
* **[!UICONTROL Nom du compartiment]** : saisissez le nom du compartiment [!DNL Amazon S3] que cette destination doit utiliser.
* **[!UICONTROL Chemin d’accès au dossier]** : saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL Type de fichier]** : sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Lorsque vous sélectionnez l’option [!UICONTROL CSV] , vous pouvez également [ configurer les options de formatage de fichier ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Format de compression]** : sélectionnez le type de compression que l’Experience Platform doit utiliser pour les fichiers exportés.
* **[!UICONTROL Inclure le fichier manifeste]** : activez cette option si vous souhaitez que les exportations incluent un fichier JSON manifeste contenant des informations sur l’emplacement d’exportation, la taille de l’exportation, etc. Le manifeste est nommé au format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Affichez un [exemple de fichier manifeste](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Le fichier de manifeste comprend les champs suivants :
   * `flowRunId` : [exécution de flux de données](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) qui a généré le fichier exporté.
   * `scheduledTime` : heure en UTC à laquelle le fichier a été exporté.
   * `exportResults.sinkPath` : chemin d’accès dans l’emplacement de stockage où le fichier exporté est déposé.
   * `exportResults.name` : nom du fichier exporté.
   * `size` : taille du fichier exporté, en octets.

>[!TIP]
>
>Dans le workflow de connexion à la destination, vous pouvez créer un dossier personnalisé dans le stockage Amazon S3 par fichier d’audience exporté. Lisez [Utiliser les macros pour créer un dossier à l’emplacement de stockage](overview.md#use-macros) pour obtenir des instructions.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Autorisations [!DNL Amazon S3] nécessaires {#required-s3-permission}

Pour établir une connexion et exporter des données vers votre emplacement de stockage [!DNL Amazon S3], créez un utilisateur de gestion des identités et des accès (IAM) pour [!DNL Platform] dans [!DNL Amazon S3] et attribuez des autorisations pour les actions suivantes :

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

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activation des données d’audience vers des destinations d’exportation de profil de lot](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Valider l’exportation des données avec succès {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez le stockage [!DNL Amazon S3] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Liste autorisée d’adresses IP {#ip-address-allow-list}

Reportez-vous à l’article [liste autorisée d’adresses IP](ip-address-allow-list.md) si vous devez ajouter des adresses IP d’Adobe à une liste autorisée.