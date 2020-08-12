---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur d’Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: a1b09f3e88e489f1b0ec0c1fcb72a2a5a4356d87
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 88%

---


# Connecteur d’Audience Manager

Le connecteur de données Adobe Audience Manager diffuse des données propriétaires collectées dans Adobe Audience Manager vers Adobe Experience Platform. Le connecteur Audience Manager ingère trois catégories de données vers Platform :

- **Données en temps réel :** données capturées en temps réel sur le serveur de collecte de données d’Audience Manager. Ces données sont utilisées dans Audience Manager pour générer des caractéristiques basées sur des règles et apparaîtront dans Platform dans le temps de latence le plus court.
- **Données de profil :** Audience Manager utilise des données en temps réel et intégrées pour dériver des profils clients. Ces profils sont utilisés pour générer des graphiques d’identités et des caractéristiques sur des réalisations de segment.

Le connecteur Audience Manager associe ces catégories de données à un schéma modèle de données d’expérience (XDM) et les envoie vers Platform. Les données en temps réel sont envoyées sous forme de données XDM ExperienceEvent, tandis que les données de Profil sont envoyées sous forme de Profils individuels XDM.

Pour obtenir des instructions sur la création d’une connexion avec Adobe Audience Manager à l’aide de l’interface utilisateur de Platform, consultez le [tutoriel sur le connecteur d’Audience Manager](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## En quoi consiste le modèle de données d’expérience (XDM) ?

XDM est une spécification documentée publiquement qui fournit un cadre normalisé grâce auquel Platform organise les données d’expérience client.

Le respect des normes XDM permet d’intégrer uniformément les données de l’expérience client, ce qui facilite la diffusion des données et la collecte des informations.

For more information about how XDM is used in Experience Platform, see the [XDM System overview](../../../xdm/home.md). Pour en savoir plus sur la manière dont les profils et les ExperienceEvent de type schéma XDM sont structurés, consultez les [principes de base de la composition des schémas](../../../xdm/schema/composition.md).

## Exemples de schémas XDM

Vous trouverez ci-dessous des exemples de structure Audience Manager mappés à des XDM ExperienceEvent et des XDM Individual Profile dans Platform.

### ExperienceEvent : pour les données en temps réel et les données intégrées

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile : pour les données de profil

![](images/aam-profile-xdm-for-profile-data.png)

## Comment les champs sont-ils mappés d’Adobe Audience Manager à XDM ?

Pour plus d’informations, veuillez consulter la documentation des [champs de mappage Audience Manager](./mapping/audience-manager.md).

## Gestion des données dans Platform

### Jeux de données

Les jeux de données sont une structure de stockage et de gestion d’une collecte de données, généralement un tableau qui contient des schémas (colonnes) et des champs (lignes) et est mis à disposition par une connexion de données. Les données Audience Manager se composent de données en temps réel, de données entrantes et de données de profil. Pour localiser vos jeux de données Audience Manager, utilisez la fonction de recherche de l’interface utilisateur en utilisant les conventions de dénomination fournies pour chaque type de données.

Par défaut, les jeux de données d&#39;Audience Manager sont désactivés pour le Profil et les utilisateurs peuvent activer ou désactiver les jeux de données en fonction de leurs cas d&#39;utilisation. Il n’est pas recommandé de désactiver les jeux de données qui seront utilisés pour l’appartenance à un segment dans le Profil.

| Nom du jeu de données | Description |
| ------------ | ----------- |
| Audience Manager Realtime | Ce jeu de données contient les données collectées à la suite d’accès directs aux points de terminaison DCS d’Audience Manager et aux mappages d’identités pour les profils Audience Manager. Conservez ce jeu de données activé pour l’ingestion dans Profile. |
| Audience Manager Realtime Profile Updates | Ce jeu de données active le ciblage en temps réel des caractéristiques et des segments d’Audience Manager. Il contient des informations pour le routage régional, les caractéristiques et l’adhésion aux segments Edge. Conservez ce jeu de données activé pour l’ingestion dans Profile. |
| Audience Manager Devices Data | Les données de l’appareil avec leurs ECID et les réalisations de segment correspondantes rassemblées dans Audience Manager. |
| Audience Manager Device Profile Data | Utilisé pour les diagnostics de connecteur d’Audience Manager. |
| Audience Manager Authenticated Profiles | Ce jeu de données contient des profils authentifiés Audience Manager. |
| Audience Manager Authenticated Profiles Meta Data | Utilisé pour les diagnostics de connecteur d’Audience Manager. |

### Connexions

Adobe Audience Manager crée une connexion dans le catalogue : **connexion Audience Manager**. Le catalogue est le système d’enregistrements pour l’emplacement et la liaison des données au sein d’Adobe Experience Platform. Une connexion est un objet du catalogue qui est une instance des connecteurs spécifique au client. Pour plus d’informations sur le catalogue, les connexions et les connecteurs, veuillez consulter la [présentation du service de catalogue](../../../catalog/home.md).

## Quelle est la latence attendue sur Platform pour les données Audience Manager ?

| Données Audience Manager | Latence | Remarques |
| --- | --- | --- |
| Données en temps réel | &lt; 35 minutes. | Temps nécessaire pour que les données capturées au niveau du nœud Realtime apparaissent dans le lac de données de Platform. |
| Données entrantes | &lt; 13 heures | Temps nécessaire pour que les données capturées au niveau des compartiments S3 apparaissent dans le lac de données de Platform. |
| Données de profil | &lt; 2 jours | Temps nécessaire pour ajouter les données en temps réel ou entrantes capturées à un profil utilisateur et faire apparaître celles-ci sur le lac de données de Platform. |