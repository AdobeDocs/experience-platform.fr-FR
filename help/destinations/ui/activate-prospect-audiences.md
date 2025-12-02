---
title: Activer les audiences de prospects vers des destinations
type: Tutorial
description: Découvrez comment activer les audiences de prospects vers les destinations
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 24%

---

# Activer les audiences de prospects

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté les packages Real-Time CDP Prime et Ultimate. Contactez votre représentant ou représentante Adobe pour plus d’informations.

Cet article explique le processus requis pour exporter des [audiences de prospects](/help/segmentation/types/prospect-audiences.md) de Adobe Experience Platform vers votre destination préférée.

## Destinations prises en charge {#supported-destinations}

Accédez à **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalog]** . Utilisez le filtre **[!UICONTROL Data types]** et sélectionnez **[!UICONTROL Prospects]** pour afficher les destinations qui prennent en charge l’activation des audiences de prospects. Actuellement, l’exportation des audiences de prospects n’est disponible que pour les destinations de stockage dans le cloud.

![Destinations qui prennent en charge les audiences de prospects.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Conditions préalables {#prerequisites}

* Vous devez d’abord ingérer des [profils de prospects](/help/profile/ui/prospect-profile.md) et créer des [audiences de prospects](/help/segmentation/types/prospect-audiences.md) avant de pouvoir les activer vers des destinations en aval.
* Pour activer les audiences de prospects vers les destinations, vous devez avoir réussi à vous connecter à une destination. Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser. Pour plus d’informations, consultez le tutoriel de l’interface utilisateur sur [connexion aux destinations](./connect-destination.md).

### Autorisations nécessaires {#permissions}

Pour activer les audiences de prospects, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Activate Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour activer les audiences de prospects, parcourez le catalogue des destinations. Si une destination dispose d’un contrôle **[!UICONTROL Activate]**, vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connections > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalog]** .

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Sélectionnez **[!UICONTROL Activate]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

>[!TIP]
>
>Les destinations pouvant exporter les audiences de profil sont indiquées par une icône dans le coin supérieur droit de la carte, similaire à la destination mise en surbrillance ci-dessous, ou vous pouvez utiliser le filtre de type de données pour afficher uniquement les destinations pouvant exporter les audiences de prospects, comme [indiqué plus haut sur la page](#supported-destinations).

![Page de destination Amazon S3 pouvant exporter les audiences de profil mises en surbrillance.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Sélectionnez **[!UICONTROL Data type Prospects]**, suivi de la connexion de destination vers laquelle vous souhaitez exporter les jeux de données, puis sélectionnez **[!UICONTROL Next]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour activer les audiences de prospects, sélectionnez **[!UICONTROL Configure new destination]** pour déclencher le workflow [Se connecter à la destination](/help/destinations/ui/connect-destination.md).

![Workflow d’activation de destination avec le contrôle Prospects mis en surbrillance.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Passez à la section suivante pour [sélectionner les audiences de votre profil](#select-profile-audiences) à exporter.

## Sélectionner les audiences de prospects {#select-prospect-audiences}

Utilisez les cases à cocher situées à gauche des noms des audiences de prospects pour sélectionner les audiences que vous souhaitez exporter vers la destination, puis sélectionnez **[!UICONTROL Next]**. Notez que seules les audiences du prospect s&#39;affichent dans cette vue, et aucune autre audience ne s&#39;affiche.

![Workflow d’exportation des jeux de données présentant l’étape de sélection des audiences dans laquelle vous pouvez sélectionner les audiences de prospects à exporter.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planification et étapes suivantes

Pour le reste du workflow d’activation afin d’exporter les audiences de prospects, consultez le tutoriel sur l’activation des données vers des destinations basées sur des fichiers. Continuez à partir de l’étape [planifier l’exportation de l’audience](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Notez que dans l&#39;étape de planification, le workflow d&#39;activation des audiences de prospects ne vous permet d&#39;[exporter des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Les exportations de fichiers incrémentiels ne sont pas prises en charge.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* [Complétez les profils propriétaires avec les attributs des partenaires de données de confiance pour améliorer votre base de données, obtenir de nouvelles informations sur votre base de clientèle et optimiser l’audience.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilisez la prise en charge de données tierces dans Real-Time CDP pour [développer votre base de profils avec les profils de prospects des partenaires de données et interagissez avec eux pour acquérir ou atteindre une nouvelle clientèle](/help/rtcdp/partner-data/prospecting.md).
* [Tirez parti de la reconnaissance assistée par un partenaire pour personnaliser les expériences sur site](/help/rtcdp/partner-data/onsite-personalization.md) au cours de la visite sans que l’utilisateur ne s’authentifie ou n’ait d’historique avec votre marque.
