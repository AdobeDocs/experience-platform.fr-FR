---
title: Exportation de jeux de données vers des destinations de stockage dans le cloud
type: Tutorial
description: Découvrez comment exporter des jeux de données d’Adobe Experience Platform vers l’emplacement d’espace de stockage de votre choix.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 9d3b6409013edc38ef41dd2a184ccbdcf7ab9edd
workflow-type: tm+mt
source-wordcount: '1891'
ht-degree: 47%

---

# Exportation des jeux de données vers des destinations de stockage dans le cloud

>[!AVAILABILITY]
>
>* Cette fonctionnalité est disponible pour les clients qui ont acheté le package Real-Time CDP Prime ou Ultimate, Adobe Journey Optimizer ou Customer Journey Analytics. Pour plus d’informations, contactez votre représentant d’Adobe.

Cet article explique le processus requis pour exporter des [jeux de données](/help/catalog/datasets/overview.md) de Adobe Experience Platform vers l’emplacement de stockage dans le cloud de votre choix, par exemple [!DNL Amazon S3], des emplacements SFTP ou [!DNL Google Cloud Storage] à l’aide de l’interface utilisateur Experience Platform.

Vous pouvez également utiliser les API Experience Platform pour exporter des jeux de données. Pour plus d’informations, consultez le [tutoriel sur l’API d’exportation de jeux de données](/help/destinations/api/export-datasets.md) .

## Jeux de données disponibles pour l’exportation {#datasets-to-export}

Les jeux de données que vous pouvez exporter dépendent de l’application Experience Platform (Real-Time CDP, Adobe Journey Optimizer), du niveau (Prime ou Ultimate) et des modules complémentaires achetés (par exemple : Data Distiller).

Identifiez dans le tableau ci-dessous les types de jeux de données que vous pouvez exporter en fonction de votre application, du niveau du produit et des modules complémentaires achetés :

<table>
<thead>
  <tr>
    <th>Application/module complémentaire</th>
    <th>Niveau</th>
    <th>Jeux de données disponibles pour l’exportation</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Jeux de données Profile et Experience Event créés dans l’interface utilisateur de l’Experience Platform après ingestion ou collecte de données par le biais de sources, SDK web, SDK mobile, Analytics Data Connector et Audience Manager.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Jeux de données Profile et Experience Event créés dans l’interface utilisateur de l’Experience Platform après ingestion ou collecte de données par le biais de sources, SDK web, SDK mobile, Analytics Data Connector et Audience Manager.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets"> Jeu de données d’instantanés de profil généré par le système </a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Reportez-vous à la documentation <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> .</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Reportez-vous à la documentation <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> .</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Toutes</td>
    <td> Jeux de données Profile et Experience Event créés dans l’interface utilisateur de l’Experience Platform après ingestion ou collecte de données par le biais de sources, SDK web, SDK mobile, Analytics Data Connector et Audience Manager.  <br> <p> <b>Remarque sur la disponibilité :</b> La possibilité d’exporter des jeux de données vers le cloud est en phase de test limité de la version et peut ne pas être encore disponible dans votre environnement. Cette note sera supprimée lorsque la fonctionnalité sera disponible. Pour plus d’informations sur le processus de publication du Customer Journey Analytics, voir <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/releases/releases.html"> versions des fonctionnalités du Customer Journey Analytics</a>. </p> </td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Distiller de données (module complémentaire)</td>
    <td>Jeux de données dérivés créés via Query Service.</td>
  </tr>
</tbody>
</table>

## Tutoriel vidéo {#video-tutorial}

Regardez la vidéo ci-dessous pour obtenir une explication de bout en bout du workflow décrit sur cette page, les avantages de l’utilisation de la fonctionnalité d’exportation de jeux de données et quelques cas d’utilisation suggérés.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## Destinations prises en charge {#supported-destinations}

Actuellement, vous pouvez exporter des jeux de données vers les destinations de stockage dans le cloud mises en évidence dans la capture d’écran et répertoriées ci-dessous.

![Page du catalogue des destinations montrant les destinations qui prennent en charge les exportations de jeux de données.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Quand activer des audiences ou exporter des jeux de données {#when-to-activate-audiences-or-activate-datasets}

Certaines destinations basées sur des fichiers du catalogue de l’Experience Platform prennent en charge l’activation de l’audience et l’exportation de jeux de données.

* Envisagez d’activer des audiences lorsque vous souhaitez que vos données soient structurées en profils regroupés par intérêt ou qualification d’audience.
* Vous pouvez également envisager des exportations de jeux de données lorsque vous cherchez à exporter des jeux de données bruts, qui ne sont pas groupés ou structurés par intérêt ou qualification d’audience. Vous pouvez utiliser ces données pour la création de rapports, des workflows de science des données et de nombreux autres cas d’utilisation. Par exemple, en tant qu’administrateur, ingénieur de données ou analyste, vous pouvez exporter des données d’Experience Platform pour les synchroniser avec votre entrepôt de données, les utiliser dans des outils d’analyse de BI, des outils ML externes dans le cloud ou les stocker dans votre système pour des besoins de stockage à long terme.

Ce document contient toutes les informations nécessaires à l’exportation de jeux de données. Si vous souhaitez activer *audiences* vers des destinations de stockage dans le cloud ou de marketing par e-mail, lisez [ Activer les données d’audience vers des destinations d’exportation de profil de lot](/help/destinations/ui/activate-batch-profile-destinations.md).

## Conditions préalables {#prerequisites}

Pour exporter des jeux de données vers des destinations d’espace de stockage, vous devez vous être [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

### Autorisations nécessaires {#permissions}

Pour exporter des jeux de données, vous avez besoin des ****, **[!UICONTROL d’afficher les jeux de données]** et **[!UICONTROL de]** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès pour  gérer et activer les destinations de jeu de données. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour exporter des jeux de données et que la destination prend en charge l’exportation de jeux de données, parcourez le catalogue des destinations. Si une destination comporte un contrôle **[!UICONTROL Activer]** ou **[!UICONTROL Exporter des jeux de données]**, vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer]** ou **[!UICONTROL Exporter des jeux de données]** sur la vignette correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

   ![Onglet Catalogue de destinations avec le contrôle Activer mis en surbrillance.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Sélectionnez **[!UICONTROL Type de données des jeux de données]** et sélectionnez la connexion de destination vers laquelle vous souhaitez exporter les jeux de données, puis sélectionnez **[!UICONTROL Suivant]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour exporter des jeux de données, sélectionnez **[!UICONTROL Configurer une nouvelle destination]** pour déclencher le workflow [Se connecter à la destination](/help/destinations/ui/connect-destination.md).

![Workflow d’activation de destination avec le contrôle Jeux de données mis en surbrillance.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. La vue **[!UICONTROL Sélectionner des jeux de données]** apparaît. Passez à la section suivante pour [sélectionner vos jeux de données](#select-datasets) pour l’exportation.

## Sélectionner vos jeux de données {#select-datasets}

Utilisez les cases à cocher situées à gauche des jeux de données pour sélectionner les jeux de données que vous souhaitez exporter vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Workflow d’exportation des jeux de données présentant l’étape de sélection des jeux de données permettant de sélectionner les jeux de données à exporter.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Planifier l’exportation des jeux de données {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Options d’exportation de fichiers pour les jeux de données"
>abstract="Sélectionnez **Exporter des fichiers incrémentiels** pour n’exporter que les données ajoutées au jeu de données depuis la dernière exportation. <br> La première exportation de fichier incrémentiel inclut toutes les données du jeu de données, agissant comme un renvoi. Les futurs fichiers incrémentiels incluent uniquement les données qui ont été ajoutées au jeu de données depuis la première exportation."

À l’étape **[!UICONTROL Planification]** , vous pouvez définir une date de début et une cadence d’exportation pour vos exportations de jeux de données.

L’option **[!UICONTROL Exporter des fichiers incrémentiels]** est automatiquement sélectionnée. Cela déclenche l’exportation d’un ou de plusieurs fichiers représentant un instantané complet du jeu de données. Les fichiers suivants sont des ajouts incrémentiels au jeu de données depuis l’exportation précédente.

>[!IMPORTANT]
>
>La première exportation de fichier incrémentiel inclut toutes les données existantes dans le jeu de données, en tant que renvoi. L’exportation peut contenir un ou plusieurs fichiers.

![Workflow d’exportation de jeu de données présentant l’étape de planification.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilisez le sélecteur **[!UICONTROL Fréquence]** pour sélectionner la fréquence d’exportation :

   * **[!UICONTROL Tous les jours]** : planification d’exportations de fichiers incrémentiels une fois par jour, tous les jours, au moment choisi.
   * **[!UICONTROL Par heure]** : planification d’exportations de fichiers incrémentiels toutes les 3, 6, 8 ou 12 heures.

2. Utilisez le sélecteur **[!UICONTROL Heure]** pour choisir l’heure de la journée, au format [!DNL UTC], à laquelle l’exportation doit avoir lieu.

3. Utilisez le sélecteur **[!UICONTROL Date]** pour choisir l’intervalle au cours duquel l’exportation doit avoir lieu. Notez que vous ne pouvez actuellement pas définir de date de fin pour les exportations. Pour plus d’informations, voir la section [limitations connues](#known-limitations).

4. Sélectionnez **[!UICONTROL Suivant]** pour enregistrer la planification et passer à la l’étape **[!UICONTROL Révision]**.

>[!NOTE]
> 
>Pour les exportations de jeu de données, les noms de fichiers ont un paramètre prédéfini, format par défaut, qui ne peut être modifié. Voir la section [Vérification de l’exportation réussie d’un jeu de données](#verify) pour plus d’informations et d’exemples de fichiers exportés.

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les jeux de données à la destination.

![Workflow d’exportation des jeux de données présentant l’étape de révision.](/help/destinations/assets/ui/export-datasets/review.png)

## Vérifier l’exportation réussie d’un jeu de données {#verify}

Lors de l’exportation de jeux de données, Experience Platform crée un ou plusieurs fichiers `.json` ou `.parquet` dans l’emplacement de stockage que vous avez fourni. Attendez-vous à ce que les nouveaux fichiers soient déposés dans votre emplacement de stockage en fonction du planning d’exportation que vous avez fourni.

Experience Platform crée une structure de dossiers dans l’emplacement de stockage que vous avez spécifié, où il dépose les fichiers de jeu de données exportés. Un nouveau dossier est créé pour chaque heure d’exportation, selon le modèle ci-dessous :

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Le nom de fichier par défaut est généré de manière aléatoire pour garantir que les noms de fichier exportés soient uniques.

### Exemples de fichiers de jeu de données {#sample-files}

La présence de ces fichiers dans votre emplacement de stockage confirme que l’activation a été réalisée avec succès. Pour comprendre la structure des fichiers exportés, vous pouvez télécharger un exemple de [fichier parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) ou de [fichier JSON](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### Fichiers de jeux de données compressés {#compressed-dataset-files}

Dans le [workflow de connexion à la destination](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), vous pouvez sélectionner les fichiers de jeu de données exportés à compresser, comme illustré ci-dessous :

![ Sélection du type de fichier et de la compression lors de la connexion à une destination pour exporter des jeux de données.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Notez la différence de format de fichier entre les deux types de fichiers, lorsqu’ils sont compressés :

* Lors de l’exportation de fichiers JSON compressés, le format de fichier exporté est `json.gz`
* Lors de l’exportation de fichiers parquet compressés, le format de fichier exporté est `gz.parquet`

## Suppression des jeux de données des destinations {#remove-dataset}

Pour supprimer des jeux de données d’un flux de données existant, procédez comme suit :

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://experience.adobe.com/platform/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos flux de données de destination existants.

   ![La vue de navigation de destination avec une connexion de destination affichée et le reste s’est estompée.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Sélectionnez l’icône filtre ![Icône Filtre](../assets/ui/edit-activation/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

1. Dans la colonne **[!UICONTROL Données d’activation]**, sélectionnez le contrôle des jeux de données pour afficher tous les jeux de données mappés à ce flux de données d’exportation.

   ![L’option de navigation des jeux de données disponibles est affichée en surbrillance dans la colonne Données d’activation.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. [!BADGE Beta] La page **[!UICONTROL Données d’activation]** de la destination apparaît. Utilisez les cases à cocher situées à gauche de la liste des jeux de données pour sélectionner les jeux de données à supprimer, puis sélectionnez **[!UICONTROL Supprimer les jeux de données]** dans le rail de droite pour déclencher la boîte de dialogue de confirmation de suppression des jeux de données.

   >[!NOTE]
   >
   >Cette fonctionnalité est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès à cette fonctionnalité, contactez votre représentant Adobe.

   ![Boîte de dialogue Supprimer le jeu de données présentant la commande Supprimer le jeu de données dans le rail de droite.](../assets/ui/export-datasets/bulk-remove-datasets.png)

1. Dans la boîte de dialogue de confirmation, sélectionnez **[!UICONTROL Supprimer]** pour supprimer immédiatement le jeu de données des exportations vers la destination.

   ![Boîte de dialogue présentant l’option Confirmer la suppression du jeu de données du flux de données.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Droits d’exportation des jeux de données {#licensing-entitlement}

Consultez les documents de description du produit pour comprendre la quantité de données que vous êtes autorisé à exporter pour chaque application Experience Platform, par an. Par exemple, vous pouvez afficher la description du produit Real-Time CDP [ici](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

Notez que les droits à l’exportation des données pour différentes applications ne sont pas additifs. Par exemple, cela signifie que si vous achetez Real-Time CDP Ultimate et Adobe Journey Optimizer Ultimate, les droits d’exportation de profil seront les plus grands des deux droits, selon les descriptions de produit. Vos droits sur le volume sont calculés en prenant le nombre total de profils sous licence et en multipliant par 500 Ko pour Real-Time CDP Prime ou 700 Ko pour Real-Time CDP Ultimate afin de déterminer le volume de données auquel vous avez droit.

D’un autre côté, si vous avez acheté des modules complémentaires tels que Data Distiller, la limite d’exportation des données à laquelle vous avez droit représente la somme du niveau produit et du module complémentaire.

Dans le tableau de bord des licences, vous pouvez consulter et suivre vos exportations de profils par rapport à vos limites contractuelles.

## Limites connues {#known-limitations}

Gardez à l’esprit les limites suivantes relatives à la disponibilité générale des exportations de jeux de données :

* Actuellement, vous ne pouvez exporter que des fichiers incrémentiels et il est impossible de sélectionner une date de fin pour vos exportations de jeux de données.
* Les noms des fichiers exportés ne peuvent actuellement pas être personnalisés.
* Les jeux de données créés via l’API ne sont actuellement pas disponibles pour l’exportation.
* Actuellement, l’interface utilisateur ne vous empêche pas de supprimer un jeu de données en cours d’exportation vers une destination. Ne supprimez aucun jeu de données en cours d’exportation vers des destinations. [Supprimez le jeu de données](#remove-dataset) d’un flux de données de destination avant de le supprimer.
* Les mesures de surveillance des exportations de jeux de données sont actuellement combinées avec les chiffres des exportations de profils afin qu’elles ne reflètent pas les vrais chiffres d’exportation.
* Les données dont l’horodatage est antérieur à 365 jours sont exclues des exportations de jeux de données. Pour plus d’informations, consultez les [barrières de sécurité pour les exportations de jeux de données planifiées](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)
