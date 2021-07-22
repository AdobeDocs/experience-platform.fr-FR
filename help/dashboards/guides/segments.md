---
keywords: Experience Platform;profil;segment;segments;segmentation;interface utilisateur;interface utilisateur;personnalisation;tableau de bord des segments;tableau de bord
title: Tableau de bord Segments
description: 'Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les segments que votre entreprise a créés. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 41ef7a6e6d3b0ee9afe762b19c8c286ceb361dbb
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 6%

---

# Tableau de bord Segments {#segment-dashboard}

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos segments, telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder au tableau de bord des segments et l’utiliser dans l’interface utilisateur. Il fournit également des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour un aperçu de toutes les fonctionnalités du service de segmentation Adobe Experience Platform dans l’interface utilisateur de Platform, consultez le [guide de l’interface utilisateur de Segmentation Service](../../segmentation/ui/overview.md).

## Données du tableau de bord de segment

Le tableau de bord des segments affiche un instantané des données d’attribut (enregistrement) dont votre organisation dispose dans la banque de profils en Experience Platform. L’instantané n’inclut aucune donnée d’événement (série temporelle).

Les données d’attribut de l’instantané affichent les données exactement telles qu’elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données et le tableau de bord du segment ne se met pas à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord des segments

Pour accéder au tableau de bord [!UICONTROL Segments] dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Segments]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Aperçu]** pour afficher le tableau de bord.

>[!NOTE]
>
>Si votre entreprise est une nouvelle entreprise de Platform et qu’elle ne dispose pas encore de jeux de données de profil principaux ni de stratégies de fusion créés, le tableau de bord [!UICONTROL Segments] n’est pas visible. L’onglet [!UICONTROL Aperçu] contient des liens et de la documentation pour vous aider à commencer la segmentation.

![](../images/segments/dashboard-overview.png)

### Modification du tableau de bord [!UICONTROL Segments]

Vous pouvez modifier l’aspect du tableau de bord [!UICONTROL Segments] en sélectionnant **[!UICONTROL Modifier le tableau de bord]**. Cela vous permet de déplacer, d’ajouter et de supprimer des widgets du tableau de bord, ainsi que d’accéder à la **[!UICONTROL bibliothèque de widgets]** pour explorer les widgets disponibles et créer des widgets personnalisés pour votre organisation.

Pour en savoir plus, reportez-vous à la documentation [Modification des tableaux de bord](../customize/modify.md) et [présentation de la bibliothèque de widgets](../customize/widget-library.md) .

## Sélection d’un segment

Le tableau de bord sélectionne automatiquement un segment à afficher. Vous pouvez toutefois le modifier à l’aide du menu déroulant ou du sélecteur de segments.

Pour choisir un autre segment, sélectionnez la liste déroulante en regard du nom du segment ou utilisez le sélecteur de segments pour ouvrir la boîte de dialogue de sélection de segment.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets et mesures

Le tableau de bord des segments est constitué de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur le segment sélectionné.

La date et l’heure de la &quot;dernière mise à jour&quot; d’un widget indique le moment où le dernier instantané des données a été pris. La date et l’heure de l’instantané sont indiquées en UTC ; il ne se trouve pas dans le fuseau horaire de l’utilisateur individuel ou de l’organisation IMS.

![](../images/segments/widget-timestamp.png)

## Widgets standard

Adobe fournit plusieurs widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos segments. Vous pouvez également créer des widgets personnalisés à partager avec votre organisation à l’aide de la [!UICONTROL bibliothèque de widgets]. Pour en savoir plus sur la création de widgets personnalisés, commencez par lire la [présentation de la bibliothèque de widgets](../customize/widget-library.md).

Pour en savoir plus sur chacun des widgets standard disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [[!UICONTROL Taille de l’audience]](#audience-size)
* [[!UICONTROL Tendance de la taille de l’audience]](#audience-size-trend)
* [[!UICONTROL Superposition des identités]](#identity-overlap)
* [[!UICONTROL Profils par identité]](#profiles-by-identity)

### [!UICONTROL Taille de l’audience] {#audience-size}

Le widget **[!UICONTROL Taille de l’audience]** affiche le nombre total de profils fusionnés dans le segment sélectionné au moment de l’instantané. Ce nombre est le résultat de l’application de la stratégie de fusion de segments à vos données de profil afin de fusionner les fragments de profil pour former un seul profil pour chaque individu du segment.

Pour plus d’informations sur les fragments et les profils fusionnés, commencez par lire la [présentation de Real-time Customer Profile](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Tendance de la taille de l’audience] {#audience-size-trend}

Le widget **[!UICONTROL Tendance de la taille de l’audience]** fournit des informations concernant le nombre total de profils dans le segment, tel qu’il a été capturé pendant l’instantané quotidien, pendant les 30 derniers jours, 90 ou 12 mois. Ce widget affiche la manière dont la taille du segment a pu varier au fil du temps, à mesure que les nouveaux profils remplissent les critères ou quittent le segment.

Pour en savoir plus sur l’évaluation des segments et sur la façon dont les profils sont qualifiés et sortent des segments, consultez la [documentation du service de segmentation](../../segmentation/home.md).

![](../images/segments/audience-size-trend.png)

### [!UICONTROL Superposition des identités] {#identity-overlap}

Le widget **[!UICONTROL chevauchement des identités]** affiche un diagramme de Venn, ou un diagramme de définition, qui montre le chevauchement des profils de votre segment contenant plusieurs identités.

Après avoir utilisé les menus déroulants du widget pour sélectionner les identités à comparer, les cercles s’affichent avec la taille relative de chaque identité, le nombre de profils contenant les deux espaces de noms étant représenté par la taille du chevauchement entre les cercles.

Si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités seront associées à ce client individuel. Par conséquent, il est probable que votre organisation dispose de plusieurs profils contenant des fragments provenant de plusieurs identités.

Pour en savoir plus sur les identités, consultez la [documentation du service Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profils par identité] {#profiles-by-identity}

Le widget **[!UICONTROL Profils par identité]** affiche la ventilation des identités entre tous les profils fusionnés de votre segment sélectionné. Le nombre total de profils par identité peut être supérieur au nombre total de profils dans le segment, car plusieurs identités peuvent y être associées pour un profil. En d’autres termes, le fait de cumuler les valeurs affichées pour chaque identité peut être supérieur à la taille totale de l’audience dans le segment, car si un client interagit avec votre marque sur plusieurs canaux, plusieurs identités peuvent être associées à ce client individuel.

Pour en savoir plus sur les identités, consultez la [documentation du service Adobe Experience Platform Identity](../../identity-service/home.md).

![](../images/segments/profiles-by-identity.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir localiser le tableau de bord des segments et sélectionner un segment à afficher. Vous devez également comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des segments dans l’interface utilisateur de l’Experience Platform, consultez le [guide de l’interface utilisateur de Segmentation Service](../../segmentation/ui/overview.md).
