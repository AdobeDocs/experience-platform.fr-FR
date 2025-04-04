---
keywords: Experience Platform;accueil;rubriques populaires;identité;Identité;graphiques XDM;service d’identités;Service d’identités
solution: Experience Platform
title: Présentation du service d’identités
description: Le service d’identités d’Adobe Experience Platform vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 8%

---

# Service d’identités d’Adobe Experience Platform

Pour offrir des expériences digitales pertinentes, vous avez besoin d’une représentation complète et précise des entités du monde réel qui constituent votre base de clients.

Les organisations et les entreprises font face aujourd’hui à un grand volume de jeux de données disparates : vos clients individuels sont représentés par divers identifiants différents. Votre client peut être lié à différents navigateurs web (Safari, Google Chrome), appareils (téléphones, ordinateurs portables) et autres identifiants de personne (CRMID, comptes de messagerie électronique). Cela crée une vue incohérente de votre client.

Vous pouvez résoudre ces problèmes grâce au service d’identités de Adobe Experience Platform et à ses fonctionnalités pour :

* Générez un **graphique d’identités** qui relie les identités disparates entre elles, vous donnant ainsi une représentation visuelle de la façon dont un client interagit avec votre marque sur différents canaux.
* Créez un graphique pour le profil client en temps réel, qui est ensuite utilisé pour créer une vue d’ensemble complète du client en fusionnant les attributs et les comportements.
* Effectuez la validation et le débogage à l’aide des différents outils.

Ce document présente Identity Service et explique comment vous pouvez utiliser ses fonctionnalités dans le cadre d’Experience Platform.

## Terminologie {#terminology}

Avant de rentrer dans les détails d’Identity Service, lisez le tableau suivant pour obtenir un résumé des termes clés :

| Terme | Définition |
| --- | --- |
| Identité | Une identité correspond à des données propres à une entité. En règle générale, il s’agit d’un objet du monde réel, tel qu’une personne individuelle, un appareil matériel ou un navigateur web (représenté par un cookie). Une identité complète se compose de deux éléments : un **espace de noms d’identité** et une **valeur d’identité**. |
| Espace de noms d’identité | Un espace de noms d’identité est le contexte d’une identité donnée. Par exemple, un espace de noms de `Email` peut correspondre à la valeur d’identité : **julien<span>@acme.com**. De même, un espace de noms de `Phone` peut correspondre à la valeur d’identité : `555-555-1234`. Pour plus d’informations, consultez la présentation des espaces de noms d’identité [identity](./features/namespaces.md). |
| Valeur de l’identité | Une valeur d’identité est une chaîne qui représente une entité du monde réel et est classée dans Identity Service par le biais d’un espace de noms. Par exemple, la valeur d’identité (chaîne) **julien<span>@acme.com** peut être classée comme espace de noms `Email`. |
| Type d’identité | Un type d’identité est un composant d’un espace de noms d’identité. Le type d’identité indique si les données d’identité sont liées ou non dans un graphique d’identités. |
| Lien | Un lien ou une liaison est une méthode permettant d’établir que deux identités disparates représentent la même entité. Par exemple, un lien entre « `Email` = julien<span>@acme.com » et « `Phone` = 555-555-1234 » signifie que les deux identités représentent la même entité. Cela suggère que le client qui a interagi avec votre marque avec l’adresse e-mail de julien<span>@acme.com et le numéro de téléphone 555-555-1234 est le même. |
| Service d’identités | Identity Service est un service d’Experience Platform qui lie (ou annule) les identités afin de gérer les graphiques d’identités. |
| Graphique d’identités | Le graphique d’identités est un ensemble d’identités qui représente un seul client. Pour plus d’informations, consultez le guide sur [l’utilisation de la visionneuse de graphiques d’identités](./features/identity-graph-viewer.md). |
| Profil client en temps réel | Le profil client en temps réel est un service de Adobe Experience Platform qui : <ul><li>Fusionne les fragments de profils pour créer un profil, en fonction d’un graphique d’identités.</li><li>Segmente les profils afin qu’ils puissent être envoyés à destination pour les activations.</li></ul> |
| Profile | Un profil est la représentation d’un sujet, d’une organisation ou d’un individu. Un profil se compose de quatre éléments : <ul><li>Attributs : les attributs fournissent des informations telles que le nom, l’âge ou le sexe.</li><li>Comportement : les comportements fournissent des informations sur les activités d’un profil donné. Par exemple, un comportement de profil peut indiquer si un profil donné « recherche des sandales » ou « commande de t-shirts ».</li><li>Identités : pour un profil fusionné, cette section fournit des informations sur toutes les identités associées à la personne. Les identités peuvent être classées en trois catégories : personne (CRMID, e-mail, téléphone), appareil (IDFA, GAID) et cookie (ECID, AAID).</li><li>Appartenance à une audience : groupes auxquels appartient le profil (utilisateurs fidèles, utilisateurs qui vivent en Californie, etc.)</li></ul> |

{style="table-layout:auto"}

## Qu’est-ce qu’Identity Service ?

![Combinaison d’identités dans Experience Platform](./images/identity-service-stitching.png)

Dans un contexte B2C (business-to-customer), les clients interagissent avec votre entreprise et établissent une relation avec votre marque. Un client type peut être actif dans un certain nombre de systèmes au sein de l’infrastructure de données de votre entreprise. Un client donné peut être actif dans vos systèmes d’e-commerce, de fidélité et de service d’assistance. Ce même client peut également interagir de manière anonyme ou par des moyens authentifiés sur un certain nombre d’appareils différents.

Tenez compte du parcours client suivant :

* Julien a créé un compte sur votre site d’e-commerce et a commandé certains articles par le passé. Julien utilise généralement son ordinateur portable personnel pour faire des achats et se connecte à son compte à chaque moment d’utilisation.
* Cependant, lors d’une de ses visites sur votre site, elle utilise une tablette pour rechercher des sandales. Au cours de cette session, comme elle utilisait un autre appareil, elle ne se connecte pas et ne passe pas de commande.
* À ce stade, les activités de Julien sont représentées dans deux profils distincts :
   * Son premier profil est son identifiant de connexion e-commerce. Ce profil est utilisé lorsqu’elle utilise un nom d’utilisateur et un mot de passe pour authentifier sa session sur votre site d’e-commerce. Ce profil est identifié par un identifiant sur l’ensemble des appareils.
   * Son deuxième profil est sa tablette. Ce profil a été créé après qu’elle ait navigué anonymement sur votre site d’e-commerce à l’aide d’une tablette sans se connecter à son compte. Ce profil est identifié par un identifiant de cookie.
* Plus tard, Julien reprend sa session sur tablette. Cependant, cette fois, elle se connecte à son compte. Par conséquent, le service d’identités associe désormais l’activité Tablet PC de Julien à son identifiant de connexion d’e-commerce.
* À l’avenir, votre contenu ciblé pourra refléter le profil complet de Julien, son historique d’achats et son activité de navigation anonyme.

>[!IMPORTANT]
>
>Vous pouvez utiliser Identity Service pour lier des identités et dresser le portrait complet de votre client qui pourrait autrement être éparpillé sur différents systèmes.

## Que fait Identity Service ?

Identity Service fournit les opérations suivantes pour accomplir sa mission :

* Créez des espaces de noms personnalisés adaptés aux besoins de votre entreprise.
* Créer, mettre à jour et afficher des graphiques d’identités.
* Supprimer les identités en fonction des jeux de données.
* Supprimez les identités pour garantir la conformité réglementaire.

## Liaison des identités par Identity Service

Un lien entre deux identités est établi lorsque l’espace de noms d’identité et les valeurs d’identité correspondent.

Un événement de connexion type **envoie deux identités** dans Experience Platform :

* Identifiant de personne (par exemple CRMID) qui représente un utilisateur authentifié.
* Identifiant du navigateur (par exemple, ECID) qui représente le navigateur web.

Examinez lʼexemple suivant :

* Connectez-vous avec votre nom d&#39;utilisateur et votre mot de passe à un site de commerce électronique à l&#39;aide de votre ordinateur portable. Cet événement vous qualifie en tant qu’utilisateur authentifié, de sorte que le service d’identités reconnaît votre CRMID.
* Votre utilisation d’un navigateur pour accéder au site Web d’e-commerce est également reconnue par le service d’identités comme un événement. Cet événement est représenté dans Identity Service par le biais d’un ECID.
* En coulisse, Identity Service traite les deux événements comme suit : `CRM_ID:ABC, ECID:123`.
   * CRMID : ABC est l’espace de noms et la valeur qui vous représente, en tant qu’utilisateur authentifié.
   * ECID : 123 est l’espace de noms et la valeur qui représentent l’utilisation de votre navigateur web sur votre ordinateur portable.
* Ensuite, si vous vous connectez avec les mêmes informations d’identification au même site web d’e-commerce, mais que vous utilisez le navigateur web sur votre téléphone au lieu du navigateur web sur votre ordinateur portable, un nouvel ECID est enregistré dans Identity Service.
* En arrière-plan, Identity Service traite ce nouvel événement en tant que `{CRM_ID:ABC, ECID:456}`, où CRM_ID : ABC représente votre ID client authentifié et ECID : 456 représente le navigateur web sur votre appareil mobile.

Compte tenu des scénarios ci-dessus, Identity Service établit un lien entre `{CRM_ID:ABC, ECID:123}` et `{CRM_ID:ABC, ECID:456}`. Vous obtenez un graphique d’identités dans lequel vous « possédez » trois identités : une pour l’identifiant de personne (CRMID) et deux pour les identifiants de cookie (ECID).

Pour plus d’informations, consultez le guide sur la [façon dont Identity Service lie les identités](./features/identity-linking-logic.md).

## Graphiques d’identités

Un graphique d’identités est une carte des relations entre différents espaces de noms d’identité, ce qui vous permet de visualiser et de mieux comprendre les identités de client qui sont regroupées, ainsi que la manière dont elles sont regroupées. Pour plus d’informations, consultez le tutoriel sur [l’utilisation de la visionneuse de graphiques d’identités](./features/identity-graph-viewer.md).

La vidéo suivante est destinée à étayer votre compréhension des identités et des graphiques dʼidentité.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Comprendre le rôle d’Identity Service dans l’infrastructure Experience Platform

Identity Service joue un rôle essentiel dans Experience Platform. Voici quelques-unes de ces intégrations clés :

* [Schémas](../xdm/home.md) : dans un schéma donné, les champs de schéma marqués comme identités permettent de créer des graphiques d’identités.
* [Jeux de données](../catalog/datasets/overview.md) : lorsqu’un jeu de données est activé pour l’ingestion dans le profil client en temps réel, des graphiques d’identités sont générés à partir du jeu de données, étant donné que le jeu de données comporte au moins deux champs marqués comme identité.
* [Web SDK](../web-sdk/home.md) : Web SDK envoie des événements d’expérience à Adobe Experience Platform et Identity Service génère un graphique lorsqu’il existe plusieurs identités dans l’événement.
* [Real-Time Customer Profile](../profile/home.md) : avant la fusion des attributs et des événements d’un profil donné, le profil client en temps réel peut référencer le graphique d’identité. Pour plus d’informations, consultez le guide sur la [compréhension de la relation entre Identity Service et le profil client en temps réel](./identity-and-profile.md).
* [Destinations](../destinations/home.md) : les destinations peuvent envoyer des informations de profil à d’autres systèmes en fonction d’un espace de noms d’identité, tel qu’un e-mail haché.
* [Correspondance de segments](../segmentation/ui/segment-match/overview.md) : la correspondance de segments correspond à deux profils dans deux sandbox différents qui ont le même espace de noms d’identité et la même valeur d’identité.
* [Privacy Service](../privacy-service/home.md) : si la demande de suppression comprend `identity`, la combinaison espace de noms et valeur d’identité spécifiée peut être supprimée d’Identity Service à l’aide de la fonctionnalité de traitement des demandes d’accès à des informations personnelles de Privacy Service.

