---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs;
title: Présentation du contrôle d’accès basé sur les attributs
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs dans Adobe Experience Platform.
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 82%

---

# Présentation du contrôle d’accès basé sur les attributs {#attribute-based-access-control-overview}

>[!CONTEXTUALHELP]
>id="platform_accesscontrol_abac_labelusageaccesspolicy"
>title="Politique d’accès d’utilisation des libellés"
>abstract=""

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des politiques d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

Utilisez cette fonctionnalité pour étiqueter les champs de schéma du modèle de données d’expérience (XDM) avec des libellés qui définissent les portées d’utilisation des données ou de l’organisation. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des politiques d’accès relatives aux champs de schéma XDM. Cela permet ainsi une meilleure gestion des accès accordés aux utilisateurs ou aux groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Enfin, le contrôle d’accès basé sur les attributs permet aux administrateurs de gérer l’accès à des segments spécifiques.

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs ne doit pas être confondu avec les fonctionnalités de gouvernance des données des Experience Platform, qui vous permettent d’utiliser des libellés et des stratégies pour contrôler la manière dont les données sont utilisées dans Platform plutôt que les utilisateurs de votre organisation qui y ont accès. Pour plus d’informations, consultez la [présentation de la gouvernance des données](../../data-governance/home.md) .

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD), aux informations d’identification personnelle (PII) et à d’autres types de données personnalisées sur l’ensemble des workflows et ressources de Platform. Les administrateurs peuvent définir des rôles d’utilisateur qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

La vidéo suivante est destinée à vous aider à comprendre le contrôle d’accès basé sur les attributs et explique comment configurer les rôles, les ressources et les stratégies.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

## Terminologie du contrôle d’accès basé sur les attributs

Le contrôle d’accès basé sur les attributs comprend les composants suivants :

| Terminologie | Définition |
| --- | --- |
| Attributs | Les attributs sont les identifiants indiquant la corrélation entre un utilisateur et les ressources Platform auxquelles il a accès. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des politiques d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs. |
| Libellés | Les libellés vous permettent de classer les jeux de données et les champs en fonction des politiques d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans Platform, ou dès que les données sont disponibles pour une utilisation dans Platform. |
| Autorisations | Les autorisations incluent la possibilité d’afficher ou d’utiliser les fonctionnalités Platform, telles que la création de sandbox, la définition de schémas et la gestion des jeux de données. |
| Jeux d’autorisations | Les jeux d’autorisations représentent un groupe d’autorisations qu’un administrateur peut appliquer à un rôle. Un administrateur peut attribuer des jeux d’autorisations à un rôle au lieu d’affecter des autorisations individuelles. Vous pouvez ainsi créer des rôles personnalisés à partir d’un rôle prédéfini contenant un groupe d’autorisations. |
| Politiques | Les politiques sont des déclarations qui réunissent des attributs pour établir des actions autorisées et non autorisées. Les politiques peuvent être locales ou globales et peuvent remplacer d’autres politiques. |
| Ressource | Une ressource est un actif ou un objet auquel un sujet peut ou ne peut pas accéder. Les ressources peuvent être des segments ou des champs de schéma. |
| Rôles | Les rôles sont des moyens de classer les types d’utilisateurs qui interagissent avec votre instance Platform et constituent des blocs élémentaires des politiques de contrôle d’accès. Dans un environnement de contrôle d’accès basé sur les rôles, la configuration de l’accès des utilisateurs est regroupée suivant les responsabilités et les besoins communs. Un rôle possède un jeu d’autorisations déterminé et les membres de votre organisation peuvent être affectés à un ou plusieurs rôles, selon la portée de l’accès en lecture ou en écriture dont ils ont besoin. |
| Objet | Un sujet est un utilisateur qui demande l’accès à une ressource pour effectuer une action. |
| Groupes d’utilisateurs | Les groupes d’utilisateurs consistent en plusieurs utilisateurs qui ont été regroupés et qui disposent des accès pour exécuter les mêmes fonctions. |

## Autorisations

>[!IMPORTANT]
>
>Une fois que votre organisation est activée pour le contrôle d’accès basé sur les attributs, vous pouvez commencer à utiliser les autorisations sur Adobe Experience Cloud, au lieu des rôles dans Adobe Admin Console, pour gérer les autorisations pour les utilisateurs, les fonctionnalités, les étiquettes et d’autres ressources de votre organisation.

La zone dédiée aux autorisations dans Experience Cloud permet aux administrateurs de définir des rôles d’utilisateur et des politiques d’accès. Ils peuvent ainsi gérer les autorisations d’accès aux fonctionnalités et objets dans une application de produit.

Grâce aux autorisations, vous pouvez créer et gérer des rôles, ainsi qu’attribuer les autorisations de ressource souhaitées pour ces rôles. Les autorisations vous permettent également de gérer les libellés, les sandbox et les utilisateurs associés à un rôle spécifique. Pour plus d’informations, consultez le [Guide des autorisations](ui/browse.md).

## API de contrôle d’accès basé sur les attributs

L’API de contrôle d’accès basé sur les attributs vous permet de gérer par programmation les rôles, les politiques et les produits dans Platform. Pour plus d’informations, consultez le guide sur l’[utilisation de l’API pour gérer les configurations de contrôle d’accès basé sur des attributs](api/overview.md).

## Contrôle d’accès basé sur les attributs dans Adobe Experience Platform

Les sections suivantes fournissent des informations sur la manière dont le contrôle d’accès basé sur les attributs est intégré à d’autres composants de Platform :

### Contrôle d’accès

Platform exploite les rôles [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des environnements de test. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités de Platform, notamment la modélisation des données, la gestion des profils et l’administration des sandbox. Une fois que votre organisation est activée pour le contrôle d’accès basé sur les attributs, vous pouvez commencer à utiliser les autorisations sur Adobe Experience Cloud, au lieu des rôles dans Adobe Admin Console, pour gérer les autorisations pour les utilisateurs, les fonctionnalités, les étiquettes et d’autres ressources de votre organisation.

La disponibilité du contrôle d’accès basé sur les attributs est limitée pour les clients qui achètent des offres Healthcare et/ou Privacy Shield. Cette fonctionnalité inclut les éléments suivants :

* Interface des autorisations : permet de définir les rôles utilisateur, les autorisations et les politiques pour le contrôle d’accès basé sur les attributs.

* Étiquetage : ajoutez, modifiez et supprimez des étiquettes pour les rôles utilisateur, les champs de schéma, les segments et d’autres objets pris en charge afin d’exploiter les stratégies de contrôle d’accès. **Remarque :** Tout segment qui utilise un attribut étiqueté doit également être étiqueté si vous souhaitez que les mêmes restrictions d’accès s’y appliquent.

Les workflows d’administration pour toutes les applications Experience Platform exécutées depuis Admin Console sont en cours de basculement vers la nouvelle interface d’autorisations.

>[!IMPORTANT]
>
>Vos rôles sont automatiquement migrés vers l’interface Autorisations lorsque votre organisation est activée. Les rôles en Admin Console resteront inchangés pour l’instant. Veuillez **ne pas** modifier vos rôles une fois votre organisation activée.

Pour plus d’informations sur le contrôle d’accès, consultez la [présentation du contrôle d’accès](../home.md).

### Destinations {#destinations}

[!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent dʼactiver facilement des données provenant de Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

En tant qu’administrateur, vous pouvez utiliser des fonctionnalités de contrôle d’accès basé sur les attributs pour :

* Configurer l’accès des utilisateurs et utilisatrices pour afficher des segments spécifiques dans le processus d’activation, en fonction du rôle, des autorisations et des étiquettes ;
   * Le processus d’activation peut inclure pour les utilisateurs la sélection obligatoire des segments qu’ils souhaitent activer vers une destination. En tant qu’administrateur, vous pouvez configurer les utilisateurs et utilisatrices de votre organisation pour qu’ils voient uniquement les segments ayant des étiquettes auxquelles ils ont accès, et les segments non étiquetés.
* Configurer l’accès des utilisateurs et utilisatrices pour afficher des champs spécifiques dans le processus d’activation, en fonction du rôle, des autorisations et des étiquettes ;
   * Dans le processus d’activation, les utilisateurs et utilisatrices peuvent avoir l’obligation de sélectionner les champs qu’ils souhaitent activer vers une destination. En tant qu’administrateur ou administratrice, vous pouvez configurer les utilisateurs et utilisatrices de votre organisation pour qu’ils ne voient que les champs étiquetés avec des étiquettes auxquelles ils ont accès et les champs ne contenant aucune étiquette.

>[!IMPORTANT]
>
>En résumé, souvenez-vous des implications suivantes quand vous utilisez des destinations et un contrôle d’accès basé sur les attributs :
>
>* Vous pouvez uniquement activer les audiences auxquelles vous êtes autorisé à accéder et à afficher dans [Audience Portal](/help/segmentation/ui/audience-portal.md#browse) et [sélectionner l’étape de segment](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) du workflow d’activation.
>* Dans l’[étape de mappage du processus d’activation](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), vous pouvez uniquement afficher et sélectionner pour activation les champs auxquels vous avez accès.
>* Si vous souhaitez activer des segments supplémentaires vers une destination existante et que vous n’avez pas accès à tous les champs mappés à l’exportation, le workflow d’activation est bloqué pour vous.

Pour plus d’informations sur les [!DNL Destinations], consultez la [[!DNL Destinations] présentation](../../destinations/home.md).

### Service d’identités

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.

Dans le cadre du contrôle d’accès basé sur les attributs, l’autorisation `view-identity-graph` vous permet de déterminer quels utilisateurs et utilisatrices de votre organisation peuvent accéder au graphique d’identité par le biais de l’interface utilisateur ou des API. Pour plus dʼinformations, consultez le guide sur lʼ[utilisation de la visionneuse de graphiques dʼidentité](../../identity-service/features/identity-graph-viewer.md).

Pour plus d’informations sur [!DNL Identity Service], consultez la [[!DNL Identity Service] présentation](../../identity-service/home.md).

### Profil client en temps réel

Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

En tant qu’administrateur, vous pouvez utiliser des fonctionnalités de contrôle d’accès basé sur les attributs pour :

* Configurer l’accès des utilisateurs et utilisatrices avec des attributs de profil spécifiques en fonction du rôle, des autorisations et des étiquettes ;
   * En tant qu’administrateur ou administratrice, vous pouvez configurer les utilisateurs et utilisatrices de votre organisation pour qu’ils voient uniquement les attributs de profil étiquetés avec des étiquettes auxquelles ils ont accès, et les attributs de profil non étiquetés ;
   * En tant qu’administrateur ou administratrice, vous pouvez configurer les utilisateurs et utilisatrices de votre organisation pour qu’ils voient uniquement les attributs de profil étiquetés avec des étiquettes auxquelles ils ont accès lors de la création de segments ;
* Configurer l’accès des utilisateurs et utilisatrices à l’aperçu des données en étiquetant les champs de données spécifiques utilisés dans le schéma XDM du modèle de données.

Pour plus d’informations sur Profil, consultez la [Présentation des profils](../../profile/home.md).

### Segmentation Service

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

En tant qu’administrateur, vous pouvez utiliser des fonctionnalités de contrôle d’accès basé sur les attributs pour :

* Configurer l’accès des utilisateurs et utilisatrices à l’affichage et à la gestion de segments spécifiques, en fonction du rôle, des autorisations et des étiquettes ;
   * En tant qu’administrateur ou administratrice, vous pouvez configurer les utilisateurs et utilisatrices de votre organisation pour qu’ils voient uniquement les attributs de profil étiquetés avec des étiquettes auxquelles ils ont accès et les segments sans aucune étiquette, lors de l’utilisation de l’interface utilisateur Segmentation.

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [[!DNL Segmentation Service] présentation](../../segmentation/home.md).

### XDM

Le modèle de données d’expérience (XDM) est une spécification open source conçue pour améliorer la puissance des expériences digitales. Il fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

Avec le contrôle d’accès basé sur les attributs, vous pouvez :

* [appliquer des étiquettes d’utilisation des données aux groupes et classes de champs](../../xdm/tutorials/labels.md). Cela permet à plusieurs schémas avec les mêmes groupes ou classes de champs d’avoir des champs balisés avec les mêmes attributs, selon les configurations au niveau du groupe de champs ou de la classe ;
* Configurer l’accès des utilisateurs et utilisatrices avec des champs de schéma XDM spécifiques en fonction des jeux d’autorisations appliqués aux rôles affectés aux utilisateurs et utilisatrices.

Pour plus d’informations sur XDM, consultez la [présentation du système XDM](../../xdm/home.md).