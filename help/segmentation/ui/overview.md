---
keywords: Experience Platform;accueil;rubriques les plus consultées;Segmentation Service;segmentation;service de segmentation;guide de l’utilisateur;guide de l’interface utilisateur;guide de l’interface utilisateur de segmentation;créateur de segments;réalisé;existant;sortie ;
solution: Experience Platform
title: Guide de l’interface utilisateur de Segmentation Service
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service fournit une interface utilisateur pour la création et la gestion des définitions de segment.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 998332007465c1f8457b5d8cf0e153d513505d39
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 25%

---

# Guide de l’interface utilisateur de Segmentation Service

[!DNL Adobe Experience Platform Segmentation Service] fournit une interface utilisateur pour la création et la gestion des définitions de segment.

## Prise en main

L’utilisation des définitions de segment nécessite une compréhension des différents services [!DNL Experience Platform] impliqués dans la segmentation. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Segmentation Service]](../home.md):  [!DNL Segmentation Service] permet de diviser les données stockées dans  [!DNL Experience Platform] qui se rapportent à des individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits.
- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permet la création de profils client en rapprochant les identités de sources de données disparates ingérées dans  [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Il est également important de connaître deux termes clés utilisés dans ce document et de comprendre la différence entre eux :
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Présentation

Dans l’[[!DNL Experience Platform] interface utilisateur](https://platform.adobe.com/), sélectionnez **[!UICONTROL Segments]** dans le volet de navigation de gauche pour ouvrir l’onglet **[!UICONTROL Aperçu]**. Cet onglet fournit des liens vers la documentation et des vidéos pour vous aider à comprendre et à commencer à utiliser les segments.

![](../images/ui/overview/segment-overview.png)

### Tableau de bord Segments

Pour certains utilisateurs, la sélection de **[!UICONTROL Segments]** dans le volet de navigation de gauche et l’ouverture de l’onglet **[!UICONTROL Aperçu]** fournissent un tableau de bord décrivant les mesures clés liées aux données de votre segment.

Pour en savoir plus, consultez le [guide du tableau de bord des segments](segment-dashboard.md).

## Parcourir

Sélectionnez l’onglet **[!UICONTROL Parcourir]** pour afficher la liste de toutes les définitions de segment pour votre organisation IMS.

![](../images/ui/overview/segment-browse-all.png)

Cet affichage répertorie des informations sur la définition de segment, notamment la ventilation, la perte de clientèle, le nombre de profils, la méthode d’évaluation, la date de création et la date de dernière modification.

La ventilation présente un graphique à barres indiquant le pourcentage de profils appartenant à chacun des états suivants : [!UICONTROL Réalisée], [!UICONTROL Existante] et [!UICONTROL Sortie].

![](../images/ui/overview/segment-browse-breakdown.png)

| État | Description |
| ------ | ----------- |
| Réalisé | Un nouveau profil dans le segment. |
| Existant | Un profil existant qui est resté dans le segment. |
| Quitter | Un profil existant qui quitte le segment. |

L’attrition représente le pourcentage de profils qui changent dans une définition de segment par rapport à la dernière exécution de la tâche de segmentation, tandis que le nombre de profils représente le nombre total de profils qui remplissent les critères pour le segment.

La méthode d’évaluation peut être soit par flux, soit par lot. Les segments par flux sont constamment évalués au fur et à mesure que les données entrent dans le système. Les segments par lot sont évalués selon un planning établi.

![](../images/ui/overview/segment-browse-segments.png)

En haut de la page se trouvent les options permettant d’ajouter tous les segments à un planning et de créer un nouveau segment.

Si vous activez **[!UICONTROL Ajouter tous les segments pour planifier]**, la segmentation planifiée sera activée. Vous trouverez plus d’informations sur la segmentation planifiée dans la [section de segmentation planifiée de ce guide d’utilisation](#scheduled-segmentation).

Sélectionnez **[!UICONTROL Créer un segment]** pour accéder au créateur de segments. Pour en savoir plus sur la création de segments, consultez la section sur la [création d’un segment dans le guide de l’utilisateur](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

La barre latérale droite contient des informations sur tous les segments de l’organisation IMS, répertoriant le nombre total de segments, la date de dernière évaluation, la date d’évaluation suivante, ainsi qu’une ventilation des segments par méthode d’évaluation.

![](../images/ui/overview/segment-browse-segment-info.png)

La sélection de la ligne de la définition de segment fournit un résumé de la définition de segment, y compris des options permettant de modifier ou de supprimer le segment, l’audience qualifiée du segment, la taille totale de l’audience, en plus du nom, de la description, de la méthode d’évaluation, de la date de création et de la date de dernière modification du segment.

![](../images/ui/overview/segment-browse-details.png)

## Détails de la définition de segment {#segment-details}

Pour afficher plus d’informations sur une définition de segment spécifique, sélectionnez le nom d’un segment dans l’onglet **[!UICONTROL Parcourir]**.

La page des détails du segment s’affiche. En haut se trouve un résumé de la définition de segment, des informations sur la taille d’audience qualifiée, ainsi que les destinations pour lesquelles le segment est activé.

![](../images/ui/overview/segment-details-summary.png)

### Synthèse des segments

La section **[!UICONTROL Résumé du segment]** fournit des informations telles que l’identifiant, le nom, la description et les détails des attributs.

De plus, vous avez la possibilité de modifier le segment. Sélectionnez **[!UICONTROL Modifier le segment]** pour accéder à [!DNL Segment Builder]. Pour plus d’informations sur l’utilisation de l’espace de travail [!DNL Segment Builder], consultez le [[!DNL Segment Builder] guide d’utilisation](./segment-builder.md).

### Audience totale dans le segment

La section **[!UICONTROL Audience totale dans le segment]** indique le nombre total de profils qui remplissent les critères pour le segment.

Les estimations sont générées en utilisant une taille d’échantillon des données d’exemple de ce jour. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

### Destinations activées

La section **[!UICONTROL Destinations activées]** indique les destinations pour lesquelles ce segment est activé.

>[!NOTE]
>
> Les destinations sont une fonctionnalité disponible avec [!DNL Real-time Customer Data Platform] et vous permettent d’exporter des données vers des plateformes externes. Pour plus d’informations sur les destinations, consultez la [présentation des destinations](../../destinations/home.md). Pour savoir comment activer un segment vers une destination, consultez le [guide sur l’activation des segments vers une destination](../../destinations/ui/activate-destinations.md).

### Exemples de profils

Vous trouverez ci-dessous un échantillon de profils qui remplissent les critères du segment, et vous trouverez des informations détaillées, y compris l’ID [!DNL Profile], le prénom, le nom et l’adresse électronique personnelle.

Le déclenchement de l’échantillonnage de données dépend de la méthode d’ingestion.

Pour l’ingestion par lots, la banque de profils est automatiquement analysée toutes les quinze minutes afin de déterminer si un nouveau lot a bien été ingéré depuis la dernière tâche d’échantillonnage exécutée. Si tel est le cas, la banque de profils est ensuite analysée afin de déterminer si le nombre d’enregistrements a changé d’au moins 5 %. Si ces conditions sont remplies, une nouvelle tâche d’échantillonnage est déclenchée.

Pour l’ingestion par flux, la banque de profils est automatiquement analysée toutes les heures afin de voir s’il y a eu au moins 5 % de changement dans le nombre d’enregistrements. Si cette condition est remplie, une nouvelle tâche d’échantillonnage est déclenchée.

La taille de l’échantillon de l’analyse dépend du nombre total d’entités dans votre banque de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Vous trouverez des informations plus détaillées sur chaque [!DNL Profile] en sélectionnant l’ [!DNL Profile] ID. Pour en savoir plus sur les détails d’un profil, consultez le [[!DNL Real-time Customer Profile] guide de l’utilisateur](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Création d’un segment {#create-segment}

Sélectionnez **[!UICONTROL Créer un segment]** dans le coin supérieur droit pour ouvrir l’espace de travail [!DNL Segment Builder], où vous pouvez commencer à créer une définition de segment.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] espace de travail

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec les éléments  [!DNL Profile] de données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

Pour plus d’informations sur l’utilisation de l’espace de travail [!DNL Segment Builder], consultez le [[!DNL Segment Builder] guide d’utilisation](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Segmentation planifiée {#scheduled-segmentation}

Une fois les définitions de segment créées, vous pouvez les évaluer par le biais d’une évaluation sur demande ou planifiée (continue). L’évaluation consiste à déplacer des données [!DNL Real-time Customer Profile] par le biais de définitions de segment afin de produire des audiences correspondantes. Une fois créées, les audiences sont enregistrées et stockées afin de pouvoir être exportées à l&#39;aide des API [!DNL Experience Platform].

L’évaluation sur demande nécessite l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, alors que l’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour évaluer les définitions de segment à un moment précis (au maximum, une fois par jour).

### Activation de la segmentation planifiée {#enable-scheduled-segmentation}

Vous pouvez activer les définitions de segment pour une évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. Dans l’interface utilisateur, revenez à l’onglet **[!UICONTROL Parcourir]** dans **[!UICONTROL Segments]** et activez l’option **[!UICONTROL Ajouter tous les segments à planifier]**. Tous les segments seront alors évalués en fonction du planning défini par votre organisation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. Si votre organisation possède plus de cinq stratégies de fusion pour [!DNL XDM Individual Profile] dans un seul environnement de test, vous ne pourrez pas utiliser l’évaluation planifiée.

Actuellement, les plannings ne peuvent être créés qu’à l’aide de l’API. Pour obtenir des instructions détaillées sur la création, la modification et l’utilisation des plannings à l’aide de l’API, suivez le tutoriel relatif à l’évaluation et à l’accès aux résultats de segmentation, en particulier la section sur [l’évaluation planifiée à l’aide de l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentation par flux {#streaming-segmentation}

La segmentation par flux permet d’effectuer une segmentation sur [!DNL Platform] en temps quasi réel, tout en se concentrant sur la richesse des données. Avec la segmentation par flux, la qualification de segment se produit désormais lorsque les données entrent dans [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation.

Vous trouverez plus d’informations sur la segmentation par flux dans le [guide d’utilisation de la segmentation par flux](./streaming-segmentation.md).

>[!NOTE]
>
>Pour que la segmentation par flux fonctionne, vous devez activer la segmentation planifiée pour l’organisation. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à la [section de la segmentation par flux de ce guide d’utilisation](#scheduled-segmentation).

## Segmentation Edge {#edge-segmentation}

La segmentation Edge permet d’évaluer instantanément les segments dans Platform, ce qui permet d’utiliser des cas de personnalisation de page et de page suivante.

Vous trouverez plus d’informations sur la segmentation Edge dans le [guide de l’interface utilisateur de la segmentation Edge](./edge-segmentation.md)

## Violations de stratégie

>[!NOTE]
>
>Les violations de stratégie ne s’appliquent que si vous créez un segment qui a été affecté à une destination.

Une fois le segment créé, il est analysé par la gouvernance des données de Adobe Experience Platform afin de s’assurer qu’il n’y a aucune violation de stratégie dans le segment. Pour de plus amples informations, rendez-vous sur la [[!DNL Data Governance]  d’aperçu](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Étapes suivantes et ressources supplémentaires {#next-steps}

L’interface utilisateur [!DNL Segmentation Service] fournit un processus riche qui vous permet d’isoler les audiences commercialisables des données [!DNL Real-time Customer Profile].

Pour en savoir plus sur [!DNL Segmentation Service], veuillez continuer à lire la documentation. Pour savoir comment utiliser l’API [!DNL Segmentation Service], consultez le [[!DNL Segmentation Service] guide de développement](../api/overview.md).
