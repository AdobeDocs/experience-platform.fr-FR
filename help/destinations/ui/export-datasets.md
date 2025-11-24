---
title: Exporter des jeux de données vers des destinations d’espace de stockage
type: Tutorial
description: Découvrez comment exporter des jeux de données d’Adobe Experience Platform vers l’emplacement d’espace de stockage de votre choix.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: de161bcb29a0d4fc9b0c419506537b18255c79a4
workflow-type: tm+mt
source-wordcount: '3005'
ht-degree: 22%

---

# Exporter des jeux de données vers des destinations d’espace de stockage

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté le package Real-Time CDP Prime ou Ultimate, Adobe Journey Optimizer ou Customer Journey Analytics. Contactez votre représentant ou représentante Adobe pour plus d’informations.

>[!IMPORTANT]
>
>**Action item** : la version [septembre 2024 d’Experience Platform](/help/release-notes/latest/latest.md#destinations) a introduit l’option permettant de définir une date `endTime` pour l’exportation des flux de données du jeu de données. Adobe a également introduit une date de fin par défaut du 1er septembre 2025 pour tous les flux de données d’exportation de jeux de données créés *avant le 1er novembre 2024*.
>
>Pour l’un de ces flux de données, vous devez mettre à jour manuellement la date de fin du flux de données avant la date de fin, sinon vos exportations s’arrêteront à cette date. Utilisez l’interface utilisateur d’Experience Platform pour afficher les flux de données qui seront définis pour s’arrêter le 1er septembre 2025.
>
>Pour plus d’informations sur la modification de la date de fin d’un flux de données d’exportation de jeux de données[ consultez la section ](#scheduling)planification.

Cet article explique le processus requis pour exporter des [jeux de données](/help/catalog/datasets/overview.md) de Adobe Experience Platform vers l’emplacement d’espace de stockage de votre choix, comme des [!DNL Amazon S3], des emplacements SFTP ou des [!DNL Google Cloud Storage] à l’aide de l’interface utilisateur d’Experience Platform.

Vous pouvez également utiliser les API Experience Platform pour exporter des jeux de données. Pour plus d’informations, consultez le tutoriel [API d’exportation de jeux de données](/help/destinations/api/export-datasets.md) .

## Jeux de données disponibles pour l’exportation {#datasets-to-export}

Les jeux de données que vous pouvez exporter varient en fonction de l’application Experience Platform (Real-Time CDP, Adobe Journey Optimizer), du niveau (Prime ou Ultimate) et des modules complémentaires que vous avez achetés (par exemple : Data Distiller).

Utilisez le tableau ci-dessous pour comprendre quels types de jeux de données vous pouvez exporter en fonction de votre application, du niveau de produit et des modules complémentaires achetés :

<table>
<thead>
  <tr>
    <th>Application/module complémentaire</th>
    <th>Niveau</th>
    <th>Jeux de données disponibles à l’exportation</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Jeux de données de profil et d’événement d’expérience créés dans l’interface utilisateur d’Experience Platform après l’ingestion ou la collecte de données par le biais de sources, de Web SDK, de Mobile SDK, du connecteur de données Analytics et d’Audience Manager.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Jeux de données de profil et d’événement d’expérience créés dans l’interface utilisateur d’Experience Platform après l’ingestion ou la collecte de données par le biais de sources, de Web SDK, de Mobile SDK, du connecteur de données Analytics et d’Audience Manager.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Jeu de données d’instantanés de profil généré par le système</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Reportez-vous à la documentation de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> .</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Reportez-vous à la documentation de <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> .</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Toutes</td>
    <td> Jeux de données de profil et d’événement d’expérience créés dans l’interface utilisateur d’Experience Platform après l’ingestion ou la collecte de données par le biais de sources, de Web SDK, de Mobile SDK, du connecteur de données Analytics et d’Audience Manager.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Distiller de données (module complémentaire)</td>
    <td>Jeux de données dérivés créés via Query Service.</td>
  </tr>
</tbody>
</table>

## Tutoriel vidéo {#video-tutorial}

Regardez la vidéo ci-dessous pour une explication de bout en bout du workflow décrit sur cette page, des avantages de l’utilisation de la fonctionnalité d’exportation du jeu de données et de certains cas d’utilisation suggérés.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## Destinations prises en charge {#supported-destinations}

Actuellement, vous pouvez exporter des jeux de données vers les destinations d’espace de stockage mises en surbrillance dans la capture d’écran et répertoriées ci-dessous.

![Page du catalogue des destinations montrant quelles destinations prennent en charge les exportations de jeux de données.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Quand activer des audiences ou exporter des jeux de données {#when-to-activate-audiences-or-activate-datasets}

Certaines destinations basées sur des fichiers du catalogue Experience Platform prennent en charge l’activation des audiences et l’exportation des jeux de données.

* Envisagez l’activation des audiences lorsque vous souhaitez que vos données soient structurées en profils regroupés par intérêt ou qualification d’audience.
* Vous pouvez également envisager des exportations de jeux de données lorsque vous cherchez à exporter des jeux de données bruts, qui ne sont pas groupés ou structurés par intérêt ou qualification d’audience. Vous pouvez utiliser ces données pour la création de rapports, les workflows de science des données et de nombreux autres cas d’utilisation. Par exemple, en tant qu’administrateur, ingénieur de données ou analyste, vous pouvez exporter des données d’Experience Platform pour les synchroniser avec votre entrepôt de données, les utiliser dans des outils d’analyse BI, des outils de ML dans le cloud externe ou les stocker dans votre système pour des besoins de stockage à long terme.

Ce document contient toutes les informations nécessaires à l’exportation de jeux de données. Si vous souhaitez activer des *audiences* vers des destinations d’espace de stockage ou de marketing par e-mail, lisez [Activer les données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md).

## Conditions préalables {#prerequisites}

Notez les conditions préalables suivantes pour exporter des jeux de données :

* Pour exporter des jeux de données vers des destinations d’espace de stockage, vous devez vous être [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.
* Les jeux de données de profil doivent être activés pour être utilisés dans le profil client en temps réel. [En savoir plus](/help/ingestion/tutorials/ingest-batch-data.md#enable-for-profile) sur la manière d’activer cette option.

### Autorisations nécessaires {#permissions}

Pour exporter des jeux de données, vous avez besoin des **[!UICONTROL View Destinations]**, **[!UICONTROL View Datasets]** et **[!UICONTROL Manage and Activate Dataset Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour exporter des jeux de données et que la destination prend en charge l’exportation de jeux de données, parcourez le catalogue des destinations. Si une destination comporte un contrôle **[!UICONTROL Activate]** ou **[!UICONTROL Export datasets]**, vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connections > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalog]** .

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activate]** ou **[!UICONTROL Export datasets]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

   ![Onglet Catalogue de destinations avec le contrôle Activer mis en surbrillance.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Sélectionnez **[!UICONTROL Data type Datasets]** et sélectionnez la connexion de destination vers laquelle vous souhaitez exporter les jeux de données, puis sélectionnez **[!UICONTROL Next]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour exporter des jeux de données, sélectionnez **[!UICONTROL Configure new destination]** pour déclencher le workflow [Se connecter à la destination](/help/destinations/ui/connect-destination.md).

![Workflow d’activation de destination avec le contrôle Jeux de données mis en surbrillance.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. La vue **[!UICONTROL Select datasets]** s’affiche. Passez à la section suivante pour [sélectionner vos jeux de données](#select-datasets) pour l’exportation.

## Sélectionner vos jeux de données {#select-datasets}

Utilisez les cases à cocher situées à gauche des noms de jeux de données pour sélectionner les jeux de données à exporter vers la destination, puis sélectionnez **[!UICONTROL Next]**.

![Workflow d’exportation des jeux de données présentant l’étape de sélection des jeux de données permettant de sélectionner les jeux de données à exporter.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

>[!NOTE]
>
>Tous les jeux de données sélectionnés ici partageront le même planning d’exportation. Si vous avez besoin de différents plannings d’exportation (par exemple, des exportations incrémentielles pour certains jeux de données et des exportations complètes uniques pour d’autres), créez des flux de données distincts pour chaque type de planning.

## Planifier l’exportation des jeux de données {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Options d’exportation de fichiers pour les jeux de données"
>abstract="Sélectionnez **Exporter des fichiers incrémentiels** pour n’exporter que les données ajoutées au jeu de données depuis la dernière exportation. <br> La première exportation de fichier incrémentiel inclut toutes les données du jeu de données, agissant comme un renvoi. Les futurs fichiers incrémentiels incluent uniquement les données qui ont été ajoutées au jeu de données depuis le premier export. <br> Sélectionnez **Exporter les fichiers complets** pour exporter l’abonnement complet de chaque jeu de données à chaque export. "

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="Mettre à jour la date de fin de ce flux de données"
>abstract="Mettre à jour la date de fin de ce flux de données"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="Mettre à jour la date de fin de ce corps de flux de données"
>abstract="En raison des mises à jour récentes apportées à cette destination, le flux de données nécessite désormais une date de fin. Adobe a défini une date de fin par défaut au 1er septembre 2025. Mettez à jour à la date de fin souhaitée. Dans le cas contraire, les exports de données s’arrêteront à la date par défaut."

>[!IMPORTANT]
>
>**La planification s’applique à tous les jeux de données du flux de données**
>
>Lorsque vous configurez ou modifiez le planning d’exportation, il s’applique à **tous les jeux de données** actuellement exportés par le biais du flux de données que vous configurez. Vous ne pouvez pas définir différents plannings pour des jeux de données individuels dans le même flux de données.
>
>Si vous avez besoin de plannings d’exportation différents pour différents jeux de données, vous devez créer des flux de données distincts (connexions de destination distinctes) pour chaque type de planning.
>
>**Exemple :** si le jeu de données A est exporté de manière incrémentielle et que vous ajoutez le jeu de données B avec un planning d’exportation complet unique, le jeu de données A sera également mis à jour vers le planning d’exportation complet unique.

Utilisez l’étape **[!UICONTROL Scheduling]** pour :

* Définissez une date de début et une date de fin, ainsi qu’une cadence d’exportation pour vos exportations de jeux de données.
* Configurez si les fichiers de jeu de données exportés doivent exporter l’appartenance complète du jeu de données ou simplement des modifications incrémentielles de l’appartenance à chaque occurrence d’exportation.
* Personnalisez le chemin du dossier à l’emplacement de stockage où les jeux de données doivent être exportés. En savoir plus sur la [modification du chemin du dossier d’exportation](#edit-folder-path).

Utilisez le contrôle **[!UICONTROL Edit schedule]** de la page pour modifier le rythme d’exportation des exportations et pour choisir d’exporter des fichiers complets ou incrémentiels.

>[!WARNING]
>
>La modification du planning ici met à jour le comportement d’exportation pour tous les jeux de données de ce flux de données. Si ce flux de données contient plusieurs jeux de données, ils seront tous affectés par cette modification.

![Modifier le contrôle de planification mis en surbrillance à l’étape Planification.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlight.png)

L’option **[!UICONTROL Export incremental files]** est sélectionnée par défaut. Cela déclenche l’exportation d’un ou de plusieurs fichiers représentant un instantané complet du jeu de données. Les fichiers suivants sont des ajouts incrémentiels au jeu de données depuis l’exportation précédente. Vous pouvez également sélectionner **[!UICONTROL Export full files]**. Dans ce cas, sélectionnez la fréquence **[!UICONTROL Once]** pour une exportation complète unique du jeu de données.

>[!IMPORTANT]
>
>La première exportation de fichier incrémentiel inclut toutes les données existantes dans le jeu de données, agissant comme un renvoi. L’exportation peut contenir un ou plusieurs fichiers.

![Workflow d’exportation de jeu de données présentant l’étape de planification.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilisez le sélecteur **[!UICONTROL Frequency]** pour sélectionner la fréquence d’exportation :

   * **[!UICONTROL Daily]** : planification d’exportations de fichiers incrémentiels une fois par jour, tous les jours, au moment choisi.
   * **[!UICONTROL Hourly]** : planification d’exportations de fichiers incrémentiels toutes les 3, 6, 8 ou 12 heures.

2. Utilisez le sélecteur **[!UICONTROL Time]** pour choisir l’heure de la journée à laquelle l’exportation doit avoir lieu, au format [!DNL UTC].

3. Utilisez le sélecteur **[!UICONTROL Date]** pour choisir l’intervalle à partir duquel l’exportation doit avoir lieu.

4. Sélectionnez **[!UICONTROL Save]** pour enregistrer le planning et passer à l’étape **[!UICONTROL Review]**.

>[!NOTE]
> 
>Pour les exportations de jeu de données, les noms de fichiers ont un paramètre prédéfini, format par défaut, qui ne peut être modifié. Voir la section [Vérification de l’exportation réussie d’un jeu de données](#verify) pour plus d’informations et d’exemples de fichiers exportés.

## Modifier le chemin du dossier {#edit-folder-path}

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="Modifier le chemin du dossier"
>abstract="Utilisez plusieurs macros fournies pour personnaliser le chemin du dossier dans lequel le jeu de données est exporté."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="Aperçu du chemin du dossier du jeu de données"
>abstract="Obtenez un aperçu de la structure de dossiers créée à l’emplacement de stockage en fonction des macros que vous avez ajoutées dans cette fenêtre."

Sélectionnez **[!UICONTROL Edit folder path]** pour personnaliser la structure de dossiers de l’emplacement de stockage où les jeux de données exportés sont déposés.

![Modifier le contrôle du chemin d’accès au dossier mis en surbrillance à l’étape de planification.](/help/destinations/assets/ui/export-datasets/edit-folder-path.png)

Vous pouvez utiliser plusieurs macros disponibles pour personnaliser le nom de dossier de votre choix. Double-cliquez sur une macro pour l’ajouter au chemin du dossier et utilisez des `/` entre les macros pour séparer les dossiers.

![Sélection des macros mise en surbrillance dans la fenêtre modale du dossier personnalisé.](/help/destinations/assets/ui/export-datasets/custom-folder-path-macros.png)

Après avoir sélectionné les macros souhaitées, vous pouvez voir un aperçu de la structure de dossiers qui sera créée à votre emplacement de stockage. Le premier niveau de la structure de dossiers représente le **[!UICONTROL Folder path]** que vous avez indiqué lorsque vous [êtes connecté à la destination](/help/destinations/ui/connect-destination.md#set-up-connection-parameters) pour exporter des jeux de données.

![Aperçu du chemin du dossier mis en surbrillance dans la fenêtre modale du dossier personnalisé.](/help/destinations/assets/ui/export-datasets/custom-folder-path-preview.png)

### Bonnes pratiques de gestion de plusieurs jeux de données {#best-practices-multiple-datasets}

Lors de l’exportation de plusieurs jeux de données, tenez compte des bonnes pratiques suivantes :

* **Mêmes exigences de planification** : regroupez les jeux de données ayant besoin du même planning d’exportation (fréquence, type) dans un seul flux de données pour une gestion plus facile.
* **Exigences de planification différentes** : créez des flux de données distincts pour les jeux de données qui nécessitent des planifications d’exportation ou des types d’exportation différents (incrémentiel ou complet). Chaque jeu de données est ainsi exporté en fonction de ses besoins spécifiques.
* **Vérifier avant de modifier** : avant de modifier le planning sur un flux de données existant, vérifiez les jeux de données qui sont déjà exportés par ce flux de données pour éviter toute modification involontaire de leur comportement d’exportation.
* **Documentez votre configuration** : suivez les jeux de données dans les flux de données, en particulier lors de la gestion de plusieurs plannings d’exportation sur différentes destinations.

## Réviser {#review}

Sur la page **[!UICONTROL Review]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Cancel]** pour interrompre le flux, **[!UICONTROL Back]** pour modifier vos paramètres ou **[!UICONTROL Finish]** pour confirmer votre sélection et commencer à exporter des jeux de données vers la destination.

![Workflow d’exportation des jeux de données présentant l’étape de révision.](/help/destinations/assets/ui/export-datasets/review.png)

## Vérifier l’exportation réussie d’un jeu de données {#verify}

Lors de l’exportation de jeux de données, Experience Platform crée un ou plusieurs fichiers `.json` ou `.parquet` dans l’emplacement de stockage que vous avez fourni. Attendez-vous à ce que de nouveaux fichiers soient déposés dans votre emplacement de stockage en fonction du planning d’exportation que vous avez fourni.

Experience Platform crée une structure de dossiers dans l’emplacement de stockage que vous avez spécifié, où il dépose les fichiers de jeu de données exportés. Le modèle d’exportation de dossier par défaut est illustré ci-dessous, mais vous pouvez [ personnaliser la structure de dossiers à l’aide de vos macros préférées](#edit-folder-path).

>[!TIP]
> 
>Le premier niveau de cette structure de dossiers, `folder-name-you-provided`, représente le **[!UICONTROL Folder path]** que vous avez indiqué lorsque vous [connecté à la destination](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) pour exporter des jeux de données.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Le nom de fichier par défaut est généré de manière aléatoire pour garantir que les noms de fichier exportés soient uniques.

### Exemples de fichiers de jeu de données {#sample-files}

La présence de ces fichiers dans votre emplacement de stockage confirme que l’export a été réalisé avec succès. Pour comprendre la structure des fichiers exportés, vous pouvez télécharger un exemple de [fichier parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) ou de [fichier JSON](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Fichiers de jeu de données compressés {#compressed-dataset-files}

Dans le workflow [Se connecter à la destination](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), vous pouvez sélectionner les fichiers de jeu de données exportés à compresser, comme illustré ci-dessous :

![Sélection du type de fichier et de la compression lors de la connexion à une destination pour exporter des jeux de données.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Notez la différence de format de fichier entre les deux types de fichiers lorsqu’ils sont compressés :

* Lors de l’exportation de fichiers JSON compressés, le format du fichier exporté est `json.gz`. Le format du fichier JSON exporté est NDJSON, qui est le format d’échange standard dans l’écosystème de Big Data. Adobe recommande d’utiliser un client compatible NDJSON pour lire les fichiers exportés.
* Lors de l&#39;exportation de fichiers parquet compressés, le format de fichier exporté est `gz.parquet`

Les exportations vers des fichiers JSON sont prises en charge *en mode compressé uniquement*. Les exportations vers les fichiers Parquet sont prises en charge en mode compressé et non compressé.

## Supprimer des jeux de données des destinations {#remove-dataset}

Pour supprimer des jeux de données d’un flux de données existant, procédez comme suit :

1. Connectez-vous à l’[interface utilisateur d’Experience Platform](https://experience.adobe.com/platform/) puis sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Browse]** dans l’en-tête supérieur pour afficher vos flux de données de destination existants.

   ![La vue de navigation de destination avec une connexion de destination affichée et le reste s’est estompée.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

2. Dans la colonne **[!UICONTROL Activation data]** , sélectionnez le contrôle des jeux de données pour afficher tous les jeux de données mappés à ce flux de données d’exportation.

   ![L’option de navigation des jeux de données disponibles est affichée en surbrillance dans la colonne Données d’activation.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. La page **[!UICONTROL Activation data]** de la destination s’affiche. Utilisez les cases à cocher situées sur le côté gauche de la liste des jeux de données pour sélectionner les jeux de données à supprimer, puis sélectionnez **[!UICONTROL Remove datasets]** dans le rail de droite pour déclencher la boîte de dialogue de confirmation de suppression du jeu de données.

   ![Boîte de dialogue Supprimer le jeu de données présentant la commande Supprimer le jeu de données dans le rail de droite.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. Dans la boîte de dialogue de confirmation, sélectionnez **[!UICONTROL Remove]** pour supprimer immédiatement le jeu de données des exportations vers la destination.

   ![Boîte de dialogue présentant l’option Confirmer la suppression du jeu de données du flux de données.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Droits d’exportation de jeux de données {#licensing-entitlement}

Reportez-vous aux documents de description du produit pour connaître la quantité de données que vous êtes autorisé à exporter pour chaque application Experience Platform, par an. Par exemple, vous pouvez afficher la description du produit Real-Time CDP [ici](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

Notez que les droits d’exportation de données pour différentes applications ne s’additionnent pas. Par exemple, cela signifie que si vous achetez Real-Time CDP Ultimate et Adobe Journey Optimizer Ultimate, le droit d’exportation du profil sera le plus grand des deux droits, conformément aux descriptions des produits. Vos droits de volume sont calculés en multipliant le nombre total de profils sous licence par 500 Ko pour Real-Time CDP Prime ou 700 Ko pour Real-Time CDP Ultimate afin de déterminer le volume de données auquel vous avez droit.

D’un autre côté, si vous avez acheté des modules complémentaires tels que Data Distiller, la limite d’exportation des données à laquelle vous avez droit représente la somme du niveau de produit et du module complémentaire.

Vous pouvez afficher et suivre les exportations de votre profil par rapport à vos limites contractuelles dans le tableau de bord [utilisation des licences](/help/landing/license-usage-and-guardrails/license-usage-dashboard.md).

## Limites connues {#known-limitations}

Gardez à l’esprit les limites suivantes pour la mise à disposition générale des exportations de jeux de données :

* Experience Platform peut exporter plusieurs fichiers, même pour de petits jeux de données. L’exportation des jeux de données est conçue pour une intégration système à système et optimisée pour les performances. Par conséquent, le nombre de fichiers exportés n’est pas personnalisable.
* Les noms des fichiers exportés ne sont actuellement pas personnalisables.
* Actuellement, l’interface utilisateur ne vous empêche pas de supprimer un jeu de données en cours d’exportation vers une destination. Ne supprimez aucun jeu de données en cours d’exportation vers des destinations. [Supprimez le jeu de données](#remove-dataset) d’un flux de données de destination avant de le supprimer.
* Les mesures de surveillance des exportations de jeux de données sont actuellement combinées avec les chiffres des exportations de profils afin qu’elles ne reflètent pas les vrais chiffres d’exportation.
* Les données dont la date et l’heure sont antérieures à 365 jours sont exclues des exportations de jeux de données. Pour plus d’informations, consultez les [mécanismes de sécurisation pour les exportations de jeux de données planifiées](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)

## Questions fréquentes {#faq}

**Pouvons-nous générer un fichier sans dossier si nous enregistrons simplement à `/` comme chemin d’accès au dossier ? En outre, si nous n’avons pas besoin d’un chemin de dossier, comment les fichiers aux noms en double seront-ils générés dans un dossier ou un emplacement ?**

+++Réponse
À compter de la version de septembre 2024, il est possible de personnaliser le nom du dossier et même d’utiliser `/` pour exporter des fichiers pour tous les jeux de données d’un même dossier. Adobe ne le recommande pas pour les destinations qui exportent plusieurs jeux de données, car les noms de fichiers générés par le système et appartenant à différents jeux de données seront mélangés dans le même dossier.
+++

**Pouvez-vous acheminer le fichier manifeste vers un dossier et les fichiers de données vers un autre dossier ?**

+++Réponse
Non, il n&#39;est pas possible de copier le fichier manifeste vers un autre emplacement.
+++

**Pouvons-nous contrôler le séquencement ou le timing de la diffusion des fichiers ?**

+++Réponse
Il existe des options pour planifier l’exportation. Il n’existe aucune option pour retarder ou séquencer la copie des fichiers. Ils sont copiés vers votre emplacement de stockage dès qu’ils sont générés.
+++

**Quels formats sont disponibles pour le fichier manifeste ?**

+++Réponse
Le fichier manifeste est au format .json.
+++

**Existe-t-il une disponibilité d’API pour le fichier manifeste ?**

+++Réponse
Aucune API n’est disponible pour le fichier manifeste, mais elle inclut une liste de fichiers comprenant l’exportation.
+++

**Pouvons-nous ajouter des détails supplémentaires au fichier manifeste (c.-à-d. le nombre d’enregistrements) ? Si oui, comment ?**

+++Réponse
Il n&#39;est pas possible d&#39;ajouter des informations supplémentaires au fichier manifeste. Le nombre d’enregistrements est disponible via l’entité `flowRun` (interrogeable via l’API). En savoir plus sur la surveillance des destinations.
+++

**Comment les fichiers de données sont-ils divisés ? Combien d’enregistrements par fichier ?**

+++Réponse
Les fichiers de données sont fractionnés selon le partitionnement par défaut dans le lac de données Experience Platform. Les jeux de données plus volumineux comportent un plus grand nombre de partitions. Le partitionnement par défaut n’est pas configurable par l’utilisateur, car il est optimisé pour la lecture.
+++

**Peut-on fixer un seuil (nombre d&#39;enregistrements par fichier) ?**

+++Réponse
Non, c&#39;est impossible.
+++

**Comment renvoyer un jeu de données si l’envoi initial est incorrect ?**

+++Réponse
Des reprises sont automatiquement en place pour la plupart des types d’erreurs système.
+++

**Puis-je définir différents plannings d’exportation pour différents jeux de données dans le même flux de données ?**

+++Réponse
Non, tous les jeux de données d’un seul flux de données partagent le même planning d’exportation. Si vous avez besoin de plannings d’exportation différents pour différents jeux de données, vous devez créer des flux de données distincts (connexions de destination) pour chaque type de planning. Par exemple, si vous souhaitez que le jeu de données A soit exporté de manière incrémentielle tous les jours et que le jeu de données B soit exporté en tant qu’exportation complète unique, vous devez créer deux flux de données distincts.
+++
