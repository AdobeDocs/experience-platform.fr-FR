---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
solution: Adobe Experience Platform
title: Guide d’utilisation de Real-time Customer Profile
topic: guide
description: Real-time Customer Profile offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Ce document sert de guide pour interagir avec Real-time Customer Profile dans l’interface utilisateur d’Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 19%

---


# [!DNL Real-time Customer Profile] guide de l&#39;utilisateur

[!DNL Real-time Customer Profile] offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces.

This document serves as a guide for interacting with [!DNL Real-time Customer Profile] in the Adobe Experience Platform user interface.

## Prise en main

This user guide requires an understanding of the various [!DNL Experience Platform] services involved with managing [!DNL Real-time Customer Profiles]. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

* [!DNL Real-time Customer Profile](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [!DNL Identity Service](../../identity-service/home.md): Permet [!DNL Real-time Customer Profile] de relier les identités à partir de sources de données disparates au fur et à mesure de leur assimilation [!DNL Platform].
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

## Présentation

Dans le [!DNL Experience Platform UI](http://platform.adobe.com), cliquez sur **[!UICONTROL Profils]** dans le volet de navigation de gauche pour ouvrir l’onglet _[!UICONTROL Aperçu]_. Cet onglet contient des liens vers la documentation et des vidéos pour vous aider à comprendre et à commencer à travailler avec des profils.

![](../images/user-guide/profiles-overview.png)

## Parcourir

Sélectionnez l’onglet *[!UICONTROL Parcourir]* pour parcourir les profils par identité.

![](../images/user-guide/profiles-browse.png)

### Mesures de profil {#profile-metrics}

Sur le côté droit de l&#39;onglet *[!UICONTROL Parcourir]* se trouvent plusieurs mesures importantes liées à vos données de profil, dont le nombre [total de](#profile-count) profils ainsi qu&#39;une liste des [profils par espace de nommage](#profiles-by-namespace).

Ces mesures de profil sont évaluées à l’aide de la stratégie de fusion par défaut de votre organisation. Pour plus d’informations sur l’utilisation des stratégies de fusion, y compris sur la manière de définir une stratégie de fusion par défaut, voir le guide [d’utilisation](merge-policies.md)Fusionner les stratégies.

Outre ces mesures, la section Mesures de profil fournit également une date et une heure de *dernière mise à jour* , indiquant le moment où les mesures ont été évaluées pour la dernière fois.

![](../images/user-guide/profiles-profile-metrics.png)

### Nombre de profils {#profile-count}

The profile count displays the total number of profiles your organization has within [!DNL Experience Platform], after your organization&#39;s default merge policy has merged together profile fragments to form a single profile for each individual customer. En d’autres termes, votre organisation peut disposer de plusieurs fragments de profil liés à un seul client qui interagit avec votre marque sur différents canaux, mais ces fragments sont fusionnés (selon la stratégie de fusion par défaut) et renvoient le nombre de profils « 1 », car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils avec des attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de séries chronologiques (événement), telles que les profils de Adobe Analytics. Le nombre de profils est régulièrement actualisé afin de fournir un nombre total de profils actualisé au sein de la Plateforme.

Lorsque l&#39;assimilation d&#39;enregistrements dans la [!DNL Profile Store] table augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour le nombre. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l&#39;assimilation par lot, dans les 15 minutes suivant l&#39;assimilation réussie d&#39;un lot dans le magasin de Profils, si le seuil de 5 % d&#39;augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre de profils.

### Profils par espace de nommage {#profiles-by-namespace}

La mesure *[!UICONTROL Profils par espace de nommage]* affiche le nombre total et la ventilation des espaces de nommage sur l’ensemble des profils fusionnés dans votre Profil Store. Le nombre total de profils par espace de nommage (en d’autres termes, l’ajout des valeurs affichées pour chaque espace de nommage) sera toujours supérieur à la mesure Nombre de profils, car un profil peut être associé à plusieurs espaces de nommage. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage sont associés à ce client individuel.

Tout comme la mesure du nombre [de](#profile-count) profils, lorsque l’assimilation d’enregistrements dans le [!DNL Profile Store] augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour les mesures d’espace de nommage. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l’assimilation par lot, dans les 15 minutes qui suivent l’assimilation réussie d’un lot dans le [!DNL Profile Store], si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour les mesures.

### Fusionner la stratégie

Le sélecteur de stratégies **[!UICONTROL de]** fusion sélectionne automatiquement la stratégie de fusion par défaut pour votre organisation. Si vous ne souhaitez pas utiliser cette stratégie de fusion, vous pouvez sélectionner la stratégie de fusion `X` en regard de la stratégie de fusion par défaut pour ouvrir une boîte de dialogue *[!UICONTROL Sélectionner la stratégie]* de fusion dans laquelle vous pouvez choisir une autre stratégie de fusion. Pour en savoir plus sur les stratégies de fusion, consultez le guide [de l’utilisateur](merge-policies.md)Fusionner les stratégies.

![](../images/user-guide/profiles-search-merge-policy.png)

### Espace de nommage d&#39;identité

Le sélecteur d&#39;espace de nommage **** d&#39;identité ouvre une boîte de dialogue dans laquelle vous pouvez choisir l&#39;espace de nommage d&#39;identité à rechercher et personnaliser les attributs affichés à partir de votre recherche en sélectionnant l&#39;icône de filtre et en choisissant les attributs à ajouter ou à supprimer.

![](../images/user-guide/profiles-search-filter.png)

Dans la boîte de dialogue *[!UICONTROL Sélectionner un espace de nommage]* d&#39;identité, choisissez l&#39;espace de nommage de recherche ou utilisez la barre de **[!UICONTROL recherche]** de la boîte de dialogue pour commencer à saisir le nom d&#39;un espace de nommage. Vous pouvez sélectionner un espace de nommage pour vue d&#39;autres détails, et une fois que vous avez trouvé l&#39;espace de nommage, vous pouvez sélectionner le bouton radio et appuyer sur **[!UICONTROL Sélectionner]** pour continuer.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valeur d’identité

Après avoir sélectionné un espace de nommage **[!UICONTROL d&#39;]** identité, vous revenez à l&#39;onglet *[!UICONTROL Parcourir]* où vous pouvez saisir une valeur **[!UICONTROL d&#39;]** identité. Cette valeur est spécifique à un profil client individuel et doit être une entrée valide pour l’espace de nommage fourni. Par exemple, la sélection de l’espace de nommage **[!UICONTROL d’]** identité &quot;courriel&quot; exigerait une valeur **[!UICONTROL d’]** identité sous la forme d’une adresse électronique valide.

![](../images/user-guide/profiles-show-profile.png)

Une fois qu’une valeur a été saisie, sélectionnez **[!UICONTROL Afficher le profil]** et un seul profil correspondant à la valeur est renvoyé. Sélectionnez l’ID **[!UICONTROL de]** Profilpour vue les détails du profil.

![](../images/user-guide/profiles-display-profile.png)

### Détails du profil {#profile-detail}

Lorsque vous sélectionnez l’ID **[!UICONTROL de]** Profil, l’onglet _[!UICONTROL Détails]_s’ouvre. Cette page affiche des informations sur le profil sélectionné, y compris les attributs de base, les identités liées et les canaux de contact disponibles. Les informations de profil affichées ont été fusionnées à partir de plusieurs fragments de profil afin de former une vue unique du client individuel.

![](../images/user-guide/profiles-profile-detail.png)

Vous pouvez vue d’autres informations relatives au profil, y compris *[!UICONTROL les attributs]*, les *[!UICONTROL Événements]* et les *[!UICONTROL segments]* auxquels le profil est membre.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Stratégies de fusion

Select the *[!UICONTROL Merge Policies]* tab to view a list of merge policies belonging to your organization. Chaque stratégie répertoriée affiche son nom, indique s’il s’agit ou non de la stratégie de fusion par défaut, et précise le schéma auquel elle s’applique.

For more information on merge policies, see the [Merge Policies user guide](merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## Schéma d’union

Sélectionnez l&#39;onglet Schéma ** d&#39;Union [!DNL Profile Store]pour vue des schémas d&#39;union de votresite. A union schema is an amalgamation of all [!DNL Experience Data Model] (XDM) fields under the same class, whose schemas have been enabled for use in [!DNL Real-time Customer Profile]. Sélectionnez une classe dans la liste de gauche pour vue de la structure de son schéma d&#39;union dans la trame.

Par exemple, la sélection de &quot;[!DNL XDM Profile]&quot; affiche le schéma d’union de la [!DNL XDM Individual Profile] classe.

Consultez la section sur les schémas d’union dans le [guide de composition de schémas](../../xdm/schema/composition.md) pour en savoir plus sur les schémas d’union et leur rôle dans [!DNL Real-time Customer Profile].

![](../images/user-guide/profiles-union-schema.png)

## Étapes suivantes

By reading this guide, you now know how to view and manage your [!DNL Profile] data using the [!DNL Experience Platform] UI. For information on how to leverage [!DNL Real-time Customer Profile] data to generate audience segments, see the [Segmentation documentation](../../segmentation/home.md).