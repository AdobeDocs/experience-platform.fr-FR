---
keywords: Experience Platform ; accueil ; rubriques populaires ; Service de segmentation ; segmentation ; service de segmentation ; guide de l’utilisateur ; guide de l’ui ; guide de segmentation ; guide de l’ui ; créateur de segments ; créateur de segments ; réalisé ; existant ; sortant ;
solution: Experience Platform
title: Guide de l’interface utilisateur du service de segmentation
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service fournit une interface utilisateur pour la création et la gestion des définitions de segment.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
translation-type: tm+mt
source-git-commit: fa2f4e046c6210137aa3e98d9f18010c1058275a
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 26%

---

# Guide de l’interface utilisateur du service de segmentation

[!DNL Adobe Experience Platform Segmentation Service] fournit une interface utilisateur pour la création et la gestion des définitions de segment.

## Prise en main

L&#39;utilisation des définitions de segment nécessite une compréhension des différents services [!DNL Experience Platform] impliqués dans la segmentation. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Segmentation Service]](../home.md):  [!DNL Segmentation Service] vous permet de diviser les données stockées dans  [!DNL Experience Platform] des données relatives à des individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits.
- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permet la création de profils client en faisant le lien entre les identités issues de sources de données disparates et qui sont incorporées dans  [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Il est également important de connaître deux termes clés utilisés dans ce document et de comprendre la différence entre eux :
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Présentation

Dans l’[[!DNL Experience Platform] interface utilisateur](https://platform.adobe.com/), sélectionnez **[!UICONTROL Segments]** dans le volet de navigation de gauche pour ouvrir l’onglet **[!UICONTROL Aperçu]**. Cet onglet fournit des liens vers la documentation et les vidéos pour vous aider à comprendre et à commencer à travailler avec les segments.

![](../images/ui/overview/segment-overview.png)

## Parcourir

Sélectionnez l&#39;onglet **[!UICONTROL Parcourir]** pour afficher une liste de toutes les définitions de segment pour votre organisation IMS.

![](../images/ui/overview/segment-browse-all.png)

Cette vue liste des informations sur la définition de segment, y compris la ventilation, l’exécution, le nombre de profils, la méthode d’évaluation, la date de création et la date de dernière modification.

La ventilation présente un graphique à barres indiquant le pourcentage de profils appartenant à chacun des états suivants : [!UICONTROL Réalisé], [!UICONTROL Existant] et [!UICONTROL Sortie].

![](../images/ui/overview/segment-browse-breakdown.png)

| État | Description |
| ------ | ----------- |
| Réalisé | Un nouveau profil dans le segment. |
| Existant | Profil existant qui est resté dans le segment. |
| Fermeture | Profil existant qui quitte le segment. |

L’événement représente le pourcentage de profils qui changent au sein d’une définition de segment par rapport à la dernière exécution de la tâche de segment, tandis que le nombre de profils représente le nombre total de profils admissibles pour le segment.

La méthode d’évaluation peut être soit par flux, soit par lot. Les segments par flux sont constamment évalués au fur et à mesure que les données entrent dans le système. Les segments par lot sont évalués selon un planning établi.

![](../images/ui/overview/segment-browse-segments.png)

En haut de la page se trouvent les options permettant d’ajouter tous les segments à un calendrier et de créer un segment.

Si vous basculez **[!UICONTROL Ajoutez tous les segments à planifier]**, la segmentation planifiée sera activée. Vous trouverez plus d&#39;informations sur la segmentation planifiée dans la section [segmentation planifiée de ce guide d&#39;utilisateur](#scheduled-segmentation).

Si vous sélectionnez **[!UICONTROL Créer un segment]**, vous accédez au Créateur de segments. Pour en savoir plus sur la création de segments, consultez la section [Création d’un segment dans le guide d’utilisateur](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

La barre latérale droite contient des informations sur tous les segments au sein de l&#39;organisation du SGI, en indiquant le nombre total de segments, la date de la dernière évaluation, la date de la prochaine évaluation, ainsi qu&#39;une ventilation des segments par méthode d&#39;évaluation.

![](../images/ui/overview/segment-browse-segment-info.png)

La sélection de la ligne de la définition de segment fournit un résumé de la définition de segment, y compris des options permettant de modifier ou de supprimer le segment, l&#39;audience qualifiée du segment, la taille totale de l&#39;audience, en plus du nom du segment, de la description, de la méthode d&#39;évaluation, de la date de création et de la date de dernière modification.

![](../images/ui/overview/segment-browse-details.png)

## Détails de la définition de segment {#segment-details}

Pour en savoir plus sur une définition de segment spécifique, sélectionnez le nom d’un segment dans l’onglet **[!UICONTROL Parcourir]**.

La page Détails du segment s’affiche. En haut, vous trouverez un résumé de la définition de segment, des informations sur la taille d’audience qualifiée, ainsi que les destinations pour lesquelles le segment est activé.

![](../images/ui/overview/segment-details-summary.png)

### Résumé de segment

La section **[!UICONTROL Résumé de segment]** fournit des informations telles que l&#39;ID, le nom, la description et les détails des attributs.

De plus, vous disposez de l’option permettant de modifier le segment. Si vous sélectionnez **[!UICONTROL Modifier le segment]**, vous accédez au [!DNL Segment Builder]. Pour plus d&#39;informations sur l&#39;utilisation de l&#39;espace de travail [!DNL Segment Builder], consultez le [[!DNL Segment Builder] guide d&#39;utilisateur](./segment-builder.md).

### Audience totale dans le segment

La section **[!UICONTROL audience totale dans le segment]** indique le nombre total de profils admissibles pour le segment.

Les estimations sont générées en utilisant la taille d’échantillon des données d’échantillon de cette journée. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

### Destinations activées

La section **[!UICONTROL Destinations activées]** affiche les destinations pour lesquelles ce segment est activé.

>[!NOTE]
>
> Les destinations sont une fonctionnalité disponible avec [!DNL Real-time Customer Data Platform] et vous permettent d’exporter des données vers des plateformes externes. Pour plus d&#39;informations sur les destinations, veuillez lire le [aperçu des destinations](../../destinations/home.md). Pour savoir comment activer un segment vers une destination, consultez le [guide sur l&#39;activation des segments vers une destination](../../destinations/ui/activate-destinations.md).

### Échantillons de profil

Vous trouverez ci-dessous un échantillon des profils qui remplissent les conditions requises pour le segment, en détaillant des informations, notamment l&#39;ID [!DNL Profile], le prénom, le nom et l&#39;adresse électronique personnelle.

La façon dont l’échantillonnage des données est déclenché dépend de la méthode d’assimilation.

Pour l’assimilation par lot, le magasin de profils est automatiquement analysé toutes les quinze minutes afin de déterminer si un nouveau lot a été correctement assimilé depuis l’exécution de la dernière tâche d’échantillonnage. Si tel est le cas, le magasin de profils est ensuite analysé pour voir s&#39;il y a eu au moins 5 % de changement dans le nombre d&#39;enregistrements. Si ces conditions sont remplies, une nouvelle tâche d’échantillonnage est déclenchée.

Pour l’assimilation en flux continu, le magasin de profils est automatiquement analysé toutes les heures afin de déterminer s’il y a eu au moins 5 % de changement dans le nombre d’enregistrements. Si cette condition est remplie, une nouvelle tâche d’échantillonnage est déclenchée.

La taille d’échantillon de l’analyse dépend du nombre total d’entités présentes dans votre magasin de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Pour obtenir des informations plus détaillées sur chaque [!DNL Profile], sélectionnez l&#39;ID [!DNL Profile]. Pour en savoir plus sur les détails d&#39;un profil, consultez le [[!DNL Real-time Customer Profile] guide d&#39;utilisation](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Création d’un segment {#create-segment}

La sélection de **[!UICONTROL Créer un segment]** dans le coin supérieur droit ouvre l&#39;espace de travail [!DNL Segment Builder], où vous pouvez commencer à créer une définition de segment.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] espace de travail

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec des éléments de  [!DNL Profile] données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

Pour plus d&#39;informations sur l&#39;utilisation de l&#39;espace de travail [!DNL Segment Builder], consultez le [[!DNL Segment Builder] guide d&#39;utilisateur](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Segmentation planifiée {#scheduled-segmentation}

Une fois les définitions de segment créées, vous pouvez les évaluer par le biais d’une évaluation sur demande ou planifiée (continue). L&#39;évaluation signifie le déplacement de [!DNL Real-time Customer Profile] données au moyen de définitions de segment afin de produire des audiences correspondantes. Une fois créées, les audiences sont enregistrées et stockées afin de pouvoir être exportées à l’aide des API [!DNL Experience Platform].

L’évaluation sur demande nécessite l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, alors que l’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour évaluer les définitions de segment à un moment précis (au maximum, une fois par jour).

### Activation de la segmentation planifiée {#enable-scheduled-segmentation}

Vous pouvez activer les définitions de segment pour une évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. Dans l’interface utilisateur, revenez à l’onglet **[!UICONTROL Parcourir]** dans **[!UICONTROL Segments]** et cochez **[!UICONTROL Ajouter tous les segments à planifier]**. Tous les segments seront alors évalués en fonction du planning défini par votre organisation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. Si votre entreprise dispose de plus de cinq stratégies de fusion pour [!DNL XDM Individual Profile] dans un seul environnement de sandbox, vous ne pourrez pas utiliser l’évaluation planifiée.

Actuellement, les plannings ne peuvent être créés qu’à l’aide de l’API. Pour obtenir des instructions détaillées sur la création, la modification et l’utilisation des plannings à l’aide de l’API, suivez le tutoriel relatif à l’évaluation et à l’accès aux résultats de segmentation, en particulier la section sur [l’évaluation planifiée à l’aide de l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentation par flux {#streaming-segmentation}

La segmentation en flux continu permet d’effectuer une segmentation sur [!DNL Platform] en temps quasi réel, tout en mettant l’accent sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit maintenant lorsque les données atteignent [!DNL Platform], ce qui évite de planifier et d’exécuter des tâches de segmentation.

Pour plus d’informations sur la segmentation en flux continu, consultez le [guide de l’utilisateur de la segmentation en flux continu](./streaming-segmentation.md).

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’entreprise. Pour plus d’informations sur l’activation de la segmentation planifiée, consultez la section [de la segmentation en flux continu dans ce guide d’utilisateur](#scheduled-segmentation).

## Segmentation Edge {#edge-segmentation}

La segmentation Edge permet d’évaluer instantanément les segments dans la plate-forme, ce qui permet d’utiliser des cas de personnalisation de la même page et de la page suivante.

Pour plus d&#39;informations sur la segmentation des arêtes, consultez le [guide de l&#39;interface utilisateur de segmentation des arêtes](./edge-segmentation.md).

## Violations de stratégie

>[!NOTE]
>
>Les violations de stratégie ne s’appliquent que si vous créez un segment qui a été affecté à une destination.

Une fois que vous avez créé votre segment, celui-ci est analysé par la gouvernance des données Adobe Experience Platform afin de s’assurer qu’il n’y a aucune violation de stratégie dans le segment. Pour plus d’informations, consultez [[!DNL Data Governance] aperçu des ](../../data-governance/home.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Étapes suivantes et ressources supplémentaires {#next-steps}

L&#39;interface utilisateur [!DNL Segmentation Service] fournit un flux de travail riche qui vous permet d&#39;isoler les audiences commercialisables des données [!DNL Real-time Customer Profile].

Pour en savoir plus sur [!DNL Segmentation Service], veuillez continuer à lire la documentation. Pour savoir comment utiliser l&#39;API [!DNL Segmentation Service], consultez le [[!DNL Segmentation Service] guide du développeur](../api/overview.md).
