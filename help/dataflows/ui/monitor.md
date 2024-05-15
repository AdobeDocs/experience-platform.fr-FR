---
title: Présentation du tableau de bord de supervision
description: Découvrez comment utiliser le tableau de bord de surveillance dans l’interface utilisateur de Adobe Experience Platform
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: 710fa6930b27f95d34539a18881c0f9d23e1debd
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 4%

---

# Présentation du tableau de bord de supervision

Utilisez le tableau de bord de surveillance de l’interface utilisateur de Adobe Experience Platform pour afficher le parcours de vos données, de l’ingestion à l’activation. Le tableau de bord de surveillance vous permet d’effectuer les opérations suivantes :

* Surveillez le parcours de vos données à partir de sources, d’Identity Service, de Real-Time Customer Profile, d’audiences et enfin dans les destinations.
* Afficher différentes mesures et différents états en fonction de l’étape dans laquelle se trouvent vos données.
* Filtrez votre vue de surveillance des données par type de données.

Le tableau de bord de surveillance prend en charge l’affichage de plusieurs types de données différents :

* **Client et compte**: les données client font référence aux données utilisées dans [Real-time Customer Data Platform](../../rtcdp/home.md), tandis que les données du compte font référence à [données des profils de compte](../../rtcdp/accounts/account-profile-overview.md) accessible lors de l’abonnement à [Real-Time CDP, édition B2B](../../rtcdp/b2b-overview.md). Si votre licence Real-Time CDP n’inclut pas Real-Time CDP, Edition B2B, vous ne pouvez utiliser que le tableau de bord de surveillance pour surveiller les données client.
* **Prospect**: [Profils de prospects](../../profile/ui/prospect-profile.md) sont utilisés pour représenter des personnes qui n’ont pas encore interagi avec votre entreprise, mais auxquelles vous souhaitez tendre la main. Avec les profils de prospect, vous pouvez compléter vos profils client avec les attributs de partenaires tiers approuvés. Vous devez posséder une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate pour afficher le type de données du prospect.
* **Enrichissement du profil du compte**: les profils de compte vous permettent d’unifier les informations de compte de plusieurs sources. Vous devez disposer d’une licence pour l’édition B2B de Real-Time CDP afin de surveiller les données d’enrichissement de profil du compte.

Lisez ce document pour savoir comment utiliser le tableau de bord de surveillance afin de surveiller le parcours de vos données sur différents services Experience Platform.

## Commencer

Ce document nécessite une compréhension pratique des composants suivants de l’Experience Platform :

* [Flux de données](../home.md): les flux de données sont des représentations des tâches de données qui déplacent les données entre les Experience Platform. Vous pouvez utiliser l’espace de travail des sources pour créer des flux de données qui assimilent des données d’une source donnée à un Experience Platform.
* [Sources](../../sources/home.md): utilisez des sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.
* [Service d’identités](../../identity-service/home.md) : obtenez une meilleure compréhension des clients individuels et de leurs comportements en reliant les identités entre les appareils et les systèmes.
* [Profil client en temps réel](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Segmentation](../../segmentation/home.md): utilisez le service de segmentation pour créer des segments et des audiences à partir de vos données Real-time Customer Profile.
* [Destinations](../../destinations/home.md): les destinations sont des intégrations préconfigurées aux applications courantes qui permettent l’activation transparente des données de Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

## Guide de supervision du tableau de bord

Dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Surveillance]** under [!UICONTROL Data Management] dans le volet de navigation de gauche.

![Le tableau de bord de surveillance dans l’interface utilisateur de l’Experience Platform.](../assets/ui/monitor-overview/monitoring.png)

Sélectionner **[!UICONTROL Type de données]** puis utilisez le menu déroulant pour sélectionner le type de données à afficher. Les types de données sont définis par les classes de schéma du modèle de données d’expérience (XDM) pour s’assurer que leurs données suivent un format standard lorsqu’elles sont ingérées dans Experience Platform. Pour plus d’informations, consultez la documentation suivante :

* [Type de données de compte B2B](../../rtcdp/b2b-tutorial.md)
* [Type de données Prospect](../../rtcdp/partner-data/prospecting.md)

Vous pouvez filtrer votre vue en fonction des types de données suivants :

>[!BEGINTABS]

>[!TAB Tous]

Sélectionner **[!UICONTROL Tous]** pour mettre à jour votre tableau de bord et afficher les mesures sur toutes les données qui ont été ingérées à Experience Platform au cours d’une période donnée.

![Le type de données de surveillance est défini sur &quot;Tous&quot;.](../assets/ui/monitor-overview/all.png)

>[!TAB Client et compte]

Sélectionner **[!UICONTROL Client et compte]** pour mettre à jour votre tableau de bord et afficher les mesures sur les données de client et de compte qui ont été ingérées par Experience Platform au cours d’une période donnée.

![Le type de données de surveillance est défini sur &quot;Client et compte&quot;.](../assets/ui/monitor-overview/customer-account.png)

>[!TAB Prospect]

Sélectionner **[!UICONTROL Prospect]** pour mettre à jour votre tableau de bord et afficher les mesures sur les données de prospection qui ont été ingérées à Experience Platform au cours d’une période donnée. **Remarque**: vous ne pouvez afficher les activités de type de données prospect que si vous [Droit aux données de prospect](../../rtcdp/partner-data/prospecting.md).

![Le type de données de surveillance est défini sur &quot;Prospect&quot;.](../assets/ui/monitor-overview/prospect.png)

>[!TAB Enrichissement du profil du compte]

Sélectionner **[!UICONTROL Enrichissement du profil du compte]** pour mettre à jour votre tableau de bord et afficher les mesures sur les données d’enrichissement de profil. **Remarque**: vous ne pouvez afficher les mesures d’enrichissement de profil de compte que si vous êtes autorisé à [Données B2B](../../rtcdp/b2b-tutorial.md).

![Le type de données de surveillance est défini sur &quot;Enrichissement du profil du compte&quot;.](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

Utilisez l’en-tête supérieur du tableau de bord pour une expérience de surveillance interservices. Vous pouvez filtrer l’affichage des mesures et des graphiques en sélectionnant la carte des fonctionnalités de votre choix dans l’en-tête de la catégorie de données.

>[!BEGINTABS]

>[!TAB Sources]

Sélectionner **[!UICONTROL Sources]** pour afficher les mesures sur le taux d’ingestion de vos sources. Lisez le guide sur [données de surveillance des sources](monitor-sources.md) pour plus d’informations.

![Le tableau de bord de surveillance dans l’interface utilisateur avec la carte sources sélectionnée.](../assets/ui/monitor-overview/sources.png)

>[!TAB Identités]

Sélectionner **[!UICONTROL Identités]** pour afficher le taux de succès du traitement de vos données d’identité. Lisez le guide sur [surveillance des données d’identité](monitor-identities.md) pour plus d’informations.

![Le tableau de bord de surveillance dans l’interface utilisateur avec la carte d’identité sélectionnée.](../assets/ui/monitor-overview/identities.png)

>[!TAB Profils]

Sélectionner **[!UICONTROL Profils]** pour afficher le taux de succès du traitement des données de votre profil. Lisez le guide sur [surveillance des données de profil](monitor-profiles.md) pour plus d’informations.

![Le tableau de bord de surveillance dans l’interface utilisateur avec la carte de profils sélectionnée.](../assets/ui/monitor-overview/profiles.png)

>[!TAB Audiences]

Sélectionner **[!UICONTROL Audiences]** pour afficher les mesures sur vos audiences et tâches de segmentation. Lisez le guide sur [surveillance des données d’audience](monitor-audiences.md) pour plus d’informations.

![Le tableau de bord de surveillance dans l’interface utilisateur avec la carte d’audiences sélectionnée.](../assets/ui/monitor-overview/audiences.png)

>[!TAB Destinations]

Sélectionner **[!UICONTROL Destinations]** pour afficher les mesures sur votre [!UICONTROL Taux d’activation par flux] et [!UICONTROL Exécution de flux de données en échec du lot]. Lisez le guide sur [surveillance des données des destinations](monitor-destinations.md) pour plus d’informations.

![Le tableau de bord de surveillance dans l’interface utilisateur avec la carte des destinations sélectionnée.](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### Configuration de la période de surveillance {#configure-monitoring-time-frame}

Par défaut, le tableau de bord de surveillance affiche les mesures sur les données ingérées au cours des dernières 24 heures. Pour mettre à jour la période, sélectionnez **[!UICONTROL 24 dernières heures]**.

![Le tableau de bord de surveillance dans l’interface utilisateur avec la configuration de l’heure sélectionnée.](../assets/ui/monitor-overview/select-time.png)

Vous pouvez configurer une nouvelle période pour votre vue de surveillance des données dans la boîte de dialogue qui s’affiche. Vous avez la possibilité de créer une période personnalisée ou de sélectionner une option dans la liste des options préconfigurées :

* [!UICONTROL 24 dernières heures]
* [!UICONTROL 7 derniers jours]
* [!UICONTROL 30 derniers jours]

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![Fenêtre contextuelle de configuration de la période dans le tableau de bord de surveillance.](../assets/ui/monitor-overview/update-time.png)

## Étapes suivantes

En lisant ce document, vous pouvez désormais parcourir le tableau de bord de surveillance dans l’interface utilisateur. Pour plus d’informations sur la manière de surveiller les données pour un service d’Experience Platform spécifique, consultez la documentation ci-dessous :

* [Surveillance des données de sources](monitor-sources.md).
* [Surveillance des données d’identité](monitor-identities.md).
* [Surveillance des données de profil](monitor-profiles.md).
* [Surveillance des données d’audience](monitor-audiences.md).
* [Surveiller les données des destinations](monitor-destinations.md).
