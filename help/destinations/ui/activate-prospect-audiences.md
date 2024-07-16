---
title: Activer les audiences de prospects vers des destinations
type: Tutorial
description: Découvrez comment activer les audiences de prospects vers les destinations
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 25%

---

# Activer les audiences de prospects

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui ont acheté les packages Real-Time CDP Prime et Ultimate. Pour plus d’informations, contactez votre représentant d’Adobe.

Cet article explique le workflow requis pour exporter les [audiences prospect](/help/segmentation/ui/prospect-audience.md) de Adobe Experience Platform vers votre destination préférée.

## Destinations prises en charge {#supported-destinations}

Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Utilisez le filtre **[!UICONTROL Types de données]** et sélectionnez **[!UICONTROL Prospects]** pour afficher les destinations qui prennent en charge l’activation des audiences de prospects. Actuellement, l’exportation d’audiences de prospects est disponible uniquement pour les destinations de stockage dans le cloud.

![Destinations qui prennent en charge les audiences de prospects.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Conditions préalables {#prerequisites}

* Vous devez d’abord ingérer les [profils de prospect](/help/profile/ui/prospect-profile.md) et créer les [audiences de prospect](/help/segmentation/ui/prospect-audience.md) avant de pouvoir les activer vers les destinations en aval.
* Pour activer les audiences de prospects vers les destinations, vous devez avoir réussi à vous connecter à une destination. Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser. Pour plus d’informations, consultez le tutoriel sur l’interface utilisateur de [connexion aux destinations](./connect-destination.md) .

### Autorisations nécessaires {#permissions}

Pour activer les audiences de prospects, vous avez besoin des **** et des **** [ autorisations de contrôle d’accès](/help/access-control/home.md#permissions) . Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour activer les audiences du prospect, parcourez le catalogue des destinations. Si une destination possède un contrôle **[!UICONTROL Activer]**, vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Sélectionnez **[!UICONTROL Activer]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

>[!TIP]
>
>Les destinations pouvant exporter des audiences de profil sont indiquées par une icône dans le coin supérieur droit de la carte, similaire à la destination mise en évidence ci-dessous. Vous pouvez également utiliser le filtre de type de données pour afficher uniquement les destinations qui peuvent exporter des audiences de prospects, comme [ affiché plus haut sur la page](#supported-destinations).

![Page de destination Amazon S3 qui peut exporter les audiences de profil mises en surbrillance.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Sélectionnez **[!UICONTROL Prospects de type de données]**, suivis de la connexion de destination vers laquelle vous souhaitez exporter les jeux de données, puis sélectionnez **[!UICONTROL Suivant]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour activer les audiences de perspective, sélectionnez **[!UICONTROL Configurer une nouvelle destination]** pour déclencher le workflow [Se connecter à la destination](/help/destinations/ui/connect-destination.md).

![Workflow d’activation de la destination avec le contrôle Prospects en surbrillance.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Passez à la section suivante : [sélectionnez les audiences de profil](#select-profile-audiences) pour l’exportation.

## Sélectionner les audiences de vos prospects {#select-prospect-audiences}

Utilisez les cases à cocher situées à gauche des noms d’audiences du prospect pour sélectionner les audiences que vous souhaitez exporter vers la destination, puis sélectionnez **[!UICONTROL Suivant]**. Notez que seules les audiences du prospect sont affichées dans cette vue et qu’aucune autre audience ne l’est.

![ Le workflow d&#39;exportation des jeux de données affiche l&#39;étape Sélectionner les audiences où vous pouvez sélectionner les audiences de prospects à exporter.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planification et étapes suivantes

Pour le reste du workflow d’activation afin d’exporter des audiences de prospects, lisez le tutoriel sur l’activation des données vers des destinations basées sur des fichiers. Passez de l’ [étape d’exportation de l’audience de planification](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Notez que dans l’étape de planification, le workflow d’activation des audiences de prospects vous permet uniquement d’ [ exporter des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Les exportations incrémentielles de fichiers ne sont pas prises en charge.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* [Complétez les profils propriétaires avec les attributs des partenaires de données de confiance pour améliorer votre base de données, obtenir de nouvelles informations sur votre base de clientèle et optimiser l’audience.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilisez la prise en charge de données tierces dans Real-Time CDP pour [développer votre base de profils avec les profils de prospects des partenaires de données et interagissez avec eux pour acquérir ou atteindre une nouvelle clientèle](/help/rtcdp/partner-data/prospecting.md).
* [Tirez parti de la reconnaissance par les partenaires pour personnaliser les expériences sur site](/help/rtcdp/partner-data/onsite-personalization.md) lors de la visite sans que l’utilisateur s’authentifie ou n’ait jamais eu d’historique avec votre marque.
