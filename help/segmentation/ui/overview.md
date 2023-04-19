---
keywords: Experience Platform;accueil;rubriques les plus consultées;Segmentation Service;segmentation;service de segmentation;guide de l’utilisateur;guide de l’interface utilisateur;guide de l’interface utilisateur de segmentation;créateur de segments;réalisé;existant;sortant;
solution: Experience Platform
title: Guide de l’IU de Segmentation Service
description: Adobe Experience Platform Segmentation Service fournit une interface utilisateur pour la création et la gestion des définitions de segment.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '2650'
ht-degree: 98%

---

# Guide de l’IU de Segmentation Service

[!DNL Adobe Experience Platform Segmentation Service] fournit une interface utilisateur pour la création et la gestion des définitions de segment.

## Prise en main

L’utilisation des définitions de segment exige une compréhension des différents services [!DNL Experience Platform] concernés par la segmentation. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Segmentation Service]](../home.md) : [!DNL Segmentation Service] permet de diviser les données stockées dans [!DNL Experience Platform] qui se rapportent aux individus (tels que les client(e)s, les prospects, les utilisateurs et utilisatrices ou les organisations) en groupes plus petits.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md) : permet la création de profils client en rapprochant des identités de sources de données disparates ingérées dans [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).

Il est également important de connaître deux termes clés utilisés dans ce document et de comprendre la différence entre eux :
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment. Cela peut être créé via Adobe Experience Platform (audience générée par Platform) ou à partir d’une source externe (audience générée en externe).

## Présentation

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Segments]** dans le volet de navigation de gauche pour ouvrir l’onglet **[!UICONTROL Vue d’ensemble]** affichant le tableau de bord des [!UICONTROL segments].

>[!NOTE]
>
>Si votre organisation débute sur Platform et n’a pas encore de jeux de données de profils actifs ou de stratégies de fusion créés, le tableau de bord [!UICONTROL Segments] n’est pas visible. Au lieu de cela, l’onglet [!UICONTROL Vue d’ensemble] affiche des liens et de la documentation pour vous aider à démarrer avec la segmentation.

### Tableau de bord des [!UICONTROL segments] {#segments-dashboard}

Le tableau de bord des **[!UICONTROL segments]** décrit les mesures clés liées aux données de segment de votre organisation.

Pour en savoir plus, consultez le [guide du tableau de bord des segments](../../dashboards/guides/segments.md).

![Le tableau de bord de segments s’affiche. Il affiche divers widgets, notamment la taille de l’audience, les profils par identité, la superposition des identités et la tendance de changement de la taille de l’audience.](../../dashboards/images/segments/dashboard-overview.png)

## Parcourir {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Attrition"
>abstract="L’attrition représente le pourcentage de profils qui changent dans une définition de segment par rapport à la dernière exécution de la tâche de segmentation."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Méthode d’évaluation"
>abstract="Les méthodes d’évaluation des segments incluent le traitement par lots, en flux continu et Edge."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Ajouter tous les segments à planifier"
>abstract="Activez cette option pour inclure tous les segments d’évaluation par lots dans la mise à jour planifiée quotidienne. Désactivez cette option pour supprimer tous les segments de la mise à jour planifiée."

Sélectionnez l’onglet **[!UICONTROL Parcourir]** pour afficher une liste de toutes les définitions de segment pour votre organisation.

![L’écran de navigation des segments s’affiche. Une liste de tous les segments appartenant à l’organisation s’affiche.](../images/ui/overview/segment-browse-all.png)

Cette vue contient des informations sur la définition de segment, y compris le nombre de profils, la date de création et la date de dernière modification.

Vous pouvez ajouter des champs supplémentaires à cet affichage en sélectionnant ![l’icône d’attribut de filtre](../images/ui/overview/filter-attribute.png). Ces champs supplémentaires comprennent la répartition, la méthode d’évaluation et l’ID de tâche.

Si la ventilation est sélectionnée, l’affichage affiche un graphique à barres indiquant le pourcentage de profils appartenant à chacun des statuts de profil calculé suivants : [!UICONTROL Réalisé] et [!UICONTROL Quitter]. De plus, la répartition affichée dans l’onglet [!UICONTROL Parcourir] est la répartition la plus précise du statut du segment. Si ce nombre diffère de ce qui est indiqué dans l’onglet [!UICONTROL Vue d’ensemble], vous devez utiliser les nombres de l’onglet [!UICONTROL Parcourir] comme source d’informations correcte, puisque les nombres de l’onglet [!UICONTROL Vue d’ensemble] ne sont mis à jour qu’une seule fois par jour.

| État | Description |
| ------ | ----------- |
| Réalisé | Le nombre de profils qui remplissent les critères pour le segment au cours des dernières 24 heures. C’est-à-dire, le nombre de profils qui remplissent les critères du segment depuis la dernière exécution de la tâche de segmentation par lots. |
| Sortant | Le nombre de profils ayant quitté le segment au cours des dernières 24 heures. Il s’agit donc du nombre de profils qui ne sont plus qualifiés pour le segment depuis la dernière exécution de la tâche de segmentation par lots. |

La méthode d’évaluation peut être soit en flux continu, par lots ou Edge. Les segments en streaming sont constamment évalués au fur et à mesure que les données entrent dans le système. Les segments par lot sont évalués selon un planning établi. Les segments Edge évaluent les segments en temps réel, ce qui permet d’utiliser les cas d’utilisation de personnalisation de la même page et de la page suivante.

![Les segments de la page de navigation des segments sont mis en surbrillance.](../images/ui/overview/segment-browse-segments.png)

En haut de la page se trouvent les options permettant d’ajouter tous les segments à un planning et de créer un nouveau segment.

Basculer vers **[!UICONTROL Ajouter tous les segments à planifier]** active la segmentation planifiée. Vous trouverez plus d’informations sur la segmentation planifiée dans la [section segmentation planifiée de ce guide d’utilisation](#scheduled-segmentation).

Sélectionner **[!UICONTROL Créer un segment]** vous amènera au créateur de segments. Pour en savoir plus sur la création de segments, consultez la section sur la [création d’un segment dans le guide d’utilisation](#create-segment).

![La barre de navigation supérieure de la page de navigation des segments est mise en surbrillance. Cette barre contient un bouton (bascule) permettant d’ajouter tous les segments à un planning et un bouton permettant de créer un segment.](../images/ui/overview/segment-browse-top.png)

La barre latérale droite contient des informations sur tous les segments de l’organisation, répertoriant le nombre total de segments, la date de dernière évaluation, la date d’évaluation suivante, ainsi qu’une répartition des segments par méthode d’évaluation.

![La barre latérale droite de la page de navigation des segments est mise en surbrillance. Des informations sur les segments dans l’organisation s’affichent. Cela inclut des informations telles que le nombre total de segments, l’heure de la dernière évaluation, l’heure de la prochaine évaluation, ainsi qu’une répartition des différents types de segments.](../images/ui/overview/segment-browse-segment-info.png)

La sélection de la ligne de la définition de segment fournit un résumé de la définition de segment, y compris des options permettant de modifier ou de supprimer le segment, d’activer le segment vers une destination, l’audience qualifiée pour le segment, la taille totale de l’audience, en plus du nom du segment, de la description, de la méthode d’évaluation, de la date de création et de la date de dernière modification.

>[!NOTE]
>
> Vous **ne pourrez pas** supprimer un segment utilisé dans une activation de destination.

![Des détails sur le segment sélectionné s’affichent. Cela inclut des détails sur le nombre de profils qualifiés, la répartition en pourcentage des profils qualifiés par rapport au total des profils et la date de la dernière évaluation.](../images/ui/overview/segment-browse-details.png)

## Détails de la définition de segment {#segment-details}

Pour afficher plus d’informations sur une définition de segment spécifique, sélectionnez le nom d’un segment dans l’onglet **[!UICONTROL Parcourir]**.

La page Détails du segment s’affiche. En haut se trouve un résumé de la définition de segment, des informations sur la taille d’audience qualifiée, ainsi que les destinations pour lesquelles le segment est activé.

![La page de détails de la définition de segment s’affiche. Le résumé du segment, l’audience totale dans le segment et les cartes de destinations activées sont mis en surbrillance.](../images/ui/overview/segment-details-summary.png)

### Résumé du segment {#segment-summary}

Le **[!UICONTROL résumé du segment]** fournit des informations telles que l’identifiant, le nom, la description et les détails des attributs.

De plus, vous avez la possibilité d’activer le segment vers une destination ou de le modifier. Sélectionner **[!UICONTROL Activer vers la destination]** vous permet d’activer le segment vers une destination. Pour plus d’informations sur l’activation d’un segment vers une destination, veuillez lire la [présentation de l’activation](../../destinations/ui/activation-overview.md).

![Le bouton Activer à la destination est mis en surbrillance.](../images/ui/overview/segment-details-activate.png)

Sélectionner **[!UICONTROL Modifier le segment]** vous amènera au [!DNL Segment Builder]. Pour plus d’informations sur l’utilisation de l’espace de travail [!DNL Segment Builder], veuillez lire le [[!DNL Segment Builder] guide de l’utilisateur](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Audience totale dans le segment

La section **[!UICONTROL Audience totale dans le segment]** indique le nombre total de profils qui remplissent les critères du segment.

Les estimations sont générées en utilisant une taille d’échantillon des données d’exemple du jour. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

### Destinations activées

La section **[!UICONTROL Destinations activées]** affiche les destinations pour lesquelles ce segment est activé.

>[!NOTE]
>
> Les destinations sont une fonctionnalité disponible avec [!DNL Adobe Real-Time Customer Data Platform] et vous permettent d’exporter des données vers des plateformes externes. Pour plus d’informations sur les destinations, veuillez lire la [présentation des destinations](../../destinations/home.md). Pour savoir comment activer un segment vers une destination, voir la [présentation de l’activation](../../destinations/ui/activation-overview.md).

### Exemples de profils

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

![Les exemples de profils pour la définition de segment sont mis en surbrillance. Les informations d’exemples de profil incluent l’identifiant du profil, le prénom, le nom et l’adresse e-mail de la personne.](../images/ui/overview/segment-details-profiles.png)

## Créer un segment {#create-segment}

Cliquez sur **[!UICONTROL Créer un segment]** dans le coin supérieur droit pour ouvrir l’espace de travail du [!DNL Segment Builder], où vous pouvez commencer à créer une définition de segment.

![Sur la page de navigation de segment, le bouton Créer un segment est mis en surbrillance.](../images/ui/overview/segment-browse-create.png)

### Espace de travail [!DNL Segment Builder]

Le [!DNL Segment Builder] offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de [!DNL Profile]. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

Pour plus d’informations sur l’utilisation de l’espace de travail du [!DNL Segment Builder], veuillez lire le [[!DNL Segment Builder] guide de l’utilisateur](./segment-builder.md).

![L‘espace de travail du créateur de segments s’affiche.](../images/ui/overview/segment-builder.png)

## Segmentation planifiée {#scheduled-segmentation}

Une fois les définitions de segment créées, vous pouvez les évaluer par le biais d’une évaluation sur demande ou planifiée (continue). L’évaluation consiste à déplacer les données [!DNL Real-Time Customer Profile] par le biais de définitions de segment afin de former des audiences correspondantes. Une fois créées, les audiences sont enregistrées et stockées afin de pouvoir être exportées à l’aide d’API [!DNL Experience Platform].

L’évaluation sur demande nécessite l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, alors que l’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour évaluer les définitions de segment à un moment précis (au maximum, une fois par jour).

### Activer la segmentation planifiée {#enable-scheduled-segmentation}

Vous pouvez activer les définitions de segment pour une évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. Dans l’interface utilisateur, revenez à l’onglet **[!UICONTROL Parcourir]** dans **[!UICONTROL Segments]** et activez l’option **[!UICONTROL Ajouter tous les segments à planifier]**. Tous les segments seront alors évalués en fonction du planning défini par votre organisation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les sandbox avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. Si votre organisation compte plus de cinq stratégies de fusion pour [!DNL XDM Individual Profile] dans un seul sandbox, vous ne pourrez pas procéder à l’évaluation planifiée.

Actuellement, les plannings ne peuvent être créés qu’à l’aide de l’API. Pour obtenir des instructions détaillées sur la création, la modification et l’utilisation des plannings à l’aide de l’API, suivez le tutoriel relatif à l’évaluation et à l’accès aux résultats de segmentation, en particulier la section sur [l’évaluation planifiée à l’aide de l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![Le bouton (bascule) Ajouter tous les segments à un planning est mis en surbrillance sur la page de navigation des segments.](../images/ui/overview/segment-browse-scheduled.png)

## Audiences {#audiences}

>[!IMPORTANT]
>
>La fonctionnalité des audiences est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs et utilisatrices. La documentation et les fonctionnalités peuvent changer.

Sélectionnez l’onglet **[!UICONTROL Audiences]** pour afficher la liste de toutes les audiences de votre organisation.

![Liste des audiences de votre organisation.](../images/ui/overview/list-audiences.png)

Par défaut, cette vue répertorie les informations sur les audiences, notamment le nom, le nombre de profils, l’origine, la date de création et la date de dernière modification.

Vous pouvez sélectionner l’icône ![Personnaliser le tableau](../images/ui/overview/customize-table.png) pour modifier les champs affichés.

![Le bouton Personnaliser le tableau est mis en surbrillance. En sélectionnant ce bouton, vous pouvez personnaliser les champs affichés sur la page de navigation Audiences.](../images/ui/overview/select-customize-table.png)

Une fenêtre contextuelle s’affiche, répertoriant tous les champs pouvant être affichés dans le tableau.

![Attributs pouvant être affichés pour la section Parcourir les audiences.](../images/ui/overview/customize-table-attributes.png)

| Champ | Description |
| ----- | ----------- | 
| [!UICONTROL Nom] | Nom de l’audience. |
| [!UICONTROL Nombre de profils] | Nombre total de profils qui remplissent les critères de l’audience. |
| [!UICONTROL Origine] | Origine de l’audience. Si cette audience a été générée par Platform, elle aura une origine de Segmentation Service. |
| [!UICONTROL Statut du cycle de vie] | Statut de l’audience. Les valeurs possibles pour ce champ incluent `Draft`, `Published` et `Archived`. |
| [!UICONTROL Fréquence de mise à jour] | Valeur qui indique la fréquence de mise à jour des données de l’audience. Les valeurs possibles pour ce champ incluent `On Demand`, `Scheduled` et `Continuous`. |
| [!UICONTROL Dernière mise à jour par] | Nom de la personne qui a mis à jour l’audience pour la dernière fois. |
| [!UICONTROL Créé] | Heure et date de création de l’audience. |
| [!UICONTROL Dernière mise à jour] | Heure et date de la dernière création de l’audience. |
| [!UICONTROL Libellés d’accès] | Libellés d’accès pour l’audience. Les libellés d’accès vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Pour plus d’informations sur les libellés d’accès, veuillez lire la documentation sur la [gestion des libellés](../../access-control/abac/ui/labels.md). |

Vous pouvez sélectionner **[!UICONTROL Créer une audience]** pour créer une audience.

![Le bouton Créer une audience est mis en surbrillance et indique l’emplacement à sélectionner pour créer une audience.](../images/ui/overview/create-audience.png)

Une fenêtre contextuelle s’affiche, vous permettant de choisir entre composer une audience ou créer des règles.

![Une fenêtre contextuelle qui affiche les deux types d’audiences que vous pouvez créer.](../images/ui/overview/create-audience-type.png)

Sélectionner **[!UICONTROL Composer les audiences]** vous conduit au créateur d’audiences. Pour en savoir plus sur la création d’audiences, veuillez lire le [Guide du créateur d’audiences](./audience-builder.md).

Sélectionner **[!UICONTROL Créer une règle]** vous dirige vers le créateur de segments. Pour en savoir plus sur la création de segments, consultez le [Guide du créateur de segments](./segment-builder.md).

## Détails de l’audience {#audience-details}

Pour afficher plus de détails sur une audience spécifique, sélectionnez le nom d’une audience dans l’onglet [!UICONTROL Audiences].

La page Détails de l’audience s’affiche. Cette page diffère en détails selon que l’audience a été générée avec Adobe Experience Platform ou à partir d’une source externe telle qu’Audience Orchestration.

### Audience générée par Platform

Pour plus d’informations sur les audiences générées par Platform, veuillez lire la [section de résumé du segment](#segment-summary).

### Audience générée de manière externe

En haut de la page des détails de l’audience se trouve un résumé de l’audience et des détails sur le jeu de données dans lequel l’audience est enregistrée.

![Détails fournis pour une audience générée de manière externe.](../images/ui/overview/externally-generated-audience.png)

La section **[!UICONTROL Résumé de l’audience]** fournit des informations telles que l’identifiant, le nom, la description et les détails des attributs.

La section **[!UICONTROL Détails du jeu de données]** fournit des informations telles que le nom, la description, le nom de la table, la source et le schéma. Vous pouvez sélectionner **[!UICONTROL Afficher le jeu de données]** pour afficher plus d’informations sur le jeu de données.

| Champ | Description |
| ----- | ----------- |
| [!UICONTROL Nom] | Nom du jeu de données. |
| [!UICONTROL Description] | Description du jeu de données. |
| [!UICONTROL Nom de la table] | Nom de la table du jeu de données. |
| [!UICONTROL Source] | Source du jeu de données. Pour les audiences générées en externe, cette valeur sera **Schéma**. |
| [!UICONTROL Schéma] | Type de schéma XDM auquel le jeu de données correspond. |

Pour en savoir plus sur les jeux de données, veuillez lire la [présentation des jeux de données](../../catalog/datasets/overview.md).

## Segmentation en flux continu {#streaming-segmentation}

La segmentation en flux continu est la possibilité d’effectuer une segmentation sur [!DNL Platform] en temps quasi réel, tout en se concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit désormais lorsque les données entrent dans [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation.

Vous trouverez plus d’informations sur la segmentation en flux continu dans le [guide d’utilisation de la segmentation en flux continu](./streaming-segmentation.md).

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’organisation. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à [la section sur la segmentation en flux continu dans le guide d’utilisation sur la segmentation](#scheduled-segmentation).

## Segmentation Edge {#edge-segmentation}

La segmentation Edge permet d’évaluer les segments dans Adobe Experience Platform instantanément sur le serveur Edge, en activant les cas d’utilisation de la personnalisation sur une même page et sur la page suivante.

Vous trouverez plus d’informations sur la segmentation Edge dans le [guide de l’interface utilisateur de segmentation Edge](./edge-segmentation.md).

## Violations de stratégie

>[!NOTE]
>
>Les violations de stratégie ne s’appliquent que si vous créez un segment qui a été affecté à une destination.

Une fois le segment créé, il est analysé par la gouvernance des données d’Adobe Experience Platform afin de s’assurer qu’il n’y a aucune violation de stratégie dans le segment. Pour plus d’informations, consultez la [présentation de la gouvernance des données](../../data-governance/home.md).

![Les violations de politique pour le segment s’affichent.](../images/ui/overview/segment-dule-policy-violations.png)

## Étapes suivantes et ressources supplémentaires {#next-steps}

L’interface utilisateur de [!DNL Segmentation Service] fournit un workflow complet qui vous permet d’isoler les audiences commercialisables des données [!DNL Real-Time Customer Profile].

Pour en savoir plus sur [!DNL Segmentation Service], veuillez continuer à lire la documentation. Pour savoir comment utiliser l’API [!DNL Segmentation Service], consultez le [[!DNL Segmentation Service] guide de développement](../api/overview.md).
