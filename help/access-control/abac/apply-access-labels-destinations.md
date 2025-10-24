---
title: Utiliser des libellés d’accès pour gérer l’accès des utilisateurs et utilisatrices aux flux de données de destination
description: Découvrez comment utiliser les libellés d’accès pour gérer l’accès des utilisateurs aux flux de données de destination afin que seul un sous-ensemble d’utilisateurs de votre organisation ait accès à des flux de données de destination spécifiques.
role: Developer, Admin, User
exl-id: 85944720-8551-491c-8991-dd9668beb0ca
source-git-commit: de71e9e7825ab9a3eaf1e06d03046636406493db
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 3%

---

# Utiliser des libellés d’accès pour gérer l’accès des utilisateurs et utilisatrices aux flux de données de destination

Dans le cadre de la fonctionnalité [[!UICONTROL attribute-based access control]](overview.md) de Real-Time CDP, vous pouvez désormais appliquer des libellés d’accès aux [flux de données de destination](../../dataflows/ui/monitor-destinations.md). Ainsi, vous pouvez vous assurer que seul un sous-ensemble d’utilisateurs de votre organisation a accès à des flux de données de destination spécifiques.

Lorsque vous ajoutez un libellé d’accès à une destination particulière, seuls les utilisateurs et utilisatrices ayant accès à un rôle auquel ce libellé est affecté peuvent voir et modifier ce flux de données de destination. Si un flux de données de destination n’est marqué d’aucun libellé, il est visible par tous les utilisateurs appartenant à votre organisation.

Lisez cette page pour comprendre les exemples de cas d’utilisation, les conditions préalables avant de pouvoir appliquer des libellés d’accès aux flux de données de destination et d’autres légendes importantes lors de l’utilisation de cette fonctionnalité.

## Conditions préalables {#prerequisites}

Notez les conditions préalables suivantes à remplir avant de commencer à utiliser cette fonctionnalité. Pour vous familiariser avec [!UICONTROL attribute-based access control], Adobe vous recommande également de lire les articles suivants :

* [Présentation du contrôle d’accès basé sur les attributs](/help/access-control/abac/overview.md)
* [Guide complet du contrôle d’accès basé sur les attributs](/help/access-control/abac/end-to-end-guide.md)

### Accès à l’interface utilisateur des autorisations {#access-permissions-ui}

[!UICONTROL Permissions] est la zone d’Experience Cloud dans laquelle les administrateurs peuvent définir des rôles d’utilisateur et des politiques afin de gérer les autorisations pour les fonctionnalités et objets d’une application de produit. Pour commencer, consultez la [section relative aux autorisations](/help/access-control/abac/end-to-end-guide.md#permissions).

### Créer des rôles, des libellés et affecter des utilisateurs {#create-roles-labels-assign-users}

Après avoir obtenu l’accès à l’interface utilisateur de [!UICONTROL permissions], vous ou un membre de votre équipe devez configurer des rôles et ajouter les libellés requis à ces rôles. Enfin, les utilisateurs et utilisatrices qui doivent accéder aux ressources libellées avec des libellés spécifiques doivent être ajoutés au rôle. Consultez les sections de documentation suivantes :

* [Créer un rôle](/help/access-control/abac/ui/roles.md)
* [Ajouter des libellés à un rôle](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Ajouter des utilisateurs à un rôle](/help/access-control/ui/users.md)

### Créer des flux de données de destination {#create-dataflow}

Vous devez d’abord vous connecter à la destination souhaitée et créer un flux de données pour exporter des données, avant de pouvoir appliquer des libellés d’accès au flux de données.

Lisez les guides sur [la connexion à une destination](/help/destinations/ui/connect-destination.md) et [l’activation des données vers la destination](/help/destinations/ui/activation-overview.md). Sélectionnez ensuite la destination souhaitée dans le [catalogue des connecteurs disponibles](/help/destinations/catalog/overview.md).

## Déjà disponible : application des libellés d’accès à d’autres ressources Experience Platform {#apply-labels-other-resources}

Bien que cette version vous permette d’accorder aux utilisateurs et utilisatrices l’accès au niveau de l’objet à des flux de données de destination spécifiques, la fonctionnalité d’octroi du contrôle d’accès au niveau de l’objet est déjà disponible pour d’autres ressources Experience Platform, telles que [audiences](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Exemple de cas d’utilisation {#use-case-example}

Avec le contrôle d’accès au niveau de l’objet pour les destinations, limitez les équipes spécifiques de spécialistes marketing à l’accès à leurs destinations spécifiques uniquement. Par exemple, si votre organisation dispose de données client dans plusieurs emplacements géographiques, comme les États-Unis et le Royaume-Uni, vous pouvez limiter une équipe marketing à l’affichage et à la modification des flux de données pour l’emplacement aux États-Unis uniquement et une autre équipe marketing à l’affichage et à la modification des flux de données pour l’emplacement au Royaume-Uni.

## Application de libellés d’accès aux flux de données de destination {#apply-labels-to-destination-dataflow}

Pour appliquer des libellés d’accès à un flux de données spécifique :

1. Accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** et localisez le flux de données de destination pour lequel vous souhaitez limiter l’accès des utilisateurs et utilisatrices.
1. Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Name] et utilisez la commande ![&#x200B; &#x200B;](/help/images/icons/key.png)Modifier les détails **[!UICONTROL Apply access labels]** pour ajouter de nouveaux libellés et gérer les libellés existants du flux de données.
   ![Sélectionnez Appliquer les libellés d’accès dans la vue Parcourir de l’espace de travail des destinations.](/help/access-control/images/olac/apply-access-labels.png)
1. Sélectionnez les libellés à ajouter au flux de données de destination et sélectionnez **[!UICONTROL Save]**.
   ![Sélectionnez les libellés d’accès dans qui doivent s’appliquer au flux de données de destination.](/help/access-control/images/olac/view-access-labels.png)
1. Notez que le flux de données dispose désormais d’un libellé d’accès affiché dans l’interface utilisateur.
   ![Affichage de plusieurs flux de données de destination avec le flux de données sélectionné et affichage d’un libellé d’accès.](/help/access-control/images/olac/dataflow-with-access-label.png)

Si un flux de données de destination n’est marqué d’aucun libellé, il est visible par tous les utilisateurs. Si le flux de données est marqué d’un ou de plusieurs libellés d’accès, il n’est visible que pour les utilisateurs appartenant à un rôle qui possède le même libellé ou la même combinaison de libellés.

Vous pouvez ajouter des libellés standard et personnalisés aux flux de données de destination. Après avoir ajouté un libellé aux flux de données de destination :

* Les utilisateurs et utilisatrices affectés à des rôles ayant accès au même libellé peuvent afficher le flux de données avec le nouveau libellé dans l’interface utilisateur. Ils peuvent afficher et modifier le flux de données de destination dans l’interface utilisateur ou par le biais d’API.

* Les utilisateurs qui ne sont *pas* affectés à des rôles ayant accès au même libellé n’ont pas accès au flux de données de destination pour l’afficher ou le modifier dans l’interface utilisateur ou via les API.

## Légendes et éléments importants à connaître {#important-callouts}

* Actuellement, les libellés d’accès ne peuvent être appliqués qu’aux flux de données existants. Cela signifie que vous devez créer un flux de données vers une destination avant de pouvoir appliquer des libellés d’accès.
* Vous ne pouvez pas appliquer de libellé d’accès à un flux de données de destination si vous n’avez pas accès à ce libellé.
* Lors de l’ajout de plusieurs libellés à un flux de données de destination, les utilisateurs qui doivent pouvoir afficher et modifier le flux de données doivent être ajoutés à un rôle avec au moins la même combinaison de libellés. Par exemple, si vous appliquez les libellés C1, I2 et un autre libellé personnalisé à un flux de données de destination, seuls les utilisateurs ajoutés aux rôles ayant accès à la combinaison de ces trois libellés peuvent afficher et modifier ce flux de données de destination spécifique.
* Les flux de données de destination auxquels un utilisateur n’a pas accès en raison des configurations des libellés d’accès peuvent apparaître dans l’interface utilisateur grisés. Les utilisateurs ne peuvent pas effectuer d’actions sur ces flux de données.

![La fenêtre Actions de la navigation dans le catalogue des destinations est grisée.](../images/olac/destinations-greyed-edit.png)

>[!NOTE]
>
> Lors de la recherche de flux de données de destination à l’aide de la zone de recherche située en haut de l’interface utilisateur d’Experience Platform, les résultats peuvent inclure des flux de données de destination que vos libellés d’accès utilisateur vous empêchent de voir. Ce comportement sera corrigé dans une mise à jour à venir.

![Diagramme de Venn montrant comment seuls certains utilisateurs ont accès aux destinations avec plusieurs libellés appliqués.](/help/access-control/images/olac/multiple-labels-venn.png)

## Étapes suivantes {#next-steps}

En suivant les étapes de ce document, vous savez maintenant comment appliquer des libellés d’accès aux flux de données de destination afin que seul un sous-ensemble d’utilisateurs de votre organisation ait accès à des flux de données de destination spécifiques.

Vous pouvez ensuite en savoir plus sur les autres fonctionnalités prises en charge par [!UICONTROL attribute-based access control] lors de l’activation de données vers les destinations. Par exemple, vous pouvez limiter l’accès des utilisateurs et utilisatrices à l’[affichage et activation de champs spécifiques uniquement](/help/access-control/abac/overview.md#destinations).
