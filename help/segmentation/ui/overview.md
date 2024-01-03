---
solution: Experience Platform
title: Guide de l’IU de Segmentation Service
description: Découvrez comment créer et gérer des audiences et des définitions de segment dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 7ee39a39aecdfc0516f63e6a9c9a06c6c4b22996
workflow-type: tm+mt
source-wordcount: '3933'
ht-degree: 87%

---

# Guide de l’IU de Segmentation Service

[!DNL Adobe Experience Platform Segmentation Service] fournit une interface utilisateur pour la création et la gestion des définitions de segment et d’audience.

## Prise en main

L’utilisation des définitions de segment et d’audience exige une compréhension des différents services d’[!DNL Experience Platform] concernés par la segmentation. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Segmentation Service]](../home.md) : [!DNL Segmentation Service] permet de segmenter les données stockées dans [!DNL Experience Platform] qui se rapportent aux particuliers (tels que les clientes et les clients, les prospects, les utilisateurs et les utilisatrices ou les organisations) en groupes plus petits.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md) : permet la création de profils client en rapprochant des identités de sources de données disparates ingérées dans [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).

Il est également important de connaître deux termes clés utilisés dans ce document et de comprendre la différence entre eux :

- **Audience** : un ensemble de personnes qui partagent des comportements et/ou des caractéristiques similaires. Ce groupe de personnes peut être généré par Adobe Experience Platform à l’aide de définitions de segment ou de la composition de l’audience (audience générée par Platform) ou à partir de sources externes comme les chargements personnalisés (audience générée en externe).
- **Définition de segment** : les règles utilisées par Adobe Experience Platform pour décrire les caractéristiques ou le comportement clés d’une audience cible.
- **Segmenter** : acte de séparation des profils en audiences.

## Vue d’ensemble

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Audiences]** dans le volet de navigation de gauche pour ouvrir l’onglet **[!UICONTROL Vue d’ensemble]** affichant le tableau de bord [!UICONTROL Audiences].

>[!NOTE]
>
>Si votre organisation débute sur Platform et ne dispose pas encore de jeux de données de profils actifs ou de politiques de fusion créés, le tableau de bord [!UICONTROL Audiences] n’est pas visible. Au lieu de cela, l’onglet [!UICONTROL Vue d’ensemble] affiche des liens et de la documentation pour vous aider à commencer avec les audiences.

### Tableau de bord [!UICONTROL Audiences] {#segments-dashboard}

Le tableau de bord **[!UICONTROL Audiences]** décrit les mesures clés liées aux données d’audience de votre organisation.

Pour en savoir plus, consultez le [guide du tableau de bord Audiences](../../dashboards/guides/audiences.md).

![Le tableau de bord Audiences s’affiche. Il affiche divers widgets, notamment la taille de l’audience, les profils par identité, le chevauchement des identités et la tendance de changement de la taille de l’audience.](../../dashboards/images/segments/dashboard-overview.png)

## Parcourir {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Attrition"
>abstract="L’attrition représente le pourcentage de profils qui changent dans une audience par rapport à la dernière exécution de la tâche de segmentation."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Méthode d’évaluation"
>abstract="Les méthodes d’évaluation des audiences incluent le traitement par lots, en flux continu et Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Ajouter toutes les audiences à planifier"
>abstract="Activez cette option pour inclure toutes les audiences évaluées à l’aide de la segmentation par lots dans la mise à jour planifiée quotidienne. Désactivez cette option pour supprimer toutes les audiences de la mise à jour planifiée."

Sélectionnez la variable **[!UICONTROL Parcourir]** pour afficher la liste de toutes les audiences de votre organisation. Cette vue répertorie des informations sur les audiences, notamment le nombre de profils, l’origine, la date de création, la date de dernière modification, les balises et la répartition.

![L’écran de navigation s’affiche. Une liste de toutes les audiences appartenant à l’organisation s’affiche.](../images/ui/overview/audience-browse.png)

Une icône de points de suspension se trouve à côté de chaque audience. Cette option affiche la liste des actions rapides disponibles pour l’audience. Cette liste d’actions diffère en fonction de l’origine de l’audience.

![La liste des actions rapides s’affiche pour les audiences dont l’origine est [!UICONTROL Composition de l’audience].](../images/ui/overview/browse-audience-composition-details.png)

| Action | Origines | Description |
| ------ | ------- | ----------- |
| [!UICONTROL Modifier] | Segmentation Service | Ouvre le créateur de segments pour modifier votre audience. Notez que si votre audience a été créée par le biais de l’API, vous allez **not** Vous pouvez le modifier à l’aide du créateur de segments. Pour plus d’informations sur l’utilisation du créateur de segments, consultez le [Guide de l’interface utilisateur du créateur de segments](./segment-builder.md). |
| [!UICONTROL Composition ouverte] | Composition de l’audience | Ouvre la composition d’audience pour afficher votre audience. Pour plus d’informations sur la composition d’audience, consultez le [Guide de l’interface utilisateur de la composition d’audience](./audience-composition.md). |
| [!UICONTROL Activer la destination] | Segmentation Service | Active l’audience vers une destination. Pour plus d’informations sur l’activation d’une audience vers une destination, consultez la [vue d’ensemble de l’activation](../../destinations/ui/activation-overview.md). |
| [!UICONTROL Partager avec les partenaires] | Composition d’audience, chargement personnalisé, Segmentation Service | Partage votre audience avec d’autres utilisateurs de Platform. Pour plus d’informations sur cette fonctionnalité, consultez la [vue d’ensemble de la correspondance de segments](./segment-match/overview.md). |
| [!UICONTROL Gestion des balises] | Composition d’audience, chargement personnalisé, Segmentation Service | Gère les balises définies par l’utilisateur qui appartiennent à l’audience. Pour plus d’informations sur cette fonctionnalité, consultez la section sur [le filtrage et le balisage](#manage-audiences). |
| [!UICONTROL Déplacer vers le dossier] | Composition d’audience, chargement personnalisé, Segmentation Service | Gère le dossier auquel l’audience appartient. Pour plus d’informations sur cette fonctionnalité, consultez la section sur [le filtrage et le balisage](#manage-audiences). |
| [!UICONTROL Copier] | Composition d’audience, chargement personnalisé, Segmentation Service | Duplique l’audience sélectionnée. |
| [!UICONTROL Appliquer les libellés d’accès] | Composition d’audience, chargement personnalisé, Segmentation Service | Gère les étiquettes d’accès qui appartiennent à l’audience. Pour plus d’informations sur les libellés d’accès, veuillez lire la documentation sur la [gestion des libellés](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Archiver] | Chargement personnalisé | Archive l’audience sélectionnée. |
| [!UICONTROL Supprimer] | Composition d’audience, chargement personnalisé, Segmentation Service | Supprime l’audience sélectionnée. |
| [!UICONTROL Ajouter au package] | Composition d’audience, chargement personnalisé, Segmentation Service | Déplace l’audience entre les environnements de test. Pour plus d’informations sur cette fonctionnalité, veuillez lire la section [guide d’outils sandbox](../../sandboxes/ui/sandbox-tooling.md). |

>[!NOTE]
>
> Vous **ne pourrez pas** supprimer une audience utilisée dans une activation de destination.

Dans la partie supérieure de la page, vous trouverez des options permettant d’ajouter toutes les audiences à un planning, d’importer une audience, de créer une audience et d’afficher une ventilation de la fréquence de mise à jour.

L’activation de l’option **[!UICONTROL Planifier toutes les audiences]** active la segmentation planifiée. Vous trouverez plus d’informations sur la segmentation planifiée dans la [section segmentation planifiée de ce guide d’utilisation](#scheduled-segmentation).

Sélection **[!UICONTROL Importer une audience]** vous permet d’importer une audience générée en externe. Pour en savoir plus sur l&#39;import d&#39;audiences, consultez la section sur [import d’une audience dans le guide d’utilisation](#import-audience).

Sélectionner **[!UICONTROL Créer une audience]** vous permet de créer une audience. Pour en savoir plus sur la création d’audiences, consultez la section sur la [création d’une audience dans le guide d’utilisation](#create-audience).

![La barre de navigation supérieure de la page de navigation des audiences est mise en surbrillance. Cette barre contient un bouton pour créer une audience et un bouton pour importer une audience.](../images/ui/overview/browse-audiences-top.png)

Vous pouvez sélectionner **[!UICONTROL Résumé de la fréquence de mise à jour]** pour afficher un graphique circulaire indiquant la fréquence de mise à jour.

![Le bouton Récapitulatif de la mise à jour de la fréquence est mis en surbrillance.](../images/ui/overview/browse-audience-update-frequency-summary.png)

Le graphique en secteurs apparaît, affichant une répartition des audiences par fréquence de mise à jour. Le graphique présente le nombre total d’audiences au milieu. Si vous passez le curseur de la souris sur les différentes parties de l’audience, le nombre d’audiences appartenant à chaque type de fréquence de mise à jour s’affiche.

![Le graphique en secteurs des fréquences de mise à jour s’affiche.](../images/ui/overview/update-frequency-chart.png)

### Personnaliser {#customize}

Vous pouvez ajouter des champs supplémentaires au [!UICONTROL Parcourir] en sélectionnant ![l’icône d’attribut de filtre](../images/ui/overview/filter-attribute.png). Ces champs supplémentaires comprennent le statut du cycle de vie, la fréquence de mise à jour, la dernière mise à jour par, la description, la création par et les libellés d’accès.

| Champ | Description |
| ----- | ----------- |
| [!UICONTROL Nom] | Nom de l’audience. |
| [!UICONTROL Nombre de profils] | Nombre total de profils qui remplissent les critères de l’audience. |
| [!UICONTROL Origine] | Origine de l’audience. Cette information indique d’où vient l’audience. Les valeurs possibles sont Segmentation Service, Chargement personnalisé, Composition de l’audience et Audience Manager. |
| [!UICONTROL Statut du cycle de vie] | Statut de l’audience. Les valeurs possibles pour ce champ incluent `Draft`, `Published` et `Archived`. |
| [!UICONTROL Fréquence de mise à jour] | Valeur qui indique la fréquence de mise à jour des données de l’audience. Les valeurs possibles pour ce champ incluent [!UICONTROL Lot], [!UICONTROL Diffusion en continu], [!UICONTROL Edge], et [!UICONTROL Non planifié]. |
| [!UICONTROL Dernière mise à jour par] | Nom de la personne qui a mis à jour l’audience pour la dernière fois. |
| [!UICONTROL Créé] | Date et heure de création de l’audience en UTC. |
| [!UICONTROL Dernière mise à jour] | Date et heure de la dernière mise à jour de l’audience en UTC. |
| [!UICONTROL Balises] | Balises définies par l’utilisateur ou l’utilisatrice qui appartiennent à l’audience. Vous trouverez plus d’informations sur ces balises dans la [section sur les balises](#tags). |
| [!UICONTROL Description] | Description de l’audience. |
| [!UICONTROL Créé par] | Nom de la personne qui a créé l’audience. |
| [!UICONTROL Libellés d’accès] | Libellés d’accès pour l’audience. Les libellés d’accès vous permettent de classer les jeux de données et les champs en fonction des politiques d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Pour plus d’informations sur les libellés d’accès, veuillez lire la documentation sur la [gestion des libellés](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Répartition] | Répartition du statut du profil pour l’audience. Vous trouverez ci-dessous une description plus détaillée de cette répartition du statut du profil. |

Si la répartition est sélectionnée, l’affichage présente un graphique à barres indiquant le pourcentage de profils appartenant à chacun des statuts suivants : [!UICONTROL Réalisé], [!UICONTROL Existant] et [!UICONTROL Sortant]. De plus, la répartition affichée dans l’onglet [!UICONTROL Parcourir] est la répartition la plus précise du statut de la définition du segment. Si ce nombre diffère de ce qui est indiqué dans l’onglet [!UICONTROL Vue d’ensemble], vous devez utiliser les nombres de l’onglet [!UICONTROL Parcourir] comme source d’informations correcte, puisque les nombres de l’onglet [!UICONTROL Vue d’ensemble] ne sont mis à jour qu’une seule fois par jour.

| État | Description |
| ------ | ----------- |
| [!UICONTROL Réalisé] | Nombre de profils qui **ont rempli les critères** du segment au cours des dernières 24 heures depuis la dernière exécution de la tâche de segmentation par lots. |
| [!UICONTROL Existant] | Nombre de profils qui **sont restés** dans le segment au cours des dernières 24 heures depuis la dernière exécution de la tâche de segmentation par lots. |
| [!UICONTROL Sortant] | Nombre de profils qui **sont sortis** du segment au cours des dernières 24 heures depuis la dernière exécution de la tâche de segmentation par lots. |

Après avoir sélectionné les champs à afficher, vous pouvez redimensionner la largeur des colonnes affichées. Pour ce faire, faites glisser la zone entre les colonnes ou sélectionnez l’option ![icône de flèche](../images/ui/overview/arrow-icon.png) de la colonne à redimensionner, suivie de **[!UICONTROL Redimensionner la colonne]**.

![Le bouton de colonne Redimensionner est mis en surbrillance.](../images/ui/overview/browse-audience-resize-column.png)

### Filtrage, dossiers et balisage {#manage-audiences}

Pour améliorer votre efficacité, vous pouvez rechercher des audiences existantes, ajouter des balises définies par l’utilisateur ou l’utilisatrice aux audiences, placer des audiences dans des dossiers et filtrer les audiences affichées.

**Recherche** {#search}

Vous pouvez rechercher vos audiences existantes dans 9 langues différentes au maximum avec [!DNL Unified Search].

Pour utiliser [!DNL Unified Search], ajoutez le terme à rechercher dans la barre de recherche en surbrillance.

![La barre de recherche est mise en surbrillance.](../images/ui/overview/browse-audience-search.png)

Pour plus d’informations sur [!DNL Unified Search], y compris les fonctionnalités prises en charge, consultez la [documentation sur Unified Search](https://experienceleague.adobe.com/docs/core-services/interface/services/search-experience-cloud.html?lang=fr).

**Balises** {#tags}

Vous pouvez ajouter des balises définies par l’utilisateur ou l’utilisatrice pour mieux décrire, trouver et gérer vos audiences.

Pour ajouter une balise, sélectionnez **[!UICONTROL Gérer les balises]** sur l’audience que vous souhaitez baliser.

![Sélection du bouton [!UICONTROL Gérer les balises] pour une audience spécifique.](../images/ui/overview/browse-manage-tags.png)

La fenêtre contextuelle **[!UICONTROL Gérer les balises]** s’affiche. Elle vous permet de sélectionner une balise classée ou non classée.

| Type de balise | Description |
| -------- | ----------- |
| Classée | Il s’agit d’une balise créée et gérée par les administrateurs et administratrices de votre organisation. |
| Non classée | Il s’agit d’une balise créée dans la fenêtre contextuelle [!UICONTROL Gérer les balises]. Tout le monde peut créer ou gérer ces types de balises. |

![La fenêtre contextuelle [!UICONTROL Gérer les balises] s’affiche. Les options de sélection d’une balise classée ou non classée sont mises en surbrillance.](../images/ui/overview/create-tag.png)

Une fois que vous avez ajouté toutes les balises à l’audience, cliquez sur **[!UICONTROL Enregistrer]**.

![Mise en surbrillance des balises ajoutées dans la fenêtre contextuelle [!UICONTROL Gérer les balises].](../images/ui/overview/created-tags.png)

Pour plus d’informations sur la création et la gestion des balises, consultez le [guide de gestion des balises](../../administrative-tags/ui/managing-tags.md).

**Dossiers** {#folders}

Vous pouvez placer des audiences dans des dossiers pour une meilleure gestion de l’audience.

Pour déplacer une audience dans un dossier, sélectionnez **[!UICONTROL Déplacer vers le dossier]** sur l’audience que vous souhaitez déplacer.

![Sélection du bouton [!UICONTROL Déplacer vers le dossier] pour une audience spécifique.](../images/ui/overview/browse-move-to-folder.png)

La fenêtre contextuelle **Déplacer l’audience vers le dossier** s’affiche. Sélectionnez le dossier vers lequel vous souhaitez déplacer l’audience, puis cliquez sur **[!UICONTROL Enregistrer]**.

![La fenêtre contextuelle Déplacer l’audience vers le dossier s’affiche. Le dossier vers lequel l’audience sera déplacée est mis en surbrillance.](../images/ui/overview/move-to-folder.png)

Une fois l’audience déplacée dans un dossier, vous pouvez choisir d’afficher uniquement les audiences d’un dossier spécifique.

![Les audiences appartenant à un dossier spécifique s’affichent.](../images/ui/overview/browse-folders.png)

**Filtre** {#filter}

Vous pouvez également filtrer les audiences selon différents paramètres.

Pour filtrer les audiences disponibles, sélectionnez l’![icône Filtrer](../images/ui/overview/filter-icon.png).

![La page Parcourir les audiences s’affiche, avec l’icône Filtrer mise en surbrillance.](../images/ui/overview/browse-select-filter.png)

La liste des filtres disponibles s’affiche.

| Filtre | Description |
| ------ | ----------- |
| [!UICONTROL Origine] | Permet de filtrer l’audience en fonction de son origine. Les options disponibles comprennent Segmentation Service, le chargement personnalisé, la composition d’audience et Audience Manager. |
| [!UICONTROL A une balise] | Permet de filtrer par balise. Vous pouvez choisir entre **[!UICONTROL A une balise]** et **[!UICONTROL A toutes les balises]**. Lors de la sélection de **[!UICONTROL A une balise]**, les audiences filtrées incluent **toutes** les balises que vous avez ajoutées. Lors de la sélection de **[!UICONTROL A toutes les balises]**, les audiences filtrées doivent inclure **toutes** les balises que vous avez ajoutées. |
| [!UICONTROL Statut du cycle de vie] | Permet de filtrer les données en fonction du statut de cycle de vie de l’audience. Les options disponibles sont les suivantes : [!UICONTROL Actif], [!UICONTROL Archivé], [!UICONTROL Supprimé], [!UICONTROL Brouillon], [!UICONTROL Inactif] et [!UICONTROL Publié]. |
| [!UICONTROL Fréquence de mise à jour] | Permet de filtrer selon la fréquence de mise à jour de l’audience. Les options disponibles sont les suivantes : [!UICONTROL Planifié], [!UICONTROL Continu] et [!UICONTROL À la demande]. |
| [!UICONTROL Créé par] | Permet de filtrer en fonction de la personne qui a créé l’audience. |
| [!UICONTROL Date de création] | Permet de filtrer en fonction de la date de création de l’audience. Vous pouvez choisir une période pour filtrer la date de création de l’audience. |
| [!UICONTROL Date de modification] | Permet de filtrer en fonction la date de dernière modification de l’audience. Vous pouvez choisir une période pour filtrer la date de la dernière modification de l’audience. |

![Les filtres disponibles sont affichés et mis en surbrillance sur la page d’accès aux audiences.](../images/ui/overview/filter-audiences.png)

### Détails de l’audience {#audience-details}

Pour afficher plus de détails sur une audience spécifique, sélectionnez le nom d’une audience dans l’onglet **[!UICONTROL Parcourir]**.

La page Détails de l’audience s’affiche. En haut se trouve un résumé de l’audience, des informations sur la taille de l’audience qualifiée, ainsi que les destinations pour lesquelles le segment est activé.

![La page des détails de l’audience s’affiche. Le résumé de l’audience, l’audience totale et les cartes de destinations activées sont mis en surbrillance.](../images/ui/overview/audience-details-summary.png)

**Résumé de l’audience** {#segment-summary}

La section **[!UICONTROL Résumé de l’audience]** fournit des informations telles que l’identifiant, le nom, la description, l’origine et les détails des attributs.

De plus, vous avez la possibilité d’activer l’audience vers une destination, d’appliquer des libellés d’accès ou de modifier/mettre à jour l’audience.

Sélectionner **[!UICONTROL Activer vers la destination]** vous permet d’activer l’audience vers une destination. Pour plus d’informations sur l’activation d’une audience vers une destination, veuillez lire la [vue d’ensemble de l’activation](../../destinations/ui/activation-overview.md).

![Le bouton Activer à la destination est mis en surbrillance.](../images/ui/overview/audience-details-activate.png)

Sélectionner **[!UICONTROL Appliquer les libellés d’accès]** vous permet de gérer les libellés d’accès qui appartiennent à l’audience. Pour plus d’informations sur les libellés d’accès, veuillez lire la documentation sur la [gestion des libellés](../../access-control/abac/ui/labels.md).

![Le bouton Appliquer les libellés d’accès est mis en surbrillance.](../images/ui/overview/audience-details-access-labels.png)

>[!BEGINTABS]

>[!TAB Composition de l’audience]

![La page des détails de l’audience s’affiche, avec le bouton [!UICONTROL Ouvrir la composition] en surbrillance.](../images/ui/overview/audience-details-open-composition.png)

Sélectionner **[!UICONTROL Ouvrir la composition]** vous permet d’afficher votre audience dans la Composition de l’audience. Pour plus d’informations sur la Composition d’audience, consultez le [Guide de l’interface utilisateur de la Composition d’audience](./audience-composition.md).

>[!TAB Chargement personnalisé]

![La page des détails de l’audience s’affiche, avec le bouton [!UICONTROL Mettre à jour l’audience] en surbrillance.](../images/ui/overview/audience-details-update-audience.png)

Sélectionner **[!UICONTROL Mettre à jour l’audience]** vous permet de charger à nouveau une audience générée en externe. Pour plus d’informations sur l’importation d’une audience générée en externe, veuillez lire la section sur l’[importation d’une audience](#import-audience).

>[!TAB Segmentation Service]

![La page des détails de l’audience s’affiche, avec le bouton [!UICONTROL Modifier l’audience] en surbrillance.](../images/ui/overview/audience-details-edit-audience.png)

Sélectionner **[!UICONTROL Modifier l’audience]** vous permet de modifier votre audience dans le créateur de segments. Pour plus d’informations sur l’utilisation de l’espace de travail [!DNL Segment Builder], veuillez lire le [[!DNL Segment Builder] guide d’utilisation](./segment-builder.md).

>[!ENDTABS]

Sélectionner **[!UICONTROL Modifier les propriétés]** vous permet de modifier les détails de base de l’audience, tels que le nom, la description et les balises.

![](../images/ui/overview/audience-details-edit-properties.png)

**Audience totale** {#audience-total}

La section **[!UICONTROL Audience totale]** indique le nombre de profils qui remplissent les critères de l’audience.

Les estimations sont générées en utilisant une taille d’échantillon des données d’exemple du jour. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations dans la [section sur la génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création d’audiences.

**Destinations activées** {#activated-destinations}

La section **[!UICONTROL Destinations activées]** affiche les destinations pour lesquelles cette audience est activée.

>[!NOTE]
>
> Les destinations sont une fonctionnalité disponible avec [!DNL Adobe Real-Time Customer Data Platform] et vous permettent d’exporter des données vers des plateformes externes. Pour plus d’informations sur les destinations, veuillez lire la [présentation des destinations](../../destinations/home.md). Pour savoir comment activer un segment vers une destination, voir la [présentation de l’activation](../../destinations/ui/activation-overview.md).

**Exemples de profils** {#profile-samples}

Ci-dessous se trouvent des exemples de profils qui remplissent les critères du segment avec des informations détaillées, y compris l’identifiant [!DNL Profile], le prénom, le nom et l’adresse e-mail personnelle.

Le déclenchement de l’échantillonnage de données dépend de la méthode d’ingestion.

Pour l’ingestion par lots, la banque de profils est automatiquement analysée toutes les quinze minutes afin de déterminer si un nouveau lot a bien été ingéré depuis la dernière tâche d’échantillonnage exécutée. Si tel est le cas, la banque de profils est ensuite analysée afin de déterminer si le nombre d’enregistrements a changé d’au moins 5 %. Si ces conditions sont remplies, une nouvelle tâche d’échantillonnage est déclenchée.

Pour l’ingestion en flux continu, la banque de profils est automatiquement analysée toutes les heures afin de voir s’il y a eu au moins 5 % de changement dans le nombre d’enregistrements. Si cette condition est remplie, une nouvelle tâche d’échantillonnage est déclenchée.

La taille de l’échantillon dépend du nombre total d’entités dans votre banque de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Des informations plus détaillées sur chaque [!DNL Profile] peuvent être consultées en sélectionnant l’identifiant [!DNL Profile]. Pour en savoir plus sur les détails d’un profil, veuillez lire le [[!DNL Real-Time Customer Profile] guide de l’utilisateur](../../profile/ui/user-guide.md#profile-detail).

![Les exemples de profil d’audience sont mis en surbrillance. Les informations d’exemples de profil incluent l’identifiant du profil, le prénom, le nom et l’adresse e-mail de la personne.](../images/ui/overview/audience-details-profiles.png)

### Créer une audience {#create-audience}

Vous pouvez sélectionner **[!UICONTROL Créer une audience]** pour créer une audience.

![Sur la page de navigation de l’audience, le bouton Créer une audience est mis en surbrillance.](../images/ui/overview/browse-create-audience.png)

Une fenêtre contextuelle s’affiche, vous permettant de choisir entre composer une audience ou créer des règles.

![Une fenêtre contextuelle qui affiche les deux types d’audiences que vous pouvez créer.](../images/ui/overview/create-audience-type.png)

**Composition de l’audience** {#audience-composition}

Sélectionner **[!UICONTROL Composer les audiences]** vous conduit à la Composition de l’audience. Cet espace de travail fournit des commandes intuitives pour la création et la modification des audiences, telles que le glisser-déposer de mosaïques utilisées pour représenter les différentes actions. Pour en savoir plus sur la création d’audiences, veuillez lire le [guide de la Composition d’audience](./audience-composition.md).

![L’espace de travail de Composition d’audience s’affiche.](../images/ui/overview/audience-composition.png)

**Créateur de segments** {#segment-builder}

Sélectionner **[!UICONTROL Créer une règle]** vous dirige vers le créateur de segments. L’espace de travail fournit des commandes intuitives pour la création et la modification de définitions de segment, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données. Pour en savoir plus sur la création de définitions de segment, consultez le [guide du créateur de segments](./segment-builder.md)

![L‘espace de travail du créateur de segments s’affiche.](../images/ui/overview/segment-builder.png)

### Importer une audience {#import-audience}

Vous pouvez sélectionner **[!UICONTROL Importer une audience]** pour importer une audience générée en externe.

![Sur la page de navigation d’audience, le bouton Importer une audience est mis en surbrillance.](../images/ui/overview/browse-import-audience.png)

Le workflow **[!UICONTROL Importer un fichier CSV d’audience]** s’affiche. Vous pouvez sélectionner un fichier CSV à importer en tant qu’audience générée en externe.

![Dans le workflow [!UICONTROL Importer un fichier CSV d’audience], la zone [!UICONTROL Glisser-déposer des fichiers] est mise en surbrillance, indiquant où vous pouvez charger votre audience générée en externe.](../images/ui/overview/import-audience-csv.png)

>[!NOTE]
>
>L’audience générée en externe **doit** être au format CSV, disposer d’un **maximum** de 11 colonnes et être inférieure à 1 Go.

Après avoir sélectionné le fichier CSV à importer, une liste de données d’exemple s’affiche pour cette audience générée en externe. Après avoir confirmé que les données d’exemple sont correctes, sélectionnez **[!UICONTROL Suivant]**.

![Des données d’exemple de l’audience générée en externe s’affichent.](../images/ui/overview/import-audience-sample-data.png)

La page **[!UICONTROL Détails de l’audience]** s’affiche. Vous pouvez ajouter des informations sur votre audience, notamment son nom, sa description, son identité principale et sa valeur d’espace de noms d’identité.

Lors de l&#39;import de l&#39;audience générée en externe, vous devez sélectionner l&#39;une des colonnes pour le champ d&#39;identité principal et spécifier la valeur de l&#39;espace de noms. Veuillez noter que tous les champs restants seront pris en compte. **attributs payload**. Ces attributs sont considérés comme **non durable**, car ils ne sont associés à cette audience qu’à des fins de personnalisation, et sont **not** connecté au profil.

![La page [!UICONTROL Détails de l’audience] s’affiche.](../images/ui/overview/import-audience-audience-details.png)

Après avoir renseigné les détails de votre audience, sélectionnez **[!UICONTROL Suivant]**.

![Le bouton [!UICONTROL Suivant] est mis en surbrillance sur la page [!UICONTROL Détails de l’audience].](../images/ui/overview/import-audience-filled-details.png)

La page **[!UICONTROL Réviser]** s’affiche. Vous pouvez consulter les détails de l’audience générée en externe nouvellement importée.

![La page [!UICONTROL Réviser] s’affiche, avec les détails de votre audience générée en externe nouvellement importée.](../images/ui/overview/import-audience-review-details.png)

Une fois que les détails sont corrects, sélectionnez **[!UICONTROL Terminer]** pour importer votre audience générée en externe dans Adobe Experience Platform.

>[!IMPORTANT]
>
>Par défaut, les audiences générées en externe ont une expiration de données de 30 jours. L’expiration des données est réinitialisée si l’audience est mise à jour ou modifiée de quelque manière que ce soit.
>
>De plus, si votre audience générée en externe contient des informations sensibles et/ou liées à la santé, vous **must** appliquez les libellés d’utilisation des données nécessaires avant de l’activer vers n’importe quelle destination. Pour plus d’informations sur l’application des libellés d’utilisation des données, consultez la documentation sur [gestion des libellés](../../access-control/abac/ui/labels.md).

## Segmentation planifiée {#scheduled-segmentation}

Une fois les audiences créées, vous pouvez les évaluer par le biais d’une évaluation sur demande ou planifiée (continue). L’évaluation consiste à déplacer les données [!DNL Real-Time Customer Profile] par le biais de traitements de segment afin de former des audiences correspondantes. Une fois créées, les audiences sont enregistrées et stockées afin de pouvoir être exportées à l’aide d’API [!DNL Experience Platform].

L’évaluation sur demande nécessite l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, alors que l’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour évaluer les audiences à un moment précis (au maximum, une fois par jour).

### Activer la segmentation planifiée {#enable-scheduled-segmentation}

Vous pouvez activer les audiences pour une évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. Dans l’interface utilisateur, revenez à l’onglet **[!UICONTROL Parcourir]** dans **[!UICONTROL Audiences]** et activez l’option **[!UICONTROL Planifier toutes les audiences]**. Toutes les audiences sont alors évaluées en fonction du planning défini par votre organisation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les sandbox avec un maximum de cinq (5) politiques de fusion pour [!DNL XDM Individual Profile]. Si votre organisation compte plus de cinq politiques de fusion pour [!DNL XDM Individual Profile] dans une seul sandbox, vous ne pourrez pas procéder à l’évaluation planifiée.

Actuellement, les plannings ne peuvent être créés qu’à l’aide de l’API. Pour obtenir des instructions détaillées sur la création, la modification et l’utilisation des plannings à l’aide de l’API, suivez le tutoriel relatif à l’évaluation des résultats de segmentation et à leur accès, en particulier la section sur [l’évaluation planifiée à l’aide de l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![Le bouton (bascule) Planifier toutes les audiences est mis en surbrillance sur la page de navigation des audiences.](../images/ui/overview/browse-audiences-scheduled.png)

## Compositions {#compositions}

Sélectionnez l’onglet **[!UICONTROL Compositions]** pour afficher la liste de toutes les audiences générées par le biais de la Composition d’audience pour votre organisation.

![Liste des audiences créées dans la Composition d’audience pour votre organisation.](../images/ui/overview/compositions.png)

Par défaut, cette vue répertorie les informations sur les audiences, notamment les éléments suivants : Nom, Statut, Date de création, Créé par, Dernière date de mise à jour et Dernière mise à jour par.

Vous pouvez sélectionner l’icône ![Personnaliser le tableau](../images/ui/overview/customize-table.png) pour modifier les champs affichés.

![Le bouton Personnaliser le tableau est mis en surbrillance. Sélectionnez ce bouton pour personnaliser les champs affichés sur la page de Composition d’audience.](../images/ui/overview/compositions-select-customize-table.png)

Une fenêtre contextuelle s’affiche, répertoriant tous les champs pouvant être affichés dans le tableau.

![Attributs pouvant être affichés pour la section Composition.](../images/ui/overview/compositions-customize-table.png)

| Champ | Description |
| ----- | ----------- | 
| [!UICONTROL Nom] | Nom de l’audience. |
| [!UICONTROL Statut] | Statut de l’audience. Les valeurs possibles pour ce champ incluent `Draft`, `Published` et `Archived`. |
| [!UICONTROL Créé] | Heure et date de création de l’audience. |
| [!UICONTROL Créé par] | Nom de la personne qui a créé l’audience. |
| [!UICONTROL Mis à jour] | Heure et date de la dernière mise à jour de l’audience. |
| [!UICONTROL Mise à jour par] | Nom de la personne qui a mis à jour l’audience pour la dernière fois. |

Pour afficher la composition de l’audience, sélectionnez le nom d’une audience sous l’onglet [!UICONTROL Audiences].

La page Composition d’audience s’affiche avec les blocs de création qui composent votre audience. Pour plus d’informations sur l’utilisation de la Composition d’audience, consultez le [guide de l’interface utilisateur de la Composition d’audience](./audience-composition.md).

## Segmentation en flux continu {#streaming-segmentation}

La segmentation en flux continu est la possibilité d’effectuer une segmentation sur [!DNL Platform] en temps quasi réel, tout en se concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification pour la segmentation se produit désormais lorsque les données entrent dans [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation.

Vous trouverez plus d’informations sur la segmentation en flux continu dans le [guide d’utilisation de la segmentation en flux continu](./streaming-segmentation.md).

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’organisation. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à [la section sur la segmentation en flux continu dans le guide d’utilisation sur la segmentation](#scheduled-segmentation).

## Segmentation Edge {#edge-segmentation}

La segmentation Edge permet d’évaluer les audiences dans Platform instantanément sur le serveur Edge, en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante.

Vous trouverez plus d’informations sur la segmentation Edge dans le [guide de l’interface utilisateur de segmentation Edge](./edge-segmentation.md).

## Violations de politique

>[!NOTE]
>
>Les violations de politique ne s’appliquent que si vous créez une audience qui a été affectée à une destination.

Une fois l’audience créée, elle est analysée par la gouvernance des données d’Adobe Experience Platform afin de s’assurer qu’il n’y a aucune violation de politique dans l’audience. Pour plus d’informations, consultez la [vue d’ensemble de la gouvernance des données](../../data-governance/home.md).

![Les violations de politique pour l’audience s’affichent.](../images/ui/overview/audience-dule-policy-violations.png)

## Étapes suivantes et ressources supplémentaires {#next-steps}

L’interface utilisateur de [!DNL Segmentation Service] fournit un workflow complet qui vous permet de créer les audiences commercialisables des données [!DNL Real-Time Customer Profile].

Pour en savoir plus sur [!DNL Segmentation Service], veuillez continuer à lire la documentation. Pour savoir comment utiliser l’API [!DNL Segmentation Service], consultez le [[!DNL Segmentation Service] guide de développement](../api/overview.md).
