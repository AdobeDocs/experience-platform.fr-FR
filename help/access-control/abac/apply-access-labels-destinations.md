---
title: Utilisation des étiquettes d’accès pour gérer l’accès des utilisateurs aux flux de données de destination
description: Découvrez comment utiliser les étiquettes d’accès pour gérer l’accès des utilisateurs aux flux de données de destination afin qu’un seul sous-ensemble d’utilisateurs de votre entreprise ait accès à des flux de données de destination spécifiques.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
exl-id: 85944720-8551-491c-8991-dd9668beb0ca
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---

# Utilisation des étiquettes d’accès pour gérer l’accès des utilisateurs aux flux de données de destination

Dans le cadre de la fonctionnalité [!UICONTROL Contrôle d’accès basé sur les attributs] de Real-Time CDP, vous pouvez désormais appliquer des libellés d’accès aux flux de données de destination. Vous pouvez ainsi vous assurer que seul un sous-ensemble d’utilisateurs de votre organisation a accès à des flux de données de destination spécifiques.

Lorsque vous ajoutez une étiquette d’accès à une destination spécifique, seuls les utilisateurs qui ont accès à un rôle qui est affecté à cette étiquette peuvent voir et modifier ce flux de données de destination. Si un flux de données de destination n’est marqué d’aucune étiquette, il est visible par tous les utilisateurs appartenant à votre organisation.

Lisez cette page pour comprendre des exemples de cas d’utilisation, les conditions préalables avant de pouvoir appliquer des étiquettes d’accès aux flux de données de destination et d’autres légendes importantes lors de l’utilisation de cette fonctionnalité.

## Conditions préalables {#prerequisites}

Notez les conditions préalables suivantes à remplir avant de commencer à utiliser cette fonctionnalité. Pour vous familiariser avec la fonctionnalité de [!UICONTROL contrôle d’accès basé sur les attributs], Adobe vous recommande également de lire les articles suivants :

* [Présentation du contrôle d’accès basé sur les attributs](/help/access-control/abac/overview.md)
* [Guide de bout en bout du contrôle d’accès basé sur les attributs](/help/access-control/abac/end-to-end-guide.md)

### Accès à l’interface utilisateur des autorisations {#access-permissions-ui}

[!UICONTROL Autorisations] est la zone de l’Experience Cloud dans laquelle les administrateurs peuvent définir des rôles utilisateur et des stratégies afin de gérer les autorisations pour les fonctionnalités et les objets dans une application de produit. Lisez la [section d’autorisations](/help/access-control/abac/end-to-end-guide.md#permissions) pour commencer.

### Création de rôles, d’étiquettes et d’affecter des utilisateurs {#create-roles-labels-assign-users}

Après avoir accédé à l’interface utilisateur [!UICONTROL permissions], vous ou un membre de votre équipe devez configurer des rôles et ajouter les étiquettes requises à ces rôles. Enfin, les utilisateurs qui doivent accéder aux ressources étiquetées avec les libellés spécifiques doivent être ajoutés au rôle . Consultez les sections de documentation suivantes :

* [Créer un rôle](/help/access-control/abac/ui/roles.md)
* [Ajout de libellés à un rôle](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Ajout d’utilisateurs à un rôle](/help/access-control/ui/users.md)

### Création de flux de données de destination {#create-dataflow}

Vous devez d’abord vous connecter à la destination souhaitée et créer un flux de données pour exporter des données, avant de pouvoir appliquer des libellés d’accès au flux de données.

Lisez les guides sur la [connexion à une destination](/help/destinations/ui/connect-destination.md) et l&#39; [activation de données à la destination](/help/destinations/ui/activation-overview.md). Sélectionnez ensuite la destination souhaitée dans le [catalogue des connecteurs disponibles](/help/destinations/catalog/overview.md).

## Déjà disponible : appliquez des étiquettes d’accès à d’autres ressources Experience Platform {#apply-labels-other-resources}

Bien que cette version vous permette d’accorder aux utilisateurs un accès au niveau de l’objet à des flux de données de destination spécifiques, la fonctionnalité d’octroi d’un contrôle d’accès au niveau de l’objet est déjà disponible en général pour d’autres ressources Experience Platform, telles que [audiences](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Exemple de cas d’utilisation {#use-case-example}

Grâce au contrôle d’accès au niveau de l’objet pour les destinations, limitez les équipes spécifiques de marketeurs à n’accéder qu’à leurs destinations spécifiques. Par exemple, si votre entreprise possède des données client dans plusieurs emplacements géographiques, comme aux États-Unis et au Royaume-Uni, vous pouvez limiter l’affichage et la modification des flux de données par une équipe marketing uniquement pour l’emplacement des États-Unis, ainsi qu’une autre équipe marketing pour afficher et modifier les flux de données pour l’emplacement du Royaume-Uni.

## Application des étiquettes d’accès aux flux de données de destination {#apply-labels-to-destination-dataflow}

Pour appliquer des libellés d’accès à un flux de données spécifique :

1. Accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** et localisez le flux de données de destination auquel vous souhaitez limiter l’accès des utilisateurs.
1. Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Nom] et utilisez le contrôle ![Modifier les détails](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL Appliquer les étiquettes d’accès]** pour ajouter de nouvelles étiquettes et gérer les étiquettes existantes pour le flux de données.
   ![Sélectionnez Appliquer les étiquettes d’accès dans la vue Parcourir de l’espace de travail des destinations.](/help/access-control/images/olac/apply-access-labels.png)
1. Sélectionnez les étiquettes à ajouter au flux de données de destination et sélectionnez **[!UICONTROL Enregistrer]**.
   ![Sélectionnez les étiquettes d’accès dans qui doivent s’appliquer au flux de données de destination.](/help/access-control/images/olac/view-access-labels.png)
1. Remarquez que le flux de données comporte désormais un libellé d’accès affiché dans l’interface utilisateur.
   ![Affichage de plusieurs flux de données de destination avec le flux de données sélectionné et affichage d’une étiquette d’accès.](/help/access-control/images/olac/dataflow-with-access-label.png)

Si un flux de données de destination n’est marqué par aucun libellé, il s’affiche pour tous les utilisateurs. Si le flux de données est marqué d’une ou de plusieurs étiquettes d’accès, il s’affiche uniquement pour les utilisateurs appartenant à un rôle qui a le même libellé ou la même combinaison de libellés.

Vous pouvez ajouter des libellés standard et personnalisés aux flux de données de destination. Après avoir ajouté un libellé aux flux de données de destination :

* Les utilisateurs affectés à des rôles ayant accès au même libellé peuvent afficher le flux de données avec le nouveau libellé dans l’interface utilisateur. Ils peuvent afficher et modifier le flux de données de destination dans l’interface utilisateur ou au moyen d’API.

* Les utilisateurs *non* affectés à des rôles ayant accès au même libellé n’ont pas accès au flux de données de destination pour l’afficher ou le modifier dans l’interface utilisateur ou via des API.

## Légendes et éléments importants à connaître {#important-callouts}

Actuellement, les libellés d’accès ne peuvent être appliqués qu’aux flux de données existants. Cela signifie qu’une personne doit créer le flux de données vers la destination avant que les étiquettes d’accès ne puissent être appliquées.

Vous ne pouvez pas appliquer une étiquette d’accès à un flux de données de destination si vous n’avez pas accès à cette étiquette.

Lors de l’ajout de plusieurs libellés à un flux de données de destination, les utilisateurs qui doivent pouvoir afficher et modifier le flux de données doivent être ajoutés à un rôle avec au moins la même combinaison de libellés. Par exemple, si vous appliquez les étiquettes C1, I2 et une autre étiquette personnalisée à un flux de données de destination, seuls les utilisateurs ajoutés aux rôles ayant accès à la combinaison de ces trois étiquettes peuvent afficher et modifier ce flux de données de destination spécifique.

![ Diagramme de Venn montrant comment seuls certains utilisateurs ont accès aux destinations avec plusieurs libellés appliqués.](/help/access-control/images/olac/multiple-labels-venn.png)

## Étapes suivantes {#next-steps}

En suivant les étapes de ce document, vous savez maintenant comment appliquer des étiquettes d’accès aux flux de données de destination afin que seul un sous-ensemble d’utilisateurs de votre entreprise ait accès à des flux de données de destination spécifiques.

Vous pouvez ensuite en savoir plus sur d’autres fonctionnalités prises en charge par le [!UICONTROL contrôle d’accès basé sur les attributs] lors de l’activation des données vers les destinations. Par exemple, vous pouvez limiter l’accès des utilisateurs à [afficher et activer des champs spécifiques uniquement](/help/access-control/abac/overview.md#destinations).
