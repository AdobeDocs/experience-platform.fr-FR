---
title: Guide de dépannage des balises
description: Obtenez des réponses aux questions les plus fréquentes à propos des balises dans Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 9701a14dc2915e0d6dcc6051c15d5113f305487f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 89%

---

# Guide de dépannage des balises

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](./term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Ce document apporte des réponses aux questions fréquentes à propos des balises dans Adobe Experience Platform.

## Que sont les balises ?

Les balises représentent la nouvelle génération des fonctionnalités de gestion des balises fournies par Adobe, intégrées à Adobe Experience Platform. Les balises permettent aux clients de :

- déployer des produits web côté client grâce à des intégrations appelées *extensions*
- fournir dynamiquement la configuration pour mettre à jour les implémentations des clients dans les applications mobiles natives
- collecter, définir, gérer et partager des données de façon constante entre les produits marketing et publicitaires d’autres fournisseurs et d’Adobe.

Les balises sont un système de diffusion de code et de configuration avancé qui évalue les conditions et exécute des actions pour déployer les bibliothèques et produits côté client de façon efficace. Il s’agit d’une solution qui offre également une approche hautement évolutive de la gestion et de la création des intégrations et disposant d’un ensemble robuste d’API pour l’interaction programmatique.

## Combien coûtent les balises ?

Les balises n’entraînent aucuns frais supplémentaires. C&#39;est un service disponible pour tous les clients [!DNL Adobe Experience Cloud].

## J’ai appris qu’il existe désormais des modules externes. De quoi s’agit-il ?

Les balises sont intégrées à Adobe Experience Platform et sont entièrement extensibles. Les clients, les partenaires d’Adobe, les agences et les fournisseurs de technologies publicitaires et marketing peuvent créer une extension de balise qui ajoute de nouvelles fonctionnalités ou qui modifie les fonctionnalités existantes. Le système permet aux partenaires et aux clients de créer, gérer et mettre à jour leurs propres intégrations. Ce n’est qu’une façon pour Adobe d’ouvrir Adobe Experience Platform aux clients et aux partenaires afin qu’ils puissent s’en servir de base pour leurs produits et entreprises. Cela permet à tous les utilisateurs de connecter plus facilement la technologie Adobe aux technologies marketing et publicitaires d’autres fournisseurs.

## Toutes les extensions tierces seront-elles disponibles immédiatement ?

Les extensions sont déjà disponibles pour les solutions Adobe et pour un nombre important et sans cesse croissant de fournisseurs et de technologies d’analyse, de marketing, de publicité et de consentement indépendants. Nous continuons de travailler avec nos partenaires pour étendre l’écosystème. Dans la mesure où les extensions peuvent être développées, gérées et mises à jour par les propriétaires de technologie, les clients n’ont pas besoin d’attendre que l’ingénierie Adobe les développe.

## Quand les clients ou les partenaires peuvent-ils développer des extensions ?

La fonctionnalité Balises a ouvert son portail en libre-service, que les développeurs d’extensions peuvent utiliser pour créer leurs propres intégrations avec Adobe Cloud Platform.

Nous avons de nombreux clients qui choisissent également de développer leurs propres extensions privées pour les utiliser uniquement dans leurs propres entreprises en utilisant les mêmes méthodes de développement d’extension.

Pour développer une extension, consultez la page [Présentation du développement d’extension](./extension-dev/overview.md).

## Les balises sont-elles conformes aux normes de sécurité de ma société ?

Les balises sont certifiées SOC-2 et conformes à la loi Gramm-Leach-Bliley Act. Les balises offrent également la possibilité d’être auto-hébergées. Les bibliothèques JavaScript ainsi que les configurations mobiles peuvent être traitées à partir de vos propres serveurs ou du réseau CDN de votre choix. Cela permet aux équipes informatiques et de sécurité d’exécuter des tests automatisés, de vérifier les fichiers dans leur propre système de contrôle de versions et de se conformer pleinement aux processus de migration de production internes, liés à la sécurité ou autres.

## Quand puis-je migrer vers les balises ?

C’est maintenant le meilleur moment pour migrer vers les balises. Le processus de migration facilite la copie de vos propriétés DTM dans les balises. Nous recommandons des tests approfondis, mais nous avons automatisé autant de processus que possible (aucun changement de code incorporé sur la page, et migration automatisée des règles et des éléments de données).

## Les balises prennent-elles en charge les applications monopage et mon framework préféré ?

Oui. Les balises disposent de fonctionnalités permettant aux utilisateurs et aux développeurs d’extensions de disposer de davantage de flexibilité pour collecter, gérer et distribuer des données au sein d’applications monopages ou de sites et pages à utilisation lourde Ajax. Cela s’applique quelles que soient vos préférences de structure de développement, que ce soit Angular, React.js, Ember, Meteor, etc.

## Les balises prennent-elles en charge les couches de données dynamiques ?

Oui. Les balises incluent une extension spécialisée dans l’écoute des modifications des couches de données dynamiques.

## Quels types dʼévénements les balises prennent-elles en charge ?

Les types d’événements sont disponibles via les extensions. Le nombre de types d’événement pris en charge varie en fonction de l’extension. Par exemple, l’extension YouTube inclut quatre types d’événements vidéo : play, pause, end et time played. Grâce aux extensions, les balises prennent en charge tout autre type d’événements de navigateur ou de synthèse, tel que des séquences d’activité de visiteurs spécifiques.

## Les balises vont-elles accélérer (ou ralentir) mon site web ?

Les balises sont conçues pour fournir et exécuter des technologies publicitaires et marketing sur votre site web aussi efficacement que possible en appliquant les bonnes pratiques actuelles. Il a été démontré que lorsqu’elles sont utilisées correctement, les balises améliorent les performances des sites web par rapport à d’autres méthodes offrant des fonctionnalités similaires.

## Quels navigateurs les balises prennent-elles en charge ?

Consultez les navigateurs [ici](./extension-dev/browsers.md) pris en charge.

La plupart des clients exploitent désormais des fonctionnalités de plateforme web plus modernes dans les navigateurs actuels et génèrent de meilleures expériences utilisateur, y compris des applications d’une seule page et des sites web et pages interactifs à utilisation lourde Ajax. Comme la plupart des clients optent pour des approches plus modernes de leurs sites, ils ont besoin d’une solution comme Balises permettant ces approches.

## Les balises fonctionnent-elles sur les applications mobiles natives ?

Oui! Balises prend désormais en charge les propriétés et la configuration des nouveaux [SDK mobiles](https://sdkdocs.com) d’Adobe Experience Platform pour mettre en œuvre la collecte et la diffusion de données dans un environnement d’application nativement mobile. Veuillez consulter la [documentation](https://sdkdocs.com) pour en savoir plus.

## Pourquoi l’interface utilisateur indique-t-elle qu’une erreur s’est produite lors du chargement de mon compte ?

Si vous recevez un message indiquant qu’une erreur s’est produite lors du chargement de votre compte, cela signifie que votre compte n’appartient à aucun profil de produit pour les balises. Consultez le guide sur la [gestion des autorisations](../collection/permissions.md) pour savoir comment configurer un profil de produit dans Adobe Admin Console pour accorder l’accès aux fonctionnalités de collecte de données dans l’interface utilisateur.

## Pourquoi m’est-il impossible d’ajouter des propriétés dans l’interface utilisateur ?

Si vous ne pouvez pas créer de propriétés lors de la connexion à l’interface utilisateur, cela signifie que votre compte n’appartient pas à un profil de produit disposant du droit Manage Properties (Gérer les propriétés).

Consultez le guide sur la [gestion des autorisations](../collection/permissions.md) pour savoir comment configurer un profil de produit dans Adobe Admin Console de manière à octroyer le droit Gérer les propriétés. Pour plus d’informations sur les différents droits relatifs aux balises, consultez la présentation des [autorisations d’utilisateur pour les balises](./ui/administration/user-permissions.md).

## Et si j’ai d’autres questions ?

Si vous avez d’autres questions, vous pouvez poser la question sur la [page de la communauté de collecte de données Adobe Experience Platform](https://adobe.com/go/launchme) sur Experience League ou rejoindre l’ [&#x200B; espace de travail du Slack de communauté](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform) pour les développeurs et les rubriques de mise en oeuvre technique.
