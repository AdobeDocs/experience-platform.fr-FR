---
title: (Version bêta) Exportation de jeux de données vers des destinations de stockage dans le cloud
type: Tutorial
description: Découvrez comment exporter des jeux de données de Adobe Experience Platform vers l’emplacement de stockage dans le cloud de votre choix.
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 9%

---

# (Version bêta) Exportation des jeux de données vers les destinations de stockage dans le cloud

>[!IMPORTANT]
>
>* La fonctionnalité d’exportation des jeux de données est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.
>* Cette fonctionnalité bêta prend en charge l’exportation des données de première génération, comme défini dans Real-time Customer Data Platform. [description du produit](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Cette fonctionnalité est disponible pour les clients qui ont acheté les packages Real-Time CDP Prime et Ultimate. Veuillez contacter votre représentant Adobe pour plus d’informations.


Cet article explique le workflow requis pour l’exportation [jeux de données](/help/catalog/datasets/overview.md) de Adobe Experience Platform à l’emplacement de stockage de votre choix dans le cloud, par exemple [!DNL Amazon S3], emplacements SFTP ou [!DNL Google Cloud Storage].

## Quand activer des segments ou exporter des jeux de données {#when-to-activate-segments-or-activate-datasets}

Certaines destinations basées sur des fichiers du catalogue de l’Experience Platform prennent en charge l’activation des segments et l’exportation des jeux de données.

* Envisagez d’activer des segments lorsque vous souhaitez que vos données soient structurées en profils regroupés par intérêt ou qualification d’audience.
* Vous pouvez également envisager des exportations de jeux de données lorsque vous cherchez à exporter des jeux de données bruts, qui ne sont pas groupés ou structurés par les intérêts ou les qualifications de l’audience. Vous pouvez utiliser ces données pour la création de rapports, les workflows de science des données, afin de répondre aux exigences de conformité et de nombreux autres cas d’utilisation.

Ce document contient toutes les informations nécessaires à l’exportation des jeux de données. Si vous souhaitez activer des segments vers des destinations de stockage dans le cloud ou de marketing par e-mail, lisez [Activation des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md).

## Conditions préalables {#prerequisites}

Pour exporter des jeux de données vers des destinations de stockage dans le cloud, vous devez avoir réussi [connecté à une destination](./connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser.

### Autorisations nécessaires {#permissions}

Pour exporter des jeux de données, vous avez besoin de la variable **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, et **[!UICONTROL Gestion et activation des destinations de jeu de données]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour exporter des jeux de données et que la destination prend en charge l’exportation de jeux de données, parcourez le catalogue des destinations. Si une destination comporte une variable **[!UICONTROL Activer]** ou **[!UICONTROL Exportation de jeux de données]** contrôle, puis vous disposez des autorisations appropriées.

## Sélectionnez votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connexions et destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destination avec la commande Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Sélectionner **[!UICONTROL Activer]** ou **[!UICONTROL Exportation de jeux de données]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

   ![Onglet Catalogue de destinations avec l’option Activer le contrôle mise en surbrillance.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Sélectionner **[!UICONTROL Jeux de données de type données]** et sélectionnez la connexion de destination vers laquelle vous souhaitez exporter les jeux de données, puis sélectionnez **[!UICONTROL Suivant]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour exporter des jeux de données, sélectionnez **[!UICONTROL Configuration d’une nouvelle destination]** pour déclencher la variable [Se connecter à la destination](/help/destinations/ui/connect-destination.md) workflow.

![Workflow d’activation de la destination avec le contrôle Jeux de données en surbrillance.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. Le **[!UICONTROL Sélectionner des jeux de données]** s’affiche. Passez à la section suivante pour [sélectionner vos jeux de données ;](#select-datasets) pour l’exportation.

## Sélectionner vos jeux de données {#select-datasets}

Utilisez les cases à cocher situées à gauche des noms des jeux de données pour sélectionner les jeux de données à exporter vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

![Workflow d’exportation des jeux de données présentant l’étape Sélectionner les jeux de données permettant de sélectionner les jeux de données à exporter.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Planification de l’exportation des jeux de données {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Options d’exportation de fichiers pour les jeux de données"
>abstract="Sélectionner **Exportation de fichiers incrémentiels** pour n’exporter que les données ajoutées au jeu de données depuis la dernière exportation. <br> La première exportation incrémentielle de fichier inclut toutes les données du jeu de données, agissant comme un renvoi. Les futurs fichiers incrémentiels incluent uniquement les données qui ont été ajoutées au jeu de données depuis la première exportation."

Dans le **[!UICONTROL Planification]** vous pouvez définir une date de début et une cadence d’exportation pour vos exportations de jeux de données.

Le **[!UICONTROL Exportation de fichiers incrémentiels]** est automatiquement sélectionnée. Cela déclenche une exportation où le premier fichier est un instantané complet du jeu de données et les fichiers suivants sont des ajouts incrémentiels au jeu de données depuis l’exportation précédente.

>[!IMPORTANT]
>
>Le premier fichier incrémentiel exporté inclut toutes les données existantes dans le jeu de données, en tant que renvoi.

![Workflow d’exportation des jeux de données présentant l’étape de planification.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilisez le sélecteur **[!UICONTROL Fréquence]** pour sélectionner la fréquence d’exportation :

   * **[!UICONTROL Quotidien]**: Planifiez les exportations incrémentielles de fichiers une fois par jour, tous les jours, au moment indiqué.
   * **[!UICONTROL Horaire]**: Planifiez les exportations incrémentielles de fichiers toutes les 3, 6, 8 ou 12 heures.

2. Utilisez le sélecteur **[!UICONTROL Heure]** pour choisir l’heure de la journée, au format [!DNL UTC], à laquelle l’exportation doit avoir lieu.

3. Utilisez le sélecteur **[!UICONTROL Date]** pour choisir l’intervalle à partir duquel l’exportation doit avoir lieu. Notez que dans la version bêta de la fonction, il n’est pas possible de définir une date de fin pour les exportations. Pour plus d’informations, voir la [limites connues](#known-limitations) .

4. Sélectionner **[!UICONTROL Suivant]** pour enregistrer le planning et passer à la **[!UICONTROL Réviser]** étape .

>[!NOTE]
> 
>Pour les exportations de jeux de données, les noms de fichier ont un format prédéfini par défaut, qui ne peut pas être modifié. Voir la section [Vérification de l’exportation réussie d’un jeu de données](#verify) pour plus d’informations et d’exemples de fichiers exportés.

## Révision {#review}

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionner **[!UICONTROL Annuler]** pour diviser le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres, ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à exporter des jeux de données vers la destination.

![Workflow d’exportation des jeux de données présentant l’étape de révision.](/help/destinations/assets/ui/export-datasets/review.png)

## Vérification de l’exportation réussie d’un jeu de données {#verify}

Lors de l’exportation de jeux de données, Experience Platform crée une `.json` ou `.parquet` dans l’emplacement de stockage que vous avez fourni. Attendez-vous à ce qu’un nouveau fichier soit déposé dans votre emplacement de stockage en fonction du planning d’exportation que vous avez fourni.

Experience Platform crée une structure de dossiers dans l’emplacement de stockage que vous avez spécifié, où il dépose les fichiers de jeu de données exportés. Un nouveau dossier est créé pour chaque heure d’exportation, selon le modèle ci-dessous :

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Le nom de fichier par défaut est généré de manière aléatoire et garantit que les noms de fichier exportés sont uniques.

### Exemples de fichiers de jeu de données {#sample-files}

La présence de ces fichiers dans votre emplacement de stockage est la confirmation d’une exportation réussie. Pour comprendre la structure des fichiers exportés, vous pouvez télécharger un exemple. [.parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) ou [fichier .json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## Supprimer un jeu de données de la destination {#remove-dataset}

Pour supprimer un jeu de données d’un flux de données existant, procédez comme suit :

1. Connectez-vous au [Interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionner **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos flux de données de destination existants.

   ![La vue de navigation de destination avec une connexion de destination affichée et le reste s’est estompé.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Icône Sélectionner le filtre ![Icône Filtre](../assets/ui/edit-activation/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

1. Dans la **[!UICONTROL Données d’activation]** , sélectionnez le contrôle des jeux de données pour afficher tous les jeux de données mappés à ce flux de données d’exportation.

   ![L’option de navigation des jeux de données disponibles est mise en surbrillance dans la colonne Données d’activation .](../assets/ui/export-datasets/go-to-datasets-data.png)

1. Le **[!UICONTROL Données d’activation]** pour la destination s’affiche. Sélectionner **[!UICONTROL Supprimer un jeu de données]** dans le rail de droite pour déclencher la boîte de dialogue de confirmation de suppression du jeu de données.

   ![Boîte de dialogue Supprimer le jeu de données présentant la commande Supprimer le jeu de données dans le rail droit.](../assets/ui/export-datasets/remove-dataset-control.png)

1. Dans la boîte de dialogue de confirmation, sélectionnez **[!UICONTROL Supprimer]** pour supprimer immédiatement le jeu de données des exportations vers la destination.

   ![Boîte de dialogue présentant l’option Confirmer la suppression du jeu de données du flux de données.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Limites connues {#known-limitations}

Gardez à l’esprit les restrictions suivantes pour la version bêta des exportations de jeux de données :

* Il existe actuellement une seule autorisation (**[!UICONTROL Gestion et activation des destinations de jeu de données]**) qui inclut des autorisations de gestion et d’activation sur les destinations des jeux de données. Ces contrôles seront ultérieurement divisés en autorisations plus granulaires. Consultez la section [autorisations requises](#permissions) pour obtenir la liste complète des autorisations dont vous avez besoin pour exporter des jeux de données.
* Actuellement, vous ne pouvez exporter que des fichiers incrémentiels et une date de fin ne peut pas être sélectionnée pour vos exportations de jeux de données.
* Les noms de fichier exportés ne sont actuellement pas personnalisables.
* Actuellement, l’interface utilisateur ne vous empêche pas de supprimer un jeu de données en cours d’exportation vers une destination. Ne supprimez aucun jeu de données qui est exporté vers des destinations. [Suppression du jeu de données](#remove-dataset) d’un flux de données de destination avant de le supprimer.
* Les mesures de surveillance des exportations de jeux de données sont actuellement combinées avec les chiffres des exportations de profils afin qu’elles ne reflètent pas les vrais chiffres d’exportation.
