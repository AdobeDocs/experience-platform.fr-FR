---
title: Prise en charge du contrôle d’accès basé sur les attributs pour les schémas ad hoc
description: Un guide pour restreindre l’accès aux champs de données dans les schémas ad hoc générés via Adobe Experience Platform Query Service.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: d955473fb9123a6fc2384cde4073c713b921f582
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 8%

---

# Prise en charge du contrôle d’accès basé sur les attributs pour les schémas ad hoc

Toutes les données introduites dans Adobe Experience Platform sont encapsulées par les schémas du modèle de données d’expérience (XDM) et peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques.

En exécutant une requête CTAS via Query Service lorsqu’aucun schéma n’est spécifié, un schéma ad hoc est généré automatiquement. Il est souvent nécessaire de restreindre l’utilisation de certains champs, ou jeux de données, de schémas ad hoc pour contrôler l’accès à des données personnelles sensibles et à des informations d’identification personnelle. Adobe Experience Platform facilite ce contrôle d’accès en vous permettant d’étiqueter les champs de schéma via l’interface utilisateur de Platform à l’aide de la fonctionnalité de contrôle d’accès basé sur les attributs.

Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Il est toutefois recommandé d’étiqueter les données dès qu’elles sont ingérées dans Platform ou dès que les données sont disponibles pour utilisation dans Platform.

L’étiquetage basé sur les schémas est un composant important du contrôle d’accès basé sur les attributs pour mieux gérer l’accès donné aux utilisateurs ou aux groupes d’utilisateurs. Adobe Experience Platform vous permet de restreindre l’accès à n’importe quel champ d’un schéma ad hoc en créant et en appliquant des étiquettes.

Ce document fournit un tutoriel pour gérer l’accès aux données sensibles en appliquant des étiquettes aux champs de données des schémas ad hoc générés via Query Service.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=fr): Découvrez comment créer et gérer des schémas et d’autres ressources dans l’interface utilisateur de Platform.
* [[!DNL Data Governance]](../../data-governance/home.md): Découvrez comment [!DNL Data Governance] vous permet de gérer les données client et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données.
* [Contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md): Le contrôle d’accès basé sur les attributs est une fonctionnalité de Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ de schéma ad hoc ou ordinaire. Un administrateur définit des stratégies d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

## Création d’un schéma ad hoc

Une fois votre requête exécutée et les résultats générés, un schéma ad hoc est automatiquement généré et ajouté à l’inventaire des schémas.

Pour ajouter une étiquette de données, accédez à [!UICONTROL Schémas] onglet de navigation du tableau de bord en sélectionnant [!UICONTROL Schémas] dans le rail gauche de l’interface utilisateur de Platform. L’inventaire des schémas s’affiche.

>[!NOTE]
>
>Les schémas ad hoc ne sont pas affichés par défaut dans l’inventaire des schémas.

## Découvrez les schémas ad hoc dans l’inventaire des schémas de l’interface utilisateur de Platform {#discover-ad-hoc-schemas}

Pour activer l’affichage des schémas ad hoc dans l’interface utilisateur de Platform, sélectionnez l’icône de filtre (![Une icône de filtre.](../images/data-governance/filter.png)) à gauche du champ de recherche, puis sélectionnez **[!UICONTROL Affichage des schémas ad hoc] dans le rail de gauche qui s’affiche.

![Le tableau de bord du schéma filtre les options du rail de gauche avec la bascule &quot;Afficher le schéma ad hoc&quot; activée.](../images/data-governance/adhoc-schema-toggle.png)

Sélectionnez le nom du schéma ad hoc récemment créé dans la liste disponible. Une visualisation de la structure de schéma ad hoc s’affiche.

![L’exemple de diagramme de structure de schéma ad hoc.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Modification des étiquettes de gouvernance

Pour modifier les libellés de données de votre schéma ad hoc, sélectionnez la variable [!UICONTROL Étiquettes] . L’espace de travail des libellés vous permet d’appliquer, de créer et de modifier des libellés à vos champs de schéma ad hoc et de contrôler les autorisations d’accès via l’interface utilisateur. Tous les champs du schéma ad hoc sont représentés ici.

## Modification des libellés du schéma ou du champ

Pour modifier les libellés de l’ensemble du schéma, sélectionnez l’icône représentant un crayon (![](../images/data-governance/edit-icon.png)) sur le côté du nom du schéma sous la propriété [!UICONTROL Étiquettes] .

![La vue des libellés dans l’espace de travail des schémas avec l’icône en forme de crayon mise en surbrillance.](../images/data-governance/edit-entire-schema-labels.png)

Pour appliquer un libellé à un champ existant, sélectionnez un ou plusieurs champs dans la liste, puis choisissez [!UICONTROL Modification des étiquettes de gouvernance] dans la barre latérale droite.

![La vue des libellés dans l’espace de travail des schémas avec l’option &quot;Modifier les libellés de gouvernance&quot; mise en surbrillance dans la barre latérale de droits.](../images/data-governance/edit-governance-labels.png)

## Fenêtre contextuelle Modifier les libellés

Le [!UICONTROL Modifier les libellés] s’affiche. Dans cette vue, vous pouvez créer ou modifier des étiquettes de gouvernance existantes via l’interface utilisateur.

![La fenêtre contextuelle Modifier les étiquettes .](../images/data-governance/edit-labels-popover.png)

Consultez la documentation pour obtenir des conseils sur la manière de procéder [créer ou modifier des libellés pour le schéma ou le champ sélectionné](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>La création d’un nouveau libellé ou la modification d’un libellé existant nécessite des autorisations d’administrateur pour votre entreprise. Si vous ne disposez pas de droits d’administrateur, contactez votre administrateur système pour en obtenir l’accès.

Vous pouvez également créer des libellés à l’aide de l’espace de travail des autorisations. Voir [guide sur la création de libellés dans l’espace de travail des autorisations](../../access-control/abac/ui/labels.md) pour obtenir des instructions.

Une fois le niveau approprié de contrôle d’accès basé sur les attributs appliqué, le comportement système suivant s’applique à toute requête exécutée via Query Service lorsqu’un utilisateur tente d’accéder à des données non accessibles :

1. Si un utilisateur n’a pas accès à l’un des champs d’un schéma, il ne pourra ni lire ni écrire sur le champ restreint. Cela s’applique aux scénarios courants suivants :

   * Lorsqu’un utilisateur tente d’exécuter une requête avec uniquement une colonne restreinte, le système génère une erreur indiquant que la colonne n’existe pas.
   * Lorsqu’un utilisateur tente d’exécuter une requête avec plusieurs colonnes contenant une colonne restreinte, le système renvoie uniquement la sortie pour toutes les colonnes non restreintes.

1. Si un utilisateur demande l’accès à un champ calculé, il doit avoir accès à tous les champs utilisés dans la composition, sinon le système lui refusera l’accès au champ calculé.

Si une identité ou une identité Principale est définie sur un schéma ad hoc, le système honore automatiquement toutes les demandes d’hygiène des données associées et nettoie les données de ces jeux de données liés à la colonne d’identité.

## Étapes suivantes

Après avoir lu ce document, vous comprenez mieux comment ajouter des libellés d’utilisation des données aux schémas ad hoc créés à l’aide de requêtes CTAS Query Service. Si vous ne l’avez pas déjà fait, les documents suivants sont utiles pour améliorer votre compréhension de la gouvernance des données dans Query Service :

* [Identités de schéma ad hoc](./ad-hoc-schema-identities.md)
* [Gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr)
