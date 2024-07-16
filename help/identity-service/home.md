---
keywords: Experience Platform;accueil;rubriques populaires;identité;Identité;graphiques XDM;service d’identités;Service d’identités
solution: Experience Platform
title: Présentation du service d’identités
description: Le service d’identités d’Adobe Experience Platform vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 8%

---

# Service d’identités d’Adobe Experience Platform

Pour offrir des expériences numériques pertinentes, vous avez besoin d’une représentation complète et exacte des entités du monde réel qui constituent votre base de clients.

Aujourd’hui, les entreprises et les entreprises font face à un grand nombre de jeux de données disparates : leurs clients individuels sont représentés par une variété d’identifiants différents. Votre client peut être lié à différents navigateurs web (Safari, Google Chrome), périphériques matériels (téléphones, ordinateurs portables) et autres identifiants de personne (identifiants CRM, comptes de messagerie électronique). Cela crée une vue disjointe de votre client.

Vous pouvez résoudre ces problèmes avec Adobe Experience Platform Identity Service et ses fonctionnalités pour :

* Générez un **graphique d’identités** qui relie des identités disparates, ce qui vous donne une représentation visuelle de la manière dont un client interagit avec votre marque sur différents canaux.
* Créez un graphique pour Real-time Customer Profile, qui est ensuite utilisé pour créer une vue d’ensemble complète du client en fusionnant les attributs et les comportements.
* Effectuez la validation et le débogage à l’aide des différents outils.

Ce document présente Identity Service et explique comment utiliser ses fonctionnalités dans le contexte d’Experience Platform.

## Terminologie {#terminology}

Avant de vous plonger dans les détails d’Identity Service, veuillez lire le tableau suivant pour obtenir un résumé des termes clés :

| Terme | Définition |
| --- | --- |
| Identité | Une identité est une donnée propre à une entité. En règle générale, il s’agit d’un objet réel, tel qu’une personne, un périphérique matériel ou un navigateur web (représenté par un cookie). Une identité complète se compose de deux éléments : un **espace de noms d’identité** et une **valeur d’identité**. |
| Espace de noms d’identité | Un espace de noms d’identité est le contexte d’une identité donnée. Par exemple, un espace de noms de `Email` peut correspondre à la valeur de l’identité : **julien<span>@acme.com**. De même, un espace de noms de `Phone` peut correspondre à la valeur d’identité : `555-555-1234`. Pour plus d’informations, consultez la [présentation de l’espace de noms d’identité](./features/namespaces.md). |
| Valeur de l’identité | Une valeur d’identité est une chaîne qui représente une entité du monde réel et qui est classée dans Identity Service par le biais d’un espace de noms. Par exemple, la valeur d’identité (chaîne) **julien<span>@acme.com** peut être catégorisée comme un espace de noms `Email`. |
| Type d’identité | Un type d’identité est un composant d’un espace de noms d’identité. Le type d’identité indique si les données d’identité sont liées ou non dans un graphique d’identités. |
| Lien | Un lien ou une liaison est une méthode permettant d’établir que deux identités disparates représentent la même entité. Par exemple, un lien entre &quot;`Email` = julien<span>@acme.com&quot; et &quot;`Phone` = 555-555-1234&quot; signifie que les deux identités représentent la même entité. Cela indique que le client qui a interagi avec votre marque avec l’adresse email de julien<span>@acme.com et le numéro de téléphone de 555-555-1234 est le même. |
| Service d’identités | Identity Service est un service d’Experience Platform qui lie (ou annule les liens) les identités pour gérer les graphiques d’identités. |
| Graphique d’identités | Le graphique d’identités est un ensemble d’identités qui représentent un seul client. Pour plus d’informations, lisez le guide sur [à l’aide de la visionneuse de graphiques d’identités](./features/identity-graph-viewer.md). |
| Profil client en temps réel | Real-Time Customer Profile est un service de Adobe Experience Platform qui : <ul><li>Fusionne des fragments de profil pour créer un profil, sur la base d’un graphique d’identités.</li><li>Segmente les profils afin qu’ils puissent ensuite être envoyés à la destination pour les activations.</li></ul> |
| Profile | Un profil est une représentation d’un sujet, d’une organisation ou d’un individu. Un profil est composé de quatre éléments : <ul><li>Attributs : les attributs fournissent des informations telles que le nom, l’âge ou le sexe.</li><li>Comportement : les comportements fournissent des informations sur les activités d’un profil donné. Par exemple, un comportement de profil peut déterminer si un profil donné &quot;recherchait des sandales&quot; ou &quot;commandait des t-shirts&quot;.</li><li>Identités : pour un profil fusionné, cette option fournit des informations sur toutes les identités associées à la personne. Les identités peuvent être classées en trois catégories : Personne (CRMID, email, téléphone), appareil (IDFA, GAID) et cookie (ECID, AAID).</li><li>Adhésions à l’audience : groupes auxquels le profil appartient (utilisateurs fidèles, utilisateurs résidant en Californie, etc.)</li></ul> |

{style="table-layout:auto"}

## Qu’est-ce qu’Identity Service ?

![Combinaison d’identités sur Platform](./images/identity-service-stitching.png)

Dans un contexte B2C (entre entreprises et clients), les clients interagissent avec votre entreprise et établissent une relation avec votre marque. Un client type peut être actif dans n’importe quel nombre de systèmes au sein de l’infrastructure de données de votre entreprise. Tout client donné peut être actif dans vos systèmes d’e-commerce, de fidélité et de service d’assistance. Ce même client peut également interagir de manière anonyme ou par des moyens authentifiés sur un certain nombre d’appareils différents.

Tenez compte du parcours client suivant :

* Julien a créé un compte sur votre site de commerce électronique et a déjà commandé quelques articles par le passé. Julien utilise généralement son ordinateur portable personnel pour faire ses achats et se connecte à son compte à chaque utilisation.
* Cependant, lors de l’une de ses visites sur votre site, elle utilise une tablette pour rechercher des sandales. Au cours de cette session, puisqu’elle a utilisé un autre appareil, elle ne se connecte pas et ne passe pas de commande.
* A ce stade, les activités de Julien sont représentées dans deux profils distincts :
   * Son premier profil est son identifiant de connexion de commerce électronique. Ce profil est utilisé lorsqu’elle utilise une combinaison de nom d’utilisateur et de mot de passe pour authentifier sa session sur votre site de commerce électronique. Ce profil est identifié par un identifiant multi-appareils.
   * Son deuxième profil est son appareil à tablette. Ce profil a été créé après qu’elle a navigué anonymement sur votre site de commerce électronique en utilisant une tablette sans se connecter à son compte. Ce profil est identifié par un identifiant de cookie.
* Plus tard, Julien reprend sa session de tablette. Cependant, cette fois, elle se connecte à son compte. Par conséquent, Identity Service associe désormais l’activité de tablette de Julien à son identifiant de connexion de commerce électronique.
* À partir de maintenant, votre contenu ciblé peut refléter le profil complet de Julien, l’historique des achats et l’activité de navigation anonyme.

>[!IMPORTANT]
>
>Vous pouvez utiliser Identity Service pour associer des identités et assembler une image complète de votre client, qui pourrait autrement être dispersée sur différents systèmes.

## Que fait Identity Service ?

Identity Service fournit les opérations suivantes pour réaliser sa mission :

* Créez des espaces de noms personnalisés en fonction des besoins de votre entreprise.
* Créez, mettez à jour et affichez des graphiques d’identités.
* Supprimer des identités basées sur des jeux de données.
* Supprimez les identités pour garantir la conformité aux réglementations.

## Comment Identity Service lie les identités

Un lien entre deux identités est établi lorsque l’espace de noms de l’identité et les valeurs d’identité correspondent.

Un événement de connexion type **envoie deux identités** dans l’Experience Platform :

* Identifiant de personne (un identifiant CRM, par exemple) qui représente un utilisateur authentifié.
* Identifiant du navigateur (tel qu’un ECID) qui représente le navigateur web.

Examinez lʼexemple suivant :

* Vous vous connectez avec votre nom d’utilisateur et votre mot de passe à un site web de commerce électronique à l’aide de votre ordinateur portable. Cet événement vous qualifie en tant qu’utilisateur authentifié, de sorte qu’Identity Service reconnaît votre ID de gestion de la relation client.
* L’utilisation d’un navigateur pour accéder au site web de commerce électronique est également reconnue comme un événement par Identity Service. Cet événement est représenté dans Identity Service par le biais d’un ECID.
* En arrière-plan, Identity Service traite les deux événements comme suit : `CRM_ID:ABC, ECID:123`.
   * Identifiant CRM : ABC est l’espace de noms et la valeur qui vous représentent, en tant qu’utilisateur authentifié.
   * ECID : 123 est l’espace de noms et la valeur qui représente l’utilisation de votre navigateur web sur votre ordinateur portable.
* Ensuite, si vous vous connectez avec les mêmes informations d’identification au même site web d’e-commerce, mais que vous utilisez le navigateur web sur votre téléphone au lieu du navigateur web sur votre ordinateur portable, un nouvel ECID est enregistré dans Identity Service.
* En arrière-plan, Identity Service traite ce nouvel événement comme `{CRM_ID:ABC, ECID:456}`, où CRM_ID: ABC représente votre ID client authentifié et ECID:456 représente le navigateur web sur votre appareil mobile.

Dans les scénarios ci-dessus, Identity Service établit un lien entre `{CRM_ID:ABC, ECID:123}` et `{CRM_ID:ABC, ECID:456}`. Cela génère un graphique d’identités dans lequel vous &quot;possédez&quot; trois identités : une pour l’identifiant de personne (ID CRM) et deux pour les identifiants de cookie (ECID).

Pour plus d’informations, consultez le guide sur la [façon dont Identity Service lie les identités](./features/identity-linking-logic.md).

## Graphiques d’identités

Un graphique d’identités est une carte des relations entre différents espaces de noms d’identité, ce qui vous permet de visualiser et de mieux comprendre les identités de client qui sont regroupées, ainsi que la manière dont elles sont regroupées. Pour plus d’informations, lisez le tutoriel sur [à l’aide de la visionneuse de graphiques d’identités](./features/identity-graph-viewer.md) .

La vidéo suivante est destinée à étayer votre compréhension des identités et des graphiques dʼidentité.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Comprendre le rôle d’Identity Service dans l’infrastructure Experience Platform

Identity Service joue un rôle essentiel dans Experience Platform. Voici quelques-unes de ces intégrations clés :

* [Schémas](../xdm/home.md) : dans un schéma donné, les champs de schéma marqués comme identité permettent de créer des graphiques d’identité.
* [Jeux de données](../catalog/datasets/overview.md) : lorsqu’un jeu de données est activé pour ingestion dans Real-Time Customer Profile, des graphiques d’identité sont générés à partir du jeu de données, étant donné que le jeu de données comporte au moins deux champs marqués comme identité.
* [SDK Web](../web-sdk/home.md) : le SDK Web envoie des événements d’expérience à Adobe Experience Platform et Identity Service génère un graphique lorsque plusieurs identités existent dans l’événement.
* [ Profil client en temps réel ](../profile/home.md) : avant la fusion des attributs et événements d’un profil donné, Real-Time Customer Profile peut référencer le graphique d’identités. Pour plus d’informations, consultez le guide sur [la compréhension de la relation entre Identity Service et Real-Time Customer Profile](./identity-and-profile.md).
* [Destinations](../destinations/home.md) : les destinations peuvent envoyer des informations de profil à d’autres systèmes en fonction d’un espace de noms d’identité, comme un courrier électronique haché.
* [Correspondance de segment](../segmentation/ui/segment-match/overview.md) : la correspondance de segment correspond à deux profils sur deux environnements de test différents ayant le même espace de noms d’identité et la même valeur d’identité.
* [Privacy Service](../privacy-service/home.md) : si la demande de suppression comprend `identity`, la combinaison d’espace de noms et de valeur d’identité spécifiée peut être supprimée d’Identity Service à l’aide de la fonctionnalité de traitement des demandes d’accès à des informations personnelles de Privacy Service.

