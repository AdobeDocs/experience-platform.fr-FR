---
keywords: Experience Platform ; profil ; segment ; segments ; segmentation ; interface utilisateur ; interface utilisateur ; personnalisation ; tableau de bord de segment ; tableau de bord
title: Tableau de bord de segments
description: 'Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez vue des informations importantes sur les segments créés par votre entreprise. '
topic-legacy: guide
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---

# (Bêta) tableau de bord de segments {#segment-dashboard}

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord décrite dans ce document est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez vue des informations importantes sur vos segments, telles qu’elles sont capturées au cours d’un instantané quotidien. Ce guide décrit comment accéder aux segments et les utiliser dans le tableau de bord d’interface utilisateur et fournit plus d’informations sur les visualisations affichées dans le tableau de bord.

Pour un aperçu de toutes les fonctionnalités du service de segmentation Adobe Experience Platform dans l’interface utilisateur de la plate-forme, consultez le [Guide de l’interface utilisateur du service de segmentation](../../segmentation/ui/overview.md).

## Données du tableau de bord de segments

Le tableau de bord de segments affiche un instantané des données d’attribut (enregistrement) que votre organisation possède dans le magasin de Profils de l’Experience Platform. L&#39;instantané n&#39;inclut aucune donnée de événement (série chronologique).

Les données d&#39;attribut de l&#39;instantané affichent les données exactement telles qu&#39;elles apparaissent au moment précis où l&#39;instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données et le tableau de bord de segments n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis l&#39;instantané ne seront pas répercutées dans le tableau de bord tant que l&#39;instantané suivant n&#39;aura pas été pris.

## Exploration du tableau de bord de segments

Pour accéder au tableau de bord de segments dans l’interface utilisateur de la plateforme, sélectionnez **[!UICONTROL Segments]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Aperçu]** pour afficher le tableau de bord.

![](../images/segments/dashboard-overview.png)

### Sélectionner un segment

Le tableau de bord sélectionne automatiquement un segment à afficher, mais vous pouvez modifier le segment affiché à l’aide du menu déroulant. Pour choisir un autre segment, sélectionnez la liste déroulante en regard du nom du segment, puis sélectionnez le segment à vue.

>[!NOTE]
>
>Le menu déroulant affiche tous les segments créés jusqu’à présent par votre organisation. Cela signifie peut-être que vous devrez faire défiler la page pour vue de la liste complète des segments disponibles.

![](../images/segments/change-segment.png)

### Widgets et mesures

Le tableau de bord de segments est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur le segment sélectionné. La date et l’heure de la &quot;dernière mise à jour&quot; du widget indiquent le moment où le dernier instantané des données a été effectué.

![](../images/segments/widget-timestamp.png)

## Widgets disponibles

Experience Platform fournit plusieurs widgets que vous pouvez utiliser pour visualiser différentes mesures liées à votre segment. Sélectionnez le nom d’un widget ci-dessous pour en savoir plus :

* [[!UICONTROL Taille du segment]](#segment-size)
* [[!UICONTROL Profils ajoutés au fil du temps]](#profiles-added-over-time)
* [[!UICONTROL Profils par espace de nommage]](#profiles-by-namespace)

### [!UICONTROL Taille du segment] {#segment-size}

Le widget **[!UICONTROL Taille du segment]** affiche le nombre total de profils fusionnés dans le segment sélectionné au moment où l&#39;instantané a été pris. Ce nombre est le résultat de l’application de la stratégie de fusion de segments à vos données de Profil afin de fusionner des fragments de profil pour former un seul profil pour chaque individu du segment.

Pour plus d’informations sur les fragments et les profils fusionnés, veuillez commencer par lire la [Présentation du Profil client en temps réel](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Profils ajoutés au fil du temps] {#profiles-added-over-time}

Le widget **[!UICONTROL Profils ajoutés au fil du temps]** fournit des informations sur le nombre total de profils du segment capturés au cours de l&#39;instantané quotidien, au cours des 30 derniers jours. Ce widget montre comment la taille du segment a pu varier sur une période de 30 jours, à mesure que de nouveaux profils sont inclus ou sortent du segment.

Pour en savoir plus sur l’évaluation des segments et sur la façon dont les profils sont qualifiés et quittent les segments, consultez la [documentation du service de segmentation](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profils par espace de nommage] {#profiles-by-namespace}

Le widget **[!UICONTROL Profils par espace de nommage]** affiche la ventilation des espaces de nommage sur tous les profils fusionnés du segment sélectionné. Le nombre total de profils par espace de nommage d’identité ([!UICONTROL espace de nommage d’ID] dans le widget) peut être supérieur au nombre total de profils dans le segment, car un profil peut être associé à plusieurs espaces de nommage. En d’autres termes, l’ajout des valeurs affichées pour chaque espace de nommage peut être supérieur au total des profils du segment, car si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage peuvent être associés à ce client.

Pour en savoir plus sur les espaces de nommage d&#39;identité, consultez la [documentation du service d&#39;identité Adobe Experience Platform](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Étapes suivantes

En suivant ce document, vous devez maintenant pouvoir localiser le tableau de bord de segments et sélectionner un segment à vue. Vous devez également comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des segments dans l’interface utilisateur de l’Experience Platform, consultez le [Guide de l’interface utilisateur du service de segmentation](../../segmentation/ui/overview.md).
