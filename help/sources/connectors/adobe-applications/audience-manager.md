---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteur d’Audience Manager;Audience Manager;gestionnaire d’audience
solution: Experience Platform
title: Présentation d’Audience Manager Source
description: La source Adobe Audience Manager diffuse les données propriétaires collectées dans Audience Manager vers Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 8ef9fedcc77f39707ef5191988a5b7360e1118cc
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 17%

---

# Source Audience Manager

>[!IMPORTANT]
>
>Lors de la configuration initiale, la source Adobe Audience Manager renvoie un message d’erreur qui explique qu’un espace de noms d’identité avec un `namespaceCode={VALUE}` donné n’existe pas. **Remarque** : en arrière-plan, `namespaceCode` est utilisé pour faire référence au symbole d’identité. Pour terminer votre intégration, vous devez :
>
>- [Créez un espace de noms personnalisé dans Identity Service](../../../identity-service/features/namespaces.md#create-custom-namespaces) avec le symbole d’identité spécifié (`VALUE`) .
>- ingérez à nouveau vos données.

La source Adobe Audience Manager diffuse les données propriétaires collectées dans Adobe Audience Manager pour activation dans Adobe Experience Platform. La source d’Audience Manager ingère deux types de données vers Platform :

- **Données en temps réel :** données capturées en temps réel sur le serveur de collecte de données d’Audience Manager. Ces données sont utilisées en Audience Manager pour remplir des caractéristiques basées sur des règles et apparaîtront dans Platform dans le temps de latence le plus court.
- **Données de profil :** l’Audience Manager utilise des données en temps réel et intégrées pour dériver des profils client. Ces profils sont utilisés pour générer des graphiques d’identités et des caractéristiques sur des réalisations de segment.

La source d’Audience Manager mappe ces types de données à un schéma de modèle de données d’expérience (XDM), puis les envoie à Platform. Les données en temps réel sont envoyées sous forme de données XDM ExperienceEvent, tandis que les données Profile sont envoyées sous forme de données XDM Individual Profile.

Pour plus d’informations, consultez le guide sur la [création d’une connexion source d’Audience Manager dans l’interface utilisateur](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## En quoi consiste le modèle de données d’expérience (XDM) ?

XDM est une spécification documentée publiquement qui fournit un cadre normalisé grâce auquel Platform organise les données d’expérience client.

Le respect des normes XDM permet d’intégrer uniformément les données de l’expérience client, ce qui facilite la diffusion des données et la collecte des informations.

Pour plus d’informations sur l’utilisation de XDM dans Experience Platform, consultez la [présentation du système XDM](../../../xdm/home.md). Pour en savoir plus sur la structure des schémas XDM entre les profils et les événements, consultez les [bases de la composition des schémas](../../../xdm/schema/composition.md).

## Exemples de schémas XDM

Vous trouverez ci-dessous des exemples de structure Audience Manager mappés à des XDM ExperienceEvent et des XDM Individual Profile dans Platform.

### ExperienceEvent : pour les données en temps réel et les données intégrées

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### XDM Individual Profile - pour les données de profil

![](images/aam-profile-xdm-for-profile-data.png)

Pour plus d’informations sur la façon dont les champs sont mappés d’Audience Manager à XDM, consultez la documentation sur les [champs de mappage d’Audience Manager](./mapping/audience-manager.md).

## Gestion des données dans Platform

### Jeux de données

Un jeu de données est une structure de stockage et de gestion pour une collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes) et qui est mis à disposition par une connexion aux données. Les données d’Audience Manager se composent de données en temps réel, de données entrantes et de données de profil. Pour localiser vos jeux de données Audience Manager, utilisez la fonction de recherche de l’interface utilisateur en utilisant les conventions de dénomination fournies pour chaque type de données.

Par défaut, les jeux de données d’Audience Manager sont désactivés pour Profile et les utilisateurs peuvent activer ou désactiver des jeux de données en fonction de leurs cas d’utilisation. Il n’est pas recommandé de désactiver les jeux de données qui seront utilisés pour l’appartenance à un segment dans Profile.

>[!NOTE]
>
>AAM temps réel est le seul jeu de données qui va au lac de données. Tous les autres jeux de données d’Audience Manager vont à [!DNL Profile] s’ils sont activés pour [!DNL Profile]. S’ils ne sont pas activés pour [!DNL Profile], ils ne reçoivent aucune donnée et s’affichent comme vides.

| Nom du jeu de données | Description | Classe |
| --- | --- | --- |
| AAM temps réel | Ce jeu de données contient les données collectées à la suite d’accès directs aux points d’entrée DCS d’Audience Manager et aux mappages d’identités pour les profils Audience Manager. Conservez ce jeu de données activé pour l’ingestion dans Profile. | Événement d’expérience |
| AAM mises à jour de profil en temps réel | Ce jeu de données permet le ciblage en temps réel des caractéristiques et des segments d’Audience Manager. Il contient des informations pour le routage régional, les caractéristiques et l’adhésion aux segments Edge. Conservez ce jeu de données activé pour l’ingestion de profils. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer le bouton d’activation/désactivation **[!UICONTROL Profile]** pour ingérer directement les données dans Profile. | Enregistrement |
| Données de périphériques AAM | Données de l’appareil avec des ECID et réalisations de segment correspondantes agrégées dans l’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer le bouton d’activation/désactivation **[!UICONTROL Profile]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM des données de profil de périphérique | Utilisé pour les diagnostics de connecteur d’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer le bouton d’activation/désactivation **[!UICONTROL Profile]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM Profils authentifiés | Ce jeu de données contient des profils authentifiés de l’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer le bouton d’activation/désactivation **[!UICONTROL Profile]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM métadonnées des profils authentifiés | Utilisé pour les diagnostics de connecteur d’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer le bouton d’activation/désactivation **[!UICONTROL Profile]** pour ingérer directement les données dans Profile. | Enregistrement |
| Renvoi de données de périphériques AAM | Jeu de données issu de l’introduction de données d’appareils antérieures. Contient les ECID et les réalisations de segment correspondantes agrégées dans l’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer le bouton d’activation/désactivation **[!UICONTROL Profile]** pour ingérer directement les données dans Profile. | Enregistrement |
| AAM renvoi des profils authentifiés | Jeu de données à partir de l’introduction de données authentifiées antérieures. Contient les profils authentifiés de l’Audience Manager. Les données ne sont pas visibles en tant que lots dans le jeu de données. Vous pouvez activer le bouton d’activation/désactivation **[!UICONTROL Profile]** pour ingérer directement les données dans Profile. | Enregistrement |

### Connexions

Adobe Audience Manager crée une connexion dans le catalogue : connexion à l’Audience Manager. Le catalogue est le système d’enregistrements pour l’emplacement et la liaison des données au sein d’Adobe Experience Platform. Une connexion est un objet Catalog qui est une instance de connecteurs spécifique au client. Pour plus d’informations sur le catalogue, les connexions et les connecteurs, consultez la [présentation du service de catalogue](../../../catalog/home.md) .

### Impact de la population de segments sur le profil

La taille des populations de segments a un impact direct sur les numéros de profils lorsque vous envoyez un segment d’Audience Manager pour la première fois à Platform. Cela signifie que la sélection de tous les segments peut entraîner des dépassements de profil qui dépassent vos droits d’utilisation de licence. Platform distingue également les nouvelles données des données historiques pour l’ingestion de profils. Un segment avec 100 identités propriétaires crée 100 profils. Cependant, si la population de ce même segment a été augmentée à 150 et a été ingérée dans Platform, le nombre de profils n’augmentera que de 50, car il n’y a que 50 nouveaux profils.

Vous pouvez également vérifier l’utilisation du profil dont votre compte dispose via le [tableau de bord de l’utilisation de la licence](../../../dashboards/guides/license-usage.md).

## Quelle est la latence attendue sur Platform pour les données Audience Manager ?

| Données Audience Manager | Type | Latence | Remarques |
| --- | --- | --- | --- |
| Données en temps réel | Événements | &lt;25 minutes | Temps nécessaire pour que la capture au niveau du noeud Audience Manager Edge apparaisse dans le lac de données. |
| Données en temps réel | Mises à jour des profils | &lt;10 minutes | Temps d’accès dans Real-time Customer Profile. |
| Données en temps réel et intégrées | Mises à jour des profils | 24 à 36 heures | Temps nécessaire pour que les données DCS/PCS Edge et les données intégrées, en cours de traitement dans un profil utilisateur, apparaissent dans Real-time Customer Profile. Actuellement, ces données ne se trouvent pas directement dans le lac de données. Le basculement de profil peut être activé pour que les jeux de données de profil d’Audience Manager assimilent directement ces données dans Real-time Customer Profile. |
