---
keywords: Experience Platform ; accueil ; rubriques populaires ; Profil client en temps réel ; Service d'identité ;
solution: Experience Platform
title: Tutoriels sur Real-time Customer Profile
topic-legacy: tutorial
type: Tutorial
description: Ce document décrit les étapes à suivre et fournit des liens vers des tutoriels pour effectuer chaque workflow séparément.
exl-id: cda6e7a7-9498-454c-94df-c6271a5a4fd4
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 25%

---

# Configuration [!DNL Real-time Customer Profile]

Pour configurer [!DNL Real-time Customer Profile] pour votre organisation, vous devez exécuter plusieurs workflows distincts. Ce document décrit les étapes à suivre et fournit des liens vers des tutoriels pour effectuer chaque workflow séparément.

Pour en savoir plus sur [!DNL Real-time Customer Profile], lisez tout d&#39;abord [Profil overview](../profile/home.md).

## Présentation de l’interface utilisateur du Profil client en temps réel

Real-time Customer Profile offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces.

**Ce guide vous aidera à :**
- Comprenez l&#39;interface utilisateur [!UICONTROL Profils] et les fonctionnalités disponibles.
- Vue et gestion des données de Profil.

Pour en savoir plus, consultez le [Guide de l’utilisateur du Profil client en temps réel](../profile/ui/user-guide.md).

## API Real-time Customer Profile

L’API Profil client en temps réel comprend plusieurs points de terminaison. Pour plus d&#39;informations sur chacun des points de terminaison disponibles et leurs cas d&#39;utilisation, consultez la [Présentation de l&#39;API Profil client en temps réel](../profile/api/overview.md).

Pour en savoir plus et obtenir les valeurs requises pour effectuer des opérations CRUD avec l’API Profil client en temps réel, consultez le [guide de prise en main](../profile/api/getting-started.md).

## Activez un schéma pour les services [!DNL Profile] et [!DNL Identity]

Avant que les données puissent être ingérées dans Adobe Experience Platform et utilisées dans la création de [!DNL Real-time Customer Profiles], un schéma doit être créé pour fournir la structure des données qui seront ingérées et ce schéma doit être activé pour être utilisé dans [!DNL Profile] et Adobe Experience Platform [!DNL Identity Service].

**Ce guide vous aidera à :**
- Parcourir les schémas existants.
- Création et attribution d’un nom à un schéma.
- Ajoutez et définissez des groupes de champs de schéma XDM.
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

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs canaux en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en continu au fur et à mesure des changements. L&#39;Adobe [!DNL Experience Platform] permet cet accès en temps réel aux données grâce à l&#39;utilisation de ce que l&#39;on appelle les contours. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie.

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
