---
keywords: Experience Platform;accueil;rubriques populaires;connecteur Audience Manager;Audience manager;audience manager
solution: Experience Platform
title: Présentation d’Audience Manager Source
description: La source Adobe Audience Manager diffuse des données propriétaires collectées dans Audience Manager vers Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 13%

---

# Source Audience Manager

>[!IMPORTANT]
>
>Lors de votre configuration initiale, la source Adobe Audience Manager renvoie un message d’erreur expliquant qu’il n’existe pas d’espace de noms d’identité avec une `namespaceCode={VALUE}` donnée. **Remarque** : en arrière-plan, `namespaceCode` est utilisé pour faire référence au symbole d’identité. Pour terminer l’intégration, vous devez :
>
>- [Créez un espace de noms personnalisé dans Identity Service](../../../identity-service/features/namespaces.md#create-custom-namespaces) avec le symbole d’identité spécifié (`VALUE`) .
>- Réingérez vos données.

La source Adobe Audience Manager diffuse des données propriétaires collectées dans Adobe Audience Manager pour activation dans Adobe Experience Platform. La source Audience Manager ingère deux types de données dans Experience Platform :

- **Données en temps réel :** données capturées en temps réel sur le serveur de collecte de données d’Audience Manager. Ces données sont utilisées dans Audience Manager pour générer des caractéristiques basées sur des règles et apparaîtront dans Experience Platform dans le temps de latence le plus court.
- **Données de profil :** Audience Manager utilise des données en temps réel et intégrées pour dériver des profils clients. Ces profils sont utilisés pour générer des graphiques d’identités et des caractéristiques sur des réalisations de segment.

La source Audience Manager mappe ces types de données à un schéma de modèle de données d’expérience (XDM), puis les envoie vers Experience Platform. Les données en temps réel sont envoyées en tant que données XDM ExperienceEvent, tandis que les données de profil sont envoyées en tant que données XDM Individual Profile.

Pour plus d’informations, consultez le guide sur la [création d’une connexion source Audience Manager dans l’interface utilisateur](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## En quoi consiste le modèle de données d’expérience (XDM) ?

XDM est une spécification documentée publiquement qui fournit un cadre normalisé selon lequel Experience Platform organise les données d’expérience client.

Le respect des normes XDM permet d’intégrer uniformément les données de l’expérience client, ce qui facilite la diffusion des données et la collecte des informations.

Pour plus d’informations sur l’utilisation de XDM dans Experience Platform, consultez la [ Présentation du système XDM ](../../../xdm/home.md). Pour en savoir plus sur la structure des schémas XDM entre les profils et les événements, lisez les [principes de base de la composition des schémas](../../../xdm/schema/composition.md).

## Exemples de schémas XDM

Vous trouverez ci-dessous des exemples de structure Audience Manager mappés à XDM ExperienceEvent et XDM Individual Profile dans Experience Platform.

### ExperienceEvent - pour les données en temps réel et les données intégrées

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile - pour les données de profil

![](images/aam-profile-xdm-for-profile-data.png)

Pour plus d’informations sur le mappage des champs d’Audience Manager à XDM, consultez la documentation sur le [mappage des champs d’Audience Manager](./mapping/audience-manager.md).

## Gestion des données sur Experience Platform

### Jeux de données

Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes) et qui est rendu disponible par une connexion aux données. Les données Audience Manager se composent de données en temps réel, de données entrantes et de données de profil. Pour localiser vos jeux de données Audience Manager, utilisez la fonction de recherche de l’interface utilisateur en utilisant les conventions de dénomination fournies pour chaque type de données.

Les jeux de données Audience Manager sont désactivés pour le profil par défaut et les utilisateurs peuvent activer ou désactiver les jeux de données en fonction de leurs cas d’utilisation. Il n’est pas recommandé de désactiver les jeux de données qui seront utilisés pour l’appartenance à un segment dans le profil.

>[!NOTE]
>
>AAM Real-time est le seul jeu de données qui va au lac de données. Tous les autres jeux de données d’Audience Manager sont [!DNL Profile], s’ils sont activés pour la [!DNL Profile]. Si elles ne sont pas activées pour [!DNL Profile], elles ne reçoivent aucune donnée et elles s’affichent comme vides.

| Nom du jeu de données | Description | Classe |
| --- | --- | --- |
| AAM en temps réel | Ce jeu de données contient les données collectées à la suite d’accès directs aux points d’entrée DCS d’Audience Manager et aux mappages d’identités pour les profils Audience Manager. Conservez ce jeu de données activé pour l’ingestion dans Profile. | Événement d’expérience |
| Mises à jour du profil en temps réel d’AAM | Ce jeu de données permet le ciblage en temps réel des caractéristiques et des segments Audience Manager. Il contient des informations pour le routage régional, les caractéristiques et l’adhésion aux segments Edge. Gardez ce jeu de données activé pour l’ingestion de profils. Les données ne sont pas visibles sous forme de lots dans le jeu de données. Vous pouvez activer le bouton (bascule) **[!UICONTROL Profil]** pour ingérer directement les données dans le profil. | Enregistrement |
| Données des appareils AAM | Données d’appareil avec ECID et réalisations de segment correspondantes agrégées dans Audience Manager. Les données ne sont pas visibles sous forme de lots dans le jeu de données. Vous pouvez activer le bouton (bascule) **[!UICONTROL Profil]** pour ingérer directement les données dans le profil. | Enregistrement |
| Données de profil d’appareil AAM | Utilisé pour les diagnostics de connecteur d’Audience Manager. Les données ne sont pas visibles sous forme de lots dans le jeu de données. Vous pouvez activer le bouton (bascule) **[!UICONTROL Profil]** pour ingérer directement les données dans le profil. | Enregistrement |
| Profils authentifiés AAM | Ce jeu de données contient des profils authentifiés Audience Manager. Les données ne sont pas visibles sous forme de lots dans le jeu de données. Vous pouvez activer le bouton (bascule) **[!UICONTROL Profil]** pour ingérer directement les données dans le profil. | Enregistrement |
| Métadonnées des profils authentifiés AAM | Utilisé pour les diagnostics du connecteur Audience Manager. Les données ne sont pas visibles sous forme de lots dans le jeu de données. Vous pouvez activer le bouton (bascule) **[!UICONTROL Profil]** pour ingérer directement les données dans le profil. | Enregistrement |
| Renvoi de données d’appareils AAM | Jeu de données provenant de l’importation de données d’appareils antérieures. Contient des ECID et les réalisations de segment correspondantes agrégés dans Audience Manager. Les données ne sont pas visibles sous forme de lots dans le jeu de données. Vous pouvez activer le bouton (bascule) **[!UICONTROL Profil]** pour ingérer directement les données dans le profil. | Enregistrement |
| Renvoi de profils authentifiés AAM | Jeu de données provenant de l’importation de données authentifiées antérieures. Contient des profils authentifiés Audience Manager. Les données ne sont pas visibles sous forme de lots dans le jeu de données. Vous pouvez activer le bouton (bascule) **[!UICONTROL Profil]** pour ingérer directement les données dans le profil. | Enregistrement |

### Connexions

Adobe Audience Manager crée une connexion dans le catalogue : connexion Audience Manager. Le catalogue est le système d’enregistrements pour l’emplacement et la liaison des données au sein d’Adobe Experience Platform. Une connexion est un objet Catalog qui est une instance de connecteurs spécifique au client. Lisez la [Présentation du service de catalogue](../../../catalog/home.md) pour plus d’informations sur le catalogue, les connexions et les connecteurs.

### Impact de la population de segments sur le profil

La taille de la population de segments a un impact direct sur les nombres de profils lorsque vous envoyez un segment Audience Manager pour la première fois à Experience Platform. Cela signifie que la sélection de tous les segments peut potentiellement entraîner des dépassements de profil supérieurs à vos droits d’utilisation de licence. Experience Platform distingue également les nouvelles données des données historiques pour l’ingestion de profils. Un segment avec 100 identités propriétaires crée 100 profils. Cependant, si la population de ce même segment a été augmentée à 150 et a été ingérée dans Experience Platform, le nombre de profils n’augmentera que de 50, car il n’y a que 50 nouveaux profils.

Vous pouvez également vérifier l’utilisation du profil de votre compte via le [Tableau de bord d’utilisation des licences](../../../dashboards/guides/license-usage.md).

## Quelle est la latence attendue pour les données Audience Manager sur Experience Platform ?

| Données Audience Manager | Type | Latence | Remarques |
| --- | --- | --- | --- |
| Données en temps réel | Événements | &lt;25 minutes | Temps écoulé entre la capture au niveau du nœud Audience Manager Edge et l’affichage dans le lac de données. |
| Données en temps réel | Mises à jour des profils | &lt;10 minutes | Temps d’arrivée dans le profil client en temps réel. |
| Données en temps réel et intégrées | Mises à jour des profils | 24 à 36 heures | Temps écoulé entre la capture des données Edge DCS/PCS et les données intégrées, leur traitement pour obtenir un profil utilisateur et leur affichage dans le profil client en temps réel. Actuellement, ces données n’arrivent pas directement dans le lac de données. Le bouton Profile peut être activé pour que les jeux de données de profil Audience Manager ingèrent directement ces données dans le profil client en temps réel. |
