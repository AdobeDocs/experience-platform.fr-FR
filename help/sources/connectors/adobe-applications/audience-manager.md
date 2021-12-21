---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteur d’Audience Manager;Audience Manager;gestionnaire d’audience
solution: Experience Platform
title: Présentation d’Audience Manager Source Connector
topic-legacy: overview
description: Le connecteur source Adobe Audience Manager diffuse les données propriétaires collectées dans Audience Manager vers Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: d0b6885b6e8606692cfe1173b75c7d3537800a5f
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 43%

---

# Connecteur d’Audience Manager

Le connecteur de données Adobe Audience Manager diffuse les données propriétaires collectées dans Adobe Audience Manager vers Adobe Experience Platform. Le connecteur d’Audience Manager ingère deux catégories de données vers Platform :

- **Données en temps réel :** Données capturées en temps réel sur le serveur de collecte de données d’Audience Manager. Ces données sont utilisées dans Audience Manager pour générer des caractéristiques basées sur des règles et apparaîtront dans Platform dans le temps de latence le plus court.
- **Données de profil :** Audience Manager utilise des données en temps réel et intégrées pour dériver des profils clients. Ces profils sont utilisés pour générer des graphiques d’identités et des caractéristiques sur des réalisations de segment.

Le connecteur Audience Manager associe ces catégories de données à un schéma modèle de données d’expérience (XDM) et les envoie vers Platform. Les données en temps réel sont envoyées sous forme de données XDM ExperienceEvent, tandis que les données de profil sont envoyées sous la forme de profils individuels XDM.

Pour obtenir des instructions sur la création d’une connexion avec Adobe Audience Manager à l’aide de l’interface utilisateur de Platform, consultez le [tutoriel sur le connecteur d’Audience Manager](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## En quoi consiste le modèle de données d’expérience (XDM) ?

XDM est une spécification documentée publiquement qui fournit un cadre normalisé grâce auquel Platform organise les données d’expérience client.

Le respect des normes XDM permet d’intégrer uniformément les données de l’expérience client, ce qui facilite la diffusion des données et la collecte des informations.

Pour plus d’informations sur l’utilisation de XDM dans Experience Platform, voir [Présentation du système XDM](../../../xdm/home.md). Pour en savoir plus sur la manière dont les profils et les ExperienceEvent de type schéma XDM sont structurés, consultez les [principes de base de la composition des schémas](../../../xdm/schema/composition.md).

## Exemples de schémas XDM

Vous trouverez ci-dessous des exemples de structure Audience Manager mappés à des XDM ExperienceEvent et des XDM Individual Profile dans Platform.

### ExperienceEvent : pour les données en temps réel et les données intégrées

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile : pour les données de profil

![](images/aam-profile-xdm-for-profile-data.png)

## Comment les champs sont-ils mappés d’Adobe Audience Manager à XDM ?

Pour plus d’informations, veuillez consulter la documentation des [champs de mappage Audience Manager](./mapping/audience-manager.md).

## Gestion des données dans Platform

### Jeux de données

Les jeux de données sont une structure de stockage et de gestion d’une collecte de données, généralement un tableau qui contient des schémas (colonnes) et des champs (lignes) et est mis à disposition par une connexion de données. Les données d’Audience Manager se composent de données en temps réel, de données entrantes et de données de profil. Pour localiser vos jeux de données Audience Manager, utilisez la fonction de recherche de l’interface utilisateur en utilisant les conventions de dénomination fournies pour chaque type de données.

Par défaut, les jeux de données d’Audience Manager sont désactivés pour Profile et les utilisateurs peuvent activer ou désactiver des jeux de données en fonction de leurs cas d’utilisation. Il n’est pas recommandé de désactiver les jeux de données qui seront utilisés pour l’appartenance à un segment dans Profile.

>[!NOTE]
>
>AAM Temps réel est le seul jeu de données qui va à la variable [!DNL Data Lake]. Tous les autres jeux de données d’Audience Manager sont dirigés vers [!DNL Profile], s’ils sont activés pour [!DNL Profile]. S’ils ne sont pas activés pour [!DNL Profile], elles ne reçoivent aucune donnée et s’affichent comme vides.

| Nom du jeu de données | Description | Classe |
| --- | --- | --- |
| AAM temps réel | Ce jeu de données contient les données collectées à la suite d’accès directs aux points de terminaison DCS d’Audience Manager et aux mappages d’identités pour les profils Audience Manager. Conservez ce jeu de données activé pour l’ingestion dans Profile. | Événement d’expérience |
| AAM mises à jour de profil en temps réel | Ce jeu de données permet le ciblage en temps réel des caractéristiques et des segments d’Audience Manager. Il contient des informations pour le routage régional, les caractéristiques et l’adhésion aux segments Edge. Conservez ce jeu de données activé pour l’ingestion dans Profile. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la variable **[!UICONTROL Profil]** pour ingérer directement les données dans Profile. | Enregistrement |
| Données de périphériques AAM | Les données de l’appareil avec leurs ECID et les réalisations de segment correspondantes rassemblées dans Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la variable **[!UICONTROL Profil]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM des données de profil de périphérique | Utilisé pour les diagnostics de connecteur d’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la variable **[!UICONTROL Profil]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM Profils authentifiés | Ce jeu de données contient des profils authentifiés Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la variable **[!UICONTROL Profil]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM métadonnées des profils authentifiés | Utilisé pour les diagnostics de connecteur d’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la variable **[!UICONTROL Profil]** pour ingérer directement les données dans Profile. | Enregistrement |
| Renvoi de données de périphériques AAM | Jeu de données d’importation de données d’appareils antérieures. Contient les ECID et les réalisations de segment correspondantes agrégées dans l’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la variable **[!UICONTROL Profil]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM renvoi des profils authentifiés | Jeu de données à partir de l’introduction de données authentifiées antérieures. Contient les profils authentifiés de l’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la variable **[!UICONTROL Profil]** pour ingérer directement les données dans Profile. | Enregistrement |

### Connexions

Adobe Audience Manager crée une connexion dans le catalogue : connexion Audience Manager. Le catalogue est le système d’enregistrements pour l’emplacement et la liaison des données au sein d’Adobe Experience Platform. Une connexion est un objet du catalogue qui est une instance des connecteurs spécifique au client. Pour plus d’informations sur le catalogue, les connexions et les connecteurs, veuillez consulter la [présentation du service de catalogue](../../../catalog/home.md).

## Quelle est la latence attendue sur Platform pour les données Audience Manager ?

| Données Audience Manager | Latence | Remarques |
| --- | --- | --- |
| Données en temps réel | &lt; 35 minutes. | Temps nécessaire pour que la capture du noeud Edge d’Audience Manager apparaisse sur le lac de données de Platform. |
| Données de profil | &lt; 2 jours | Temps nécessaire pour que les données DCS/PCS Edge et les données intégrées, en cours de traitement dans un profil utilisateur, apparaissent ensuite dans Profile. Ces données ne se trouvent pas directement sur le lac de données de Platform aujourd’hui. Le basculement de profil peut être activé pour que les jeux de données Profile d’Audience Manager assimilent ces données directement dans Profile. |
