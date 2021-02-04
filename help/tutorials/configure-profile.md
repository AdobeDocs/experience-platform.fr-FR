---
keywords: Experience Platform ; accueil ; rubriques populaires ; Profil client en temps réel ; Service d'identité ;
solution: Experience Platform
title: Tutoriels sur Real-time Customer Profile
topic: tutorial
type: Tutorial
description: Ce document décrit les étapes à suivre et fournit des liens vers des tutoriels pour effectuer chaque workflow séparément.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 26%

---


# Configurer [!DNL Real-time Customer Profile] et [!DNL Identity Service]

Pour configurer [!DNL Real-time Customer Profile] pour votre organisation, vous devez exécuter plusieurs workflows distincts. Ce document décrit les étapes à suivre et fournit des liens vers des tutoriels pour effectuer chaque workflow séparément.

Pour en savoir plus sur [!DNL Real-time Customer Profile], lisez tout d&#39;abord [Profil overview](../profile/home.md).

## Présentation de l’interface utilisateur du Profil client en temps réel

Real-time Customer Profile offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces.

**Ce guide vous aidera à :**
- Comprenez l&#39;interface utilisateur [!UICONTROL Profils] et les fonctionnalités disponibles.
- Vue et gestion des données de Profil.

Pour en savoir plus, consultez le [Guide de l’utilisateur du Profil client en temps réel](../profile/ui/user-guide.md).

## API Real-time Customer Profile

L’API Profil client en temps réel comprend plusieurs points de terminaison. Profile vous permet de consolider diverses données clients provenant de plusieurs canaux, comme les données en ligne, hors ligne, CRM et tierces, en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client. Pour plus d&#39;informations sur chacun des points de terminaison disponibles et leurs cas d&#39;utilisation, consultez la [Présentation de l&#39;API Profil client en temps réel](../profile/api/overview.md).

**Les guides suivants à l’intention des développeurs d’API sont disponibles :**
- [Attributs calculés (alpha)  ](../profile/api/computed-attributes.md) - Découvrez les cas d&#39;utilisation des attributs calculés ainsi que comment configurer, accéder, mettre à jour et supprimer un attribut calculé.
- [Projections](../profile/api/edge-projections.md)  Edge - Découvrez comment créer, vue, mettre à jour, supprimer et liste des destinations de projection. De plus, ce document contient des informations sur l&#39;inscription et la création de configurations de projection et fournit des exemples d&#39;utilisation des sélecteurs.
- [Entités (accès au Profil)](../profile/api/entities.md)  - Apprenez à accéder aux données du profil par identité ou liste d&#39;identités. En outre, apprenez à accéder à des événements de séries chronologiques pour plusieurs profils à l’aide d’identités, d’un seul profil par identité et d’un accès à plusieurs entités de schéma.
- [Tâches d’exportation (exportation de Profil)](../profile/api/export-jobs.md)  - Découvrez comment créer, vue, surveiller et annuler des tâches d’exportation.
- [Fusionner les stratégies](../profile/api/merge-policies.md)  - Découvrez les composants des stratégies de fusion ainsi que comment accéder, créer, mettre à jour et supprimer une stratégie de fusion.
- [Etat de l&#39;échantillon de prévisualisation (prévisualisation de Profil)](../profile/api/preview-sample-status.md)  - Découvrez comment vue votre dernier état d&#39;échantillon, la distribution des profils de liste par jeu de données et la distribution des profils de liste par espace de nommage.
- [Tâches du système de profil (supprimer des requêtes)](../profile/api/profile-system-jobs.md)  - Découvrez comment vue, créer et supprimer une requête de suppression pour un jeu de données ou un lot dans le magasin de Profils.

Pour en savoir plus et obtenir les valeurs requises pour effectuer des opérations CRUD avec l’API Profil client en temps réel, consultez le [guide de prise en main](../profile/api/getting-started.md).

## Activez un schéma pour les services [!DNL Profile] et [!DNL Identity]

Avant que les données puissent être ingérées dans Adobe Experience Platform et utilisées dans la création de [!DNL Real-time Customer Profiles], un schéma doit être créé pour fournir la structure des données qui seront ingérées et ce schéma doit être activé pour être utilisé dans [!DNL Profile] et Adobe Experience Platform [!DNL Identity Service].

**Ce guide vous aidera à :**
- Parcourir les schémas existants.
- Création et attribution d’un nom à un schéma.
- Ajoutez et définissez des mixins XDM.
- Définissez vos champs de schéma comme champs d’identité.
- Activez le Profil pour votre schéma.

Pour obtenir des instructions détaillées sur la création d&#39;un schéma activé à la fois pour [!DNL Profile] et [!DNL Identity Service], consultez les didacticiels pour [créer un schéma à l&#39;aide de l&#39;API de registre de Schéma](../xdm/tutorials/create-schema-api.md) ou [créer un schéma à l&#39;aide de l&#39;interface utilisateur de Schéma Builder](../xdm/tutorials/create-schema-ui.md).

## Configurez un jeu de données pour [!DNL Profile] et [!DNL Identity]

Pour commencer à ingérer des données dans [!DNL Profile], vous devez disposer d&#39;un jeu de données correctement configuré pour être utilisé avec [!DNL Real-time Customer Profile] et [!DNL Identity Service].

**Ce guide vous aidera à :**
- Créez un jeu de données activé pour le Profil.
- Configurez des jeux de données existants.
- Ingestion de données dans le jeu de données.
- Vérifiez que le jeu de données est activé par Profil et que vous utilisez Identity Service.

Pour commencer, suivez le didacticiel de l&#39;API pour [configurer un jeu de données pour le Profil et l&#39;identité](../profile/tutorials/dataset-configuration.md).

## Configuration des stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lorsque ces données sont regroupées, les stratégies de fusion sont les règles que [!DNL Platform] utilise pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer cette vue unifiée.

**Ce guide vous aidera à :**
- Créez de nouvelles stratégies de fusion.
- Gérer les stratégies de fusion existantes.
- Définissez une stratégie de fusion par défaut pour votre organisation.
- Comprendre les violations de stratégie de fusion.

Pour utiliser les stratégies de fusion dans l&#39;interface utilisateur [!DNL Platform], consultez le [guide de l&#39;utilisateur des stratégies de fusion](../profile/ui/merge-policies.md). Pour utiliser des stratégies de fusion à l’aide de l’API Real-time Customer Profile, consultez le [guide de développement sur les stratégies de fusion](../profile/api/merge-policies.md).

## Configuration des projections de périphérie

Afin d’offrir à vos clients des expériences coordonnées, cohérentes et personnalisées sur plusieurs canaux en temps réel, les bonnes données doivent être facilement disponibles et mises à jour en continu, au fur et à mesure des changements. L&#39;Adobe [!DNL Experience Platform] permet cet accès en temps réel aux données grâce à l&#39;utilisation de ce que l&#39;on appelle les contours. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie.

**Ce guide vous aidera à :**
- Liste, création, vue, mise à jour et suppression d&#39;une destination de projection de bord.
- Liste et créer une configuration de projection de bord.
- Comprendre les sélecteurs.

Pour plus d&#39;informations et pour commencer à travailler avec les arêtes, consultez le [!DNL Real-time Customer Profile] sous-guide de l&#39;API [sur les projections des arêtes](../profile/api/edge-projections.md).

## Personnalisation de l’affichage des données de Profil dans l’interface utilisateur

Dans l’interface utilisateur de l’Experience Platform, vous pouvez vue et interagir avec les données du Profil client en temps réel sous la forme de profils client. Les informations de profil affichées dans l’interface utilisateur ont été fusionnées à partir de plusieurs fragments de profil afin de former une seule vue pour chaque client. Cela inclut des détails tels que les attributs de base, les identités liées et les préférences de canal. Les champs par défaut affichés dans les profils peuvent également être modifiés au niveau de l’organisation pour afficher les attributs de Profil préférés.

**Ce guide vous aidera à :**
- Réorganiser, redimensionner, modifier et supprimer des cartes.
- Ajouter des attributs.
- Ajoutez une nouvelle carte.
- Restaurer les valeurs par défaut.

Pour en savoir plus sur la personnalisation des données de profil, consultez la [documentation sur la personnalisation des Profils](../profile/ui/profile-customization.md).

## Étapes suivantes

Une fois que vous avez configuré [!DNL Real-time Customer Profile] pour votre organisation, vous pouvez commencer à ajouter des données à des profils clients individuels et à créer des segments d&#39;audience en fonction d&#39;attributs de client spécifiques. Pour commencer, consultez les tutoriels suivants :

- [Ajout de données à Real-time Customer Profile](../profile/tutorials/add-profile-data.md)
- [Création d’un segment](../segmentation/tutorials/create-a-segment.md)