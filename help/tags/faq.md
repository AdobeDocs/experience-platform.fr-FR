---
title: Guide de dépannage des balises
description: Obtenez des réponses aux questions les plus fréquentes sur les balises dans Adobe Experience Platform.
source-git-commit: dc957372e5e8c6f034f2e0cd0283e0e997501ba8
workflow-type: ht
source-wordcount: '1055'
ht-degree: 100%

---

# Guide de dépannage des balises

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](./term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Ce document apporte des réponses aux questions fréquentes sur les balises dans Adobe Experience Platform.

## Que sont les balises ?

Les balises représentent la nouvelle génération des fonctionnalités de gestion des balises fournies par Adobe et intégrées à Adobe Experience Platform. Les balises offrent aux clients les fonctionnalités suivantes :

- déployer des produits web côté client grâce à des intégrations appelées *extensions*
- fournir dynamiquement la configuration pour mettre à jour les implémentations des clients dans les applications mobiles natives
- collecter, définir, gérer et partager des données de façon constante entre les produits marketing et publicitaires d’autres fournisseurs et d’Adobe.

Les balises sont un système de diffusion de code et de configuration avancé qui évalue les conditions et exécute des actions pour déployer les bibliothèques et produits côté client de façon efficace. Elles offrent également une approche hautement évolutive de la gestion et de la création des intégrations et disposent dʼun ensemble robuste dʼAPI pour lʼinteraction programmatique.

## Combien coûtent les balises ?

Les balises nʼentraînent aucuns frais supplémentaires. Elles sont disponibles pour tous les clients dʼ[!DNL Adobe Experience Cloud].

## J’ai appris qu’il existe désormais des modules externes. De quoi s’agit-il ?

Les balises sont intégrées à Adobe Experience Platform et sont totalement extensibles. Les clients, les partenaires dʼAdobe, les agences et les fournisseurs de technologies publicitaires ou marketing peuvent créer une extension de balise qui ajoute de nouvelles fonctionnalités ou modifie les fonctionnalités existantes. Le système permet aux partenaires et aux clients de créer, gérer et mettre à jour leurs propres intégrations. Ce nʼest quʼune façon pour Adobe dʼouvrir Adobe Experience Platform aux clients et aux partenaires afin quʼils puissent sʼen servir pour leurs produits et entreprises. Cela permet à tous les utilisateurs de connecter plus facilement la technologie Adobe aux technologies marketing et publicitaires d’autres fournisseurs.

## Toutes les extensions tierces seront-elles disponibles immédiatement ?

Les extensions sont déjà disponibles pour les solutions Adobe et un nombre important et croissant de fournisseurs et de technologies dʼanalyse, de marketing, de publicité et de consentement indépendants. Nous continuons de travailler avec nos partenaires pour étendre l’écosystème. Dans la mesure où les extensions peuvent être développées, gérées et mises à jour par les propriétaires de technologie, les clients nʼont pas besoin dʼattendre que lʼingénierie dʼAdobe les développe.

## Quand les clients ou les partenaires peuvent-ils développer des extensions ?

Les balises ont ouvert leur portail virtuel en libre-service, que les développeurs dʼextensions peuvent utiliser pour créer leurs propres intégrations à Adobe Cloud Platform.

Nous avons de nombreux clients qui choisissent également de développer leurs propres extensions privées pour les utiliser uniquement dans leurs propres entreprises en utilisant les mêmes méthodes de développement d’extension.

## Les balises sont-elles conformes aux normes de sécurité de ma société ?

Les balises possèdent la certification SOC-2 et sont conformes à la loi Gramm-Leach-Bliley. Les balises offrent également la possibilité dʼêtre auto-hébergées. Les bibliothèques JavaScript et les configurations mobiles peuvent être diffusées à partir de vos propres serveurs ou du réseau de diffusion de contenu (CDN) de votre choix. Cela permet aux équipes informatiques et de sécurité d’exécuter des tests automatisés, de vérifier les fichiers dans leur propre système de contrôle de versions et de se conformer pleinement aux processus de migration de production internes, liés à la sécurité ou autres.

## À quelle date puis-je migrer vers les balises ?

Cʼest le meilleur moment pour migrer vers les balises. Le processus de migration facilite la copie de vos propriétés DTM dans des balises. Nous recommandons des tests approfondis, mais nous avons automatisé autant de processus que possible (aucun changement de code incorporé sur la page, et migration automatisée des règles et des éléments de données).

## Les balises prennent-elles en charge les applications monopage et mon framework préféré ?

Oui. Les balises disposent de fonctionnalités permettant aux utilisateurs et aux développeurs dʼextensions de disposer de davantage de flexibilité pour collecter, gérer et distribuer des données au sein dʼapplications monopage ou de sites et pages à utilisation intensive Ajax. Cela s’applique quelles que soient vos préférences de structure de développement, que ce soit Angular, React.js, Ember, Meteor, etc.

## Les balises prennent-elles en charge les couches de données dynamiques ?

Oui. Les balises incluent une extension spécialisée dans lʼécoute des modifications des couches de données dynamiques.

## Quels types dʼévénements les balises prennent-elles en charge ?

Les types d’événements sont disponibles via les extensions. Le nombre de types dʼévénements pris en charge varie en fonction de lʼextension. Par exemple, l’extension YouTube inclut quatre types d’événements vidéo : play, pause, end et time played. Grâce aux extensions, les balises peuvent prendre en charge tout autre type dʼévénements de navigateur ou de synthèse, tels que des séquences dʼactivité de visiteurs spécifiques.

## Les balises vont-elles accélérer (ou ralentir) mon site web ?

Les balises sont conçues pour fournir et exécuter des technologies publicitaires et marketing sur votre site web aussi efficacement que possible en appliquant les bonnes pratiques actuelles. Lorsquʼelles sont utilisées correctement, les balises ont démontré quʼelles améliorent les performances des sites web par rapport à dʼautres méthodes offrant des fonctionnalités similaires.

## Quels navigateurs les balises prennent-elles en charge ?

Les balises prennent en charge les navigateurs suivants :

- [!DNL Chrome] (version la plus récente)
- [!DNL Safari] (version la plus récente)
- [!DNL Firefox] (version la plus récente)
- [!DNL Microsoft Edge] (version la plus récente)
- [!DNL Internet Explorer] (version 10 et supérieure)
- [!DNL iOS Safari] (version la plus récente)
- [!DNL Android Chrome] (version la plus récente)

Lʼinterface dʼapplication des balises prend en charge les navigateurs suivants :

- [!DNL Chrome] (version la plus récente)
- [!DNL Safari] (version la plus récente)
- [!DNL Firefox] (version la plus récente)
- [!DNL Microsoft Edge] (version la plus récente)

La plupart des clients dʼAdobe exploitent des fonctionnalités de plateforme web plus modernes dans les navigateurs actuels afin de créer de meilleures expériences utilisateur, y compris des applications monopage et des sites web et pages à utilisation intensive Ajax. Comme la plupart des clients optent pour des approches plus modernes de leurs sites, ils ont besoin dʼune solution comme les balises qui permet ces approches.

## Les balises fonctionnent-elles sur les applications mobiles natives ?

Oui! Les balises prennent désormais en charge les propriétés et la configuration mobiles des nouveaux [SDK mobiles](https://sdkdocs.com) Adobe Experience Platform pour implémenter la collecte et la diffusion de données dans un environnement dʼapplication mobile natif. Veuillez consulter la [documentation](https://sdkdocs.com) pour en savoir plus.

## Pourquoi l’interface utilisateur indique-t-elle qu’une erreur s’est produite lors du chargement de mon compte ?

Si vous recevez un message indiquant qu’une erreur s’est produite lors du chargement de votre compte, cela signifie que votre compte n’appartient à aucun profil de produit pour les balises. Consultez le guide sur la [gestion des autorisations](./ui/administration/manage-permissions.md) pour savoir comment configurer un profil de produit dans Adobe Admin Console de manière à octroyer l’accès à l’interface utilisateur de la collecte de données.

## Pourquoi m’est-il impossible d’ajouter des propriétés dans l’interface utilisateur ?

Si vous ne pouvez pas créer de propriété lorsque vous êtes connecté à l’interface utilisateur de la collecte de données, cela signifie que votre compte n’appartient pas à un profil de produit disposant du droit Gérer les propriétés.

Consultez le guide sur la [gestion des autorisations](./ui/administration/manage-permissions.md) pour savoir comment configurer un profil de produit dans Adobe Admin Console de manière à octroyer le droit Gérer les propriétés. Pour plus d’informations sur les différents droits relatifs aux balises, consultez la présentation des [autorisations d’utilisateur pour les balises](./ui/administration/user-permissions.md).

## Et si j’ai d’autres questions ?

Si vous avez dʼautres questions, contactez la communauté Adobe sur la page principale dédiée aux balises située à cette adresse [https://adobe.com/go/launchme](https://adobe.com/go/launchme).

Les balises ne sont quʼun exemple parmi dʼautres de la direction que prend notre plateforme : plus ouverte, plus intégrée et, comme toujours, vouée au succès de nos clients.
