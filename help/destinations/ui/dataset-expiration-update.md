---
title: Étendre les plannings d’exportation de jeux de données pour les flux de données créés avant novembre 2024
description: Découvrez comment étendre le planning d’exportation des flux de données d’exportation de jeux de données créés avant novembre 2024 qui cesseront de fonctionner le 1er septembre 2025.
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 6f8b906729ec31cc0c4847ccd0ae0f89f63a1627
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# Étendre les plannings d’exportation de jeux de données pour les flux de données créés avant novembre 2024

>[!IMPORTANT]
>
>**Action requise** : si votre organisation dispose de [flux de données d’exportation de jeux de données](export-datasets.md) créés avant novembre 2024, ces flux de données cesseront de fonctionner le 1er septembre 2025. Ce guide explique comment étendre le planning d’exportation au-delà de cette date pour les flux de données que vous souhaitez conserver.

## Vue d’ensemble {#overview}

Dans la version [septembre 2024 d’Experience Platform](/help/release-notes/2024/september-2024.md#destinations), Adobe a introduit une date de fin par défaut du **1er mai 2025** pour tous les flux de données d’exportation de jeux de données créés avant la version de septembre 2024.

**Cette date a depuis été mise à jour au 1er septembre 2025** pour tous les flux de données d’exportation de jeux de données créés **avant novembre 2024**.

Les flux de données d’exportation de jeux de données créés avant novembre 2024 cesseront d’exporter des données le **1er septembre 2025** sauf si vous étendez manuellement leur date d’expiration.

Si vous avez besoin des flux de données pour continuer à exporter des données après le **1er septembre 2025**, vous devez étendre leurs plannings pour chaque destination vers laquelle vous exportez des jeux de données, en suivant les étapes de ce guide.

## Destinations affectées {#affected-destinations}

Votre organisation peut avoir des flux de données d’exportation de jeux de données actifs qui envoient des données aux destinations répertoriées ci-dessous. Suivez les étapes des sections suivantes et regardez la vidéo de présentation pour savoir comment identifier les jeux de données qui vont expirer.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## Tutoriel vidéo {#video}

Regardez la vidéo ci-dessous pour une démonstration détaillée de la manière d’identifier les exportations de jeux de données avec les dates de fin à venir et d’étendre le planning d’exportation des flux de données que vous souhaitez conserver.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## Étape 1 : identifier les flux de données affectés {#identify-dataflows}

Avant d’étendre le planning d’exportation de vos flux de données d’exportation de jeux de données, vous devez d’abord identifier les flux de données qui sont affectés par la date d’expiration à venir. Suivez les étapes ci-dessous pour localiser les flux de données qui nécessitent une action.

1. Accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]** dans l’interface utilisateur d’Experience Platform.
2. Sélectionnez **[!UICONTROL Activer]** sur une destination qui comporte des flux de données d’exportation de jeux de données actifs.

   >[!TIP]
   >
   >Utilisez le filtre **[!UICONTROL Types de données]** sur le côté gauche du catalogue pour filtrer les destinations disponibles par **[!UICONTROL Jeux de données]**.

3. Sélectionnez le type de données **[!UICONTROL Jeux de données]** pour afficher uniquement les flux de données avec des exportations de jeux de données.
   ![Capture d’écran montrant comment filtrer les flux de données par type de données.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. Sélectionnez l’en-tête de colonne **[!UICONTROL Créé]** et choisissez **[!UICONTROL Trier par ordre croissant]** pour afficher les flux de données plus anciens.
   ![Capture d’écran montrant comment trier les flux de données par ordre croissant.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. Identifiez le flux de données créé avant novembre 2024 que vous souhaitez conserver.

## Étape 2 : accéder au workflow d’exportation des jeux de données {#access-workflow}

Pour chaque flux de données que vous souhaitez conserver, vous devez accéder au workflow d’exportation des jeux de données pour modifier le planning.

1. Sélectionnez le nom du flux de données dans la colonne **[!UICONTROL Nom]**. Vous accédez alors à la page **[!UICONTROL Exécutions de flux de données]**.
2. Sur cette page, sélectionnez l’option **[!UICONTROL Exporter les jeux de données]**.
   ![Capture d’écran affichant l’option Exporter les jeux de données dans la page exécutions de flux de données.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. Sur la page **[!UICONTROL Sélectionner des jeux de données]**, sélectionnez **[!UICONTROL Suivant]**. Vous n’avez pas besoin d’ajouter de nouveaux jeux de données au flux de données.
4. Vous accédez alors à la page **[!UICONTROL Planification]** où vous pouvez également voir une notification vous informant de la date d’expiration de l’exportation du jeu de données.
   ![Flux de données d’exportation de jeux de données avec notification d’expiration](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## Étape 3 : Étendre le planning d’exportation {#extend-export-schedule}

Vous pouvez maintenant modifier le planning d’exportation pour l’étendre au-delà du 1er septembre 2025.

1. Sélectionnez **[!UICONTROL Modifier le planning]**.
   ![Capture d’écran de l’étape Planification affichant le bouton Modifier le planning.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. Sélectionnez un nouveau planning d’exportation, puis sélectionnez **[!UICONTROL Enregistrer]**.
   ![Capture d’écran de l’étape Planification affichant les options de planification.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >Consultez la [documentation sur l’exportation des jeux de données](export-datasets.md#scheduling) pour obtenir des conseils détaillés sur la configuration des plannings d’exportation des jeux de données.

## Que se passera-t-il si je ne respecte pas la date limite du 1er septembre 2025 ? {#missed-deadline}

Si vos flux de données d’exportation de jeux de données expirent le 1er septembre 2025 et que vous n’avez pas étendu leurs plannings, il existe une période de grâce de **30 jours** pendant laquelle vous pouvez contacter Adobe pour réactiver vos flux de données sans perte de données. Cela inclut les données qui n’ont pas été exportées entre le 1er septembre et la date à laquelle vous avez contacté Adobe.

>[!IMPORTANT]
>
>Bien qu’Adobe offre cette période de grâce, nous vous recommandons vivement d’étendre vos plannings avant l’échéance du 1er septembre 2025 afin d’assurer la continuité des exportations de données et d’éviter toute interruption de service potentielle.
