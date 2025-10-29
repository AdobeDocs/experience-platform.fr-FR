---
title: Connexion Azure Data Lake Storage Gen2
description: Découvrez comment vous connecter à Azure Data Lake Storage Gen2 pour activer des audiences et exporter des jeux de données.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 42%

---

# Connexion [!DNL Azure Data Lake Storage Gen2]

## Présentation {#overview}

Lisez cette page pour apprendre à créer une connexion sortante active vers votre lac de données [[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) ([!DNL ADLS Gen2]) pour exporter périodiquement des fichiers de données à partir d’Experience Platform.

## Connexion à votre stockage [!DNL ADLS Gen2] via l’API ou l’interface utilisateur {#connect-api-or-ui}

* Pour vous connecter à l’emplacement de stockage de votre [!DNL ADLS Gen2] à l’aide de l’interface utilisateur d’Experience Platform, lisez les sections [Se connecter à la destination](#connect) et [Activer des audiences vers cette destination](#activate) ci-dessous.
* Pour vous connecter à votre emplacement de stockage [!DNL ADLS Gen2] par programmation, lisez le tutoriel [&#x200B; Activer des audiences vers des destinations basées sur des fichiers à l’aide de l’API Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Profile-based]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables (par exemple votre PPID), tels que choisis dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Batch]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exporter des jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez les tutoriels :

* Comment [exporter des jeux de données à l’aide de l’interface utilisateur Experience Platform](/help/destinations/ui/export-datasets.md).
* Comment [exporter des jeux de données par programmation à l’aide de l’API Flow Service](/help/destinations/api/export-datasets.md).

## Format des données exportées {#file-format}

Lors de l’exportation de *données d’audience*, Experience Platform crée un fichier `.csv`, `parquet` ou `.json` à l’emplacement de stockage indiqué. Pour plus d’informations sur les fichiers, consultez la section [formats de fichiers pris en charge pour l’exportation](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) dans le tutoriel sur l’activation des audiences.

Lors de l’exportation de *jeux de données*, Experience Platform crée un fichier `.parquet` ou `.json` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [vérifier la réussite de l’exportation du jeu de données](../../ui/export-datasets.md#verify) dans le tutoriel sur l’exportation des jeux de données.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](/help/destinations/ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

* **[!UICONTROL URL]** : point d’entrée pour [!DNL Azure Data Lake Storage Gen2]. Le modèle de point d’entrée est le suivant : `abfss://<container>@<accountname>.dfs.core.windows.net`.
* **[!UICONTROL Tenant]** : informations du client qui contient votre application.
* **[!UICONTROL Service principal ID]** : identifiant client de l’application.
* **[!UICONTROL Service principal key]** : clé de l’application.
* **[!UICONTROL Encryption key]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous.

  ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Folder path]** : saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL File type]** : sélectionnez le format qu’Experience Platform doit utiliser pour les fichiers exportés. Lors de la sélection de l’option [!UICONTROL CSV] , vous pouvez également [configurer les options de formatage des fichiers](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]** : sélectionnez le type de compression qu’Experience Platform doit utiliser pour les fichiers exportés.
* **[!UICONTROL Include manifest file]** : activez cette option si vous souhaitez que les exportations incluent un fichier JSON manifeste contenant des informations sur l’emplacement de l’exportation, la taille de l’exportation, etc. Le manifeste est nommé à l’aide du format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Affichez un [exemple de fichier de manifeste](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Le fichier manifeste comprend les champs suivants :
   * `flowRunId` : exécution [flux de données](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) qui a généré le fichier exporté.
   * `scheduledTime` : heure en UTC à laquelle le fichier a été exporté.
   * `exportResults.sinkPath` : chemin d’accès à l’emplacement de stockage où le fichier exporté est déposé.
   * `exportResults.name` : nom du fichier exporté.
   * `size` : taille du fichier exporté, en octets.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [&#x200B; Activer les données d’audience vers des destinations d’exportation de profils par lots &#x200B;](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Planification {#scheduling}

Dans l’étape de **[!UICONTROL Scheduling]**, vous pouvez [configurer le planning d’exportation](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour votre destination [!DNL Azure Data Lake Storage Gen2] et vous pouvez également [configurer le nom de vos fichiers exportés](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapper les attributs et les identités {#map}

L’étape **[!UICONTROL Mapping]** vous permet de sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activer l’interface utilisateur des destinations par lot.

## Valider l’exportation des données avec succès {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez le stockage [!DNL Azure Data Lake Storage Gen2] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
