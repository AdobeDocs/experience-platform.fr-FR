---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: fb4ffa2c95365905f5417586fa7ecf88523009a0
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---


# Connecteur Audience Manager

Le connecteur de données Adobe Audience Manager diffuse les données propriétaires collectées dans Adobe Audience Manager vers Adobe Experience Platform. Le connecteur Audience Manager ingère trois catégories de données à la plate-forme :

- **Données en temps réel :** Données capturées en temps réel sur le serveur de collecte de données d’Audience Manager. Ces données sont utilisées dans Audience Manager pour renseigner les caractéristiques basées sur les règles et apparaîtront dans Platform dans le délai de latence le plus court.
- **Données intégrées (entrées) :** Il s’agit des fichiers téléchargés par un utilisateur vers un emplacement Amazon S3 hébergé par Audience Manager. Audience Manager utilise ces données pour renseigner les caractéristiques embarquées à l’aide de la méthode de fichier entrant et aura une certaine latence.
- **Données du Profil :** Audience Manager utilise les données en temps réel et intégrées pour dériver les profils client. Ces profils sont utilisés pour remplir des graphiques d’identité et des caractéristiques sur les realisations de segments.

Le connecteur Audience Manager mappe ces catégories de données au schéma de modèle de données d’expérience (XDM) et les envoie à la plate-forme. Les données en temps réel et les données intégrées sont envoyées sous forme de données XDM ExperienceEvent, tandis que les données de Profil sont envoyées sous forme de Profils individuels XDM.

Pour obtenir des instructions sur la création d’une connexion avec Adobe Audience Manager à l’aide de l’interface utilisateur de la plate-forme, consultez le didacticiel [sur le connecteur](../../tutorials/ui/create/adobe-applications/audience-manager.md)Audience Manager.

## Qu’est-ce que le modèle de données d’expérience (XDM) ?

XDM est une spécification publiquement documentée qui fournit un cadre standardisé par lequel Platform organise les données d’expérience client.

Le respect des normes XDM permet d’intégrer uniformément les données d’expérience client, ce qui facilite la diffusion des données et la collecte des informations.

Pour plus d’informations sur l’utilisation de XDM dans Experience Platform, voir l’aperçu [du système](../../../xdm/home.md)XDM. Pour en savoir plus sur la structure des Schémas XDM tels que Profil et ExperienceEvent, consultez les [bases de la composition](../../../xdm/schema/composition.md)des schémas.

## Exemples de schémas XDM

Vous trouverez ci-dessous des exemples de la structure de Audience Manager mise en correspondance avec XDM ExperienceEvent et XDM Individuel Profil in Platform.

### ExperienceEvent - pour les données en temps réel et les données intégrées

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Profil XDM individuel - pour les données de Profil

![](images/aam-profile-xdm-for-profile-data.png)

## Comment les champs d’Adobe Audience Manager sont-ils mappés à XDM ?

Pour plus d&#39;informations, consultez la documentation relative aux champs [de mappage d&#39;](./mapping/audience-manager.md) Audience Manager.

## Data Management sur la plate-forme

### Jeux de données

Les jeux de données sont un concept d&#39;enregistrement et de gestion pour une collection de données, généralement une table, qui contient des schémas (colonnes) et des champs (lignes) et est rendue disponible par une connexion aux données. Les données du Gestionnaire d’Audiences se composent de données en temps réel, de données entrantes et de données de Profil. Pour localiser vos jeux de données Audience Manager, utilisez la fonction de recherche dans l’interface utilisateur avec les conventions d’affectation de nom fournies pour chaque type de données.

Par défaut, les jeux de données d’Audience Manager sont désactivés pour le Profil et les utilisateurs peuvent activer ou désactiver les jeux de données en fonction de leurs cas d’utilisation. Il n’est pas recommandé de désactiver les jeux de données qui seront utilisés pour l’appartenance à un segment dans le Profil.

| Nom du jeu de données | Description |
| ------------ | ----------- |
| Audience Manager en temps réel | Ce jeu de données contient les données collectées par les accès directs sur les points de terminaison DCS de Audience Manager et les cartes d’identité pour les Profils Audience Manager. Laissez ce jeu de données activé pour l&#39;assimilation de Profils. |
| Mises à jour du Profil en temps réel d’Audience Manager | Ce jeu de données permet le ciblage en temps réel des caractéristiques et des segments d’Audience Manager. Il contient des informations sur les routages régionaux Edge, leurs caractéristiques et les adhésions aux segments. Laissez ce jeu de données activé pour l&#39;assimilation de Profils. |
| Données des périphériques Audience Manager | Données de périphérique avec les ECID et les réalisations de segments correspondantes agrégées dans Audience Manager. |
| Données du Profil du périphérique Audience Manager | Utilisé pour les diagnostics du connecteur d’Audience Manager. |
| Profils authentifiés d’Audience Manager | Ce jeu de données contient des profils authentifiés Audience Manager. |
| Métadonnées des Profils authentifiés de Audience Manager | Utilisé pour les diagnostics du connecteur d’Audience Manager. |
| Audience Manager entrant {ID de source de données} **(obsolète)** | Ce jeu de données représente les enregistrements intégrés dans Audience Manager via la méthode de fichier entrant. Ce flux de données est obsolète et sera supprimé dans une version ultérieure. |
| Métadonnées entrantes du Gestionnaire d’Audiences **(obsolète)** | Utilisé pour les diagnostics du connecteur d’Audience Manager. Ce flux de données est obsolète et sera supprimé dans une version ultérieure. |

### Connexions

Adobe Audience Manager crée une connexion dans le catalogue : **Audience Manager Connection**. Le catalogue est le système des enregistrements pour l’emplacement et le lignage des données dans Adobe Experience Platform. Une connexion est un objet Catalog qui est une instance spécifique au client de Connectors. Pour plus d’informations sur le catalogue, les connexions et les connecteurs, consultez la présentation [du service de](../../../catalog/home.md) catalogue.

## Quelle est la latence attendue pour les données d’Audience Manager sur la plateforme ?

| Audience Manager Data | Latence | Notes |
| --- | --- | --- |
| Données en temps réel | &lt; 35 minutes. | Temps passé de la capture au noeud Realtime à l’apparition sur Platform Data Lake. |
| Données entrantes | &lt; 13 heures | Temps passé de la capture dans les seaux S3 à l&#39;apparition sur Platform Data Lake. |
| Données du Profil | &lt; 2 jours | Temps écoulé entre la capture des données en temps réel et les données entrantes et leur ajout à un profil utilisateur et leur affichage final sur Platform Data Lake. |