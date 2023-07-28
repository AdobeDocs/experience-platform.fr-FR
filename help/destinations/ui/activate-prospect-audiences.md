---
title: Activation des audiences de prospects vers les destinations
type: Tutorial
hide: true
hidefromtoc: true
description: Découvrez comment activer les audiences de prospects vers les destinations
source-git-commit: e04d7a3cd75f4e61329a2de8ca5ddcc4d9518a57
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 18%

---


# Activation des audiences de prospects

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté les packages Real-Time CDP Prime et Ultimate. Pour plus d’informations, contactez votre représentant d’Adobe.

Cet article explique le workflow requis pour l’exportation [audiences prospects](/help/segmentation/ui/prospect-audience.md) de Adobe Experience Platform à votre destination préférée.

## Destinations prises en charge {#supported-destinations}

Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Utilisez la variable **[!UICONTROL Types de données]** filtrer et sélectionner **[!UICONTROL Perspectives]** pour voir les destinations qui prennent en charge l’activation des audiences de prospects. Actuellement, l’exportation d’audiences de prospects est disponible uniquement pour le [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) destination.

![Destinations qui prennent en charge les exportations de jeux de données](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Conditions préalables {#prerequisites}

* Vous devez d’abord ingérer [profils de prospect](/help/profile/ui/prospect-profile.md) et créez [audiences prospects](/help/segmentation/ui/prospect-audience.md) avant de pouvoir les activer vers les destinations en aval.
* Pour activer les audiences de prospects vers les destinations, vous devez avoir réussi à vous connecter à une destination. Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser. Lisez le tutoriel de l’interface utilisateur sur [connexion aux destinations](./connect-destination.md) pour plus d’informations.

### Autorisations nécessaires {#permissions}

Pour activer les audiences de prospects, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour activer les audiences du prospect, parcourez le catalogue des destinations. Si une destination comporte une variable **[!UICONTROL Activer]** contrôlez, puis vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Sélectionner **[!UICONTROL Activer]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

>[!TIP]
>
>Les destinations pouvant exporter des audiences de profil sont signalées par une icône dans le coin supérieur droit de la carte, semblable à la destination mise en évidence ci-dessous. Vous pouvez également utiliser le filtre de type de données pour afficher uniquement les destinations qui peuvent exporter des audiences de prospects, comme [affiché plus haut sur la page](#supported-destinations).

![Page de destination Amazon S3 qui peut exporter les audiences de profil mises en surbrillance.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Sélectionner **[!UICONTROL Perspectives de type de données]**, suivi de la connexion de destination vers laquelle vous souhaitez exporter des jeux de données, puis sélectionnez **[!UICONTROL Suivant]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour activer les audiences de perspective, sélectionnez **[!UICONTROL Configuration d’une nouvelle destination]** pour déclencher la variable [Se connecter à la destination](/help/destinations/ui/connect-destination.md) workflow.

![Workflow d’activation de la destination avec le contrôle Prospects en surbrillance.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Passez à la section suivante pour [sélectionner les audiences de votre profil ;](#select-profile-audiences) pour l’exportation.

## Sélectionner les audiences de vos prospects {#select-prospect-audiences}

Utilisez les cases à cocher situées à gauche des noms d’audiences du prospect pour sélectionner les audiences que vous souhaitez exporter vers la destination, puis sélectionnez **[!UICONTROL Suivant]**. Notez que seules les audiences du prospect sont affichées dans cette vue et qu’aucune autre audience ne l’est.

![Le workflow d’exportation des jeux de données affiche l’étape Sélectionner les audiences dans laquelle vous pouvez sélectionner les audiences de prospects à exporter.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planification et étapes suivantes

Pour le reste du workflow d’activation afin d’exporter des audiences de prospects, lisez le tutoriel sur l’activation des données vers des destinations basées sur des fichiers. Continuez à partir du [étape planifier l’exportation de l’audience](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Notez que dans l’étape de planification, le workflow d’activation des audiences prospects vous permet uniquement d’effectuer les opérations suivantes : [export des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Les exportations incrémentielles de fichiers ne sont pas prises en charge.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->