---
keywords: Experience Platform ; accueil ; rubriques populaires ; Service de segmentation ; segmentation ; service de segmentation ; guide de l’utilisateur ; guide de l’interface utilisateur ; guide de l’interface utilisateur de segmentation ; créateur de segments ; réalisation ; existante ; sortie ;
solution: Experience Platform
title: Guide de l'interface utilisateur du service de segmentation
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service fournit une interface utilisateur pour la création et la gestion des définitions de segments.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: d65bcf62f0de29dc293a1a1313178a408613a024
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 23%

---

# Guide de l’interface utilisateur du service de segmentation

[!DNL Adobe Experience Platform Segmentation Service] fournit une interface utilisateur pour la création et la gestion des définitions de segment.

## Prise en main

L’utilisation des définitions de segment nécessite une compréhension des différents [!DNL Experience Platform] services impliqués dans la segmentation. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] permet de diviser les données stockées dans [!DNL Experience Platform] qui se rapporte à des personnes (telles que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits.
- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permet la création de profils de clients en fusionnant les identités de sources de données disparates en cours d&#39;assimilation dans [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Il est également important de connaître deux termes clés utilisés dans ce document et de comprendre la différence entre eux :
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Présentation

Dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Segments]** dans le menu de navigation de gauche pour ouvrir la **[!UICONTROL Présentation]** affichant la [!UICONTROL Segments] tableau de bord.

>[!NOTE]
>
>Si votre entreprise n’est pas nouvelle dans la plate-forme et n’a pas encore créé de jeux de données de profil actifs ou de stratégies de fusion, la [!UICONTROL Segments] tableau de bord n&#39;est pas visible. Au lieu de cela, [!UICONTROL Présentation] affiche les liens et la documentation qui vous aideront à vous familiariser avec les segments.

### [!UICONTROL Segments] tableau de bord {#segments-dashboard}

Le **[!UICONTROL Segments]** le tableau de bord décrit les mesures clés liées aux données de segment de votre organisation.

Pour en savoir plus, consultez la page [guide du tableau de bord des segments](../../dashboards/guides/segments.md).

![](../../dashboards/images/segments/dashboard-overview.png)

## Parcourir

Sélectionnez l’option **[!UICONTROL Parcourir]** pour afficher la liste de toutes les définitions de segment pour votre organisation IMS.

![](../images/ui/overview/segment-browse-all.png)

Cette vue répertorie des informations sur la définition de segment, y compris la ventilation, l’organisation, le nombre de profils, la méthode d’évaluation, la date de création et la date de dernière modification.

La ventilation présente un graphique à barres décrivant le pourcentage de profils appartenant à chacun des états suivants : [!UICONTROL Réalisé], [!UICONTROL Existant]et [!UICONTROL Sortie]. En outre, la ventilation indiquée sur la [!UICONTROL Parcourir] est la ventilation la plus précise de l’état du segment. Si ce nombre diffère de ce qui est indiqué sur la [!UICONTROL Présentation] , vous devez utiliser les nombres figurant sur la [!UICONTROL Parcourir] comme source d’informations correcte, depuis [!UICONTROL Présentation] les numéros de tabulation ne sont mis à jour qu’une fois par jour.

![](../images/ui/overview/segment-browse-breakdown.png)

| État | Description |
| ------ | ----------- |
| Réalisé | Nouveau profil dans le segment. |
| Existant | Un profil existant qui est resté dans le segment. |
| Sortie | Un profil existant qui quitte le segment. |

L’unité représente le pourcentage de profils qui changent au sein d’une définition de segment par rapport à la dernière fois que la tâche de segment a été exécutée, tandis que le nombre de profils représente le nombre total de profils qui sont admissibles pour le segment.

La méthode d’évaluation peut être soit par flux, soit par lot. Les segments par flux sont constamment évalués au fur et à mesure que les données entrent dans le système. Les segments par lot sont évalués selon un planning établi.

![](../images/ui/overview/segment-browse-segments.png)

En haut de la page se trouvent les options permettant d’ajouter tous les segments à un planning et de créer un segment.

Basculement **[!UICONTROL Ajouter tous les segments à la planification]** active la segmentation planifiée. Pour plus d’informations sur la segmentation planifiée, consultez la section [section de segmentation planifiée de ce guide d’utilisateur](#scheduled-segmentation).

Sélection **[!UICONTROL Créer un segment]** vous amène au créateur de segments. Pour en savoir plus sur la création de segments, lisez la section sur [création d’un segment dans le guide de l’utilisateur](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

La barre latérale de droite contient des renseignements sur tous les segments de l&#39;organisation du SGI, indiquant le nombre total de segments, la date de la dernière évaluation, la date de la prochaine évaluation, ainsi qu&#39;une ventilation des segments par méthode d&#39;évaluation.

![](../images/ui/overview/segment-browse-segment-info.png)

La sélection de la ligne de la définition de segment fournit un résumé de la définition de segment, y compris des options pour modifier ou supprimer le segment, activer le segment vers une destination, l’audience qualifiée pour le segment, la taille totale de l’audience, en plus du nom du segment, de la description, de la méthode d’évaluation, de la date de création et de la date de dernière modification.

>[!NOTE]
>
> Vous **non** peuvent supprimer un segment utilisé dans une activation de destination.

![](../images/ui/overview/segment-browse-details.png)

## Détails de la définition de segment {#segment-details}

Pour afficher plus d’informations sur une définition de segment spécifique, sélectionnez le nom d’un segment dans la zone **[!UICONTROL Parcourir]** .

La page de détails du segment s’affiche. En haut, vous trouverez un résumé de la définition du segment, des informations sur la taille d’audience qualifiée, ainsi que les destinations pour lesquelles le segment est activé.

![](../images/ui/overview/segment-details-summary.png)

### Résumé des segments

Le **[!UICONTROL Résumé des segments]** fournit des informations telles que l’ID, le nom, la description et les détails des attributs.

En outre, vous avez la possibilité d’activer le segment vers une destination ou de le modifier. Sélection **[!UICONTROL Activer vers la destination]** vous permet d’activer le segment vers une destination. Pour plus d’informations sur l’activation d’un segment vers une destination, veuillez lire la section [présentation de l’activation](../../destinations/ui/activation-overview.md).

![](../images/ui/overview/segment-details-activate.png)

Sélection **[!UICONTROL Modifier le segment]** vous amènera au [!DNL Segment Builder]. Pour plus d’informations sur l’utilisation de la propriété [!DNL Segment Builder] espace de travail, lisez [[!DNL Segment Builder] guide de l’utilisateur](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Nombre total d’audiences dans le segment

Le **[!UICONTROL Nombre total d’audiences dans le segment]** affiche le nombre total de profils qui sont admissibles pour le segment.

Les estimations sont générées en utilisant une taille d&#39;échantillon des données d&#39;échantillon de cette journée. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

### Destinations activées

Le **[!UICONTROL Destinations activées]** affiche les destinations pour lesquelles ce segment est activé.

>[!NOTE]
>
> Les destinations sont une fonctionnalité disponible avec [!DNL Real-time Customer Data Platform]et vous permettent d’exporter des données vers des plates-formes externes. Pour plus d’informations sur les destinations, veuillez lire le fichier [présentation des destinations](../../destinations/home.md). Pour savoir comment activer un segment vers une destination, voir [présentation de l’activation](../../destinations/ui/activation-overview.md).

### Exemples de profils

En dessous se trouve un échantillon de profils qui répondent aux critères du segment, qui détaille les informations, y compris les [!DNL Profile] ID, prénom, nom et adresse électronique personnelle.

La façon dont l’échantillonnage des données est déclenché dépend de la méthode d’ingestion.

Pour l’assimilation par lots, le magasin de profils est automatiquement analysé toutes les quinze minutes pour voir si un nouveau lot a été correctement assimilé depuis la dernière tâche d’échantillonnage exécutée. Si tel est le cas, le magasin de profils est ensuite analysé pour voir s&#39;il y a eu au moins 5 % de changement dans le nombre d&#39;enregistrements. Si ces conditions sont remplies, une nouvelle tâche d’échantillonnage est déclenchée.

Pour la diffusion en continu, la banque de profils est automatiquement analysée toutes les heures pour voir s’il y a eu au moins 5 % de changement dans le nombre d’enregistrements. Si cette condition est remplie, une nouvelle tâche d’échantillonnage est déclenchée.

La taille de l’échantillon de l’analyse dépend du nombre total d’entités dans votre banque de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Informations plus détaillées sur chaque [!DNL Profile] peut être affiché en sélectionnant l’option [!DNL Profile] ID. Pour en savoir plus sur les détails d’un profil, lisez le fichier [[!DNL Real-time Customer Profile] guide de l’utilisateur](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Création d’un segment {#create-segment}

Sélection **[!UICONTROL Créer un segment]** dans le coin supérieur droit s’ouvre sur la [!DNL Segment Builder] , où vous pouvez commencer à créer une définition de segment.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] espace de travail

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec [!DNL Profile] éléments de données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

Pour plus d’informations sur l’utilisation de la propriété [!DNL Segment Builder] espace de travail, lisez [[!DNL Segment Builder] guide de l’utilisateur](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Segmentation planifiée {#scheduled-segmentation}

Une fois les définitions de segment créées, vous pouvez les évaluer par le biais d’une évaluation sur demande ou planifiée (continue). Évaluation signifie déménagement [!DNL Real-time Customer Profile] par le biais de définitions de segments afin de produire des publics correspondants. Une fois créés, les publics sont enregistrés et stockés afin qu’ils puissent être exportés à l’aide de [!DNL Experience Platform] API.

L’évaluation sur demande nécessite l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, alors que l’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour évaluer les définitions de segment à un moment précis (au maximum, une fois par jour).

### Activation de la segmentation planifiée {#enable-scheduled-segmentation}

Vous pouvez activer les définitions de segment pour une évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. Dans l’interface utilisateur, revenez à la **[!UICONTROL Parcourir]** dans **[!UICONTROL Segments]** et activer **[!UICONTROL Ajouter tous les segments à la planification]**. Tous les segments seront alors évalués en fonction du planning défini par votre organisation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. Si votre organisation a plus de cinq stratégies de fusion pour [!DNL XDM Individual Profile] dans un environnement sandbox unique, vous ne pourrez pas utiliser l’évaluation planifiée.

Actuellement, les plannings ne peuvent être créés qu’à l’aide de l’API. Pour obtenir des instructions détaillées sur la création, la modification et l’utilisation des plannings à l’aide de l’API, suivez le tutoriel relatif à l’évaluation et à l’accès aux résultats de segmentation, en particulier la section sur [l’évaluation planifiée à l’aide de l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentation par flux {#streaming-segmentation}

La segmentation en flux continu permet d’effectuer la segmentation sur [!DNL Platform] en temps quasi réel, tout en se concentrant sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit maintenant lorsque les données atterrissent dans [!DNL Platform], ce qui évite de devoir planifier et exécuter des tâches de segmentation.

Pour plus d’informations sur la segmentation de la diffusion en continu, consultez la section [guide de l’utilisateur de la segmentation en flux continu](./streaming-segmentation.md).

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’organisation. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à la section [la section de segmentation de diffusion dans ce guide d’utilisateur](#scheduled-segmentation).

## Segmentation des contours {#edge-segmentation}

La segmentation Edge permet d’évaluer instantanément les segments de la plate-forme sur le bord, ce qui permet d’utiliser des exemples d’utilisation de personnalisation de la même page et de la page suivante.

Pour plus d’informations sur la segmentation des contours, consultez la section [guide de l’interface utilisateur de segmentation des contours](./edge-segmentation.md)

## Violations de stratégie

>[!NOTE]
>
>Les violations de stratégie ne s&#39;appliquent que si vous créez un segment qui a été affecté à une destination.

Une fois que vous avez terminé la création de votre segment, celui-ci sera analysé par Adobe Experience Platform Data Governance pour s&#39;assurer qu&#39;il n&#39;y a aucune violation de stratégie au sein du segment. Pour plus d’informations, consultez la [[!DNL Data Governance] présentation](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Étapes suivantes et ressources supplémentaires {#next-steps}

Le [!DNL Segmentation Service] L’interface utilisateur fournit un flux de production riche qui vous permet d’isoler des publics commercialisables de [!DNL Real-time Customer Profile] données.

Pour en savoir plus sur [!DNL Segmentation Service], veuillez continuer à lire la documentation. Pour savoir comment utiliser l’outil [!DNL Segmentation Service] API, veuillez lire la section [[!DNL Segmentation Service] guide du développeur](../api/overview.md).
