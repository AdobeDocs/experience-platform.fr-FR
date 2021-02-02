---
keywords: Experience Platform ; profil ; profil client en temps réel ; interface utilisateur ; interface utilisateur ; personnalisation ; tableau de bord profil ; tableau de bord
title: Guide de l'interface utilisateur du Tableau de bord profil
description: 'Ce guide décrit le tableau de bord de données du Profil client en temps réel disponible dans l’interface utilisateur de Adobe Experience Platform. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---


# (Alpha) [!DNL Real-time Customer Profile] tableau de bord {#profile-dashboard}

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord décrite dans ce document est actuellement en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord par lequel vous pouvez vue des informations importantes sur vos données [!DNL Real-time Customer Profile], telles qu’elles sont capturées au cours d’un instantané quotidien. Ce guide décrit comment accéder au tableau de bord [!DNL Profile] dans l’interface utilisateur et l’utiliser. Il fournit également des informations supplémentaires sur les mesures affichées dans le tableau de bord.

Pour un aperçu de toutes les fonctionnalités de Profil de l’interface utilisateur de l’Experience Platform, consultez le [Guide de l’interface utilisateur du Profil client en temps réel](user-guide.md).

## Données du tableau de bord profil

Le tableau de bord de Profil affiche un instantané des données d’attribut (enregistrement) que votre organisation possède dans le magasin de Profils de l’Experience Platform. L&#39;instantané n&#39;inclut aucune donnée de événement (série chronologique).

Les données d&#39;attribut de l&#39;instantané affichent les données exactement telles qu&#39;elles apparaissent au moment précis où l&#39;instantané a été pris. En d&#39;autres termes, l&#39;instantané n&#39;est pas une approximation ou un échantillon des données et le tableau de bord de Profil n&#39;est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis l&#39;instantané ne seront pas répercutées dans le tableau de bord tant que l&#39;instantané suivant n&#39;aura pas été pris.

Les mesures affichées dans le tableau de bord de Profil sont basées sur la stratégie de fusion par défaut de votre organisation. Pour plus d&#39;informations sur les stratégies de fusion et sur la manière de sélectionner ou de modifier votre stratégie de fusion par défaut, consultez le [guide d&#39;interface utilisateur des stratégies de fusion](merge-policies.md).

## Exploration du tableau de bord de Profil

Pour accéder au tableau de bord de Profil dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Profils]** dans le rail de gauche, puis sélectionnez l’onglet **[!UICONTROL Aperçu]** pour afficher le tableau de bord.

![](../images/profile-dashboard/dashboard-overview.png)

### Widgets et mesures

Le tableau de bord est composé de widgets, qui sont des mesures en lecture seule fournissant des informations importantes sur vos données de Profil. La date et l’heure de la &quot;dernière mise à jour&quot; du widget indiquent le moment où le dernier instantané des données a été effectué.

![](../images/profile-dashboard/dashboard-timestamp.png)

## Widgets disponibles

Experience Platform fournit plusieurs widgets que vous pouvez utiliser pour visualiser différentes mesures liées à vos données de Profil. Sélectionnez le nom d’un widget ci-dessous pour en savoir plus :

* [[!UICONTROL Taille de l&#39;Audience]](#audience-size)
* [[!UICONTROL Profils par espace de nommage]](#profiles-by-namespace)

### [!UICONTROL Taille de l&#39;Audience] {#audience-size}

Le widget **[!UICONTROL Taille d&#39;Audience]** affiche le nombre total de profils fusionnés dans le magasin de données du Profil au moment où l&#39;instantané a été pris. Ce nombre est le résultat de l’application de la stratégie de fusion par défaut de votre organisation à vos données de Profil afin de fusionner des fragments de profil pour former un seul profil pour chaque individu.

Pour plus d&#39;informations sur les fragments et les profils fusionnés, veuillez commencer par lire la section *fragments de Profil par rapport aux profils fusionnés* de la [vue d&#39;ensemble du Profil](../home.md).

>[!NOTE]
>
>La stratégie de fusion utilisée pour calculer cette mesure n&#39;est pas identique à la stratégie de fusion générée par le système utilisée pour calculer [!UICONTROL audiences adressables] dans le tableau de bord [!UICONTROL Utilisation de la licence]. Par conséquent, le nombre d&#39;audiences dans les tableaux de bord [!DNL Profile] et [!UICONTROL Utilisation de la licence] ne sera probablement pas exactement le même.

![](../images/profile-dashboard/audience-size.png)

### [!UICONTROL Profils par espace de nommage] {#profiles-by-namespace}

Le widget **[!UICONTROL Profils par espace de nommage]** affiche la ventilation des espaces de nommage sur tous les profils fusionnés de votre magasin de Profils. Le nombre total de profils par [!UICONTROL espace de nommage d&#39;ID] (en d&#39;autres termes, l&#39;ajout des valeurs affichées pour chaque espace de nommage) sera toujours supérieur au nombre total de profils de fusion, car un profil peut être associé à plusieurs espaces de nommage. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage sont associés à ce client individuel.

Pour en savoir plus sur les espaces de nommage d&#39;identité, consultez la [documentation du service d&#39;identité Adobe Experience Platform](../../identity-service/home.md).

![](../images/profile-dashboard/profiles-by-namespace.png)

## Tableaux de bord supplémentaires

L’interface utilisateur de la plate-forme fournit des tableaux de bord supplémentaires pour l’affichage d’instantanés de vos données dans l’Experience Platform. Ces tableaux de bord incluent la segmentation et l’utilisation des licences. Pour plus d’informations sur ces tableaux de bord supplémentaires, sélectionnez l’un des liens suivants :

* [Tableau de bord de segment](../../segmentation/ui/segment-dashboard.md)
* [Tableau de bord d&#39;utilisation de la licence](../../landing/license-usage-dashboard.md)

## Étapes suivantes

En suivant ce document, vous devez maintenant pouvoir localiser le tableau de bord de Profil et comprendre les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l&#39;utilisation des données [!DNL Profile] dans l&#39;interface utilisateur Experience Platform, consultez le [[!DNL Profile] guide de l&#39;interface utilisateur](user-guide.md).