---
keywords: Experience Platform ; accueil ; rubriques populaires ; connecteur d’Audience Manager ; gestionnaire d’Audiences ; gestionnaire d’audiences
solution: Experience Platform
title: Présentation du connecteur de source d'Audience Manager
topic-legacy: overview
description: Le connecteur source Adobe Audience Manager diffuse les données propriétaires collectées en Audience Manager à Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 45%

---

# Connecteur d’Audience Manager

Le connecteur de données Adobe Audience Manager diffuse les données propriétaires collectées à Adobe Audience Manager vers Adobe Experience Platform. Le connecteur d’Audience Manager ingère deux catégories de données à la plate-forme :

- **Données en temps réel :** données capturées en temps réel sur le serveur de collecte de données d’Audience Manager. Ces données sont utilisées dans Audience Manager pour générer des caractéristiques basées sur des règles et apparaîtront dans Platform dans le temps de latence le plus court.
- **Données de profil :** l’Audience Manager utilise des données en temps réel et intégrées pour générer des profils client. Ces profils sont utilisés pour générer des graphiques d’identités et des caractéristiques sur des réalisations de segment.

Le connecteur Audience Manager associe ces catégories de données à un schéma modèle de données d’expérience (XDM) et les envoie vers Platform. Les données en temps réel sont envoyées sous forme de données XDM ExperienceEvent, tandis que les données de Profil sont envoyées sous forme de Profils individuels XDM.

Pour obtenir des instructions sur la création d’une connexion avec Adobe Audience Manager à l’aide de l’interface utilisateur de Platform, consultez le [tutoriel sur le connecteur d’Audience Manager](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## En quoi consiste le modèle de données d’expérience (XDM) ?

XDM est une spécification documentée publiquement qui fournit un cadre normalisé grâce auquel Platform organise les données d’expérience client.

Le respect des normes XDM permet d’intégrer uniformément les données de l’expérience client, ce qui facilite la diffusion des données et la collecte des informations.

Pour plus d&#39;informations sur l&#39;utilisation de XDM dans l&#39;Experience Platform, consultez l&#39;[Présentation du système XDM](../../../xdm/home.md). Pour en savoir plus sur la manière dont les profils et les ExperienceEvent de type schéma XDM sont structurés, consultez les [principes de base de la composition des schémas](../../../xdm/schema/composition.md).

## Exemples de schémas XDM

Vous trouverez ci-dessous des exemples de structure Audience Manager mappés à des XDM ExperienceEvent et des XDM Individual Profile dans Platform.

### ExperienceEvent - pour les données en temps réel et les données intégrées

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile : pour les données de profil

![](images/aam-profile-xdm-for-profile-data.png)

## Comment les champs sont-ils mappés d’Adobe Audience Manager à XDM ?

Pour plus d’informations, veuillez consulter la documentation des [champs de mappage Audience Manager](./mapping/audience-manager.md).

## Gestion des données dans Platform

### Jeux de données

Les jeux de données sont une structure de stockage et de gestion d’une collecte de données, généralement un tableau qui contient des schémas (colonnes) et des champs (lignes) et est mis à disposition par une connexion de données. Les données d’Audience Manager se composent de données en temps réel, de données entrantes et de données de Profil. Pour localiser vos jeux de données Audience Manager, utilisez la fonction de recherche de l’interface utilisateur en utilisant les conventions de dénomination fournies pour chaque type de données.

Par défaut, les jeux de données d&#39;Audience Manager sont désactivés pour le Profil et les utilisateurs peuvent activer ou désactiver les jeux de données en fonction de leurs cas d&#39;utilisation. Il n’est pas recommandé de désactiver les jeux de données qui seront utilisés pour l’appartenance à un segment dans le Profil.

| Nom du jeu de données | Description |
| ------------ | ----------- |
| AAM Temps réel | Ce jeu de données contient les données collectées à la suite d’accès directs aux points de terminaison DCS d’Audience Manager et aux mappages d’identités pour les profils Audience Manager. Conservez ce jeu de données activé pour l’ingestion dans Profile. |
| AAM mises à jour du Profil en temps réel | Ce jeu de données permet le ciblage en temps réel des caractéristiques et des segments d’Audience Manager. Il contient des informations pour le routage régional, les caractéristiques et l’adhésion aux segments Edge. Conservez ce jeu de données activé pour l’ingestion dans Profile. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la bascule **[!UICONTROL Profil]** pour assimiler directement les données au Profil. |
| Données des périphériques AAM | Les données de l’appareil avec leurs ECID et les réalisations de segment correspondantes rassemblées dans Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la bascule **[!UICONTROL Profil]** pour assimiler directement les données au Profil. |
| Données de Profil de périphérique AAM | Utilisé pour les diagnostics de connecteur d’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la bascule **[!UICONTROL Profil]** pour assimiler directement les données au Profil. |
| profils authentifiés AAM | Ce jeu de données contient des profils authentifiés Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la bascule **[!UICONTROL Profil]** pour assimiler directement les données au Profil. |
| Métadonnées des Profils authentifiés AAM | Utilisé pour les diagnostics de connecteur d’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la bascule **[!UICONTROL Profil]** pour assimiler directement les données au Profil. |
| Renvoi de données AAM périphériques | Jeu de données d&#39;importation de données de périphériques antérieures. Il contient des ECID et les réalisations de segments correspondantes agrégées en Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la bascule **[!UICONTROL Profil]** pour assimiler directement les données au Profil. |
| Renvoi de Profils authentifiés AAM | Jeu de données d’importation de données authentifiées antérieures. Contient des profils authentifiés par Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer la bascule **[!UICONTROL Profil]** pour assimiler directement les données au Profil. |

### Connexions

Adobe Audience Manager crée une connexion dans le catalogue : connexion Audience Manager. Le catalogue est le système d’enregistrements pour l’emplacement et la liaison des données au sein d’Adobe Experience Platform. Une connexion est un objet du catalogue qui est une instance des connecteurs spécifique au client. Pour plus d’informations sur le catalogue, les connexions et les connecteurs, veuillez consulter la [présentation du service de catalogue](../../../catalog/home.md).

## Quelle est la latence attendue sur Platform pour les données Audience Manager ?

| Données Audience Manager | Latence | Remarques |
| --- | --- | --- |
| Données en temps réel | &lt; 35 minutes. | Temps passé de la capture au noeud Audience Manager Edge à l&#39;apparition sur Platform Data Lake. |
| Données de profil | &lt; 2 jours | Temps écoulé entre la capture via les données Edge DCS/PCS et les données intégrées, le traitement vers un profil utilisateur, puis leur apparition dans le Profil. Ces données ne se posent pas directement sur Platform Data Lake aujourd&#39;hui. Le basculement de profil peut être activé pour que les jeux de données de Profil d&#39;Audience Manager assimilent directement ces données dans le Profil. |
