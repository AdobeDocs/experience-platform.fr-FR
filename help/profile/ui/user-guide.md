---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile;Union schema;UNION PROFILE;union profile
title: Guide de l’interface utilisateur du Profil client en temps réel
topic: guide
description: Real-time Customer Profile offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Ce document sert de guide pour interagir avec Real-time Customer Profile dans l’interface utilisateur d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 14%

---


# [!DNL Real-time Customer Profile] Guide de l’interface

[!DNL Real-time Customer Profile] offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. This document serves as a guide for interacting with [!DNL Real-time Customer Profile] data in the Adobe Experience Platform user interface (UI).

## Prise en main

This UI guide requires an understanding of the various [!DNL Experience Platform] services involved with managing [!DNL Real-time Customer Profiles]. Avant de lire ce guide ou de travailler dans l’interface utilisateur, consultez la documentation relative aux services suivants :

* [[!DNL Real-time Customer Profile]](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Identity Service]](../../identity-service/home.md): Permet [!DNL Real-time Customer Profile] de relier les identités à partir de sources de données disparates au fur et à mesure de leur assimilation [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

## Présentation

Dans l’ [[!DNL Experience Platform] interface utilisateur](http://platform.adobe.com), sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche pour ouvrir l’onglet **[!UICONTROL Aperçu]** . Cet onglet contient des liens vers la documentation et des vidéos pour vous aider à comprendre et à commencer à travailler avec des profils.

![](../images/user-guide/profiles-overview.png)

## Parcourir

Sélectionnez l’onglet **[!UICONTROL Parcourir]** pour parcourir les profils par identité.

![](../images/user-guide/profiles-browse.png)

### Mesures de profil {#profile-metrics}

Sur le côté droit de l&#39;onglet **[!UICONTROL Parcourir]** se trouvent plusieurs mesures importantes liées à vos données de profil, dont le nombre [total de](#profile-count) profils ainsi qu&#39;une liste des [profils par espace de nommage](#profiles-by-namespace).

Ces mesures de profil sont évaluées à l’aide de la stratégie de fusion par défaut de votre organisation. Pour plus d’informations sur l’utilisation des stratégies de fusion, y compris sur la manière de définir une stratégie de fusion par défaut, voir le guide [d’utilisation](merge-policies.md)Fusionner les stratégies.

Outre ces mesures, la section Mesures de profil fournit également une date et une heure de dernière mise à jour, indiquant le moment où les mesures ont été évaluées pour la dernière fois.

![](../images/user-guide/profiles-profile-metrics.png)

### Nombre de profils {#profile-count}

The profile count displays the total number of profiles your organization has within [!DNL Experience Platform], after your organization&#39;s default merge policy has merged together profile fragments to form a single profile for each individual customer. En d’autres termes, votre organisation peut disposer de plusieurs fragments de profil liés à un seul client qui interagit avec votre marque sur différents canaux, mais ces fragments sont fusionnés (selon la stratégie de fusion par défaut) et renvoient le nombre de profils « 1 », car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils avec des attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de séries chronologiques (événement), telles que les profils de Adobe Analytics. Le nombre de profils est régulièrement actualisé afin de fournir un nombre total de profils actualisé au sein de la Plateforme.

Lorsque l’assimilation d’enregistrements dans la [!DNL Profile] boutique augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour le nombre. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l&#39;assimilation par lot, dans les 15 minutes suivant l&#39;assimilation réussie d&#39;un lot dans le magasin de Profils, si le seuil de 5 % d&#39;augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre de profils.

### Profils par espace de nommage {#profiles-by-namespace}

La mesure **[!UICONTROL Profils par espace de nommage]** affiche le nombre total et la ventilation des espaces de nommage sur l’ensemble des profils fusionnés dans votre Profil Store. Le nombre total de profils par espace de nommage (en d’autres termes, l’ajout des valeurs affichées pour chaque espace de nommage) sera toujours supérieur à la mesure Nombre de profils, car un profil peut être associé à plusieurs espaces de nommage. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage sont associés à ce client individuel.

Tout comme la mesure du nombre [de](#profile-count) profils, lorsque l’assimilation d’enregistrements dans la [!DNL Profile] boutique augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour les mesures d’espace de nommage. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l’assimilation par lot, dans les 15 minutes qui suivent l’importation d’un lot dans la [!DNL Profile] boutique, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour les mesures.

### Fusionner la stratégie

Le sélecteur de stratégies **[!UICONTROL de]** fusion sélectionne automatiquement la stratégie de fusion par défaut pour votre organisation. Si vous ne souhaitez pas utiliser cette stratégie de fusion, vous pouvez sélectionner la stratégie de fusion `X` en regard de la stratégie de fusion par défaut pour ouvrir la boîte de dialogue **[!UICONTROL Sélectionner la stratégie]** de fusion, dans laquelle vous pouvez choisir une autre stratégie de fusion. Pour en savoir plus sur les stratégies de fusion et leur rôle dans Platform, consultez le guide [d’utilisation des stratégies de](merge-policies.md)fusion.

![](../images/user-guide/profiles-search-merge-policy.png)

### Espace de nommage d&#39;identité

Le sélecteur d&#39;espace de nommage **** d&#39;identité ouvre une boîte de dialogue dans laquelle vous pouvez choisir l&#39;espace de nommage d&#39;identité à rechercher et personnaliser les attributs affichés à partir de votre recherche en sélectionnant l&#39;icône de filtre et en choisissant les attributs à ajouter ou à supprimer.

![](../images/user-guide/profiles-search-filter.png)

Dans la boîte de dialogue **[!UICONTROL Sélectionner un espace de nommage]** d&#39;identité, choisissez l&#39;espace de nommage de recherche ou utilisez la barre de recherche de la boîte de dialogue pour commencer à saisir le nom d&#39;un espace de nommage. Vous pouvez sélectionner un espace de nommage pour vue des détails supplémentaires, et une fois que vous avez trouvé l&#39;espace de nommage que vous souhaitez utiliser, vous pouvez sélectionner le bouton radio et appuyer sur **[!UICONTROL Sélectionner]** pour continuer.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valeur d’identité

Après avoir sélectionné un espace de nommage d&#39;identité, vous revenez à l&#39;onglet **[!UICONTROL Parcourir]** où vous pouvez saisir une valeur **** d&#39;identité. Cette valeur est spécifique à un profil client individuel et doit être une entrée valide pour l’espace de nommage fourni. Par exemple, la sélection de l&#39;espace de nommage d&#39;identité &quot;Courriel&quot; exigerait une valeur d&#39;identité sous la forme d&#39;une adresse électronique valide.

![](../images/user-guide/profiles-show-profile.png)

Une fois qu’une valeur a été saisie, sélectionnez **[!UICONTROL Afficher le profil]** et un seul profil correspondant à la valeur est renvoyé. Sélectionnez l’ID **[!UICONTROL de]** Profilpour vue les détails du profil.

![](../images/user-guide/profiles-display-profile.png)

### Détails du profil {#profile-detail}

Lorsque vous sélectionnez l’ID **[!UICONTROL de]** Profil, l’onglet **[!UICONTROL Détails]** s’ouvre. The profile information displayed on the **[!UICONTROL Detail]** tab has been merged together from multiple profile fragments to form a single view of the individual customer. Cela inclut les détails du client tels que les attributs de base, les identités liées et les préférences de canal. Les champs par défaut affichés peuvent également être modifiés au niveau de l’organisation pour afficher les attributs de Profil préférés. Pour en savoir plus sur la personnalisation de ces champs, y compris des instructions détaillées pour l’ajout et la suppression d’attributs et le redimensionnement des panneaux de tableau de bord, consultez le guide [de personnalisation des détails du](profile-customization.md)profil.

![](../images/user-guide/profiles-profile-detail.png)

Vous pouvez vue des informations supplémentaires relatives à chaque profil en sélectionnant un autre onglet disponible. Ces onglets comprennent des attributs, des événements et des adhésions de segments, qui affichent les segments pour lesquels le profil est actuellement qualifié.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Stratégies de fusion

Dans le menu **[!UICONTROL Profils]** principal, sélectionnez l’onglet **[!UICONTROL Fusionner les stratégies]** pour vue d’une liste de stratégies de fusion appartenant à votre organisation. Chaque stratégie répertoriée affiche son nom, indique s’il s’agit ou non de la stratégie de fusion par défaut, et précise le schéma auquel elle s’applique.

For more information on merge policies, see the [merge policies UI guide](merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## Schéma d’union {#union-schema}

Dans le menu **[!UICONTROL Profils]** principal, sélectionnez l&#39;onglet Schéma **** d&#39;Union pour vue des schémas d&#39;union pour vos données assimilées. A union schema is an amalgamation of all [!DNL Experience Data Model] (XDM) fields under the same class, whose schemas have been enabled for use in [!DNL Real-time Customer Profile].

Pour plus d’informations sur les schémas d’union, consultez le guide [de l’interface utilisateur de schéma d’](union-schema.md)union.

![](../images/user-guide/profiles-union-schema.png)

## Étapes suivantes

By reading this guide, you now know how to view and manage your [!DNL Profile] data using the [!DNL Experience Platform] UI. Pour plus d’informations sur la façon d’utiliser les données de Profil à l’aide de l’API Profil client en temps réel, consultez le guide [du développeur de](../api/overview.md)Profils.