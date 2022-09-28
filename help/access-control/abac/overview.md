---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;
title: Présentation du contrôle d’accès basé sur les attributs
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs dans Adobe Experience Platform.
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: b095461b0c2510e84ca9a3a368f4907f8b3d5370
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 34%

---

# Contrôle d’accès basé sur les attributs - Aperçu

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible pour un nombre restreint d’utilisateurs, qui sont actifs dans le secteur de la santé et basés aux États-Unis. Cette fonctionnalité sera disponible pour tous les clients Real-time Customer Data Platform dès son déploiement à grande échelle.

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des stratégies d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

Cette fonctionnalité vous permet d’étiqueter les champs de schéma du modèle de données d’expérience (XDM) avec des libellés qui définissent les portées d’utilisation des données ou de l’organisation. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des stratégies d’accès autour des champs de schéma XDM et mieux gérer l’accès attribué aux utilisateurs ou groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Enfin, le contrôle d’accès basé sur les attributs permet aux administrateurs de gérer l’accès à des segments spécifiques.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD), aux informations d’identification personnelle (PII) et au type de données personnalisé dans tous les workflows et ressources Platform. Les administrateurs peuvent définir des rôles d’utilisateur qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

## Terminologie du contrôle d’accès en fonction des attributs

Le contrôle d’accès basé sur les attributs implique les composants suivants :

| Terminologie | Définition |
| --- | --- |
| Attributs | Les attributs sont les identifiants qui indiquent la corrélation entre un utilisateur et les ressources Platform auxquelles il a accès. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des stratégies d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs. |
| Libellés | Les libellés vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans  Platform, ou dès que les données sont disponibles pour une utilisation dans Platform. |
| Autorisations | Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités  Platform, telles que la création d’environnements de test, la définition de schémas et la gestion des jeux de données. |
| Jeux d’autorisations | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| Stratégies | Les politiques sont des déclarations qui réunissent des attributs pour établir des actions permises et non admissibles. Les stratégies peuvent être locales ou globales et peuvent remplacer d’autres stratégies. |
| Ressource | Une ressource est la ressource ou l’objet auquel un sujet peut ou ne peut pas accéder. Les ressources peuvent être des segments ou des champs de schéma. |
| Rôles | Les rôles sont des moyens de catégoriser les types d’utilisateurs qui interagissent avec votre instance Platform et sont des blocs élémentaires des stratégies de contrôle d’accès. Dans un environnement de contrôle d’accès basé sur les rôles, la configuration de l’accès des utilisateurs est regroupée par le biais de responsabilités et de besoins communs. Un rôle possède un ensemble donné d’autorisations et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin. |
| Objet | Un objet est l’utilisateur qui demande l’accès à une ressource pour effectuer une action. |
| Groupes d’utilisateurs | Les groupes d’utilisateurs sont plusieurs utilisateurs qui ont été regroupés et qui ont l’accès pour exécuter les mêmes fonctions. |

## Autorisations

>[!IMPORTANT]
>
>Une fois que votre organisation a activé le contrôle d’accès basé sur les attributs, vous pouvez commencer à utiliser les autorisations sur Adobe Experience Cloud, au lieu des profils de produit dans Adobe Admin Console, pour gérer les autorisations des utilisateurs, fonctionnalités, libellés et autres ressources de votre organisation.

La zone dédiée aux autorisations dans Experience Cloud permet aux administrateurs de définir des rôles d’utilisateur et des stratégies d’accès. Ils peuvent ainsi gérer les autorisations d’accès aux fonctionnalités et objets dans une application de produit.

Grâce aux autorisations, vous pouvez créer et gérer des rôles, ainsi qu’attribuer les autorisations de ressource souhaitées pour ces rôles. Les autorisations vous permettent également de gérer les libellés, les sandbox et les utilisateurs associés à un rôle spécifique. Pour plus d’informations, voir [Guide des autorisations](ui/browse.md).

## API de contrôle d’accès basé sur les attributs

L’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les rôles, les stratégies et les produits dans Platform à l’aide des API. Pour plus d’informations, consultez le guide sur [utilisation de l’API pour gérer les configurations de contrôle d’accès basées sur des attributs](api/overview.md).

## Contrôle d’accès basé sur les attributs dans Adobe Experience Platform

Les sections suivantes fournissent des informations sur la manière dont le contrôle d’accès basé sur les attributs est intégré à d’autres composants de Platform :

### Contrôle d&#39;accès

 Platform exploite les profils de produit [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des environnements de test. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités de Platform, notamment la modélisation des données, la gestion des profils et l’administration des environnements de test. Une fois que votre organisation a activé le contrôle d’accès basé sur les attributs, vous pouvez commencer à utiliser les autorisations sur Adobe Experience Cloud, au lieu des profils de produit dans Adobe Admin Console, pour gérer les autorisations des utilisateurs, fonctionnalités, libellés et autres ressources de votre organisation.

Pour plus d’informations sur le contrôle d’accès, voir [présentation du contrôle d’accès](../home.md).

### Destinations {#destinations}

[!DNL Destinations] sont des intégrations prédéfinies avec des plateformes de destination qui permettent l’activation transparente des données de Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

En tant qu’administrateur, vous pouvez utiliser des fonctionnalités de contrôle d’accès basées sur des attributs pour :

* Configurez l’accès des utilisateurs pour afficher des segments spécifiques dans le processus d’activation, en fonction du rôle, des autorisations et des libellés.
   * Dans le processus d’activation, les utilisateurs peuvent être tenus de sélectionner les segments qu’ils souhaitent activer vers une destination. En tant qu’administrateur, vous pouvez configurer les utilisateurs de votre entreprise pour qu’ils n’affichent que les segments étiquetés avec des étiquettes auxquelles les utilisateurs ont accès et les segments qui ne contiennent pas d’étiquettes.
* Configurez l’accès des utilisateurs pour afficher des champs spécifiques dans le processus d’activation, en fonction du rôle, des autorisations et des libellés.
   * Dans le processus d’activation, les utilisateurs peuvent être tenus de sélectionner les champs qu’ils souhaitent activer vers une destination. En tant qu’administrateur, vous pouvez configurer les utilisateurs de votre entreprise pour qu’ils n’affichent que les champs étiquetés avec des libellés auxquels les utilisateurs ont accès et les champs qui ne contiennent aucun libellé.

>[!IMPORTANT]
>
>En résumé, gardez à l’esprit les implications suivantes lorsque vous utilisez des destinations et un contrôle d’accès basé sur les attributs :
>
>* Vous ne pouvez activer que les segments que vous êtes autorisé à accéder et à afficher dans le [vue de navigation dans les segments](/help/segmentation/ui/overview.md#browse) et [étape sélection d’un segment](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) du workflow d’activation.
>* Dans le [étape de mappage du workflow d’activation](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), vous pouvez uniquement afficher et sélectionner pour activation les champs auxquels vous avez accès.
>* Lorsque vous souhaitez activer des segments supplémentaires vers une destination existante où vous n’avez pas accès à tous les champs mappés à l’exportation, le workflow d’activation est bloqué pour vous.


Pour plus d’informations sur [!DNL Destinations], reportez-vous à la section [[!DNL Destinations] aperçu](../../destinations/home.md).

### Service d’identités

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

Dans le cadre du contrôle d’accès basé sur les attributs, la variable `view-identity-graph` L’autorisation vous permet de déterminer quels utilisateurs de votre entreprise peuvent accéder au graphique d’identités par le biais de l’interface utilisateur ou des API. Pour plus d’informations, consultez le guide sur [utilisation de la visionneuse de graphiques d’identités](../../identity-service/ui/identity-graph-viewer.md).

Pour plus d’informations sur [!DNL Identity Service], reportez-vous à la section [[!DNL Identity Service] aperçu](../../identity-service/home.md).

### Profil client en temps réel

 Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Real-time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

En tant qu’administrateur, vous pouvez utiliser des fonctionnalités de contrôle d’accès basées sur des attributs pour :

* Configurez l’accès des utilisateurs à des attributs de profil spécifiques en fonction du rôle, des autorisations et des libellés.
   * En tant qu’administrateur, vous pouvez configurer les utilisateurs de votre entreprise pour qu’ils ne voient que les attributs de profil étiquetés avec des étiquettes auxquelles les utilisateurs ont accès et les attributs de profil qui ne contiennent pas de libellé.
   * En tant qu’administrateur, vous pouvez configurer les utilisateurs de votre entreprise pour qu’ils ne voient que les attributs de profil étiquetés avec des étiquettes auxquelles les utilisateurs ont accès lors de la création de segments ;
* Configurez l’accès de l’utilisateur à l’aperçu des données en étiquetant les champs de données spécifiques utilisés dans le schéma XDM du modèle de données.

Pour plus d’informations sur Profile, reportez-vous à la section [Présentation des profils](../../profile/home.md).

### Segmentation Service

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

En tant qu’administrateur, vous pouvez utiliser des fonctionnalités de contrôle d’accès basées sur des attributs pour :

* Configurez l’accès des utilisateurs pour afficher et gérer des segments spécifiques, en fonction du rôle, des autorisations et des étiquettes ;
   * En tant qu’administrateur, vous pouvez configurer les utilisateurs de votre entreprise pour qu’ils n’affichent que les segments étiquetés avec des étiquettes auxquelles les utilisateurs ont accès et les segments qui ne contiennent aucun libellé, lors de l’utilisation de l’interface utilisateur Segmentation .

Pour plus d’informations sur [!DNL Segmentation Service], reportez-vous à la section [[!DNL Segmentation Service] aperçu](../../segmentation/home.md).

### XDM

Le modèle de données d’expérience (XDM) est une spécification open source conçue pour améliorer la puissance des expériences digitales. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur  Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

Avec le contrôle d’accès basé sur les attributs, vous pouvez :

* [Application des libellés d’utilisation des données aux groupes et classes de champs](../../xdm/tutorials/labels.md). Cela permet à plusieurs schémas avec les mêmes groupes ou classes de champs d’avoir des champs balisés avec les mêmes attributs, selon les configurations au niveau du groupe de champs ou de la classe ;
* Configurez l’accès des utilisateurs à des champs de schéma XDM spécifiques en fonction des jeux d’autorisations appliqués aux rôles affectés aux utilisateurs.

Pour plus d’informations sur XDM, reportez-vous à la section [Présentation de XDM](../../xdm/home.md).