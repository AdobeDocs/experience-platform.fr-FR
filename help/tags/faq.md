---
title: FAQ
description: Obtenez des réponses aux questions fréquentes sur les balises dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 30%

---

# Guide de dépannage des balises

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](./term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Ce document répond aux questions les plus fréquemment posées sur les balises dans Adobe Experience Platform.

## Que sont les balises ?

Les balises représentent la nouvelle génération des fonctionnalités de gestion des balises fournies par Adobe, intégrées à Adobe Experience Platform. Les balises permettent aux clients de :

- déployer des produits web côté client grâce à des intégrations appelées *extensions*
- fournir dynamiquement la configuration pour mettre à jour les implémentations des clients dans les applications mobiles natives
- collecter, définir, gérer et partager des données de façon constante entre les produits marketing et publicitaires d’autres fournisseurs et d’Adobe.

Les balises sont un système de diffusion de code et de configuration avancé qui évalue les conditions et exécute des actions pour déployer les bibliothèques et produits côté client de manière efficace. Ils offrent également une approche hautement évolutive de la gestion et de la création des intégrations et disposent d’un solide ensemble d’API pour l’interaction programmatique.

## Combien coûtent les balises ?

Les balises sont gratuites. Ils sont disponibles pour tous les clients [!DNL Adobe Experience Cloud].

## J’ai appris qu’il existe désormais des modules externes. De quoi s’agit-il ?

Les balises sont intégrées à Adobe Experience Platform et sont entièrement extensibles. Les clients, les partenaires d’Adobe, les agences et les fournisseurs de technologies publicitaires et marketing peuvent créer une extension de balise qui ajoute de nouvelles fonctionnalités ou modifie les fonctionnalités existantes. Le système permet aux partenaires et aux clients de créer, gérer et mettre à jour leurs propres intégrations. Il s’agit d’une manière d’ouvrir Adobe Experience Platform afin que les clients et les partenaires puissent y développer des produits et des entreprises. Cela permet à tous les utilisateurs de connecter plus facilement la technologie Adobe aux technologies marketing et publicitaires d’autres fournisseurs.

## Toutes les extensions tierces seront-elles disponibles immédiatement ?

Les extensions sont déjà disponibles pour les solutions Adobe et un nombre important et croissant de fournisseurs et de technologies d’analyse, de marketing, de publicité et de consentement indépendants. Nous continuons de travailler avec nos partenaires pour étendre l’écosystème. Les extensions pouvant être créées, gérées et mises à jour par les propriétaires de technologie, les clients n’ont pas à attendre que l’ingénierie d’Adobe les développe.

## Quand les clients ou les partenaires peuvent-ils développer des extensions ?

Les balises ont ouvert son portail en libre-service ou presque, que les développeurs d’extensions peuvent utiliser pour créer leurs propres intégrations avec Adobe Cloud Platform.

Nous avons de nombreux clients qui choisissent également de développer leurs propres extensions privées pour les utiliser uniquement dans leurs propres entreprises en utilisant les mêmes méthodes de développement d’extension.

## Les balises sont-elles conformes aux normes de sécurité de mon entreprise ?

Les balises sont certifiées SOC-2 et Gramm-Leach-Bliley Act prêtes. Les balises offrent également la possibilité d’être auto-hébergées. Les bibliothèques JavaScript et les configurations mobiles peuvent être diffusées à partir de vos propres serveurs ou du réseau de diffusion de contenu de votre choix. Cela permet aux équipes informatiques et de sécurité d’exécuter des tests automatisés, de vérifier les fichiers dans leur propre système de contrôle de versions et de se conformer pleinement aux processus de migration de production internes, liés à la sécurité ou autres.

## Quand puis-je passer aux balises ?

C’est le meilleur moment pour passer aux balises. Le processus de migration facilite la copie des propriétés de la gestion dynamique des balises dans les balises. Nous recommandons des tests approfondis, mais nous avons automatisé autant de processus que possible (aucun changement de code incorporé sur la page, et migration automatisée des règles et des éléments de données).

## Les balises prennent-elles en charge les applications d’une seule page et mon framework préféré ?

Oui. Les balises offrent la possibilité aux utilisateurs et aux développeurs d’extensions de collecter, gérer et distribuer des données dans le cadre d’expériences d’application d’une seule page ou de sites très lourds Ajax. Cela s’applique quelles que soient vos préférences de structure de développement, que ce soit Angular, React.js, Ember, Meteor, etc.

## Les balises prennent-elles en charge les couches de données dynamiques ?

Oui. Les balises comprennent une extension spécialisée dans l’écoute des modifications des couches de données dynamiques.

## Quels types d’événement les balises prennent-elles en charge ?

Les types d’événements sont disponibles via les extensions. Le nombre de types d’événement pris en charge varie en fonction de l’extension. Par exemple, l’extension YouTube inclut quatre types d’événements vidéo : play, pause, end et time played. Grâce aux extensions, les balises peuvent prendre en charge tout autre type d’événement de navigateur ou de synthèse, tel que des séquences d’activité de visiteur spécifiques.

## Les balises vont-elles accélérer (ou ralentir) mon site web ?

Les balises sont conçues pour fournir et exécuter des technologies publicitaires et marketing sur votre site web aussi efficacement que possible à l’aide des bonnes pratiques actuelles. Lorsqu’elles sont utilisées correctement, les balises ont démontré qu’elles améliorent les performances des sites web par rapport à d’autres méthodes offrant des fonctionnalités similaires.

## Quels navigateurs les balises prennent-elles en charge ?

Prise en charge des navigateurs pour les balises :

- [!DNL Chrome] (version la plus récente)
- [!DNL Safari] (version la plus récente)
- [!DNL Firefox] (version la plus récente)
- [!DNL Microsoft Edge] (version la plus récente)
- [!DNL Internet Explorer] (version 10 et supérieure)
- [!DNL iOS Safari] (version la plus récente)
- [!DNL Android Chrome] (version la plus récente)

Prise en charge du navigateur pour l’interface de l’application de balises :

- [!DNL Chrome] (version la plus récente)
- [!DNL Safari] (version la plus récente)
- [!DNL Firefox] (version la plus récente)
- [!DNL Microsoft Edge] (version la plus récente)

La plupart des clients Adobe utilisent des fonctionnalités de plateforme web plus modernes dans les navigateurs actuels pour créer de meilleures expériences utilisateur, notamment des applications d’une seule page et des sites web et pages interactifs Ajax. La plupart des clients ayant recours à des approches plus modernes de leurs sites, ils ont besoin d’une solution telle que des balises qui permettent ces approches.

## Les balises fonctionnent-elles sur les applications mobiles natives ?

Oui! Les balises prennent désormais en charge les propriétés et la configuration mobiles des nouveaux [SDK mobiles de Adobe Experience Platform](https://sdkdocs.com) pour mettre en oeuvre la collecte et la diffusion de données dans un environnement d’application mobile natif. Veuillez consulter la [documentation](https://sdkdocs.com) pour en savoir plus.

## Et si j’ai d’autres questions ?

Si vous avez d’autres questions, contactez la communauté Adobe sur la page des balises principale située à l’adresse [https://adobe.com/go/launchme](https://adobe.com/go/launchme).

Les balises ne sont qu’un exemple parmi d’autres de la direction que prend notre plateforme : plus ouvert, plus intégré et, comme toujours, dédié au succès client.
