---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur   Manager
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# Connecteur   Manager

Le connecteur de données d’Adobe   Manager diffuse les données propriétaires collectées dans Adobe  Manager vers Adobe Experience Platform. Le connecteur  Gestionnaire de  de intègre trois de données à la plateforme :

- **Données en temps réel :** Données capturées en temps réel sur  serveur de collecte de données de  Manager. Ces données sont utilisées dans  Gestionnaire de  de pour renseigner les caractéristiques basées sur les règles et apparaîtront dans la plateforme dans le temps de latence le plus court.
- **Onboarded (inbound) data:** These are the files uploaded by a user into an Amazon S3 location hosted by Audience Manager. Audience Manager uses this data to populate onboarded traits using the inbound file method and will have some latency.
- **Données  :**  Gestionnaire de  de utilise des données en temps réel et intégrées pour dériver le du client . These profiles are used to populate identity graphs and traits on segment realizations.

Le connecteur  Gestionnaire de  de données mappe ces de données  aumodèle de données d’expérience (XDM) et les envoie à la plateforme. Les données en temps réel et les données intégrées sont envoyées sous la forme de données XDM ExperienceEvent, tandis que les données  sont envoyées sous la forme d’un  XDM individuel.

Pour plus d’informations sur la création d’une connexion avec Adobe  Gestionnaire de à l’aide de l’interface utilisateur de la plateforme, reportez-vous au didacticiel [sur le connecteur du Gestionnaire de](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)de la plate-forme.

## Qu’est-ce que le modèle de données d’expérience (XDM) ?

XDM est une spécification publiquement documentée qui fournit un cadre standardisé par lequel Platform organise les données d’expérience client.

Le respect des normes XDM permet d’intégrer uniformément les données d’expérience client, ce qui facilite la diffusion des données et la collecte des informations.

Pour plus d’informations sur l’utilisation de XDM dans Experience Platform, voir Présentation [du système](../../../xdm/home.md)XDM. Pour en savoir plus sur la manière dont les XDM  tels que  et ExperienceEvent sont structurés, reportez-vous aux [bases de la composition](../../../xdm/schema/composition.md)de la  de l’architecture.

## Exemples de  XDM

Vous trouverez ci-dessous des exemples de la structure   Manager mappée à XDM ExperienceEvent et XDM Individuel dans Platform.

### ExperienceEvent - for Realtime data and Onboarded data

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile - for Profile data

![](images/aam-profile-xdm-for-profile-data.png)

## Comment les champs sont-ils mappés d’Adobe  Gestionnaire de à XDM ?

Pour plus d&#39;informations, consultez la documentation pour [champs][audience-manager-mapping-fields] de mappage de  Manager.

##  sur la plate-forme

### Jeux de données

Les jeux de données sont un concept  de  et de gestion pour une collection de données, généralement un tableau, qui contient des (colonnes) et des champs (lignes) et qui est rendu disponible par une connexion aux données.  données du Gestionnaire de  de se composent de données en temps réel, de données d’entrée et de données de. Pour localiser vos jeux de données  Manager , utilisez la fonction de recherche dans l’interface utilisateur avec les conventions d’affectation de nom fournies pour chaque type de données.

Bien que les utilisateurs puissent désactiver les jeux de données, il n’est pas recommandé de désactiver les jeux de données qui seront utilisés pour l’adhésion aux segments dans les  de.

| Nom du jeu de données | Description |
| ------------ | ----------- |
|  Gestionnaire de  en temps réel | Ce jeu de données contient des données collectées par des accès directs sur  points de fin DCS de  Manager et des cartes d’identité pour leGestionnaire de de . Conservez ce jeu de données activé pour l’assimilation de  d’. |
|  Gestionnaire de   Gestionnaire de Mises à jour en temps réel | Ce jeu de données active le ciblage en temps réel des caractéristiques et segments   Manager. Il contient des informations sur les  régionales Edge, les caractéristiques et l’appartenance aux segments. Conservez ce jeu de données activé pour l’assimilation de  d’. |
|  de données sur les périphériques  Manager | Données de périphérique avec les ECID et les réalisations de segments correspondantes agrégées dans  Gestionnaire de  de. |
|  de données de de périphérique   Manager | Utilisé pour  diagnostics du connecteur  Manager. |
|  Gestionnaire de  de  authentifié | Ce jeu de données contient   Gestionnaire de  authentifié. |
|  Gestionnaire de  de a authentifié les métadonnées de l’ | Utilisé pour  diagnostics  Manager Connector. |
|  Gestionnaire de  de entrant {ID de source de données} **(obsolète)** | Ce jeu de données représente les enregistrements intégrés dans  Gestionnaire  via la méthode de fichier entrant. Ce flux de données est obsolète et sera supprimé dans une version ultérieure. |
|  de métadonnées entrantes du Gestionnaire  de **(obsolète)** | Utilisé pour  diagnostics du connecteur  Manager. Ce flux de données est obsolète et sera supprimé dans une version ultérieure. |

### Connexions

Adobe   Manager crée une connexion dans le catalogue : **connexion** Manager. Le catalogue est le système des enregistrements de l’emplacement et de la lignée des données dans Adobe Experience Platform. Une connexion est un objet Catalog qui est une instance spécifique au client de Connectors. Pour plus d’informations sur le catalogue, les connexions et les connecteurs, consultez la présentation [du service de](../../../catalog/home.md) catalogue.

## What is the expected latency for Audience Manager Data on Platform?

| Audience Manager Data | Latence | Notes |
| --- | --- | --- |
| Données en temps réel | &lt; 35 minutes. | Time from being captured at Realtime node to appearing on Platform Data Lake. |
| Données entrantes | &lt; 13 heures | Time from being captured at S3 buckets to appearing on Platform Data Lake. |
| Profile data | &lt; 2 jours | Temps écoulé entre la capture des données en temps réel/entrantes et leur ajout à un  utilisateur et leur affichage final sur Platform Data Lake. |